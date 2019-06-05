---
title: 版本之间的互操作性
titleSuffix: Configuration Manager
description: 了解如何避免同一网络上多个 Configuration Manager 层次结构之间发生冲突。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51243f8df55f2736cfb053f9e38cc7b6716b2158
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354858"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>System Center Configuration Manager 不同版本之间的互操作性

适用范围：  System Center Configuration Manager (Current Branch)

可在同一网络上安装和运行多个独立的 System Center Configuration Manager 层次结构。 但是，由于 Configuration Manager 的各层次结构仅在迁移过程中进行交互，因此每个层次结构都需要配置以防止彼此间存在冲突。 此外，可创建某些配置，帮助所管理的资源与相应层次结构中的站点系统进行交互。  

下列部分提供有关在同一网络上使用不同版本的 Configuration Manager 的信息：  

- [System Center Configuration Manager 和 早期版本之间的互操作性](#BKMK_SupConfigInterop)  

- [Configuration Manager 控制台的互操作性](#BKMK_ConsoleInterop)  

- [混合版本层次结构中的 Configuration Manager 限制](#bkmk_mixed)  


## <a name="BKMK_SupConfigInterop"></a> System Center Configuration Manager 和 早期版本之间的互操作性  

不同版本的站点不能在同一 Configuration Manager 层次结构中共存。 唯一的例外是在以下升级方案过程中：

- 从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager
- 使用控制台中的更新从 System Center Configuration Manager 版本升级到较新版本

可以通过现有 System Center 2012 Configuration Manager 站点或者层次结构并排部署一个 System Center Configuration Manager 站点和层次结构。 计划阻止任一版本的客户端尝试从另一版本加入站点。

例如，如果两个或两个以上的 Configuration Manager 层次结构具有包含相同网络位置的[重叠边界](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)，那么请将每个新客户端分配给特定站点，而不是使用自动站点分配。 有关详细信息，请参阅[如何向站点分配客户端](/sccm/core/clients/deploy/assign-clients-to-a-site)。  

此外，不能将 System Center 2012 Configuration Manager 中的客户端安装到托管 System Center Configuration Manager 中的站点系统角色的计算机上。 也不能将 System Center Configuration Manager 客户端安装到托管 System Center 2012 Configuration Manager 中的站点系统角色的计算机上。  

不支持以下客户端和连接：  

- 任何 System Center 2012 Configuration Manager 或更早版本的计算机客户端  

- 任何 System Center 2012 Configuration Manager 或早期设备管理客户端  

- Windows CE Platform Builder 设备管理客户端（任意版本）  

- System Center Mobile Device Manager VPN 连接  

### <a name="BKMK_SupConfigSiteAssignment"></a> 客户端站点分配注意事项  

仅可将 Configuration Manager 客户端分配到单个主站点。 满足所有以下条件时，不能预测客户端的实际站点分配：

- 在客户端安装期间，使用自动站点分配将客户端分配到站点
- 多个边界组包括相同边界
- 边界组有不同的分配站点

如果多个 Configuration Manager 站点和层次结构之间的边界重叠，则可能不会将客户端分配到所期望的站点，或者根本不能分配到站点。  

System Center Configuration Manager 客户端会在完成站点分配之前检查站点版本。 如果站点边界重叠，则不能将客户端分配到使用以前版本的站点。 但是，早期版本的 System Center 2012 Configuration Manager 客户端可能会错误分配到更高版本的 System Center Configuration Manager 站点。  

为了防止在两个层次结构有重叠的边界时将客户端意外地分配到错误的站点，请配置客户端安装参数以将客户端分配到特定站点。  

## <a name="bkmk_mixed"></a> 混合版本层次结构中的 Configuration Manager 限制  

在升级 System Center Configuration Manager 层次结构时，有时不同的站点会拥有不同的版本。 例如，首先升级管理中心站点。 由于站点维护时段，要到以后的时间和日期才升级主站点。  

当单一层次结构中的不同站点使用不同版本时，某些功能不可用。 此行为可能会影响在 Configuration Manager 控制台中管理 Configuration Manager 对象的方式，并影响客户端可用的功能。 通常，无法在站点上或通过运行较低 Service Pack 版本的客户端访问 Configuration Manager 较新版本中的功能。  

### <a name="network-access-account"></a>网络访问帐户

将管理中心站点升级到 System Center Configuration Manager。 可以从连接到此更新站点的 Configuration Manager 控制台查看网络访问帐户的详细信息。 它不会显示仍运行 System Center 2012 Configuration Manager 的站点中的帐户详细信息。

将主站点升级到与管理中心站点相同的版本后，可在控制台中看到帐户详细信息。

在 System Center Configuration Manager 的不同版本之间进行更新时，也会应用相同行为。

### <a name="boot-images-for-os-deployment"></a>操作系统部署的启动映像

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-system-center-configuration-manager"></a>从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 时

层次结构的顶层站点升级到 System Center Configuration Manager 时，会自动更新默认启动映像以使用 Windows 评估和部署工具包 (ADK) 版本 10。 仅将这些启动映像用于对 System Center Configuration Manager 站点中客户端的部署。 有关详细信息，请参阅[规划操作系统部署互操作性](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability)。

#### <a name="when-upgrading-between-system-center-configuration-manager-versions"></a>当在 System Center Configuration Manager 各版本之间进行升级时

只要新版本的 Configuration Manager 不更新当前使用的 Windows ADK 版本，就不会对启动映像造成影响。

### <a name="new-task-sequence-steps"></a>新建任务序列步骤

使用某个 Configuration Manager 版本中介绍的步骤创建任务序列时（早期版本中不可用），可能会遇到下列问题：

- 尝试从运行 Configuration Manager 先前版本的站点编辑任务序列时出错。

- 在运行早期版本 Configuration Manager 客户端的计算机上，任务序列不运行。

### <a name="client-to-down-level-management-point-communications"></a>客户端到下层管理点的通信

对于与某个站点中的管理点通信的 Configuration Manager 客户端，如果该站点运行的版本比客户端低，则该客户端只能使用 Configuration Manager 的下层版本所支持的功能。 例如，如果将内容从近期升级的 System Center Configuration Manager 站点部署到与管理点通信的客户端，但该客户端尚未升级到此版本，则该客户端无法使用最新版本中的新增功能。

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>将包和任务序列部署到旧客户端

<!-- SCCMDocs-pr issue #3493 -->

从版本 1902 开始，不能将包或任务序列部署到客户端版本 5.7730 或更早版本。 若要解决此限制，请将客户端升级到更高版本。


## <a name="BKMK_ConsoleInterop"></a>Configuration Manager 控制台的互操作性  

本部分包含在具有 Configuration Manager 混合版本的环境中使用 Configuration Manager 控制台的相关信息。  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-system-center-configuration-manager"></a>同时具有 System Center 2012 Configuration Manager 和 System Center Configuration Manager 的环境

若要管理 Configuration Manager 站点，控制台及其连接到的站点必须运行相同版本的 Configuration Manager。 例如，无法使用 System Center 2012 Configuration Manager 控制台管理 System Center Configuration Manager 站点，反之亦然。

不支持在同一计算机上安装 System Center 2012 Configuration Manager 控制台和 System Center Configuration Manager 控制台。

### <a name="an-environment-with-multiple-versions-of-system-center-configuration-manager"></a>具有 System Center Configuration Manager 的多个版本的环境

System Center Configuration Manager 不支持在某一计算机上安装多个 Configuration Manager 控制台。 若要使用特定于 System Center Configuration Manager 的不同版本的多个控制台，请在单独的计算机上安装不同的控制台。

在将层次结构中的站点更新到新版本的过程中，你可以将控制台连接到运行更新的版本的站点，并查看关于该层次结构中其他站点的信息。 但是，不建议使用此配置。 控制台版本和 Configuration Manager 站点版本之间的差异可能会导致数据问题。 控制台中将不提供最新产品版本中提供的某些功能。

使用的控制台的版本与站点版本不匹配时，不支持对站点进行管理。 这样可能会导致数据丢失，并会将你的站点置于风险之中。 例如，不支持使用版本为 1610 的控制台来管理运行版本 1606 的站点。
