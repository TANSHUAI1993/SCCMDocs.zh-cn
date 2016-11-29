---
title: "将客户端分配给站点 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中将客户端分配给站点。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3540b178bf8d7c6473b94a7300578ed7cf0dce29

---
# <a name="how-to-assign-clients-to-a-site-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中将客户端分配到一个站点

*适用范围：System Center Configuration Manager (Current Branch)*

安装 System Center Configuration Manager 客户端后，它必须加入 Configuration Manager 主站点才能进行管理。 客户端加入的站点称为其分配的站点。 无法将客户端分配给管理中心站点或辅助站点。  

 分配过程在成功安装客户端之后执行，并确定管理客户端计算机的站点。 在 Configuration Manager 注册过程中安装移动设备客户端时，此过程始终会将移动设备自动分配给站点。 在计算机上安装客户端时，也可以将客户端分配给站点，或者只安装客户端而不将其分配给站点。 但是，如果安装了客户端但未分配客户端，则站点分配成功之前，客户端不受管理。  

 为了分配客户端计算机，你可以将客户端直接分配到站点，或者可以使用自动站点分配（客户端基于其当前网络位置或为层次结构配置的回退站点自动查找合适的站点）。  

> [!NOTE]  
>  始终从相同版本的 Configuration Manager 向站点分配客户端。 避免将较新版本的 Configuration Manager 客户端分配给较旧版本的站点。   如有必要，请将主站点更新为与使用的客户端相同的 Configuration Manager 版本。  

 客户端分配到站点之后，将保持分配到该站点，即使客户端更改了其 IP 地址并漫游到其他站点。 仅管理员可以在以后将客户端手动分配到其他站点或删除客户端分配。  

> [!WARNING]  
>  如果在启用写入筛选器时在 Windows Embedded 设备上分配客户端，则分配给站点的客户端例外。 如果在分配客户端之前未首先禁用写入筛选器，则在下次重启设备时客户端的站点分配状态将恢复为其原始状态。  
>   
>  例如，为自动站点分配配置了客户端，则客户端在启动时将重新分配并且可能会分配给其他站点。 如果没有为自动站点分配配置客户端，但客户端需要手动站点分配，则必须先在启动之后手动重新分配客户端，然后才可以使用 Configuration Manager 管理此客户端。  
>   
>  要避免此行为，请在嵌入式设备上分配客户端之前禁用写入筛选器，然后在验证站点分配成功之后启用写入筛选器。  

 如果客户端无法分配到站点，则客户端软件仍然会安装，但是将不受管理。 如果客户端已安装但尚未分配到站点，或已分配到站点但不能与管理点通信，则客户端会被视为不受管理。  

##  <a name="a-namebkmkmanualassignmenta-using-manual-site-assignment-for-computers"></a><a name="BKMK_ManualAssignment"></a>对计算机使用手动站点分配  
 可以使用下面两种方法将客户端计算机手动分配到站点：  

-   使用指定站点代码的客户端安装属性。  

-   在控制面板内的“Configuration Manager” 中，指定站点代码。  

> [!NOTE]  
>  如果将客户端计算机手动分配到不存在的 Configuration Manager 站点代码，则站点分配将失败。 客户端仍然会安装，但是在分配到有效的 Configuration Manager 站点之前不受管理。  

##  <a name="a-namebkmkautomaticassignmenta-using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a>对计算机使用自动站点分配  
 在客户端部署过程中，或者当你在控制面板内揅onfiguration Manager 属性?  的“高级”  选项卡中单击“发现站点”  时，可能会发生自动站点分配。 Configuration Manager 客户端会将其自己的网络位置与在 Configuration Manager 层次结构中配置的边界进行比较。 如果客户端的网络位置在为站点分配启用的边界组内，或者为回退站点配置了层次结构，则会将客户端自动分配给该站点，你不必指定站点代码。  

 你可以使用下列一项或多项来配置边界：  

-   IP 子网  

-   Active Directory 站点  

-   IP v6 前缀  

-   IP 地址范围  

