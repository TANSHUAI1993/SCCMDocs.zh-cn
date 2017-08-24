---
title: "配置报表 | Microsoft 文档"
description: "阅读有关如何在 Configuration Manager 层次结构中设置报表，包括 SQL Server Reporting Services 的信息。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 7ae6bac23e585d6f61aff0f3155d050f1b537620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>配置 System Center Configuration Manager 中的报表

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 控制台中创建、修改和运行报表之前，必须执行许多配置任务。 使用本主题中的下列部分帮助在 Configuration Manager 层次结构中配置报表：  

 在层次结构中继续安装和配置 Reporting Services 之前，请查看以下 Configuration Manager 报表主题：  

-   [System Center Configuration Manager 中的报表简介](../../../core/servers/manage/introduction-to-reporting.md)  

-   [规划 System Center Configuration Manager 中的报表](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services 是基于服务器的报表平台，它为各种数据源提供综合性报表功能。 Configuration Manager 中的 Reporting Services 点与 SQL Server Reporting Services 通信，以将 Configuration Manager 报表复制到指定的报表文件夹，配置 Reporting Services 设置以及配置 Reporting Services 安全设置。 Reporting Services 连接到 Configuration Manager 站点数据库，以检索运行报表时返回的数据。  

 在 Configuration Manager 站点中安装 Reporting Services 点之前，必须在托管 Reporting Services 点站点系统角色的站点系统上安装和配置 SQL Server Reporting Services。 有关安装 Reporting Services 的信息，请参阅 [SQL Server TechNet Library（SQL Server TechNet 库）](http://go.microsoft.com/fwlink/p/?LinkId=266389)。  

 使用以下过程验证 SQL Server Reporting Services 是否已安装并且正确运行。  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>验证 SQL Server Reporting Services 是否已安装并且正在运行  

1.  在桌面上依次单击“开始”、“所有程序”、“Microsoft SQL Server 2008 R2”、“配置工具”和“Reporting Services Configuration Manager”。  

2.  在“Reporting Services 配置连接”对话框中，指定承载 SQL Server Reporting Services 的服务器的名称，在菜单上，选择在其上安装了 SQL Reporting Services 的 SQL Server 的实例，然后单击“连接”。 此时将打开 Reporting Services Configuration Manager。  

3.  在“报表服务器状态”页上，验证“报表服务状态”是否设置为“已启动”。 如果没有，请单击“启动”。  

4.  在“Web 服务 URL”页上，单击“Report Service Web 服务 URL”中的 URL 以测试报表文件夹连接。 此时可能会打开“Windows 安全”对话框并提示你输入安全凭据。 默认情况下，将显示你的用户帐户。 输入你的密码，然后单击“确定”。 验证是否成功地打开了该网页。 关闭浏览器窗口。  

5.  在“数据库”页上，使用“本机”验证是否已配置“报表服务器模式”设置。  

6.  在“报表管理器 URL”页上，单击“报表管理器站点标识”中的 URL 以测试报表管理器虚拟目录连接。 此时可能会打开“Windows 安全”对话框并提示你输入安全凭据。 默认情况下，将显示你的用户帐户。 输入你的密码，然后单击“确定”。 验证是否成功地打开了该网页。 关闭浏览器窗口。  

    > [!NOTE]  
    >  Configuration Manager 中的报表不需要 Reporting Services 报表管理器，但是如果想要在 Internet 浏览器上运行报表或使用报表管理器管理报表，则需要它。  

7.  单击“退出”以关闭 Reporting Services 配置管理器。  

##  <a name="BKMK_ReportBuilder3"></a>将报表配置为使用报表生成器 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>将报表生成器清单名称更改为 Report Builder 3.0 的报表生成器清单名称  

1.  在运行 Configuration Manager 控制台的计算机上打开 Windows 注册表编辑器。  

2.  浏览到“HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting”。  

3.  双击“ReportBuilderApplicationManifestName”项以编辑值数据。  

4.  将“ReportBuilder_2_0_0_0.application”更改为“ReportBuilder_3_0_0_0.application”，然后单击“确定”。  

5.  关闭 Windows 注册表编辑器。  

##  <a name="BKMK_InstallReportingServicesPoint"></a>安装 Reporting Services 点  
 必须在站点上安装 Reporting Services 点以管理该站点上的报表。 Reporting Services 点将报表文件夹和报表复制到 SQL Server Reporting Services，对报表和文件夹应用安全策略，并在 Reporting Services 中设置配置设置。 在 Configuration Manager 控制台中显示报表之前，以及在 Configuration Manager 中管理报表之前，必须配置 Reporting Services 点。 Reporting Services 点是必须在安装并运行 Microsoft SQL Server Reporting Services 的服务器上配置的站点系统角色。 有关先决条件的详细信息，请参阅[报表的先决条件](prerequisites-for-reporting.md)。  

> [!IMPORTANT]  
>  选择站点以安装 Reporting Services 点时，请记住将访问报表的用户所在的安全作用域必须与安装 Reporting Services 点所在的站点的安全作用域相同。  

> [!NOTE]  
>  在站点系统上安装 Reporting Services 点之后，请不要更改报表服务器的 URL。 例如，创建 Reporting Services 点，然后在 Reporting Services Configuration Manager 中修改报表服务器的 URL，则 Configuration Manager 控制台将继续使用旧的 URL，并且你无法从控制台中运行、编辑或创建报表。 如果必须更改报表服务器的 URL，请删除 Reporting Services 点，更改 URL，然后重新安装 Reporting Services 点。  

> [!IMPORTANT]    
> 安装 Reporting Services 点时，必须指定 Reporting Services 点帐户。 之后，来自不同域的用户在尝试运行报表时，报表将无法运行，除非域间建立起双向信任。

 使用以下过程来安装 Reporting Services 点。  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>在站点系统上安装 Reporting Services 点  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”工作区中，展开“站点配置”，然后单击“服务器和站点系统角色”。  

    > [!TIP]  
    >  要仅列出承载 Reporting Services 点站点角色的站点系统，请右键单击“服务器和站点系统角色”以选择“Reporting Services 点”。  

3.  使用关联的步骤将 Reporting Services 点站点系统角色添加到新的或现有的站点系统服务器：  

    > [!NOTE]  
    >  有关配置站点系统的详细信息，请参阅[为 Center Configuration Manager 添加站点系统角色](../deploy/configure/add-site-system-roles.md)。  

    -   **新建站点系统**：在“主页”选项卡的“创建”组中，单击“创建站点系统服务器”。 “创建站点系统服务器向导”将会打开。  

    -   “现有站点系统”：单击要在其上安装 Reporting Services 点站点系统角色的服务器。 单击服务器时，会在结果窗格中显示服务器上已经安装的站点系统角色的列表。  

         在“主页”选项卡上的“服务器”组中，单击“添加站点系统角色”。 “添加站点系统角色向导”将会打开。  

4.  在“常规”页上，指定站点系统服务器的一般设置。 向现有站点系统服务器添加 Reporting Services 点时，请验证以前配置的值。  

5.  在“系统角色选择”页上的可用角色列表中选择“Reporting Services 点”，然后单击“下一步”。  

6.  在“Reporting Services 点”页上配置下列设置：  

    -   **站点数据库服务器名称**：指定托管 Configuration Manager 站点数据库的服务器名称。 通常，向导会自动检索服务器的完全限定的域名 (FQDN)。 要指定数据库实例，请使用格式 &lt;*服务器名称*>\&lt;*实例名称*>。  

    -   **数据库名称**：指定 Configuration Manager 站点数据库的名称，然后单击“验证”以确认向导具有访问站点数据库的权限。  

        > [!IMPORTANT]  
        >  将要创建 Reporting Services 点的用户帐户必须对站点数据库具有“读取”访问权限。 如果连接测试失败，则会出现一个红色警告图标。 将光标移到此图标之上以阅读失败的详细信息。 更正该失败，然后再次单击“测试”。  

    -   **文件夹名称**：指定所创建且用于托管 Reporting Services 中的 Configuration Manager 报表的文件夹名称。  

    -   “Reporting Services 服务器实例”：在 Reporting Services 的 SQL Server 实例列表中进行选择。 只发现一个实例时，默认情况下会列出并选择该实例。 如果未发现实例，请验证是否安装和配置了 SQL Server Reporting Services，并且是否在站点系统上启动了 SQL Server Reporting Services 服务。  

        > [!IMPORTANT]  
        >  Configuration Manager 在当前用户上下文中连接至所选站点系统上的 Windows Management Instrumentation (WMI)，以检索 Reporting Services 的 SQL Server 实例。 当前用户必须对站点系统上的 WMI 具有“读取”访问权限，否则将无法检索 Reporting Services 实例。  

    -   **Reporting Services 点帐户**：单击“设置”，然后选择在 Reporting Services 点上的 SQL Server Reporting Services 连接到 Configuration Manager 站点数据库时要使用的帐户，以检索报表中显示的数据。 选择“现有帐户”以指定以前配置为 Configuration Manager 帐户的 Windows 用户帐户，或者选择“新帐户”以指定当前未配置为 Configuration Manager 帐户的 Windows 用户帐户。 Configuration Manager 会自动授予指定用户访问站点数据库的权限。 “管理”工作区内“安全”节点的“帐户”子文件夹中会显示该帐户，以及“ConfigMgr Reporting Services 点”帐户名称。  

         运行 Reporting Services 的帐户必须属于域本地安全组“Windows Authorization Access Group”，并且必须为其将“读取 tokenGroupsGlobalAndUniversal”权限设置为“允许”。 必须为来自与 Reporting Services 点帐户不同域的用户建立双向信任，以便成功运行报表。

         指定 Windows 用户帐户和密码经过加密并存储在 Reporting Services 数据库中。 Reporting Services 通过使用此帐户和密码从站点数据库中检索报表的数据。  

        > [!IMPORTANT]  
        >  指定的帐户在承载 Reporting Services 数据库的计算机上必须具有“本地登录”权限。  

7.  在“Reporting Services 点”页上，单击“下一步”。  

8.  在“摘要”页上，验证设置，然后单击“下一步”以安装 Reporting Services 点。  

     向导完成后，会创建报表文件夹，并将 Configuration Manager 报表复制到指定的报表文件夹中。  

    > [!NOTE]  
    >  创建报表文件夹并将报表复制到报表服务器时，Configuration Manager 会确定适合对象的语言。 如果在站点上安装了关联的语言包，则 Configuration Manager 会采用站点报表服务器上运行的操作系统的语言创建对象。 如果该语言不可用，则会用英文创建和显示报表。 在无语言包的站点上安装 Reporting Services 点时，会安装英文报表。 如果在安装 Reporting Services 点之后安装语言包，则必须先卸载然后重新安装 Reporting Services 点，以获得采用合适语言包语言的报表。 有关语言包的详细信息，请参阅 [System Center Configuration Manager 中的语言包](../deploy/install/language-packs.md)。  

###  <a name="BKMK_FileInstallationAndSecurity"></a>文件安装和报表文件夹安全权限  
 Configuration Manager 执行以下操作来安装 Reporting Services 点以及配置 Reporting Services：  

> [!IMPORTANT]  
>  系统使用为 SMS_Executive 服务配置的帐户（通常是站点服务器本地系统帐户）的凭据来执行以下列表中的操作。  

-   安装 Reporting Services 点站点角色。  

-   使用在向导中指定的存储凭据在 Reporting Services 中创建数据源。 这是当你运行报表时 Reporting Services 用于连接到站点数据库的 Windows 用户帐户和密码。  

-   在 Reporting Services 中创建 Configuration Manager 根文件夹。  

-   在 Reporting Services 中添加“ConfigMgr 报表用户”和“ConfigMgr 报表管理员”安全角色。  

-   创建子文件夹，并将 %ProgramFiles%\SMS_SRSRP 中的Configuration Manager 报表部署到 Reporting Services。  

-   将 Reporting Services 中的 **ConfigMgr 报表用户**角色添加到 Configuration Manager中具有“站点读取”权限的所有用户帐户的根文件夹。  

-   将 Reporting Services 中的 **ConfigMgr 报表管理员**角色添加到 Configuration Manager中具有“站点修改”权限的所有用户帐户的根文件夹。  

-   检索报表文件夹与 Configuration Manager 受保护对象类型（在 Configuration Manager 站点数据库中进行维护）之间的映射。  

-   针对 Reporting Services 中的特定报表文件夹，为 Configuration Manager 中的管理用户配置以下权限：  

    -   添加用户，针对具有 Configuration Manager 对象的“运行报表”权限的管理用户，将 **ConfigMgr 报表用户**角色分配到其关联报表文件夹。  

    -   添加用户，针对具有 Configuration Manager 对象的“修改报表”权限的管理用户，将 **ConfigMgr 报表管理员**角色分配到其关联报表文件夹。  

     Configuration Manager 将连接到 Reporting Services，并对 Configuration Manager 和 Reporting Services 根文件夹和特定报表文件夹设置用户权限。 在 Reporting Services 点的初始安装后，Configuration Manager 将每隔 10 分钟连接到 Reporting Services 一次，以验证对报表文件夹配置的用户权限是否为 Configuration Manager 用户设置的关联权限。 在使用 Reporting Services 报表管理器添加用户或修改报表文件夹的用户权限时，Configuration Manager 将使用站点数据库中存储的基于角色的分配覆盖这些更改。 Configuration Manager 还会删除在 Configuration Manager 中不具有报表权限的用户。  

##  <a name="BKMK_SecurityRoles"></a>Configuration Manager 的 Reporting Services 安全角色  
 Configuration Manager 安装 Reporting Services 点时，会在 Reporting Services 中添加以下安全角色：  

-   “ConfigMgr 报表用户”：分配有此安全角色的用户只能运行 Configuration Manage 报表。  

-   “ConfigMgr 报表管理员”：分配有此安全角色的用户可执行与 Configuration Manage 中的报表相关的所有任务。  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a>验证 Reporting Services 点安装  
 添加 Reporting Services 点站点角色后，你可以通过查看特定状态消息和日志文件条目来验证安装。 使用以下过程来验证 Reporting Services 点安装是否成功。  

> [!WARNING]  
>  如果报表显示在 Configuration Manage 控制台的“监视”工作区中“报表”节点的“报表”子文件夹中，则可以跳过此过程。  

#### <a name="to-verify-the-reporting-services-point-installation"></a>验证 Reporting Services 点安装  

1.  在 Configuration Manager 控制台中，单击“监视”。  

2.  在“监视”工作区中，展开“系统状态”，然后单击“组件状态”。  

3.  在组件列表中单击“SMS_SRS_REPORTING_POINT”。  

4.  在“主页”选项卡上的“组件”组中，单击“显示消息”，然后单击“全部”。  

5.  为安装 Reporting Services 点之前的期间指定日期和时间，然后单击“确定”。  

6.  验证是否列出了状态消息 ID 1015，指明 Reporting Services 点已成功安装。 或者，可以打开位于 &lt;*ConfigMgr 安装路径*>\Logs 中的 Srsrp.log 文件，并查看“安装已成功”。  

     在 Windows 资源管理器中，导航到 &lt;*ConfigMgr 安装路径*>\Logs。  

7.  打开 Srsrp.log，并从 Reporting Services 点成功安装的时间开始逐句浏览该日志文件。 验证是否创建了报表文件夹、部署了报表并且确认了针对每个文件夹的安全策略。 在安全策略确认的最后一行之后查找“Successfully checked that the SRS web service is healthy on server”（已成功检查 SRS Web 服务在服务器上是否正常）。  

##  <a name="BKMK_Certificate"></a>为 Configuration Manager 控制台计算机配置自签名证书  
 你可以使用许多选项来创作 SQL Server Reporting Services 报表。 在 Configuration Manager 控制台中创建或编辑报表时，Configuration Manage 将打开报表生成器以用作创作环境。 无论如何创作 Configuration Manager 报表，均需一个自签名证书以便向站点数据库服务器进行服务器验证。 Configuration Manager 会将证书自动安装在站点服务器和安装了 SMS 提供程序的计算机上。 因此，当 Configuration Manager 控制台从其中一台计算机中运行时，可以直接通过该控制台创建或编辑报表。 但是，从安装在另一台计算机上的 Configuration Manager 控制台创建或修改报表时，必须从站点服务器导出证书并将其添加到运行 Configuration Manager 控制台的计算机上的**受信任人**证书存储。  

> [!NOTE]  
>  有关 SQL Server Reporting Services 的其他报表创作环境的详细信息，请参阅 SQL Server 2008 联机丛书中的 [比较报表创作环境](http://go.microsoft.com/fwlink/p/?LinkId=242805) 。  

 使用以下过程作为示例，了解如何将自签名证书的副本从站点服务器传输到运行 Configuration Manager 控制台的另一台计算机（如果两台计算机都运行 Windows Server 2008 R2）。 如果由于操作系统版本不同而无法按此过程进行操作，请参阅操作系统文档来了解等效的过程。  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>将自签名证书的副本从站点服务器传输到另一台计算机  

1.  在站点服务器上执行以下步骤以导出自签名证书：  

    1.  单击“启动”，再单击“运行”，然后键入 **mmc.exe**。 在空白控制台中，单击“文件”，然后单击“添加/删除管理单元”。  

    2.  在“添加/删除管理单元”对话框中，从“可用的管理单元”列表中选择“证书”，然后单击“添加”。  

    3.  在“证书管理单元”对话框中，选择“计算机帐户”，然后单击“下一步”。  

    4.  在“选择计算机”对话框中，确保选中“本地计算机: (运行此控制台的计算机)”，然后单击“完成”。  

    5.  在“添加/删除管理单元”对话框中，单击“确定”。  

    6.  在控制台中展开“证书(本地计算机)”，展开“受信任人”，并选择“证书”。  

    7.  右键单击友好名称为&lt;*站点服务器的 FQDN*> 的证书，单击“所有任务”，然后选择“导出”。  

    8.  通过使用默认选项完成“证书导出向导”，并使用“.cer”文件扩展名保存证书。  

2.  在运行 Configuration Manager 控制台的计算机上执行以下步骤，将自签名证书添加到“受信任人”证书存储：  

    1.  重复前面 1.a 到 1.e 的步骤 在管理点计算机上的 MMC 中配置**证书**管理单元。  

    2.  在控制台中，展开“证书(本地计算机)”，展开“受信任人”，右键单击“证书”，选择“所有任务”，然后选择“导入”以启动“证书导入向导”。  

    3.  在“要导入的文件”页上，选择在步骤 1.h 中保存的证书，然后单击“下一步”。  

    4.  在“证书存储”页上，选择“将所有的证书放入下列存储”（“证书存储”设置为“受信任人”），然后单击“下一步”。  

    5.  单击“完成”关闭向导并在计算机上完成证书配置。  

##  <a name="BKMK_ModifyReportingServicesPoint"></a>修改 Reporting Services 点设置  
 安装了 Reporting Services 点之后，你可以在 Reporting Services 点属性中修改站点数据库连接和身份验证设置。 使用以下过程来修改 Reporting Services 点设置。  

#### <a name="to-modify-reporting-services-point-settings"></a>修改 Reporting Services 点设置  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”工作区中，展开“站点配置”，然后单击“服务器和站点系统角色”以列出站点系统。  

    > [!TIP]  
    >  要仅列出承载 Reporting Services 点站点角色的站点系统，请右键单击“服务器和站点系统角色”以选择“Reporting Services 点”。  

3.  选择承载你要修改其设置的 Reporting Services 点的站点系统，然后在“站点系统角色”中选择“Reporting Services 点”。  

4.  在“站点角色”选项卡上的“属性”组中，单击“属性”。  

5.  在“Reporting Services 点属性”对话框上，你可以修改以下设置：  

    -   **站点数据库服务器名称**：指定托管 Configuration Manager 站点数据库的服务器名称。 通常，向导会自动检索服务器的完全限定的域名 (FQDN)。 要指定数据库实例，请使用格式 &lt;*服务器名称*>\&lt;*实例名称*>。  

    -   **数据库名称**：指定 System Center 2012 Configuration Manager 站点数据库的名称，然后单击“验证”以确认向导具有访问站点数据库的权限。  

        > [!IMPORTANT]  
        >  创建 Reporting Services 点的用户帐户必须具有站点数据库的“读取”访问权限。 如果连接测试失败，则会出现一个红色警告图标。 将光标移到此图标之上以阅读失败的详细信息。 更正该失败，然后再次单击“测试”。  

    -   **用户帐户**：单击“设置”，然后选择在 Reporting Services 点上的 SQL Server Reporting Services 连接到 Configuration Manager 站点数据库时要使用的帐户，以检索报表中显示的数据。 选择“现有帐户”以指定具有现有 Configuration Manager 权限的 Windows 用户帐户，或者选择“新帐户”以指定当前不具有 Configuration Manager 中权限的 Windows 用户帐户。 Configuration Manager 会自动授予指定用户帐户访问站点数据库的权限。 该帐户在“管理”工作区中“安全”节点的“帐户”子文件夹中显示为“ConfigMgr SRS 报表点”帐户。  

         指定 Windows 用户帐户和密码经过加密并存储在 Reporting Services 数据库中。 Reporting Services 通过使用此帐户和密码从站点数据库中检索报表的数据。  

        > [!IMPORTANT]  
        >  当站点数据库位于远程站点系统上时，你指定的帐户必须具有计算机的“在本机登录”权限。  

6.  单击“确定”保存更改并退出对话框。  

## <a name="upgrading-sql-server"></a>升级 SQL Server  
 升级 SQL Server 以及用作 Reporting Services 点数据源的 SQL Server Reporting Services 后，你可能会在从 Configuration Manager 控制台中运行或编辑报表时遇到错误。 要使报表从 Configuration Manager 控制台中正常工作，必须删除站点的 Reporting Services 点站点系统角色，然后再重新安装。 不过，在升级之后，你可以继续从 Internet 浏览器中成功运行和编辑报表。  

##  <a name="BKMK_ConfigureReportOptions"></a>配置报表选项  
 使用 Configuration Manager 站点的报表选项选择用于管理报表的默认 Reporting Services 点。 尽管一个站点上可以有多个 Reporting Services 点，但只会使用在报表选项中选择的默认报表服务器来管理报表。 使用以下过程来配置站点的报表选项。  

#### <a name="to-configure-report-options"></a>要配置报表选项  

1.  在 Configuration Manager 控制台中，单击“监视”。  

2.  在“监视”工作区中，展开“报表”，然后单击“报表”。  

3.  在“主页”选项卡上的“设置”组中，单击“报表选项”。  

4.  在列表中选择默认报表服务器，然后单击“确定”。 如果列表未列出任何 Reporting Services 点，请验证是否已在该站点中成功安装和配置了 Reporting Services 点。  

## <a name="next-steps"></a>后续步骤
[报表的操作和维护](operations-and-maintenance-for-reporting.md)
