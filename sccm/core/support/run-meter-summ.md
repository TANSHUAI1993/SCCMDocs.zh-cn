---
title: 运行计量摘要工具
titleSuffix: Configuration Manager
description: 使用运行计量摘要工具在 Configuration Manager 中触发软件计数摘要任务。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7bfb6758d62fb76650e019d00eef1ac2b2803d4b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126957"
---
# <a name="run-meter-summarization-tool"></a>运行计量摘要工具

适用范围：System Center Configuration Manager (Current Branch)

运行计量摘要工具是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 使用它可以立即触发主站点上的软件计数摘要的维护任务。 默认情况下，这些任务按照“站点维护”任务中的计划运行，即从每天中午 12:00 开始。 

这些任务汇总了 MeterData SQL 表中的数据，并将汇总结果写入 FileUsageSummary 和 MonthlyUsageSummary 表。 然后，会在软件计数报表中看到汇总结果。 可以连接到主站点数据库的任何 Configuration Manager 管理用户都可以使用此工具运行摘要。 

此工具运行“文件使用情况摘要”和“每月使用情况摘要”软件计数数据摘要任务。 它概述了没有通常 12 小时等待期的所有现有计量数据。 在托管站点数据库的 SQL 服务器上运行它。 如果摘要成功，则退出代码设置为 `0`。 如果出现错误，则退出代码为 `1`。



## <a name="usage"></a>用法

### <a name="command-line"></a>命令行

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>选项

#### <a name="database-name"></a>数据库名称
SQL Server 上站点数据库的名称。

#### <a name="delay-in-hours-for-summarization"></a>摘要延迟小时数
该工具汇总了延迟之前生成的软件计数使用情况。 默认情况下，此延迟为零。


### <a name="example"></a>示例

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>汇总 12 小时前生成的软件计数使用情况

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>另请参阅

- [维护任务](/sccm/core/servers/manage/maintenance-tasks)
- [使用软件计数监视应用使用情况](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)
