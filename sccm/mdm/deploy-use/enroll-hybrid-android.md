---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Android 混合设备管理 | Microsoft Docs"
description: "使用 Configuration Manager 和 Intune 准备管理 Android 移动设备。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: ab892174643e7565ad9a74abc4f83f2f152669bd


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 设置 Android 混合设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

对于 System Center Configuration Manager，用户可以从 Google Play 中下载 Android 公司门户应用以注册 Android（包括 Samsung KNOX 标准版）设备。 利用 Android 公司门户应用，你可以管理符合性设置、擦除或删除 Android 设备、部署应用以及收集软件和硬件清单。 如果 Android 设备上未安装 Android 公司门户应用，则你不会拥有所有的管理功能，如清单和符合性设置，但是你仍然可以将应用部署到 Android 设备。  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>使用 Configuration Manager 和 Intune 准备管理 Android 移动设备  
 以下步骤可让 Configuration Manager 管理 Android 设备。  

#### <a name="to-enable-android-enrollment"></a>若要启用 Android 注册  

1.  **先决条件** - 在为任何平台安装注册前，必须先完成[安装混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。  

2.  在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。  

3.  在“主页”选项卡上的“订阅”组中，单击“配置平台” > “Android”。  

4.  在“Microsoft Intune 订阅属性”  对话框中，选择“Android”  选项卡并单击选择“启用 Android 注册”  复选框。  

 设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。



<!--HONumber=Dec16_HO3-->