> [!NOTE]  
>  如果 Configuration Manager 客户端有多个网络适配器（可能是一个 LAN 网络适配器和一个拨号调制解调器）并因此具有多个 IP 地址，则用于评估客户端站点分配的 IP 地址是不确定的。  

 有关如何为站点分配配置边界组以及如何为自动站点分配配置回退站点的信息，请参阅 [Define site boundaries and boundary groups for System Center Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。  

 使用自动站点分配的 Configuration Manager 客户端会尝试查找发布到 Active Directory 域服务的站点边界组。 如果此方法失败（例如，没有为 Configuration Manager 扩展 Active Directory 架构，或者客户端是工作组计算机），则客户端可以从管理点中查找边界组信息。  

 你可以指定管理点以供客户端计算机在安装时使用，或者客户端可以使用 DNS 发布或 WINS 定位管理点。  

 如果客户端找不到与包含其网络位置的边界组关联的站点，并且层次结构没有回退站点，则客户端每 10 分钟会重试一次，直到能够分配给站点为止。  

 如果应用了以下任何方案，Configuration Manager 客户端计算机将无法自动分配到站点，相反，必须进行手动分配：  

-   客户端当前已分配到站点。  

-   客户端在 Internet 上或者被配置为仅 Internet 客户端。  

-   客户端的网络位置不在 Configuration Manager 层次结构中配置的其中一个边界组之内，并且层次结构没有回退站点。  

##  <a name="a-namebkmksitecompatibilitya-completing-site-assignment-by-checking-site-compatibility"></a><a name="BKMK_SiteCompatibility"></a>通过检查站点兼容性完成站点分配  
 在客户端找到分配的站点后，将检查客户端的版本和操作系统以确保 Configuration Manager 站点可以管理该客户端。 例如，Configuration Manager 无法管理 Configuration Manager 2007 客户端、System Center 2012 Configuration Manager 客户端或正在运行 Windows 2000 的客户端。  

 然而，如果你将运行 Windows 2000 的客户端分配给 Configuration Manager 站点，则站点分配将失败；当你将 Configuration Manager 2007 客户端或 System Center 2012 Configuration Manager 客户端分配给 Configuration Manager (Current Branch) 站点时，站点分配将继续支持自动客户端升级。 但是，在较旧一代客户端升级到 Configuration Manager (Current Branch) 客户端之前，Configuration Manager 无法使用客户端设置、应用程序或软件更新来管理此客户端。  

> [!NOTE]  
>  若要支持将 Configuration Manager 2007 或 System Center 2012 Configuration Manager 客户端的站点分配到 Configuration Manager (Current Branch) 站点，则必须为层次结构配置自动客户端升级。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

 Configuration Manager 还会检查是否已将 Configuration Manager (Current Branch) 客户端分配给支持它的站点。 从以前版本的 Configuration Manager 进行迁移，可能会在迁移期间出现以下情况。  

-   情况：你使用了自动站点分配，并且边界与 Configuration Manager 以前版本中所定义的边界重叠。  

     在这种情况下，客户端会自动尝试查找 Configuration Manager (Current Branch) 站点。  

     客户端首先检查 Active Directory 域服务，如果它找到发布的 Configuration Manager (Current Branch) 站点，则站点分配将成功。 如果此操作失败（例如，没有发布 Configuration Manager (Current Branch) 站点，或者计算机是工作组客户端），则客户端会从其分配的管理点中检查站点信息。  

    > [!NOTE]  
    >  可通过使用 Client.msi 属性 **SMSMP=&lt;server_name>** 在客户端安装期间将管理点分配给客户端。  

     如果这些方法都失败，则站点分配将失败，你必须手动分配客户端。  

-   情况：你使用特定站点代码（而不是自动站点分配）分配了 Configuration Manager (Current Branch) 客户端，并且错误地为早于 System Center 2012 R2 Configuration Manager 的 Configuration Manager 版本指定了站点代码。  

     在这种情况下，站点分配将失败，必须手动将客户端重新分配给 Configuration Manager (Current Branch) 站点。  

 站点兼容性检查需要下列条件之一：  

-   客户端可以访问发布到 Active Directory 域服务的站点信息。  

-   客户端可以与站点中的管理点通信。  

 如果站点兼容性检查无法成功完成，则在再次运行站点兼容性检查并成功完成之前，站点分配将失败，并且客户端将保持不受管理。  

 执行站点兼容性检查的例外情况是为基于 Internet 的管理点配置了客户端时。 在这种情况下，不进行站点兼容性检查。 如果将客户端分配到包含基于 Internet 的站点系统的站点，并指定基于 Internet 的管理点，请确保将客户端分配到正确的站点。 如果错误地将客户端分配到 Configuration Manager 2007 站点、System Center 2012 Configuration Manager 站点或分配到不具有基于 Internet 的站点系统角色的 Configuration Manager 站点，客户端将不受管理。  

##  <a name="a-namebkmklocatingmpsa-locating-management-points"></a><a name="BKMK_LocatingMPs"></a>定位管理点  
 将客户端成功分配给站点之后，它将定位站点中的管理点。  

 客户端计算机会下载它们可以连接到的站点中管理点的列表。 每当客户端重启、每 25 小时，以及在客户端检测到网络更改（如计算机在网络上先断开然后重新连接）或收到新 IP 地址的情况下，会发生此过程。 此列表包含 Intranet 上的管理点，并指明管理点是通过 HTTP 还是 HTTPS 接受客户端连接。 当客户端计算机在 Internet 上并且客户端仍没有管理点列表时，它会连接到指定的基于 Internet 的管理点以获取管理点的列表。 当客户端具有其分配的站点的管理点列表时，它会选择一个要连接到的管理点：  

-   当客户端在 Intranet 并且具有可以使用的有效 PKI 证书时，客户端会在选择 HTTP 管理点之前优先选择 HTTPS 管理点。 然后基于管理点的林成员身份查找最近的管理点。  

-   当客户端在 Internet 上时，它会不确定地选择基于 Internet 的管理点之一。  

 Configuration Manager 注册的移动设备客户端只连接到其分配的站点中的一个管理点，决不会连接到辅助站点中的管理点。 这些客户端始终通过 HTTPS 进行连接，并且管理点必须配置为通过 Internet 接受客户端连接。 当主站点中的移动设备客户端有多个管理点时，Configuration Manager 会在分配过程中不确定地选择其中一个管理点，并且移动设备客户端会继续使用相同的管理点。  

 当客户端从其站点中的管理点下载了客户端策略后，该客户端将随即成为被管理的客户端。  

##  <a name="a-namebkmkdownloadsitesettingsa-downloading-site-settings"></a><a name="BKMK_DownloadSiteSettings"></a>下载站点设置  
 在站点分配成功并且客户端找到管理点之后，使用 Active Directory 域服务检查其站点兼容性的客户端计算机将下载其分配的站点的客户端相关站点设置。 这些设置包括客户端证书选择条件、是否使用证书吊销列表以及客户端请求端口号。 客户端将继续定期检查这些设置。  

 当客户端计算机无法从 Active Directory 域服务获取站点设置时，它们会从其管理点下载这些设置。 客户端计算机也可以通过使用客户端请求在进行安装时获取站点设置，或者你可以使用 CCMSetup.exe 和客户端安装属性手动指定站点设置。 有关客户端安装属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

##  <a name="a-namebkmkdownloadclientsettingsa-downloading-client-settings"></a><a name="BKMK_DownloadClientSettings"></a>下载客户端设置  
 所有客户端均下载默认客户端设置策略或任何合适的自定义客户端设置策略。 软件中心依赖于 Windows 计算机的这些客户端配置策略，并且将通知用户在下载此配置信息之前软件中心无法成功运行。 根据配置的客户端设置，初次下载客户端设置可能需要些时间，并且在此过程完成之前某些客户端管理任务可能无法运行。  

##  <a name="a-namebkmkverifyassignmenta-verifying-site-assignment"></a><a name="BKMK_VerifyAssignment"></a>验证站点分配  
 可以使用下面任何一种方法验证站点分配是否成功：  

-   对于 Windows 计算机上的客户端，使用控制面板中的 Configuration Manager 并验证站点代码是否正确显示在“站点”选项卡中。  

-   对于客户端计算机，请在“资产和符合性”  工作区中使用“设备”  节点验证计算机是否在“客户端”  列中显示“是”  ，并且是否在“站点代码”  列中显示正确的主站点代码。  

-   对于移动设备客户端，请在“资产和符合性”  工作区中使用“所有移动设备”  集合验证移动设备是否在“客户端”  列中显示“是”  ，并且是否在“站点代码”  列中显示正确的主站点代码。  

-   使用客户端分配和移动设备注册的报表。  

-   对于客户端计算机，请使用客户端上的 LocationServices.log 文件。  

##  <a name="a-namebkmkroaminga-roaming-to-other-sites"></a><a name="BKMK_Roaming"></a>漫游到其他站点  
 如果将 Intranet 上的客户端计算机分配给主站点，但更改其网络位置以便其在为另一个站点配置的边界组内，则客户端计算机已漫游到另一个站点。 如果此站点是分配的站点的辅助站点，则客户端可以使用辅助站点中的管理点以下载客户端策略以及上载客户端数据，这会避免通过潜在的慢速网络发送此数据。 但是，如果这些客户端漫游到另一个主站点或辅助站点（不是其分配的站点的子站点）的边界中，则这些客户端始终使用其分配的站点中的管理点下载客户端策略以及将数据上载到其站点。  

 漫游到其他站点（所有主站点和所有辅助站点）的这些客户端计算机始终可以将其他站点中的管理点用于内容位置请求。 当前站点中的管理点可以为客户端提供具有客户端所请求内容的分发点的列表。  

 对于为仅通过 Internet 进行客户端管理而配置的客户端计算机，以及对于 Configuration Manager 注册的 Mac 计算机和移动设备，这些客户端仅与为它们分配的站点中的管理点通信。 这些客户端从来不会与辅助站点中的管理点或者其他主站点中的管理点通信。  



<!--HONumber=Nov16_HO1-->


