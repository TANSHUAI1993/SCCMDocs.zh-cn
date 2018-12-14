---
title: Current Branch 版本
titleSuffix: Configuration Manager
description: 查看 Configuration Manager 的版本历史记录，并了解所提供服务的各个阶段。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35b5baec-d313-46aa-9d14-c443aa0d6c09
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd8116bc74f855fff956d0bb201691c741a6d351
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455982"
---
# <a name="support-for-configuration-manager-current-branch-versions"></a>对 Configuration Manager Current Branch 版本的支持

*适用范围：System Center Configuration Manager (Current Branch)*

Microsoft 计划每年发布几次 Configuration Manager Current Branch 的更新。 对于 1710 前发布的 Configuration Manager 版本，支持期为 12 个月。 从版本 1710 开始，每个更新版本从其公开发布日期起 18 个月内都保持支持状态。 Microsoft 会在整个支持期内始终提供技术支持。 有两个不同的服务阶段，具体取决于最新 Current Branch 版本的可用性。  

-   “安全和关键更新”服务阶段 - 运行最新的 Configuration Manager 版本时，你会同时收到安全更新和关键更新。  

-   “安全更新”（仅）服务阶段 - 新的 Current Branch 版本发布之后，Microsoft 在该版本支持生命周期的剩余时间内仅支持旧版本的安全更新（如图 1 所示）。  

 ![Configuration Manager 服务和支持时间线图](media/CM_Servicing_support_timeline1.png)  
图 1. Current Branch 服务支持发布周期重叠示例。 此示例用于说明该周期，并不代表实际或预期的发布日期。

> [!NOTE]  
>  最新 Current Branch 版本始终处于“安全更新和关键更新”服务阶段。 此支持声明意味着如果遇到需要关键更新的代码缺陷，则必须安装最新 Current Branch 版本才会接收修补程序。 所有其他受支持的 Current Branch 版本仅有资格接收安全更新。
> - 对于版本 1710 以及之后的版本，所有支持都会在 Current Branch 版本的 18 个月生命周期过期之后结束。
> - 对于 1706 及更早版本，将在 12 个月生命周期过期之后结束支持。
> 
> 在当前版本的支持到期之前，将 Configuration Manager 的环境更新到最新版本。

有关 Current Branch 版本的列表，请参阅[版本的详细信息](/sccm/core/servers/manage/updates#version-details)。

若要详细了解版本号以及作为控制台中更新或基线的可用性，请参阅[基线和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)。
