---
title: "发现方法 | Microsoft Docs"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 442e5e1fbddd00248819a8de79adc78929474fc0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>有关 System Center Configuration Manager 的发现方法

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 发现方法可以在网络上找到不同设备，或从 Active Directory 找到设备和用户。 若要有效地使用发现方法，应了解及其可用配置和限制。  

##  <a name="bkmk_aboutForest"></a> Active Directory 林发现  
 **可配置：**是  

 **默认启用：**否  

 可用于运行此方法的**帐户**：  

-   **Active Directory 林发现帐户**（用户定义）  

-   站点服务器的**计算机帐户**  

与其他 Active Directory 发现方法不同，Active Directory 林发现不会发现可管理的资源。 而会发现 Active Directory 中配置的网络位置，并可将这些位置转换为边界，供在整个层次结构中使用。  

此方法运行时，它会搜索本地 Active Directory 林、每个受信任的林以及在 Configuration Manager 控制台的“Active Directory 林”节点中配置的所有其他林。  

借助 Active Directory 林发现，可：  

-   发现 Active Directory 站点和子网，然后基于这些网络位置创建 Configuration Manager 边界。  

-   标识分配到 Active Directory 站点的超网，并将每个超网转换为 IP 地址范围边界。  

-   当启用“发布到林”并且指定的 Active Directory 林帐户具有该林的权限时，则发布到该林中的 Active Directory 域服务 (AD DS)。  

可以从以下节点在 Configuration Manager 控制台中管理 Active Directory 林发现，这些节点位于“管理”工作区的“层次结构配置”下：  

-   **发现方法**：你可在此处启用 Active Directory 林发现以在层次结构的顶层站点上运行。 你也可以指定一个简单的计划来运行发现，并将其配置为依据所发现的 IP 子网和 Active Directory 站点自动创建边界。 Active Directory 林发现无法在子主站点或辅助站点上运行。  

-   **Active Directory 林**：在此处配置要发现的其他 Active Directory 林，为每个林指定要用作 Active Directory 林帐户的帐户，并配置针对每个林的发布。 此外，可以监视发现过程，并将 IP 子网和 Active Directory 站点作为边界和边界组的成员添加到 Configuration Manager。  

要为层次结构中的每个站点配置 Active Directory 林发布，请将 Configuration Manager 控制台连接到层次结构的顶层站点。 Active Directory 站点的“属性”对话框中的“发布”选项卡只能显示当前站点及其子站点。 如果针对某个林启用了发布，并且为 Configuration Manager 扩展了该林的架构，则会为已启用以发布到该 Active Directory 林的每个站点发布下列信息：  

-    **SMS-Site-&lt;site code>**

-   **SMS-MP-&lt;site code>-&lt;site system server name>**  

-   **SMS-SLP-&lt;site code>-&lt;site system server name>**  

-   **SMS-&lt;site code>-&lt;Active Directory site name or subnet>**  

> [!NOTE]  
>  辅助站点始终使用辅助站点服务器计算机帐户来发布到 Active Directory。 如果希望辅助站点发布到 Active Directory，则请确保辅助站点服务器计算机帐户具有发布到 Active Directory 的权限。 辅助站点无法将数据发布到不受信任的林。  

> [!CAUTION]  
>  如果取消选中将站点发布到 Active Directory 林的选项，则会从 Active Directory 中删除之前为该站点发布的信息，其中包括可用站点系统角色。  

Active Directory 林发现操作记录在下列日志中：  

-   站点服务器上的 **&lt;InstallationPath>\Logs** 文件夹内的 **ADForestDisc.Log** 文件中记录了除与发布相关的操作之外的所有操作。  

-   站点服务器上的 **&lt;InstallationPath>\Logs** 文件夹内的 **hman.log** 和 **sitecomp.log** 文件中记录了 Active Directory 林发现发布操作。  

有关如何配置此发现方法的详细信息，请参阅[为 System Center Configuration Manager 配置发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)。  

##  <a name="bkmk_aboutGroup"></a> Active Directory 组发现  
**可配置：**是  

**默认启用：**否  

可用于运行此方法的**帐户**：  

-   **Active Directory 组发现帐户**（用户定义）  

-   站点服务器的**计算机帐户**  

