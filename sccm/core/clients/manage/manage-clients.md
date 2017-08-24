---
title: "管理客户端 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中管理客户端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3a86924b2e5db3ac16eeda78b95ae6747ffd656f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理客户端

*适用范围：System Center Configuration Manager (Current Branch)*

安装了 System Center Configuration Manager 客户端并将其成功分配到 Configuration Manager 站点后，将在“设备”节点的“资产和符合性”工作区中，以及在“设备集合”节点的一个或多个集合中看到该设备。 选择设备或集合时，可执行管理操作。 但是，也可以使用其他方式管理客户端，这可能涉及控制台中的其他工作区或不使用 Configuration Manager 控制台的任务。  

> [!NOTE]  
>  Configuration Manager 客户端可能已安装但未显示在 Configuration Manager 控制台中。 如果尚未将客户端成功分配到站点，或者必须刷新控制台或集合成员身份已更新，则可能发生此情况。  
>   
>  此外，在未安装 Configuration Manager 客户端时，设备也可能显示在控制台中。 如果发现了设备，但未安装和分配 Configuration Manager 客户端，则可能发生此情况。 通过使用 Exchange Server 连接器管理的移动设备，以及通过 Microsoft Intune 注册的设备不会安装 Configuration Manager 客户端。  
>   
>  使用 Configuration Manager 控制台中的“客户端”列来确定是否安装了 Configuration Manager 客户端，以便可以从 Configuration Manager 控制台对其进行管理。  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> 通过“设备”节点管理客户端  

请注意：其中某些选项可能不可用，具体取决于设备类型。  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” >  “设备”。  

