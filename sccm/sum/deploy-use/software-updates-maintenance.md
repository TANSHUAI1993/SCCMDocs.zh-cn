---
title: 软件更新维护
titleSuffix: Configuration Manager
description: 若要在 Configuration Manager 中维护更新，可以计划 WSUS 清理任务，也可以手动运行它。
author: aczechowski
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a44643870234a08169db1d55cc834e4ca5fcbb5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385484"
---
# <a name="software-updates-maintenance"></a>软件更新维护

*适用范围：System Center Configuration Manager (Current Branch)*

可从 Configuration Manager 控制台和软件更新点组件属性中计划和运行 WSUS 清理任务。 首次选择运行 WSUS 清理任务时，它将在下一次软件更新同步后运行。  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>计划和运行 WSUS 清理作业 
通过运行以下步骤来计划 WSUS 清理作业：   

1.  在 Configuration Manager 控制台中，导航到“管理” > “概述” > “站点配置” > “站点”。 
2. 选择 Configuration Manager 层次结构顶部的站点。 

3.  单击“设置”  组中的  “配置站点组件”，然后单击“软件更新点”  以打开软件更新点组件属性。  

4. 评审“取代行为”。 如果需要，修改行为。 
![取代行为屏幕截图](media/sccm-supersedence-behavior.PNG)

5.  单击“取代规则”选项卡，选择“运行 WSUS 清理向导”。 在版本 1806 中，该选项重命名为“同步后运行 WSUS 清理”。 
 
6. 单击“确定”（如果运行版本 1806，请单击“关闭”）。

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>版本 1802 及更早版本中的 WSUS 清理行为
在 Configuration Manager 版本 1806 之前，WSUS 清理选项运行以下项： 
- 仅限顶层站点的 WSUS 服务器上的 WSUS 清理向导中的“过期更新”选项。 
![WSUS 已过期更新清理屏幕截图](media/wsus-cleanup-expired.PNG)

-  Configuration Manager 数据库中的软件更新配置项每七天进行一次清理，并从控制台中删除不需要的更新。 
   - 如果当前已部署，则此清理不会从 Configuration Manager 控制台中删除过期的更新。 

顶层 WSUS 数据库和环境中的所有其他 WSUS 数据库仍需其他维护。 有关详细信息和说明，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/)博客文章的完整指南。 


## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>从版本 1806 开始的 WSUS 清理行为
从 1806 版开始，WSUS 清理选项在每次同步后出现，并执行以下清理项：<!--1357898 -->
- CAS 和主站点上的 WSUS 服务器的“已过期更新”选项。
    - 用于辅助站点的 WSUS 服务器不会针对过期更新运行 WSUS 清理。 
- Configuration Manager 从其数据库构建已取代的更新列表。 该列表基于“软件更新点”组件属性中的取代行为。 
    - 符合取代行为标准的更新配置项在 Configuration Manager 控制台中已过期。
    - 在 WSUS 中，对于 CAS 和主站点拒绝更新，但对于辅助站点不拒绝更新。
- Configuration Manager 数据库中的软件更新配置项每七天进行一次清理，并从控制台中删除不需要的更新。 
    - 如果当前已部署，则此清理不会从 Configuration Manager 控制台中删除过期的更新。 

> [!NOTE]
> “取代更新过期前需等待的月数”基于取代更新的创建日期。 例如，如果将此设置设为 2 个月，则在 WSUS 中已被取代的更新将被拒绝，而在 Configuration Manager 中，如果取代更新存在 2 个月，更新将过期。 

需要在辅助站点 WSUS 数据库上手动运行所有 WSUS 维护。 CAS 和主站点上未运行以下“WSUS 服务器清理向导”选项：

- 未使用的更新和更新修订
- 未联系服务器的计算机
- 不需要的更新文件

 有关详细信息和说明，请参阅 [Microsoft WSUS 和 Configuration Manager SUP 维护](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/)博客文章的完整指南。 

## <a name="updates-cleanup-log-entries"></a>更新清理日志条目
 
可通过查看以下条目的 wsyncmgr.log 来验证此清理： 
  - 看到此日志项目时，WSUS 中已取代更新的拒绝已完成：`Cleanup processed <number> total updates and declined <number>`
  - 看到此项目时，WSUS 清理开始：`Calling WSUS Cleanup.`
  - 看到此项目时，已完成对已过期更新的 WSUS 清理：`Successfully completed WSUS Cleanup.`
  - 看到此项目时，Configuration Manager 过期更新配置项清理开始：`Deleting old expired updates...`
  - 看到此项目时，Configuration Manager 过期更新配置项清理已完成：`Deleted <number> expired updates total`
