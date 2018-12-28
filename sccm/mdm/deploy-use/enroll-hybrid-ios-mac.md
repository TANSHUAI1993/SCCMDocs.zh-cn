---
title: 使用 Microsoft Intune 设置 iOS 和 Mac 混合设备管理
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager 和 Microsoft Intune 设置 iOS 设备管理。
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1357c54b0f848374ea15727bb6265f68400f88c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422362"
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>设置 iOS 混合使用 System Center Configuration Manager 和 Microsoft Intune 的设备管理

*适用于：System Center Configuration Manager (Current Branch)*

利用 Configuration Manager 和 Intune，可以启用 iOS 和 macOS 设备注册，以允许 iPhone、iPad 和 Mac 用户访问公司电子邮件和资源。 用户安装 Intune 公司门户应用后，即可向其设备应用策略。 你必须先从 Apple 导入 Apple Push Notification 服务 (APNs) 证书，然后才能管理 iOS 和 Mac 设备。 此证书允许 Intune 通过建立与 Apple 设备管理服务的连接来管理 iOS 和 Mac 设备。  

 还可注册企业所有的 iOS 设备。  请参阅[注册公司拥有的设备](enroll-company-owned-devices.md)。  

**先决条件**<br>
在为任何平台设置注册前，必须先完成[设置混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。

要支持 iOS 设备注册，必须执行以下步骤：  

## <a name="download-a-certificate-signing-request"></a>下载证书签名请求
需要证书签名请求文件来请求 Apple 的 APNs 证书。  

1.  在 Configuration Manager 控制台中的“管理”工作区中，转到“云服务”> “Microsoft Intune 订阅”。  

2.  在“主页”  选项卡上，单击“创建 APNs 证书请求” 。 “请求 Apple Push Notification 服务证书签名请求”  对话框随即打开。  

3.  “浏览”到要保存新的证书签名请求文件的路径。 本地保存证书签名请求文件。  

4.  单击“下载” 。 下载新的 Microsoft Intune 证书签名请求文件，并由 Configuration Manager 保存。 证书签名请求文件用于从 Apple Push Certificates 门户请求信任关系证书。  

## <a name="request-an-mdm-push-certificate-from-apple"></a>请求 Apple 的 MDM Push Certificate
MDM Push Certificate 用于在管理服务、Intune 和注册的 iOS 移动设备之间建立信任关系。  

1.  在浏览器中，转到 [Apple Push Certificates 门户](http://go.microsoft.com/fwlink/?LinkId=269844) 并使用贵公司 Apple ID 登录。 若要续订 APN 证书，必须在将来使用此 Apple ID。  

2.  使用证书签名请求 (.csr) 文件完成向导。 下载 MDM Push Certificate 并在本地保存 pem 文件。 此证书 (.pem) 文件用于在 Apple 推送通知服务器和 Intune 的移动设备管理机构之间建立信任关系。  

> [!NOTE]  
>  在 Configuration Manager 控制台中启用 iOS 注册之前，请不要将 Apple Push Notification 服务 (APN) 证书上传到 Intune。  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>启用注册并上传 MDM Push Certificate
启用 iOS 注册，上传 APNs 证书。  

1.  在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。  

2.  在“主页”选项卡上的“订阅”组中，单击“配置平台” > “iOS”。  

3.  在“Microsoft Intune 订阅属性”  对话框中，选择“iOS”  选项卡并单击选择“启用 iOS 注册”  复选框。  
4.  单击“浏览” 并转到“从 Apple 下载的 APNs 证书(.cer)文件”。 Configuration Manager 会显示 APNs 证书信息。 单击“确定”，将 APN 证书保存到 Intune。  

设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/end-user-educate)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。

## <a name="configure-enrollment-restrictions"></a>配置注册限制

可以阻止个人拥有的设备，从而限制能够注册的设备。 这样可防止用户使用公司门户注册自己的设备。 如果阻止个人拥有的设备，只能注册以下设备：
- [预声明设备](predeclare-devices-with-hardware-id.md)
- [Apple Configurator 管理设备](ios-hybrid-enrollment-using-apple-configurator.md)
- [设备注册计划 (DEP) 管理设备](ios-device-enrollment-program-for-hybrid.md)
- 使用[设备注册管理器帐户](enroll-devices-with-device-enrollment-manager.md)注册的设备

### <a name="to-enable-enrollment-restrictions"></a>启用注册限制的具体步骤
1.  在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。
2.  在“主页”选项卡上的“订阅”组中，单击“配置平台” > “iOS”。
3.  选择“阻止个人拥有的设备”，限制为仅注册公司拥有的设备。

> [!div class="button"]
> [< 上一步](create-service-connection-point.md)  [下一步 >](set-up-additional-management.md)
