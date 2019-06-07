---
title: OS 部署互操作性
titleSuffix: Configuration Manager
description: 了解单一层次结构中的不同 System Center Configuration Manager 站点使用不同版本时的互操作性问题。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d4f6275ede2a751acb8ca14d7b8b6ad307e78bd
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355018"
---
# <a name="plan-for-os-deployment-interoperability"></a>规划 OS 部署互操作性

*适用范围：System Center Configuration Manager (Current Branch)*

当单一层次结构中的不同 System Center Configuration Manager 站点使用不同版本时，某些 Configuration Manager 功能不可用。 通常，无法在运行较低版本的站点上或通过运行较低版本的客户端访问较新版本 Configuration Manager 中的功能。 有关详细信息，请参阅 [System Center Configuration Manager 不同版本之间的互操作性](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions)。  


## <a name="objects"></a>对象

在升级层次结构中的顶层站点和升级层次结构中运行较低版本的 Configuration Manager 的其他站点时，请考虑以下对象：  

### <a name="client-installation-package"></a>客户端安装包  

- 默认客户端安装包的源会自动升级。 系统会使用新的客户端安装包更新层次结构中的所有分发点。 即使在层次结构中版本较低的站点中的分发点上，也会发生此行为。  

- 你无法将新版客户端分配给尚未升级到新版本的站点。 将在管理点处阻止分配。  

### <a name="boot-images"></a>启动映像  

- 将顶层站点升级到 Configuration Manager 最新版本时，它会自动更新默认启动映像（x86 和 x64）。 此更新使用适用于 Windows 10 的 Windows ADK，其中包括 Windows PE 10。 与默认启动映像关联的文件会使用这些文件的最新 Configuration Manager 版本进行更新。 该站点不会自动更新自定义启动映像。 你需要手动更新自定义启动映像，其中包括旧版 Windows PE。  

- 如果站点层次结构包含具有不同 Configuration Manager 版本的站点，请勿使用动态媒体， 而是使用基于站点的媒体来联系特定的管理点。 将所有站点更新到相同的 Configuration Manager 版本后，可以再次使用动态媒体。

- 确保最新的 Configuration Manager 启动映像包含你的自定义项。 然后使用最新版本的新启动映像更新新版站点中的所有分发点。  

### <a name="user-state-migration-tool-usmt"></a>用户状态迁移工具 (USMT)  

将顶层站点升级到 Configuration Manager 最新版本时，它会将默认 USMT 包自动更新为最新版本。 它不会自动更新任何自定义 USMT 包。 你需要手动更新这些包。  

### <a name="new-task-sequence-steps"></a>新建任务序列步骤  

新任务序列步骤将定期引入到新版本的 Configuration Manager 中。 将具有新步骤的任务序列部署到较旧的客户端时，该任务序列步骤将失败。 在部署具有新步骤的任务序列之前，请确保目标集合中的客户端都更新到最新版本。  

### <a name="os-deployment-media"></a>OS 部署媒体  

将站点更新为新版本后，使用新的 Configuration Manager 客户端包更新所有媒体。 这些媒体类型包括可启动媒体、捕获媒体、预安排媒体和独立媒体。

### <a name="third-party-extensions-to-os-deployment"></a>OS 部署的第三方扩展  

当具有 OS 部署的第三方扩展且拥有不同版本的 Configuration Manager 站点或 Configuration Manager 客户端时，扩展可能存在问题。  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>混合层次结构中 Configuration Manager 站点的最新版本  

将站点升级到 Configuration Manager 最新版本时，引用默认客户端安装包的任务序列将自动启动，以部署最新 Configuration Manager 客户端版本。

引用自定义客户端安装包的任务序列将继续部署该自定义包中包含的客户端版本。 自定义包可能包含以前的 Configuration Manager 客户端版本。 若要避免任务序列部署失败，请将所有自定义客户端安装包都更新到最新版本。

将任务序列配置为使用自定义客户端安装包时，请执行以下操作之一：

- 将任务序列步骤更新为使用客户端安装包的最新 Configuration Manager 版本
- 将自定义包更新为使用最新的 Configuration Manager 客户端安装源

> [!IMPORTANT]  
> 不要将引用最新 Configuration Manager 客户端安装包的任务序列部署到较旧的 Configuration Manager 站点中的客户端。 当分配到较旧的 Configuration Manager 站点的客户端升级到最新的 Configuration Manager 客户端版本时，Configuration Manager 会阻止将客户端分配到较旧的 Configuration Manager 站点。 这些客户端不再分配给任何站点。 在将客户端手动分配给最新的 Configuration Manager 站点，或在计算机上重新安装客户端较旧的 Configuration Manager 版本之前，这些客户端处于不受管理状态。


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>混合层次结构中的旧版 Configuration Manager  

将管理中心站点升级到 Configuration Manager 最新版本时，请确保部署的 OS 部署任务序列未将这些客户端置于不受管理状态。 例如，如果部署到分配给较旧 Configuration Manager 站点（尚未升级到 Configuration Manager 最新版本）的客户端。

创建用于部署到最新版 Configuration Manager 站点中的客户端的任务序列的副本。 然后修改该任务序列，以便将其部署到较旧 Configuration Manager 站点中的客户端。 将该任务序列配置为引用使用较旧 Configuration Manager 客户端安装源的自定义客户端安装包。 如果还没有引用较旧 Configuration Manager 客户端安装源的自定义客户端安装包，请手动创建一个。  

> [!Important]  
> 从版本 1902 开始，不能将包或任务序列部署到客户端版本 5.7730 或更早版本。 若要解决此限制，请将客户端升级到更高版本。<!-- SCCMDocs-pr issue #3493 -->
