---
title: "配置发现 | Microsoft Docs"
description: "配置发现方法，以在 Configuration Manager 站点运行，从而找到可以从网络基础结构和 Active Directory 管理的资源。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 34a539ceaea6b070f81a28d2c0a9ce388e26cfeb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>配置 System Center Configuration Manager 的发现方法

*适用范围：System Center Configuration Manager (Current Branch)*


配置发现方法，以在 System Center Configuration Manager site 站点运行，从而找到可以从网络基础结构和 Active Directory 管理的资源。 这需要启用要用于搜索环境的每种方法并进行配置。 （也可通过使用与启用相同的过程来禁用某种方法。）其中两个例外情况是检测信号发现和服务器发现：  

-   默认情况下，安装 Configuration Manager 主站点时，检测信号已处于启用状态，并配置为按基本计划运行。 保持检测信号发现为启用状态是个好办法，因为此方法可确保设备的发现数据记录 (DDR) 保持最新。 有关检测信号发现的详细信息，请参阅[关于检测信号发现](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。  

-   服务器发现是一种自动发现方法，用于查找用作站点系统的计算机。 不能对其进行配置或将其禁用。  

**启用可配置的发现方法：**  
 > [!NOTE]  
 > 以下信息不适用于 Azure Active Directory 用户发现。 请参阅本主题后续部分的[配置 Azure AD 用户发现](#azureaadisc)。

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为要在其中启用发现的站点选择发现方法。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”，然后在“常规”选项卡上，选中“启用&lt;发现方法\>”复选框。  

     如果此复选框已处于选中状态，可以通过取消选中复选框来禁用发现方法。  

4.  选择“确定”保存配置。  


##  <a name="BKMK_ConfigADForestDisc"></a>配置 Active Directory 林发现  
若要完成 Active Directory 林发现的配置，必须在两个位置中配置设置：  

-   在“发现方法”节点中，可以：

    - 启用此发现方法。
    - 设置轮询计划。
    - 选择发现是否为其发现的 Active Directory 站点和子网自动创建边界。  

-   在“Active Directory 林”节点中，可以：

    - 添加想要发现的林。
    - 启用对该林中 Active Directory 站点和子网的发现。
    - 将启用 Configuration Manager 站点的设置配置为将其站点信息发布到林。
    - 为每个林分配一个帐户以用作 Active Directory 林帐户。  

使用以下过程来启用 Active Directory 林发现，并配置单独的林以用于 Active Directory 林发现。  

#### <a name="to-enable-active-directory-forest-discovery"></a>启用 Active Directory 林发现  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为要在其中配置发现的站点选择“Active Directory 林发现”方法。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  在“常规”选项卡上，选中复选框以启用发现。 或者可以立即配置发现，然后稍后返回以启用发现。  

5.  指定为发现的位置创建站点边界的选项。  

6.  指定有关发现何时运行的计划。  

7.  完成为此站点配置 Active Directory 林发现的操作后，选择“确定”保存配置。  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>为 Active Directory 林发现配置林  

1.  在“管理”工作区中，选择“Active Directory 林”。 如果 Active Directory 林发现之前已运行，你将在结果窗格中看到每个发现的林。 当 Active Directory 林发现运行时，将发现本地林和任何受信任林。 只有不受信任的林才必须手动添加。  

    -   若要配置先前发现的林，请在结果窗格中选择林。 然后在“主页”选项卡上的“属性”组中，选择“属性”以打开林属性。 继续执行步骤 3。  

    -   若要配置未列出的新林，请在“主页”选项卡上的“创建”组中选择“添加林”以打开“添加林”对话框。 继续执行步骤 3。  

2.  在“常规”选项卡上，为要发现的林完成配置，并指定“Active Directory 林帐户”。  

    > [!NOTE]  
    >  Active Directory 林发现需要全局帐户才能发现和发布到不受信任林。 如果不使用站点服务器的计算机帐户，则只能选择全局帐户。  

3.  如果打算允许站点将站点数据发布到此林，请在“发布”选项卡上完成用于发布到此林的配置。  

    > [!NOTE]  
    >  如果允许站点发布到林，则必须为 Configuration Manager 扩展该林的 Active Directory 架构。 Active Directory 林帐户必须对该林中的“系统”容器拥有“完全控制”权限。  

4.  完成配置此林以用于 Active Directory 林发现的操作后，选择“确定”保存配置。  

##  <a name="BKMK_ConfigADDiscGeneral"></a>为计算机、用户或组配置 Active Directory 发现  
 使用下列部分中的信息来配置计算机、用户或组的发现。 将使用这些发现方法：  

-   Active Directory 组发现  

-   Active Directory 系统发现  

-   Active Directory 用户发现  

> [!NOTE]  
>  本部分中的信息不适用于 Active Directory 林发现。  

 尽管每种发现方法都相互独立，但它们共用类似的选项。 有关这些配置选项的详细信息，请参阅[组、系统和用户发现的共享选项](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared)。  

> [!WARNING]  
>  每种发现方法进行的 Active Directory 轮询可能会产生大量的网络流量。 请考虑将每种发现方法安排为在此网络流量不会对企业的网络使用造成负面影响时运行。  

#### <a name="to-configure-active-directory-group-discovery"></a>配置 Active Directory 组发现  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为要在其中配置发现的站点选择“Active Directory 组发现”方法。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  在“常规”选项卡上，选中复选框以启用发现。 或者可以立即配置发现，然后稍后返回以启用发现。  

5.  选择“添加”以配置发现作用域，选择“组”或“位置”，并在“添加组”或“添加 Active Directory 位置”对话框中完成以下配置：  

    1.  为此发现作用域指定“名称”  。  

    2.  指定要搜索的“Active Directory 域”  或“位置”  ：  

        -   如果选择了“组”，请指定要发现的一个或多个 Active Directory 组。  

        -   如果选择了“位置”，请指定 Active Directory 容器作为要发现的位置。 你也可以为此位置启用对 Active Directory 子容器的递归搜索。  

    3.  指定用于搜索此发现作用域的“Active Directory 组发现帐户”  。  

    4.  选择“确定”保存发现作用域配置。  

6.  为要定义的每个其他发现作用域重复步骤 6。  

7.  在“轮询计划”  选项卡上，配置完整发现轮询计划和增量发现。  

8.  （可选）在“选项”选项卡上，可以配置选项以从发现中筛选出或排除过期计算机记录，并发现通讯组的成员身份。  

    > [!NOTE]  
    >  默认情况下，Active Directory 组发现只会发现安全组的成员身份。  

9. 完成为此站点配置 Active Directory 组发现的操作后，选择“确定”保存配置。  

#### <a name="to-configure-active-directory-system-discovery"></a>配置 Active Directory 系统发现  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为要在其中配置发现的站点选择方法。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  在“常规”选项卡上，选中复选框以启用发现。 或者可以立即配置发现，然后稍后返回以启用发现。  

5.  选择“新建”图标![新建图标](media/Disc_new_Icon.gif)以指定新的 Active Directory 容器。 在“Active Directory 容器”对话框框中，完成以下配置：  

    1.  指定要搜索的一个或多个位置。  

    2.  对于每个位置，指定更改搜索行为的选项。  

    3.  对于每个位置，指定要用作“Active Directory 发现帐户” 的帐户。  

        > [!TIP]  
        >  对于指定的每个位置，你可以配置一组发现选项和唯一的 Active Directory 发现帐户。  

    4.  选择“确定”保存 Active Directory 容器配置。  

6.  在“轮询计划”  选项卡上，配置完整发现轮询计划和增量发现。  

7.  （可选）在“Active Directory 属性”  选项卡上，你可以为要发现的计算机配置其他 Active Directory 属性。 还会列出默认对象属性。  

8.  （可选）在“选项”选项卡上，可以配置选项以从发现中筛选出或排除过期计算机记录。  

9. 完成为此站点配置 Active Directory 系统发现的操作后，选择“确定”保存配置。  

#### <a name="to-configure-active-directory-user-discovery"></a>配置 Active Directory 用户发现  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为要在其中配置发现的站点选择“Active Directory 用户发现”方法。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  在“常规”选项卡上，选中复选框以启用发现。 或者可以立即配置发现，然后稍后返回以启用发现。  

5.  选择“新建”图标![新建图标](media/Disc_new_Icon.gif)以指定新的 Active Directory 容器。 在“Active Directory 容器”对话框框中，完成以下配置：  

    1.  指定要搜索的一个或多个位置。  

    2.  对于每个位置，指定更改搜索行为的选项。  

    3.  对于每个位置，指定要用作“Active Directory 发现帐户” 的帐户。  

        > [!NOTE]  
        >  对于指定的每个位置，你可以配置一组唯一的发现选项和唯一的 Active Directory 发现帐户。  

    4.  选择“确定”保存 Active Directory 容器配置。  

6.  在“轮询计划”  选项卡上，配置完整发现轮询计划和增量发现。  

7.  （可选）在“Active Directory 属性”  选项卡上，你可以为要发现的计算机配置其他 Active Directory 属性。 还会列出默认对象属性。  

8.  完成为此站点配置 Active Directory 用户发现的操作后，选择“确定”保存配置。  

## <a name="azureaadisc"></a>配置 Azure AD 用户发现
从版本 1706 开始，可在将 Configuration Manager 连接到 [Azure 订阅和 Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) 时配置 Azure Active Directory 用户发现。

将 Azure AD 用户发现配置为云管理的一部分。 主题“配置 Azure 服务以用于 Configuration Manager”的[创建 Azure Web 应用以用于 Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) 中详细介绍了执行此操作的过程。




##  <a name="BKMK_ConfigHBDisc"></a>配置检测信号发现  
 默认情况下，检测信号发现在安装 Configuration Manager 主站点时启用。 因此，若不想使用每隔 7 天的默认设置，只需配置有关客户端将检测信号发现数据记录发送到管理点的频率的计划。  

> [!NOTE]  
>  如果在同一站点上同时启用了“清除安装标志”  客户端请求安装和站点维护任务，请将检测信号发现的计划设置为小于“清除安装标志”  站点维护任务的“客户端重新发现期间”  。 有关站点维护任务的详细信息，请参阅 [System Center Configuration Manager 的维护任务](../../../../core/servers/manage/maintenance-tasks.md)。  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>配置检测信号发现计划  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为要在其中配置检测信号发现的站点选择“检测信号发现”。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  配置客户端提交检测信号发现数据记录的频率，然后选择“确定”保存配置。  

##  <a name="BKMK_ConfigNetworkDisc"></a>配置网络发现  
 使用下列部分中的信息来帮助你配置网络发现。  

###  <a name="BKMK_AboutConfigNetworkDisc"></a>关于配置网络发现  
 在配置网络发现之前，你必须了解以下各项：  

-   网络发现的可用级别  

-   可用的网络发现选项  

-   在网络上限制网络发现  

有关详细信息，请参阅[关于网络发现](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork)。  

 下列部分提供有关网络发现的常见配置的信息。 你可以配置其中一个或多个配置以在同一发现轮次中使用。 如果使用多个配置，你必须规划可能影响发现结果的交互。  

 例如，可能会希望发现使用特定 SNMP 共同体名称的所有简单网络管理协议 (SNMP) 设备。 此外，对于同一发现轮次，你可以禁用针对特定子网的发现。 当发现运行时，网络发现不会发现你已禁用的子网上具有指定共同体名称的 SNMP 设备。  

####  <a name="BKMK_DetermineNetTopology"></a>确定网络拓扑  
 你可以使用仅拓扑发现来映射你的网络。 这种类型的发现不会发现潜在客户端。 仅拓扑网络发现依赖于 SNMP。  

 映射网络拓扑时，必须在“网络发现属性”对话框中的“SNMP”选项卡上配置“最大跃点数”。 只需一些跃点，便可以帮助控制运行发现时使用的网络带宽。 在发现网络的更多内容时，可以增加跃点数以更好地了解网络拓扑。  

 了解网络拓扑后，可以配置网络发现的其他属性， 以在使用可用配置限制网络发现能够搜索的网络段时发现潜在的客户端及其操作系统。  

####  <a name="BKMK_LimitBySubnet"></a>使用子网限制搜索  
 可以将网络发现配置为在发现运行期间搜索特定子网。 默认情况下，网络发现会搜索运行发现的服务器的子网。 配置和启用的任何其他子网仅适用于 SNMP 和动态主机配置协议 (DHCP) 搜索选项。 当网络发现搜索域时，子网配置未对其进行限制。  

 如果你在“网络发现属性”  对话框中的“子网”  选项卡上指定一个或多个子网，则仅搜索标记为“已启用”  的子网。  

 禁用子网后，会从发现中排除此子网，并且以下条件适用：  

-   不在子网上运行基于 SNMP 的查询。  

-   DHCP 服务器未以位于子网上的资源的列表形式予以回复。  

-   基于域的查询可以发现位于子网上的资源。  

####  <a name="BKMK_SearchByDomain"></a>搜索特定域  
 可以将网络发现配置为在发现运行期间搜索特定域或一组域。 默认情况下，网络发现会搜索运行发现的服务器的本地域。  

 如果你在“网络发现属性”  对话框中的“域”  选项卡上指定一个或多个域，则仅搜索标记为“已启用”  的域。  

 禁用域后，会从发现中排除此域，并且以下条件适用：  

-   网络发现不查询该域中的域控制器。  

-   基于 SNMP 的查询仍然可以在域中的子网上运行。  

-   DHCP 服务器仍然能够以位于域中的资源的列表形式予以回复。  

####  <a name="BKMK_LimitBySNMPname"></a>使用 SNMP 共同体名称限制搜索  
 可以将网络发现配置为在发现运行期间搜索特定 SNMP 共同体或一组共同体。 默认情况下，为使用配置了“公共”  共同体名称。  

 网络发现使用共同体名称来获得对路由器（SNMP 设备）的访问权。 路由器可以向网络发现提供有关链接到第一个路由器的其他路由器和子网的信息。  

> [!NOTE]  
>  SNMP 共同体名称类似于密码。 网络发现只能从已指定共同体名称的 SNMP 设备中获得信息。 每个 SNMP 设备均可以拥有自己的共同体名称，但是同一个共同体名称通常会由几个设备共享。 此外，大多数 SNMP 设备都有默认的“公共” 共同体名称。 但某些组织会删除其设备的“公共”共同体名称以作为安全措施。  

 如果“网络发现属性”对话框中的“SNMP”选项卡上显示了多个 SNMP 共同体，则网络发现按照共同体的显示顺序搜索共同体。 为了帮助最大程度降低因使用不同名称尝试连接设备所产生的网络流量，请确保最频繁使用的名称位于列表的顶部。  

> [!NOTE]  
>  除了使用 SNMP 共同体名称之外，还可以指定特定 SNMP 设备的 IP 地址或可解析名称。 可使用“网络发现属性”对话框的“SNMP 设备”选项卡来执行此操作。  

####  <a name="BKMK_SearchByDHCP"></a>搜索特定的 DHCP 服务器  
 可以将网络发现配置为使用特定 DHCP 服务器或多个服务器在发现运行期间发现 DHCP 客户端。  

 网络发现搜索你在“网络发现属性”  对话框中的“DHCP”  选项卡上指定的每个 DHCP 服务器。 如果正在运行发现的服务器从 DHCP 服务器中租赁其 IP 地址，则可以通过选中“包括要将站点服务器配置为使用的 DHCP 服务器”复选框将发现配置为搜索该 DHCP 服务器。  

> [!NOTE]  
>  为了在网络发现中成功配置 DHCP 服务器，你的环境必须支持 IPv4。 你无法将网络发现配置为使用本机 IPv6 环境中的 DHCP 服务器。  

###  <a name="BKMK_HowToConfigNetDisc"></a>如何配置网络发现  
 使用以下过程首先仅发现网络拓扑，然后使用一个或多个可用的网络发现选项将网络发现配置为发现潜在客户端。  

##### <a name="to-determine-your-network-topology"></a>确定网络拓扑  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为想要在其中运行网络发现的站点选择“网络发现”。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

    -   在“常规”选项卡上，选中“启用网络发现”复选框，然后从“发现类型”选项中选择“拓扑”。  

    -   在“子网”选项卡上，选中“搜索本地子网”复选框。  

        > [!TIP]  
        >  如果知道构成网络的特定子网，则可以取消选中“搜索本地子网”复选框并使用“新建”图标![新建图标](media/Disc_new_Icon.gif)来添加要搜索的特定子网。 对于大型网络，通常最好一次仅搜索一两个子网，以最大程度降低网络带宽使用量。  

    -   在“域”选项卡上，选中“搜索本地域”复选框。  

    -   在“SNMP”  选项卡上，使用“最大跃点数”  下拉列表指定在映射拓扑过程中网络发现可以接受的路由器跃点数。  

        > [!TIP]  
        >  首次映射网络拓扑时，请仅配置少量路由器跃点以最大程度降低网络带宽使用量。  

4.  在“计划”选项卡上，选择“新建”图标![新建图标](media/Disc_new_Icon.gif)以设置用于运行网络发现的计划。  

    > [!NOTE]  
    >  你无法将不同的发现配置分配给单独的网络发现计划。 每次运行网络发现时，它都使用当前发现配置。  

5.  选择“确定”以接受配置。 网络发现将按计划的时间运行。  

##### <a name="to-configure-network-discovery"></a>配置网络发现  

1.  在 Configuration Manager 控制台中，依次选择“管理” > “层次结构配置”，然后选择“发现方法”。  

2.  为想要在其中运行网络发现的站点选择“网络发现”。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  在“常规”选项卡上，选中“启用网络发现”复选框，然后从“发现类型”选项中选择想要运行的发现的类型。  

5.  若要将发现配置为搜索子网，请选择“子网”选项卡，然后配置以下一个或多个选项：  

    -   若要在运行发现的计算机的本地子网上运行发现，请选中“搜索本地子网”复选框。  

    -   若要搜索特定子网，请确保该子网在“要搜索的子网”中列出，并且其“搜索”值必须为“已启用”：  

        1.  如果未列出子网，请选择“新建”图标![新建图标](media/Disc_new_Icon.gif)。 在“新建子网分配”对话框中，输入“子网”和“掩码”信息，然后选择“确定”。 默认情况下，为搜索启用了新子网。  

        2.  若要更改所列子网的“搜索”值，请选择子网，然后选择“切换”图标以在“已禁用”和“已启用”之间切换。  

6.  若要将发现配置为搜索域，请选择“域”选项卡，然后配置以下一个或多个选项：  

    -   若要在运行发现的计算机的域上运行发现，请选中“搜索本地域”复选框。  

    -   若要搜索特定域，请确保该域在“域”中列出，并且其“搜索”值必须为“已启用”：  

        1.  如果未列出域，请选择“新建”图标![新建图标](media/Disc_new_Icon.gif)。 在“域属性”对话框中，输入**域**信息，然后选择“确定”。 默认情况下，为搜索启用了新域。  

        2.  若要更改所列域的“搜索”值，请选择域，然后选择“切换”图标以在“已禁用”和“已启用”之间切换。  

7.  若要将发现配置为搜索 SNMP 设备的特定 SNMP 共同体名称，请选择“SNMP”选项卡，然后配置以下一个或多个选项：  

    -   要将 SNMP 共同体名称添加到“SNMP 共同体名称”列表中，选择“新建”图标![新建图标](media/Disc_new_Icon.gif)。 在“新建 SNMP 共同体名称”对话框中，指定 SNMP 共同体的**名称**，然后选择“确定”。  

    -   若要删除 SNMP 共同体名称，请选择共同体名称，然后选择“删除”图标![删除图标](media/Disc_delete_Icon.gif)。  

    -   若要调整 SNMP 共同体名称的搜索顺序，请选择共同体名称，然后选择“上移项目”图标![上移项目](media/Disc_moveUp_Icon.gif)，或“下移项目”图标![下移项目](media/Disc_moveDown_Icon.gif)。 当运行发现时，会按照从上向下的顺序搜索共同体名称。 请记住下列几点。

        > [!NOTE]  
        >  网络发现使用 SNMP 共同体名称来获得对路由器（SNMP 设备）的访问权。 路由器可以通知网络发现有关链接到第一个路由器的其他路由器和子网的信息。  

        -   SNMP 共同体名称类似于密码。  

        -   网络发现只能从已指定共同体名称的 SNMP 设备中获得信息。  

        -   每个 SNMP 设备均可以拥有自己的共同体名称，但是同一个共同体名称通常会由几个设备共享。  

        -   大多数 SNMP 设备都有默认的**公共**共同体名称。 如果不知道任何其他共同体名称，则可以使用此名称。 但是，某些组织将删除其设备的“公共”  共同体名称以作为安全措施。  

8.  若要配置供 SNMP 搜索使用的最大路由器跃点数，请选择“SNMP”选项卡，然后从“最大跃点数”下拉列表中选择跃点数。  

9. 要配置 SNMP 设备，选择“SNMP 设备”选项卡。 如果未列出设备，请选择“新建”图标![新建图标](media/Disc_new_Icon.gif)。 在“新建 SNMP 设备”对话框中，指定 SNMP 设备的 IP 地址或设备名称，然后选择“确定”。  

    > [!NOTE]  
    >  如果指定设备名称，则 Configuration Manager 必须能够将 NetBIOS 名称解析为 IP 地址。  

10. 若要将发现配置为查询 DHCP 客户端的特定 DHCP 服务器，请单击“DHCP”选项卡，然后配置以下一个或多个选项：  

    -   若要在运行发现的计算机上查询 DHCP 服务器，请选中“始终使用站点服务器的 DHCP 服务器”复选框。  

        > [!NOTE]  
        >  为了使用此选项，服务器必须从 DHCP 服务器租赁其 IP 地址，并且不能使用静态 IP 地址。  

    -   要查询特定的 DHCP 服务器，选择“新建”图标![新建图标](media/Disc_new_Icon.gif)。 在“新建 DHCP 服务器”对话框中指定 DHCP 服务器的 IP 地址或服务器名称，然后选择“确定”。  

        > [!NOTE]  
        >  如果指定服务器名称，则 Configuration Manager 必须能够将 NetBIOS 名称解析为 IP 地址。  

11. 若要配置发现运行的时间，请选择“计划”选项卡，然后选择“新建”图标![新建图标](media/Disc_new_Icon.gif)以设置用于运行网络发现的计划。  

     可以配置多个重复计划以及多个无重复计划。  

    > [!NOTE]  
    >  如果“计划”选项卡上同时显示多个计划，则所有计划均会根据在配置时该计划中指示的时间运行网络发现。 循环计划也是如此。  

12. 选择“确定”保存配置。  

###  <a name="BKMK_HowToVerifyNetDisc"></a>如何验证网络发现是否已完成  
 完成网络发现所需的时间可能因多种因素而异。 这些因素可能包括以下一项或多项：  

-   你的网络规模  

-   你的网络拓扑  

-   为在网络中查找路由器而配置的最大跃点数  

-   正在运行的发现的类型  

因为网络发现不会在发现完成时创建消息来通知你，所以你可以使用以下过程来验证是否完成了发现。  

##### <a name="to-verify-that-network-discovery-has-finished"></a>验证是否完成了网络发现  

1.  在 Configuration Manager 控制台中，选择“监视”。  

2.  在“监视”工作区中，展开“系统状态”，然后选择“状态消息查询”。  

3.  选择“所有状态消息”。  

4.  在“主页”选项卡上的“状态消息查询”组中，选择“显示消息”。  

5.  在“选择日期和时间”下拉列表中，选择一个说明多久之前启动发现的值，然后选择“确定”以打开“Configuration Manager 状态消息查看器”。  

    > [!TIP]  
    >  你也可以使用“指定日期和时间”  选项选择运行发现的指定日期和时间。 当你在指定日期运行网络发现并且想要仅检索该日期中的消息时，此选项很有用。  

6.  要验证网络发现是否已经完成，请搜索具有以下详细信息的状态消息：  

    -   消息 ID： **502**  

    -   组件： **SMS_NETWORK_DISCOVERY**  

    -   描述： **此组件已停止**  

    如果不存在此状态消息，则网络发现尚未完成。  

7.  要验证网络发现的启动时间，请搜索具有以下详细信息的状态消息：  

    -   消息 ID： **500**  

    -   组件： **SMS_NETWORK_DISCOVERY**  

    -   描述： **此组件已启动**  

    此信息验证是否已启动网络发现。 如果没有此信息，请重新计划网络发现。  