3.  选择一台或多台设备，然后从功能区中选择或通过右键单击设备来选择其中一个客户端管理任务：  

    -   **管理用户设备相关性信息**  

         配置用户和设备之间的关联，以便高效地向用户部署软件。  

         请参阅[在 System Center Configuration Manager 中将用户和设备与用户设备相关性相链接](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **将设备添加到新集合或现有集合**  

         使用直接规则向集合添加设备。  
         
    -   **通过使用客户端请求向导来安装和重新安装客户端**  

         安装和重新安装 Configuration Manager 客户端，以便对其进行修复或者在运行 Windows 的计算机上对其进行重新配置。 包括站点配置选项以及为客户端请求安装设置的 client.msi 属性。  

        > [!TIP]  
        >  可通过多种不同的方式来安装（和重新安装）Configuration Manager 客户端。 尽管客户端请求向导提供一种方便的客户端安装方法（因为你可从控制台中运行它），但此方法有许多依赖关系，并且不适合于所有环境。 有关依赖关系的详细信息，请参阅[在 System Center Configuration Manager 中将客户端部署到 Windows 计算机的先决条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)。 有关其他客户端安装方法的详细信息，请参阅 [System Center Configuration Manager 中的客户端安装方法](../../../core/clients/deploy/plan/client-installation-methods.md)。  

         请参阅 [如何使用客户端请求安装 Configuration Manager 客户端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。  

    -   **重新分配站点**  

         将一个或多个客户端（包括被管理的移动设备）重新分配到层次结构中的另一个主站点。 可以单独重新分配客户端，也可以选择多个客户端并成批重新分配到新站点。  

    -   **以远程方式管理客户端**  

         你可以运行资源浏览器来查看 Windows 客户端中的硬件和软件清单信息，并通过使用远程控制、远程协助或远程桌面对其进行远程管理。  

         请参阅[如何使用资源浏览器来查看 System Center Configuration Manager 中的硬件清单](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)和[如何使用资源浏览器来查看 System Center Configuration Manager 中的软件清单](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

         请参阅[如何使用 System Center Configuration Manager 远程管理 Windows 客户端计算机](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)。  

    -   **批准客户端**  

         客户端使用 HTTP 和自签名证书与站点系统通信时，必须批准这些客户端以将其标识为受信任计算机。 默认情况下，站点配置会自动批准同一 Active Directory 林和受信任林中的客户端，这样你就不必手动批准每个客户端。 但是，你必须手动批准你信任的工作组计算机以及你信任但未获批准的任何其他计算机。  

        > [!WARNING]  
        >  尽管某些管理功能可能适合于未批准的客户端，但 Configuration Manager 不支持这种情况。  

         不必批准始终使用 HTTPS 与站点系统通信的客户端，或在通过 HTTP 与站点系统通信时使用 PKI 证书的客户端。 这些客户端通过使用 PKI 证书建立信任。  

    -   **阻止或解除阻止客户端**  

         阻止不再信任的客户端，以防止该客户端接收客户端策略并防止 Configuration Manager 站点系统与之通信。  

        > [!WARNING]  
        >  阻止客户端的操作只会阻止从客户端到 Configuration Manager 站点系统的通信，而不会阻止与其他设备的通信。 此外，当客户端通过使用 HTTP（而不是 HTTPS）与站点系统通信时，还有一些安全限制。  

         可取消阻止已阻止的客户端。 但是，如果你在阻止了为 AMT 设置的基于 Intel AMT 的计算机后取消阻止该计算机，你必须执行其他步骤，然后才能再次在带外管理该计算机。  

         请参阅[确定是否在 System Center Configuration Manager 中阻止客户端](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)。  

    -   **清除所需的 PXE 部署**  

         为计算机重新部署所需的 PXE 部署。  

         请参阅[使用 PXE 与 System Center Configuration Manager 一起通过网络部署 Windows](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

    -   **管理客户端属性**  

         查看发现数据和针对客户端的部署。 也可以配置任务序列用于将操作系统部署到设备的变量。  

    -   **删除客户端**  

        > [!WARNING]  
        >  如果要卸载 Configuration Manager 客户端或将其从集合中移除，请不要删除客户端。  

         “删除”操作会从 Configuration Manager 数据库手动删除客户端记录，除非用于故障排除方案，否则通常不应使用此操作。 如果删除客户端记录，而客户端仍处于已安装状态并与 Configuration Manager 通信，则检测信号发现会重新创建客户端记录，并且该记录会重新出现在 Configuration Manager 控制台中，尽管客户端历史记录和任何以前的关联将丢失。  

        > [!NOTE]  
        >  删除通过 Configuration Manager 注册的移动设备客户端时，此操作还会吊销颁发给移动设备的 PKI 证书，并且管理点随后会拒绝此证书（即使 IIS 未检查 CRL）。 在删除这些客户端时，不会吊销移动设备旧客户端上的证书。  

         要卸载客户端，请参阅 [卸载 Configuration Manager 客户端](#BKMK_UninstalClient)。  

         要将客户端分配到一个新的主站点，请参阅[如何在 System Center Configuration Manager 中将客户端分配到一个站点](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

         要从集合中删除客户端，请重新配置集合属性。 请参阅[如何在 System Center Configuration Manager 中管理集合](../../../core/clients/manage/collections/manage-collections.md)。  

    -   **擦除移动设备**  

         你可以擦除支持擦除命令的移动设备。  

         此操作会永久删除移动设备上的所有数据，包括个人设置和个人数据。 通常，此操作会将移动设备重置回出厂默认值。 移动设备不再受信任（例如，丢失或被盗）时将其擦除。  

        > [!TIP]  
        >  请检查制造商的文档以了解有关移动设备如何处理远程擦除命令的详细信息。  

         移动设备收到擦除命令之前通常会有延迟：  

        -   如果移动设备是通过 Configuration Manager 或 Microsoft Intune 注册的，则客户端会在下载客户端策略时收到命令。  

        -   如果通过 Exchange Server 连接器管理移动设备，则移动设备会在其与 Exchange 同步时收到命令。  

         可使用“擦除状态” 列来监视设备何时收到擦除命令。 设备将擦除确认发送到 Configuration Manager 之前，可以取消擦除命令。  

    -   **停用移动设备**  

         只有通过 Intune 或本地移动设备管理注册的移动设备才支持“停用”选项。  

         有关详细信息，请参阅 [使用 System Center Configuration Manager 的远程擦除、远程锁定或密码重置功能帮助保护数据](../../../mdm/deploy-use/wipe-lock-reset-devices.md)。  

    -   **更改设备的所有权**  

         如果设备未加入域并且未安装 Configuration Manager 客户端，则可以将设备的所有权更改为“公司”或“个人”。  

         可在应用程序要求中使用此值来控制部署，以及控制从用户设备中收集的清单数量。  

        可能需要右键单击任意列标题并选择“设备所有者”列，将此列添加到视图中。

         有关详细信息，请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)。  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> 通过“设备集合”节点管理客户端  
  可在“设备”节点中的单台设备或多台设备上执行的许多任务也可在集合上执行。 这会将操作自动应用于集合中的所有合格设备。 请注意：这会生成大量网络数据包，并增加站点服务器上的 CPU 使用率。  

  在执行集合级别客户端管理任务之前，请考虑集合中有多少设备、这些设备是否通过低带宽网络连接进行连接，以及对于所有设备任务将花费多长时间完成。 开始后，无法从控制台中停止任务。  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>通过“设备集合”节点管理客户端  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “设备集合”。  

3.  选择一个集合，然后从功能区中选择或通过右键单击集合来选择下列客户端管理任务之一。 这些客户端管理任务只能在集合级别执行。  

    -   **扫描计算机以查找恶意软件并下载反恶意软件定义文件。**  

         请参阅 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

    -   **部署软件、配置基线和任务序列。**  

         请参阅：  

        -   [在 System Center Configuration Manager 中部署软件更新](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [在 System Center Configuration Manager 中规划和配置符合性设置](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **配置电源管理设置。**  

         请参阅[如何在 System Center Configuration Manager 中创建并应用电源计划](../../../core/clients/manage/power/create-and-apply-power-plans.md)。 电源计划只能用于运行 Windows 的计算机。  

    -   **通知计算机尽快下载策略。**  

         使用客户端通知来通知所选 Windows 客户端，在客户端策略轮询间隔外尽快下载计算机策略。  

         客户端通知任务显示在“监视”  工作区的“客户端操作”  节点中。  

##  <a name="BKMK_ClientCache"></a> 为 Configuration Manager 客户端配置客户端缓存  
客户端缓存会存储客户端安装应用程序和程序时的临时文件。 软件更新也使用客户端缓存，但软件更新不受配置的缓存大小所限，并且将始终尝试下载到缓存。 可在手动安装 Configuration Manager 客户端时、使用客户端请求安装时或在安装客户端之后配置客户端缓存设置，例如大小和位置。

自 Configuration Manager 1606 版开始，可使用 Configuration Manager 控制台中的客户端设置来指定缓存文件夹大小。   

 Configuration Manager 客户端缓存的默认位置为 %*windir*%\ccmcache，默认磁盘空间为 5120 MB。  

> [!IMPORTANT]  
>  不要对用于客户端缓存的文件夹进行加密。 Configuration Manager 无法将内容下载到加密的文件夹。  

### <a name="about-client-cache"></a>关于客户端缓存  

Configuration Manager 客户端会在接收部署之后立即下载所需软件的内容，但会等到部署计划时间之后才会运行。 在计划的时间，Configuration Manager 客户端将检查以确定缓存中是否有内容。 如果内容位于缓存中且版本正确，则客户端会使用该缓存内容。 如果内容的所需版本已更改或者已将内容删除以便为另一个包腾出空间，则会将内容再次下载到缓存。  

如果客户端尝试下载的程序或应用程序内容大小超出缓存的大小，则部署将因缓存大小不足而失败，并且 Configuration Manager 将生成状态消息 ID 10050。 如果以后增加了缓存大小，则会出现以下结果：  

-   对于所需程序：客户端不会自动重试下载内容。 你必须将包和程序重新部署到客户端。  
-   对于所需应用程序：客户端会在下载其客户端策略时自动重试下载内容。  

如果客户端尝试下载的包小于缓存大小，但缓存已满，则所有必需的部署将在下载超时之前或达到缓存空间失败的重试限制之前一直重试，直至缓存空间可用。 如果稍后增加了缓存大小，则 Configuration Manager 客户端将尝试在下一次重试间隔期间再次下载该包。 客户端将每隔四小时尝试下载内容一次，直至尝试 18 次为止。  

在客户端使用了缓存的内容后，将不会自动删除该内容，但会将其在缓存中保留至少一天。 如果将包属性配置为包含将内容保留在客户端缓存中的选项，则客户端不会自动从缓存中删除包内容。 如果客户端缓存空间由最近 24 小时内下载的包占用，并且客户端必须下载新包，你可以增加客户端缓存大小，或选择删除选项以删除保留的缓存内容。  

 使用以下过程在手动客户端安装过程中或在安装客户端之后配置客户端缓存。  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>在使用手动客户端安装来安装客户端时配置客户端缓存  

从安装源位置运行 CCMSetup.exe 命令，并指定所需的以下属性，用空格分隔：  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > 对于版本 1606，请使用 Configuration Manager 控制台中“客户端设置”的可用缓存大小设置而不是 SMSCACHESIZE。 有关详细信息，请参阅[客户端缓存设置](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)。

有关如何使用 CCMSetup.exe 的这些命令行属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>在使用客户端请求安装来安装客户端时配置客户端缓存文件夹  

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”。  

3.  选择相应站点，然后在“主页”选项卡上的“设置”组中，选择“客户端安装设置” > “安装属性”选项卡。  

5.  指定以下属性，并使用空格分隔：  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > 对于版本 1606，请使用 Configuration Manager 控制台中“客户端设置”的可用缓存大小设置而不是 SMSCACHESIZE。 有关详细信息，请参阅[客户端缓存设置](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)。

       有关如何使用 CCMSetup.exe 的这些命令行属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>在客户端计算机上配置客户端缓存文件夹  

1.  在客户端计算机上的控制面板中，导航到“Configuration Manager” ，然后双击以打开属性。  

2.  在“缓存”选项卡上，设置空间和位置属性。 默认位置为 *%windir%*\ccmcache。  

5.  若要删除缓存文件夹中的文件，请选择“删除文件”。  

    > [!NOTE]
    > 
    > 缓存文件夹是常规的 Windows 文件夹，因此可使用脚本、实用工具或 PowerShell cmdlet `Remove-Item` 自动删除文件夹内容。 


### <a name="to-configure-client-cache-size-in-client-settings"></a>在客户端设置中配置客户端缓存大小

从版本 1606 开始，可以在无需重新安装客户端的情况下调整客户端缓存文件夹的大小。 若要执行此操作，请在 Configuration Manager 控制台中使用客户端设置配置客户端缓存大小。  

1. 在 Configuration Manager 控制台中，转到“管理” > “客户端设置”。

2. 双击“默认客户端设置”。
  还可以创建自定义客户端设置，以便更有选择性地应用缓存大小。 有关默认客户端设置和自定义客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../core/clients/deploy/configure-client-settings.md)。

 3. 选择“客户端缓存设置”，并针对“配置客户端缓存大小”选择“是”，然后选择使用“MB”或“磁盘设置的百分比”。 缓存可调整为任何小于最大缓存的大小。

     在下载下一个客户端策略时，Configuration Manager 客户端将使用这些设置配置缓存大小。

##  <a name="BKMK_UninstalClient"></a> 卸载 Configuration Manager 客户端  
 可通过将 **CCMSetup.exe** 与 **/Uninstall** 属性一起使用从计算机卸载 Windows Configuration Manager 客户端软件。 在单独的计算机上从命令提示符运行 CCMSetup.exe，或部署包和程序为计算机集合卸载客户端。  

> [!WARNING]  
>  无法从移动设备中卸载 Configuration Manager 客户端。 如果必须从移动设备中删除 Configuration Manager 客户端，则必须擦除设备，从而删除移动设备上的所有数据。  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>通过命令提示符卸载 Configuration Manager 客户端  

1.  打开 Windows 命令提示符，并将文件夹更改到 CCMSetup.exe 所在的位置。  

2.  键入 **Ccmsetup.exe /uninstall**，然后按   

> [!NOTE]  
>  卸载过程不会在屏幕上显示结果。 要验证客户端卸载是否成功，请检查客户端计算机上 *%windir%\ ccmsetup* 文件夹中的日志文件 **CCMSetup.log**。  

##  <a name="BKMK_ConflictingRecords"></a> 为 Configuration Manager 客户端管理冲突的记录  
 Configuration Manager 使用硬件 ID 来尝试标识可能重复的客户端，并发出有关冲突的记录的警报。 例如，若重新安装计算机，则硬件 ID 将相同，但 Configuration Manager 使用的 GUID 可能已更改。  

 Configuration Manager 能够通过使用计算机帐户的 Windows 身份验证或来自受信任来源的 PKI 证书解决冲突时，会自动解决冲突。 但是，Configuration Manager 无法解决冲突时，它将使用层次结构设置，该设置会在检测到重复的硬件 ID 时自动合并记录（默认设置），或允许你决定何时合并、阻止或创建新客户端记录。 如果决定手动管理重复记录，则必须在 Configuration Manager 控制台中手动解决冲突的记录。  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>更改用于管理冲突的记录的层次结构设置  

1.  在 Configuration Manager 控制台中，选择“管理” > “站点配置” > “站点” > “层次结构设置”
2.  在“客户端批准和冲突的记录”选项卡上，选择“自动解决冲突的记录”或“手动解决冲突的记录”。  

#### <a name="to-manually-resolve-conflicting-records"></a>手动解决冲突的记录  

1.  在 Configuration Manager 控制台中，选择“监视” > “系统状态” > “冲突的记录”。  

3.  选择一个或多个冲突的记录，然后选择“冲突的记录”。  

4.  选择以下选项之一：  

    -   选择“合并”以合并新检测到的记录和现有客户端记录。  

    -   选择“新建” 为冲突的客户端记录创建新记录。  

    -   选择“阻止” 为冲突的客户端记录创建新记录，但将其标记为已阻止。  

## <a name="manage-duplicate-hardware-identifiers"></a>管理重复的硬件标识符
从 Configuration Manager 版本 1610 开始，可以提供 Configuration Manager 为实现 PXE 启动和客户端注册而将忽略的硬件 ID 列表。 这可以帮助解决两个常见问题。

1. 许多新设备（如 Surface Pro 3）不包含板载以太网端口。 为部署操作系统，通常会使用 USB 转以太网适配器来建立有线连接。 但是，出于成本和一般可用性的考虑，这些适配器通常会共享使用。 由于此适配器的 MAC 地址用于标识设备，因此在每次部署之间若无额外的管理员操作，重用适配器就会出现问题。 从版本 1610 开始，可排除此适配器的 MAC 地址，以便在此种情况下重复使用该适配器。
2. 虽然 SMBIOS ID 应该是唯一的硬件标识符，但是某些特殊硬件设备自身具有重复 ID。 尽管不像上述的 USB 转以太网适配器情景那样普遍，但是硬件 ID 列表也可用于解决此问题。

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>添加 Configuration Manager 要忽略的硬件标识符  
1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “站点配置” > “站点”。
2. 在“主页”选项卡上的“站点”组中，选择“层次结构设置”。
3. 在“客户端批准和冲突的记录”选项卡上的“复制硬件标识符”部分，选择“添加”以添加新的硬件标识符。

##  <a name="BKMK_PolicyRetrieval"></a> 为 Configuration Manager 客户端启动策略检索  
 Windows Configuration Manager 客户端按配置为客户端设置的计划下载其客户端策略。 然而，有时可能需要从客户端启动临时策略检索，例如，进行故障排除或测试时。  

可使用以下方法启动策略检索：


- [客户端通知](#initiate-client-policy-retrieval-using-client-notification) 
- [客户端上的“操作”选项卡](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [脚本](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  有关运行 Linux 和 UNIX 的客户端的策略检索的信息，请参阅 [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU)。  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>使用客户端通知启动客户端策略检索  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “设备集合”。  

3.  选择包含要下载策略的计算机的设备集合。 在“主页”选项卡上的“集合”组中，选择“客户端通知” > “下载计算机策略”。  

    > [!NOTE]  
    >  你也可以使用客户端通知为显示在“设备”  节点下的临时集合节点中的一台或多台所选设备启动策略检索。  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>使用 Configuration Manager 客户端上的“操作”选项卡手动启动客户端策略检索  

1.  在计算机的控制面板中选择“Configuration Manager”  。  

2.  在“操作”选项卡上，选择“计算机策略检索和评估周期”以启动计算机策略，然后选择“立即运行”。  

4.  选择“确定”，确认提示。  

5.  为所需的任何其他操作（例如用户客户端设置的“用户策略检索和评估周期”）重复步骤 3 和 4。  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>使用脚本手动启动客户端策略检索  

1.  打开文本编辑器，例如记事本。  

2.  将以下内容复制并粘贴到文件中：  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  以 .vbs 扩展名保存文件。  

4.  在客户端计算机上，使用下列方法之一运行该文件：  

    -   使用 Windows 资源管理器导航到该文件，然后双击脚本文件。  

    -   打开命令提示符，然后键入：**cscript &lt;path\filename.vbs>**。  

5.  在“Windows 脚本宿主”对话框中，选择“确定”。  
