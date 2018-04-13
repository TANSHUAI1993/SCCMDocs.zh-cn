---
title: 配置边界组
titleSuffix: Configuration Manager
description: 通过使用边界组以逻辑方式对称为边界的相关网络位置进行整理，帮助客户端查找站点系统
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 297f4a5ecb7650a4ea643fff00dd67b6580256de
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>配置 System Center Configuration Manager 的边界组


*适用范围：System Center Configuration Manager (Current Branch)*

使用 Configuration Manager 中的边界组以逻辑方式对相关网络位置（[边界](/sccm/core/servers/deploy/configure/boundaries)）进行整理，以便更轻松地管理基础结构。 使用边界组之前应向其分配边界。

默认情况下，Configuration Manager 在每个站点创建默认站点边界组。

若要配置边界组，请将边界（网络位置）和站点系统角色（如分发点）关联到边界组。 此配置有助于将客户端关联到站点系统服务器，例如位于网络上的客户端附近的分发点。

若要提高站点系统服务器（如分发点）的可用性，使其可用于更广泛的网络位置，请向多个边界组分配相同的边界和相同的服务器。

客户端使用边界组来执行以下操作：  

-   自动站点分配  
-   查找可以提供包括以下某种服务的站点系统服务器：
    - 内容位置的的分发点
    -   软件更新点
    - 状态迁移点
    - 首选管理点（若要使用首选管理点，则必须为层次结构启用此选项，但不是从边界组配置中启用。 请参阅本主题中的[启用对首选管理点的使用](#to-enable-use-of-preferred-management-points)。）

##  <a name="boundary-groups-and-relationships"></a>边界组和关系
对于层次结构中的每个边界组，你可以分配：

-  一个或多个边界。 客户端的**当前**边界组是一个网络位置，定义为分配给特定边界组的边界。 一个客户端可具有多个当前边界组。
- 一个或多个站点系统角色。 客户端始终可以使用与它们当前边界组关联的站点系统角色。 根据其他配置，它们可能可以使用附加边界组中的站点系统角色。  

对于你创建的每个边界组，你可以配置指向另一个边界组的单向链接。 此链接称为**关系**。 链接的边界组称为**邻居**边界组。 边界组可以具有多个关系，每个关系都有特定的邻居边界组。

当客户端在其当前边界组中找不到可用的站点系统服务器时，每个关系的配置可确定它何时开始搜索相邻边界组。 对其他组的这一搜索称为**回退**。

## <a name="fallback"></a>回退
若要防止客户端在其当前边界组中找不到可用站点系统时出现问题，请为回退行为定义边界组之间的关系。 回退允许客户端将搜索范围扩展到附加的边界组，以查找可用的站点系统。

关系在边界组属性“关系”选项卡上配置。在配置关系时，你将定义指向邻居边界组的链接。 对于每种受支持的站点系统角色，可配置独立的设置以回退到该相邻边界组。 例如，在配置特定边界组的关系时，可将分发点的回退设置为在 20 分钟而不是默认的 120 分钟后发生。 有关更广泛的示例，请参阅[使用边界组的示例](#example-of-using-boundary-groups)。

如果客户端在其当前边界组中找不到可用的站点系统角色，它会使用以分钟为单位的回退时间。 此回退时间用于确定客户端何时开始搜索与相邻边界组关联的可用站点系统。  

当客户端找不到可用的站点系统，并开始从相邻边界组搜索位置时，它会扩大可用站点系统池。 边界组的配置及其关系定义了客户端对该可用站点系统池的使用。

- 一个边界组可具有多个关系。 通过多个关系，可以将每种站点系统配置为在不同的时间段之后回退到不同的相邻边界组。    
- 客户端仅回退到是其当前边界组的直接邻居的边界组。
- 当某个客户端是多个边界组的成员时，当前边界组即被定义为该客户端的所有边界组的联合。 该客户端会回退到任何这些原始边界组的相邻边界组。

### <a name="the-default-site-boundary-group"></a>默认站点边界组
除了所创建的边界组，每个站点还具有 Configuration Manager 创建的默认站点边界组。 此组命名为 ***Default-Site-Boundary-Group&lt;sitecode>***。 例如，站点 ABC 的组将被命名为 *Default-Site-Boundary-Group&lt;ABC>。*

对于你创建的每个边界组，Configuration Manager 自动在层次结构中创建指向每个默认站点边界组的隐式链接。
-   隐式链接是一个默认回退选项，从当前边界组到站点默认边界组，默认回退时间为 120 分钟。
-   对于不在与任何边界组关联的边界中的客户端：若要识别有效的站点系统角色，请使用已分配站点中的默认站点边界组。

管理默认站点边界组的回退：
- 打开站点默认边界组的属性，更改“默认行为”选项卡上的值。将在此处所做的更改应用到*所有*指向此边界组的隐式链接。 在你从另一个边界组配置显式链接到此默认站点边界组时，可以覆盖这些设置。
- 打开自定义边界组的属性。 将显式链接的值更改为默认站点边界组。 为回退或块回退设置以分钟为单位的新的时间时，所做的更改会影响你正在配置的链接。 显式链接的配置会覆盖默认站点边界组“默认行为”选项卡上的设置。


## <a name="site-assignment"></a>站点分配  
 你可以使用客户端的分配的站点配置每个边界组。  

-   使用自动站点分配的新安装的客户端将加入包含客户端当前网络位置的边界组的分配的站点。  
-   分配到站点后，当更改其网络位置时，客户端不会更改其站点分配。 例如，如果客户端漫游到一个新的网络位置，该位置由具有不同站点分配的边界组中的某个边界表示，则该客户端的已分配站点保持不变。  
-   当 Active Directory 系统发现发现新资源时，将依据边界组的边界对所发现的资源的网络信息进行评估。 此过程将新资源与分配的站点关联，以供客户端请求安装方法使用。  
-   当边界是多个边界组（这些边界组具有不同的分配的站点）的成员时，客户端会随机选择其中一个站点。  
-   对分配了边界组的站点的更改仅适用于新的站点分配操作。 以前分配给某个站点的客户端不会根据对边界组配置（或它们自身网络位置）的更改重新评估其站点分配。  

有关客户端站点分配的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端分配到一个站点](../../../../core/clients/deploy/assign-clients-to-a-site.md)中的[对计算机使用自动站点分配](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)。  

## <a name="distribution-points"></a>分发点

当客户端请求分发点的位置时，Configuration Manager 会向客户端发送一个站点系统列表。 这些站点系统采用与包含客户端当前网络位置的每个边界组相关联的适当类型：

-   **在软件分发期间**，客户端请求从一个分发点或其他有效的内容源提供的部署内容的位置（如配置为对等缓存的客户端）。

-   **在操作系统部署期间**，客户端请求用以发送或接收其状态迁移信息的位置。  

在内容部署期间，如果客户端请求的内容在其当前边界组的某个源中找不到，该客户端会继续请求该内容。 它会尝试搜索其当前边界组中的其他内容源，直至达到相邻边界组或默认站点边界组的回退时间。 如果客户端尚未找到内容，它将会扩展其内容源的搜索范围，以包括邻居边界组。

如果按需分发内容，但当客户端请求时，在分发点上找不到该内容，则启动将内容传输到该分发点的流程。 客户端可能会在回退为使用相邻边界组之前找到该服务器作为内容源。

## <a name="software-update-points"></a>软件更新点
客户端使用边界组来查找新的软件更新点。 若要控制客户端可以找到哪些服务器，请将各个软件更新点添加到不同的边界组。

如果更新 1702 之前的版本，则每个站点都会将现有的所有软件更新点添加到默认站点边界组中。 此站点更新行为可保持先前的客户端行为，以从可用服务器池中选择软件更新点。 将保持此行为直到你为控制选择和回退行为选择将单个软件更新点添加到不同的边界组。

如果安装新站点，则不会将软件更新点添加到默认站点边界组。 将软件更新点分配给边界组，以便客户端可以查找并使用它们。

### <a name="fallback-for-software-update-points"></a>软件更新点的回退
软件更新点的回退配置和其他站点系统角色一样，但有以下注意事项：
- **新的客户端使用边界组来选择软件更新点。** 安装的新客户端从那些与已配置的边界组关联的服务器中选择软件更新点。 此行为将取代以前的行为，即客户端从共享客户端林的服务器列表中随机选择一个软件更新点。

- **客户端继续使用上次已知良好的软件更新点，直到它们回退并找到新的软件更新点。** 已有软件更新点的客户端继续使用该点，直到无法连接它为止。 此行为包括继续使用与客户端当前边界组无关联的软件更新点。

  即使现有软件更新点不在客户端的当前边界组中，仍继续使用该服务器是有意而为之。 当软件更新点发生更改时，客户端会与新服务器同步数据，这会导致占用大量网络。 如果所有客户端同时切换到新服务器，则转换延迟有助于避免网络饱和。

- 在开始回退之前，客户端在 120 分钟内始终尝试连接其上次已知良好的软件更新点。 120 分钟后，如果客户端未建立联系，那么它将开始回退。 开始回退时，客户端从其当前边界组中接收所有软件更新点的列表。 可根据回退配置使用来自相邻边界组和站点默认边界组的其他软件更新点。

### <a name="fallback-configurations-for-software-update-points"></a>软件更新点的回退配置
#### <a name="beginning-with-version-1706"></a>从版本 1706年开始   
可以将软件更新点的“回退时间(分钟)”配置为小于 120 分钟。 但是，客户端仍试图在 120 分钟内连接其原始软件更新点。 然后，它将搜索范围扩展到其他服务器。 边界组回退时间从客户端第一次无法连接其原始服务器时开始。 当客户端扩展其搜索范围时，站点会提供配置为少于 120 分钟的所有边界组。

若要阻止软件更新点回退到相邻边界组，请将该设置配置为“永不回退”。

如果在两个小时内无法连接到其原始服务器，则客户端使用更短循环建立到新的软件更新点的连接。 此行为使客户端能够快速搜索潜在软件更新点的扩展列表。

 -  **回退示例：**  
    客户端的当前边界组对软件更新点的回退设置：将边界组 *A* 配置为 *10* 分钟，将边界组 *B* 配置为 *130* 分钟。当客户端无法连接其上次已知良好的软件更新点时：
    -   客户端尝试在接下来的 120 分钟内仅连接其原始服务器。 10 分钟后，边界组 A 的软件更新点会添加到可用服务器池中。 但是，在与原始服务器重新连接的初始 120 分钟未消耗完之前，客户端无法尝试连接到它们或任何其他服务器。
    -   尝试查找原始软件更新点 120 分钟后，客户端可能会扩展其搜索范围。 此时，客户端会将其当前边界组中的服务器以及配置为 120 分钟或更短时间的所有相邻边界组中的服务器添加到可用的软件更新点池中。 池中包括边界组 A 中先前添加到可用服务器池的服务器。
    -       再过 10 分钟后（客户端首次连接上次已知良好的软件更新点失败后的总时间为 130 分钟），客户端扩展搜索范围，以包括边界组 B 的软件更新点。  

#### <a name="prior-to-version-1706"></a>1706 之前的版本
对于 1706 之前的版本，软件更新点的回退配置不支持以分钟为单位的可配置时间。 相反，回退行为仅限于以下选项：

  - **回退时间(分钟)**：此选项针对软件更新点显示为灰色，并且无法配置。 它被设置为 120 分钟。
  -     **永不回退：**当使用此配置时，你可以阻止软件更新点回退到邻居边界组。

如果已有软件更新点的客户端无法连接该点，该客户端会回退并查找另一个软件更新点。 使用回退时，客户端将从其当前边界组中接收所有软件更新点的列表。 如果在 120 分钟内找不到可用服务器，它会回退到其相邻边界组和默认站点边界组。 回退到这两个边界组的操作将同时发生。 软件更新点回退到相邻组的时间设置为 120 分钟。 你无法更改此回退时间。 此外，120 分钟是用于回退到默认站点边界组的默认时间。 当客户端回退到邻居边界组和默认站点边界组时，客户端会尝试联系邻居边界组中的软件更新点，然后尝试使用默认站点边界组中的一个软件更新点。

### <a name="manually-switch-to-a-new-software-update-point"></a>手动切换到新的软件更新点
除了使用回退之外，还可以使用“客户端通知”手动强制设备切换到新的软件更新点。

切换到新服务器时，设备使用回退来查找新的服务器。 请查看边界组配置。 确保软件更新点位于正确的边界组后，再开始进行此更改。

有关详细信息，请参阅[将客户端手动切换到新的软件更新点](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point)。



## <a name="management-points"></a>管理点
<!-- 1324594 -->
从版本 1802 开始，可在边界组之间配置管理点的回退关系。 此行为可以更好地控制客户端使用的管理点。 在边界组属性的“关系”选项卡上，有一个管理点列。 在添加新回退边界组时，当前管理点的回退时间始终为零 (0)。 对于站点默认边界组上的“默认行为”，此行为是相同的。

在此之前，当安全网络中有一个受保护的管理点，会出现一个常见问题。 主要公司网络上的客户端接收策略，其中包括此受保护的管理点，即使它们无法通过防火墙与管理点进行通信。 若要解决此问题，请使用“从不回退”选项，以确保客户端仅回退到它们可以与之通信的管理点。

当站点升级到版本 1802 时，Configuration Manager 会将所有非面向 Internet 的管理点添加到站点默认边界组。 此升级行为可确保旧版客户端继续与管理点通信。 若要充分利用此功能，请将管理点移到所需的边界组。

在客户端安装 (ccmsetup.exe) 过程中，管理点边界组回退不会更改行为。 如果命令行未使用 /MP 参数指定初始管理点，新的客户端将收到完整的可用管理点列表。 在其初始启动过程中，客户端使用它可以访问的第一个管理点。 一旦客户端注册站点，它便会收到通过此新行为正确排序的管理点列表。 

若要让客户端使用此功能，请在“层次结构设置”中启用以下设置：“客户端首选使用边界组中指定的管理点”。 

> [!Note]
> 操作系统部署进程不知道边界组。

### <a name="troubleshooting"></a>故障排除
在“LocationServices.log”中出现新条目。 “Locality”属性标识以下状态之一：
- 0：未知
- 1：指定管理点仅在回退的站点默认边界组中
- 2：指定管理点位于远程或相邻边界组中。 当相邻和站点默认边界组中都存在管理点时，locality 为 2。
- 3：指定管理点位于本地或当前边界组中。 如果当前边界组以及相邻或站点默认边界组中均存在管理点，locality 为 3。 如果在“层次结构设置”中未启用首选管理点设置，locality 始终为 3，而不考虑管理点位于哪个边界组。

客户端首先使用本地管理点 (locality 3)，第二个为远程管理点 (locality 2)，然后使用回退 (locality 1)。 

如果客户端在 10 分钟内收到五个错误，并且无法与当前边界组中的管理点进行通信，它将尝试联系相邻边界组或站点默认边界组中的管理点。 如果当前边界组中的管理点稍后重新联机，客户端将在下一个刷新周期返回到本地管理点。 刷新周期为 24 小时，或当 Configuration Manager 代理服务重新启动时。




## <a name="preferred-management-points"></a>首选管理点

 > [!Note]
 > 此层次结构设置（“客户端首选使用边界组中指定的管理点”）的行为从版本 1802 开始有所变化。 当你启用此设置时，Configuration Manager 会对分配的管理点使用边界组功能。 有关详细信息，请参阅[管理点](#management-points)。 

 首选管理点使客户端能够识别与当前网络位置（边界）关联的管理点。  

-   客户端先尝试使用已分配站点中的首选管理点，然后再使用已分配站点中未配置为首选的管理点。  
-   若要使用此选项，请在“层次结构设置”中启用“客户端首选使用边界组中指定的管理点”。 然后在各个主站点上配置边界组。 包括应与该边界组的相关边界关联的管理点。
-   如果你配置了首选管理点，客户端在整理其管理点列表时，会将首选管理点放在该列表的顶部。 该列表包含客户端已分配站点中的所有管理点。  

> [!NOTE]  
>  客户端漫游意味着它会更改自己的网络位置。 例如，将笔记本电脑携带到远程办公地点时。 当客户端漫游时，它可能会先在新位置使用本地站点中的管理点或代理管理点，然后再尝试使用其已分配站点中的服务器。 由已分配站点中的服务器组成的这个列表中包含首选管理点。 有关详细信息，请参阅[了解客户端如何查找站点资源和服务](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

## <a name="overlapping-boundaries"></a>重叠边界  
 Configuration Manager 对于内容位置支持重叠边界配置。 当客户端网络位置属于多个边界组时：

-   当客户端请求内容时，Configuration Manager 向客户端发送包含该内容的所有分发点的列表。  
-   当客户端请求服务器发送或接收其状态迁移信息时，Configuration Manager 向客户端发送与包括客户端当前网络位置的边界组关联的所有状态迁移点的列表。  

此行为使客户端能够选择从中传输内容或站点迁移信息的最近的服务器。  



## <a name="example-of-using-boundary-groups"></a>使用边界组的示例
以下示例使用客户端从分发点进行内容搜索。 此示例可以应用于使用边界组的其他站点系统角色。 请记住，软件更新点不支持配置回退到相邻组，并且始终使用 120 分钟的时间段。

创建三个边界组，使其不共享边界或站点系统服务器：
-   组 BG_A，包含与该组关联的 DP_A1 和 DP_A2 分发点
-   组 BG_B，包含与该组关联的 DP_B1 和 DP_B2 分发点
-   组 BG_C，包含与该组关联的 DP_C1 和 DP_C2 分发点

仅向 BG_A 边界组添加客户端的网络位置作为边界。 然后配置从该边界组到其他两个边界组的关系：
-   将第一个*相邻*组 (BG_B) 的分发点配置为 10 分钟后使用。 此组包含分发点 DP_B1 和 DP_B2。 这两个分发点都很好地连接到第一组边界位置。
-   将第二个*相邻*组 (BG_C) 配置为 20 分钟后使用。 此组包含分发点 DP_C1 和 DP_C2。 这两个分发点都从其他两个边界组跨越 WAN。
-   此外，向站点的默认站点边界组添加站点服务器上的另一个分发点。 此服务器是你最不想使用的内容源位置，但它位于所有边界组的中心位置。

    边界组和回退时间的示例：

     ![边界组和回退时间的示例](media/BG_Fallback.png)


使用该配置：
-   客户端开始从其*当前*边界组 (BG_A) 中的分发点搜索内容。 每个分发点搜索两分钟，然后切换到边界组中的下一个分发点。 有效的内容源位置的客户端池包括 DP_A1 和 DP_A2。
-   如果在搜索 10 分钟之后客户端无法从其当前边界组找到内容，然后，它将向它的搜索添加 BG_B 边界组中的分发点。 然后，它继续从合并服务器池的某个分发点中搜索内容。 该池现在包含 BG_A 和 BG_B 边界组中的服务器。 客户端继续对每个分发点进行为时两分钟的访问，然后切换到池中的下一个服务器。 有效的内容源位置的客户端池包括 DP_A1、DP_A2、DP_B1 和 DP_B2。
-   再过 10 分钟（总共 20 分钟）后，如果客户端仍未在分发点中找到内容，它会对池进行扩展，以便包含第二个*相邻*组（边界组 BG_C）中的可用服务器。 客户端现在有六个分发点可供搜索（DP_A1、DP_A2、DP_B2、DP_B2、DP_C1 和 DP_C2）。 它继续每隔两分钟切换到一个新的分发点，直到找到内容为止。
-   如果客户端在总共 120 分钟后还未找到内容，则它将回退，以将默认站点边界组纳入其继续搜索的一部分。 现在，池中包含这三个已配置的边界组中的所有分发点，并且最后一个分发点位于站点服务器上。 然后，客户端继续执行对内容的搜索，并每隔两分钟对分发点进行更改直到找到内容。

通过将不同的相邻组配置为在不同的时间可用，可控制何时添加特定分发点作为内容源位置。 对于在其他任何位置都找不到的内容，客户端使用回退到默认站点边界组作为其安全保障。





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>以前版本中的更改
以下是 Configuration Manager Current Branch 中对边界组以及客户端查找内容的方式的关键更改。 这些更改许多都和概念协同工作。


-   已删除对于快速或慢速的配置：不再将单独的分发点配置为快速或慢速。 相反，每个与边界组相关联的站点系统都将视为相同的系统。 由于有此更改，边界组属性的“引用”选项卡不再支持快速或慢速的配置。
- 每个站点的新默认边界组：每个主站点都具有一个名为 ***Default-Site-Boundary-Group&lt;sitecode>*** 的新默认边界组。 当客户端不在分配给边界组的网络位置时，它会从分配的站点中使用与默认组相关联的站点系统。 计划使用此边界组作为回退内容位置概念的替换。   
 -  已删除“允许回退内容源位置”：不再将分发点显式配置为用于回退。 已从控制台中删除配置此设置的选项。

    此外，已更改应用程序部署类型上的**允许客户端使用内容的回退源位置**的设置结果。 部署类型上的此设置现在允许客户端使用默认站点边界组作为内容源位置。

 -  边界组关系：每个边界组都可链接到一个或多个其他的边界组。 这些链接就会形成关系，并在名为“关系”的新边界组属性选项卡上进行配置：
    -   客户端直接与之关联的每个边界组都称为**当前**边界组。  
    -   由于客户端的*当前*边界组和另一个组之间存在关联，因此，客户端可以使用的任何边界组都称为**相邻**边界组。
    -  在“关系”选项卡上，添加要用作*相邻*边界组的边界组。 还可以配置回退时间（分钟）。 当客户端在*当前*组的某个分发点中找不到内容时，此时间便作为客户端开始从*相邻*边界组中搜索内容位置的时间。

        添加或更改边界组配置时，可以选择阻止从正在配置的当前组回退到该特定的边界组。

    若要使用新配置，请定义从一个边界组到另一个边界组的显式关联（链接）。 以相同的时间（分钟）配置该关联组中的所有分发点。 当客户端在其*当前*边界组中找不到内容源时，配置的时间可确定客户端开始从其相邻边界组搜索内容源的时间。

    除了显式配置的边界组外，每个边界组都具有指向默认站点边界组的隐式链接。 该链接在 120 分钟后变为活动状态。 接着，默认站点边界组变为相邻边界组。 此行为允许客户端将与该边界组关联的分发点用作内容源位置。

    此行为替换以前称为内容回退的行为。 通过将默认站点边界组显式关联到*当前*组，可覆盖此默认行为（120 分钟）。 设置以分钟为单位的特定时间，或完全阻止使用回退。


-   客户端尝试从每个分发点获取内容，用时长达 2 分钟：客户端搜索内容源位置时，会尝试对每个分发点进行 2 分钟的访问，然后再尝试访问另一个分发点。 此行为与以前版本有所不同，在以前版本中，客户端尝试连接到分发点的时间长达 2 小时。

    - 客户端从客户端的一个或多个*当前*边界组中的可用服务器池中随机选择第一个分发点。

    - 两分钟后，如果客户端找不到内容，它将切换到新的分发点并尝试从该服务器获取内容。 每隔两分钟重复此过程，直到客户端找到内容或到达其池中的最后一个服务器。

    - 如果在达到*相邻*边界组的回退时间前，客户端在其*当前*池中找不到有效的内容源位置，则客户端会将该*相邻*组中的分发点添加到其当前列表的末尾。 然后，它会搜索扩展的源位置组，其中包含这两个边界组中的分发点。

        > [!TIP]  
        > 当你创建从当前边界组到默认站点边界组的显式链接，并定义比链接到相邻边界组的回退时间更短的回退时间时，客户端会在添加相邻组之前先从默认站点边界组开始搜索源位置。

    - 客户端无法从池中的最后一个服务器获取内容时，它将再次开始该过程。


## <a name="procedures-for-boundary-groups"></a>边界组的过程

### <a name="to-create-a-boundary-group"></a>创建边界组  
1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” >  “边界组”。  

2.  在“主页”  选项卡上的“创建”  组中，单击“创建边界组” 。  

3.  在“创建边界组”对话框中，选择“常规”选项卡，为此边界组指定“名称”。  

4.  单击“确定”  保存新边界组。  


### <a name="to-configure-a-boundary-group"></a>配置边界组  
 1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” >  “边界组”。  

 2.  选择要修改的边界组。  

 3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

 4.  在边界组的“属性”  对话框中，选择“常规”  选项卡以修改作为此边界组成员的边界：  

     -   要添加边界，请单击“添加” ，选中一个或多个边界的复选框，并单击“确定” 。  

     -   要删除边界，请选择边界并单击“删除” 。  

 5.  选择“引用”  选项卡以修改站点分配和关联的站点系统服务器配置：  

     -   若要启用此边界组供客户端用于站点分配，请选择“将此边界组用于站点分配”。 然后从“分配的站点”下拉列表中选择一个站点。  

     -   配置与此边界组关联的可用站点系统服务器：  

     1.  单击“添加” ，然后选中一个或多个服务器的复选框。 将服务器添加为此边界组的关联站点系统服务器。 仅在其上安装有受支持的站点系统角色的服务器可用。  

         > [!NOTE]  
         >  你可从层次结构中的任何站点选择可用站点系统的任意组合。 所选的站点系统列在作为此边界组成员的每个边界的属性中的“站点系统”  选项卡上。  

     2.  要从此边界组中删除服务器，请选择该服务器，然后单击“删除” 。  

         > [!NOTE]  
         >  若要停止使用此边界组来关联站点系统，请删除列为关联站点系统服务器的所有服务器。  

 6.  若要配置回退行为，请选择“关系”选项卡：  

     - 单击“添加”，然后选择要配置的边界组。

     - 设置分发点的回退时间。 在此时间段之后，边界组中正在配置关系的客户端将能够开始从正在添加的边界组中的分发点搜索内容。

     - 若要阻止回退到特定边界组（包括默认配置的*默认站点边界组*），请选择该边界组，然后选中“永不回退”复选框。   

 7.  单击“确定”  关闭边界组属性并保存配置。  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>将站点系统服务器与边界组关联  
 1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” >  “边界组”。  

 2.  选择要修改的边界组。  

 3.  在“主页”选项卡上的“属性”组中，单击“属性”。  

 4.  在边界组的“属性”  对话框中，选择“引用”  选项卡。  

 5.  在“选择站点系统服务器”下，单击“添加”。 选择要与此边界组关联的站点系统服务器，然后单击“确定”。  

 6.  单击“确定”  关闭对话框并保存边界组配置。  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>为自动站点分配配置回退站点  

  1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” >  “站点”。  

  2.  在“主页”  选项卡上的“站点”  组中，单击“层次结构设置” 。  

  3.  在“常规”  选项卡上，选中“使用回退站点” 复选框，然后从“回退站点”  下拉列表中选择一个站点。  

  4.  单击“确定”  保存配置。  

#### <a name="to-enable-use-of-preferred-management-points"></a>若要启用对首选管理点的使用  

 1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”，然后在“主页”选项卡上选择“层次结构设置”。  

 2.  在“层次结构设置”的“常规”  选项卡上，选择“客户端首选使用边界组中指定的管理点” 。  

 3.  单击“确定”  关闭对话框并保存配置。  
