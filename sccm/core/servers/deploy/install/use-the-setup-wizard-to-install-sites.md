---
title: 安装向导
titleSuffix: Configuration Manager
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c51158412b8bc9737c4851fc43dc2a7776488b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501260"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>使用安装向导安装 Configuration Manager 站点

适用范围：System Center Configuration Manager (Current Branch)

若要使用引导式用户界面安装新的 Configuration Manager 站点，请使用 Configuration Manager 安装向导 (setup.exe)。 该向导支持安装主站点或管理中心站点。 还可使用该向导将 Configuration Manager 的[评估安装升级](/sccm/core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install)为完全许可的安装。 如果不想使用此向导，可改用[安装脚本](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites)并运行无人参与的命令行安装。

在 Configuration Manager 控制台中安装辅助站点。 辅助站点不支持脚本化的命令行安装。



## <a name="bkmk_primary"></a> 安装管理中心站点或主站点

使用下面的过程安装管理中心站点或主站点。 还可以使用它将评估站点升级到获得完整许可的 Configuration Manager 站点。   

开始安装站点前，请先熟悉以下文章中的详细信息：
- [安装站点的准备工作](/sccm/core/servers/deploy/install/prepare-to-install-sites)
- [安装站点的先决条件](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites)

如果要在站点扩展方案期间安装管理中心站点，请在执行以下步骤前查看[扩展独立主站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand)。

### <a name="bkmk_installpri"></a> 安装主站点或管理中心站点的过程

1. 在想要安装该站点的计算机上，运行 `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` 以启动“System Center Configuration Manager 安装向导”。  

    > [!NOTE]  
    > 若要安装管理中心站点以便展开独立主站点，或在现有层次结构中安装新的子主站点，请使用与一个或多个现有站点的版本匹配的安装介质（源文件）。 如果安装的控制台内部更新更改了以前安装的站点版本，请勿使用原始安装介质。 请改用已更新站点的 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)中的源文件。 Configuration Manager 要求所用的源文件必须与新站点要连接到的现有站点版本相匹配。  

2. 在“开始之前”页上，选择“下一步”。  

3. 在“入门”页面上，选择要安装的站点类型：  

    - **管理中心站点** - 作为新层次结构的第一个站点，或在扩展独立主站点时使用：  

        选择“安装 Configuration Manager 管理中心站点”。  

        在此过程的后续步骤中，可以选择安装管理中心站点作为新层次结构的第一个站点，或者安装管理中心站点以扩展独立主站点。  

    - **主站点** - 作为独立主站点（即新层次结构的第一个站点），或作为子主站点：  

        选择“安装 Configuration Manager 主站点”。  

        > [!TIP]  
        > 通常，当想要在测试环境中安装独立主站点时，你只需选择“为独立主站点使用典型安装选项”  选项即可。 当选择此选项时，安装程序将执行以下操作：  
        > 
        > - 将站点自动配置为独立主站点。  
        > - 使用默认安装路径。  
        > - 对站点数据库使用 SQL Server 默认实例的本地安装。  
        > - 在站点服务器计算机上安装管理点和分发点。  
        > - 使用英语以及主站点服务器上操作系统的显示语言配置站点（如果它匹配 Configuration Manager 支持的其中一种语言）。  

4. “产品密钥”页：  

    - 选择将 Configuration Manager 安装为评估版还是许可版。  

        - 如果选择许可版，请输入你的产品密钥，然后选择“下一步”。  

        - 如果选择评估版，请选择“下一步”。 （随后可将评估版安装升级为完整版安装。）  

    - 此外可以指定许可协议的软件保障到期日期。 它可以方便地就该日期进行提醒。 如果在设置期间未输入此日期，则稍后可在 Configuration Manager 控制台中指定。  

        > [!NOTE]   
        > Microsoft 不会验证所输入的到期日期，且不会使用此日期验证许可证。 可以使用该日期作为到期日期提醒。 此日期很有用，因为 Configuration Manager 定期检查在线提供的新软件更新。 软件保障许可证状态应该处于最新状态，以便有资格使用这些额外的更新。    

    有关详细信息，请参阅[许可和分支](/sccm/core/understand/learn-more-editions)。  

