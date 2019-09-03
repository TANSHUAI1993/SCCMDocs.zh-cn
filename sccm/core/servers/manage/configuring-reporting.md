---
title: 配置报表
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 层次结构中设置报表，包括 SQL Server Reporting Services 的信息。
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc84435b36fe413f9eab81ebdc0161b7cd64ab53
ms.sourcegitcommit: e2e07d74779a2f48693ecaa17a5974204949d109
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999376"
---
# <a name="configure-reporting-in-configuration-manager"></a>在 Configuration Manager 中配置报表

适用范围：  System Center Configuration Manager (Current Branch)

在 Configuration Manager 控制台中创建、修改和运行报表之前，需要完成许多配置任务。 使用本文帮助在 Configuration Manager 层次结构中配置报表。  

在层次结构中安装和配置 SQL Server Reporting Services 之前，请查看以下 Configuration Manager 报表文章：  

- [Configuration Manager 中的报表简介](/sccm/core/servers/manage/introduction-to-reporting)  

- [在 Configuration Manager 中规划报表](/sccm/core/servers/manage/planning-for-reporting)  

## <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services

SQL Server Reporting Services 是基于服务器的报表平台，它为各种类型的数据源提供综合性报表功能。 Configuration Manager 中的 Reporting Services 点与 SQL Server Reporting Services 通信，并执行以下操作：

- 将 Configuration Manager 报表复制到指定的报表文件夹
- 配置 Reporting Services 设置
- 配置 Reporting Services 安全设置

运行报表时，Reporting Services 组件连接到 Configuration Manager 站点数据库，以检索数据。  

在 Configuration Manager 站点中安装 Reporting Services 点之前，请在目标站点系统上安装和配置 SQL Server Reporting Services。 有关详细信息，请参阅[安装 SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services)。  

使用以下过程验证 SQL Server Reporting Services 是否已安装并且正确运行。  

1. 转到站点系统上的“开始”菜单，并打开“Reporting Services 配置管理器”   。 可能会在“Microsoft SQL Server”组的“配置工具”部分找到它   。

2. 在“Reporting Services 配置连接”  窗口中，输入托管 SQL Server Reporting Services 的服务器的名称。 选择在其上安装了 SQL Reporting Services 的 SQL Server 实例。 然后选择“连接”  ，打开 Reporting Services 配置管理器。  

3. 在“报表服务器状态”  页上，验证“报表服务状态”  是否为“已启动”  。 如果未处于此状态，请选择“启动”  。  

4. 在“Web 服务 URL”页上，选择“报表服务 Web 服务 URL”中的 URL   。 此操作测试与报表文件夹的连接。 浏览器可能会提示你输入凭据。 验证是否成功地打开了该网页。

5. 在“数据库”  页上，  验证“报表服务器模式”  是否设置为“本机”。  

6. 在“报表管理器 URL”页上，选择“报表管理器站点标识”中的 URL   。 此操作将测试与报表管理器的虚拟目录的连接。 浏览器可能会提示你输入凭据。 验证是否成功地打开了该网页。

    > [!NOTE]  
    > Configuration Manager 中的报表不需要 Reporting Services 报表管理器。 只有当想要在浏览器中运行报表或使用报表管理器管理报表时，才需要使用此方法。  

7. 选择“退出”  以关闭 Reporting Services 配置管理器。  

## <a name="BKMK_ReportBuilder3"></a>将报表配置为使用报表生成器 3.0

1. 在运行 Configuration Manager 控制台的计算机上打开 Windows 注册表编辑器。  

2. 浏览到“HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting”  。  

3. 打开“ReportBuilderApplicationManifestName”  项以编辑值数据。  

4. 将“ReportBuilder_2_0_0_0.application”  更改为“ReportBuilder_3_0_0_0.application”  ，然后选择“确定”  。  

5. 关闭 Windows 注册表编辑器。  

## <a name="BKMK_InstallReportingServicesPoint"></a>安装 Reporting Services 点

要管理该站点上的报表，请安装 Reporting Services 点。 Reporting Services 点将执行以下操作：

- 将报表文件夹和报表复制到 SQL Server Reporting Services
- 为报表和文件夹应用安全策略
- 在 Reporting Services 中设置配置设置

### <a name="a-namebkmk_requirements--requirements-and-limitations"></a><a name="bkmk_requirements" /> 要求和限制

在 Configuration Manager 控制台中查看或管理报表之前，需要一个 Reporting Services 点。 使用 Microsoft SQL Server Reporting Services 在服务器上配置此站点系统角色。 有关详细信息，请参阅[报表的先决条件](/sccm/core/servers/manage/prerequisites-for-reporting)。  

