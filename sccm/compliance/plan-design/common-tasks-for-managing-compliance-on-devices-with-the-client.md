---
title: '客户端托管设备的常见符合性管理任务 '
titleSuffix: Configuration Manager
description: 通过完成一些常见方案，了解 System Center Configuration Manager 符合性设置。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67a23fd5c1791253a7789fda74a30a0e71566f92
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550818"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>使用 System Center Configuration Manager 客户端在设备上管理符合性的常见任务

*适用范围：System Center Configuration Manager (Current Branch)*

本文提供了指导用户完成时可能遇到的一些常见方案中使用 System Center Configuration Manager 符合性设置的说明。  

 在已熟悉符合性设置的前提下，若要详细了解所有可用功能，可参阅[使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/create-configuration-items.md)。  

 在开始之前，请阅读[符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)若要了解有关符合性设置的一些基础知识。 读取[规划和配置符合性设置](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)有关必需的先决条件的信息。  

## <a name="general-information-for-each-scenario"></a>每个方案的一般信息  
 在每个方案中，将创建可执行特定任务的配置项目。 若要打开创建配置项目向导并开始，执行以下步骤：  

1.  在 Configuration Manager 控制台中，选择“资产和符合性”   > “符合性设置”   > “配置项目”  。  

1.  在“主页”  选项卡的“创建”  组中，选择“创建配置项目”  。  

1.  上**常规**创建配置项目向导中，这在以下屏幕截图中所示的页上，指定的名称和说明的配置项。 在本文中，然后选择每个方案的相应的配置项类型。  

     ![“创建配置项目向导”的“常规”页](/sccm/mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>方案： Windows 10 设备上禁用蓝牙

 在此方案中，安全部门已确定设备上的蓝牙功能可用于在公司外传输敏感企业信息。 你最近已升级到 Windows 10 的所有计算机。 您决定这些设备上禁用蓝牙。  

1. 在“创建配置项目向导”的“常规”  页上，选择“Windows 10”  配置项目类型，然后选择“下一步”  。  

2. 在向导的“支持的平台”  页上，选择所有 Windows 10 平台。  

3. 上**设备设置**页上，选择**设备**，然后选择**下一步**。  

4. 在“设备”  页上，选择“禁止”  作为  “蓝牙”的值。  

5. 选择“修正非符合性设置”  以确保更改被应用到所有 Windows 10 设备上。  

6. 完成向导以创建配置项目。  

 现在便可以通过[使用 System Center Configuration Manager 创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)一文中的信息将创建的配置部署到设备。  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>方案：修正 Windows 台式计算机上的不正确的注册表值

> [!NOTE] 
> 在运行 Configuration Manager 客户端的 Mac 计算机上，有两种评估符合性的选项：  
> - 评估 Mac OS X 首选项 (plist) 文件。
> - 使用自定义脚本并评估由该脚本返回的结果。  
>
>有关详细信息，请参阅[如何为 System Center Configuration Manager 客户端管理的Mac OS X 设备创建配置项目](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)。  

 在此方案中，你将发现在你管理某些 Windows 8.1 计算机上正确运行并不重要的业务线应用。 确定这是因为某些计算机上名为“HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1”  的注册表项的值已被设置为“0”  。 若想成功运行业务线应用，需要将该值设置为“1”  。  

 在此过程中，需要创建一个配置项目，它会监视并自动修正发现的任何错误的注册表项值。  

1. 在“创建配置项目向导”的“常规”  页上，选择“Windows 台式机和服务器(自定义)”  配置项目类型，然后选择“下一步”  。  

2. 在向导的“支持的平台”  页上，选择“Windows 8.1”  （目的是确保配置项目仅应用于受影响的计算机）。  

3. 在“设置”  页上，选择“新建”  以创建新的设置。  

4. 在“创建设置”  对话框的“常规”  选项卡上，配置以下设置：  

   -   **名称** > **示例设置**  

   -   **设置类型** > **注册表值**  

   -   “数据类型”   > “整数”  （因为该值仅包含一个数字）  

   -   **Hive** > **HKEY_LOCAL_MACHINE**  

   -   **密钥** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **值** > **1** （必需值）  

5. 上**符合性规则**选项卡**创建设置**对话框中，选择**新建**。 在中**创建规则**对话框框中，配置这些设置：  

   -   **名称** > **规则示例**  

   -   “所选设置”  > 验证所选设置是否为“示例设置”  。

   -   **规则类型** > **值**  

   -   “设置必须符合以下规则”  > 验证设置名称是否正确，并配置选项以指定设置值必须等于“1”  。  

   -   “修正非符合性规则(如果支持)”  > 选中此复选框可以确保 Configuration Manager 在注册表项值不正确时将其重置为正确的值。  

6. 完成向导以创建配置项目。  

 现在可以使用[用于创建和部署配置基线的常见任务](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)一文中的信息将创建的配置部署到设备。  

## <a name="next-steps"></a>后续步骤

[创建和部署配置基线](/sccm/compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines)
