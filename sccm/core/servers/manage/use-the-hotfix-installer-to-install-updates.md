---
title: "修补程序安装程序 | Microsoft Docs"
description: "了解何时以及如何通过 Configuration Manager 的修补程序安装更新。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8ffc7383e895909e6e6c4b8a7875fd5f0df2220e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-hotfix-installer-to-install-updates-for-system-center-configuration-manager"></a>使用修补程序安装程序来安装 System Center Configuration Manager 的更新

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 的某些更新无法从 Microsoft 云服务获取，只能在带外获取。 用于解决特定问题的受限版本修补程序是一个示例。   
必须安装从 Microsoft 接收的更新（或修补程序），并且该更新的文件名是以 **.exe** 扩展名（而非 **update.exe**）结尾时，可使用该修补程序下载所随附的修补程序安装程序，将更新直接安装到 Configuration Manager 站点服务器。  

 如果修补程序文件有 **.update.exe** 文件扩展名，请参阅[使用更新注册工具将修补程序导入 System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)。  

> [!NOTE]  
>  本主题提供有关如何安装更新 System Center Configuration Manager 的修补程序的常规指导。 有关特定更新的详细信息，请参阅 Microsoft 支持上该更新的相应知识库 (KB) 文章。  

##  <a name="bkmk_Overview"></a> Configuration Manager 修补程序概述  
 Configuration Manager 的修补程序类似于其他 Microsoft 产品（例如 SQL Server）的修补程序，包含一个单独的修复程序或一个捆绑包（多个修复程序的汇总），如 Microsoft 知识库文章中所述。  

 单独的更新包含针对特定版本 Configuration Manager 的修补程序的单个重点更新。  
更新捆绑包具有针对 Configuration Manager 特定版本的多个更新。  
不能从更新捆绑中安装单独更新。  

 如果你计划创建部署以在其他计算机上安装更新，则必须在管理中心站点服务器或主站点服务器上安装更新捆绑。  

 运行更新捆绑时将发生以下事件：  

-   它从更新捆绑中提取每个适用组件的更新文件。  

-   启动向导，指导你完成配置更新和更新部署选项的过程。  

-   完成该向导后，在站点服务器上安装捆绑中适用于该站点服务器的更新。  

向导也会创建部署，你可以使用这些部署在其他计算机上安装更新。 你可以使用诸如软件部署包或 Microsoft System Center Updates Publisher 2011 之类受支持的部署方法将更新部署到其他计算机。  

 运行向导时，会在站点服务器上创建一个要与 Updates Publisher 2011 一起使用的 **.cab** 文件。 （可选）你可以将向导配置为创建一个或多个软件部署包。 可以使用这些部署在客户端或 Configuration Manager 控制台等组件上安装更新。 也可以在未运行 Configuration Manager 客户端的计算机上手动安装更新。  

 可以更新 Configuration Manager 中的下列三个组：  

-   Configuration Manager 服务器角色，其中包括：  

    -   管理中心站点  

    -   主站点  

    -   辅助站点  

    -   远程 SMS 提供程序  

-   Configuration Manager 控制台  

-   Configuration Manager 客户端  

> [!NOTE]  
>  **针对站点系统角色的更新**（包括站点数据库更新和基于云的分发点更新）作为针对站点服务器和服务的更新中的一部分，由站点组件管理器安装。  
>   
>  但是，更新请求分发点是由分发管理器而非站点组件管理器维护。  

 Configuration Manager 的每个更新捆绑包都是可自提取的 .exe 文件 (SFX)，此文件包括在 Configuration Manager 的适用组件上安装更新所需的文件。 通常，SFX 文件可能包含下列文件：  

