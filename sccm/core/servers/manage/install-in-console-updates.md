---
title: 控制台中更新
titleSuffix: Configuration Manager
description: 从 Microsoft 云安装 Configuration Manager 更新
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c1d83f6dc0de701176bbf6eeec8936afa081829
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420679"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>为 Configuration Manager 安装控制台内更新

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 与 Microsoft 云服务同步，以获取更新。 随后从 Configuration Manager 控制台安装这些更新。



## <a name="get-available-updates"></a>获取可用更新

该站点仅下载适用于你的基础结构和版本的更新。 此同步可以自动或手动进行，具体取决于为层次结构配置服务连接点的方式：

-   在 **联机模式**下，服务连接点会自动连接到 Microsoft 云服务并下载适用的更新。  

     默认情况下，Configuration Manager 会每 24 小时检查一次新的更新。 请手动检查 Configuration Manager 控制台中的更新。 转到“管理”工作区，选择“更新和维护服务”节点，然后单击功能区中的“检查更新”。  

-   在“脱机模式”下，服务连接点不会连接到 Microsoft 云服务。 要下载并导入可用更新，请[使用服务连接工具](/sccm/core/servers/manage/use-the-service-connection-tool)。  

> [!NOTE]  
> 必要时，可将带外修复程序导入到控制台。 为此，请使用[更新注册工具](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)。 这些带外修复程序对你在与 Microsoft 云服务同步时获取的更新进行了补充。  


更新同步后，可以在 Configuration Manager 控制台中查看它们。 转到“管理”工作区，选择“更新和维护服务”节点。  

-   未安装的更新显示为“可用”。  

-   已安装的更新显示为“已安装”。 仅显示最近安装的更新。 在功能区上单击“历史记录”按钮，以查看以前安装的更新。  


配置服务连接点之前，需了解和规划它的其他使用情况。 以下使用情况会影响你配置此站点系统角色的方式：  

-   该站点使用服务连接点上载有关你的站点的使用情况信息。 此信息可帮助 Microsoft 云服务标识你基础结构的当前版本可用的更新。 有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。  

