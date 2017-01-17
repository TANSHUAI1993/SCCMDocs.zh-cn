---
title: "Configuration Manager 版本之间的互操作性 | Microsoft Docs"
description: "了解如何避免同一网络上多个 System Center Configuration Manager 层次结构之间发生冲突。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 32182f06a90d768c40e29ed8a8e89cb45114bd15


---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>System Center Configuration Manager 不同版本之间的互操作性

*适用范围：System Center Configuration Manager (Current Branch)*

支持在同一网络上安装和运行多个独立的 System Center Configuration Manager 层次结构。 但是，由于不同的 Configuration Manager 层次结构不会在迁移外部交互操作，因此每个层次结构都需要配置以防止相互之间冲突。 此外，你可以进行某些配置来帮助你所管理的资源与正确层次结构中的站点系统交互。  

 下列部分提供有关在同一网络上使用不同版本的 Configuration Manager 的信息：  

-   [System Center Configuration Manager 和 早期版本之间的互操作性](#BKMK_SupConfigInterop)  

-   [Configuration Manager 控制台的互操作性](#BKMK_ConsoleInterop)  

-   [混合版本层次结构中的 Configuration Manager 限制](#bkmk_mixed)  

##  <a name="a-namebkmksupconfiginteropa-interoperability-between-system-center-configuration-manager-and-earlier-product-versions"></a><a name="BKMK_SupConfigInterop"></a> System Center Configuration Manager 和 早期版本之间的互操作性  
 除了在从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 或从某一 System Center Configuration Manager 版本升级到较新版本（使用控制台内更新）期间外，不同版本的站点无法同时存在于同一层次结构中。  

 因为可以通过现有 System Center 2012 Configuration Manager 站点或者层次结构并排部署一个 System Center Configuration Manager 站点和层次结构，计划阻止其他版本的客户端试图从一个站点加入另一个站点。 例如，如果两个或更多 Configuration Manager 层次结构具有包含相同网络位置的重叠边界（见[有关重叠边界](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md#BKMK_BoundaryOverlap)），则最好将每个新客户端分配给特定站点，而不是使用自动站点分配。 有关 System Center 2012 Configuration Manager 中自动站点分配的信息，请参阅 [如何在 System Center Configuration Manager 中将客户端分配到一个站点](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

 此外，不支持在托管 System Center Configuration Manager 中的站点系统角色的计算机上从 System Center 2012 Configuration Manager 安装客户端，也不支持在托管 System Center 2012 Configuration Manager 中的站点系统角色的计算机上安装 System Center Configuration Manager 客户端。  

 类似地，以下客户端和虚拟专用网 (VPN) 连接不受支持：  

-   任何 System Center 2012 Configuration Manager 或更早版本的计算机客户端  

-   任何 System Center 2012 Configuration Manager 或早期设备管理客户端  

-   Windows CE Platform Builder 设备管理客户端（任意版本）  

-   System Center Mobile Device Manager VPN 连接  

###  <a name="a-namebkmksupconfigsiteassignmenta-client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> 客户端站点分配注意事项  
 仅可将 System Center Configuration Manager 客户端分配到单个主站点。 当在客户端安装期间使用自动站点分配将客户端分配到站点，多个边界组包括相同的边界，并且边界组有不同的已分配站点时，将无法预测客户端的实际站点分配。  

 如果多个 Configuration Manager 站点和层次结构之间的边界重叠，则可能不会将客户端分配到所期望的站点，或者根本不能分配到站点。  

 System Center Configuration Manager 客户端将在完成站点分配之前检查 Configuration Manager 站点的版本，如果边界重叠，则无法分配到早期版本。 但是，System Center 2012 Configuration Manager 客户端可能会错误分配到 System Center Configuration Manager 站点。  

 为了防止在两个层次结构有重叠的边界时将客户端意外地分配到错误的站点，请配置 Configuration Manager 客户端安装参数以将客户端分配到特定站点。  

##  <a name="a-namebkmkmixeda-configuration-manager-limitations--in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> 混合版本层次结构中的 Configuration Manager 限制  
 在升级 System Center Configuration Manager 站点的过程中，有时不同的站点会位于不同的版本中。  例如，可能会将管理中心站点升级到新版本，但由于站点维护窗口，需要一段时间以后才能升级一个或多个主站点。  

 当单一层次结构中的不同站点使用不同版本时，某些功能不可用。 这可能会影响在 Configuration Manager 控制台中管理 Configuration Manager 对象的方式，并影响客户端可用的功能。 通常，无法在站点上或通过运行较低 Service Pack 版本的客户端访问 Configuration Manager 较新版本中的功能。  

### <a name="limitations-when-upgrading--configuration-manager"></a>升级 Configuration Manager 的限制  

|对象|详细信息|  
|------------|-------------|  
|网络访问帐户|**从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 时：**使用连接到已更新为 System Center Configuration Manager 的管理中心站点的 Configuration Manager 控制台来查看网络访问帐户详细信息时，控制台不显示在运行 System Center 2012 Configuration Manager 的主站点配置的帐户的详细信息。 主站点升级到与管理中心站点相同的版本后，将可在控制台中看到帐户详细信息。<br /><br /> **在 System Center Configuration Manager 版本之间进行升级时：**使用连接到已更新为新版本 System Center Configuration Manager 的管理中心站点的 Configuration Manager 控制台以查看网络访问帐户详细信息时，控制台不显示在运行旧版本的主站点进行配置的帐户的详细信息。 主站点升级到与管理中心站点相同的版本后，将可在控制台中看到帐户详细信息。|  
|操作系统部署的启动映像|**从 System Center 2012 Configuration Manager 升级到 System Center Configuration Manager 时：**层次结构的顶层站点升级到 System Center Configuration Manager 时，默认启动映像会自动更新为基于 Windows ADK 10 的启动映像。 仅将这些启动映像用于对 System Center Configuration Manager 站点中客户端的部署。 有关详细信息，请参阅[在 System Center Configuration Manager 中规划操作系统部署互操作性](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)。<br /><br /> **在 System Center Configuration Manager 各版本之间升级时：**只要新版本的 cm6long 未更新正在使用的 Windows ADK 版本，就不会对启动映像造成影响。|  
|新建任务序列步骤|创建包含某版本的 Configuration Manager 中引入的任务序列步骤的任务序列时，可能会遇到下列问题：<br /><br /> --   当尝试从运行以前版本的 Configuration Manager 站点编辑任务序列时，就会出错。<br /><br /> -- 在运行早期版本 Configuration Manager 客户端的计算机上将不运行任务序列。|  
|客户端到下层管理点的通信|对于与某个站点中的管理点通信的 Configuration Manager 客户端，如果该站点运行的版本比客户端低，则该客户端只能使用 Configuration Manager 的下层版本所支持的功能。 例如，如果将内容从最近更新的 System Center Configuration Manager 站点部署到与管理点通信的客户端，而该客户端尚未升级到该版本，则该客户端无法使用最新版本的新功能。|  

##  <a name="a-namebkmkconsoleinteropa-interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Configuration Manager 控制台的互操作性  
 下表包含在具有 Configuration Manager 混合版本的环境中使用 Configuration Manager 控制台的相关信息。  

|互操作性环境|更多信息|  
|----------------------------------|----------------------|  
|同时具有 System Center 2012 Configuration Manager 和 System Center Configuration Manager 的环境|若要管理 Configuration Manager 站点，控制台及其连接到的站点必须运行相同版本的 Configuration Manager。 例如，无法使用 System Center 2012 Configuration Manager 控制台管理 System Center Configuration Manager 站点，反之亦然。<br /><br /> 不支持在同一计算机上安装 System Center 2012 Configuration Manager 控制台和 System Center Configuration Manager 控制台。|  
|具有 System Center Configuration Manager 的多个版本的环境|System Center Configuration Manager 不支持在某一计算机上安装多个 Configuration Manager 控制台。 若要使用特定于 System Center Configuration Manager 的不同版本的多个控制台，必须在单独的计算机上安装不同的控制台。<br /><br /> 在升级层次结构中的站点过程中，你可以将控制台连接到运行更新的版本的站点，并查看关于该层次结构中其他站点的信息。 但是，不建议使用此配置，因为控制台版本和 Configuration Manager 站点版本之间的差异可能导致数据问题，且某些在最新产品版本中可用的功能在控制台中不可用。|  



<!--HONumber=Dec16_HO3-->


