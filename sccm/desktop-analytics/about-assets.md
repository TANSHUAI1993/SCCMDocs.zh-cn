---
title: 桌面分析中的资产
titleSuffix: Configuration Manager
description: 了解桌面分析中的设备、驱动程序和应用。
ms.date: 08/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b60326a746768e7045104a571d05a085ac0bd2a
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72387122"
---
# <a name="assets-in-desktop-analytics"></a>桌面分析中的资产

设备将数据报告到桌面分析后，会提供以下资产的清单：

- 装置
- 安装的应用  

在服务门户中，在 "桌面分析" 菜单中选择 "**资产**"。


## <a name="devices"></a>装置

"**设备**" 选项卡显示你的组织中注册到桌面分析的所有设备的关键信息。 您可以对任何列或筛选特定值进行排序。

> [!NOTE]  
> 如果仪表板未报告你希望为环境显示的设备数，请参阅[桌面分析故障排除](/sccm/desktop-analytics/troubleshooting)。  

在部署计划中，有关设备的更多详细信息。 有关详细信息，请参阅[计划资产](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>应用

"**应用**" 选项卡显示服务在 Windows 设备上检测到的所有已安装的应用。

在超过2% 的已注册设备上安装**值得注意**的应用。

通过设置下列类别之一来配置应用的**重要性**：

- 严重
- 重要
- 忽略 
- 未查看
- 不重要<!-- 3587232 -->


从列表中选择应用，然后选择 "**编辑**"。 此操作显示应用的详细信息。 选择 "**重要性**" 下拉菜单并设置一个值。 你还可以分配一个**所有者**。 如果进行了任何更改，请选择 "**保存**"。

### <a name="a-namebkmk_plan-autoapp--automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> 系统和应用商店应用的自动升级决策

<!-- 3587232 -->
确定**重要性**和**升级决策**对于桌面分析工作流中的所有值得注意的应用而言至关重要。 为了帮助减少对这些应用进行注释的工作量，某些类型的应用会自动标记为*不重要*。 这些应用的部署计划升级决策也标记为 "*就绪*"。 以下应用是兼容的，并且应在升级 Windows 后继续工作：

- Microsoft 发布的系统应用和组件

- 从 Microsoft Store 管理和更新的应用

> [!Tip]
> 管理全局级别或按部署计划的任何应用的输入。 
>
> 1. 在桌面分析门户的 "**管理**" 菜单中，选择 "**资产**"。 然后选择 "**应用**"。
>
> 2. 使用 "**类型**" 和 "**类别**" 列可以管理这些应用类别：
>
>    - 适用于应用商店应用，筛选器**类型**为**新式**
>    - 对于系统应用，筛选**类别**为**后台进程**或**Windows 组件**



在部署计划中，还可以设置**升级决策**。 有关详细信息，请参阅[计划资产](/sccm/desktop-analytics/about-deployment-plans#plan-assets)




## <a name="next-steps"></a>后续步骤

- [了解桌面分析部署计划](/sccm/desktop-analytics/about-deployment-plans)  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

- [桌面分析中的兼容性评估](/sccm/desktop-analytics/compat-assessment)  
