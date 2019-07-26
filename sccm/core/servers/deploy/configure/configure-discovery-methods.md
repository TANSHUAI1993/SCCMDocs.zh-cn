---
title: 配置发现
titleSuffix: Configuration Manager
description: 配置发现方法，从网络、Active Directory 和 Azure Active Directory 找到要管理的资源。
ms.date: 08/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17851c3d90bfd8ffedc0ab3b40fec4362ab0d8ea
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68338163"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>配置 Configuration Manager 的发现方法

适用范围：  System Center Configuration Manager (Current Branch)


配置发现方法，从网络、Active Directory 和 Azure Active Directory (Azure AD) 找到要管理的资源。 首先启用要用于搜索环境的每种方法，然后对这些方法进行配置。 也可通过使用与启用相同的过程来禁用某种方法。 此过程的其中两个例外情况是检测信号发现和服务器发现：  

-  默认情况下，检测信号发现在安装 Configuration Manager 主站点时就已经启用。 它配置为按照一个基本计划运行。 请保持检测信号发现为启用状态。 此方法可确保设备的发现数据记录 (DDR) 保持最新。 有关检测信号发现的详细信息，请参阅[关于检测信号发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat)。  

-  服务器发现是一种自动发现方法。 它查找用作站点系统的计算机。 不能对其进行配置或将其禁用。  

