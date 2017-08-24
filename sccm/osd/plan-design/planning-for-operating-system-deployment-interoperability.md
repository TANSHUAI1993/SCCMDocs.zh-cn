---
title: "规划操作系统部署互操作性 | Microsoft Docs"
description: "了解单一层次结构中的不同 System Center Configuration Manager 站点使用不同版本时的互操作性问题。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划操作系统部署互操作性

*适用范围：System Center Configuration Manager (Current Branch)*

当单一层次结构中的不同 System Center Configuration Manager 站点使用不同版本时，某些 Configuration Manager 功能不可用。 通常，无法在站点上或通过运行较低版本的客户端访问 Configuration Manager 的较新版本中的功能。 有关详细信息，请参阅 [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)。  

 在升级层次结构中的顶层站点和升级层次结构中运行具有较低版本的 Configuration Manager 的其他站点时，请考虑以下事项：  

-   客户端安装包  

    -   会自动升级默认客户端安装包的来源，并使用新的客户端安装包更新层次结构中的所有分发点，即使在层次结构具有较低版本的站点处的分发点上也是如此。  

    -   无法将运行新版本的客户端分配给尚未升级到新版本的站点。 将在管理点处阻止分配。  

-   启动映像  

    -   将顶层站点升级到 Configuration Manager 的最新版本时，默认启动映像（x86 和 x64）会自动更新为使用 Windows PE 10 且基于适用于 Windows 10 的 Windows ADK 启动映像。 与默认启动映像关联的文件会使用这些文件的最新 Configuration Manager 版本进行更新。 自定义启动映像不会自动更新。 将需要手动更新自定义启动映像，其中包括旧版 Windows PE。  

    -   如果站点层次结构包含具有不同 Configuration Manager 版本的站点，则避免使用动态媒体。 相反，使用基于站点的媒体来联系特定的管理点，直到所有站点均升级到相同版本的 Configuration Manager 版本。  

    -   验证最新的 Configuration Manager 启动映像是否包含所需的自定义项，然后使用新的启动映像更新具有最新版 Configuration Manager 站点中的所有分发点。  

-   用户状态迁移工具 (USMT)  

    -   将顶层站点升级到 Configuration Manager 最新版本时，默认 USMT 包将自动更新为最新版本。 自定义 USMT 包不会自动更新。 将需要手动更新这些包。  

-   新建任务序列步骤  

    -   新任务序列步骤将定期引入到新版本的 Configuration Manager 中。 将具有新步骤的任务序列部署到较旧的客户端时，任务序列步骤将失败。 在部署具有新步骤的任务序列之前，请确保目标集合中的客户端都更新到最新版本。  

-   操作系统部署媒体  

    -   将站点更新到新版本时，必须使用新的 Configuration Manager 客户端包更新所有媒体（可启动媒体、捕获媒体、预留媒体和独立媒体）。  

-   操作系统部署的第三方扩展  

    -   当具有操作系统部署的第三方扩展且拥有不同版本的 Configuration Manager 站点或 Configuration Manager 客户端（即混合层次结构）时，扩展可能存在问题。  

 在主动升级层次结构中的站点时，请使用下列部分来帮助你进行操作系统部署。  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>混合层次结构中 Configuration Manager 站点的最新版本  
 将站点升级到 Configuration Manager 的最新版本时，引用默认客户端安装包的任务序列将自动启动，以部署最新 Configuration Manager 客户端版本。 引用自定义客户端安装包的任务序列将继续部署该自定义包中包含的客户端版本（可能是以前的 Configuration Manager 客户端版本），并且必须更新以避免任务序列部署失败。 如果有配置为使用自定义客户端安装包的任务序列，则必须更新任务序列步骤以使用客户端安装包的最新 Configuration Manager 版本，或更新自定义包以使用最新 Configuration Manager 客户端安装源。  

> [!IMPORTANT]  
>  不要将引用最新 Configuration Manager 客户端安装包的任务序列部署到较旧的 Configuration Manager 站点中的客户端。 当分配到较旧的 Configuration Manager 站点的客户端升级到最新的 Configuration Manager 客户端版本时，Configuration Manager 会阻止将客户端分配到较旧的 Configuration Manager 站点。 因此，在将客户端手动分配给最新的 Configuration Manager 站点或在计算机上重新安装客户端较旧的 Configuration Manager 版本之前，客户端将不再分配给任何站点，并处于不受管理状态。  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>混合层次结构中 Configuration Manager 的较旧版本  
 如果已将管理中心站点升级到 Configuration Manager 的最新版本，必须执行以下步骤，以确保部署到（已分配给较旧 Configuration Manager 站点的）客户端（尚未升级到 Configuration Manager 的最新版本）的操作系统部署任务序列未将这些客户端置于不受管理状态。  

-   创建一个将仅用于在 Configuration Manager 站点中部署到客户端的任务序列。 同样，你将建立用于在 Configuration Manager 站点的最新版本中部署到客户端的任务序列的副本，然后修改该任务序列，以便能够在较旧的 Configuration Manager 站点中的客户端。 然后，配置任务序列以引用使用较旧的 Configuration Manager 客户端安装源的自定义客户端安装包。 如果还没有一个引用较旧的 Configuration Manager 客户端安装源的自定义安装包，则必须手动创建该安装包。  