5. 在“Microsoft 软件许可条款”  页上，阅读并接受许可条款。  

6. 在“先决条件许可证”  页上，阅读并接受必备软件的许可条款。 安装程序将在必需时下载该软件并将其自动安装到站点系统或客户端上。 接受所有条款才能继续进入下一页。  

7. 在“先决条件下载”页上，指定安装程序是必须从 Internet 下载最新的必备软件可再发行文件还是使用以前下载的文件：  

    - 如果想要安装程序现在下载文件，请选择“下载所需的文件”。 然后指定存储文件的位置。  

    - 如果以前通过使用[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)下载了文件，请选择“使用以前下载的文件”。 然后指定下载文件夹。  

        > [!TIP]  
        > 如果使用以前下载的文件，请验证下载文件夹的路径是否包含文件的最新版本。  

8. 在“服务器语言选择”页面中，选择可用于 Configuration Manager 控制台和报表的语言。 （默认选中“英语”且不可删除。）有关详细信息，请参阅[语言包](/sccm/core/servers/deploy/install/language-packs)。  

9. 在“客户端语言选择”页上，选择客户端计算机可用的语言。 此外指定是否为移动设备客户端启用所有客户端语言。 （默认选中“英语”且不可删除。）  

    > [!IMPORTANT]  
    > 使用管理中心站点时，请确保管理中心站点处配置的客户端语言包含各子主站点处所配置的全部客户端语言。 从分发点安装的客户端具有从顶层站点访问客户端语言的权限，而从管理点安装的客户端具有从其已分配的主站点访问客户端语言的权限。  

10. 在“站点和安装设置”页上，为要安装的新站点指定以下设置：  

    - **站点代码**：[层次结构中的每个站点代码都必须是唯一的](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_sitecodes)。 使用三个字母数字：A 到 Z 和 0 到 9。 由于文件夹名称中使用了站点代码，因此请勿使用 Windows 保留的名称，包括：    
        - AUX  
        - CON    
        - NUL    
        - PRN    
        - SMS  

        > [!NOTE]  
        > 安装程序不会验证你指定的站点代码是否未被使用，或者它是否具有保留名称。  

    - **站点名称**：每个站点都需要此友好名称，它可帮助你标识站点。  

    - **安装文件夹**：此文件夹是 Configuration Manager 安装的路径。 安装站点后，无法更改位置。 该路径不能包含 Unicode 字符或尾随空格。  

11. 在“站点安装”页上，使用与你的方案匹配的以下选项：  

    - **正在安装管理中心站点：**  

        在“管理中心站点安装”页上，选择“安装为新层次结构中的第一个站点”，然后选择“下一步”继续操作。  

    - **正在将独立主站点扩展到包含管理中心站点的层次结构中：**  

        在“管理中心站点安装”页上，选择“将现有的独立主站点扩展到层次结构中”。 然后，指定独立主站点服务器的 FQDN，并选择“下一步”以继续。  

        安装新的管理中心站点时所用的介质必须与主站点的版本相匹配。  

    - **正在安装独立主站点：**  

        在“主站点安装”页上，选择“以独立站点形式安装主站点”，然后选择“下一步”。  

    - **正在安装子主站点：**  

        在“主站点安装”页上，选择“将主站点加入到现有层次结构”。 然后指定管理中心站点的 FQDN，并选择“下一步”。  

