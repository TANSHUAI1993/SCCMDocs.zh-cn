---
title: "1511、1602 和 1606 的边界组 | System Center Configuration Manager"
description: "通过 1511、1602 和 1606 版 Configuration Manager 使用边界组。"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b64f1f06af1ab4a255b6291b6eb5f85cff99ae63
ms.openlocfilehash: ef408041eb6d0d6716e244d34b9a2a4ebe5cb9cc


---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>System Center Configuration Manager 1511、1602 和 1606 版的边界组

*适用范围：System Center Configuration Manager (Current Branch)*

本主题中的信息特定于通过 1511、1602 和 1606 版 System Center Configuration Manager 使用边界组。
如果使用的是 1610 或更高版本，请参阅*定义站点边界和边界组或 System Center Configuration Manager* 中的[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-group/)，了解如何使用重新设计的边界组。  


##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 将边界组创建为以逻辑方式对相关的网络位置（边界）进行分组，以便可以更轻松的管理你的基础结构。 你必须将边界分配给边界组，然后才能使用边界组。 客户端使用边界组配置用于：  

-   自动站点分配  

-   内容位置  

-   首选管理点（若要使用首选管理点，则必须为层次结构启用此选项，但不是从边界组配置中启用。 请参阅以下过程 “若要启用对首选管理点的使用”）  

在配置边界组时，你将一个或多个边界添加到该边界组，然后配置其他设置以供位于这些边界上的客户端使用。  

#### <a name="to-create-a-boundary-group"></a>创建边界组  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” >  “边界组”。  

2.  在“主页”  选项卡上的“创建”  组中，单击“创建边界组” 。  

3.  在“创建边界组”  对话框中，选择“常规”  选项卡，并为此边界组指定“名称”  。  

4.  单击“确定”  保存新边界组。  

#### <a name="to-configure-a-boundary-group"></a>配置边界组  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” >  “边界组”。  

2.  选择要修改的边界组。  

3.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

4.  在边界组的“属性”  对话框中，选择“常规”  选项卡以修改作为此边界组成员的边界：  

    -   要添加边界，请单击“添加” ，选中一个或多个边界的复选框，并单击“确定” 。  

    -   要删除边界，请选择边界并单击“删除” 。  

5.  选择“引用”  选项卡以修改站点分配和关联的站点系统服务器配置：  

    -   要启用此边界组以供站点分配的客户端使用，请选中“将此边界组用于站点分配” 复选框，然后从“分配的站点”  下拉框中选择一个站点。  

    -   配置与此边界组关联的可用站点系统服务器：  

    1.  单击“添加” ，然后选中一个或多个服务器的复选框。 将服务器添加为此边界组的关联站点系统服务器。 仅在其上安装有受支持的站点系统角色的服务器可用。  

        > [!NOTE]  
        >  你可从层次结构中的任何站点选择可用站点系统的任意组合。 所选的站点系统列在作为此边界组成员的每个边界的属性中的“站点系统”  选项卡上。  

    2.  要从此边界组中删除服务器，请选择该服务器，然后单击“删除” 。  

        > [!NOTE]  
        >  要停止为关联的站点系统使用此边界组，则必须删除列为关联站点系统服务器的所有服务器。  

    3.  要更改此边界组站点系统服务器的网络连接速度，请选择该服务器，然后单击“更改连接” 。  

         默认情况下，每个站点系统的连接速度为“快” ，但可更改为“慢” 。 网络连接速度和部署的配置确定客户端是否能够从服务器下载内容。  

6.  单击“确定”  关闭边界组属性并保存配置。  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>将内容部署服务器或管理点与边界组关联  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” >  “边界组”。  

2.  选择要修改的边界组。  

3.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

4.  在边界组的“属性”  对话框中，选择“引用”  选项卡。  

5.  在“选择站点系统服务器” 下，单击“添加” ，选中要与此边界组关联的站点系统服务器的复选框，然后单击“确定” 。  

6.  单击“确定”  关闭对话框并保存边界组配置。  

#### <a name="to-enable-use-of-preferred-management-points"></a>若要启用对首选管理点的使用  

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”，然后在“主页”选项卡上选择“层次结构设置”。  

2.  在“层次结构设置”的“常规”  选项卡上，选择“客户端首选使用边界组中指定的管理点” 。  

