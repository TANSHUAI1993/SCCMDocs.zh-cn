---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 iOS 和 Mac 混合设备管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 iOS 设备管理。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 1a93a542f55d02df20865fa4ae8d7590dd9be753
ms.contentlocale: zh-cn
ms.lasthandoff: 07/29/2017

---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>设置 iOS 混合使用 System Center Configuration Manager 和 Microsoft Intune 的设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

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
4.  单击“浏览” 并转到“从 Apple 下载的 APNs 证书(.cer)文件”。 Configuration Manager 会显示 APNs 证书信息。 单击“确定”  ，将 APNs 证书保存到 Intune。  

> [!NOTE]
> “注册限制”功能此时不可用。 

> [!div class="button"]
[< 上一步](create-service-connection-point.md)  [下一步 >](set-up-additional-management.md)

