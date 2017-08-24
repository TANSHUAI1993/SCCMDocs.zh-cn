---
title: "安装向导 | Microsoft Docs"
ms.custom: na
ms.date: 7/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 678f1b35fe6f7649dacb766f7c671f4ec8ea1435
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>使用安装向导安装 System Center Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*


若要使用引导式用户界面安装新的 System Center Configuration Manager 站点，请使用 Configuration Manager 安装向导 (setup.exe)。 该向导支持安装主站点或管理中心站点。 还可使用该向导将 Configuration Manager 的[评估安装升级](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md)为完全许可的安装。 如果不想使用此向导，可改用[安装脚本](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)并运行无人参与的命令行安装。

若要安装辅助站点，必须在 Configuration Manager 控制台内安装该站点。 辅助站点不支持脚本化的命令行安装。

## <a name="bkmk_primary"></a>安装管理中心站点或主站点
使用下列过程安装管理中心站点或主站点，或者将评估站点升级到完全许可的 Configuration Manager 站点。   

开始安装站点前，请先熟悉以下文章中的详细信息：
 -  [安装站点的准备工作](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [安装站点的先决条件](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

如果要在站点扩展方案期间安装管理中心站点，请在执行以下步骤前查看本主题中的[扩展独立主站点](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)部分。

### <a name="bkmk_installpri"></a>安装主站点或管理中心站点

1.  在想要安装该站点的计算机上，运行 **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** 以启动“System Center Configuration Manager 安装向导”。  

    > [!NOTE]  
    > 若要安装管理中心站点以便展开独立主站点，或在现有层次结构中安装新的子主站点，必须使用与现有站点或站点版本匹配的安装媒体（源文件）。 如果安装的控制台内部更新更改了以前安装的站点版本，请勿使用原始安装介质。 请改用已更新站点的 [CD.Latest 文件夹](../../../../core/servers/manage/the-cd.latest-folder.md)中的源文件。 Configuration Manager 要求所用的源文件必须与新站点要连接到的现有站点版本相匹配。  

2.  在“开始之前”页上，选择“下一步”。  

3.  在“入门”页面上，选择要安装的站点类型：  

    -   **管理中心站点** - 作为新层次结构的第一个站点，或在扩展独立主站点时使用：  

        选择“安装 Configuration Manager 管理中心站点”。  

         在此过程的后续步骤中，你可以选择安装管理中心站点作为新层次结构的第一个站点，或者安装管理中心站点以扩展独立主站点。  

    -    **主站点** - 作为独立主站点（即新层次结构的第一个站点），或作为子主站点：  

        选择“安装 Configuration Manager 主站点”。  

        > [!TIP]  
        > 通常，当想要在测试环境中安装独立主站点时，你只需选择“为独立主站点使用典型安装选项”  选项即可。 选择此选项时，安装程序会：  

        > -   将站点自动配置为独立主站点。  
        > -   使用默认安装路径。  
        > -   对站点数据库使用 SQL Server 默认实例的本地安装。  
        > -   在站点服务器计算机上安装管理点和分发点。  
        > -   使用英语以及主站点服务器上操作系统的显示语言配置站点（如果它匹配 Configuration Manager 支持的其中一种语言）。  

4.  “产品密钥”页：
    - 选择将 Configuration Manager 安装为评估版还是许可版。  

      -   如果选择许可版，请输入你的产品密钥，然后选择“下一步”。  

      -   如果选择评估版，请选择“下一步”。 （随后可将评估版安装升级为完整版安装。）  
    - 自 2016 年 10 月发布 System Center Configuration Manager 的 1606 版基线介质起，可指定软件保障协议的到期日期。 在此页上，可选择指定许可协议的**软件保障到期日期**，以便接收该日期的提醒。 如果在设置期间未输入此信息，则稍后可在 Configuration Manager 控制台中指定。

      > [!NOTE]   
      > Microsoft 不会验证所输入的到期日期，且不会使用此日期验证许可证。 相反，可以使用该日期作为到期日期提醒。 这很有用，因为 Configuration Manager 会定期检查在线提供的新软件更新，而软件保障许可证应为最新状态，才有资格使用这些额外的更新。    

      有关详细信息，请参阅 [System Center Configuration Manager 的许可和分支](/sccm/core/understand/learn-more-editions)。

5.  在“Microsoft 软件许可条款”  页上，阅读并接受许可条款。  

6.  在“先决条件许可证”  页上，阅读并接受必备软件的许可条款。 安装程序将在必需时下载该软件并将其自动安装到站点系统或客户端上。 必须勾选所有框，然后才能转到下一页。  

7.  在“先决条件下载”  页上，指定安装程序是必须从 Internet 下载最新的必备软件可再发行文件还是使用以前下载的文件：  

    -   如果想要安装程序现在下载文件，请选择“下载所需的文件”  并指定存储文件的位置。  

    -   如果以前通过使用[安装程序下载程序](../../../../core/servers/deploy/install/setup-downloader.md)下载了文件，请选择“使用以前下载的文件”并指定下载文件夹。  

        > [!TIP]  
        > 如果使用以前下载的文件，请验证下载文件夹的路径是否包含文件的最新版本。  

8.  在“服务器语言选择”页面中，选择可用于 Configuration Manager 控制台和报表的语言。 （默认选中“英语”且不可删除。）  

9. 在“客户端语言选择”页上，选择可用于客户端计算机的语言，并指定是否为移动设备客户端启用所有客户端语言。 （默认选中“英语”且不可删除。）  

    > [!IMPORTANT]  
    > 使用管理中心站点时，请确保管理中心站点处配置的客户端语言包含各子主站点处所配置的全部客户端语言。 这是因为从分发点安装的客户端具有从顶层站点访问客户端语言的权限，而从管理点安装的客户端具有从其已分配的主站点访问客户端语言的权限。  

10. 在“站点和安装设置”页上，为要安装的新站点指定以下内容：  

    -   **站点代码**：[层次结构中的每个站点代码必须唯一](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes)，且由 3 个字母数字（A 到 Z 和 0 到 9）组成。 由于文件夹名称中使用了站点代码，因此请勿在站点中使用 Windows 保留的名称，包括：    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > 安装程序不会验证所指定的站点代码是否未被使用，或者它是否具有保留名称。  

    -   **站点名称：**每个站点都需要此友好名称，它可帮助你标识站点。  

    -   **安装文件夹：**这是 Configuration Manager 安装的文件夹路径。 安装站点后，无法更改位置。 此外，该路径不能包含 Unicode 字符或尾随空格。  

11. 在“站点安装”页上，使用与你的方案匹配的以下选项：  

    -   **正在安装管理中心站点：**  

         在“管理中心站点安装”页上，选择“安装为新层次结构中的第一个站点”，然后选择“下一步”继续操作。  

    -   **正在将独立主站点扩展到包含管理中心站点的层次结构中：**  

         在“管理中心站点安装”页上，选择“将现有的独立主站点扩展到层次结构中”，指定独立主站点服务器的 FQDN，然后选择“下一步”继续操作。  

         安装新的管理中心站点时所用的介质必须与主站点的版本相匹配。  

    -   **正在安装独立主站点：**  

         在“主站点安装”页上，选择“以独立站点形式安装主站点”，然后选择“下一步”。  

    -   **正在安装子主站点：**  

         在“主站点安装”页上，选择“将主站点加入到现有层次结构”，指定管理中心站点的 FQDN，然后选择“下一步”。  

12. 在“数据库信息”页面中，指定下列信息：  

    -   **SQL Server 名称 (FQDN)：** 默认情况下，此项设置为站点服务器计算机。

     如果使用自定义端口，请将该端口添加到 SQL Server 的 FQDN。 若要执行此操作，请在后续服务器的 FQDN 后附加逗号，然后附加端口号。   例如，对于服务器 SQLServer1.fabrikam.com，使用以下语句指定端口 1551：SQLServer1.fabrikam.com,1551

    -   **实例名称：**此项默认为空。 它在站点服务器计算机上使用 SQL 的默认实例。  

    -   **数据库名称：**默认情况下，将此设置为 CM_&lt;Sitecode\>。 可随意使用所指定的其他名称。  

    -   **Service Broker 端口**：默认情况下，设置为使用默认 SQL Server Service Broker (SSB) 端口 4022。 SQL 通过该端口与其他站点的站点数据库直接通信。  

13. 在第二个“数据库信息”页面上，可为站点数据库指定 SQL Server 数据文件和 SQL Server 日志文件的非默认位置：  

    -   提供了 SQL Server 的默认文件位置。  

    -   使用 SQL Server 群集时，不可指定非默认文件位置。  

    -   先决条件检查程序不会检查非默认文件位置的可用磁盘空间。  

14. 在“SMS 提供程序设置”  页上，指定要在其上安装 SMS 提供程序的服务器的 FQDN。  

    -   默认情况下，已指定站点服务器。  

    -   安装站点后，可配置其他 SMS 提供程序。  

15. 在“客户端通信设置”  页上，选择是将所有站点系统配置为仅接受来自客户端的 HTTPS 通信，还是接受为每个站点系统角色配置的通信方法所传输的信息。  

    如果选择“所有站点系统角色仅接受来自客户端的 HTTPS 通信”，则客户端计算机必须具有有效的 PKI 证书才可进行客户端身份验证。 有关 PKI 证书要求的详细信息，请参阅 [Configuration Manager 的 PKI 证书要求](https://technet.microsoft.com/library/gg699362.aspx)。  

    > [!NOTE]  
    > 此步骤仅在安装主站点时适用。 如果要安装管理中心站点，则跳过此步骤。  

16. 在“站点系统角色”  页上，选择是要安装管理点还是安装分发点。 对于每个选择使用安装程序安装的角色：  

    -   必须输入要托管角色的计算机的“FQDN”，并选择服务器将支持的客户端连接方法（HTTP 或 HTTPS）。  

    -   如果在上一页上选择了“所有站点系统角色仅接受来自客户端的 HTTPS 通信”，则会针对 HTTPS 自动配置客户端连接设置，且只有返回去才可更改此设置。  

    > [!NOTE]  
    > 此步骤仅在安装主站点时适用。 如果要安装管理中心站点，则跳过此步骤。  

    > [!NOTE]  
    > 若要安装站点系统角色，安装程序将使用“站点系统安装帐户” 。 默认情况下，这将使用主站点的计算机帐户。 此帐户必须是远程计算机上的本地管理员才能安装站点系统角色。 如果此帐户缺少所需的权限，则在配置其他帐户用作站点系统安装帐户之后，取消选中站点系统角色，并在以后从 Configuration Manager 中安装它们。  

17. 在“使用情况数据”页上，查看 Microsoft 收集的相关数据信息，然后选择“下一步”。  

18. “服务连接点设置”页面仅在设置期间可用：  

    -   在要安装独立主站点时。  

    -   在要安装管理中心站点时。  

    > [!NOTE]  
    > 如果要安装子级主站点，则跳过此步骤（此页面不可用）。  

     如果要在站点扩展方案期间安装管理中心站点，且已在独立主站点上安装此角色，则必须从独立主站点中卸载此角色。 层次结构中只可存在此角色的一个实例，且该实例仅可位于层次结构的顶层站点。  

     选择“服务连接点”的配置后，选择“下一步”。 （安装程序完成后，可以在 Configuration Manager 控制台中更改此配置。）  

19. 在“设置摘要”页上，查看所选的设置。 准备就绪后，选择“下一步”以启动必备组件检查程序。  

20. 在“先决条件安装检查”页上，将列出可识别的任何问题。  

    -   如果必备组件检查程序发现问题，请选择列表中的项目，详细了解如何解决该问题。  

    -   必须处理所有状态为“失败”的项目，才能继续安装站点。 需处理状态为“警告”的项目，但它们不会阻止站点的安装。  

    -   解决问题后，选择“运行检查”以重新运行必备组件检查程序。  

     如果必备组件检查程序运行后检查均未收到“失败”状态，则可选择“开始安装”以启动站点安装。  

    > [!TIP]  
    > 除了向导中提供的反馈，当在计算机系统驱动器的根目录中查看要在其上安装的“ConfigMgrPrereq.log”文件时，可找到有关先决条件问题的其他信息。 有关安装先决条件规则和描述的列表，请参阅 [System Center Configuration Manager 的先决条件检查列表](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)。  

21. 在“安装”  页上，安装程序将显示安装状态。 核心站点服务器安装完成后，可选择**关闭**安装向导。 关闭向导后，将在后台继续进行安装和初始站点配置。  

    -   在安装完成前，可将 Configuration Manager 控制台连接到该站点。 此控制台将作为只读连接，并允许你查看对象和设置，但不能引入编辑。  

    -   安装完成后，将能够连接可编辑对象和设置的控制台。  


## <a name="bkmk_expand"></a>扩展独立主站点
安装好独立主站点作为第一个站点后，稍后可通过安装管理中心站点将该站点扩展到更大的层次结构中。   

扩展独立主站点时，将会安装新的管理中心站点，此站点使用现有独立主站点的数据库作为引用。 安装新管理中心站点后，独立主站点将充当子级主站点。

-   仅可以将独立主站点扩展到新层次结构中。  

-   并且仅可以将一个独立主站点扩展到特定层次结构中。 此选项不能用于将其他独立主站点加入同一层次结构中。 相反，可以使用“迁移”将数据从一个层次结构迁移到另一个层次结构中。  

-   将独立站点扩展到包含管理中心站点的层次结构中后，可以添加其他子级主站点。  

-   若要从具有管理中心站点的层次结构中删除主站点，则必须卸载此主站点。  

若要扩展该站点，请使用 System Center Configuration Manager 安装向导以安装新的管理中心站点，但必须注意以下几点：  

-   必须使用相同版本的 Configuration Manager 将管理中心站点安装为独立主站点。  

-   在安装向导的“入门”页上，选择用于安装管理中心站点的选项。 在安装的后面阶段，选择用于扩展现有独立主站点的选项。  

-   在配置新的管理中心站点的“客户端语言选择”页面时，选择的客户端语言必须与为要扩展的独立主站点配置的客户端语言相同。  

-   在“站点安装”页上，选择扩展独立主站点的选项。  

若要扩展独立主站点，请首先查看[扩展站点的先决条件](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)，然后使用本文前面部分介绍的过程 *[ 安装主站点或管理中心站点 ](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*。


## <a name="bkmk_secondary"></a>安装辅助站点
 使用 Configuration Manager 控制台安装辅助站点。  

-   如果使用的控制台未连接到将充当新辅助站点的父级站点的主站点，则安装该站点的命令将被复制到正确的主站点。  

-   在开始站点安装之前，确保你的用户帐户具有必备权限，并且托管新辅助站点的计算机满足充当辅助站点服务器的所有先决条件。  

-   安装辅助站点时，Configuration Manager 将配置新站点以使用父级主站点上配置的客户端通信端口。  

### <a name="bkmk_installsecondary"></a>安装辅助站点  


1.  在 Configuration Manager 控制台中，导航到“管理” > “站点配置” > “站点”。 选择将成为新辅助站点的父主站点的站点。  

2.  选择“创建辅助站点”以启动“创建辅助站点向导”。  

3.  在“开始之前”页上，确认列出的主站点是你想让其成为新辅助站点父级的站点。 然后选择“下一步”。  

4.  在“常规”  页面上，指定下列值：  

    -   **站点代码**：层次结构中的每个站点代码必须唯一，且由 3 个字母数字（A 到 Z 和 0 到 9）组成。 由于文件夹名称中使用了站点代码，因此请勿在站点中使用 Windows 保留的名称，包括：  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > 安装程序不会验证你指定的站点代码是否未被使用，或者它是否具有保留名称。  

    -   **站点服务器名称**：这是新辅助站点将在其中安装的服务器的 FQDN。  

    -   **站点名称**：每个站点都需要此友好名称，它可帮助你标识站点。  

    -   **安装文件夹**：这是 Configuration Manager 安装的文件夹路径。 安装站点后，无法更改位置。 该路径不能包含 Unicode 字符或尾随空格。  

    > [!IMPORTANT]  
    > 在此页上指定详细信息后，可选择“摘要”以对其余的辅助站点选项使用默认设置，并直接转到向导的“摘要”页面。  

    > -   仅当熟悉此向导中的默认设置，并且它们是你想要使用的设置时，才使用此选项。  
    > -   如果使用默认设置，则边界组与分发点无关。 因此，在配置含有辅助站点服务器的边界组之前，客户端不会将此辅助站点上安装的分发点用作内容源位置。  

5.  在“安装源文件”  页上，选择辅助站点计算机如何获取用于安装该站点的源文件。  

     使用网络或辅助站点计算机上存储的源文件时：  

    -   源文件位置必须包含一个“Redist”文件夹，内附以前使用安装程序下载程序下载的所有文件。  

    -   如果“Redist”中的所有文件都不可用，安装程序将无法安装辅助站点。  

    -   辅助站点计算机的计算机帐户必须具有对源文件文件夹和共享的 **读取** 权限。  

6.  在“SQL Server 设置”  页上，指定要使用的 SQL Server 版本，然后配置相关设置。  

    > [!NOTE]  
    > 开始安装前，安装程序不会验证你在此页上输入的信息。 在继续之前，请验证这些设置。  

     **在辅助站点计算机上安装和配置 SQL Express 的本地副本**  

    -   **SQL Server 服务端口**：指定供 SQL Server Express 使用的 SQL Server 服务端口。 通常，此服务端口被配置为使用 TCP 端口 1433，但你可以配置其他端口。  

    -   **SQL Server Broker 端口**：指定供 SQL Server Express 使用的 SQL Server Service Broker (SSB) 端口。 通常，Service Broker 被配置为使用 TCP 端口 4022，但你可以配置其他端口。 必须指定其他站点/服务均未使用且防火墙限制均未阻止的有效端口。  

    > [!IMPORTANT]  
    > 当 Configuration Manager 安装 SQL Server Express 时，它会安装不带 service pack 的 SQL Server Express 2012：  

    > -   若要让辅助站点受到支持，必须在安装站点后将 SQL Server Express 2012 升级到[受支持的版本](/sccm/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions)。
    > -   此外，如果无法完成新辅助站点安装，但先完成了 SQL Server Express 2012 的安装，则必须先更新 SQL Server Express 实例，才能使 Configuration Manager 成功重试辅助站点安装。  

     **使用现有的 SQL Server 实例**  

    -   **SQL Server FQDN**：查看运行 SQL Server 的计算机的 FQDN。 必须使用运行 SQL Server 的本地服务器托管辅助站点数据库，且此设置不可修改。  

    -   **SQL Server 实例**：指定要用作辅助站点数据库的 SQL Server 实例。 将此选项留空以使用默认实例。  

    -   **ConfigMgr 站点数据库名称**：指定要用于辅助站点数据库的名称。  

    -   **SQL Server Broker 端口**：指定供 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 你必须指定没有其他站点或服务使用或没有防火墙限制阻止的有效端口。  

    > [!TIP]  
    > 关于 System Center Configuration Manager 所支持的 SQL Server 版本的列表，请参阅[支持的 SQL Server 版本](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

7.  在“分发点”  页上，配置将在辅助站点服务器上安装的分发点的设置。  

     **必需设置：**  

    -   **指定客户端设备与分发点通信的方式**：选择 HTTP 或 HTTPS。  

    -   **创建自签名证书或导入 PKI 客户端证书**：选择使用自签名证书（该证书允许从 Configuration Manager 客户端匿名连接到内容库）或者从 PKI 导入证书。  

         在分发点发送状态消息之前，此证书用于向管理点验证分发点。  

         有关证书要求的信息，请参阅 [Configuration Manager 的 PKI 证书要求](https://technet.microsoft.com/library/gg699362.aspx)。  

    **可选设置：**  

    -   **在 Configuration Manager 要求的情况下安装和配置 IIS**：选择此设置，让 Configuration Manager 在服务器上安装和配置 Internet 信息服务 (IIS)（如果尚未安装）。 必须在所有分发点上安装 IIS。  

        > [!NOTE]  
        > 虽然此设置是可选的，但必须先在服务器上安装 IIS 才能成功安装分发点。  

    -   **启用和配置此分发点的 BranchCache**。  

    -   **说明**。 这是分发点的易懂描述，可帮助理解。  

    -   **为预留内容启用此分发点**。  

8.  在“驱动器设置”  页上，指定辅助站点分发点的驱动器设置。  

     可以为内容库和包共享分别配置最多两个磁盘驱动器。 但是，当前两个驱动器达到配置的驱动器空间预留量时，Configuration Manager 可使用其他驱动器。 在“驱动器设置”页中，可配置磁盘驱动器的优先级以及各磁盘驱动器上剩余的可用磁盘空间量。  

    -   **保留的驱动器空间 (MB)**：在 Configuration Manager 选择其他驱动器并对其继续执行复制过程之前，为此设置配置的值会确定驱动器上的可用空间量。 内容文件可以跨多个驱动器。  

    -   **内容位置**：指定内容库和包共享的内容位置。 Configuration Manager 会将内容复制到主内容位置，直到可用空间量达到指定的“保留的驱动器空间 (MB)”值。

     默认情况下，内容位置设置为“自动” 。 主内容位置设置为安装时具有最多磁盘空间的磁盘驱动器。 辅助位置设置为次于主驱动器但具有最多可用磁盘空间的磁盘驱动器。 当主驱动器和辅助驱动器达到保留的驱动器空间时，Configuration Manager 将选择另一个具有最多可用磁盘空间的可用驱动器，并继续执行复制过程。  

9. 在“内容验证”  页上，指定是否验证分发点上的内容文件的完整性。  

    -   如果按计划启用内容验证，Configuration Manager 将在计划的时间启动过程，并且会验证分发点上的所有内容。  

    -   你还可以配置“内容验证优先级” 。  

    -   若要查看内容验证过程的结果，请在 Configuration Manager 控制台中，导航到“监视” > “分发状态” > “内容状态”。 将显示每种包类型（例如，应用程序、软件更新包以及启动映像）的内容。  

10. 在“边界组”页上，管理此分发点分配到的边界组：  

    -   在内容部署过程中，客户端必须位于与分发点关联的边界组中，才能将其用作内容的源位置。  

    -   你可以选择“允许内容源位置回退”  选项，以便在没有首选分发点可用时让这些边界组外部的客户端回退并使用分发点作为内容的源位置。  

     有关首选分发点的详细信息，请参阅[内容管理的基本概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)主题。  

11. 在“摘要”页上，验证设置，然后选择“下一步”以安装辅助站点。 当向导显示“完成”页面时，可以关闭向导。 辅助站点安装将在后台继续进行。  


### <a name="bkmk_verify"></a>验证辅助站点安装状态  

1.  在 Configuration Manager 控制台中，导航到“管理” > “站点配置” > “站点”。  

2.  选择要安装的辅助站点服务器，然后选择“显示安装状态”。  

    > [!TIP]  
    > 同时安装多个辅助站点时，必备组件检查程序一次针对一个站点运行，且必须在完成一个站点后才可开始检查下一站点。  