-   该站点使用服务连接点通过 Microsoft Intune 和 Configuration Manager 本地移动设备管理来管理设备。 有关详细信息，请参阅[混合移动设备管理 (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management)。  

若要更好地了解下载更新时会发生什么状况，请参阅以下流程图：  

-   [流程图 - 下载更新](/sccm/core/servers/manage/download-updates-flowchart)  

-   [流程图 - 更新复制](/sccm/core/servers/manage/update-replication-flowchart)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>分配查看和管理更新和功能的权限

若要在控制台中查看更新，用户必须具有基于角色且包含“更新包”安全类的管理安全角色。 此类授予访问权限以在 Configuration Manager 控制台中查看和管理更新。    


#### <a name="about-the-update-packages-class"></a>关于更新程序包类   
默认情况下，更新程序包类 (SMS_CM_Updatepackages) 是以下具有列出权限的内置安全角色的一部分：  

-  具有**修改**和**读取**权限的**完全权限管理员**：  

    -   具有此安全角色并具有对所有安全域访问权限的用户可以查看和安装更新。 该用户还可以在安装过程中启用功能，在站点更新后启用各个功能。  

    - 具有此安全角色并具有对默认安全域访问权限的用户可以查看和安装更新。 该用户还可以在安装过程中启用功能，在站点更新后查看功能。 但是，在站点更新后，此用户无法启用功能。  

- 具有**读取**权限的**只读分析员**：  

  -  具有此安全角色并具有对**默认**作用域访问权限的用户可以查看更新，但不能安装更新。 此用户还可以在站点更新后查看功能，但不能启用功能。  


#### <a name="permissions-required-for-updates-and-servicing"></a>更新和维护服务所需的权限   
- 使用分配有安全角色（包括具有**修改**和**读取**权限的**更新包**类）的帐户。  

- 为该帐户分配**默认**作用域。  

#### <a name="permissions-to-only-view-updates"></a>仅查看更新的权限   
- 使用分配有安全角色（包括仅具有**读取**权限的**更新包**类）的帐户。  

- 为该帐户分配**默认**作用域。  

#### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>在站点更新后启用功能所需的权限   
-  使用分配有安全角色（包括具有**修改**和**读取**权限的**更新包**类）的帐户。  

-  为该帐户分配**全部**作用域。  



##  <a name="bkmk_beforeinstall"></a>安装控制台内部更新之前  

在从 Configuration Manager 控制台中安装更新之前，请查看以下步骤。  


###  <a name="bkmk_step1"></a>步骤 1：查看更新清单  

若要了解开始更新前执行的操作，请查看适用的更新清单：

- [用于安装更新 1810 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1810)  

- [用于安装更新 1806 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1806)  

- [用于安装更新 1802 的清单](/sccm/core/servers/manage/checklist-for-installing-update-1802)


###  <a name="bkmk_step2"></a>步骤 2：安装更新之前运行先决条件检查程序  

安装更新之前，请考虑运行针对该更新的先决条件检查。 如果在安装更新之前运行先决条件检查：  

-   站点会在安装更新之前将更新文件复制到其他站点。  

-   选择安装更新时，先决条件检查会再次自动运行。  

> [!NOTE]   
> 启动先决条件检查，然后查看状态时，**安装**阶段似乎处于活动状态。 但站点实际上并未安装更新。 为了运行先决条件检查，更新过程从内容库中提取包。 然后，它将包放入一个暂存文件夹中，它可以在该文件夹中访问当前的先决条件检查。 这与安装更新时运行的过程相同。 此行为就是安装阶段显示为“正在进行”的原因。 “安装”类别中仅显示“提取更新程序包”步骤。  

以后在安装更新时，可以配置更新以忽略先决条件检查警告。  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>安装更新之前运行先决条件检查程序  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，并选择“更新和维护服务”节点。   

2.  选择要对其运行先决条件检查的更新包。  

3.  单击功能区中的“运行先决条件检查”。  

     运行先决条件检查时，更新的内容会复制到子站点。 查看站点服务器上的 **distmgr.log** 以确认该内容复制成功。  

4.  若要查看先决条件检查的结果，请执行以下操作：  

    1. 在 Configuration Manager 控制台中，转到“监视”工作区。  

    2. 选择“更新和维护服务状态”节点，然后查找先决条件状态。  

    3. 有关详细信息，请参阅站点服务器上的 **ConfigMgrPrereq.log**。  



##  <a name="bkmk_install"></a>安装控制台内部更新  

准备好从 Configuration Manager 控制台安装更新后，请从层次结构的顶层站点开始。 此站点是管理中心站点或独立主站点。  

在正常营业时间之外为每个站点安装更新，以尽量减少对业务运营的影响。 更新安装可能包括重新安装站点组件和站点系统角色之类的操作。  

-   管理中心站点完成更新安装之后，子主站点会自动启动更新。 这是建议的默认流程。 若要控制主站点安装更新的时间，请使用[站点服务器的服务时段](/sccm/core/servers/manage/service-windows)。  

-   在主父站点更新完成后，从 Configuration Manager 控制台手动更新辅助站点。 不支持辅助站点服务器的自动更新。  

-   在站点更新之后使用 Configuration Manager 控制台时，系统会提示你更新控制台。  

-  站点服务器成功完成安装更新后，它将自动更新所有合适的站点系统角色。 但是，所有分发点都不会重新安装，它们将处于脱机状态以便同时更新。 而站点服务器使用站点的内容分发设置，一次性将更新分发到分发点的子集。 结果只有某些分发点脱机以安装更新。 尚未开始更新或已完成更新的分发点保持联机状态，并能够向客户端提供内容。


###  <a name="bkmk_overview"></a>控制台内部更新安装的概述  

#### <a name="1-when-the-update-installation-starts"></a>1.更新安装启动时  
你会看到更新向导，该向导显示更新适用的产品区域的列表。  

- 在该向导的“常规”页面中，根据需要配置“先决条件警告”：  

  - 先决条件错误会始终停止更新安装。 请先解决错误，然后才能成功地重试更新安装。 有关详细信息，请参阅[重试失败更新的安装](#bkmk_retry)。  

  - 先决条件警告也可以停止更新安装。 重试更新安装之前，请先解决警告问题。 有关详细信息，请参阅[重试失败更新的安装](#bkmk_retry)。  

  - **无论是否缺少要求，都将忽略任何先决条件检查警告并安装此更新**：设置更新安装的条件以忽略先决条件警告。 此选项允许更新安装以继续操作。 如果不选择此选项，则在更新安装遇到警告时会停止该过程。 除非以前为站点运行了先决条件检查并解决了先决条件警告，否则不要使用此选项。  

    在“管理”和“监视”这两个工作区中，“更新和维护服务”节点都在功能区上包含了一个名为“忽略先决条件警告”的按钮。 当因先决条件检查警告而导致无法完成更新包安装时，可以使用此按钮。 例如，安装更新而不使用忽略先决条件警告选项（从更新向导中）。 更新安装停止，出现先决条件警告的状态，但没有发生错误。 稍后单击功能区中的“忽略先决条件警告”。 此操作会触发自动继续安装该更新而忽略先决条件警告。 使用此选项时，几分钟后将自动继续更新安装。  


- 当 Configuration Manager 客户端有适用的更新时，请选择使用一组有限的客户端来测试该客户端更新。 有关详细信息，请参阅[如何在预生产集合中测试客户端升级](/sccm/core/clients/manage/upgrade/test-client-upgrades)。  


#### <a name="2-during-the-update-installation"></a>2.更新安装过程中  
在更新安装过程中，Configuration Manager 会执行以下操作：  

-   重新安装任何受影响的组件，如站点系统角色或 Configuration Manager 控制台。  

-   基于针对客户端试验以及针对[自动客户端升级](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade)进行的选择来管理客户端的更新。  

-   站点系统服务器通常不需要在更新过程中重启。 如果某个角色使用 .NET，并且更新包更新该必备组件，则站点系统可能会重启。  

> [!TIP]  
>  安装 Configuration Manager 更新时，站点还会更新 CD.Latest 文件夹。 有关详细信息，请参阅 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)。  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3.在更新安装时监视更新进度  
按以下步骤监视进度：  

-   在 Configuration Manager 控制台中，转到“管理”工作区，并选择“更新和维护服务”节点。 此节点显示所有更新包的安装状态。  

-   在 Configuration Manager 控制台中，转到“监视”工作区，并选择“更新与维护服务状态”节点。 此节点仅显示站点正在安装的当前更新包的安装状态。  

    为便于监视，更新安装划分为多个阶段。 对于以下每个阶段，安装状态中的其他详细信息都说明了要查看哪个日志文件来了解详细信息：  

    -   **下载**：此阶段仅适用于具有服务连接点的顶层站点。   

    -   **复制**   

    -   **先决条件检查**   

    -   **安装**    

    -   **安装后**：有关详细信息，请参阅[安装后任务](#post-installation-tasks)。  

-   查看站点服务器上 `<ConfigMgr_Installation_Directory>\Logs` 中的 **CMUpdate.log** 文件。  


#### <a name="4-when-the-update-installation-completes"></a>4.更新安装完成时  
第一个站点更新完成安装之后：  

-   子主站点会自动安装更新。 不需要采取任何进一步措施。  

-   从 Configuration Manager 控制台手动更新辅助站点。 有关详细信息，请参阅[在辅助站点上启动更新安装](#bkmk_secondary)。  

-   在层次结构中的所有站点均更新为新版本之前，你的层次结构会在混合版本模式下运行。 有关详细信息，请参阅[不同版本之间的互操作性](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions)。  


#### <a name="5-update-configuration-manager-consoles"></a>5.更新 Configuration Manager 控制台  
在管理中心站点或主站点更新之后，还必须更新连接到该站点的每个 Configuration Manager 控制台。 系统会在以下情况下提示你更新控制台：  

-   打开控制台时  

-   在打开的控制台中转至新节点时  

在站点更新后立即更新控制台。  

在控制台更新完成之后，验证控制台和站点版本是否正确。 转至控制台左上角的“关于 System Center Configuration Manager”。  

 > [!Note]  
 > 从 1802 版开始，控制台版本现在与站点版本略有不同。 控制台的次要版本现在对应于 Configuration Manager 发行版。 例如，在 Configuration Manager 1802 版中，初始站点版本为 5.0.8634.1000，初始控制台版本为 5.**1802**.1082.1700。 内部版本号 (1082) 和修订版本号 (1700) 可能会随 1802 发行版的未来修补程序而变化。



###  <a name="bkmk_toptier"></a> 在顶层站点上启动更新安装  

在层次结构的顶层站点上的 Configuration Manager 控制台中，转到“管理”工作区，并选择“更新和维护服务”节点。 选择状态为“可用”的更新，然后单击功能区中的“安装更新包”。  


###  <a name="bkmk_secondary"></a> 在辅助站点上启动更新安装  

更新辅助站点的父主站点之后，从 Configuration Manager 控制台中更新辅助站点。 为此，请使用“升级辅助站点向导”。  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择要更新的辅助站点，然后单击功能区中的“升级”。  

2.  单击“是”以启动辅助站点的更新。  

若要监视某个辅助站点上的更新安装，请选择该辅助站点，然后单击功能区中的“显示安装状态”。 同时将“版本”列添加到“站点”节点中，以便查看每个辅助站点的版本。  

在某些情况下，控制台中的状态不会刷新或显示更新失败。 成功更新辅助站点后，使用“重新尝试安装”选项。 对于成功安装更新的辅助站点，此选项不会重新安装更新，但会强制控制台更新状态。


### <a name="post-installation-tasks"></a>安装后任务

当站点安装更新时，有几个任务要等站点服务器上的更新安装完成后才能启动。 此列表包含对站点和层次结构操作而言非常关键的安装后任务。 因为它们很关键，所以系统会主动监视。 不直接监视的其他任务包括重新安装站点系统角色。 若要查看关键的安装后任务的状态，请在监视站点更新安装时选择“安装后”任务。

并非所有任务都会立即完成。 每个站点完成更新安装之前，某些任务不会启动。 这些任务完成之前，新功能可能会被延迟。 由于在所有站点都完成更新安装之前不会开始启用新功能，因此新功能可能在一段时间内不显示。

安装后任务包括：

- 安装 SMS_EXECUTIVE 服务
  -   在站点服务器上运行的关键服务。
  -   重新安装此服务应快速完成。


- 安装 SMS_DATABASE_NOTIFICATION_MONITOR 组件
  -   SMS_EXECUTIVE 服务的关键站点组件线程。
  -   重新安装此服务应快速完成。


- 安装 SMS_HIERARCHY_MANAGER 组件
  -   在站点服务器上运行的关键站点组件。
  -   负责在站点系统服务器上重新安装角色。 不显示单个站点系统角色的重新安装状态。
  -   重新安装此服务应快速完成。


- 安装 SMS_REPLICATION_CONFIGURATION_MONITOR 组件
  -   在站点服务器上运行的关键站点组件。
  -   重新安装此服务应快速完成。


- 安装 SMS_POLICY_PROVIDER 组件
  -   仅在主站点上运行的关键站点组件。
  -   重新安装此服务应快速完成。


- 监视复制初始化   
  -   此任务仅显示在管理中心站点和子主站点中。
  -   取决于 SMS_REPLICATION_CONFIGURATION_MONITOR。
  -   应快速完成。


- 更新 Configuration Manager 客户端预生产包    
  -   即使客户端预生产（也称为客户端试验）未启用以供使用，此任务也会显示。
  -   层次结构中的所有站点都完成安装更新之前不会启动。


- 更新站点服务器上的客户端文件夹
  -   如果在预生产环境中使用客户端，则不显示此任务。  
  -   应快速完成。


- 更新 Configuration Manager 客户端包
  -   如果在预生产环境中使用客户端，则不显示此任务。  
  -   只有在所有站点都安装更新后才完成。  


- 打开功能
  -   此任务仅显示在层次结构的顶层站点中。
  -   层次结构中的所有站点都完成安装更新之前不会启动。
  -   不显示各项功能。



##  <a name="bkmk_retry"></a>重试失败更新的安装  

更新安装失败时，查看控制台内部反馈以确定针对警告和错误的解决方法。 有关更多详细信息，请查看站点服务器上的 **ConfigMgrPrereq.log**。 重试更新安装之前，必须解决错误，并且应解决警告。  

> [!TIP]  
> 如果更新存在下载或复制问题，请使用[更新重置工具](/sccm/core/servers/manage/update-reset-tool)。  

准备好重试安装更新后，选择失败的更新，然后选择适用的选项。 更新安装重试行为取决于开始重试的节点以及使用的重试选项。  

#### <a name="retry-installation-for-the-hierarchy"></a>为层次结构重试安装
当某个更新处于以下状态之一时，为整个层次结构重试安装该更新：  

  -   先决条件检查已通过但存在一个或多个警告，并且未在更新向导中设置用于忽略先决条件检查警告的选项。 （“更新和维护服务”节点中“忽略先决条件警告”的更新值为“否”。）   

  -   先决条件失败    

  -   安装失败  

  -   内容复制到站点失败   

转到“管理”工作区，选择“更新和维护服务”节点。 选择更新，然后选择下列选项之一：  

  -   **重试**：从“更新和维护服务”重试时，将再次开始更新安装，并自动忽略先决条件警告。 如果之前复制内容失败，则会重新复制更新的内容。  

  - **忽略先决条件警告**：如果由于警告而导致更新安装停止，则可以选择“忽略先决条件警告”。 此操作允许在几分钟后继续安装更新，并使用用于忽略先决条件警告的选项。   

#### <a name="retry-installation-for-the-site"></a>为站点重试安装  
当某个更新处于以下状态之一时，在特定站点上重试安装该更新：  

  -   先决条件检查已通过但存在一个或多个警告，并且未在更新向导中设置用于忽略先决条件检查警告的选项。 （“更新和维护服务”节点中“忽略先决条件警告”的更新值为“否”。）  

  -   先决条件失败    

  -   安装失败    

转到“监视”工作区，选择“站点维护服务状态”节点。 选择更新，然后单击下列选项之一：  

  - **重试**：从“站点维护服务状态”重试时，仅在此站点重启更新安装。 与从“更新和维护服务”节点运行**重试**不同，此重试不会忽略先决条件警告。  

  - **忽略先决条件警告**：如果由于警告而导致更新安装停止，则可以单击“忽略先决条件警告”。 此操作允许在几分钟后继续安装更新，并使用用于忽略先决条件警告的选项。  



##  <a name="bkmk_after"></a> 站点安装更新之后  

站点更新后，查看更新后清单以寻找适用的版本：  

- [版本 1810 的更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist)  

- [版本 1806 的更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist)  

- [版本 1802 的更新后清单](/sccm/core/servers/manage/checklist-for-installing-update-1802#post-update-checklist)  



##  <a name="bkmk_options"></a>启用更新中的可选功能  

当更新包含一个或多个可选功能时，可以选择在层次结构中启用这些功能。 在安装更新时启用功能，或者稍后返回控制台启用可选功能。

若要查看可用功能及其状态，请在控制台中转到“管理”工作区，展开“更新和维护服务”，然后选择“功能”节点。

会自动安装不可选的功能。 该功能不会出现在“功能”节点中。  

> [!Important]  
> 在多站点层次结构中，只能从管理中心站点启用可选功能或预发行功能。 此行为确保层次结构中不会出现冲突。 <!--507197-->
 

启用新功能或预发行功能时，配置管理器层次结构管理器 (HMAN) 必须在该功能可用之前处理更改。 更改的处理通常是即时的。 根据 HMAN 处理周期，可能最多需要 30 分钟才能完成。 处理更改后，必须重启控制台，才能使用该功能。

#### <a name="list-of-optional-features"></a>可选功能列表
下面列出了 Configuration Manager 最新版本中的可选功能：<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

-->

- [包转换管理器](/sccm/apps/pcm/package-conversion-manager) <!--1357861-->
- [第三方软件更新](/sccm/sum/deploy-use/third-party-software-updates)<!--1357605,1352101,1358714-->
- [审批每台设备的用户的应用程序请求](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  
- [iOS 支持 Cisco AnyConnect 4.0.07x 及更高版本](/sccm/mdm/deploy-use/create-vpn-profiles)<!--1357393-->
- [用于条件访问的符合性策略的设备运行状况证明评估](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)<!--1235616-->
- [创建和运行脚本](/sccm/apps/deploy-use/create-deploy-scripts)<!--1236459-->
- [运行任务序列步骤](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [任务序列内容预缓存](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Surface 驱动程序更新](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [数据仓库服务点](/sccm/core/servers/manage/data-warehouse)<!--1277922-->
- [客户端对等缓存](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [PFX 创建](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Azure Log Analytics 连接器](/sccm/core/clients/manage/sync-data-log-analytics) <!--1258052-->
- [Windows Defender 攻击防护策略](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)<!--1355468-->
- [适用于 Windows 10 的 VPN](/sccm/protect/deploy-use/vpn-profiles)<!--1283610-->
- [Windows Hello 企业版](/sccm/protect/deploy-use/windows-hello-for-business-settings)（以前称为 Passport for Work）<!--1245704-->
- [托管电脑的条件访问](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)<!--1191496-->


> [!Tip]  
> 若要详细了解需要同意才能启用的功能，请参阅[预发布功能](/sccm/core/servers/manage/pre-release-features)。  
> 
> 若要详细了解仅在技术预览分支中可用的功能，请参阅[技术预览版](/sccm/core/get-started/technical-preview)。



##  <a name="bkmk_prerelease"></a>使用更新中的预发行功能

Current Branch 包含预发行功能，用于生产环境中的早期测试。 有关详细信息，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。



## <a name="bkmk_faq"></a>常见问题

###  <a name="why-dont-i-see-certain-updates-in-my-console"></a>为什么我在控制台中看不到某些更新？  

如果在与 Microsoft 云服务成功同步之后无法在控制台中找到特定更新，此行为可能由以下原因之一引起：  

-   该更新需要基础结构不使用的配置，或者当前产品版本不满足接收该更新的先决条件。  

     如果认为已拥有所需的配置和缺失更新的先决条件，则确认服务连接点是否处于联机模式。 然后，使用“更新和维护服务”节点的“检查更新”选项强制执行检查。 如果服务连接点处于脱机模式，请使用服务连接工具手动与云服务同步。  

-   对于在 Configuration Manager 控制台中查看更新，你的帐户缺少正确的基于角色的管理权限。 有关详细信息，请参阅[用于管理更新的权限](#assign-permissions-to-view-and-manage-updates-and-features)。  