- 选择站点安装 Reporting Services 点时，将访问报表的用户所在的安全作用域必须与安装角色的站点的安全作用域相同。  

- 在站点系统上安装 Reporting Services 点之后，请不要更改报表服务器的 URL。

    例如，你创建 Reporting Services 点。 然后，在 Reporting Services 配置管理器中修改报表服务器的 URL。 Configuration Manager 控制台继续使用旧的 URL。 无法从控制台中运行、编辑或创建报表。

    如果需要更改报表服务器 URL，请首先删除现有的 Reporting Services 点。 更改 URL，然后重新安装 Reporting Services 点。  

- 安装 Reporting Services 点时，指定 [Reporting Services 点帐户](/sccm/core/plan-design/hierarchy/accounts#reporting-services-point-account)。 对于不同域中要运行报表的用户，请在域之间创建双向信任。 否则，报表将无法运行。

### <a name="a-namebkmk_install--install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> 在站点系统上安装 Reporting Services 点  

有关配置站点系统的详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点    。  

1. 将 Reporting Services 点添加到新的或现有站点系统服务器：  

    - *新站点系统*：在功能区的“主页”选项卡上的“创建”组中，选择“创建站点系统服务器”    。 “创建站点系统服务器向导”  将会打开。  

    - *现有站点系统*：选择目标服务器。 在功能区的“主页”选项卡上的“创建”组中，选择“创建站点系统服务器”    。 “添加站点系统角色向导”  将会打开。  

1. 在“常规”  页上，指定站点系统服务器的一般设置。 向现有服务器添加 Reporting Services 点时，请验证以前配置的值。  

1. 在“系统角色选择”  页上的可用角色列表中选择“Reporting Services 点”  ，然后选择“下一步”  。  

1. 在“Reporting Services 点”  页上配置下列设置：  

    - **站点数据库服务器名称**：指定托管 Configuration Manager 站点数据库的服务器名称。 通常，向导会检索服务器的完全限定的域名 (FQDN)。 要指定数据库实例，请使用格式 &lt;服务器名称  >\&lt;实例名称  >。 例如，`sqlserver\named1`。

    - **数据库名称**：指定 Configuration Manager 站点数据库的名称。 选择“验证”  以确认向导有权访问站点数据库。  

        > [!IMPORTANT]  
        > 用于创建 Reporting Services 点的用户帐户必须具有站点数据库的“读取”访问权限  。 如果连接测试失败，则会出现一个红色警告图标。 图标上的上下文悬停文本包含失败的详细信息。 更正该失败，然后再次选择“测试”  。  

    - **文件夹名称**：指定要创建且用于 Reporting Services 中的 Configuration Manager 报表的文件夹名称。  

    - **Reporting Services 服务器实例**：选择 Reporting Services 的 SQL Server 实例。 如果此页未列出任何实例，请验证是否已安装、配置和启动 SQL Server Reporting Services。  

        > [!IMPORTANT]  
        > Configuration Manager 在当前用户的上下文中建立与所选站点系统上的 WMI 的连接。 它使用此连接检索 Reporting Services SQL Server 的实例。 当前用户必须对站点系统上的 WMI 具有“读取”  访问权限，否则向导无法获取 Reporting Services 实例。  

    - **Reporting Services 点帐户**：选择“设置”，然后选择要使用的帐户  。 Reporting Services 点上的 SQL Server Reporting Services 使用此帐户连接到 Configuration Manager 站点数据库。 此连接用于检索报表的数据。 选择“现有帐户”以指定先前配置为 Configuration Manager 帐户的 Windows 用户帐户  。 选择“新帐户”以指定当前未配置使用的 Windows 用户帐户  。 Configuration Manager 会自动授予指定用户访问站点数据库的权限。  

        运行 Reporting Services 的帐户必须属于域本地安全组“Windows Authorization Access Group”  。 它还需要将 Read tokenGroupsGlobalAndUniversal  权限设置为“允许”  。 需要为来自与 Reporting Services 点帐户不同域的用户建立双向信任，以便成功运行报表。

        指定 Windows 用户帐户和密码经过加密并存储在 Reporting Services 数据库中。 Reporting Services 通过使用此帐户和密码从站点数据库中检索报表的数据。  

        > [!IMPORTANT]  
        > 指定的帐户在托管 Reporting Services 数据库的服务器上必须具有“本地登录”  权限。  

1. 完成向导。

向导完成后，Configuration Manager 将在 Reporting Services 中创建报表文件夹。 然后，它将其报表复制到指定的报表文件夹。  

> [!TIP]  
> 要仅列出托管 Reporting Services 点站点角色的站点系统，请右键单击“服务器和站点系统角色”  ，并选择“Reporting Services 点”  。  

### <a name="a-namebkmk_languages--languages-for-reports"></a><a name="bkmk_languages" /> 报表的语言

<!-- SCCMDocs#1067 -->

在创建报表文件夹并将报表复制到报表服务器时，Configuration Manager 会确定适合对象的语言。

- 创建报表文件夹，复制报表

  - 使用站点服务器操作系统的区域设置创建对象

  - 如果特定语言包不可用，则默认为英语 (ENU)

- 在 Web 浏览器中查看报表

  - 文件夹和报表名称：与站点服务器相同的区域设置
  
  - 报表内容：基于浏览器区域设置动态变化

- 在 Configuration Manager 控制台中查看报表

  - 文件夹和报表名称：基于控制台的区域设置动态变化
  
  - 报表内容：基于控制台的区域设置动态变化

在无语言包的站点上安装 Reporting Services 点时，会安装英文报表。 如果在安装 Reporting Services 点之后安装语言包，则必须先卸载然后重新安装 Reporting Services 点，以获得采用合适语言包语言的报表。  

有关详细信息，请参阅[语言包](/sccm/core/servers/deploy/install/language-packs)。

### <a name="BKMK_FileInstallationAndSecurity"></a>文件安装和报表文件夹安全权限

Configuration Manager 执行以下操作来安装 Reporting Services 点以及配置 Reporting Services：  

> [!IMPORTANT]  
> 站点在为 SMS_Executive 服务配置的帐户的上下文中执行这些操作。 通常，此帐户是站点服务器本地系统帐户。  

- 安装 Reporting Services 点站点角色。  

- 使用在向导中指定的存储凭据在 Reporting Services 中创建数据源。 此帐户是当你运行报表时 Reporting Services 用于连接到站点数据库的 Windows 用户帐户和密码。  

- 在 Reporting Services 中创建 Configuration Manager 根文件夹。  

- 在 Reporting Services 中添加“ConfigMgr 报表用户”  和“ConfigMgr 报表管理员”  安全角色。  

- 创建子文件夹，然后将站点服务器上 `%ProgramFiles%\SMS_SRSRP` 的 Configuration Manager 报表部署到 Reporting Services。  

- 将 Reporting Services 中的“ConfigMgr 报表用户”  角色添加到 Configuration Manager 中具有“站点读取”  权限的所有用户帐户的根文件夹。  

- 将 Reporting Services 中的“ConfigMgr 报表管理员”  角色添加到 Configuration Manager 中具有“站点修改”  权限的所有用户帐户的根文件夹。  

- 检索报表文件夹与 Configuration Manager 安全对象类型之间的映射。 Configuration Manager 将在站点数据库中维护此映射。  

- 针对 Reporting Services 中的特定报表文件夹，为 Configuration Manager 中的管理用户配置以下权限：  

  - 添加用户，针对具有 Configuration Manager 对象的“运行报表”  权限的管理用户，将“ConfigMgr 报表用户”  角色分配到其关联报表文件夹。  

  - 添加用户，针对具有 Configuration Manager 对象的“修改报表”  权限的管理用户，将“ConfigMgr 报表管理员”  角色分配到其关联报表文件夹。  

Configuration Manager 将连接到 Reporting Services，并对 Configuration Manager 和 Reporting Services 根文件夹和特定报表文件夹设置用户权限。 在 Reporting Services 点的初始安装后，Configuration Manager 将每隔 10 分钟连接到 Reporting Services 一次，以验证对报表文件夹配置的用户权限是否为 Configuration Manager 用户设置的关联权限。 在使用 Reporting Services 报表管理器添加用户或修改报表文件夹的用户权限时，Configuration Manager 将使用站点数据库中存储的基于角色的分配覆盖这些更改。 Configuration Manager 还会删除在 Configuration Manager 中不具有报表权限的用户。  

### <a name="BKMK_SecurityRoles"></a> Reporting Services 安全角色

Configuration Manager 安装 Reporting Services 点时，会在 Reporting Services 中添加以下安全角色：  

- **ConfigMgr 报表用户**：分配有此安全角色的用户只能运行 Configuration Manager 报表。  

- **ConfigMgr 报表管理员**：分配有此安全角色的用户可执行与 Configuration Manager 中的报表相关的所有任务。  

## <a name="BKMK_VerifyReportingServicesPointInstallation"></a> 验证安装

通过查看特定状态消息和日志文件条目来验证 Reporting Services 点的安装。 使用以下过程来验证 Reporting Services 点安装是否成功。  

> [!Note]  
> 如果在 Configuration Manage 控制台的“监视”  工作区中“报表”  节点的“报表”  子文件夹中看到此报表，则可以跳过此过程。

### <a name="verify-installation-by-status-message"></a>通过状态消息验证安装

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“组件状态”节点    。  

1. 选择 SMS_SRS_REPORTING_POINT  组件。  

1. 在功能区“主页”  选项卡上的“组件”  组中，选择“显示消息”  ，然后选择“全部”  。  

1. 为安装 Reporting Services 点之前的期间指定日期和时间，然后选择“确定”  。  

1. 验证状态消息 ID 1015  。 此状态消息指示 Reporting Services 点已成功安装。

### <a name="verify-installation-by-log-file"></a>通过日志文件验证安装

打开位于 Configuration Manager 安装路径的“日志”目录中的 Srsrp.log 文件   。 查找字符串 `Installation was successful`。

从 Reporting Services 点成功安装的时间开始逐句浏览此日志文件。 验证是否创建了报表文件夹、部署了报表并且确认了针对每个文件夹的安全策略。 在最后一行安全策略确认之后，查找字符串 `Successfully checked that the SRS web service is healthy on server`。  

## <a name="BKMK_Certificate"></a> 配置证书以创作报表

可以使用许多选项在 SQL Server Reporting Services 中创作报表。 在 Configuration Manager 控制台中创建或编辑报表时，Configuration Manage 将打开报表生成器以用作创作环境。 无论如何创作 Configuration Manager 报表，均需一个自签名证书以便向站点数据库服务器进行服务器身份验证。

> [!NOTE]  
> 若要详细了解如何使用 SQL Server Reporting Services 创作报表，请参阅[报表生成器创作环境](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs)。  

Configuration Manager 会将证书自动安装在站点服务器和任何 SMS 提供程序角色上。 当 Configuration Manager 控制台从其中一台服务器中运行时，可以直接通过该控制台创建或编辑报表。

从其他计算机上的 Configuration Manager 控制台创建或修改报表时，请从站点服务器导出证书。 特定证书的友好名称是本地计算机“受信任人”证书存储中站点服务器的 FQDN  。 在运行 Configuration Manager 控制台的计算机上，将此证书添加到“受信任人”证书存储  。  

## <a name="BKMK_ModifyReportingServicesPoint"></a> 修改 Reporting Services 点设置

安装此角色之后，可以在 Reporting Services 点属性中修改站点数据库连接和身份验证设置。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点    。  

    > [!TIP]  
    > 要仅列出托管 Reporting Services 点的站点系统，请右键单击“服务器和站点系统角色”节点  ，并选择“Reporting Services 点”  。  

1. 选择托管 Reporting Services 点的站点系统。 然后在详细信息窗格中选择“Reporting Services 点”站点系统角色  。

1. 在功能区“站点角色”  选项卡的“属性”  组中，选择“属性”  。  

1. 在“Reporting Services 点属性”  中，可以修改以下设置：  

    - **站点数据库服务器名称**

    - **数据库名称**

    - **用户帐户**

1. 选择“确定”保存所做的更改并关闭属性  。  

有关这些设置的详细信息，请参阅[在站点系统上安装 Reporting Services 点](#bkmk_install)一节中的说明。

## <a name="a-namebkmk_upgradesql--upgrade-sql-server"></a><a name="bkmk_upgradesql" /> 升级 SQL Server

要升级 SQL Server 和 SQL Server Reporting Services，请首先从站点中删除 Reporting Services 点。 升级 SQL Server 之后，请在 Configuration Manager 中重新安装 Reporting Services 点。

如果未执行此过程，则在从 Configuration Manager 控制台运行或编辑报表时，会看到错误。 可以继续从 Web 浏览器中成功运行和编辑报表。  

## <a name="BKMK_ConfigureReportOptions"></a>配置报表选项

可以选择用于管理报表的默认 Reporting Services 点。 站点可以有多个 Reporting Services 点，但它只使用默认服务器来管理报表。 使用以下过程来配置站点的报表选项。  

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”，然后选择“报表”节点    。  

1. 在功能区“主页”  选项卡的“设置”  组中，选择“报表选项”  。  

1. 在列表中选择默认报表服务器，然后选择“确定”  。

如果未显示任何服务器，请验证是否在站点中安装和配置了 Reporting Services 点。 有关详细信息，请参阅[验证安装](#BKMK_VerifyReportingServicesPointInstallation)。

请确保计算机运行的 SQL Server 报表生成器的版本与你用于报表服务器的 SQL Server 版本相匹配。 否则，将看到一个错误，默认报表服务器不会保存，并且你无法创建或编辑报表。<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>后续步骤

[报表的操作和维护](/sccm/core/servers/manage/operations-and-maintenance-for-reporting)
