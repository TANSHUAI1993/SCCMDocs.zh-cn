---
title: "使用 System Center Configuration Manager 和 Microsoft Intune 设置 Android 混合设备管理 | Microsoft Docs"
description: "使用 Configuration Manager 和 Intune 准备管理 Android 移动设备。"
ms.custom: na
ms.date: 07/31/2017
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
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: b47ecd1754a623b1b57dc5c5ecb42a6b0b64404e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/29/2017

---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 设置 Android 混合设备管理

*适用范围：System Center Configuration Manager (Current Branch)*

本主题帮助 IT 管理员启用 Android 和 Android for Work 设备的混合注册。 然后，IT 管理员可以使用 System Center Configuration Manger 通过配置的 Microsoft Intune 订阅来管理设备。 用户可以从 Google Play 中下载 Android 公司门户应用，以便他们可以注册 Android（包括 Samsung KNOX 标准）和 Android for Work 设备。

作为 Configuration Manager 管理员，可以管理符合性设置、擦除或删除 Android 设备、部署应用以及收集软件和硬件清单。 设备上未安装 Android 公司门户应用的情况下，你不会拥有管理功能（如清单和符合性设置），但是你仍然可以将应用部署到 Android 设备。  

## <a name="enable-android-enrollment"></a>启用 Android 注册  
采用以下步骤，可使 Configuration Manager 管理 Android 设备，而无需使用工作配置文件（即“经典 Android”注册）。

1. 在为任何平台设置注册前，必须先完成[设置混合 MDM](setup-hybrid-mdm.md) 中的先决条件和过程。  
2. 在 Configuration Manager 控制台的“管理”工作区中，选择“概述” > “云服务” > “Microsoft Intune 订阅”，然后选择你的 Intune 订阅。  
3. 在“主页”选项卡上的“订阅”组中，选择“配置平台” > “Android”。  
4. 在“Microsoft Intune 订阅属性” 对话框中，选择“Android” 选项卡并选中“启用 Android 注册” 框。  

> [!NOTE]
>  “阻止个人拥有的设备”功能目前不可用。 

 设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。

## <a name="enable-android-for-work-enrollment"></a>启用 Android for Work 注册
采用以下步骤，可使 Configuration Manager 通过工作配置文件管理 Android 设备。

1. 在 https://accounts.google.com/SignUp 上创建一个 Google 帐户作为你的 Android for Work 管理帐户。 或者，使用与此 Intune 租户的所有 Android for Work 管理任务相关联的帐户登录。 此帐户可以是在管理 Android 设备的管理员之间共享的 Google 帐户。 组织使用此 Google 帐户，在 Play for Work 控制台中管理和发布应用。 此帐户将用于在 Play for Work 应用商店中批准应用，因此请记录帐户名和密码。
2. 通过将 Google 帐户绑定到在 Configuration Manager 中托管的 Intune 租户来启用 Android 注册：
   1. 在 Configuration Manager 控制台的“管理”工作区中，选择“概述” > “云服务” > “Microsoft Intune 订阅”，然后选择你的 Intune 订阅。
   2. 在“主页”选项卡上的“订阅”组中，选择“配置平台” > “Android for Work”。
   3. 在对话框中，选择“在 Intune 控制台中配置 Android for Work”。 Intune 控制台将在 Web 浏览器中打开。
   4. 使用你的 Intune 管理员凭据登录 Intune 门户。
   5. 选择“配置”，打开 Google Play 的 Android for Work 网站。
   6. 在 Google 登录页上，输入步骤 1 中的 Google 帐户凭据，然后提供公司信息。
3. 返回 Intune 门户时，Android for Work 已启用，Android for Work 设备有三个注册选项：
   - **将所有设备作为 Android 管理**（已禁用）。 所有 Android 设备（包括支持 Android for Work 的设备）均将注册为传统的 Android 设备。
   - **将受支持设备作为 Android for Work 管理**（已启用）。 将支持 Android for Work 的所有设备均注册为 Android for Work 设备。 任何不支持 Android for Work 的 Android 设备均将注册为传统的 Android 设备。
   - **仅为这些组中的用户将受支持设备作为 Android for Work 管理**（仅针对某些组启用）。 可以将 Android for Work 管理目标定位到有限的一组用户。 只有在所选组的成员注册支持 Android for Work 的设备后，这些设备才能注册为 Android for Work 设备。 其他所有设备均注册为 Android 设备。

> [!NOTE]
> 一个已知的问题将阻止“仅为这些组中的用户将受支持设备作为 Android for Work 设备管理”选项按预期方式正常运行。 指定 Azure AD 组中的用户设备将注册为 Android 而不是 Android for Work。 若要启用 Android for Work，必须使用“将所有受支持设备作为 Android for Work 管理”选项。


设置完成后，需要让用户知道如何注册其设备。 请参阅[用户需要了解的有关设备注册的内容](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)。 此信息适用于 Microsoft Intune 和 Configuration Manager 托管的移动设备。

完成绑定后，可以在 Intune 门户中看到帐户名和组织名称。 此时，可关闭两个浏览器。

### <a name="enroll-an-android-for-work-device"></a>注册 Android for Work 设备
用户注册 Android for Work 设备的方式与注册 Android 设备的方式类似。 用户可以在其移动设备上下载并安装适用于 Android 的公司门户应用。 在注册过程中，应用将提示他们创建工作配置文件。 创建工作配置文件后，用户必须切换到公司门户的托管版本。 托管的公司门户的右下角具有小型橙色公文包标记。

### <a name="manage-android-for-work-devices"></a>管理 Android for Work 设备
启用 Android for Work 注册后，可以为 Android for Work 设备执行以下管理任务：
- [批准应用](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [创建配置项目](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [管理符合性设置](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [管理电子邮件配置文件](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [有选择地擦除工作配置文件](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< 上一步](create-service-connection-point.md)  [下一步 >](set-up-additional-management.md)