|文件|详细信息|  
|----------|-------------|  
|&lt;Product version\>-QFE-KB&lt;KB article ID\>-&lt;platform\>-&lt;language\>.exe|这是更新文件。 此文件的命令行由 Updatesetup.exe 进行管理。<br /><br /> 例如：<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|此 .msi 包装管理更新捆绑的安装。<br /><br /> 运行更新时，Updatesetup.exe 会检测运行它的计算机的显示语言。 默认情况下，此更新的用户界面是英文。 但是，如果支持显示语言，则会以计算机的本地语言显示用户界面。|  
|License_&lt;language\>.rtf|如果适用，每个更新都会包含支持语言的一个或多个许可证文件。|  
|&lt;Product&updatetype>-&lt;product version\>-&lt;KB article ID\>-&lt;platform\>.msp|如果更新适用于 Configuration Manager 控制台或客户端，则更新捆绑包会包括单独的 Windows Installer 修补 (.msp) 文件。<br /><br /> 例如：<br /><br /> **Configuration Manager 控制台更新：** ConfigMgr1511 AdminUI KB1234567 i386.msp<br /><br /> **客户端更新：**ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

 默认情况下，更新捆绑会将其操作记录到站点服务器上的 .log 文件中。 此日志文件与更新捆绑同名，并且会写入到 **%SystemRoot%/Temp** 文件夹中。  

 运行更新捆绑时，会将与更新捆绑同名的文件提取到计算机上的临时文件夹中，然后运行 Updatesetup.exe。 Updatesetup.exe 会为 Configuration Manager &lt;产品版本\> &lt;KB 编号\> 向导启动软件更新。  

 在适用的更新范围内，此向导会在站点服务器上的 System Center Configuration Manager 安装文件夹下创建一系列文件夹。 文件夹结构如下所示：   
 **\\\\&lt;服务器名称\>\SMS_&lt;站点代码\>\修补程序\\&lt;KB 编号\>\\&lt;更新类型\>\\&lt;平台\>**。  

 下表提供了有关文件夹结构中的各个文件夹的详细信息：  

|文件夹名称|更多信息|  
|-----------------|----------------------|  
|&lt;服务器名称\>|这是在其中运行更新捆绑的站点服务器的名称。|  
|SMS_&lt;站点代码\>|这是 Configuration Manager 安装文件夹的共享名称。|  
|&lt;KB 编号\>|这是此更新捆绑的知识库文章的 ID 编号。|  
|&lt;更新类型\>|这些是 Configuration Manager 的更新类型。 向导会为更新捆绑中包含的每种更新类型创建一个单独的文件夹。 文件夹名称表示更新类型。 它们包括以下内容：<br /><br /> **服务器**：包括对站点服务器、站点数据库服务器和运行 SMS 提供程序的计算机的更新。<br /><br /> **客户端**：包括对 Configuration Manager 客户端的更新。<br /><br /> **AdminConsole**：包括对 Configuration Manager 客户端的更新<br /><br /> 除了上述更新类型之外，向导还会创建一个名为 **SCUP**的文件夹。 此文件夹并不表示更新类型，而是包含更新发布服务器的 .cab 文件。|  
|&lt;平台\>|这是特定于平台的文件夹。 它包含特定于处理器类型的更新文件。  这些文件夹包括：<br /><br />- x64<br /><br /> - I386|  

##  <a name="bkmk_Install"></a> 如何安装更新  
 要安装更新，必须首先在站点服务器上安装更新捆绑。 安装更新捆绑时，会为该更新启动安装向导。 此向导将执行以下操作：  

-   提取更新文件  

-   帮助你配置部署  

-   在本地计算机的服务器组件上安装适用的更新  

在站点服务器上安装更新捆绑包之后，可以更新 Configuration Manager 的其他组件。 下表描述了适用于这些不同组件的更新操作：  

