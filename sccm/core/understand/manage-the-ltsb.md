---
title: "管理 LTSB | Microsoft Docs"
description: "System Center Configuration Manager 的 LTSB 的管理差异。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>管理 Configuration Manager 的 Long Term Servicing Branch

*适用范围：System Center Configuration Manager (Long-Term Servicing Branch)*

使用 System Center Configuration Manager 的 Long Term Servicing Branch (LTSB) 时，可以参阅下列内容，了解会对基础结构管理方式产生影响的重要更改。

因为 LTSB 等效于 Current Branch 版本 1606（一些例外情况除外，如 Intune 集成和云相关功能），所以大部分规划、部署、配置和日常管理任务都是相同的。

例如，LTSB 和 Current Branch 支持相同的站点数、站点类型、客户端以及一般基础结构。 因此，可以使用站点中的指南以及适用于 Current Branch 的层次结构规划和设计主题。 同样，对于这两个分支都支持的 LTSB 功能（如软件更新或操作系统部署），可以参阅 Current Branch 文档中相关部分的指南，但请注意，无法查看 Current Branch 版本 1606 之后引入的功能更改。

以下各部分介绍了不相似的管理任务。

## <a name="updates-and-servicing"></a>更新和服务
LTSB 中仅提供作为控制台中更新的关键安全更新。  

控制台中显示后续 Current Branch 版本的定期更新信息，但不向 LTSB 提供这些信息。 无法下载和安装它们。

若要支持关键安全修补程序的控制台中更新，LTSB 站点要求使用[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 可以在脱机或联机模式下配置此站点系统角色，这与在 Current Branch 中相同。 与 Current Branch 相同，LTSB 会收集并提交遥测和使用情况数据。

LTSB 支持使用修补程序安装程序和更新注册工具，这与 Current Branch 相同。

有关更新和服务的常规信息，请参阅 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)。


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>站点扩展和 CD.Latest 文件夹的更改
如果运行 LTSB 且要通过安装新的管理中心站点扩展独立主站点，必须使用 1606 版基线介质中的安装程序和源文件。 对于 Current Branch，运行 CD.Latest 文件夹中的安装程序并使用此文件夹中的源文件。

虽然不从 CD.Latest 文件夹运行安装文件用于站点扩展，但仍将 CD.Latest 文件夹用于站点恢复，并且当第一个 LTSB 是管理中心站点时，仍安装新的子主站点。

若要详细了解网站扩展，请参阅[扩展独立主网站](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)。 有关 CD.Latest 文件夹的详细信息，请参阅 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)。


## <a name="recovery"></a>恢复
恢复网站时，必须将网站或网站数据库还原到其原始分支中。 无法将 Current Branch 站点数据库恢复到 LTSB 安装，反之亦然。
