---
title: "控制台中更新 | Microsoft Docs"
description: "System Center Configuration Manager 与 Microsoft 云服务同步，以获取可以从控制台中进行安装的更新。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: 1b7063d45c6dc9b42e5002f684043a8e846416a2


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 安装控制台内部更新

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 与 Microsoft 云服务同步，以获取随后可以从 Configuration Manager 控制台中进行安装的更新。

## <a name="get-available-updates"></a>获取可用更新
只有适用于你的基础结构和版本的更新才会进行下载并可用于你的层次结构中。 此同步可以自动或手动进行，具体取决于为层次结构配置服务连接点的方式：

-   在 **联机模式**下，服务连接点会自动连接到 Microsoft 云服务并下载适用的更新。  

     默认情况下，Configuration Manager 会每 24 小时检查一次新的更新。 从 1602 版本或更高版本开始，还可以通过在 Configuration Manager 控制台的“管理” > “云服务” > “更新与维护服务”节点中单击“检查更新”，来立即检查更新。  

-   在**脱机模式**下，服务连接点不会连接到 Microsoft 云服务，必须手动[使用 System Center Configuration Manager 的服务连接工具](../../../core/servers/manage/use-the-service-connection-tool.md)以下载并导入可用更新。  

> [!NOTE]  
>  除了在与 Microsoft 云服务同步时获取的更新之外，使用 [更新注册工具](http://technet.microsoft.com/library/mt691544.aspx) 安装的带外修复也会导入你的控制台中，你随后可以在控制台中选择它们进行安装。  

对更新进行同步之后，可以通过导航到“管理” > “云服务” > “更新与维护服务”节点，在 Configuration Manager 控制台中查看它们：  

-   未安装的更新显示为“可用”。

-   已安装的更新显示为“已安装”。  从版本 1606 开始，只显示最新安装的更新，并且可以单击功能区上的“历史记录”按钮以查看之前安装的更新。



配置服务连接点之前，需了解和规划它的其他使用情况，这会影响你配置此站点系统角色的方式：  

-   服务连接点用于上载有关你站点的使用情况信息。 此信息可帮助 Microsoft 云服务标识你基础结构的当前版本可用的更新。 有关详细信息，请参阅 [System Center Configuration Manager 的诊断和使用情况数据](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

-   服务连接点用于使用 Microsoft Intune 管理设备和使用 Configuration Manager 管理本地移动设备。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)。  

若要更好地理解什么情况会下载更新，请参阅：  

-   [流程图 - 下载 System Center Configuration Manager 的更新](../../../core/servers/manage/download-updates-flowchart.md)

-   [流程图 - 更新 System Center Configuration Manager 的副本](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>查看和管理更新和功能的权限
安装更新 1606 之前，若要在控制台中查看更新，用户必须分配有安全角色，该角色在权限组 **站点** 中包括 **读取**权限并且安全作用域为 **全部**。 从更新 1606 开始，引入新的名为 **更新包** 的基于角色的管理安全类，授予查看和管理 Configuration Manager 控制台中更新的访问。    

**更新包类的信息：**  
默认情况下， **更新包** (SMS_CM_Updatepackages) 是以下具有列出权限的内置安全角色的一部分：
 -  具有**修改** 和 **读取** 权限的 **完全权限管理员** ：
    -   具有此安全角色和具有对 **全部** 安全作用域访问权限的用户可以查看更新、安装更新并在安装过程中启用功能，以及启用各个功能（以前已安装更新）。
    - 具有此安全角色和具有对 **默认** 安全作用域访问权限的用户可以查看更新、安装更新并在安装过程中启用功能，以及查看各个功能（以前已安装更新但未启用该功能）。

- 具有**读取** 权限的 **只读分析员** ：
  -  具有此安全角色，从 1511 版升级到 1606 版或对**默认**作用域有访问权限的用户可以查看更新，但不能安装它们，并且可以查看各个功能（已安装更新但未启用此功能）。

**更新和维护所需的权限汇总：**   
  - 使用分配有安全角色（包括具有 **修改** 和 **读取** 权限的 **更新包** 类）的帐户。
  - 必须为帐户分配 **默认** 作用域。

**仅查看更新**：
  - 使用分配有安全角色（包括具有 **读取** 权限的 **更新包** 类）的帐户。
  - 必须为帐户分配 **默认** 作用域。

**安装更新后启用功能：**
  -   使用分配有安全角色（包括具有 **修改** 和 **读取** 权限的 **更新包** 类）的帐户。
  -  必须为帐户分配 **全部** 作用域。






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> 安装控制台内部更新之前  
 在从 Configuration Manager 控制台中安装更新之前，请查看以下步骤：  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> 步骤 1：查看更新清单  
在从 Configuration Manager 控制台中安装新的更新之前，查看适用的更新清单以了解在开始更新之前要执行的操作：  

-   从[升级到 System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 升级到 1511    

-   从 1511 更新到 1602：请参阅 [1602 的安装更新清单](../../../core/servers/manage/checklist-for-installing-update-1602.md)

- 从 1511 或 1602 更新到 1606：请参阅 [1606 的安装更新清单](../../../core/servers/manage/checklist-for-installing-update-1606.md)  

- 从 1511、1602 或 1606 更新到 1610：请参阅 [1610 的安装更新清单](../../../core/servers/manage/checklist-for-installing-update-1610.md)  

###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> 步骤 2：安装更新之前测试数据库升级  
在层次结构中安装新的更新（如更新 1602）之前，应测试站点数据库的升级。 用于对将更新安装到站点数据库备份进行测试的命令行选项的名称是 **testdbupgrade**。  

与 Configuration Manager 的早期版本不同，如果安装更新失败，则无需执行站点恢复，而应重试安装更新。 因此，虽然与过去的产品版本相比，数据库的测试升级不太重要，不过这仍然是建议步骤。  

#### <a name="to-run-testdbupgrade-before-installing-an-update"></a>安装更新之前运行 testdbupgrade  

1.  从运行计划更新的版本的站点的 **CD.Latest** 文件夹获取一组源文件。 这可能需要首先在运行该版本的 System Center Configuration Manager 实验室或测试环境中安装站点。  

     站点的 **CD.Latest** 文件夹包含该版本的源文件。 必须使用这些源文件运行站点数据库的测试升级。 有关详细信息，请参阅 [System Center Configuration Manager 的 CD.Latest 文件夹](../../../core/servers/manage/the-cd.latest-folder.md)。  

     例如，如果你的站点运行版本 1501 并且你要更新为 1602，则必须从已更新为版本 1602 的站点获取 CD.Latest 文件夹。 通常，可以在实验室中安装一个新的临时站点，然后将该站点升级到版本 1602 以创建具有所需文件的 CD.Latest 文件夹。  

2.  将 CD.Latest 文件夹复制到将用于运行测试数据库升级的 SQL Server 上的某个位置。 （请参阅下一步）。  

3.  创建要测试升级的站点数据库的备份，然后将该数据库的副本还原到未托管 Configuration Manager 站点的 SQL Server 实例。 该 SQL Server 使用的 SQL Server 版本必须与站点数据库相同。  

4.  还原数据库副本之后，在从实验室或测试环境复制的 CD.Latest 文件夹中运行 **安装程序** 。 运行安装程序时，使用 **/TESTDBUPGRADE** 命令行选项。 如果承载数据库副本的 SQL Server 实例不是默认实例，你还必须提供命令行参数以确定承载站点数据库副本的实例。  

     例如，你计划升级数据库名称为 SMS_ABC 的站点数据库。 你将此站点数据库的副本还原到实例名称为 DBTest 的受支持 SQL Server 实例。 要测试站点数据库的此副本的升级，请使用下列命令行： **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     可以在 System Center Configuration Manager 的源媒体上的下列位置中找到 Setup.exe：**SMSSETUP\BIN\X64**。  

5.  在运行数据库升级测试的 SQL Server 实例上，监视系统驱动器根目录中的 ConfigMgrSetup.log 以了解进度和成功情况。  

     如果测试升级失败，请解决与站点数据库升级失败相关的任何问题，创建站点数据库的新备份，然后测试站点数据库的新副本的升级。  

     过程成功完成后，你可以删除该数据库副本。  

    > [!NOTE]  
    >  不支持还原用于测试升级的站点数据库的副本以用作任何站点上的站点数据库。  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> 步骤 3：安装更新之前运行先决条件检查程序  
安装更新之前，请考虑运行针对该更新的先决条件检查。 如果在安装更新之前运行先决条件检查：  

-   更新文件会在安装更新之前复制到其他站点  

-   选择安装更新时，先决条件检查会再次自动运行  

以后在安装更新时，你可以选择配置更新以忽略先决条件检查警告。  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>安装更新之前运行先决条件检查程序  

1.  在 Configuration Manager 控制台中，转到“管理” > “云服务” > “更新与维护服务”。  

2.  右键单击要对其运行先决条件检查的更新包。  

3.  选择“运行先决条件检查”。  可以查看  

     运行先决条件检查时，更新的内容会复制到子站点。  可以查看站点服务器上的 **distmgr.log** 以确认该内容复制成功。  

4.  若要查看检查的结果，请在 Configuration Manager 控制台中转到“监视” > “更新与维护服务状态”，然后查找先决条件状态。 还可以查看站点服务器上的 ConfigMgrPrereq.log 以了解更多详细信息。  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> 安装控制台内部更新  
 准备好从 Configuration Manager 控制台中安装更新后，请从层次结构的顶层站点开始。 这是管理中心站点或独立主站点。  

 我们建议你计划在正常营业时间之外为每个站点安装更新，此时安装更新的过程以及用于重新安装站点组件和站点系统角色的操作对业务运营的影响最小。  

-   管理中心站点完成更新安装之后，子主站点会自动启动更新。 这是建议的默认进程。 但可以使用[站点服务器的服务时段](#bkmk_ServiceWindow)控制主站点安装更新的时间。  

-   在主父站点更新完成之后，必须从 Configuration Manager 控制台中手动更新辅助站点。 不支持辅助站点服务器的自动更新。  

-   在站点更新之后使用 Configuration Manager 控制台时，系统会提示你更新控制台。  

-  站点服务器成功完成安装更新后，它将自动更新所有合适的站点系统角色。  唯一需要注意的是分发点：
  - 由于 1606 版更新中引入了更改，将更新安装到已运行 1606 版或更高版本的站点时，所有分发点不再脱机安装更新。 而站点服务器使用站点的内容分发设置，一次性将更新分发到分发点的子集。 结果只有某些分发点脱机以安装更新。 这允许尚未开始更新或已完成更新的分发点保持联机状态，并能够向客户端提供内容。


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> 控制台内部更新安装的概述  
**1.更新安装启动时**  
会向你呈现更新向导，显示更新适用的产品区域的列表。  

-   在该向导的“常规”页面中，可以配置“先决条件警告”。  
      -   先决条件错误会始终停止更新安装。 必须先解决错误，然后才能成功地重试更新安装。 有关详细信息，请参阅 [重试失败更新的安装](#bkmk_retry) 。  

    -   先决条件警告也可以停止更新安装。 重试更新安装之前，应解决警告。   有关详细信息，请参阅[重试失败更新的安装](#bkmk_retry)。  
    -   选择选项“忽略任何先决条件检查警告并安装此更新，无论是否缺少要求”，为更新安装设置忽略先决条件警告的条件，并允许更新安装继续。 如果不选择此选项，则在遇到警告时会停止更新安装。 除非以前为站点运行了先决条件检查并解决了先决条件警告，否则我们不建议使用此选项。  

      从 1606 版本开始，“管理”和“监视”这两个工作区中的“更新和维护”节点都包括功能区上一个名为“忽略先决条件警告”的按钮。 当因先决条件检查警告而导致无法完成更新包安装时，可以使用此按钮。  例如，如果不使用“忽略先决条件警告”的选项安装更新（从更新向导中），更新安装中止并出现先决条件警告状态，但没有发生错误，那么之后可以在功能区选择“忽略先决条件警告”来触发自动继续忽略先决条件警告的更新安装。  使用此选项时，几分钟后将自动继续更新安装。



-   更新适用于 Configuration Manager 客户端时，将向你提供一个选项，即使用一组有限的客户端来测试该客户端更新。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

**2.更新安装过程中**  
作为更新安装的一部分，Configuration Manager 将：  

-   重新安装任何受影响的组件，如站点系统角色或 Configuration Manager 控制台。  

-   基于你针对客户端试验以及针对 [自动客户端升级](https://technet.microsoft.com/library/mt627885.aspx)进行的选择来管理客户端的更新  

-   在更新过程中无需重新启动站点系统服务器（除非作为站点系统角色先决条件的一部分安装 .NET）  

> [!TIP]  
>  安装更新时，Configuration Manager 还会更新在站点恢复期间使用的 CD.Latest 文件夹。  

**3.在安装更新时监视更新进度**  
使用以下操作可监视进度：  

-   在 Configuration Manager 控制台中：转到“管理” > “云服务” > “更新与维护服务”。 此节点显示所有更新包的安装状态。


-   在 Configuration Manager 控制台中：转到“监视” > “概述” > “更新与维护服务”节点。 此节点仅显示当前正在安装的更新包的安装状态。  

    从版本 1606 开始，为便于监视，将更新包安装划分为以下几个阶段。 对于每个阶段，现在提供了更多详细信息，包括要查看有关详细信息的日志文件：  
    -   **下载**（此阶段仅适用于已安装服务连接点站点系统角色所在的顶层站点）
    -   **复制**
    -   **先决条件检查**
    -   **安装**
    -   **安装后**（此阶段适用于 1610 以及之后的版本）

-   可以查看 **&lt;ConfigMgr_Installation_Directory>\Logs** 中的 **CMUpdate.log** 文件  

**4.更新安装完成时**  
第一个站点更新完成安装之后：  

-   子主站点会自动安装更新。 不需要采取任何进一步措施。  

-   必须从 Configuration Manager 控制台中手动更新辅助站点。
> [!TIP]
> 虽然控制台中不会显示辅助站点的版本，但可以使用 Configuration Manager SDK 确认站点版本。 请参阅 [SMS_Site Server WMI 类](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx)。


-   在层次结构中的所有站点均更新为新版本之前，你的层次结构会在混合版本模式下运行。 有关详细信息，请参阅 [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md)。  

**5. 更新 Configuration Manager 控制台**  
在管理中心站点或主站点更新之后，还必须更新连接到该站点的每个 Configuration Manager 控制台。 系统会在以下情况下提示你更新控制台：  

-   打开控制台时  

-   在打开的控制台中导航到新节点时  

我们建议立即安装更新，而不是延迟。  

控制台更新完成之后，可以验证控制台和站点版本是否正确。 转到控制台左上角的“关于 System Center Configuration Manager”，新站点和控制台版本将会显示在那里。  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> 在顶层站点上启动更新安装  
在层次结构的顶层站点上，在 Configuration Manager 控制台中，转到“管理” > “云服务” > “更新与维护服务”，选择“可用”更新，然后单击“安装更新包”。  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> 在辅助站点上启动更新安装  
更新辅助站点父主站点之后，随后可以从 Configuration Manager 控制台中更新辅助站点。  为此，请使用“升级辅助站点向导”。  

1.  在 Configuration Manager 控制台中，转到“管理” > “站点配置” > “站点”，选择要更新的站点，然后在“主页”选项卡上的“站点”组中，单击“升级”。  

2.  单击“是”以启动辅助站点的更新。  

若要在辅助站点上监视更新安装，请选择辅助站点服务器，然后在“开始”选项卡上的“站点”组中，单击“显示安装状态”。 还可以将“版本”列添加到控制台显示中，以便可以查看每个辅助站点的版本。  

成功更新辅助站点后，如果控制台中的状态未刷新或显示更新失败，则可以使用“重试安装”选项。 此选项不会重新安装辅助站点（未成功安装更新）的更新，但会强制控制台更新状态。


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> 重试失败更新的安装  
更新安装失败时，查看控制台内部反馈以确定针对警告和错误的解决方法。  还可以查看站点服务器上的 ConfigMgrPrereq.log 以了解更多详细信息。 重试更新安装之前，必须解决错误，并且应解决警告。  

准备重试安装更新时，选择失败的更新，然后选择适用的选项。 更新安装重试行为取决于开始重试的节点以及使用的重试选项：  

1.  **为层次结构重试安装：**  
当某个更新处于以下状态之一时，可以为整个层次结构重试该更新的安装：  

    -   先决条件检查已通过但存在一个或多个警告，并且未在更新向导中设置用于忽略先决条件检查警告的选项（“更新和维护”节点中的“忽略先决条件警告”的更新值是“否”）   
    -   先决条件失败    
    -   安装失败
    -   内容复制到站点失败   

    转到“管理” > “云服务” > “更新和维护”，选择更新并单击下列选项之一：  

    -   **重试** - 当你从该节点运行重试时，将再次开始更新安装，并自动忽略先决条件警告。 如果之前复制失败，它还将重新复制更新的内容。
    - **忽略先决条件警告** - 从版本 1606 开始，如果由于警告而导致更新安装中止，则可以单击“忽略先决条件警告”。 此操作将允许继续安装更新（几分钟后），并使用“忽略先决条件警告”的选项。   

2.  **为站点重试安装：**  
 当某个更新处于以下状态之一时，可以在特定站点上重试该更新的安装：  

    -   先决条件检查已通过但存在一个或多个警告，并且未在更新向导中设置用于忽略先决条件检查警告的选项（“更新和维护”节点中的“忽略先决条件警告”的更新值是“否”）  
    -   先决条件失败    
    -   安装失败    

    转到“监视” > “概述” > “站点服务状态”，选择更新，然后单击下列选项之一：

       - **重试** - 当从该节点运行重试时，仅在此站点重启安装更新。 与从更新和维护节点运行重试不同，此重试不会忽略先决条件警告。
       -    **忽略先决条件警告** - 从版本 1606 开始，如果由于警告而导致更新安装中止，则可以单击“忽略先决条件警告”。 此操作将允许继续安装更新（几分钟后），并使用“忽略先决条件警告”的选项。

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> 站点安装更新之后  
使用以下清单可完成在站点更新之后进行的常见任务和配置：  

**确认站点到站点复制处于活动状态：**在 Configuration Manager 控制台中，转到以下位置以查看状态并确保复制处于活动状态：  

-   “监视” > “概述” > “站点层次结构”  

-   “监视” > “概述” > “数据库复制”  

有关详细信息，请参阅 [System Center Configuration Manager 中的监视层次结构和复制基础结构](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md)和[关于复制链接分析器](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)。  

 **确认站点服务器和远程站点系统服务器已重新启动（如果需要）：** 查看站点基础结构，并确保适用的站点服务器和站点系统服务器（远离站点服务器）已成功重新启动。  通常，仅当 Configuration Manager 安装 .NET 作为站点系统角色的先决条件时，这才是预期行为。  

 **更新独立 Configuration Manager 控制台：**确保所有远程 Configuration Manager 控制台都更新为相同版本。 系统会在以下情况下提示你更新控制台：  

-   在控制台中导航到新节点  

-   打开控制台时  

**为主站点中的管理点重新配置数据库副本：** 如果将数据库副本用于主站点中的管理点，则必须先卸载数据库副本，再更新站点。 更新主站点之后，为管理点重新配置数据库副本。 有关详细信息，请参阅 [System Center Configuration Manager 管理点的数据库副本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

**重新配置在更新之前禁用的任何数据库维护任务：**如果更新之前在站点上禁用了 [System Center Configuration Manager 的数据库维护任务 ](../../../core/servers/manage/maintenance-tasks.md)，请使用与更新之前存在的相同设置在站点上重新配置这些任务。  

**升级客户端：**有关如何升级现有客户端和如何安装新客户端的信息，请参阅[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)  

**其他配置：** 查看在启动更新之前进行的更改，然后将这些配置还原到站点和层次结构。  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> 启用更新中的可选功能  
当安装的更新包含一个或多个可选功能时，你可以选择在层次结构中启用这些功能。  可以在安装更新时执行此操作，或在稍后返回控制台并启用可选功能时执行此操作。

若要查看可用功能及其状态，请在控制台中导航到“管理” > “云服务” > “更新和维护” > “功能”。

当功能不可选时，它会自动安装，不会出现在“功能”节点中。  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> 使用更新中的预发行功能
从 1606 开始，必须同意使用 System Center Configuration Manager 中的预发行功能，然后才可以选择并启用它们。  

预发行功能包含在产品中，用于在生产环境中进行早期测试，但不应将其视为生产就绪。

若要同意，则在控制台中导航到“管理” > “站点配置” > “站点”，然后选择“层次结构设置”。 在“常规”选项卡上，选择“同意使用预发行功能”。
 -  同意是对每个层次结构执行的一次性操作，不能撤消  
 -  除非你同意，否则不能启用1606 版或更高版本的更新版本中包括的新的预发行功能

 > [!NOTE]
 > 如果安装更新 1606 之前启用了更新 1602 的预发行功能，即使你不同意使用预发行功能，安装 1606 后也可使用这些功能。

当你的层次结构运行版本 1606 或更高版本，然后再安装包含预发行功能的更新时，这些功能和此次更新包含的常规功能在更新和维护向导中可见：
  - **如果同意：** 安装更新时，可以启用更新和维护向导中的预发行功能。 为此，请选择预发行功能，就像选择任何其他功能那样。     

    也可以之后从控制台的“管理” > “云服务” > “更新和维护服务” > “功能”节点启用预发行功能。 为此，请在“功能”节点中选择要该功能，然后单击“开启”。 （你同意之前，此选项将灰显且不可用。）  
  -   **如果不同意：** 安装更新时，预发行功能在更新和维护向导中可见，但将灰显且不能启用。 安装更新之后，你可以在功能节点中查看这些功能，但不可启用它们（直到你在层次结构设置同意）。

 > [!TIP]
 > 安装 1606 版更新时，1606 版更新中包含的预发行功能在更新和维护向导中不可见，且此时不可启用。 安装 1606 版更新后，可以查看功能节点中包括的预发行功能。

如果同意在独立主站点通过安装新的管理中心站点扩展层次结构，则还必须在管理中心站点也同意这样做。

**可以使用以下预发行功能：**

 |功能                    |添加为预发行功能 |添加为完整版功能 |  
|----------------------------|---------------------|------------------------|
| 用于向客户端进行内容分发的对等缓存 |  [版本 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 云管理网关 |  [版本 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 客户端数据源仪表板 |  [版本 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite (OMS) 连接器  | [版本 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 维护群集感知集合（为服务器组提供服务）| [版本 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|对由 System Center Configuration Manager 管理的电脑进行条件访问 | [版本 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |




##  <a name="a-namebkmkservicewindowa-service-windows-for-site-servers"></a><a name="bkmk_ServiceWindow"></a> 站点服务器的服务时段  
在站点服务器上，可以配置服务时段以控制 Configuration Manager 的基础结构更新可应用于此站点服务器的时间。  每个站点服务器支持多个时段，时段允许用于安装基础结构更新，更新由为该站点服务器配置的所有时段的组合决定。  

**配置服务时段：**  

1.  在 Configuration Manager 控制台中，打开“管理” > “站点配置” > “站点”，然后选择要在其中配置服务时段的站点服务器。  

2.  接下来，编辑站点服务器“属性”，然后选择“服务时段”选项卡，此时你可以在其中为该站点服务器设置一个或多个服务时段。  

##  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a>为什么我在控制台中看不到某些更新？  
 如果你在成功与 Microsoft 云服务同步之后在控制台中找不到特定更新或任何更新，这可能是因为：  

-   更新需要基础结构不使用的配置，或者当前产品版本不满足接收更新的先决条件。  

     如果你认为自己对于缺少的更新具有所需配置或满足其他先决条件，请确认服务连接点处于联机模式，然后使用“更新和维护”节点中的“检查更新”选项来强制执行检查。  如果处于脱机模式，则必须使用服务连接工具手动与云服务同步。  

-   对于在 Configuration Manager 控制台中查看更新，你的帐户缺少正确的基于角色的管理权限。

    有关查看更新并从控制台启用功能所需权限的信息，请参阅此主题中[管理更新的权限](../../../core/servers/manage/install-in-console-updates.md#permissions-to-view-and-manage-updates-and-features)。



<!--HONumber=Dec16_HO3-->


