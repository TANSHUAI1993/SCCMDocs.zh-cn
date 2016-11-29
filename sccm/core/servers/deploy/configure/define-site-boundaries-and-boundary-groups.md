---
title: "定义站点边界 | System Center Configuration Manager"
description: "了解如何在 Intranet 上定义可包含你要管理的设备的网络位置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 定义站点边界和边界组

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 的边界在 Intranet 上定义可包含你要管理的设备的网络位置。 边界组是你所配置的边界的逻辑分组。 边界组和边界在整个层次结构中可用，并且你不为单独的站点配置边界和边界组。  

 层次结构可以包含任意数量的边界组，每个边界组可以包含以下边界类型的任意组合：  

-   IP 子网，  

-   Active Directory 站点名称  

-   IPv6 前缀  

-   IP 地址范围  

Intranet 上的客户端评估其当前网络位置，然后使用该信息确定它们所属的边界组。  

 客户端使用边界组以：  

-   **查找分配的站点：** 边界组使客户端能够为客户端分配（自动站点分配）查找主站点。  

-   **查找可以使用的某些站点系统角色：**  当你将边界组与某些站点系统角色相关联时，边界组向客户端提供在内容定位期间以及作为首选管理点使用的站点系统的列表。  

位于 Internet 上或配置为仅 Internet 的客户端不使用边界信息。 这些客户端无法使用自动站点分配，并可始终从为其分配的站点中的任何分发点下载内容（如果分发点配置为允许来自 Internet 的客户端连接）。  


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> 边界  
 你可以手动创建单个边界。 此外，还可以将 [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) 配置为自动发现并为每个 IP 子网和其发现的 Active Directory 站点创建边界。  

-   每个边界都表示其中的一个网络位置，并可被层次结构中的每个站点使用。  

-   Configuration Manager 不支持以边界的形式直接输入超网。 作为替代，请使用 IP 地址范围边界类型。  

-   当 Active Directory 林发现确定分配给 Active Directory 站点的超网时，Configuration Manager 将超网转换为 IP 地址范围边界。  

-   客户端所在的边界相当于 Active Directory 站点，或客户端标识的网络 IP 地址。 （客户端使用 Configuration Manager 管理员感知不到的 IP 地址的情况并不罕见。 如果不确定客户端网络位置，请在客户端上使用 **IPCONFIG** 命令确认客户端所报告的自身位置。）  

当你创建边界时，边界会自动获得一个名称，该名称基于边界的类型和作用域。 你无法修改此名称。 作为替代方式，当你配置边界时，可指定一个描述以帮助在 Configuration Manager 控制台中标识该边界。  

 创建边界之后，你可以修改其属性以执行以下操作：  

-   将边界添加到一个或多个边界组。  

-   更改边界的类型或作用域。  

-   查看边界“站点系统”  选项卡以了解哪些站点系统服务器（分发点、状态迁移点和管理点）与边界相关联。  

#### <a name="to-create-a-boundary"></a>创建边界  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” > “边界”  

2.  在“主页”  选项卡上的“创建”  组中，单击“创建边界” ** Boundary.**。  

3.  在“创建边界”对话框的“常规”  选项卡上，你可以指定“描述”  以便通过友好名称或引用来标识边界。  

4.  为此边界选择“类型”  ：  

    -   如果选择“IP 子网” ，你必须为此边界指定“子网 ID”  。  

        > [!TIP]  
        >  你可以指定“网络”  和“子网掩码”  以便自动指定“子网 ID”  。 在保存边界时，只会保存子网 ID 值。  

    -   如果选择“Active Directory 站点” ，则必须指定或“浏览”  到站点服务器的本地林中的 Active Directory 站点。  

        > [!IMPORTANT]  
        >  如果为边界指定 Active Directory 站点，则边界包括作为该 Active Directory 站点成员的每个 IP 子网。 如果 Active Directory 站点的配置在 Active Directory 中发生变化，则此边界中包括的网络位置也会更改。  

    -   如果选择“IPv6 前缀” ，你必须以 IPv6 前缀格式指定“前缀”  。  

    -   如果选择“IP 地址范围” ，你必须指定包括 IP 子网的一部分或包括多个 IP 子网的“起始 IP 地址”  和“结束 IP 地址”  。  

5.  单击“确定”  保存新边界。  

#### <a name="to-configure-a-boundary"></a>配置边界  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” > “边界”  

2.  选择要修改的边界。  

3.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

4.  在边界的“属性”  对话框中，选择“常规”  选项卡以编辑边界的“描述”  或“类型”  。 你也可以通过编辑边界的网络位置来更改边界的作用域。 例如，对于 Active Directory 站点边界，你可以指定新的 Active Directory 站点名称。  

5.  选择“站点系统”  选项卡以查看与此边界关联的站点系统。 你无法从边界的属性中更改此配置。  

    > [!TIP]  
    >  对于列为边界的站点系统的站点系统服务器，站点系统服务器必须关联为包含此边界的至少一个边界组的站点系统服务器。 这配置在边界组的“引用”  选项卡上。  

6.  选择“边界组”  选项卡以修改此边界的边界组成员身份：  

    -   要将此边界添加到一个或多个边界组，请单击“添加” ，选中一个或多个边界组的复选框，然后单击“确定” 。  

    -   要从某个边界组中删除此边界，请选择该边界组，然后单击“删除” 。  

7.  单击“确定”  关闭边界属性并保存配置。  

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

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> 边界最佳实践  

-   **只有在无法使用其他边界类型时才考虑使用 IP 地址范围边界类型：**  

     在设计边界策略时，我们建议你在使用其他边界类型之前使用基于 Active Directory 站点的边界。 在无法选择基于 Active Directory 站点的边界的情况下，则使用 IP 子网或 IPv6 边界。 如果你无法选择其中任何选项，请利用 IP 地址范围边界。 这是因为站点会定期评估边界成员，并且，相对于对其他边界类型的成员进行评估所需的查询而言，对 IP 地址范围的成员进行评估所需的查询需要使用的 SQL Server 资源要多很多。  

-   **避免自动站点分配的重叠边界：**  

     虽然每个边界组同时支持站点分配配置和用于内容位置的配置，但最好创建一组仅用于站点分配的单独的边界组。 意味着：确保边界组中的每个边界不是具有不同站点分配的另一个边界组的成员。 这是因为：  

    -   单一边界可以包含在多个边界组中  

    -   每个边界组可与站点分配的不同主站点相关联  

    -   边界上的客户端（该边界是具有不同站点分配的两个不同边界组的成员）将随机选择要加入的站点，而这可能不是你希望客户端加入的站点。  此配置称为重叠边界。  

     重叠边界并不是内容位置的问题，相反，它通常是一项所需配置，可为客户端提供其他资源或可供他们使用的内容位置。  



<!--HONumber=Nov16_HO1-->


