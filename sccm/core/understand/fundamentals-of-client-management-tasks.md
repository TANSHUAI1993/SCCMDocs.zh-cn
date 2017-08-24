---
title: "客户端管理基础知识 | Microsoft Docs"
description: "了解有关用于管理 System Center Configuration Manager 客户端运行的任务的详细信息。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fee4f4ba462e59859ac93c4218b67cb26bdd6f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的客户端管理任务基础

*适用范围：System Center Configuration Manager (Current Branch)*

安装 System Center Configuration Manager 客户端后，可以运行几个任务来管理客户端。  可从 Configuration Manager 控制台运行一些任务。 可从 Configuration Manager 客户端应用程序运行其他任务。 使用 Configuration Manager 客户端软件安装 Configuration Manager 客户端应用程序。

## <a name="configuration-manager-console-tasks"></a>Configuration Manager 控制台任务
 可在 Configuration Manager 控制台中执行不同的客户端管理任务：  

-   部署应用程序、软件更新、维护脚本和操作系统。 可将安装配置为在指定日期和时间进行，在用户请求时提供可供安装的软件，或配置要卸载的应用程序。  

-   帮助计算机抵御恶意软件和安全威胁，并在检测到问题时通知你。  

-   定义要监视并在违反符合性时修正的客户端配置的设置。  

-   收集硬件和软件清单信息，包括来自 Microsoft 的监视和协调许可证信息。  

-   使用远程控制对计算机进行故障排除。  

-   实施电源管理设置，以管理和监视计算机的功耗。  

Configuration Manager 控制台几乎可实时监视之前的任务。 Configuration Manager 控制台中提供每个任务的通知和状态信息。 若要捕获数据和分析历史趋势，请使用集成的 SQL Server Reporting Services 报表功能。 客户端将详细信息作为客户端状态提交给站点。  客户端状态信息提供客户端和客户端的活动运行状况的相关数据，并且可以在控制台中或使用 Configuration Manager 的内置报表查看此客户端状态信息。 此数据帮助识别未响应的计算机，而且在一些情况下可以自动修正问题。  

 有关客户端管理任务的详细信息，请参阅[如何在 System Center Configuration Manager 中管理客户端](../../core/clients/manage/manage-clients.md)和[如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 服务器客户端](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)。 若要了解报表的使用，请参阅   
            [System Center Configuration Manager 中的报表简介](../../core/servers/manage/introduction-to-reporting.md)。  

## <a name="configuration-manager-client-application"></a>Configuration Manager 客户端应用程序  
 安装 Configuration Manager 客户端软件时，同时也会安装 Configuration Manager 客户端应用程序。 与软件中心不同的是，Configuration Manager 客户端应用程序是为技术支持工程师而不是最终用户设计的。 使用某些配置选项需要本地管理权限，而且使用大部分选项都要求掌握有关 Configuration Manager 客户端应用程序工作原理的技术知识。 可以使用此应用程序在客户端上执行下列任务：  

-   查看有关客户端的属性，例如内部版本号、为它分配的站点、它与之通信的管理点以及客户端使用的是公钥基础结构 (PKI) 证书还是自签名证书。  

-   第一次安装客户端后，确认该客户端已成功安装客户端策略。 还要根据 Configuration Manager 控制台中配置的客户端设置，确认已按预期启用或禁用客户端设置。  

-   启动客户端操作。 例如，如果最近在 Configuration Manager 控制台中更改了配置，且不希望等到下次计划时间，则可以下载客户端策略。  

-   手动将客户端分配到 Configuration Manager 站点，或尝试查找站点。 然后为发布到 DNS 的管理点指定域名系统 (DNS) 后缀。  

-   配置临时存储文件的客户端缓存。 如果需要更多的磁盘空间来安装软件，则删除缓存中的文件。  

-   配置用于执行基于 Internet 的客户端管理的设置。  

-   查看已部署到客户端的配置基线，启动符合性评估，以及查看符合性报告。  
