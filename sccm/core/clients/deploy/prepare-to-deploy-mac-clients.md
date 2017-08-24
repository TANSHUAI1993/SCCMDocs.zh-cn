---
title: "将客户端软件部署到 Mac 的准备工作 | Microsoft Docs"
description: "将 Configuration Manager 客户端部署到 Mac 计算机前的配置任务。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3bb72f81812705b4654e268025074402e89a7cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>将客户端软件部署到 Mac 的准备工作

*适用范围：System Center Configuration Manager (Current Branch)*

按照下列步骤，确保你已准备好[将 Configuration Manager 客户端部署到 Mac 计算机](/sccm/core/clients/deploy/deploy-clients-to-macs)。 

## <a name="mac-prerequisites"></a>Mac 先决条件

Mac 客户端安装包未与 Configuration Manager 媒体一同提供。 可从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载**适用于其他操作系统的客户端**。  

**支持的版本：**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

## <a name="certificate-requirements"></a>证书要求
在 Mac 计算机上安装和管理客户端需要公钥基础结构 (PKI) 证书。 PKI 证书通过使用手动身份验证和加密的数据传输来保护 Mac 计算机和 Configuration Manager 站点之间的通信的安全。 Configuration Manager 可通过将 Microsoft 证书服务与企业证书颁发机构 (CA)、Configuration Manager 注册点和注册代理点站点系统角色一起使用，从而请求和安装用户客户端证书。 或者，如果证书满足 Configuration Manager 的要求，你可以独立于 Configuration Manager 请求和安装计算机证书。   
  
Configuration Manager Mac 客户端始终执行证书吊销检查。 不能禁用此功能。  
  
如果 Mac 客户端由于无法找到 CRL 而无法确认服务器证书的证书吊销状态，它们将无法成功连接到 Configuration Manager 站点系统。 特别是，对于所在的林与证书颁发机构不同的 Mac 客户端，请检查你的 CRL 设计以确保 Mac 客户端可找到并连接到 CRL 分发点 (CDP) 以便连接站点系统服务器。  

在 Mac 计算机上安装 Configuration Manager 客户端之前，请决定安装客户端证书的方式：  

-   通过使用 [CMEnroll 工具](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac)注册 Configuration Manager。 注册过程不支持自动证书续订，因此你必须在安装的证书过期之前重新注册 Mac 计算机。  

-   [使用与 Configuration Manager 无关的证书请求和安装方法](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager)。  

有关 Mac 客户端证书要求和支持 Mac 计算机所需的其他 PKI 证书的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

会自动将 Mac 客户端分配给对其进行管理的 Configuration Manager 站点。 即使仅与 Intranet 通信，Mac 客户端也将安装为仅 Internet 的客户端。 这种客户端配置意味着，当你将为客户端分配的站点中的站点系统角色（管理点和分发点）配置为允许来自 Internet 的客户端连接时，它们只会与这些站点系统角色通信。 Mac 计算机不会与为其分配的站点范围外的站点系统角色通信。  

> [!IMPORTANT]  
>  Configuration Manager Mac 客户端不能用于连接到配置为使用[数据库副本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)的管理点。  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>将 Web 服务器证书部署到站点系统服务器  
如果这些站点系统不具有 Web 服务器证书，请将该证书部署到具有这些站点系统角色的计算机：  

-   管理点  

-   分发点  

-   注册点  

-   注册代理点  

Web 服务器证书必须包含在站点系统属性中指定的 Internet FQDN。 但不可通过 Internet 访问的服务器也支持 Mac 计算机。 如果不需要基于 Internet 的客户端管理，你可以为 Internet FQDN 指定 Intranet FQDN 值。  

可在管理点、分发点和注册代理点的 Web 服务器证书中指定站点系统的 Internet FQDN 值。 

有关创建和安装此 Web 服务器证书的部署示例，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>将客户端身份验证证书部署到站点系统服务器  
 如果这些站点系统没有客户端身份验证证书，请向托管以下站点系统角色的计算机部署客户端身份验证证书：  

-   管理点  

