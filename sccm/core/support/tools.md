---
title: Configuration Manager 工具
titleSuffix: Configuration Manager
description: 了解可帮助管理 Configuration Manager 基础结构并对其进行故障排除的工具。
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b3324189cdf482684cc0738c51fbf336a65ee221
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500690"
---
# <a name="configuration-manager-tools"></a>Configuration Manager 工具

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 工具包括[基于客户端的工具](#client-tools)和[基于服务器的工具](#server-tools)。 使用这些工具，帮助管理 Configuration Manager 基础结构并对其进行故障排除。

从 Configuration Manager 版本 1806 开始，这些工具包含在站点服务器上的 `CD.Latest\SMSSETUP\Tools` 文件夹中。 无需进行其他安装。<!--1357145--> 将这些版本的工具与 Configuration Manager 版本 1806 及更高版本一起使用。

所有在[客户端和设备支持的操作系统](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中列为受支持客户端的 Windows 操作系统均支持使用这些工具。

> [!Note]  
> 仍可从 Microsoft 下载中心获取 [System Center 2012 R2 Configuration Manager 工具包](https://www.microsoft.com/en-us/download/details.aspx?id=50012)。 对于 Configuration Manager 版本 1806 及更高版本，在站点服务器上的 CD.Latest 文件夹中使用这些版本的工具。 有些工具之前位于工具包中，但不包括在版本 1806 中。 不再支持这些旧工具。


## <a name="client-tools"></a>客户端工具

- [CMTrace](/sccm/core/support/cmtrace)：查看、监视并分析 Configuration Manager 日志文件  

- [客户端 Spy](/sccm/core/support/clispy)：对与软件分发、清单和计数相关的问题进行故障排除

- [部署监视工具](/sccm/core/support/deployment-monitoring-tool)：对应用程序、更新和基线部署进行故障排除  

- [策略监视](/sccm/core/support/policy-spy)：查看策略分配  

- [电源查看器工具](/sccm/core/support/power-viewer-tool)：查看电源管理功能状态  

- [发送计划工具](/sccm/core/support/send-schedule-tool)：触发配置基线的计划和评估  

> [!Note]  
> ClientTools 文件夹还包含文件 Microsoft.Diagnostics.Tracing.EventSource.dll。 好几个客户端工具都需要此库。 不能直接使用它。  


## <a name="server-tools"></a>服务器工具

- [DP 作业队列管理器](/sccm/core/support/dp-job-manager)：对面向分发点的内容分发作业进行故障排除  

- [集合评估查看器](/sccm/core/support/ceviewer)：查看集合评估详细信息  

- [内容库资源管理器](/sccm/core/support/content-library-explorer)：查看内容库单一实例存储的内容  

- [内容库转让](/sccm/core/support/content-library-transfer)：在驱动器之间转让内容库  

- [内容所有权工具](/sccm/core/support/content-ownership-tool)：更改孤立包的所有权。 这些包存在于没有自有站点服务器的站点。  

- [基于角色的管理和审核工具](/sccm/core/support/rbaviewer)：帮助管理员审核角色配置  

- [运行计量摘要工具](/sccm/core/support/run-meter-summ)：运行计数摘要任务并分析计量数据

> [!Note]  
> ServerTools 文件夹还包括以下文件：
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> 好几个服务器工具都需要这些库。 不能直接使用它们。  



## <a name="other-tools-and-toolkits"></a>其他工具和工具包

- [内容库清理工具](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool)：使用 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中的 ContentLibraryCleanup.exe 来从分发点删除孤立的内容。  

- [层次结构维护工具](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe)：使用站点服务器上 `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` 共享文件夹中的 Preinst.exe 将命令传送到层次结构管理器组件。  

- [更新重置工具](/sccm/core/servers/manage/update-reset-tool)：在控制台中更新出现下载或复制问题时，可使用 `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` 中的 CMUpdateReset.exe 修复这些问题。  

- [服务连接工具](/sccm/core/servers/manage/use-the-service-connection-tool)：服务连接点处于脱机状态时，可使用 `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` 中的 ServiceConnectionTool.exe 使站点保持最新状态。  

- [支持中心](/sccm/core/support/support-center)：进行故障排除时，请从客户端收集信息以便于分析。

- [Microsoft Deployment Toolkit (MDT)](/sccm/mdt/)：一系列工具、流程和指南，用于自动执行桌面和服务器 OS 部署。

- [System Center Updates Publisher (SCUP)](/sccm/sum/tools/updates-publisher)：用于管理和导入自定义软件更新的独立工具。

- [安全内容自动化协议 (SCAP) 扩展](/sccm/compliance/plan-design/scap/about-scap)：分析和评估你的环境与 NIST 基线的符合性。

- [包转换管理器](/sccm/apps/pcm/package-conversion-manager)：将旧包转换为应用程序。
