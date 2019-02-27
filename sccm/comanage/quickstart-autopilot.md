---
title: 通过共同管理的 Windows Autopilot
titleSuffix: Configuration Manager
description: 使用 Windows Autopilot 通过共同管理配置管理器中，简化了的新 Windows 10 设备。
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838746"
---
# <a name="windows-autopilot-with-co-management"></a>通过共同管理的 Windows Autopilot

接收新的 Windows 10 设备是令人兴奋。 但是，可能需要时间来配置所有设置和应用程序，以便您可以提高工作效率。 共同管理解决了此设备预配 Windows Autopilot 问题。

Autopilot 为您和您在以下情况下的用户提供简化的体验：
- 设置和预配置的新 Windows 10 设备  
- 重置、 回收，并恢复现有的设备  

Autopilot 减少了时间、 资源和与部署、 管理和停用设备相关联的复杂性。 同时，为你的用户体验是简化和易于从首次启动。

Windows Autopilot 支持多种方案，所有这些最大化并将共同管理：

- 用户可以推动他们自己的新设备的部署到混合 Azure AD 加入与 Active Directory 或 Azure Active Directory (Azure AD)  

- 可以设置自部署新的设备部署到 Azure AD 中为共享的设备和网亭  

- 与现有设备的 Windows Autopilot，使用配置管理器来将现有的设备从 Windows 7 和 Active Directory 迁移到 Windows 10 和 Azure AD  

在以下视频中，高级项目经理 Danny Guillory 和首席计划经理 Andrew McMurray 讨论并演示 Windows Autopilot 通过共同管理：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>优点

当您使用共同管理和 Autopilot 组合在一起时，请确保输入您的网络的新设备最终会在相同的管理状态。 在此设置，设备在 Intune 中注册和 Configuration Manager 客户端。  它允许你使用新的 Windows 10 预配模型，并可帮助你无需创建、 维护和更新自定义 OS 映像。 

在所有这些情况下，您可以自动[启用共同管理](/sccm/comanage/how-to-prepare-win10)由 Intune。 这种自动化可帮助设置过程中，使用和的日常管理的设备。

使用 Autopilot，无需担心有关映像和驱动程序。 专注于通过此自动化过程，通过共同管理使用 Intune 和 Configuration Manager 预配设备。


下面是如何结合使用共同管理和 Autopilot 可以帮助您稍后再试：

#### <a name="reduce-time-costs-and-complexity"></a>减少时间、 成本和复杂性
Windows Autopilot 设备上使用 Windows 10 已预装的 OEM 优化版本。 此配置将保存组织的无需维护自定义映像和驱动程序中使用设备的每个模型的工作量。 而不是设备重置映像，将转换现有的 Windows 10 安装到"业务就绪"状态。 它将应用设置和策略、 安装应用程序，并更改版本的 Windows 10。 例如，从升级 Windows 10 专业版到 Windows 10 企业版，以便可以支持高级的功能。

#### <a name="improve-the-user-experience"></a>改善用户体验
最佳用户体验干扰最少，帮助他们重新回到将重点放在其工作。 Windows Autopilot 提供了一种简单的方法，以帮助用户获取快速使用几下即可和设置其 Azure AD 凭据。 对于具有大型字段远程员工的很多组织，使用 Windows Autopilot 直接从制造商提供的新设备。

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>使用 Autopilot 和配置管理器来将现有的 Windows 7 设备迁移到 Windows 10
与现有设备的 Windows Autopilot，您将创建配置文件，并将其部署与 Configuration Manager 任务序列。 此过程轻松地将迁移现有的设备从 Windows 7 到 Windows 10。 使用配置管理器中的签名 Windows 10 映像，然后将其应用于使用 Autopilot 配置现有的 Windows 7 设备。 当用户启动设备时，它们使用 Autopilot 面向用户的加入过程。

适用于现有设备的 Autopilot 步骤如下：

![适用于现有设备的 Windows Autopilot 过程概述](media/autopilot-for-existing-devices.png)

1. 部署组策略将已知的文件夹重定向到 OneDrive
2. 生成 Autopilot 配置文件
3. 部署任务序列升级到 Windows 10
4. Windows 10 计算机上首次启动经历 Autopilot

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>建立新式设备预配的所有类型的辅助角色
使用 Autopilot，现在可以提供无 OS 部署到无人操作的设备或使用自部署模式下的共享的设备。 此设置符合所有的辅助角色的不同类型的需求。 此外，可确保重新预配的新用户的设备是简单且轻松地重置 Windows Autopilot 函数。 此过程简化了什么具有传统上是一个困难的任务具有季节性或协定辅助角色时。 



## <a name="case-study"></a>案例研究

正使用德语的逻辑和 rail 货运公司 DB Shenker 使用 Autopilot 来提高员工工作效率和释放其 IT 团队在日常支持任务。 Shenker 具有移开传统的映像，并替换为通过云预配。 他们现在使用 Azure AD 加入和 Intune，以快速启动和运行新的设备。 

而不是具有其远程工作人员将时间浪费在出差到具有 IT 服务的位置，Shenker 现在使用 Windows Autopilot。 它们到与其当地的现场分支机构直接从制造商交付其辅助角色的硬件。 工作线程将新设备连接到 internet，并且它们使用其 Azure AD 凭据登录。 然后，设备连接到应用程序和服务该 Schenker IT 部门将分配给用户的单个配置文件。

有关详细信息，请参阅[全局物流公司可集中管理 IT，并具有现代数字工作区的员工](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10)。



## <a name="value-proposition"></a>价值主张

通过创建更好的用户体验为您的用户在组织中创建的满意度。 使用 Windows Autopilot 来降低成本。 让您腾出时间专注于其他项目来驱动更多价值和为你的组织的影响。



## <a name="configure"></a>配置

有关详细信息，请参阅下列文章：

[使用 Intune 创建 Windows Autopilot 配置文件](https://docs.microsoft.com/intune/enrollment-autopilot)

[现有的设备的 Windows Autopilot](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices)任务序列

