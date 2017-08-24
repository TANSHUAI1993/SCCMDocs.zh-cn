---
title: "客户端托管的设备的常见符合性管理任务 - Configuration Manager | Microsoft Docs"
description: "通过完成一些常见方案，了解 System Center Configuration Manager 符合性设置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 2012ab5e55da8d707fd668e0163b42fe7d56c72f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>使用 System Center Configuration Manager 客户端在设备上管理符合性的常见任务

*适用范围：System Center Configuration Manager (Current Branch)*

本主题中的方案通过演示你可能遇到的一些常见情景介绍如何使用 System Center Configuration Manager 符合性设置。  

 如果你已熟悉符合性设置，有关所有可用功能的详细文档，可参阅[使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)部分。  

 在开始之前，请阅读[符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)以了解有关符合性设置的一些基础知识，另请阅读[规划和配置符合性设置](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)来实施任何必要的先决条件。  

## <a name="general-information-for-each-scenario"></a>每个方案的一般信息  
 在每个方案中，将创建可执行特定任务的配置项目。 打开“创建配置项目向导”，使用以下步骤：  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置项目”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建配置项目” 。  

4.  在“创建配置项目”向导的“常规”  选项卡上（如下所示），指定配置项目的名称和说明，然后选择本主题中的每个方案的相应配置项目类型。  

     ![将显示“创建配置项目向导”的常规页。](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>使用 Configuration Manager 客户端管理的 Windows 10 设备的方案  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>方案：在 Windows 10 设备上禁用蓝牙  
 在此方案中，安全部门已将设备上的蓝牙功能识别为可用于在公司外传输敏感企业信息的一种手段。 你最近已将所有的 PC 都升级到了 Windows 10 并决定禁用这些设备上的蓝牙功能。  

1.  在“创建配置项目”向导的“常规”  页上，选择  “Windows 10”配置项目类型，然后单击“下一步” 。  

2.  在向导的“支持的平台”  页上，选择所有 Windows 10 平台。  

3.  在“设备设置”  页上，选择“设备” ，然后单击“下一步” 。  

4.  在“设备”  页上，选择“禁止”  作为 “蓝牙”的值。  

5.  选择“修正非符合性设置”  以确保更改被应用到所有 Windows 10 设备上。  

6.  完成向导以创建配置项目。  

 现在便可以通过[使用 System Center Configuration Manager 创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主题中的信息将创建的配置部署到设备。  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>使用 Configuration Manager 客户端管理的 Windows 台式机和服务器计算机的方案  
 在运行 Configuration Manager 客户端的 Mac 计算机上，有两种评估符合性的选项：  

-   评估 Mac OS X 首选项 (plist) 文件。  

-   使用自定义脚本并评估由该脚本返回的结果。  

 有关详细信息，请参阅[如何为 System Center Configuration Manager 客户端管理的Mac OS X 设备创建配置项目](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)。  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>方案：修正 Windows 台式计算机上的不正确的注册表值  
 在此方案中，你将发现重要的业务线应用在你管理的运行 Windows 8.1 的某些计算机上未正确运行。 经过调查发现，这是因为某些计算机上名为“HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1”  的注册表值已被设置为了“0”  。 若想成功运行业务线应用，必须将该值设置为“1” 。  

 在此过程中，你需要创建一个配置项目，它会监视并自动修正发现的任何错误的注册表项值。  

1.  在“创建配置项目”向导的“常规”  页上，选择  “Windows 台式机和服务器(自定义)”配置项目类型，然后单击 “下一步”。  

2.  在向导的“支持的平台”  页上，选择“Windows 8.1”  （以确保配置项目仅应用于受影响的计算机）。  

3.  在“设置”  页上，单击“新建”  创建新的设置。  

4.  在“创建设置”  对话框的“常规”  选项卡上，配置以下信息：  

    -   **名称** > **示例设置**  

    -   **设置类型** > **注册表值**  

    -   **数据类型** > **整数** （因为该值仅包含一个数字）  

    -   **Hive** > **HKEY_LOCAL_MACHINE**  

    -   **密钥** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **值** > **1** （必需值）  

5.  在  “创建设置”对话框的“符合性规则”  选项卡上，单击“新建” ，然后在“创建规则”  对话框中，配置以下信息：  

    -   **名称** > **规则示例**  

    -   **所选设置** – 验证所选设置是否为“示例设置” 。  

    -   **规则类型** > **值**  

    -   **设置必须符合以下规则** – 验证设置名称是否正确，并配置选项以指定设置值必须等于“1” 。  

    -   **修正非符合性规则(如果支持)** – 勾选此框，以确保 Configuration Manager 在注册表项值不正确时将其重置为正确的值。  

6.  完成向导以创建配置项目。  

 现在可以使用[用于创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主题中的信息将创建的配置部署到设备。  
