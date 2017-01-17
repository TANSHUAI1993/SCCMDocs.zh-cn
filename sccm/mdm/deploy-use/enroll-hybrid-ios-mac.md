---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 iOS 和 Mac 混合设备管理 | Microsoft Docs"
description: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 iOS 设备管理。"
ms.custom: na
ms.date: 10/06/2016
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
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 74c75653e69154ced18d5bc713b1d9b89e88ae64


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>设置 iOS 混合使用 System Center Configuration Manager 和 Microsoft Intune 的设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

利用 Configuration Manager 和 Intune，可以启用 BYOD（“自带设备办公”）iOS 和 Mac OS X 设备注册，以允许 iPhone、iPad 和 Mac 用户访问公司电子邮件和资源。 用户安装 Intune 公司门户应用后，即可向其设备应用策略。 你必须先从 Apple 导入 Apple Push Notification 服务 (APNs) 证书，然后才能管理 iOS 和 Mac 设备。 此证书使 Intune 可管理 iOS 和 Mac 设备并与移动设备管理机构服务建立公认和加密的 IP 连接。  

 还可注册企业所有的 iOS 设备。  请参阅[注册公司拥有的设备](enroll-company-owned-devices.md)。  

## <a name="enable-ios-device-enrollment"></a>启用 iOS 设备注册  
 要支持 iOS 设备注册，必须执行以下步骤：  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>在 Configuration Manager 中设置 iOS 设备注册  

1.  **先决条件** - 在为任何平台安装注册前，必须先完成[安装混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。    

2.  **下载证书签名请求** – 证书签名请求文件 (.csr) 要求请求 Apple 的 APNs 证书。  

    1.  在 Configuration Manager 控制台中的“管理”工作区中，转到“云服务”> “Microsoft Intune 订阅”。  

    2.  在“主页”  选项卡上，单击“创建 APNs 证书请求” 。 “请求 Apple Push Notification 服务证书签名请求”  对话框随即打开。  

    3.  “浏览” 到要保存新的证书签名请求 (.csr) 文件的路径。 本地保存证书签名请求 (.csr) 文件。  

    4.  单击“下载” 。 下载新 Microsoft Intune .csr 文件，并由 Configuration Manager 保存。 .Csr 文件用于从 Apple 推送证书门户请求信任关系证书。  

3.  **请求 Apple 的 APNs 证书** – Apple Push Notification 服务 (APNs) 证书用于在管理服务、Intune 和注册的 iOS 移动设备之间建立信任关系。  

    1.  在浏览器中，转到 [Apple Push Certificates 门户](http://go.microsoft.com/fwlink/?LinkId=269844) 并使用贵公司 Apple ID 登录。 若要续订 APN 证书，必须在将来使用此 Apple ID。  

    2.  使用证书签名请求 (.csr) 文件完成向导。 下载 APNs 证书并在本地保存 .pem 文件。 此 APNs 证书 (.pem) 文件用于在 Apple 推送通知服务器和 Intune 的移动设备管理机构之间建立信任关系。  

4.  **启用注册并上载 APNs 证书** – 若要启用 iOS 注册，请上载 APNs 证书。  

    1.  在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。  

    2.  在“主页”选项卡上的“订阅”组中，单击“配置平台” > “iOS”。  

        > [!NOTE]  
        >  在 Configuration Manager 控制台中启用 iOS 注册之前，请不要上载 Apple Push Notification 服务 (APN) 证书。  

    3.  在“Microsoft Intune 订阅属性”  对话框中，选择“iOS”  选项卡并单击选择“启用 iOS 注册”  复选框。  

    4.  单击“浏览” 并转到“从 Apple 下载的 APNs 证书(.cer)文件”。 Configuration Manager 会显示 APNs 证书信息。 单击“确定”  ，将 APNs 证书保存到 Intune。  

 设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。



<!--HONumber=Dec16_HO3-->


