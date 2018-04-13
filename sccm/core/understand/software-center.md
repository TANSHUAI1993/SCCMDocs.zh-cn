---
title: 软件中心用户指南
titleSuffix: Configuration Manager
description: 了解软件中心的功能和特性
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 4ffe2a5049f31b5d4c06267b7683f90b0bd72633
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="software-center-user-guide"></a>软件中心用户指南

*适用范围：System Center Configuration Manager (Current Branch)*

组织的 IT 管理员可使用软件中心安装应用程序和软件更新并升级 Windows。 本用户指南为计算机用户介绍了软件中心的功能。

### <a name="general-notes-about-software-center-functionality"></a>关于软件中心功能的一般说明
- 本文介绍软件中心的最新功能。 如果组织正在使用较旧但仍受支持的软件中心版本，则并非所有功能都可用。 有关详细信息，请联系 IT 管理员。
- IT 管理员可能会禁用软件中心的某些方面。 用户的具体体验可能有所不同。
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>如何打开软件中心

若要以最简单的方式在 Windows 10 计算机上启动软件中心，请按“开始”并键入 `Software Center`。 

如果在“开始”菜单中导航，请查看“Microsoft System Center”组下的“软件中心”图标。



## <a name="applications"></a>应用程序

单击“应用程序”选项卡，查找并安装 IT 管理员为用户或此计算机部署的应用程序。
- **全部**：显示可安装的所有应用程序
- **必需**：IT 管理员会强制安装这些应用程序。 如果用户卸载其中一个应用程序，软件中心会重新安装它。
- **筛选器**：IT 管理员可能会创建各种应用程序。 如果可用，请单击下拉列表进行筛选，以便仅查看特定类别的应用程序。 选择“全部”可显示所有应用程序。
- **排序方式**：重新排列应用程序列表。 默认情况下，此列表按“最近的”排序。
- **搜索**：仍找不到要查找的内容？ 在“搜索”框中输入关键字来查找它！
-  切换视图：单击图标以在列表视图和磁贴视图之间进行切换。 默认情况下，应用程序列表显示为图形磁贴。 
    - 磁贴视图：IT 管理员可以自定义图标。 在每个磁贴下方显示应用程序名称、发布者和版本。 
    - 列表视图：此视图显示应用程序图标、名称、发布者、版本和状态。 


### <a name="install-multiple-applications"></a>安装多个应用程序 
<!-- 1357126 -->
一次安装多个应用程序，而不是等一个完成后再开始下一个。 并非所有应用程序都符合以下要求：
- 该应用对用户可见
- 尚未下载或安装该应用
- IT 管理员不需要获得批准即可安装该应用

若要一次安装多个应用程序，请执行以下操作：
 1. 若要在列表视图中进入多选模式，请单击多选图标 ![软件中心多选图标](media/software-center-multi-select-apps.png) 新图标。
 2. 通过单击列表中应用左侧的复选框，选择两个或多个应用进行安装。
 3. 单击“安装所选”按钮。

照常安装应用，只是现在连续进行安装。




## <a name="updates"></a>更新

单击“更新”选项卡可查看并安装 IT 管理员部署到此计算机的软件更新。  
- **全部**：显示可安装的所有更新
- **必需**：IT 管理员会强制安装这些更新。
- **排序方式**：重新排列更新列表。 默认情况下，此列表按“应用程序名称: A 到 Z”排序。

若要安装更新，请单击“全部安装”。

若仅安装特定更新，请单击图标进入多选模式。 检查要安装的更新，然后单击“安装选定更新”。



## <a name="operating-systems"></a>操作系统

单击“操作系统”选项卡可查看并安装 IT 管理员部署到此计算机的 Windows 版本。  
- **全部**：显示可安装的所有 Windows 版本
- **必需**：IT 管理员会强制安装这些升级。
- **排序方式**：重新排列更新列表。 默认情况下，此列表按“应用程序名称: A 到 Z”排序。



## <a name="installation-status"></a>安装状态

单击“安装状态”选项卡可查看应用程序的状态。 用户可能会看到以下状态：
- **已安装**：软件中心已在此计算机上安装此应用程序。
- **正在下载**：软件中心正在下载要在此计算机上安装的软件。
- **失败**：软件中心在尝试安装软件时出错。



## <a name="device-compliance"></a>设备符合性

单击“设备符合性”选项卡可查看此计算机的符合性状态。

单击“检查符合性”可根据 IT 管理员定义的安全策略评估此设备的设置。



## <a name="options"></a>选项

单击“选项”选项卡可查看此计算机的其他设置。

### <a name="work-information"></a>工作信息

指示用户平时的工作时间。 IT 管理员在安排软件安装时可能会避开用户的工作时间。 每天至少留出四小时执行系统维护任务。 IT 管理员仍可以在工作时间安装关键应用程序和软件更新。

- 单击下拉列表以选择此计算机的最早使用时间和最晚使用时间。 这些值默认为“早上 5 点”到“晚上 10 点”

- 选中通常使用此计算机的每周天数旁边的复选框。 默认情况下，软件中心只选择工作日。  


### <a name="power-management"></a>电源管理

IT 管理员可能会设置电源管理策略。 这些策略可帮助组织在不使用此计算机时节约用电。 

若要使此计算机免受这些策略的影响，请选中“不将 IT 部门的电源设置应用于此计算机”复选框。 此设置默认处于禁用状态；计算机将应用电源设置。 


### <a name="computer-maintenance"></a>计算机维护

指定软件中心在截止时间前向软件应用更改的方式
- **仅在指定的工作时间之外自动安装或卸载所需软件并重新启动计算机**：此设置默认处于禁用状态。
- **当我的计算机处于演示模式时暂停软件中心活动**：此设置默认处于启用状态。
- **同步策略**：在 IT 管理员的指示下单击此按钮。此计算机会检查服务器中的所有更新，比如应用程序、软件更新或操作系统。

