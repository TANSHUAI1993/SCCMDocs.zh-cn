---
title: "Technical Preview 1706 | Microsoft 文档"
description: "了解在 System Center Configuration Manager 的 Technical Preview 1706 中的可用功能。"
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d45f504dfe0a4c7852b0e2c8ff60d54005346c02
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>在 System Center Configuration Manager 的 Technical Preview 1706 中的功能

*适用范围：System Center Configuration Manager（Technical Preview）*

本文将介绍在 System Center Configuration Manager 的 Technical Preview 1706 中的可用功能。 你可以安装此版本，以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 中的已知问题：**

-   移动分发点 - 由于单一主站点 Technical Preview 的限制，控制台中用于在站点之间移动分发点的选项不能用于此版本。

-   设备符合性设置 - 当使用两个新的设备符合性设置时，可能会遇到相反的行为：
    - **在设备上阻止进行 USB 调试**
    - **阻止来自未知源的应用**

        例如，如果管理员将“在设备上阻止进行 USB 调试”设置为“true”，则所有未启用 USB 调试的设备均会被标记为不符合。

**以下是此版本可以试用的新功能。**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>改进了软件更新点的边界组
<!-- 1324591 -->
此版本包括了针对软件更新点如何与边界组配合使用的多项改进。 以下内容总结了新的回退行为：
-   现在，软件更新点的回退使用一个可配置的时间来回退到相邻边界组，最小时间为 120 分钟。

-   独立于回退配置，客户端会尝试访问它使用了 120 分钟的最后一个软件更新点。 在 120 分钟无法访问该服务器后，客户端将检查其池中可用的软件更新点，以便找到一个新的软件更新点。

  -   客户端当前边界组中的所有软件更新点都将立即添加到客户端池。

  -   因为客户端在查找新的软件更新点之前，会尝试在 120 分钟内使用原始服务器，所以在两小时过去之前不会联系其他服务器。

  -   如果回退到相邻组配置为最小 120 分钟，那么来自该相邻边界组的软件更新点将成为客户端可用服务器池的一部分。

-   如果在两个小时内无法连接到其原始服务器，则客户端会切换到一个短循环，以联系新的软件更新点。

    这意味着，如果客户端无法连接到新的服务器，它就会从自己的可用服务器池中快速选择下一个服务器，并尝试进行连接。

  -   此循环将一直持续下去，直到客户端连接到可以使用的软件更新点。
  -   在客户端找到软件更新点后，当满足每个相邻边界组的回退时间时，会将其他服务器添加到可用服务器池中。

有关详细信息，请参阅 Current Branch 的边界组主题中的[软件更新点](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)。


## <a name="site-server-role-high-availability"></a>站点服务器角色的高可用性
<!-- 1128774 -->
站点服务器角色的高可用性是一个基于 Configuration Manager 的解决方案，用以在“被动”模式下安装其他主站点服务器。 被动模式站点服务器是现有处于“主动”模式的主站点服务器的另一个服务器。 在需要时可立即使用被动模式站点服务器。

被动模式主站点服务器：
-   使用相同的站点数据库作为活动站点服务器。
-   接收活动站点服务器内容库的副本，然后同步保存。
-   只要在被动模式下，将不会向站点数据库写入数据。
-   只要在被动模式下，将不支持安装或删除可选的站点系统角色。

要将被动模式站点服务器设置成为主动模式站点服务器，可通过手动进行提升。 这会将主动站点服务器切换为被动站点服务器。 只要该计算机可以访问，在原始主动模式服务器上可用的站点系统角色将仍然可用。 仅站点服务器角色会在主动和被动模式之间切换。

要安装被动模式站点服务器，可使用“创建站点系统服务器向导”来配置一个类型为“主站点服务器”、模式为“被动”的新站点服务器。 然后，该向导将在指定服务器上运行 Configuration Manager 安装程序，以在被动模式下安装新的站点服务器。 安装完成后，主动模式站点服务器将保留被动模式站点服务器及其内容库，以便与你对活动站点服务器所做的更改或配置进行同步。

### <a name="prerequisites-and-limitations"></a>先决条件和限制
-   每个主站点均支持在被动模式下的单一站点服务器。

-   被动模式下的站点服务器可以是本地服务器或是 Azure 中基于云的服务器。

-   主动模式和被动模式站点服务器都必须位于同一域中。