### <a name="enable-a-configurable-discovery-method"></a>启用可配置的发现方法  
> [!NOTE]  
> 以下信息不适用于 Azure AD 用户发现。 Azure AD 用户请参阅本文后续部分的[配置 Azure AD 用户发现](#azureaadisc)。

1.  在 Configuration Manager 控制台中的“管理”  工作区中，展开“层次结构配置”  ，然后选择“发现方法”  。  

2.  为要在其中启用发现的站点选择发现方法。  

3.  在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。 接下来在“常规”  选项卡上，选择“启用&lt;发现方法\>”  选项。  

    如果该选项已启用，可以通过取消选中复选框来禁用发现方法。  

4.  选择“确定”  保存配置。  



##  <a name="BKMK_ConfigADForestDisc"></a>配置 Active Directory 林发现  

若要完成 Active Directory 林发现的配置，请在 Configuration Manager 控制台的以下位置中配置这些设置：  

- 在“发现方法”  节点中：

  - 启用此发现方法。  

  - 设置轮询计划。  

  - 选择发现是否为其发现的 Active Directory 站点和子网自动创建边界。  

- 在“Active Directory 林”  节点中：

  - 添加想要发现的林。  

  - 启用对该林中 Active Directory 站点和子网的发现。  

  - 将启用 Configuration Manager 站点的设置配置为将其站点信息发布到林。  

  - 为每个林分配一个帐户以用作 Active Directory 林帐户。  

使用以下过程来启用 Active Directory 林发现，并配置单独的林以用于 Active Directory 林发现。  


### <a name="enable-active-directory-forest-discovery"></a>启用 Active Directory 林发现  

1.  在 Configuration Manager 控制台中的“管理”  工作区中，展开“层次结构配置”  ，然后选择“发现方法”  节点。  

2.  为要在其中配置发现的站点选择“Active Directory 林发现”方法。  

3.  在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4.  在“常规”  选项卡上，选中复选框以启用发现。 或者可以立即配置发现，然后稍后返回以启用发现。  

5.  指定为发现的位置创建站点边界的选项。  

6.  指定有关发现何时运行的计划。  

7.  选择“确定”  保存配置。  


### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>为 Active Directory 林发现配置林  

1.  在“管理”  工作区中，展开“层次结构配置”  ，然后选择“Active Directory 林”  节点。 如果 Active Directory 林发现之前已运行，你将在结果窗格中看到每个发现的林。 当 Active Directory 林发现运行时，将发现本地林和任何受信任林。 你只需手动添加不受信任的林。  

    - 若要配置先前发现的林，请在结果窗格中选择林。 然后在功能区“主页”  选项卡上的“属性”  组中，选择“属性”  以打开林属性。 继续执行步骤 3。  

    - 若要配置未列出的新林，请在功能区“主页”  选项卡上的“创建”  组中，选择“添加林”  。 此操作将打开“添加林”  对话框。 继续执行步骤 3。  

2.  在“常规”  选项卡上，为要发现的林完成配置，并指定“Active Directory 林帐户”  。 有关此帐户的详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#active-directory-forest-account)。  

    > [!NOTE]  
    > Active Directory 林发现需要全局帐户才能发现和发布到不受信任林。 如果不使用站点服务器的计算机帐户，则只能选择全局帐户。  

3.  如果打算允许站点将站点数据发布到此林，请在“发布”  选项卡上完成用于发布到此林的配置。  

    > [!NOTE]  
    > 如果允许站点发布到林，则为 Configuration Manager 扩展该林的 Active Directory 架构。 Active Directory 林帐户必须对该林中的“系统”容器拥有“完全控制”权限。  

4.  选择“确定”  保存配置。  



##  <a name="BKMK_ConfigADDiscGeneral"></a> 为计算机、用户或组配置 Active Directory 发现  

若要配置计算机、用户或组的发现，开始执行以下常见步骤：

1.  在 Configuration Manager 控制台中的“管理”  工作区中，展开“层次结构配置”  ，然后选择“发现方法”  节点。  

2.  为要在其中配置发现的站点选择方法。  

3.  在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4.  在“常规”  选项卡上，选中复选框以启用发现。 或者可以立即配置发现，然后稍后返回以启用发现。  

然后使用下列部分中的信息来配置特定发现方法：  

- [Active Directory 组发现](#bkmk_config-adgd)  

- [Active Directory 系统发现](#bkmk_config-adgd)  

- [Active Directory 用户发现](#bkmk_config-adud)  

> [!NOTE]  
> 本部分中的信息不适用于 Active Directory 林发现。  

 尽管每种发现方法都相互独立，但它们共用类似的选项。 有关这些配置选项的详细信息，请参阅[组、系统和用户发现的共享选项](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_shared)。  

> [!WARNING]  
> 每种发现方法进行的 Active Directory 轮询可能会产生大量的网络流量。 请考虑将每种发现方法安排为在此网络流量不会对企业的网络使用造成负面影响时运行。  


### <a name="bkmk_config-adgd"></a> 配置 Active Directory 组发现  

1. 在“Active Directory 组属性”窗口的“常规”  选项卡上，选择“添加”  以配置发现作用域。 选择“组”  或“位置”  。 然后在“添加组”  或“添加 Active Directory 位置”  对话框中完成以下配置：  

    1.  为此发现作用域指定“名称”  。  

    2.  指定要搜索的“Active Directory 域”  或“位置”  ：  

        - 如果选择了“组”  ，请指定要发现的一个或多个 Active Directory 组。  

        - 如果选择了“位置”  ，请指定 Active Directory 容器作为要发现的位置。 你也可以为此位置启用对 Active Directory 子容器的递归搜索。  

    3.  指定站点用于搜索此发现作用域的“Active Directory 组发现帐户”  。 有关详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#active-directory-group-discovery-account)。  

    4.  选择“确定”  保存发现作用域配置。  

2.  为要定义的每个其他发现作用域重复以上步骤。  

3.  在“轮询计划”  选项卡上，配置完整发现轮询计划和增量发现。  

4.  在“选项”  选项卡上，可以配置这些设置，以从发现中筛选出或排除过期的计算机记录。 同时配置对分发组成员身份的发现。  

    > [!NOTE]  
    > 默认情况下，Active Directory 组发现只会发现安全组的成员身份。  

5. 选择“确定”  保存配置。  


### <a name="bkmk_config-adsd"></a> 配置 Active Directory 系统发现  

1. 在“Active Directory 系统发现属性”窗口的“常规”  选项卡中，选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)，以指定新的 Active Directory 容器。 在“Active Directory 容器”  对话框框中，完成以下配置：  

    1.  键入或浏览到“路径”  位置。 此值是容器或组织单位 (OU) 的有效 LDAP 路径。 在站点查询此资源路径。 例如 `LDAP://CN=Computers,DC=contoso,DC=com`  

    2.  指定更改搜索行为的选项：  

        - **发现 Active Directory 组内的对象**：该站点还会查看此路径中的组的成员资格。  

        - **以递归方式搜索 Active Directory 子容器：** ：如果启用此选项，该站点将搜索以上路径中的任何其他容器或 OU。 如果禁用此选项，该站点仅搜索特定路径中的资源。  

          从版本 1806 开始，请选择要从此递归搜索中排除的子容器。 此选项有助于减少发现的对象数。 选择“添加”  选择以上路径下的容器。 在“选择新容器”对话框中，选择要排除的子容器。 选择“确定”  ，以关闭“选择新容器”对话框。<!--1358143-->

          > [!Tip]  
          > “Active Directory 系统发现属性”窗口中的 Active Directory 容器列表包含列“已排除”  。 当选择要排除的容器，此值为“是”  。  

    3.  对于每个位置，指定要用作“Active Directory 发现帐户”  的帐户。 有关详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#active-directory-system-discovery-account)。  

        > [!TIP]  
        > 对于指定的每个位置，可以配置一组发现选项和唯一的 Active Directory 发现帐户。  

    4.  选择“确定”  保存 Active Directory 容器配置。  

2.  在“轮询计划”  选项卡上，配置完整发现轮询计划和增量发现。  

3.  在“Active Directory 属性”  选项卡上，为要发现的计算机配置其他 Active Directory 属性。 此选项卡会列出默认对象属性。  

     > [!Tip]  
     > 例如，你的组织在 Active Directory 中的计算机帐户上使用 Description 属性  。 选择“自定义”  ，然后将 `Description` 添加为自定义属性。 在此发现方法运行后，这一属性显示在 Configuration Manager 控制台的设备“属性”选项卡上。<!--513948-->  

4.  在“选项”  选项卡上，可以配置这些设置，以从发现中筛选出或排除过期的计算机记录。  

5. 选择“确定”  保存配置。  


### <a name="bkmk_config-adud"></a> 配置 Active Directory 用户发现  

1.  在“Active Directory 用户发现属性”窗口的“常规”  选项卡中，选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)以指定新的 Active Directory 容器。 在“Active Directory 容器”  对话框框中，完成以下配置：  

    1.  指定要搜索的一个或多个位置。  

    2.  对于每个位置，指定更改搜索行为的选项。  

    3.  对于每个位置，指定要用作“Active Directory 发现帐户”  的帐户。 有关详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#active-directory-user-discovery-account)。  

        > [!NOTE]  
        > 对于指定的每个位置，可以配置一组唯一的发现选项和唯一的 Active Directory 发现帐户。  

    4.  选择“确定”  保存 Active Directory 容器配置。  

6.  在“轮询计划”  选项卡上，配置完整发现轮询计划和增量发现。  

7.  在“Active Directory 属性”  选项卡上，为要发现的计算机配置其他 Active Directory 属性。 此选项卡会列出默认对象属性。  

8.  选择“确定”  保存配置。  



## <a name="azureaadisc"></a>配置 Azure AD 用户发现

Azure AD 用户发现未启用，或与其他发现方法的配置相同。 在将 Configuration Manager 站点载入到 Azure AD 时对其进行配置。 为实现云管理而  [配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)时，也可启用和配置此发现方法。 

在配置云管理 Azure 服务  时： 
- 在向导的“发现”  页上，选择“启用 Azure Active Directory 用户发现”  选项。 
- 选择“设置”  。 
- 在“Azure AD 用户发现设置”对话框中，配置出现发现的时间计划。 此外，还可以启用增量发现，仅用于查看 Azure AD 中新增或更改的帐户。 

有关详细信息，请参阅 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)。

> [!Important]  
> 将 Azure AD 应用导入 Configuration Manager 之前，需授予用于从 Azure AD 读取目录数据的服务器应用程序权限  。 
> - 在 [Azure 门户](https://portal.azure.com)中转至 Azure Active Directory 边栏选项卡  。 
> - 选择“应用注册”  并在需要的时候切换为“所有应用”  。 
> - 选择类型为“Web 应用/API”  的服务器应用，然后选择“设置”  。 
> - 选择“所需权限”  ，然后选择“授予权限”  。
>  
> 如果服务器应用是从 Configuration Manager 中创建的  ，Azure AD 会自动创建该应用程序的权限。 仍需在 Azure 门户中向应用程序授予许可。

> [!Note]  
> 如果用户是联合标识或同步标识，则必须使用 Configuration Manager [Active Directory 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)和 Azure AD 用户发现。 若要详细了解混合标识，请参阅[定义混合标识采用策略](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)。<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a>配置检测信号发现  

安装主站点时，Configuration Manager 会启用检测信号发现方法。 如果想要使用每隔七天的默认计划，则没有其他要配置的内容。 否则，你只需要配置有关客户端将检测信号发现数据记录发送到管理点的频率的计划。  

> [!NOTE]  
> 如果在同一站点上同时启用了“清除安装标志”  客户端请求安装和站点维护任务，请将检测信号发现的计划设置为小于“清除安装标志”  站点维护任务的“客户端重新发现期间”  。 有关站点维护任务的详细信息，请参阅[维护任务](/sccm/core/servers/manage/maintenance-tasks)。  


### <a name="configure-the-heartbeat-discovery-schedule"></a>配置检测信号发现计划  

1.  在 Configuration Manager 控制台中的“管理”  工作区中，展开“层次结构配置”  ，然后选择“发现方法”  节点。  

2.  为要在其中配置检测信号发现的站点选择“检测信号发现”  方法。  

3.  在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4.  配置客户端提交检测信号发现数据记录的频率。 然后选择“确定”  保存配置。  



<a name="BKMK_AboutConfigNetworkDisc"></a>

##  <a name="BKMK_ConfigNetworkDisc"></a>配置网络发现  

 在配置网络发现之前，先了解下列主题：  

- 网络发现的可用级别  

- 可用的网络发现选项  

- 在网络上限制网络发现  

有关详细信息，请参阅[关于网络发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutNetwork)。  

下列部分提供有关网络发现的常见配置的信息。 你可以配置其中一个或多个配置以在同一发现轮次中使用。 如果使用多个配置，则规划可能影响发现结果的交互。  

例如，你会发现使用特定 SNMP 共同体名称的所有简单网络管理协议 (SNMP) 设备。 对于同一发现轮次，可以禁用针对特定子网的发现。 当发现运行时，网络发现不会发现已禁用的子网上具有指定共同体名称的 SNMP 设备。  


###  <a name="BKMK_DetermineNetTopology"></a>确定网络拓扑  

你可以使用仅拓扑发现来映射你的网络。 这种类型的发现不会发现潜在客户端。 仅拓扑网络发现依赖于 SNMP。  

映射网络拓扑时，在“网络发现属性”  对话框中的“SNMP”  选项卡上配置“最大跃点数”  。 只需几个跃点，便可以帮助控制运行发现时使用的网络带宽。 在发现网络的更多内容时，增加跃点数可更好地了解网络拓扑。  

了解网络拓扑后，配置网络发现的其他属性。 这些属性有助于发现潜在客户端及其操作系统。 此外，配置网络发现以限制它可以搜索的网段。  

有关详细信息，请参阅[如何确定网络拓扑](#bkmk_proc-top)


### <a name="network-discovery-search-options"></a>网络发现搜索选项

Configuration Manager 支持以下搜索网络的方法：
- [使用子网限制搜索](#BKMK_LimitBySubnet)
- [搜索特定域](#BKMK_SearchByDomain)
- [使用 SNMP 共同体名称限制搜索](#BKMK_LimitBySNMPname)
- [搜索特定的 DHCP 服务器](#BKMK_SearchByDHCP)

####  <a name="BKMK_LimitBySubnet"></a>使用子网限制搜索  

可以将网络发现配置为在发现运行期间搜索特定子网。 默认情况下，网络发现会搜索运行发现的服务器的子网。 配置和启用的任何其他子网仅适用于 SNMP 和 DHCP 搜索选项。 当网络发现搜索域时，子网配置未对其进行限制。  

如果你在“网络发现属性”  对话框中的“子网”  选项卡上指定一个或多个子网，则仅搜索标记为“已启用”  的子网。  

禁用子网后，站点会从发现中排除此子网，并适用下列条件：  

- 不在子网上运行基于 SNMP 的查询。  

- DHCP 服务器不回复位于子网上的资源列表。  

- 基于域的查询可以发现位于子网上的资源。  


####  <a name="BKMK_SearchByDomain"></a>搜索特定域  

可以将网络发现配置为在发现运行期间搜索特定域或一组域。 默认情况下，网络发现会搜索运行发现的服务器的本地域。  

如果你在“网络发现属性”  对话框中的“域”  选项卡上指定一个或多个域，则仅搜索标记为“已启用”  的域。  

禁用域后，站点会从发现中排除此域，并适用下列条件：  

- 网络发现不查询该域中的域控制器。  

- 基于 SNMP 的查询仍然可以在域中的子网上运行。  

- DHCP 服务器仍然能够以位于域中的资源的列表形式予以回复。  


#### <a name="BKMK_LimitBySNMPname"></a>使用 SNMP 共同体名称限制搜索  

可以将网络发现配置为在发现运行期间搜索特定 SNMP 共同体或一组共同体。 默认情况下，该方法将配置公共  共同体名称。  

网络发现使用共同体名称来获得对路由器（SNMP 设备）的访问权。 路由器可以向网络发现提供有关链接到第一个路由器的其他路由器和子网的信息。  

> [!NOTE]  
> SNMP 共同体名称类似于密码。 网络发现只能从已指定共同体名称的 SNMP 设备中获得信息。 每个 SNMP 设备均可以拥有自己的共同体名称，但是同一个共同体名称通常会由几个设备共享。 此外，大多数 SNMP 设备都有默认的“公共”  共同体名称。 但某些组织会删除其设备的“公共”  共同体名称以作为安全措施。  

如果“网络发现属性”  对话框中的“SNMP”  选项卡上包含多个 SNMP 共同体，则会按照共同体的显示顺序搜索共同体。 请确保使用频率最高的名称位于列表顶部。 此配置有助于最小化站点在尝试使用不同名称联系设备时产生的网络流量。

> [!NOTE]  
> 除了使用 SNMP 共同体名称之外，还可以指定特定 SNMP 设备的 IP 地址或可解析名称。 可使用“网络发现属性”  对话框的“SNMP 设备”  选项卡来执行此操作。  


####  <a name="BKMK_SearchByDHCP"></a>搜索特定的 DHCP 服务器  

可以将网络发现配置为使用特定 DHCP 服务器或多个服务器在发现运行期间发现 DHCP 客户端。  

网络发现搜索你在“网络发现属性”  对话框中的“DHCP”  选项卡上指定的每个 DHCP 服务器。 如果正在运行发现的服务器从 DHCP 服务器租赁其 IP 地址，可以配置发现来搜索该 DHCP 服务器。 使用选项“包括配置站点服务器使用的 DHCP 服务器”  来启用此行为。  

> [!NOTE]  
> 为了在网络发现中成功配置 DHCP 服务器，你的环境必须支持 IPv4。 你无法将网络发现配置为使用本机 IPv6 环境中的 DHCP 服务器。  


###  <a name="BKMK_HowToConfigNetDisc"></a>如何配置网络发现  

使用以下过程首先仅发现网络拓扑，然后使用一个或多个可用的网络发现选项将网络发现配置为发现潜在客户端。  

#### <a name="bkmk_proc-top"></a> 如何确定网络拓扑  

1.  在 Configuration Manager 控制台中的“管理”  工作区中，展开“层次结构配置”  ，然后选择“发现方法”  节点。  

2.  为要在其中发现网络资源的站点选择“网络发现”  方法。  

3.  在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

    - 在“常规”  选项卡上，选择“启用网络发现”  选项。 然后从“发现类型”  选项中选择“拓扑”  。  

    - 在“子网”  选项卡上，选择“搜索本地子网”  选项。  

      > [!TIP]  
      > 如果你知道构成网络的特定子网，请取消选中“搜索本地子网”  复选框。 然后选择“新建”图标  ![新建图标](media/Disc_new_Icon.gif)，并添加想要搜索的特定子网。 对于大型网络，一次仅搜索一两个子网，从而最大程度地降低网络带宽使用量。  

    - 在“域”  选项卡上，选择“搜索本地域”  选项。  

    - 在“SNMP”  选项卡上，从“最大跃点数”  下拉列表选择一个选项。 此选项指定在映射拓扑时可以使用的网络发现路由器跃点数。  

      > [!TIP]  
      > 首次映射网络拓扑时，请仅配置少量路由器跃点以最大程度降低网络带宽使用量。  

4.  在“计划”  选项卡上，选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)，并设置用于运行发现的计划。  

    > [!NOTE]  
    > 你无法将不同的发现配置分配给单独的网络发现计划。 每次运行网络发现时，它都使用当前发现配置。  

5.  选择“确定”  以接受配置。 网络发现将按计划的时间运行。  


#### <a name="bkmk_proc-config"></a>如何配置网络发现  

1.  在 Configuration Manager 控制台中的“管理”  工作区中，展开“层次结构配置”  ，然后选择“发现方法”  节点。  

2.  为要在其中发现网络资源的站点选择“网络发现”  方法。  

3.  在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

4.  在“常规”  选项卡上，选择“启用网络发现”  选项。  

    - 从“发现类型”  选项选择要运行的发现类型。  

    - 启用 Configuration Manager 的“慢速网络”  选项，对低带宽网络进行自动调整。  

5.  若要配置发现以搜索子网，切换到“子网”  选项卡。然后配置下列一个或多个选项：  

    - 若要在运行发现的计算机的本地子网上运行发现，请启用“搜索本地子网”  选项。  

    - 若要搜索特定子网，请确保该子网在“要搜索的子网”  中列出，并且其“搜索”  值必须为“已启用”  ：  

      1.  如果未列出子网，请选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)。 在“新建子网分配”  对话框中，输入“子网”  和“掩码”  信息，然后选择“确定”  。 默认情况下，为搜索启用了新子网。  

      2.  若要更改所列子网的搜索  值，请在列表中选择它。 然后选择“切换”  图标，在“禁用”  和“启用”  之间切换值。  

6.  若要配置发现以搜索域，切换到“域”  选项卡。然后配置下列一个或多个选项：  

    - 若要在运行发现的计算机的域上运行发现，请启用“搜索本地域”  选项。  

    - 若要搜索特定域，请确保该域在“域”  中列出，并且其“搜索”  值必须为“已启用”  ：  

      1.  如果未列出域，请选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)。 在“域属性”  对话框中，输入域  信息，然后选择“确定”  。 默认情况下，为搜索启用了新域。  

      2.  若要更改所列域的搜索  值，请在列表中选择它。 然后选择“切换”  图标，在“禁用”  和“启用”  之间切换值。  

7.  若要将发现配置为搜索 SNMP 设备的特定 SNMP 共同体名称，切换到“SNMP”  选项卡。然后配置下列一个或多个选项：  

    - 要将 SNMP 共同体名称添加到“SNMP 共同体名称”  列表中，选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)。 在“新建 SNMP 共同体名称”  对话框中，指定 SNMP 共同体的**名称**，然后选择“确定”  。  

    - 若要删除 SNMP 共同体名称，请选择共同体名称，然后选择“删除”  图标![删除图标](media/Disc_delete_Icon.gif)。  

    - 若要调整 SNMP 共同体名称的搜索顺序，请从列表中选择共同体名称。 然后选择“向上移动项目”  图标![上移图标](media/Disc_moveUp_Icon.gif)或**向下移动项目**图标![下移图标](media/Disc_moveDown_Icon.gif)。 当运行发现时，会按照从上向下的顺序搜索共同体名称。 

    - 若要配置供 SNMP 搜索使用的最大路由器跃点数，从“最大跃点数”  下拉列表中选择跃点数。  

8. 若要配置 SNMP 设备，切换到“SNMP 设备”  选项卡。如果未列出设备，请选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)。 在“新建 SNMP 设备”  对话框中，指定 SNMP 设备的 IP 地址或设备名称，然后选择“确定”  。  

    > [!NOTE]  
    > 如果指定设备名称，则 Configuration Manager 必须能够将 NetBIOS 名称解析为 IP 地址。  

9. 若要配置发现以查询特定 DHCP 服务器，切换到“DHCP”  选项卡。然后配置下列一个或多个选项：  

    - 若要在运行发现的计算机上查询 DHCP 服务器，请启用“始终使用站点服务器的 DHCP 服务器”  选项。  

      > [!NOTE]  
      > 为了使用此选项，服务器必须从 DHCP 服务器租用其 IP 地址，并且不能使用静态 IP 地址。  

    - 要查询特定的 DHCP 服务器，选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)。 在“新建 DHCP 服务器”  对话框中指定 DHCP 服务器的 IP 地址或服务器名称，然后选择“确定”  。  

      > [!NOTE]  
      > 如果指定服务器名称，则 Configuration Manager 必须能够将 NetBIOS 名称解析为 IP 地址。  

10. 若要在发现运行时进行配置，切换到“计划”  选项卡。然后选择“新建”  图标![新建图标](media/Disc_new_Icon.gif)以设置用于运行网络发现的计划。 可以配置多个重复计划以及多个无重复计划。  

    > [!NOTE]  
    > 如果“计划”  选项卡同时显示多个计划，则所有计划均会根据在配置时该计划中指示的时间运行网络发现。 定期计划的行为也是如此。  

11. 选择“确定”  保存配置。  


###  <a name="BKMK_HowToVerifyNetDisc"></a>如何验证网络发现是否已完成  

 完成网络发现所需的时间可能因下列一个或多个因素而异：  

- 你的网络规模  

- 你的网络拓扑  

- 为在网络中查找路由器而配置的最大跃点数  

- 正在运行的发现的类型  

网络发现不会创建消息在完成时通知你。 使用以下过程验证发现何时完成：  

1.  在 Configuration Manager 控制台中，转到“监视”  工作区。 展开“系统状态”  ，然后选择“状态消息查询”  节点。  

2.  选择“所有状态消息”  查询。  

3.  在功能区“主页”  选项卡上的“状态消息查询”  组中，选择“显示消息”  。  

4.  在“所有状态消息”窗口中，从“选择日期和时间”  下拉列表选择一个值，说明多久之前启动发现。 然后选择“确定”  以打开“Configuration Manager 状态消息查看器”  。  

    > [!TIP]  
    > 你也可以使用“指定日期和时间”  选项选择运行发现的指定日期和时间。 当你在指定日期运行网络发现并且想要仅检索该日期中的消息时，此选项很有用。  

5.  要验证网络发现是否已经完成，请搜索具有以下详细信息的状态消息：  

    - 消息 ID：**502**  

    - 组件：**SMS_NETWORK_DISCOVERY**  

    - 描述:**此组件已停止**  

    如果不存在此状态消息，则网络发现尚未完成。  

7.  要验证网络发现的启动时间，请搜索具有以下详细信息的状态消息：  

    - 消息 ID：**500**  

    - 组件：**SMS_NETWORK_DISCOVERY**  

    - 描述:**此组件已启动**  

    此信息验证是否已启动网络发现。 如果没有此信息，请重新计划网络发现。  