12. 在“数据库信息”页面中，指定下列信息：  

    - **SQL Server 名称 (FQDN)**：默认情况下，此值设置为站点服务器计算机。  

        如果使用自定义端口，请将该端口添加到 SQL Server 的 FQDN。 请在 SQL Server 的 FQDN 后附加逗号，然后附加端口号。 例如，对于服务器 SQLServer1.fabrikam.com，请使用以下内容指定端口 1551：`SQLServer1.fabrikam.com,1551`  

    - **实例名称**：默认情况下，该值为空。 它在站点服务器计算机上使用 SQL 的默认实例。  

    - **数据库名称**：默认情况下，该值设置为 `CM_<Sitecode>`。 可以自定义此值。  

    - **Service Broker 端口**：默认情况下，此值设置为使用默认 SQL Server Service Broker (SSB) 端口 4022。 SQL 通过该端口与其他站点的站点数据库直接通信。  

13. 在第二个“数据库信息”页面上，可为站点数据库指定 SQL Server 数据文件和 SQL Server 日志文件的自定义位置：  

    - 默认情况下，它使用 SQL Server 的默认文件位置。  

    - 使用 SQL Server 群集时，不可指定自定义文件位置。  

    - 先决条件检查程序不会检查自定义文件位置的可用磁盘空间。  

14. 在“SMS 提供程序设置”  页上，指定要在其上安装 SMS 提供程序的服务器的 FQDN。  

    - 默认情况下，它指定站点服务器。  

    - 安装站点后，可配置其他 SMS 提供程序。 有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。  

15. 在“客户端通信设置”  页上，选择是将所有站点系统配置为仅接受来自客户端的 HTTPS 通信，还是接受为每个站点系统角色配置的通信方法所传输的信息。  

    如果选择“所有站点系统角色仅接受来自客户端的 HTTPS 通信”，则客户端计算机必须具有有效的 PKI 证书才可进行客户端身份验证。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

    > [!NOTE]  
    > 此步骤仅在安装主站点时适用。 如果要安装管理中心站点，则跳过此步骤。  

16. 在“站点系统角色”  页上，选择是要安装管理点还是安装分发点。 对于每个选择使用安装程序安装的角色：  

    - 输入将托管角色的服务器的 FQDN。 然后选择服务器支持的客户端连接方法：HTTP 或 HTTPS。  

    - 如果在上一页上选择了“所有站点系统角色仅接受来自客户端的 HTTPS 通信”，则会针对 HTTPS 自动配置客户端连接设置。 只有返回上一页才可更改此设置。  

    > [!NOTE]  
    > 此步骤仅在安装主站点时适用。 如果要安装管理中心站点，则跳过此步骤。  

    > [!NOTE]  
    > 若要安装站点系统角色，安装程序将使用“站点系统安装帐户” 。 默认情况下，这将使用主站点的计算机帐户。 此帐户必须是远程计算机上的本地管理员才能安装站点系统角色。 如果此帐户缺少所需的权限，则在配置其他帐户用作站点系统安装帐户之后，取消选中站点系统角色，并在以后从 Configuration Manager 中安装它们。 有关详细信息，请参阅[帐户](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account)。  

17. 在“使用情况数据”页上，查看 Microsoft 收集的相关数据信息，然后选择“下一步”。 有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。  