3.  单击“确定”  关闭对话框并保存配置。  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>为自动站点分配配置回退站点  

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” >  “站点”。  

2.  在“主页”  选项卡上的“站点”  组中，单击“层次结构设置” 。  

3.  在“常规”  选项卡上，选中“使用回退站点” 复选框，然后从“回退站点”  下拉列表中选择一个站点。  

4.  单击“确定”  保存配置。  

 下列部分提供了有关边界组配置的其他详细信息。  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> 有关站点分配  
 你可以使用客户端的分配的站点配置每个边界组。  

-   使用自动站点分配的新安装的客户端将加入包含客户端当前网络位置的边界组的分配的站点。  

-   分配到站点后，当更改其网络位置时，客户端不会更改其站点分配。 例如，客户端漫游到由具有不同站点分配的边界组中的某个边界表示的新网络位置，则该客户端的分配的站点将保持不变。  

-   当 Active Directory 系统发现发现新资源时，将依据边界组的边界对所发现的资源的网络信息进行评估。 此过程将新资源与分配的站点关联，以供客户端请求安装方法使用。  

-   当边界是具有不同分配站点的多个边界组的成员时，客户端将随机选择其中一个站点。  

-   对分配了边界组的站点的更改仅适用于新的站点分配操作。 以前分配给站点的客户端不会根据对边界组的配置（或它们自身网络位置）的更改重新评估其站点分配。  

有关客户端站点分配的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端分配到一个站点](../../../../core/clients/deploy/assign-clients-to-a-site.md)中的[对计算机使用自动站点分配](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)。  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> 有关内容位置  
 你可以使用一个或多个分发点和状态迁移点配置每个边界组，并可将相同的分发点和状态迁移点与多个边界组关联。  

-   **在软件分发过程中**，客户端请求用于部署内容的位置。 Configuration Manager 将向客户端发送包括客户端当前网络位置的每个边界组关联的分发点列表。  

-   **在操作系统部署期间，客户端** 请求用以发送或接收其状态迁移信息的位置。 Configuration Manager 将向客户端发送包括客户端当前网络位置的每个边界组关联的状态迁移点列表。  

此行为使客户端能够选择从中传输内容或站点迁移信息的最近的服务器。  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> 关于首选管理点  
 首选管理点使客户端能够识别与当前网络位置（边界）关联的管理点。  

-   客户端先尝试使用分配的站点中的首选管理点，然后再使用分配的站点中未配置为首选的管理点。  

-   若要使用此选项，必须为层次结构启用该选项，并将各主站点的边界组配置为包括应与边界组的关联边界相关联的管理点  

-   配置了首选管理点后，客户端在组织其管理点列表时将首选管理点放置于其分配的管理点列表（其中包括该客户端的分配的站点中的所有管理点）的顶部  

> [!NOTE]  
>  当客户端漫游时（这意味着更改其网络位置，例如，便携式计算机前往远程办公地点时），在尝试使用其分配的站点中的管理点（其中包括首选管理点）之前，它可能会使用来自其新位置的本地站点中的管理点（或代理管理点）。  有关详细信息，请参阅[了解客户端如何查找 System Center Configuration Manager 的站点资源和服务](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> 有关重叠边界  
 Configuration Manager 对于内容位置支持重叠边界配置：  

-   **当客户端请求内容**，并且客户端网络位置属于多个边界组时，Configuration Manager 将向客户端发送具有内容的所有分发点的列表。  

-   **当客户端请求服务器发送或接收其状态迁移信息**，并且客户端网络位置属于多个边界组时，Configuration Manager 将向客户端发送与包括客户端当前网络位置的边界组关联的所有状态迁移点的列表。  

此行为使客户端能够选择从中传输内容或站点迁移信息的最近的服务器。  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> 有关网络连接速度  
 你可以为边界组中的每个站点系统服务器设置网络连接速度。 此设置适用于基于此边界组配置连接到站点系统的客户端。 同一站点系统服务器在不同的边界组中可设置不同的连接速度。  

 默认情况下，网络连接速度配置为“快” ，但也可将其配置为“慢” 。 网络连接速度和部署配置确定当客户端位于关联的边界组中时是否能从分发点下载内容。  

 有关网络连接速度配置如何影响客户端获取内容的方式的详细信息，请参阅[内容管理的基本概念](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  



<!--HONumber=Dec16_HO3-->