|组件|说明|  
|---------------|------------------|  
|站点服务器|当你未选择直接在远程站点服务器上安装更新捆绑时将更新部署到该远程站点服务器。|  
|站点数据库|对于远程站点服务器，如果未直接在该远程站点服务器上安装更新捆绑，则将包括更新的服务器更新部署到站点数据库。|  
|Configuration Manager 控制台|初次安装 Configuration Manager 控制台后，可以在运行该控制台的每台计算机上为 Configuration Manager 控制台安装更新。 无法修改 Configuration Manager 控制台安装文件以在初次安装控制台过程中应用更新。|  
|远程 SMS 提供程序|为安装更新捆绑所在的非站点服务器计算机上运行的每个 SMS 提供程序实例安装更新。|  
|Configuration Manager 客户端|初次安装 Configuration Manager 客户端后，可以在运行该客户端的每台计算机上为 Configuration Manager 客户端安装更新。|  

> [!NOTE]  
>  可以只对运行 Configuration Manager 客户端的计算机部署更新。  

 如果重新安装客户端、Configuration Manager 控制台或 SMS 提供程序，则还必须为这些组件重新安装更新。  

 使用下列各部分中的信息在 Configuration Manager 的每个组件上安装更新。  

###  <a name="bkmk_servers"></a> 更新服务器  
 服务器更新可能包括**站点**、**站点数据库**和运行 **SMS 提供程序**实例的计算机的更新：  

####  <a name="bkmk_site"></a>更新站点  
 要更新 Configuration Manager 站点，可以直接在站点服务器上安装更新捆绑包，也可以在其他站点上安装更新捆绑包之后，将更新部署到站点服务器。  

 在站点服务器上安装更新时，更新安装进程会管理应用更新所需的其他操作，如更新站点系统角色。 此情况的例外是站点数据库。 以下部分包含有关如何更新站点数据库的信息。  

####  <a name="bkmk_database"></a>更新站点数据库  
 为了更新站点数据库，安装进程会对站点数据库运行一个名为“update.sql”  的文件。 你可以将更新进程配置为自动更新站点数据库，或者可以以后手动更新站点数据库。  

 **自动更新站点数据库**  

 在站点服务器上安装更新捆绑时，可以选择在安装服务器更新时自动更新站点数据库。 此决策仅适用于安装了更新捆绑的站点服务器，不适用于为在远程站点服务器上安装更新而创建的部署。  

> [!NOTE]  
>  选择自动更新站点数据库时，进程会更新数据库，而不考虑数据库是位于站点服务器上还是位于远程计算机上。  

> [!IMPORTANT]  
>  在更新站点数据库之前，请创建站点数据库的备份。 你不能卸载站点数据库的更新。 有关如何创建 Configuration Manager 的备份信息，请参阅 [System Center Configuration Manager 的备份和恢复](../../../protect/understand/backup-and-recovery.md)。  

 **手动更新站点数据库**  

 如果选择在站点服务器上安装更新捆绑时不自动更新站点数据库，则服务器更新不会在运行更新捆绑的站点服务器上修改数据库。 但是，使用为软件部署或该安装创建的包的部署将始终更新站点数据库。  

> [!WARNING]  
>  如果更新包括站点服务器更新和站点数据库更新，则在为站点服务器和站点数据库完成更新之前，此更新将不能正常运行。 对站点数据库应用更新之前，站点处于不受支持状态。  

 **手动更新站点数据库：**  

1.  在站点服务器上停止 SMS_SITE_COMPONENT_MANAGER 服务，然后停止 SMS_EXECUTIVE 服务。  

2.  关闭 Configuration Manager 控制台。  

3.  在该站点的数据库上运行名为 **update.sql** 的更新脚本。 有关如何运行脚本来更新 SQL Server 数据库的信息，请参阅用于站点数据库服务器的 SQL Server 版本的文档。  

4.  重启在前面的步骤中停止的服务。  

5.  安装更新捆绑包时，会将 **update.sql** 提取到站点服务器上的以下位置：**\\\\&lt;Server Name\>\SMS_&lt;Site Code\>\Hotfix\\&lt;KB Number\>\update.sql**  