-   分发点  

 有关创建和安装管理点的客户端证书的示例部署，请参阅[为 Windows 计算机部署客户端证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 有关创建和安装分发点的客户端证书的示例部署，请参阅[为分发点部署客户端证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)。  

>[!IMPORTANT]
>  若要将客户端部署到运行 macOS Sierra 的设备上，必须正确配置管理点证书的使用者名称（例如，使用管理点服务器的 FQDN）。

## <a name="prepare-the-client-certificate-template-for-macs"></a>为 Mac 准备客户端证书模板  

 对于将在 Mac 计算机上注册证书的用户帐户，证书模板必须具有“读取”  和“注册”  权限。  

 请参阅[部署 Mac 计算机的客户端证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)。  

## <a name="configure-the-management-point-and-distribution-point"></a>配置管理点和分发点  
 为下列选项配置管理点：  

-   HTTPS  

-   允许来自 Internet 的客户端连接。 管理 Mac 计算机需要该配置值。 但是，它并不意味着站点系统服务器必须可从 Internet 中访问。  

-   允许移动设备和 Mac 计算机使用此管理点  

 尽管安装客户端无需分发点，但是，如果要在安装客户端之后将软件部署到这些计算机，则必须配置分发点以允许来自 Internet 的客户端连接。  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>配置管理点和分发点以支持 Mac  

在开始此过程之前，请确保运行管理点和分发点的站点系统服务器配置为包含 Internet FQDN。 如果这些服务器不支持基于 Internet 的客户端管理，则可以将 Intranet FQDN 指定为 Internet FQDN 值。 

这些站点系统角色必须位于主站点中。  


1.  在 Configuration Manager 控制台中，选择“管理” > “站点配置” > “服务器和站点系统角色”，然后选择拥有正确站点系统角色的服务器。  

3.  在“详细信息”窗格中，右键单击“管理点”，选择“角色属性”，并在“管理点属性”对话框中配置这些选项：  

    1.  选择“HTTPS”。  

    2.  选择“仅允许 Internet 客户端连接”或“允许 Intranet 和 Internet 客户端连接”。 这些选项需要 Internet 或 Intranet FQDN。  

    3.  选择“允许移动设备和 Mac 计算机使用此管理点”。  

4.  在“详细信息”窗格中，右键单击“分发点”，选择“角色属性”，并在“分发点属性”对话框中配置这些选项：  

    -   选择“HTTPS”。  

    -   选择“仅允许 Internet 客户端连接”或“允许 Intranet 和 Internet 客户端连接”。 这些选项需要 Internet 或 Intranet FQDN。  

    -   选择“导入证书”，浏览到导出的客户端分发点证书文件，然后指定密码。  

5.  对将用于 Mac 的主站点中的所有管理点和分发点重复步骤 2 至 4。  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>配置注册代理点和注册点  
 你必须在同一站点中安装这两个站点系统角色，但不必将它们安装在同一站点系统服务器上或同一 Active Directory 林中。  

 有关站点系统角色布局和注意事项的详细信息，请参阅[为 System Center Configuration Manager 规划站点系统服务器和站点系统角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)中的[站点系统角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)。  

 这些过程配置站点系统角色以支持 Mac 计算机。   

-   [新建站点系统服务器](#new-site-system-server)  

-   [现有站点系统服务器](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>新建站点系统服务器  

1.  在 Configuration Manager 控制台中，选择“管理” >  “站点配置” > “服务器和站点系统角色”  

3.  在“主页”选项卡上的“创建”组中，选择“创建站点系统服务器”。  

4.  在“常规”页上，指定站点系统的常规设置。  请确保为 Internet FQDN 指定值。 如果不能从 Internet 中访问服务器，请使用 Intranet FQDN。  

5.  在“系统角色选择”页上，从可用角色列表中选择“注册代理点”和“注册点”。  

6.  在“注册代理点”页上，查看设置并进行任何必要的更改。  

7.  在“注册点设置”页上，查看设置并进行任何必要的更改。 然后完成该向导。  

### <a name="existing-site-system-server"></a>现有站点系统服务器  

1.  在 Configuration Manager 控制台中，选择“管理” >  “站点配置” > “服务器和站点系统角色”，然后选择要用于支持 Mac 的服务器。  

3.  在“主页”选项卡上的“创建”组中，选择“添加站点系统角色”。  

4.  在“常规”  页上，指定站点系统的常规设置，然后单击“下一步” 。 请确保为 Internet FQDN 指定值。 如果不能从 Internet 中访问服务器，请使用 Intranet FQDN。   

5.  在“系统角色选择”页上，从可用角色列表中选择“注册代理点”和“注册点”。  

6.  在“注册代理点”页上，查看设置并进行任何必要的更改。  

7.  在“注册点设置”页上，查看设置并进行任何必要的更改。 然后完成该向导。  

## <a name="install-the-reporting-services-point"></a>安装 Reporting Services 点  
 如果要为 Mac 运行报表，请[安装 Reporting Services 点](../../../core/servers/manage/configuring-reporting.md)。  

### <a name="next-steps"></a>后续步骤

[将 Configuration Manager 客户端部署到 Mac 计算机](/sccm/core/clients/deploy/deploy-clients-to-macs)。  