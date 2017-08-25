---
title: "结合使用 Configuration Manager 扩展互操作性客户端与 Current Branch | Microsoft Docs"
description: "了解如何将 Configuration Manager Long-Term Servicing Branch 中的客户端与 Current Branch 站点结合使用。"
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: robstackmsft
ms.author: robstack
ms.openlocfilehash: 6487a7c0eb958c74ca4c6a7233747966110eceb9
ms.sourcegitcommit: b41d3e5c7f0c87f9af29e02de3e6cc9301eeafc4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>使用 Configuration Manager 客户端软件，实现与未来 Current Branch 站点版本的扩展互操作性

*适用范围：System Center Configuration Manager (Current Branch) 和 (Long-Term Servicing Branch)*  

在某些情况下，公司策略可能不允许定期更新某些电脑上的 Configuration Manager 客户端。 例如，可能需要遵守变更管理策略，或设备可能是任务关键型。

虽然应尽可能继续对大多数客户端使用自动客户端升级，但自 Configuration Manager 更新 1610 起，也可以安装名为扩展互操作性客户端 (EIC) 的新客户端，以供长期使用，从而满足这些需求。

EIC 与运行版本 1610 或更高版本的 Configuration Manager 站点兼容。 EIC 应仅用于无法经常更新的特定电脑，如展台或销售点设备。 对其他所有电脑使用最新的 Configuration Manager 客户端。

## <a name="how-this-scenario-works"></a>此方案的工作原理

通常，为 Current Branch 安装新的控制台内更新时，客户端会自动更新其客户端软件以使用这些新功能。

在此方案中，使用 Current Branch 并接收最新功能和更新。 大多数客户端从 Current Branch 运行客户端软件，并可使用每个已安装的版本更新来更新客户端软件。 但在不想接收客户端软件更新的关键系统子集上，安装扩展互操作性客户端。 在显式部署新版客户端软件之前，此类客户端不会安装新的客户端软件。

>[!IMPORTANT]
>Current Branch 站点必须运行版本 1610 或更高版本。

## <a name="how-to-use-the-eic"></a>如何使用 EIC

1. 从 Configuration Manager 1606 更新安装介质的 \SMSSETUP\Client 文件夹获取 EIC（客户端版本 5.00.8412）。 请务必复制文件夹的全部内容。
2. 在这些设备上手动安装 EIC。 [详细了解如何手动安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)。
3. 从客户端升级中排除此集合。

>[!TIP]
>若要在批量许可服务中心 (VLSC) 查找 System Center Configuration Manager 版本 1606，请转到 [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) 的“下载和密钥”选项卡，搜索“system center config”，然后选择“System Center Config Mgr (当前分支和 LTSB)”。

## <a name="the-extended-interoperability-client-software"></a>扩展互操作性客户端

2018 年 11 月 18 日前，当前 EIC 可继续与更新后的 Configuration Manager Current Branch 版本结合使用。 此后，请查看此页面，了解新 EIC 的详细信息，或对现有 EIC 的支持扩展。

>[!TIP]
>EIC 支持期为版本发布后至少两年（请参阅[对 System Center Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)）。 例如，对当前 EIC 的支持期为 1610 版本发布后的两年，即 2018 年 11 月 18 日停止支持。

计划在客户端到期之前，在使用 Current Branch 管理的设备上更新扩展互操作性客户端。 为此，请从 Microsoft 下载新版客户端，再在使用当前扩展互操作性客户端的设备上，部署更新后的客户端软件。

## <a name="limitations-of-the-extended-interoperability-client"></a>扩展互操作性客户端的限制

- 扩展互操作性客户端软件的更新不可通过控制台内更新进行。 在更新后的客户端发布时，将提供有关部署更新后的客户端软件的更多详细信息。
- EIC 仅支持软件更新、清单、包和程序。

## <a name="next-steps"></a>后续步骤

请按照[如何监视客户端](/sccm/core/clients/manage/monitor-clients)中的说明操作，确保客户端已正确安装到所需设备上。
