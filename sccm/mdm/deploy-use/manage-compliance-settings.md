---
title: "管理使用 Intune 管理的设备上的符合性 | Microsoft Docs"
description: "通过完成一些常见方案，了解 System Center Configuration Manager 符合性设置。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3a63f6c55c317c9c84d4394dfdcb9f1cbbbc90b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="managing-compliance-on-devices-managed-with-intune"></a>管理使用 Intune 管理的设备上的符合性

*适用范围：System Center Configuration Manager (Current Branch)*

这些方案通过演示你可能遇到的一些常见情景介绍如何使用 System Center Configuration Manager 符合性设置。  

 如果你已熟悉符合性设置，可参阅[使用 Intune 管理的设备的配置项](#configuration-items-for-devices-managed-with-intune)部分，了解有关所有可用功能的详细文档。  

 [符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)提供有关符合性设置的基础知识，而[规划和配置符合性设置](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)将帮助实施任何必要的先决条件。  

## <a name="general-information-for-each-scenario"></a>每个方案的一般信息  
 在每个方案中，将创建可执行特定任务的配置项目。 打开“创建配置项目向导”，使用以下步骤：  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置项目”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建配置项目” 。  

4.  在“创建配置项目”向导的“常规”  选项卡上（如下所示），指定配置项目的名称和说明，然后选择本主题中的每个方案的相应配置项目类型。  

     ![将显示“创建配置项目向导”的常规页。](media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-with-intune"></a>使用 Intune 管理的 Windows 8.1 和 Windows 10 设备的方案  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>方案：限制在所有 Windows PC 上对应用商店的访问  
 在此方案中，你是公司的 IT 管理员，负责处理高敏感度的信息。 因此，你要限制用户可以安装的应用。 你想要阻止所有 Windows 10 PC 用户从 Windows 商店下载应用，那么你要采取以下措施。  

1.  在“创建配置项目”向导的“常规”  页上，选择“Windows 8.1 和 Windows 10”  配置项目类型，然后单击“下一步” 。  

2.  在“支持的平台”页上，选择所有 Windows 10 平台。  

3.  在“设备设置”  页上，选择“商店” ，然后单击“下一步” 。  

4.  在“商店”  页上，选择“禁止”  作为“应用商店” 的值。  

5.  选择 **修正非符合性设置** 以确保更改被应用到所有 PC 上。  

6.  完成向导以创建配置项目。  

 现在可以使用[用于创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主题中的信息将创建的配置部署到设备。  

## <a name="scenarios-for-windows-phone-devices-managed-with-intune"></a>使用 Intune 管理的 Windows Phone 设备的方案  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>方案：禁用 Windows Phone 上屏幕捕获的使用  
 在此场景下，你在公司中使用 Windows Phone 8.1 设备。 这些设备运行一个包含敏感信息的销售应用。 要保护你的公司，你要禁用设备上屏幕捕获的使用，因为这可能被用来传输敏感信息到公司外部。  

1.  在“创建配置项目”向导的“常规”  页上，选择“Windows Phone”  配置项目类型，然后单击“下一步” 。  

2.  在“支持的平台”页上，选择**所有 Windows Phone 8.1** 平台。  

3.  在“设备设置”  页上，选择“设备” ，然后单击“下一步” 。  

4.  在“设备”  页上，选择“禁用”  作为“屏幕捕获” 的值。  

5.  选择“修正非符合性设置”  以确保更改被应用到所有 Windows Phone 8.1 上。  

6.  完成向导以创建配置项目。  

 现在便可以通过[使用 System Center Configuration Manager 创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主题中的信息将创建的配置部署到设备。  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-with-intune"></a>使用 Intune 管理的 iOS 和 Mac OS X 设备的方案  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>方案：禁用 iOS 设备上的相机  
 在此场景下，你的公司为新产品设计创作了蓝图。 它们包含着一定不能被泄露的敏感信息。 由于公司向所有员工都发放了 iPhone 或 iPad，你要禁用这些设备上的相机使用以阻止它们被用来拍摄蓝图。  

1.  在“创建配置项目”向导的“常规”  页上，选择“iOS 和 Mac OS X”  配置项目类型，然后单击“下一步” 。  

2.  在“支持的平台”页上，选择所有 iPhone 和所有 iPad 设备平台。  

3.  在“设备设置”  页上，选择“安全” ，然后单击“下一步” 。  

4.  在“安全”  页上，选择“禁用”  作为“相机” 的值。  

5.  选择“修正非符合性设置”  以确保更改被应用到所有 iOS 设备上。  

6.  完成向导以创建配置项目。  

 现在便可以通过[使用 System Center Configuration Manager 创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主题中的信息将创建的配置部署到设备。  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>使用 Intune 管理的 Android 和Samsung KNOX 标准版设备的方案  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>方案：在所有 Android 5 设备上要求密码  
 在此场景下，你将为 Android 5 设备创建一个配置项目，需要用户在他们的设备上配置一个包含至少 6 个字符的密码。 此外，如果用户输入不正确密码 5 次，那么设备将被擦除。  

1.  在“创建配置项目”向导的“常规”  页上，选择“Android 和 Samsung KNOX”  配置项目类型，然后单击“下一步” 。  

2.  在“支持的平台”页上，只选择“Android 5”（以确保仅将设置应用到该平台）。  

3.  在“设备设置”  页上，选择“密码” ，然后单击“下一步” 。  

4.  在“密码”  页上，配置下列设置：  

    -   **设备上需要密码设置** > **必需**  

    -   **最短密码长度（字符）** > **6**  

    -   **擦除设备前的失败登录尝试次数** > **5**  

5.  完成向导以创建配置项目。  

 现在可以使用[用于创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主题中的信息将创建的配置部署到设备。  

## <a name="configuration-items-for-devices-managed-with-intune"></a>使用 Intune 管理的设备的配置项

以下 System Center Configuration Manager 配置项类型适用于不由 Configuration Manager 客户端管理的设备（例如向 Microsoft Intune 注册的设备）。  

 -   [如何为使用 Intune 管理的 Windows 8.1 和 Windows 10 设备创建配置项](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [如何为使用 Intune 管理的 Windows Phone 设备创建配置项](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [如何为使用 Intune 管理的 iOS 和 Mac OS X 设备创建配置项](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [如何为使用 Intune 管理的 Android 和 Samsung KNOX 标准版设备创建配置项](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