> [!TIP]  
>  有关除本部分外的其他信息，请参阅 [Active Directory 组、系统和用户发现的常见功能](#bkmk_shared)。  

使用此方法搜索 Active Directory 域服务以识别：  

-   本地、全局和通用安全组。  

-   组的成员身份。  

-   有关组的成员计算机和用户的有限信息（即使这些计算机和用户以前未被另一种发现方法发现过）。  

此发现方法用于确定组和组成员的组关系。 默认情况下，只会发现安全组。 如果还想要找到分发组的成员身份，则必须在“Active Directory 组发现属性”对话框中的“选项”选项卡上，选中“发现分发组的成员身份”选项的复选框。  

Active Directory 组发现不支持可通过使用 Active Directory 系统发现或 Active Directory 用户发现确定的扩展 Active Directory 属性。 由于此发现方法未经过优化，无法发现计算机和用户资源，因此请考虑在运行 Active Directory 系统发现和 Active Directory 用户发现之后运行此发现方法。 这是因为此方法会为组创建完整的发现数据记录 (DDR)，但只会为作为组成员的计算机和用户创建有限的 DDR。  

可以配置下列发现作用域，控制此方法搜索信息的方式：  

-   **位置**：如果要搜索一个或多个 Active Directory 容器，请使用位置。 此作用域选项支持对指定的 Active Directory 容器进行递归搜索，该搜索还会搜索指定容器下的每个子容器。 此过程将继续，直至找不到其他子容器为止。  

-   **组**：如果要搜索一个或多个特定 Active Directory 组，请使用组。 可以配置“Active Directory 域”以使用默认域和林，或将搜索范围限制为单独的域控制器。 此外，你可以指定要搜索的一个或多个组。 如果未指定至少一个组，则会搜索在指定“Active Directory 域”  位置中找到的所有组。  

> [!CAUTION]  
>  在配置发现作用域时，请仅选择必须发现的组。 这是因为 Active Directory 组发现会尝试发现发现作用域中每个组的每个成员。 大组的发现可能需要使用大量的带宽和 Active Directory 资源。  

> [!NOTE]  
>  必须先运行 Active Directory 系统发现或 Active Directory 用户发现（具体取决于想要发现的内容），然后才可创建基于扩展 Active Directory 属性的集合并确保计算机和用户的发现结果准确。  

站点服务器上 **&lt;InstallationPath\>\LOGS** 文件夹内的 **adsgdis.log** 文件中记录了 Active Directory 组发现操作。  

有关如何配置此发现方法的详细信息，请参阅[为 System Center Configuration Manager 配置发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)。  

##  <a name="bkmk_aboutSystem"></a> Active Directory 系统发现  
**可配置：**是  

**默认启用：**否  

可用于运行此方法的**帐户**：  

-   **Active Directory 系统发现帐户**（用户定义）  

-   站点服务器的**计算机帐户**  

> [!TIP]  
>  有关除本部分外的其他信息，请参阅 [Active Directory 组、系统和用户发现的常见功能](#bkmk_shared)。  

使用此发现方法在指定的 Active Directory 域服务位置中搜索可用于创建集合和查询的计算机资源。 还可以使用客户端请求安装在已发现设备上安装 Configuration Manager 客户端。  

默认情况下，此方法将发现有关计算机的基本信息，其中包括：  

-   计算机名称  

-   操作系统和版本  

-   Active Directory 容器名称  

-   IP 地址  

-   Active Directory 站点  

-   上次登录的时间戳  

若要成功创建计算机的 DDR，Active Directory 系统发现则必须能够识别计算机帐户，然后成功地将计算机名称解析为 IP 地址。  

在“Active Directory 系统发现属性”对话框中的“Active Directory 属性”选项上，可查看 Active Directory 系统发现已返回的默认对象属性的完整列表。 还可配置方法来发现其他（扩展）属性。  

站点服务器上 **&lt;InstallationPath\>\LOGS** 文件夹内的 **adsysdis.log** 文件中记录了 Active Directory 系统发现操作。  

有关如何配置此发现方法的详细信息，请参阅[为 System Center Configuration Manager 配置发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)。  

##  <a name="bkmk_aboutUser"></a> Active Directory 用户发现  
**可配置：**是  

**默认启用：**否  

可用于运行此方法的**帐户**：  

-   **Active Directory 用户发现帐户**（用户定义）  

-   站点服务器的**计算机帐户**  

> [!TIP]  
>  有关除本部分外的其他信息，请参阅 [Active Directory 组、系统和用户发现的常见功能](#bkmk_shared)。  

使用此发现方法搜索 Active Directory 域服务，以确定用户帐户和关联属性。 默认情况下，此方法将发现有关用户帐户的基本信息，其中包括：  

-   用户名  

-   唯一用户名（包括域名）  

-   Domain  

-   Active Directory 容器名称  

在“Active Directory 用户发现属性”对话框中的“Active Directory 属性”选项卡上，可查看 Active Directory 用户发现所返回的默认对象属性的完整列表。 还可配置方法来发现其他（扩展）属性。

站点服务器上 **&lt;InstallationPath\>\LOGS** 文件夹内的 **adusrdis.log** 文件中记录了 Active Directory 用户发现操作。  

有关如何配置此发现方法的详细信息，请参阅[为 System Center Configuration Manager 配置发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)。  

## <a name="azureaddisc"></a>Azure Active Directory 用户发现
从版本 1706 开始，在将环境配置为使用 Azure 服务时，可以使用 Azure Active Directory (Azure AD) 用户发现。
使用此发现方法在 Azure AD 中搜索对 Azure AD 实例进行身份验证的用户，以查找以下属性：  
-   objectId
-   displayName
-   mail
-   mailNickname
-   onPremisesSecurityIdentifier
-   userPrincipalName
-   AAD tenantID

此方法支持对 Azure AD 中用户数据的完全同步和增量同步。 然后可以将此信息与从其他发现方法收集的发现数据一起使用。

Azure AD 用户发现的操作记录在层次结构顶层站点服务器上的 SMS_AZUREAD_DISCOVERY_AGENT.log 文件中。

要配置 Azure AD 用户发现，请使用 Azure 服务向导。  有关如何配置此发现方法的详细信息，请参阅[配置 Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods)。





##  <a name="bkmk_aboutHeartbeat"></a>检测信号发现  
**可配置：**是  

**默认启用：**是  

可用于运行此方法的**帐户**：  

-   站点服务器的**计算机帐户**  

检测信号发现不同于其他 Configuration Manager 发现方法。 它默认为启用状态，并且在每个计算机客户端（而非站点服务器）上运行以创建 DDR。 对于移动设备客户端，移动设备客户端正在使用的管理点会创建此 DDR。 若要帮助维护 Configuration Manager 客户端的数据库记录，请不要禁用检测信号发现。 除了维护数据库记录，此方法能够以新资源记录形式强制进行计算机发现，或者可以重新填写从数据库中删除的计算机的数据库记录。  

检测信号发现按照为层次结构中所有客户端配置的计划运行，或者（若手动调用）通过运行客户端 Configuration Manager 程序中“操作”选项卡上的“发现数据收集周期”，在特定客户端上运行。 检测信号发现的默认计划设置为每 7 天进行一次。 如果你更改检测信号发现间隔，请确保它比从站点数据库中删除非活动客户端记录的“删除过期的发现数据” 站点维护任务运行得更加频繁。 你可以仅为主站点配置“删除过期的发现数据”  任务。  

运行检测信号发现时，它会创建具有客户端当前信息的 DDR。 然后，客户端将此大小约 1 KB 的小文件复制到管理点，使主站点可对其进行处理。 该文件包含以下信息：  

-   网络位置  

-   NetBIOS 名称  

-   客户端代理版本  

-   操作状态详细信息  

检测信号发现是唯一提供有关客户端安装状态的详细信息的发现方法。 它通过更新系统资源客户端属性，以将某个值设置为“是”来实现此操作。  

> [!NOTE]  
>  即使禁用检测信号发现，也仍然会针对活动的移动设备客户端来创建和提交 DDR。 这可以确保“删除过期的发现数据”  任务不影响活动的移动设备。 实现此操作的原因是，在“删除过期发现数据” 任务删除移动设备的数据库记录时，它还会吊销设备证书并阻止移动设备连接到管理点。  

检测信号发现操作记录在以下位置：  

-   对于计算机客户端，检测信号发现操作记录在 %Windir%\CCM\Logs 文件夹内 **InventoryAgent.log** 文件中的客户端上。  

-   对于移动设备客户端，检测信号发现操作记录在移动设备客户端使用的管理点的 %Program Files%\CCM\Logs 文件夹内的 **DMPRP.log** 文件中。  

有关如何配置此发现方法的详细信息，请参阅[为 System Center Configuration Manager 配置发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)。  

##  <a name="bkmk_aboutNetwork"></a>网络发现  
**可配置：**是  

**默认启用：**否  

可用于运行此方法的**帐户**：  

-   站点服务器的**计算机帐户**  

使用此方法发现网络的拓扑，并在拥有 IP 地址的网络上发现设备。 网络发现通过查询运行 DHCP 的 Microsoft 实现的服务器、路由器中的地址解析协议 (ARP) 缓存、启用了 SNMP 的设备以及 Active Directory 域，在网络中搜索启用了 IP 的资源。  

使用网络发现前，必须指定要运行的发现的*级别*。 你也需要配置一个或多个发现机制，以使网络发现能够查询网络段或设备。 你也可以配置有助于控制网络上的发现操作的设置。 最后，你可以定义网络发现运行的一个或多个计划。  

为使此方法成功发现资源，网络发现必须识别资源的 IP 地址以及子网掩码。 使用以下方法来确定对象的子网掩码：  

-   **路由器 ARP 缓存：**网络发现将查询路由器的 ARP 缓存来查找子网信息。 通常，路由器 ARP 缓存中的数据生存时间很短。 因此，当网络发现查询 ARP 缓存时，ARP 缓存可能不再包含有关所请求的对象的信息。  

-   **DHCP：**网络发现查询指定的每个 DHCP 服务器，以发现 DHCP 服务器为其提供了租约的设备。 网络发现只支持运行 DHCP 的 Microsoft 实现的 DHCP 服务器。  

-   **SNMP 设备：**网络发现可以直接查询 SNMP 设备。 设备必须安装本地 SNMP 代理，网络发现才能查询该设备。 还必须将网络发现配置为使用 SNMP 代理所使用的共同体名称。  

当发现识别到可寻址 IP 的对象并且可以确定该对象的子网掩码时，它将为该对象创建 DDR。 由于可以将不同类型的设备连接到网络，因此网络发现可以发现无法支持 Configuration Manager 客户端软件的资源。 例如，可以发现但无法管理的设备包括打印机和路由器。  

网络发现可以返回多个属性作为它所创建的发现记录的一部分。 其中包括:  

-   NetBIOS 名称  

-   IP 地址  

-   资源域  

-   系统角色  

-   SNMP 社区名称  

-   MAC 地址  

网络发现活动记录在运行发现的站点服务器上的 &lt;InstallationPath\>\Logs 内的 **Netdisc.log** 文件中。  

 有关如何配置此发现方法的详细信息，请参阅[为 System Center Configuration Manager 配置发现方法](../../../../core/servers/deploy/configure/configure-discovery-methods.md)。  

> [!NOTE]  
>  复杂的网络和低带宽连接可能导致网络发现运行缓慢并生成大量的网络流量。 作为一种最佳方案，请仅在其他发现方法找不到你必须发现的资源时，才运行网络发现。 例如，你必须发现工作组计算机，则使用网络发现。 其他发现方法不发现工作组计算机。  

###  <a name="BKMK_NetDiscLevels"></a>网络发现的级别  
配置网络发现时，你可以指定以下三个发现级别之一：  

|发现的级别|详细信息|  
|------------------------|-------------|  
|拓扑|此级别发现路由器和子网，但不标识对象的子网掩码。|  
|拓扑和客户端|除了拓扑之外，此级别还发现潜在的客户端（如计算机）以及如打印机和路由器等资源。 此级别的发现尝试识别它所发现的对象的子网掩码。|  
|拓扑、客户端和客户端操作系统|除了拓扑和潜在客户端之外，此级别还尝试发现计算机操作系统名称和版本。 该级别使用 Windows 浏览器和 Windows 网络调用。|  

 对于每个增量级别，网络发现会增加其活动的网络带宽使用量。 在启用网络发现的各个方面之前，请考虑可以生成的网络流量。  

 例如，在首次使用网络发现时，你可以仅从此拓扑级别开始标识网络基础结构。 然后，可以将网络发现重新配置为发现对象及其设备操作系统。 还可以通过配置设置，将网络发现限制在某个特定范围的网段内。 如此一来，就能在所需的网络位置中发现对象，从而避免不必要的网络流量，并且还可以从边缘路由器或网络外部发现对象。  

###  <a name="BKMK_NetDiscOptions"></a>网络发现选项  
要启用网络发现以搜索 IP 可寻址的设备，必须配置以下一个或多个选项以指定如何查询设备。  

> [!NOTE]  
>  网络发现在运行发现的站点服务器的计算机帐户上下文中运行。 如果计算机帐户对不受信任的域没有权限，则域和 DHCP 服务器配置可能无法发现资源。  

**DHCP：**  

指定你希望网络发现查询的每个 DHCP 服务器。 （网络发现只支持运行 DHCP 的 Microsoft 实现的 DHCP 服务器。）  

-   网络发现使用对 DHCP 服务器上的数据库的远程过程调用来检索信息。  

-   网络发现可以查询 32 位和 64 位 DHCP 服务器以获取向每个服务器注册的设备的列表。  

-   为了让网络发现成功地查询 DHCP 服务器，运行发现的服务器的计算机帐户必须是 DHCP 服务器上 DHCP 用户组的成员。 例如，满足以下条件之一时存在此访问级别：  

    -   指定的 DHCP 服务器是运行发现的服务器的 DHCP 服务器。  

    -   运行发现的计算机和 DHCP 服务器在相同域中。  

    -   运行发现的计算机和 DHCP 服务器之间存在双向信任。  

    -   站点服务器为 DHCP 用户组的成员。  

-   当网络发现枚举 DHCP 服务器时，它并不始终发现静态 IP 地址。 网络发现不查找 DHCP 服务器上已排除的 IP 地址范围中的 IP 地址。 并且它也不发现为手动分配所保留的 IP 地址。  

**域：**  

指定你希望网络发现查询的每个域。  

-   运行发现的站点服务器的计算机帐户必须有权读取每个指定域中的域控制器。  

-   若要发现本地域中的计算机，必须至少在一个与运行网络发现的站点服务器处于同一子网的计算机上启用计算机浏览器服务。  

-   网络发现可以发现你可以在浏览网络时从站点服务器中查看的任何计算机。  

-   网络发现检索 IP 地址，然后使用 Internet 控制消息协议 (ICMP) 回显请求 ping 它所发现的每个设备。 **ping** 命令有助于确定当前处于活动状态的计算机。  

**SNMP 设备：**  

指定你希望网络发现查询的每个 SNMP 设备。  

-   网络发现从响应查询的任何 SNMP 设备中检索 ipNetToMediaTable 值。 此值返回作为客户端计算机或其他资源（如打印机、路由器或其他可寻址 IP 的设备）的 IP 地址的数组。  

-   若要查询设备，必须指定设备的 IP 地址或 NetBIOS 名称。  

-   你必须将网络发现配置为使用设备的共同体名称，否则设备将拒绝基于 SNMP 的查询。  

###  <a name="BKMK_LimitNetDisc"></a>限制网络发现  
当网络发现在网络边缘上查询 SNMP 设备时，它可以标识关于在中间网络之外的子网和 SNMP 设备的信息。 使用以下信息，通过配置发现可以与其通信的 SNMP 设备以及指定要查询的网络段，可以限制网络发现。  

**子网：**  

配置网络发现在使用 SNMP 和 DHCP 选项时查询的子网。 这两个选项仅搜索启用的子网。  

例如，DHCP 请求可以从整个网络内的位置中返回设备。 如果只想发现特定子网上的设备，请在“网络发现属性”对话框中的“子网”选项卡上指定和启用该特定子网。 指定和启用子网时，将未来的 DHCP 和 SNMP 发现任务限制为仅针对那些子网。  

> [!NOTE]  
>  子网配置不限制**域**发现选项发现的对象。  

**SNMP 共同体名称：**  

要使网络发现能够成功查询 SNMP 设备，请使用设备的社区名称配置网络发现。 如果未使用 SNMP 设备的社区名称来配置网络发现，则设备会拒绝查询。  

**最大跃点数：**  

配置最大路由器跃点数时，你可以限制网络发现能够使用 SNMP 查询的网络段和路由器的数目。  

你配置的跃点数可以限制网络发现可以查询的其他设备和网络段的数目。  

例如，路由器跃点数为“0” （零）的仅拓扑的发现会发现发起服务器所在的子网。 它包含该子网上的任何路由器。  

下图显示了在路由器跃点数指定为 0 的服务器 1 上运行仅拓扑的网络发现查询时，该网络发现查询所找到的内容：子网 D 和路由器 1。  

 ![路由器跃点为零的发现图像](media/Disc-0.gif)  

 下图显示了在路由器跃点数指定为 0 的服务器 1 上运行拓扑和客户端网络发现查询时，该网络发现查询所找到的内容：子网 D 和路由器 1，以及子网 D 上的所有潜在客户端。  

 ![有一个路由器跃点的发现图像](media/Disc-1.gif)  

 为了更好地了解其他路由器跃点如何增加发现的网络资源量，请考虑以下网络：  

 ![有两个路由器跃点的发现图像](media/Disc-2.gif)  

 从具有一个路由器跃点的服务器 1 中运行仅限拓扑的网络发现将发现以下各项：  

-   路由器 1 和子网 10.1.10.0（已找到，跃点数为零）  

-   子网 10.1.20.0 和 10.1.30.0、子网 A 和路由器 2（在第一个跃点上找到）  

> [!WARNING]  
>  路由器跃点数每增加一个都可能大幅增加可发现的资源数，并增加网络发现所使用的网络带宽。  

##  <a name="bkmk_aboutServer"></a>服务器发现  
**可配置：**否  

除了用户可配置的发现方法之外，Configuration Manager 还使用名为**服务器发现** (SMS_WINNT_SERVER_DISCOVERY_AGENT) 的进程。 此发现方法为作为站点系统的计算机（如配置为管理点的计算机）创建资源记录。  

##  <a name="bkmk_shared"></a>Active Directory 组发现、系统发现和用户发现的常用功能  
本部分提供以下发现方法常见功能的相关信息：  

-   Active Directory 组发现  

-   Active Directory 系统发现  

-   Active Directory 用户发现  

> [!NOTE]  
>  本部分中的信息不适用于 Active Directory 林发现。  

这三种发现方法的配置和操作类似。 它们可以发现计算机、用户以及关于 Active Directory 域服务中存储的资源的组成员身份信息。 发现进程由发现代理进行管理，该发现代理在每个站点中配置为运行发现的站点服务器上运行。 你可以将其中每种发现方法配置为搜索一个或多个 Active Directory 位置，并将其作为本地林或远程林中的位置实例。  

当发现在不受信任的林中搜索资源时，发现代理必须能够解析以下对象，才能成功进行操作：  

-   若要使用 Active Directory 系统发现来发现计算机资源，发现代理必须能够解析资源的 FQDN。 如果无法解析 FQDN，则它将尝试通过资源的 NetBIOS 名称来解析资源。  

-   若要使用 Active Directory 用户发现或 Active Directory 组发现来发现用户或组资源，发现代理必须能够解析为 Active Directory 位置指定的域控制器名称的 FQDN。  

对于指定的每个位置，可以配置单个搜索选项，如启用位置的 Active Directory 子容器的递归搜索。 也可以将唯一帐户配置为在搜索该位置时使用。 这样，你可以灵活地在一个站点配置发现方法以跨多个林搜索多个 Active Directory 位置，而不必配置对所有位置拥有权限的单个帐户。  

在特定站点运行这三种发现方法中的每种发现方法时，该站点中的 Configuration Manager 站点服务器会与指定 Active Directory 林中最近的域控制器联系，以查找 Active Directory 资源。 域和林可以处于任何支持的 Active Directory 模式下。 分配给每个位置实例的帐户必须对指定的 Active Directory 位置具有“读取”访问权限。

发现会在指定位置中搜索对象，然后尝试收集有关那些对象的信息。 如果能够确定足够的资源相关信息，则将创建 DDR。 所需信息因使用的发现方法而异。  

如果将同一发现方法配置为在不同的 Configuration Manager 站点上运行，以利用查询本地 Active Directory 服务器的优势，可以将每个站点配置为包含一组独特的发现选项。 由于发现数据与层次结构中的每个站点共享，因此请避免这些配置之间出现重叠，以一次性高效地发现每个资源。

对于较小的环境，可以考虑仅在层次结构中的一个站点上运行每个发现方法，以减少管理开销并降低多个发现操作重新发现同一资源的可能性。 将运行发现的站点数量减至最少时，可降低该发现所使用的整体网络带宽。 此外，还可以减少所创建的且必须由站点服务器进行处理的 DDR 的总体数量。  

许多发现方法配置是一目了然的。 使用下列部分来了解有关在你对其进行配置之前可能需要其他信息的发现选项的详细信息。  

以下选项适用于与多个 Active Directory 发现方法配合使用：  

-   [增量发现](#bkmk_delta)  

-   [按域登录名筛选过期计算机记录](#bkmk_stalelogon)  

-   [按计算机密码筛选过期记录](#bkmk_stalepassword)  

-   [搜索自定义的 Active Directory 属性](#bkmk_customAD)  

###  <a name="bkmk_delta"></a>增量发现  
适用于：  

-   Active Directory 组发现  

-   Active Directory 系统发现  

-   Active Directory 用户发现  

增量发现不是独立的发现方法，而是可用于适用发现方法的选项。 增量发现会搜索特定的 Active Directory 属性，查找自适用的发现方法的上一次完整发现周期以来所做的更改。 此属性更改会提交至 Configuration Manager 数据库，以更新资源的发现记录。  

默认情况下，增量发现按 5 分钟一个周期进行运行。 这比完整发现周期的典型计划要更为频繁。  此频繁周期之所以可行，是因为增量发现使用的站点服务器和网络资源比完整发现周期使用的少。 使用增量发现时，可针对该发现方法减小完整发现周期的频率。  

增量发现检测到的最常见更改如下：  

-   添加到 Active Directory 中的新计算机或用户  

-   对基本计算机和用户信息所做的更改  

-   添加到组中的新计算机或用户  

-   从组中删除的计算机或用户  

-   对系统组对象所做的更改  

虽然增量发现可以检测新资源以及对组成员身份所做的更改，但它无法检测从 Active Directory 中删除资源的时间。 对增量发现所创建的 DDR 进行处理的方式类似于由完整发现周期创建的 DDR。  

你在每个发现方法的属性中的“轮询计划”  选项卡上配置增量发现。  

###  <a name="bkmk_stalelogon"></a>按域登录名筛选过期计算机记录  
适用于：  

-   Active Directory 组发现  

-   Active Directory 系统发现  

可以配置发现，以根据计算机的最后一个域登录名排除具有过期计算机记录的计算机。 如果启用此选项，Active Directory 系统发现将评估它识别的每台计算机。 Active Directory 组发现将评估作为所发现的组的成员的每台计算机。  

使用此选项：  

-   必须将计算机配置为更新 Active Directory 域服务中的 **lastLogonTimeStamp** 属性。  

-   必须将 Active Directory 域功能级别设置为 Windows Server 2003 或更高版本。  

在配置上一次登录后的时间（想要用于此设置）时，请考虑域控制器之间的复制间隔。  

可在“Active Directory 系统发现属性”和“Active Directory 组发现属性”对话框中的“选项”选项卡上配置筛选。 选择“仅发现登录到域一段给定时间的计算机”选项。  

> [!WARNING]  
>  如果配置此筛选，并且**按计算机密码筛选过期记录**，则会从发现中排除满足任一筛选器条件的计算机。  

###  <a name="bkmk_stalepassword"></a>按计算机密码筛选过期记录  
适用于：  

-   Active Directory 组发现  

-   Active Directory 系统发现  

可以配置发现，以根据计算机进行的最后一次计算机帐户密码更新，排除具有过期计算机记录的计算机。 如果启用此选项，Active Directory 系统发现将评估它识别的每台计算机。 Active Directory 组发现将评估作为所发现的组的成员的每台计算机。  

使用此选项：  

-   必须将计算机配置为更新 Active Directory 域服务中的 **pwdLastSet** 属性。  

在配置此选项时，除了考虑域控制器之间的复制间隔外，还要考虑此属性的更新间隔。  

可在“Active Directory 系统发现属性”和“Active Directory 组发现属性”对话框中的“选项”选项卡上配置筛选。 选择“仅发现具有更新的计算机帐户密码一段给定时间的计算机”选项。  

> [!WARNING]  
>  如果配置此筛选，并且**按域登录名筛选过期记录**，则会从发现中排除满足任一筛选器条件的计算机。  

###  <a name="bkmk_customAD"></a>搜索自定义的 Active Directory 属性  
 适用于：  

-   Active Directory 系统发现  

-   Active Directory 用户发现  

每种发现方法都支持可发现的 Active Directory 属性的唯一列表。  

可在“Active Directory 系统发现属性”和“Active Directory 用户发现属性”对话框中的“Active Directory 属性”选项卡上，查看和配置自定义属性列表。  