####  <a name="bkmk_provider"></a>更新运行 SMS 提供程序的计算机  
 安装包含 SMS 提供程序的更新的更新捆绑之后，必须将更新部署到运行 SMS 提供程序的每台计算机。 唯一的例外是，你安装此更新捆绑的站点服务器上以前安装的 SMS 提供程序实例。 在你安装此更新捆绑时，会更新站点服务器上的 SMS 提供程序的本地实例。  

 如果删除某计算机上的 SMS 提供程序，然后重新安装它，则之后必须在该计算机上重新安装 SMS 提供程序的更新。  

###  <a name="BKMK_clients"></a>更新客户端  
 如果安装的更新中包含针对 Configuration Manager 客户端的更新，则需选择是在更新安装过程中自动升级客户端，还是以后手动升级客户端。 有关客户端自动升级的详细信息，请参阅 [如何升级 Windows 计算机的客户端](https://technet.microsoft.com/library/mt627885.aspx)。  

 可以将更新与 Updates Publisher 或软件部署包一起部署，也可以选择在每个客户端上手动安装更新。 有关如何使用部署来安装更新的详细信息，请参阅本主题中的 [为 Configuration Manager 部署更新](#BKMK_Deploy) 部分。  

> [!IMPORTANT]  
>  在安装客户端更新且更新捆绑包含服务器更新时，请务必也在客户端分配到的主站点上安装服务器更新。  

若要手动安装客户端更新，则在每个 Configuration Manager 客户端上都必须运行 **Msiexec.exe**，并且引用特定于平台的客户端更新 .msp 文件。  

 例如，可以使用下列命令行来更新客户端。 此命令行在客户端计算机上运行 MSIEXEC，并且引用更新捆绑包在站点服务器上提取的 .msp 文件：**msiexec.exe /p \\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;KB Number\>\Client\\&lt;Platform\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="BKMK_console"></a>更新 Configuration Manager 控制台  
 若要更新 Configuration Manager 控制台，必须在控制台安装完成后在运行控制台的计算机上安装更新。  

> [!IMPORTANT]  
>  在安装 Configuration Manager 控制台的更新，且更新捆绑包具有服务器更新时，请务必也在与 Configuration Manager 控制台一起使用的站点上安装服务器更新。  

如果更新的计算机运行 Configuration Manager 客户端：  

-   可以使用部署来安装更新。 有关如何使用部署来安装更新的详细信息，请参阅本主题中的 [为 Configuration Manager 部署更新](#BKMK_Deploy) 部分。  

-   如果你是直接登录到客户端计算机，则可通过交互方式运行安装。  

-   你可以在每台计算机上手动安装更新。 若要手动安装 Configuration Manager 控制台更新，则在运行 Configuration Manager 控制台的每台计算机上运行 Msiexec.exe，并引用 Configuration Manager 控制台更新 .msp 文件。  

例如，可以使用下列命令行来更新 Configuration Manager 控制台。 此命令行在客户端计算机上运行 MSIEXEC，并且引用更新捆绑在站点服务器上提取的 .msp 文件：**msiexec.exe /p \\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;KB Number\>\AdminConsole\\&lt;Platform\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="BKMK_Deploy"></a> 为 Configuration Manager 部署更新  
 在站点服务器上安装了更新捆绑之后，可以通过以下三种方法之一将更新部署到其他计算机。  

###  <a name="BKMK_DeploySCUP"></a>使用 Updates Publisher 2011 安装更新  
 在站点服务器上安装更新捆绑时，安装向导会为 Updates Publisher 创建一个目录文件，用于将更新部署到适用的计算机。 即使选择“使用包和程序来部署此更新” 选项，此向导也会创建该目录。  

 Updates Publisher 的目录名为 **SCUPCatalog.cab**，它位于运行更新捆绑包的计算机上的下列位置：**\\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;KB Number\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
>  在创建 SCUPCatalog.cab 时，使用了安装更新捆绑的站点服务器的特定路径，因此，无法在其他站点服务器上使用该文件。  

 在向导完成之后，可以将该目录导入到 Updates Publisher，然后使用 Configuration Manager 软件更新来部署更新。 有关 Updates Publisher 的信息，请参阅 System Center 2012 的 TechNet 库中的 [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkID=83449)。  

 使用下列过程将 SCUPCatalog.cab 文件导入到更新发布服务器，然后发布更新。  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>将更新导入到 Updates Publisher 2011  

1.  启动 Updates Publisher 控制台，然后单击“导入”。  

2.  在“Import Software Updates Catalog Wizard”（导入软件更新目录向导）的“Import Type”（导入类型）  页上，选择“Specify the path to the catalog to import”（指定要导入的目录的路径） ，然后指定 SCUPCatalog.cab 文件。  

3.  单击“Next”（下一步） ，然后再次单击“Next”（下一步）  。  

4.  在“Security Warning - Catalog Validation”（安全警告 - 目录验证）  对话框中，单击“Accept”（接受） 。 在向导完成后关闭它。  

5.  在 Updates Publisher 控制台中，选择要部署的更新，然后单击“发布”。  

6.  在“Publish Software Updates Wizard”（发布软件更新向导）的“Publish Options”（发布选项）  页上，选择“Full Content”（完整内容） ，然后单击“Next”（下一步） 。  

7.  完成向导以发布更新。  

###  <a name="BKMK_DeploySWDist"></a>使用软件部署来安装更新  
 在主站点或管理中心站点的站点服务器上安装更新捆绑时，可以配置安装向导以创建软件部署的更新包。 然后，可以将每个包部署到要更新的计算机的集合。  

 若要创建软件部署包，在向导的“Configure Software Update Deployment”（配置软件更新部署）  页上，选中要更新的每种更新包类型的复选框。 可用的类型可能包括服务器、Configuration Manager 控制台和客户端。 对于所选的每种更新类型，都会单独创建一个包。  

> [!NOTE]  
>  服务器的包将包含下列组件的更新：  
>   
>  -   站点服务器  
>  -   SMS 提供程序  
>  -   站点数据库  

 接下来，在向导的“Configure Software Update Deployment Method”（配置软件更新部署方法）  页上，选择“I will use software distribution”（我将使用软件分发） 选项。 选择此选项指示向导创建软件部署包。  

 在向导完成之后，可以在 Configuration Manager 控制台的“软件库”工作区的“包”节点中查看该向导创建的包。 然后，可以按照标准过程将软件包部署到 Configuration Manager 客户端。 当包在客户端上运行时，它会在客户端计算机上安装对相应的 Configuration Manager 组件的更新。  

 有关如何将包部署到 Configuration Manager 客户端的详细信息，请参阅 [System Center Configuration Manager 中的包和程序](../../../apps/deploy-use/packages-and-programs.md)。  

###  <a name="BKMK_DeployCollections"></a>创建集合以将更新部署到 Configuration Manager  
 可以将特定的更新部署到合适的客户端。 下列信息可以帮助你为 Configuration Manager 的不同组件创建设备集合。  

|Configuration Manager 组件|说明|  
|----------------------------------------|------------------|  
|管理中心站点服务器|创建直接成员身份查询，并且添加管理中心站点服务器计算机。|  
|所有主站点服务器|创建直接成员身份查询，并且添加每台主站点服务器计算机。|  
|所有辅助站点服务器|创建直接成员身份查询，并且添加每台辅助站点服务器计算机。|  
|所有 x86 客户端|使用下列查询条件创建集合：<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"**|  
|所有 x64 客户端|使用下列查询条件创建集合：<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"**|  
|运行 Configuration Manager 控制台的所有计算机|创建直接成员身份查询，并且添加每台计算机。|  
|运行 SMS 提供程序实例的远程计算机|创建直接成员身份查询，并且添加每台计算机。|  

> [!NOTE]  
>  若要更新站点数据库，请将更新部署到该站点的站点服务器。  

 有关如何创建集合的信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../core/clients/manage/collections/create-collections.md)。  
