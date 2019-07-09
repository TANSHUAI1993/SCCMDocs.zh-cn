---
title: Azure AD 身份验证工作流
titleSuffix: Configuration Manager
description: 在具有 Azure Active Directory 身份验证的 Windows 10 设备上安装 Configuration Manager 客户端过程的详细信息
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8bb386aea70253fa033f59ab85732e0b99987c16
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550965"
---
# <a name="azure-ad-authentication-workflow"></a>Azure AD 身份验证工作流

适用范围：  System Center Configuration Manager (Current Branch)

本文是有关在连接到 Azure Active Directory (Azure AD) 的 Windows 10 设备上安装 Configuration Manager 客户端的技术参考。 它详细说明了设备身份验证和客户端安装的工作流过程。  
 

## <a name="azure-ad-token-request-workflow"></a>Azure AD 令牌请求工作流

![Azure AD CCMSetup 工作流关系图](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1.Azure AD 令牌请求

Windows 10 Azure AD 已加入域的客户端使用 Azure AD 参数来请求令牌。 下列条目将被记录到 ccmsetup.log  ：

- 请求 Azure AD 设备令牌：

    ```
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- 如果无法获取设备令牌，它将请求 Azure AD 用户令牌：

    ```
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> 加入 Azure AD 时，客户端应获取工作区加入 (WPJ) 证书。 如果找不到工作区加入证书，客户端不会尝试使用安全令牌服务通信通道 (CCM_STS) 创建请求。 此行为是因为客户端不能将 Azure AD 令牌添加到请求。 当客户端未正确加入到 Azure AD，设备通常没有此证书。
>
> 此外，如果令牌无效，云管理网关 (CMG) 不会将请求转发到内部站点角色。 如果租户未注册为 Configuration Manager 中的云管理服务，该令牌可能无效。


### <a name="2-configuration-manager-client-token-request"></a>2.Configuration Manager 客户端令牌请求

一旦客户端获取 Azure AD 令牌，它将请求 Configuration Manager 客户端 (CCM) 令牌。

下列条目将被记录到 CMG 虚拟机的 ccmsetup.log  ：

```
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 CMG 获取请求

下列条目将被记录到 IIS.log  ：

```
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 CMG 将请求转发到 CMG 连接点

下列条目将被记录到 CMGService.log  ：

```
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 CMG 连接点将 CMG 客户端请求转换为管理点客户端请求

以下条目将被记录到 SMS_CLOUD_PROXYCONNECTOR.log  ：

```
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 管理点会验证站点数据库中的用户令牌

下列条目将被记录到 CCM_STS.log  ：

```
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>内容位置请求

一旦客户端使用 CCM 令牌获得响应，它将缓存并使用它通过 CMG 请求站点信息和内容位置。 下列条目将被记录到 ccmsetup.log  ：

```
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>客户端安装

设备将下载客户端内容并开始安装。

### <a name="communication-validation"></a>通信验证

- CMG 通过 CMG、CMG 连接点和 HTTP(S) 以及管理点数据库请求验证客户端令牌。
- 客户端会验证 CMG 服务证书或管理证书
- CMG 服务证书的 PKI：客户端需要本地存储的 CMG 证书的根证书颁发机构 (CA)
- 第三方 CMG 服务证书：客户端会自动验证证书，并将其根 CA 发布到 Internet


## <a name="common-issues"></a>常见问题

- 不存在根 CA
- 启用了 CRL 检查：在 Internet 上发布 CRL 或在命令行中使用 /NoCRLcheck  选项
- 找不到 WPJ 证书：客户端已在 Azure AD 中注册，但未加入到 Azure AD

使用 /NoCRLCheck 仅适用于启动 ccmsetup。 为了使客户端能够完全正常工作，应在 Internet 上发布 CRL。 作为一种解决方法，可以在站点的客户端通信配置上禁用 CRL 检查。 否则，在位置服务刷新安全设置之后，客户端将停止与服务器通信。


## <a name="client-registration"></a>客户端注册

![Azure AD 注册工作流关系图](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1.Configuration Manager 客户端请求注册

ClientIDManagerStartup.log  记录下列条目：

```
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...        
Registering client using AAD auth.  
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2.Configuration Manager 请求获取用于注册客户端的 Azure AD 令牌

ADALOperationProvider.log  记录下列条目：
```
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000' 

```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 Configuration Manager 客户端已注册  

ClientIDManagerStartup.log  记录下列条目：

```
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3  
```

> [!NOTE]  
> 在客户端注册期间，证书验证始终运行。 即使要使用 Azure AD 身份验证方法注册客户端，也会发生此过程。


### <a name="3-configuration-manager-client-token-request"></a>3.Configuration Manager 客户端令牌请求

在站点注册客户端后，客户端便会请求获取 CCM 令牌。 CCM 令牌针对本地系统帐户 (S-1-5-18) 进行加密，并缓存 8 小时。 8 小时后，令牌到期，客户端请求令牌续订。

ClientIDManagerStartup.log  记录下列条目：

```
Getting CCM Token from STS server 'MP.MYCORP.COM'   
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'   
```

#### <a name="31-cmg-gets-request"></a>3.1 CMG 获取请求

下列条目将被记录到 IIS.log  ：

```
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 CMG 将请求转发到 CMG 连接点

下列条目将被记录到 CMGService.log  ：

```
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3 CMG 连接点将 CMG 客户端请求转换为管理点客户端请求

以下条目将被记录到 SMS_CLOUD_PROXYCONNECTOR.log  ：

```
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 管理点验证站点数据库中的用户令牌

下列条目将被记录到 CCM_STS.log  ：

```
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