18. “服务连接点设置”页面仅在以下情况下可用：  

    - 在要安装独立主站点时。  

    - 在要安装管理中心站点时。  

    > [!NOTE]  
    > 如果要安装子主站点，则跳过此步骤。  

     如果要在站点扩展方案期间安装管理中心站点，且已在独立主站点上安装此角色，则首先从独立主站点中卸载此角色。 层次结构中只可存在此角色的一个实例，且该实例仅在层次结构的顶层站点受支持。  

     选择“服务连接点”的配置后，选择“下一步”。 安装程序完成后，可以在 Configuration Manager 控制台中更改此配置。 有关详细信息，请参阅[关于服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。  

19. 在“设置摘要”页上，查看所选的设置。 准备就绪后，选择“下一步”以启动必备组件检查程序。  

20. 在“先决条件安装检查”页上，它将列出检查程序可识别的任何问题。  

    - 如果必备组件检查程序发现问题，请选择列表中的项目，详细了解如何解决该问题。  

    - 在继续安装站点之前，请解决“失败”项。 还应解决状态为“警告”的项目，但它们不会阻止站点安装。  

    - 解决问题后，选择“运行检查”以重新运行必备组件检查程序。  

        如果必备组件检查程序运行后检查均未收到“失败”状态，则可选择“开始安装”以启动站点安装。  

    > [!TIP]  
    > 除了向导提供的反馈之外，还可以在 ConfigMgrPrereq.log 文件中找到关于先决条件问题的其他信息。 它位于安装站点的计算机的系统驱动器的根目录中。 有关详细信息，请参阅[先决条件检查列表](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)。  

21. 在“安装”  页上，安装程序将显示安装状态。 核心站点服务器安装完成后，可以“关闭”安装向导。 关闭向导后，将在后台继续进行安装和初始站点配置。  

    - 在安装完成前，可将 Configuration Manager 控制台连接到该站点。 此控制台将作为只读连接，并允许你查看对象和设置，但不能修改任何内容。  

    - 安装完成后，可以连接可编辑对象和设置的控制台。  



## <a name="bkmk_expand"></a>扩展独立主站点

安装好独立主站点作为第一个站点后，稍后可通过安装管理中心站点将该站点扩展到更大的层次结构中。   

扩展独立主站点时，将会安装新的管理中心站点，此站点使用现有独立主站点的数据库作为引用。 安装新管理中心站点后，独立主站点将充当子级主站点。

- 只能将独立主站点扩展到新层次结构中。  

- 只能将一个独立主站点扩展到特定层次结构中。 此选项不能用于将其他独立主站点加入同一层次结构中。 相反，可以使用“迁移向导”将数据从一个层次结构迁移到另一个层次结构中。 有关详细信息，请参阅[在层次结构之间迁移数据](/sccm/core/migration/migrate-data-between-hierarchies)。  

- 将独立站点扩展到包含管理中心站点的层次结构中后，可以添加其他子级主站点。  

- 若要从具有管理中心站点的层次结构中删除主站点，请先卸载此主站点。  


若要扩展该站点，请使用“Configuration Manager 安装向导”以安装新的管理中心站点，但必须注意以下几点：  

- 使用相同版本的 Configuration Manager 将管理中心站点安装为独立主站点。  

- 在安装向导的“入门”页上，选择用于安装管理中心站点的选项。 在安装的后面阶段，选择用于扩展现有独立主站点的选项。  

- 在配置新的管理中心站点的“客户端语言选择”页时，选择的客户端语言必须与为要扩展的独立主站点配置的客户端语言相同。  

- 在“站点安装”页上，选择扩展独立主站点的选项。  


若要扩展独立主站点，首先查看[扩展站点的先决条件](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)。 然后使用本文前面部分介绍的[安装主站点或管理中心站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_installpri)过程。




## <a name="bkmk_secondary"></a>安装辅助站点

使用 Configuration Manager 控制台安装辅助站点。  

- 如果使用的控制台未连接到将充当新辅助站点的父站点的主站点，则安装该站点的命令将被复制到正确的主站点。  

- 在启动站点安装之前，请确保用户帐户具有必备权限。 此外确保托管新辅助站点的服务器满足用作辅助站点服务器的所有先决条件。  

- 安装辅助站点时，Configuration Manager 将配置新站点以使用父级主站点上配置的客户端通信端口。  


### <a name="bkmk_installsecondary"></a> 安装辅助站点的过程  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择将成为新辅助站点的父主站点的站点。  

2. 若要启动“创建辅助站点向导”，请选择功能区中的“创建辅助站点”。  

3. 在“开始之前”页上，确认列出的主站点是你想让其成为新辅助站点父级的站点。 然后选择“下一步”。  

4. 在“常规”  页上，指定下列设置：  

    - **站点代码**：层次结构中的每个站点代码都必须是唯一的。 使用三个字母数字：A 到 Z 和 0 到 9。 由于文件夹名称中使用了站点代码，因此请勿使用 Windows 保留的名称，包括：  

        - AUX    
        - CON    
        - NUL    
        - PRN  
        - SMS  

    > [!NOTE]  
    > 安装程序不会验证你指定的站点代码是否未被使用，或者它是否具有保留名称。  

    - **站点服务器名称**：此值是将安装新辅助站点的服务器的 FQDN。  

    - **站点名称**：每个站点都需要此友好名称，它可帮助你标识站点。  

    - **安装文件夹**：此文件夹是 Configuration Manager 安装的路径。 安装站点后，无法更改位置。 该路径不能包含 Unicode 字符或尾随空格。  

    > [!IMPORTANT]  
    > 在此页面上指定详细信息之后，可以选择“摘要”直接转到向导的“摘要”页。 此操作对其余辅助站点选项使用默认设置。  
    > 
    > - 仅当熟悉此向导中的默认设置，并且它们是你想要使用的设置时，才使用此选项。  
    > - 如果使用默认设置，则边界组与分发点无关。 在配置含有辅助站点服务器的边界组之前，客户端不会将此辅助站点上安装的分发点用作内容源位置。  

5. 在“安装源文件”  页上，选择辅助站点计算机如何获取用于安装该站点的源文件。  

    当使用在网络上共享或本地复制到目标辅助站点服务器的 CD.Latest 源文件时：  

    - 1802 版及更早版本

        - CD.Latest 源文件位置包括一个名为“Redist”的文件夹。 将此“Redist”文件夹作为子文件夹移动到“SMSSETUP”文件夹下。  

            > [!Note]  
            > 如果在安装过程中出现哈希不匹配错误，请更新“Redist”文件夹。 使用[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)获取最新文件。 此外，对于任何导致哈希不匹配错误的文件，请将它们从更新的“Redist”文件夹复制到“SMSSETUP\BIN\X64”文件夹。 

    - **1806 版及更高版本**<!-- SCCMDocs-pr issue 3164 -->

        - CD.Latest 源文件位置包括一个名为“Redist”的文件夹。 将此“Redist”文件夹作为子文件夹移动到“SMSSETUP”文件夹下。  

        - 将以下文件从“Redist”文件夹复制到“SMSSETUP\BIN\X64”文件夹：   
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - 如果“Redist”中的所有文件都不可用，安装程序将无法安装辅助站点。  

    - 辅助站点服务器的计算机帐户必须具有对源文件文件夹和共享的“读取”权限。  

6. 在“SQL Server 设置”  页上，指定要使用的 SQL Server 版本，然后配置相关设置。  

    > [!NOTE]  
    > 开始安装前，安装程序不会验证你在此页上输入的信息。 在继续之前，请验证这些设置。  

    - **在辅助站点计算机上安装和配置 SQL Express 的本地副本**  

        - **SQL Server 服务端口**：指定 SQL Server Express 要使用的 SQL Server 服务端口。 通常，此服务端口被配置为使用 TCP 端口 1433，但你可以配置其他端口。  

        - **SQL Server Broker 端口**：指定 SQL Server Express 要使用的 SQL Server Service Broker (SSB) 端口。 通常，Service Broker 被配置为使用 TCP 端口 4022，但你可以配置其他端口。 指定其他站点/服务均未使用且防火墙限制均未阻止的有效端口。  

    - **使用现有的 SQL Server 实例**  

        - **SQL Server FQDN**：查看运行 SQL Server 的计算机的 FQDN。 必须使用运行 SQL Server 的本地服务器托管辅助站点数据库，且此设置不可修改。  

        - **SQL Server 实例**：指定要用作辅助站点数据库的 SQL Server 实例。 将此选项留空以使用默认实例。  

        - **ConfigMgr 站点数据库名称**：指定要用于辅助站点数据库的名称。  

        - **SQL Server Broker 端口**：指定 SQL Server 要使用的 SQL Server Service Broker (SSB) 端口。 指定其他站点/服务均未使用且防火墙限制均未阻止的有效端口。  

    > [!TIP]  
    > 关于 System Center Configuration Manager 所支持的 SQL Server 版本列表，请参阅[支持的 SQL Server 版本](/sccm/core/plan-design/configs/support-for-sql-server-versions)。  

7. 在“分发点”  页上，配置将在辅助站点服务器上安装的分发点的设置。  

    - **必需设置：**  

        - **指定客户端设备与分发点通信的方式**：介于HTTP 和 HTTPS 之间进行选择。  

        - **创建自签名证书或导入 PKI 客户端证书**：选择使用自签名证书还是从 PKI 导入证书。 使用自签名证书，可从 Configuration Manager 客户端匿名连接到内容库。 在分发点发送状态消息之前，此证书用于向管理点验证分发点。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

    - **可选设置：**  

        - **在 Configuration Manager 要求的情况下安装和配置 IIS**：选择此设置可让 Configuration Manager 安装并配置尚未安装在服务器上的 Internet Information Services (IIS)。 所有分发点都需要 IIS。  

            > [!NOTE]  
            > 虽然此设置是可选的，但必须先在服务器上安装 IIS 才能成功安装分发点。  

        - **启用和配置此分发点的 BranchCache**  

        - **描述**：此值是分发点的易懂说明，可帮助理解。  

        - **为预安排内容启用此分发点**  

8. 在“驱动器设置”  页上，指定辅助站点分发点的驱动器设置。  

    可以为内容库和包共享分别配置最多两个磁盘驱动器。 但是，当前两个驱动器达到配置的驱动器空间预留量时，Configuration Manager 可使用其他驱动器。 在“驱动器设置”页中，可配置磁盘驱动器的优先级以及各磁盘驱动器上剩余的可用磁盘空间量。  

    - **保留的驱动器空间 (MB)**：在 Configuration Manager 选择其他驱动器并对其继续执行复制过程之前，为此设置配置的值会确定驱动器上的可用空间量。 内容文件可以跨多个驱动器。  

    - **内容位置**：指定内容库和包共享的内容位置。 Configuration Manager 会将内容复制到主内容位置，直到可用空间量达到为“保留的驱动器空间 (MB)”指定的值。  

    默认情况下，内容位置设置为“自动” 。 主内容位置设置为安装时具有最多磁盘空间的磁盘驱动器。 辅助位置设置为次于主驱动器但具有最多可用磁盘空间的磁盘驱动器。 当主驱动器和辅助驱动器达到保留的驱动器空间时，Configuration Manager 将选择另一个具有最多可用磁盘空间的可用驱动器，并继续执行复制过程。  

9. 在“内容验证”  页上，指定是否验证分发点上的内容文件的完整性。  

    - 如果按计划启用内容验证，Configuration Manager 将在计划的时间启动进程。 会验证分发点上的所有内容。  

    - 你还可以配置“内容验证优先级” 。  

    - 要查看内容验证过程的结果，请转到 Configuration Manager 控制台的“监视”工作区，展开“分发状态”，并选择“内容状态”节点。 它显示每种包类型的内容。 这些类型包括应用程序、软件更新包和启动映像。  

10. 在“边界组”页上，管理此分发点分配到的边界组：  

    - 在内容部署过程中，客户端必须位于与分发点关联的边界组中，才能将其用作内容的源位置。  

    - 你可以选择“允许内容源位置回退”  选项，以便在没有首选分发点可用时让这些边界组外部的客户端回退并使用分发点作为内容的源位置。  

        有关详细信息，请参阅[内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)。  

11. 在“摘要”页上，验证设置，然后选择“下一步”以安装辅助站点。 当向导显示“完成”页面时，可以关闭向导。 辅助站点安装将在后台继续进行。  


### <a name="bkmk_verify"></a> 如何验证辅助站点安装状态  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2. 选择要安装的辅助站点，然后在功能区中选择“显示安装状态”。  

    > [!TIP]  
    > 同时安装多个辅助站点时，必备组件检查程序一次针对一个站点运行。 必须在完成一个站点检查后才可开始检查下一站点。  