-   主动模式和被动模式站点服务器都必须使用相同的站点数据库，该数据库必须远离每个站点服务器的计算机。

    -   承载数据库的 SQL Server 可以使用默认实例、命名实例、SQL Server 群集或 Always On 可用性组。

    -   被动模式下的站点服务器被配置为使用与主动模式站点服务器相同的站点数据库。 但是，被动模式站点服务器在提升为主动模式之前将不使用该数据库。

-   将运行被动模式站点服务器的计算机：

    -   必须满足[安装主站点的先决条件](https://docs.microsoft.com/en-us/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site)。

    -   使用与主动模式站点服务器的版本相匹配的源文件进行安装。

    -   在安装被动模式站点之前，不能从任何站点获得站点系统角色。

-   主动和被动模式站点服务器计算机可运行不同的操作系统或服务包版本，只要它们一直受 Configuration Manager 版本的支持。

-   被动模式站点服务器到主动模式服务器的提升为手动操作。 没有任何自动故障转移。

-   只能在处于主动模式的站点服务器上安装站点系统角色。

    -   主动模式下的站点服务器支持所有站点系统角色。 在被动模式下时，无法在服务器上安装站点系统角色。

    -   使用数据库（如报告点）的站点系统角色必须在远离主动模式和被动模式站点服务器的服务器上拥有该数据库。

    -   SMS_Provider 不会以被动模式安装在站点服务器上。 因为必须连接到站点的 SMS_Provider 手动将被动模式站点服务器提升为主动模式，我们建议在其他计算机上[至少安装一个附加的提供程序实例](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。

**已知问题**：   
此版本中，以下条件的状态在控制台中将显示为数值，而不是可读文本：
-   131071 – 站点服务器安装失败
-   720895 – 站点服务器角色卸载失败
-   851967 – 故障转移失败

### <a name="add-a-site-server-in-passive-mode"></a>添加被动模式站点服务器
1.  在控制台中，转到“管理” > “站点配置” > “站点”，并启动[“添加站点系统角色向导”](/sccm/core/servers/deploy/configure/install-site-system-roles)。 还可以使用“创建站点系统服务器向导”。

2.  在“常规”页上，指定将承载被动模式站点服务器的服务器。 在被动模式下安装站点服务器之前，你指定的服务器不能承载任何站点系统角色。

3.  在“系统角色选择”页上，仅选择“被动模式下的主站点服务器”。

4.  要完成向导，必须提供用于在指定服务器上运行安装程序并安装站点服务器角色的以下信息：
    -   选择将安装文件从主动站点服务器复制到新的被动模式站点服务器，或指定一个包含主动站点服务器“CD.Latest”文件夹内容位置的路径。

    -   指定主动模式站点服务器使用的同一站点数据库服务器和数据库名称。

5.  然后，Configuration Manager 在指定服务器上安装被动模式站点服务器。

有关详细的安装状态，请转到“管理” > “站点配置” > “站点”。
-   被动模式下的站点服务器状态将显示为“正在安装”。

-   选择服务器，然后单击“显示状态”，打开“站点服务器安装状态”，以查看更多详细信息。



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>将被动模式站点服务器提升为主动模式
如果想要将被动模式站点服务器更改为主动模式，则可以从“管理” > “站点配置” > “站点”的“节点”窗格中执行此操作。 只要可以访问 SMS_Provider 实例，便可以访问站点来执行此更改。
1.  在 Configuration Manager 控制台的“节点”窗格中，选择被动模式下的站点服务器，然后从功能区中选择“提升为主动”。

2.  正在提升的服务器的简单“状态”在“节点”窗格中显示为“正在提升”。

3.  在提升完成后，“状态”列将对这两个新的主动模式站点服务器和新的被动模式站点服务器显示为“确定”。

4.  在“管理” > “站点配置” > “站点”中，主站点服务器的名称现在显示主动模式站点服务器的新名称。
有关详细状态，请转到“监视” > “站点服务器状态”。
    -   “模式”列将标识哪个服务器为主动或被动。

    -   将服务器从被动模式提升到主动模式时，选择要提升为主动的站点服务器，然后从功能区选择“显示状态”。 这将会打开“站点服务器升级状态”窗口，其中显示有关该流程的其他详细信息。

当主动模式下的站点服务器切换为被动模式时，仅站点系统角色会成为被动模式。 在该计算机上安装的所有其他站点系统角色则保持主动状态，并可供客户端访问。


### <a name="daily-monitoring"></a>每日监视
如果你有被动模式下的主站点，请进行每日监视，以确保其与主动模式站点服务器保持同步并可供使用。 要执行此操作，请转到“监视” > “站点服务器状态”。 在此你可以查看主动模式和被动模式站点服务器。

“摘要”选项卡：
-   “模式”列标识哪个服务器为主动或被动。
-   “状态”列在被动模式服务器与主动模式服务器同步时会显示“确定”。
-   要查看有关内容同步状态的其他详细信息，请单击“内容同步状态”中的“显示状态”。 这将会打开“内容库”选项卡，你可以在其中尝试修复内容同步问题。

“内容库”选项卡：
-   查看从主动站点服务器同步到被动模式站点服务器的内容的“状态”。
-   你可以选择状态为“失败”的内容，然后从功能区选择“同步所选项”。 此操作将尝试重新将内容从内容源同步到被动模式站点服务器。 在恢复期间，状态将显示为“正在进行”，并在同步后显示为“成功”。

### <a name="try-it-out"></a>试试看！
请尝试完成以下任务，然后从功能区的“主页”选项卡向我们发送“反馈”，让我们了解它的工作状况：
-   我可以在被动模式下安装主站点。
-   我可以使用控制台来提升被动模式站点服务器，以使其成为主动模式站点服务器，并确认这两个站点服务器的状态更改。


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>在 Device Guard 策略中包括对特定文件和文件夹的信任
<!-- 1324676 -->
在此版本中，我们已向 [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) 策略管理添加了更多功能

现在可以选择在 Device Guard 策略中添加对特定文件或文件夹的信任。 此操作可让你：

1.  解决托管安装程序行为的问题
2.  信任无法使用 Configuration Manager 部署的业务线应用
3.  信任包括在操作系统部署映像中的应用

### <a name="try-it-out"></a>试试看！

1.  在创建 Device Guard 策略时，在“创建 Device Guard 策略向导”的“包含”项选项卡上，单击“添加”。
2.  在“添加受信任文件或文件夹”对话框中，指定有关你想要信任的文件或文件夹的信息。 你可以指定本地文件或文件夹路径，或者连接到你有权连接的远程设备，并指定文件或文件夹在该设备上的路径。
3.  完成向导。


## <a name="hide-task-sequence-progress"></a>隐藏任务序列进度
<!-- 1354291 -->
在此版本中，你可以通过使用新的变量控制何时向最终用户显示任务序列进度。 在任务序列中，使用“设置任务序列变量”步骤来设置“TSDisableProgressUI”变量的值，以隐藏或显示任务序列进度。 你可以在任务序列中多次使用“设置任务序列变量”步骤来更改变量的值。 这样可以在任务序列进度的不同部分中隐藏或显示任务序列。

#### <a name="to-hide-task-sequence-progress"></a>隐藏任务序列进度
在任务序列编辑器中，使用[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤将“TSDisableProgressUI”变量的值设置为“True”，以隐藏任务序列进度。

#### <a name="to-display-task-sequence-progress"></a>显示任务序列进度
在任务序列编辑器中，使用[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤将“TSDisableProgressUI”变量的值设置为“False”，以显示任务序列进度。

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>指定安装内容和卸载内容的不同内容位置
<!-- 1097546 -->
在今天的 Configuration Manager 中，你可以指定包含应用安装程序文件的安装位置。 指定安装位置时，它同样可用作应用程序内容的卸载位置。
根据你的反馈，当想要卸载部署的应用程序，并且应用内容不在客户端计算机上时，客户端会在卸载应用程序之前再次下载所有应用安装程序文件。
为了解决此问题，现在你可以同时指定一个安装内容位置和一个可选的卸载内容位置。 此外，你还可以选择不指定卸载内容位置。

### <a name="try-it-out"></a>试试看！

1. 在应用程序的部署类型属性中，请单击“内容”选项卡。
2. 将“安装内容位置”配置为常规。
3. 对于“卸载内容设置”，请选择以下项之一：
    - 与安装内容相同 - 无论是安装还是卸载应用程序，都将使用相同的内容位置。
    - 没有卸载内容 - 如果你不想为应用程序提供卸载内容位置，则选择此选项。
    - 不同于安装内容 - 如果你想要指定不同于安装内容位置的卸载内容位置，则选择此选项。
5. 如果你选择“不同于安装内容”，则浏览到或输入将用于卸载应用程序的应用内容的位置。
6. 单击“确定”以关闭部署类型属性对话框。


## <a name="accessibility-improvements"></a>辅助功能改进  
<!--1253000 -->
此预览版在 Configuration Manager 控制台中引入了对[辅助功能](/sccm/core/understand/accessibility-features)的多项改进。 其中包括:     

**在控制台中移动的新键盘快捷方式：**
-   Ctrl + M - 将焦点设置在主（中心）窗格中。
-   Ctrl + T - 将焦点设置到导航窗格中的顶级节点。 如果焦点已在此窗格中，则将焦点设置到你访问的最后一个节点。
-   Ctrl + I - 将焦点设置到功能区下方的痕迹导航栏中。
-   Ctrl + L - 将焦点设置到“搜索”字段中（可用时）。
-   Ctrl + D - 将焦点设置到“详细信息”窗格中（可用时）。
-   Alt – 将焦点移入和移出功能区。

**一般改进：**
-   改进了在导航窗格键入节点名称字母时的导航。
-   现在通过主视图和功能区的键盘导航为圆形。
-   现在详细信息窗格中的键盘导航为圆形。 要返回到上一个对象或窗格，使用 Ctrl + D，然后按住 Shift + TAB 即可实现。
-   在刷新工作区视图后，焦点将设置到该工作区的主窗格中。
-   修复了一个问题，可使屏幕阅读器公布列表项的名称。
-   为页面上的多个控件添加了可访问名称，使得屏幕阅读器可以公布重要信息。


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>更改 Azure 服务向导以支持升级就绪情况
<!-- 1353331 -->
从此版本开始，可使用 Azure 服务向导来配置从 Configuration Manager 到[升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)的连接。 通过使用相关 Azure 服务的常见向导，简化了连接器的配置。   

虽然配置连接的方法已更改，但是连接的先决条件和对“升级就绪情况”的使用方式仍保持不变。   

### <a name="prerequisites-for-upgrade-readiness"></a>升级就绪情况的先决条件
[与升级就绪情况的连接](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness)的先决条件与所述的 Configuration Manager 的 Current Branch 相比，没有变化。 为方便起见，在此予以重复列出：  

**先决条件**
-   若要添加连接，Configuration Manager 环境必须先在[联机模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)下配置[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 将连接添加到环境时，它还会在运行此站点系统角色的计算机上安装 Microsoft Monitoring Agent。
-   将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具，并获得[来自此注册的客户端 ID](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)。
-   在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。
-   在 Azure 管理门户中，向已注册的 Web 应用提供访问 OMS 的权限，如[向 Configuration Manager 提供 OMS 权限](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)中所述。

> [!IMPORTANT]       
> 配置访问 OMS 的权限时，请务必选择**参与者**角色，并向其分配注册应用的资源组的权限。

配置先决条件后，便可以使用该向导来创建连接。

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>使用 Azure 服务向导配置升级就绪情况
1.  在控制台中，转到“管理” > “概述” > “云服务” > “Azure 服务”，然后从功能区的“主页”选项卡上选择“配置 Azure 服务”，以启动“Azure 服务向导”。

2.  在“Azure 服务”页上，选择“升级就绪情况连接器”，然后单击“下一步”。

3.  在“应用”页上，指定你的“Azure 环境”（Technical Preview仅支持公有云）。 然后，单击“导入”，以打开“导入应用”窗口。

4.  在“导入应用”窗口中，指定 Azure AD 中现存的 Web 应用的详细信息。
    -   为 Azure AD 租户名称提供一个友好名称。 然后，指定租户 ID、应用名称、客户端 ID、Azure Web 应用的密钥，以及应用 ID URI。
    -   单击“验证”，如果成功，则单击“确定”以继续。

5.   在“配置”页上，指定想要与此升级就绪情况的连接一起使用的订阅、资源组和 Windows Analytics 工作区。  

6.  单击“下一步”转到“摘要”页，然后完成向导以创建连接。


## <a name="new-client-settings-for-cloud-services"></a>云服务的新客户端设置
<!-- 1319883 -->

在此版本中，我们向 Configuration Manager 添加了两个新的客户端设置。 这两个新设置将可以在“云服务”部分找到。  这些设置为你提供了以下功能：

- 控制哪些 Configuration Manager 客户端可以访问已配置的云管理网关。
- 在 Azure Active Directory 中自动注册已加入域的 Windows 10 Configuration Manger 客户端。

这些新设置可帮助你实现 [Configuration Manager 1705 Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management)中所述的功能。

### <a name="before-you-start"></a>开始之前

你必须在本地 Active Directory 和 Azure AD 租户之间安装并配置 Azure AD Connect。

如果你删除了该连接，设备不会取消注册，但不会注册新的设备。

### <a name="try-it-out"></a>试试看！

1. 使用[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)中的信息来配置以下客户端设置（在云服务中找到）部分。
    -   在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备 – 设置为“是”（默认值），或“否”。
    -   允许客户端使用云管理网关 – 设置为“是”（默认值），或“否”。
2.  将客户端设置部署到所需的设备集合。

要确认设备是否已加入 Azure AD，请在命令提示符窗口运行命令“dsregcmd.exe /status”。 如果设备已加入 Azure AD，结果中的“AzureAdjoined”字段将显示“YES”。

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台创建并运行 PowerShell 脚本
<!-- 1236459 -->

在 Configuration Manager 中，你可以使用包和程序将脚本部署到客户端设备。 在此 Technical Preview 中，我们添加了可以让你执行以下操作的新功能：

- 将 PowerShell 脚本导入到 Configuration Manager
- 从 Configuration Manager 控制台编辑脚本（仅针对未签名的脚本）
- 将脚本标记为“已批准”或“已拒绝”，以提高安全性
- 在 Windows 客户端 PC 和本地托管的 Windows PC 的集合上运行脚本。 不过，你不需要部署脚本，它们可以在客户端设备上近乎实时的运行。
- 在 Configuration Manager 控制台中检查脚本返回的结果。


### <a name="prerequisites"></a>先决条件

要使用这些脚本，你必须是相应 Configuration Manager 安全角色的成员。

- 导入并编写脚本 - 对于“符合性设置管理员”安全角色中的“SMS 脚本”，你的帐户必须具有“创建”权限。
- 批准或拒绝脚本 - 对于“符合性设置管理员”安全角色中的“SMS 脚本”，你的帐户必须具有“批准”权限。
- 运行脚本 - 对于“符合性设置管理员”安全角色中的“集合”，你的帐户必须具有“运行脚本”权限。

有关 Configuration Manager 安全角色的详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。

默认情况下，用户不能批准他们创建的脚本。 由于这些脚本功能非常强大、用途多样，并且可以部署到多个设备，因此，我们引入了一种新的概念，用于将脚本创建者和脚本批准者之间的角色相互分开。 这样做可以额外提升安全级别，避免在没有监督的情况下运行脚本。 你可以关闭此辅助批准策略，以方便测试，尤其是在Technical Preview 中。

若允许用户批准他们自己的脚本：

1. 在 Configuration Manager 控制台中，单击“管理”。
2. 在“管理”工作区中，展开“站点配置”，然后单击“站点”。
3. 在站点列表中，选择你的站点，然后在“主页”选项卡的“站点”组中，单击“层次结构设置”。
4. 在“层次结构设置属性”对话框的“常规”选项卡中，清除“不允许脚本创建者批准他们自己的脚本”复选框。


### <a name="try-it-out"></a>试试看！

#### <a name="import-and-edit-a-script"></a>导入和编辑脚本

1. 在 Configuration Manager 控制台中，单击“软件库”。
2. 在“软件库”工作区中，单击“脚本”。
3. 在“主页”选项卡的“创建”组中，单击“创建脚本”。
4. 在“创建脚本”向导的“脚本”页，配置以下各项：
    - 脚本名称 - 输入脚本的名称。 虽然可以创建具有相同名称的多个脚本，但这会让你难以在 Configuration Manager 控制台中查找所需的脚本。
    - 脚本语言 - 目前，仅支持“PowerShell”脚本。
    - 导入 - 将 PowerShell 脚本导入到控制台。 该脚本将在“脚本”字段中显示。
    - 清除 - 从“脚本”字段中删除当前脚本。
    - 脚本 - 显示当前导入的脚本。 你可以在此字段中根据需要编辑脚本。
5. 完成向导。 新脚本将显示在“脚本”列表，且状态显示为“正等待审批”。 在客户端设备上运行此脚本之前，必须先批准它。


#### <a name="approve-or-deny-a-script"></a>批准或拒绝脚本



在可以运行脚本之前，必须先通过审批。 批准脚本：

1. 在 Configuration Manager 控制台中，单击“软件库”。
2. 在“软件库”工作区中，单击“脚本”。
3. 在“脚本”列表中，选择想要批准或拒绝的脚本，然后在“主页”选项卡“脚本”组中，单击“批准/拒绝”。
4. 在“批准或拒绝脚本”对话框中，“批准”或“拒绝”脚本，并根据需要输入有关你决定的批注。 如果拒绝脚本，它将无法在客户端设备上运行。
5. 完成向导。 在“脚本”列表，你将看到“批准状态”列中发生的变化，具体要取决于你进行的操作。

#### <a name="run-a-script"></a>运行脚本

脚本批准后，它即可在你选择的集合上运行。

1. 在 Configuration Manager 控制台中，单击“资产和符合性”。
2. 在“资产和符合性”工作区中，单击“设备集合”。
3. 在“设备集合”列表中，单击要在其中运行脚本的设备集合。
3. 在“主页”选项卡的“所有系统”组中，单击“运行脚本”。
4. 在“运行脚本”向导的“脚本”页，从列表中选择一个脚本。 仅显示已批准的脚本。 单击“下一步”，然后完成向导。

#### <a name="monitor-a-script"></a>监视脚本

在客户端设备中运行脚本后，使用此过程来监视操作成功与否。

1. 在 Configuration Manager 控制台中，单击“监视”。
2. 在“监视”工作区中，单击“脚本结果”。
3. 在“脚本结果”列表中，可以查看在客户端设备上运行的每个脚本的结果。 脚本退出代码“0”，通常表示脚本已成功运行。

## <a name="pxe-network-boot-support-for-ipv6"></a>PXE 网络启动对 IPv6 的支持
<!-- 1269793 -->
你现在可以启用对 IPv6 的 PXE 网络启动支持，以启动任务序列操作系统部署。 当你使用此设置时，启用 PXE 的分发点将支持 IPv4 和 IPv6。 此选项不需要 WDS，并且存在的话，将会停止 WDS。

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>启用 PXE 启动对 IPv6 的支持
使用以下过程来启用 PXE 的 IPv6 支持选项。

1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “分发点”，然后单击“属性”，获得启用 PXE 的分发点。
2. 在“PXE”选项卡上，选择“支持 IPv6”，以启用 PXE 的 IPv6 支持。

## <a name="manage-microsoft-surface-driver-updates"></a>管理 Microsoft Surface 驱动程序更新
<!-- 1098490 -->
你现在可以使用 Configuration Manager 来管理 Microsoft Surface 驱动程序更新。

### <a name="prerequisites"></a>先决条件
所有软件更新点都必须运行 Windows Server 2016。

### <a name="try-it-out"></a>试试看！
请尝试完成以下任务，然后从功能区的“主页”选项卡向我们发送“反馈”，让我们了解它的工作状况：
1. 为 Microsoft Surface 驱动程序启用同步。 使用[配置分类和产品](/sccm/sum/get-started/configure-classifications-and-products)中的过程，并选择“分类”选项卡上的“包括 Microsoft Surface 驱动程序和固件更新”，以启用 Surface 驱动程序。
2. [同步 Microsoft Surface 驱动程序](/sccm/sum/get-started/synchronize-software-updates.md)。
3. [部署同步的 Microsoft Surface 驱动程序](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>配置 Windows Update for Business 延迟策略
<!-- 1290890 -->
现在，你可以针对 Windows 10 功能更新或直接由 Windows Update for Business 托管的 Windows 10 设备的质量更新，配置延迟策略。 你可以在“软件库” > “Windows 10 维护服务”下方的新“Windows Update for Business 策略”节点中管理延迟策略。

### <a name="prerequisites"></a>先决条件
由 Windows Update for Business 托管的 Windows 10 设备必须具有 Internet 连接。

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>创建 Windows Update for Business 延迟策略
1. 在“软件库” > “Windows 10 维护服务” > “Windows Update for Business 策略”中
2. 在“主页”选项卡的“创建”组中，选择“创建 Windows Update for Business 策略”，以打开“创建 Windows Update for Business 策略向导”。
3. 在“常规”页上，提供策略的名称和描述。
4. 在“延迟策略”页上，配置是否要延迟或暂停功能更新。    
    功能更新通常是针对 Windows 的新增功能。 在配置“分支就绪级别”设置后，你可以根据其可用性定义是否要延迟从 Microsoft 接收功能更新以及延迟时长。
    - 分支就绪级别：设置设备将为其接收 Windows 更新的分支（Current Branch 或 Current Branch for Business）。
    - 延迟期(天)：指定功能更新将被延迟的天数。 你可以自更新发布之日起，在 180 天内延迟接收这些功能更新。
    - 暂停功能更新启动：选择是否要暂停设备接收功能更新，暂停时间为自暂停更新之日起的 60 天内。 在设置的最大天数过后，暂停功能将自动过期，并且设备将扫描 Windows 更新以获取适用的更新。 在此扫描之后，你可以再次暂停更新。 通过清除该复选框，可以取消暂停功能更新。   
5. 选择是否要延迟或暂停质量更新。     
    质量更新通常是对现有 Windows 功能的修复和改进，通常会在每个月的第一个星期二发布，虽然 Microsoft 可以在任何时候发布。 你可以根据其可用性定义是否要延迟接收质量更新，以及它的延迟时长。
    - 延迟期(天)：指定功能更新将被延迟的天数。 你可以自更新发布之日起，在 180 天内延迟接收这些功能更新。
    - 暂停质量更新启动：选择是否要暂停设备接收质量更新，暂停时间为自暂停更新之日起的 35 天内。 在设置的最大天数过后，暂停功能将自动过期，并且设备将扫描 Windows 更新以获取适用的更新。 在此扫描之后，你可以再次暂停更新。 通过清除该复选框，可以取消暂停质量更新。
6. 选择“安装来自其他 Microsoft 产品的更新”，可启用使延迟设置适用于 Microsoft 更新以及 Windows 更新的组策略设置。
7. 选择“包括 Windows 更新中的驱动程序”，可自动更新 Windows 更新中的驱动程序。 如果清除此设置，则不会从 Windows 更新下载驱动程序更新。
8. 完成向导以创建新的延迟策略。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>部署 Windows Update for Business 延迟策略
1. 在“软件库” > “Windows 10 维护服务” > “Windows Update for Business 策略”中
2. 在“主页”选项卡的“部署”组中，选择“部署 Windows Update for Business 策略”。
3. 配置下列设置：
    - 要部署的配置策略：选择要部署的 Windows Update for Business 策略。
    - 集合：单击“浏览”，可选择要在其中部署策略的集合。
    - 在支持时修正非符合性规则：选择该选项，可自动修正 Windows Management Instrumentation (WMI)、注册表、脚本和 Configuration Manager 所注册移动设备的所有设置的任何非符合性规则。
    - 允许维护时段外的修正：如果已为你向其部署策略的集合配置了维护时段，启用此选项可以让符合性设置在维护时段外修正值。 有关维护时段的详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。
    - 生成警报：配置一个警报，在指定日期和时间之前配置基线符合性小于指定百分比时，生成一个警报。 你也可以指定是否希望将警报发送到 System Center Operations Manager。
    - 随机延迟(小时)：指定延迟时段，以免网络设备注册服务的处理负荷过重。 默认值为 64 小时。
    - 计划：指定在客户端计算机上对部署的配置文件进行评估所依据的符合性评估计划。 该计划可以是简单计划或自定义计划。 当用户登录时，客户端计算机将评估配置文件。
4.  完成向导以部署配置文件。



## <a name="support-for-entrust-certification-authorities"></a>支持 Entrust 证书颁发机构
<!-- 1350740 -->
现在，Configuration Manager 可支持 Entrust 证书颁发机构；这使得 PFX 证书可传送到在 Microsoft Intune 中注册的设备。

在 Configuration Manager 中添加“证书注册点”角色时，你可以将 Entrust 配置为证书颁发机构。 在添加颁发 PFX 证书的新证书配置文件时，你可以选择 Microsoft 或 Entrust 证书颁发机构。

已知问题：在 Technical Preview 1706 中，没有为 Microsoft 证书颁发机构颁发 PFX 证书。 这并不会影响导入的 PFX 证书或 SCEP 配置文件。


## <a name="cisco-ipsec-support-for-macos-vpn-profiles"></a>macOS VPN 配置文件的 Cisco (IPsec) 支持
<!-- 1321367 -->

你可以使用 Cisco (IPsec) 作为连接类型创建 macOS VPN 配置文件。 有关详细信息，请参阅[创建 VPN 配置文件](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)。


## <a name="new-windows-configuration-item-settings"></a>新 Windows 配置项设置
<!-- 1354715 -->

在此版本中，我们添加了以下你可以在 Windows 配置项中使用的新设置：

### <a name="password"></a>Password

- **设备加密**

### <a name="device"></a>设备

- **修改区域设置(仅限桌面设备)**
- **电源和睡眠设置修改**
- **语言设置修改**
- **系统时间修改**
- **设备名称修改**

### <a name="store"></a>应用商店

- **自动更新来自应用商店的应用**
- **仅使用专用应用商店**
- **启动来自应用商店的应用**

### <a name="microsoft-edge"></a>Microsoft Edge

- **阻止关于标志的访问**
- **SmartScreen 提示重写**
- **文件的 SmartScreen 提示替代**
- **WebRTC localhost IP 地址**
- **默认搜索引擎**
- **OpenSearch XML URL**
- **主页(仅限桌面)**

有关符合性设置的详细信息，请参阅[确保设备符合性](/sccm/compliance/understand/ensure-device-compliance)。


## <a name="new-device-compliance-policy-rules"></a>新设备符合性策略规则

* **所需的密码类型**。 指定用户是否必须创建字母数字密码或数字密码。 对于字母数字密码，你还可以指定密码必须包含的字符集的最小个数。 有以下四个字符集：小写字母、大写字母、符号和数字。

    **在以下设备上受支持：**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **在设备上阻止进行 USB 调试**。 无需配置此设置，因为已在 Android for Work 的设备上禁用 USB 调试。

    **在以下设备上受支持：**
    * Android 4.0+
    * Samsung KNOX 标准版 4.0+
<br></br>
* **阻止来自未知源的应用**。 要求设备阻止安装来自未知源的应用。 无需配置此设置，因为 Android for Work 设备始终限制来自未知源的安装。

    **在以下设备上受支持：**
    * Android 4.0+
    * Samsung KNOX 标准版 4.0+
<br></br>
* **要求对应用进行威胁扫描**。 此设置指定在设备上启用的“验证”应用功能。

    **在以下设备上受支持：**
    * Android 4.2 到 4.4
    * Samsung KNOX 标准版 4.0+

请参阅[创建和部署设备符合性策略](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy)，尝试新的设备符合性规则。

## <a name="new-mobile-application-management-policy-settings"></a>新移动应用程序管理策略设置
从此版本开始，你可以使用三个新的移动应用程序管理 (MAM) 策略设置：

- 阻止屏幕捕获(仅限 Android 设备)：指定在使用该应用时，阻止设备的屏幕捕获功能。

- 禁用联系人同步：阻止应用将数据保存到设备上的本机“联系人”应用。

- 禁用打印：阻止应用打印工作或学校数据。

请参阅[使用 Configuration Manager 中的应用保护策略来保护应用](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)，尝试新的应用保护策略设置。

## <a name="android-and-ios-enrollment-restrictions"></a>Android 和 iOS 注册限制
<!-- 1290826 -->
从此版本开始，管理员现在可以指定用户不能在其混合环境中注册个人 Android 或 iOS 设备。 这可让你将注册的设备限制为预先声明的公司所有设备，或仅限注册了“设备注册计划”的 iOS 设备。

### <a name="try-it-out"></a>试试看
1. 在“管理”工作区中的 Configuration Manager 控制台中，转到“云服务” > “Microsoft Intune 订阅”。
2. 在“主页”选项卡的“订阅”组中，选择“配置平台”，然后选择“Android”或“iOS”。
3. 选择“阻止个人所有的设备”。

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>针对复制粘贴的 Android for Work 应用程序管理策略
针对“允许工作和个人配置文件间的数据共享”选项，我们已更新了 Android for Work 配置项的设置说明。

|在 Technical Preview 1706 之前 | 新选项名称 | 行为|
|-|-|-|
|阻止任何跨边界的共享| 默认共享限制| 工作到个人：默认（期望在所有版本上阻止） <br>个人到工作：默认（在 6.x+ 上允许，在 5.x 上阻止）|
|无限制|   个人配置文件中的应用可以处理来自工作配置文件的共享请求| 工作到个人：允许  <br>个人到工作：允许|
|工作配置文件中的应用可以处理来自个人配置文件的共享请求 |工作配置文件中的应用可以处理来自个人配置文件的共享请求 |工作到个人：默认<br>个人到工作：允许<br>（仅在个人到工作阻止的 5.x 上可用）|

这些选项都不直接阻止复制粘贴行为。 我们对 1704 版本中的服务和公司门户应用添加了自定义设置，可以对其进行配置以防止复制粘贴。 这可以通过自定义 URI 来设置。

-   OMA-URI:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   值类型：布尔

设置 DisallowCrossProfileCopyPaste，以确实阻止 Android for Work 个人和工作配置文件之间的复制粘贴行为。

### <a name="try-it-out"></a>试试看
1. 在 Configuration Manager 控制台中，选择“资产和符合性” > “概述” > “符合性设置” > “配置项”。
2. 选择“创建”以创建一个新的配置项，并指定“名称”和“Android for Work”。
3. 在设备设置组中进行配置，选择“工作配置文件”，然后选择“下一步”。
4. 选择“允许在工作和个人配置文件之间共享数据”，然后完成向导。

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>用于条件访问的符合性策略的“设备运行状况证明”评估
<!-- 1097546 -->
从此版本开始，你可以将“设备运行状况证明”状态用作对公司资源进行条件性访问的符合性策略规则。

### <a name="try-it-out"></a>试试看
选择一个“设备运行状况证明”规则作为符合性策略评估的一部分。
