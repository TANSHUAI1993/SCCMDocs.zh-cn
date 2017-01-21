---
title: "安装程序命令行选项 | Microsoft Docs"
description: "使用本文中的信息从命令行配置脚本或安装 System Center Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f2b5a1dfa654a30e03bce2b56100bc876358c9fe

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>System Center Configuration Manager 的适用于安装程序的命令行选项

*适用范围：System Center Configuration Manager (Current Branch)*


 在从命令行配置脚本或安装 System Center Configuration Manager 时，请使用下表中的信息。  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a>适用于安装程序的命令行选项  
 **/DEINSTALL**  
 卸载站点。 必须从站点服务器计算机中运行安装程序。  

 **/DONTSTARTSITECOMP**  
 安装站点，但是阻止站点组件管理器服务启动。 在站点组件管理器服务启动之前，该站点未处于活动状态。 站点组件管理器负责在站点安装和启动 SMS_Executive 服务以及其他进程。 站点安装完成之后，如果你启动站点组件管理器服务，则它将安装 SMS_Executive 以及站点运行所需的其他进程。  

 **/HIDDEN**  
 在安装过程中隐藏用户界面。 此选项必须与 **/SCRIPT** 选项结合使用，并且无人参与的脚本文件必须提供所有必需的选项，否则安装程序将失败。  

 **/NOUSERINPUT**  
 在安装过程中禁用用户输入，但显示“安装向导”  界面。 此选项必须与 **/SCRIPT** 选项结合使用，并且无人参与的脚本文件必须提供所有必需的选项，否则安装程序将失败。  

 **/RESETSITE**  
 执行站点重置，该操作将重置站点的数据库和服务帐户。 必须从站点服务器上的 **&lt;ConfigMgrInstallationPath\>\BIN\X64** 中运行安装程序。 有关站点重置的详细信息，请参阅[修改 System Center Configuration Manager 基础结构](../../../../core/servers/manage/modify-your-infrastructure.md)主题中的[运行站点重置](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset)部分。  

 **/TESTDBUPGRADE &lt;*InstanceName\DatabaseName*>**  
 对站点数据库的备份执行测试以确保它能够升级。 你必须提供站点数据库的实例名称和数据库名称。 如果仅指定数据库名称，安装程序将使用默认实例名称。  

> [!IMPORTANT]  
>  不支持在生产站点数据库上运行此命令行选项。 执行此操作会升级站点数据库，并可能导致你的站点无法运行。  

 **/UPGRADE**  
 运行站点的无人参与升级。 在使用 /UPGRADE 时，你还必须指定产品密钥，包括短划线 (-)。 此外，你必须指定以前下载的安装程序先决条件文件的路径。  

 示例：**setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;内部组件文件路径\>**  

 有关安装程序的先决条件文件的详细信息，请参见此主题中的  [安装程序下载程序](#bkmk_SetupDownloader) 部分。  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 执行无人参与的安装。在使用 **/SCRIPT** 选项时，需要一个安装程序初始化文件。 有关如何运行无人参与的安装程序的详细信息，请参阅[使用命令行安装站点](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)。  

 **/SDKINST &lt;*FQDN*>**  
 在指定计算机上安装 SMS 提供程序。 你必须提供 SMS 提供程序计算机的 FQDN。 有关 SMS 提供程序的详细信息，请参阅[为 System Center Configuration Manager 规划 SMS 提供程序](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)。  

 **/SDKDEINST &lt;*FQDN*>**  
 在指定计算机上卸载 SMS 提供程序。 你必须提供 SMS 提供程序计算机的 FQDN。  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
 管理安装在以前安装的站点上的语言。要使用此选项，必须从站点服务器上的 **&lt;ConfigMgrInstallationPath\>\BIN\X64** 中运行安装程序，并提供包含语言设置的语言脚本文件的位置。 有关语言安装程序脚本文件中可用的语言选项的详细信息，请参阅本主题中的 [用于管理语言的命令行选项](#bkmk_Lang) 部分。  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a>用于管理语言的命令行选项  
 **标识**  

-   **项名称：**Action  

    -   **是否必需：** 是  

    -   **值：**ManageLanguages  

    -   **详细信息：**管理站点上的服务器、客户端和移动客户端语言支持。  

**选项**  

-   **项名称：**AddServerLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的服务器语言。 默认情况下使用英语。  

-   **项名称：**AddClientLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定将可供客户端计算机使用的语言。 默认情况下使用英语。  

-   **项名称：**DeleteServerLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定将不再可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的要删除的语言。 默认情况下使用英语，因此无法删除它。  

-   **项名称：**DeleteClientLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定将不再可用于客户端计算机的要删除的语言。 默认情况下使用英语，因此无法删除它。  

-   **项名称：**MobileDeviceLanguage  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装移动设备客户端语言。  

-   **项名称：**PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。  

-   **项名称：**PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a>无人参与安装程序脚本文件项  
 使用下列部分来帮助你为无人参与安装程序创建脚本。 表格列出了可用的安装程序脚本项、其对应的值、是否需要它们、它们用于哪种安装类型以及项的简要描述。  

### <a name="unattended-install-for-a-central-administration-site"></a>中心管理站点的无人参与安装  
 使用下列详细信息通过无人参与的安装程序脚本文件来安装管理中心站点。  

**标识**  

-   **项名称：**Action  

    -   **是否必需：** 是  

    -   **值：**InstallCAS  

    -   **详细信息：**安装管理中心站点。  

**选项**  

-   **项名称：**ProductID  

    -   **是否必需：** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **详细信息：**指定 Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 以安装 Configuration Manager 的评估版。  

-   **项名称：**SiteCode  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteCode*>  

    -   **详细信息：**指定三个字母数字字符，以唯一标识层次结构中的站点。  

-   **项名称：**SiteName  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteName*>  

    -   **详细信息：**指定此站点的名称。  

-   **项名称：**SMSInstallDir  

    -   **是否必需：** 是  

    -   **值：***ConfigMgrInstallationPath*  

    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。  

-   **项名称：**SDKServer  

    -   **是否必需：** 是  

    -   **值：**&lt;SMS 提供程序的 FQDN>  

    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。  
        你可以在初始安装后为站点配置其他 SMS 提供程序。  

-   **项名称：**PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。  

-   **项名称：**PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

-   **项名称：**AdminConsole  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装 Configuration Manager 控制台。  

-   **项名称：**JoinCEIP  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **详细信息：** 指定是否加入客户体验改善计划。  

-   **项名称：**AddServerLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的服务器语言。 默认情况下使用英语。  

-   **项名称：**AddClientLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定将可供客户端计算机使用的语言。 默认情况下使用英语。  

-   **项名称：**DeleteServerLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**在安装站点后对其进行修改。  
        指定将不再可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的要删除的语言。 默认情况下使用英语，因此无法删除它。  

-   **项名称：**DeleteClientLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**在安装站点后对其进行修改。  
        指定将不再可用于客户端计算机的要删除的语言。 默认情况下使用英语，因此无法删除它。  

-   **项名称：**MobileDeviceLanguage  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装移动设备客户端语言。  

**SQLConfigOptions**  

-   **项名称：**SQLServerName  

    -   **是否必需：** 是  

    -   **值：***SQLServerName*  

    -   **详细信息：**指定运行 SQL Server 的服务器或群集实例的名称。 它将承载站点数据库。  

-   **项名称：**DatabaseName  

    -   **是否必需：** 是  

    -   **值：***&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **详细信息：**  

         指定要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。  

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。  

-   **项名称：**SQLSSBPort  

    -   **是否必需：** 否  

    -   **值：**&lt;*SSBPortNumber*>  

    -   **详细信息：**指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。  

-   **项名称：**SQLDataFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库 .MDB 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .MDB 文件的替代位置。  

-   **项名称：**SQLLogFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库.LDF 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .LDF 文件的替代位置。  

**CloudConnectorOptions**  

-   **项名称：**CloudConnector  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否将在此站点上安装服务连接点。 因为服务连接点只能安装在层次结构的顶层站点上，此值对子主站点必须为 0。  

-   **项名称：**CloudConnectorServer  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;服务连接点服务器 FQDN>  

    -   **详细信息：**指定将承载服务连接点站点系统角色的服务器的 FQDN。  

-   **项名称：**UseProxy  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定服务连接点是否将使用代理服务器。  

-   **项名称：**ProxyName  

    -   **是否必需：**当 UseProxy 等于 1 时需要  

    -   **值：**&lt;代理服务器 FQDN>  

    -   **详细信息：**指定将用于服务连接点站点系统角色的代理服务器的 FQDN。  

-   **项名称：**ProxyPort  

    -   **是否必需：**当 UseProxy 等于 1 时需要  

    -   **值：**&lt;*PortNumber*>  

    -   **详细信息：**指定要使用的端口号。  

### <a name="unattended-install-for-a-primary-site"></a>主站点的无人参与安装  
使用下列详细信息通过无人参与的安装程序脚本文件来安装主站点。  

使用下列详细信息通过无人参与的安装程序脚本文件来安装管理中心站点。  

**标识**  

-   **项名称：**Action  

    -   **是否必需：** 是  

    -   **值：**InstallPrimarySite  

    -   **详细信息：**安装主站点。  

**选项**  

-   **项名称：**ProductID  

    -   **是否必需：** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **详细信息：**指定 Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 以安装 Configuration Manager 的评估版。  

-   **项名称：**SiteCode  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteCode*>  

    -   **详细信息：**指定三个字母数字字符，以唯一标识层次结构中的站点。  

-   **项名称：**SiteName  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteName*>  

    -   **详细信息：**指定此站点的名称。  

-   **项名称：**SMSInstallDir  

    -   **是否必需：** 是  

    -   **值：***ConfigMgrInstallationPath*  

    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。  

-   **项名称：**SDKServer  

    -   **是否必需：** 是  

    -   **值：**&lt;SMS 提供程序的 FQDN>  

    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。  
        你可以在初始安装后为站点配置其他 SMS 提供程序。  

-   **项名称：**PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。  

-   **项名称：**PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

-   **项名称：**AdminConsole  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装 Configuration Manager 控制台。  

-   **项名称：**JoinCEIP  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **详细信息：** 指定是否加入客户体验改善计划。  

-   **项名称：**ManagementPoint  

    -   **是否必需：** 否  

    -   **值：** &lt;*Management point site server FQDN*>  

    -   **详细信息：**指定将承载管理点站点系统角色的服务器的 FQDN。  

-   **项名称：**ManagementPointProtocol  

    -   **是否必需：** 否  

    -   **值：**HTTPS 或 HTTP  

    -   **详细信息：**指定要用于管理点的协议。  

-   **项名称：**DistributionPoint  

    -   **是否必需：** 否  

    -   **值：** &lt;*Distribution Point site server FQDN*>  

    -   **详细信息：**指定要用于管理点的协议。  

-   **项名称：**DistributionPointProtocol  

    -   **是否必需：** 否  

    -   **值：**HTTPS 或 HTTP  

    -   **详细信息：**指定要用于分发点的协议。  

-   **项名称：**RoleCommunicationProtocol  

    -   **是否必需：** 是  

    -   **值：**EnforceHTTPS 或 HTTPorHTTPS  

    -   **详细信息：**指定是将所有站点系统配置为仅接受来自客户端的 HTTPS 通信，还是为每个站点系统角色配置通信方法。 如果选择“EnforceHTTPS” ，则客户端计算机必须具有有效的 PKI 证书以进行客户端身份验证。  

-   **项名称：**ClientsUsePKICertificate  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不使用  

         1 = 使用  

    -   **详细信息：**指定客户端是否将使用客户端 PKI 证书与站点系统角色通信。  

-   **项名称：**AddServerLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的服务器语言。 默认情况下使用英语。  

-   **项名称：**AddClientLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**指定将可供客户端计算机使用的语言。 默认情况下使用英语。  

-   **项名称：**DeleteServerLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**在安装站点后对其进行修改。  
        指定将不再可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的要删除的语言。 默认情况下使用英语，因此无法删除它。  

-   **项名称：**DeleteClientLanguages  

    -   **是否必需：** 否  

    -   **值：**DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    -   **详细信息：**在安装站点后对其进行修改。  
        指定将不再可用于客户端计算机的要删除的语言。 默认情况下使用英语，因此无法删除它。  

-   **项名称：**MobileDeviceLanguage  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装移动设备客户端语言。  

**SQLConfigOptions**  

-   **项名称：**SQLServerName  

    -   **是否必需：** 是  

    -   **值：***SQLServerName*  

    -   **详细信息：**指定运行 SQL Server 的服务器或群集实例的名称。 它将承载站点数据库。  

-   **项名称：**DatabaseName  

    -   **是否必需：** 是  

    -   **值：***&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **详细信息：**  

         指定要创建或用于安装主站点数据库的 SQL Server 数据库的名称。  

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。  

-   **项名称：**SQLSSBPort  

    -   **是否必需：** 否  

    -   **值：**&lt;*SSBPortNumber*>  

    -   **详细信息：**指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。  

-   **项名称：**SQLDataFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库 .MDB 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .MDB 文件的替代位置。  

-   **项名称：**SQLLogFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库.LDF 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .LDF 文件的替代位置。  

**HierarchyExpansionOption**  

-   **项名称：**CCARSiteServer  

    -   **是否必需：** 否  

    -   **值：** &lt;管理中心站点的 FQDN>  

    -   **详细信息：**指定主站点加入 Configuration Manager 层次结构时将要附加到的管理中心站点。 必须在安装过程中指定管理中心站点。  

-   **项名称：**CASRetryInterval  

    -   **是否必需：** 否  

    -   **值：**&lt;Interval>  

    -   **详细信息：** 指定连接失败后尝试连接到管理中心站点的重试间隔（以分钟为单位）。 例如，如果连接到管理中心站点失败，则主站点将等待你为 CASRetryInterval 指定的分钟数，然后重新尝试连接。  

-   **项名称：**WaitForCASTimeout  

    -   **是否必需：** 否  

    -   **值：** &lt;Timeout>  

         0 到 100 的值  

    -   **详细信息：**指定主站点连接到管理中心站点的最大超时值（以分钟为单位）。 例如，如果主站点未能连接到管理中心站点，则在达到 WaitForCASTimeout 期间之前，主站点将基于 CASRetryInterval 重新尝试连接到管理中心站点。 你可以指定 0 到 100 的值。  

**CloudConnectorOptions**  

-   **项名称：**CloudConnector  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否将在此站点上安装服务连接点。 因为服务连接点只能安装在层次结构的顶层站点上，此值对子主站点必须为 0。  

-   **项名称：**CloudConnectorServer  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;服务连接点服务器 FQDN\>  

    -   **详细信息：**指定将承载服务连接点站点系统角色的服务器的 FQDN。  

-   **项名称：**UseProxy  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定服务连接点是否将使用代理服务器。  

-   **项名称：**ProxyName  

    -   **是否必需：**当 UseProxy 等于 1 时需要  

    -   **值：**&lt;代理服务器 FQDN>  

    -   **详细信息：**指定将用于服务连接点站点系统角色的代理服务器的 FQDN。  

-   **项名称：**ProxyPort  

    -   **是否必需：**当 UseProxy 等于 1 时需要  

    -   **值：**&lt;*PortNumber*>  

    -   **详细信息：**指定要使用的端口号。  

### <a name="unattended-recovery-for-a-central-administration-site"></a>中心管理站点的无人参与恢复  
 使用下列详细信息通过无人参与的安装程序脚本文件来恢复管理中心站点。  

**标识**  

-   **项名称：**Action  

    -   **是否必需：** 是  

    -   **值：** RecoverCCAR  

    -   **详细信息：**恢复管理中心站点。  

**RecoveryOptions**  

-   **项名称：**ServerRecoveryOptions  

    -   **是否必需：** 是  

    -   **值：** 1、2 或 4  

         1 = 恢复站点服务器和 SQL Server。  

         2 = 仅恢复站点服务器。  

         4 = 仅恢复 SQL Server。  

    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：  

        -   值 = 1：你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

        -   值 = 2：你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

        -   值 = 4：如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置值 **10** ，则需要 **BackupLocation** 项。  

-   **项名称：**DatabaseRecoveryOptions  

    -   **是否必需：**当 ServerRecoveryOptions 设置的值为 **1** 或 **4** 时，需要此项。  

    -   **值：** 10、20、40、80  

         10 = 从备份中还原站点数据库。  

         20 = 使用已通过另一种方法手动恢复的站点数据库。  

         40 = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  

         80 = 跳过数据库恢复。  

    -   **详细信息：**指定安装程序如何恢复 SQL Server 中的站点数据库。  

-   **项名称：**ReferenceSite  

    -   **是否必需：**当 **DatabaseRecoveryOptions** 设置的值为 **40** 时，需要此项。  

    -   **值：**&lt;*ReferenceSiteFQDN*>  

    -   **详细信息：** 指定在数据库备份早于更改跟踪保持期或者在没有备份的情况下恢复站点时，管理中心站点用于恢复全局数据的引用主站点。  

         如果未指定引用站点，并且备份早于更改跟踪保持期，则会使用管理中心站点中的还原数据重新初始化所有主站点。  

         如果未指定引用站点，并且备份在更改跟踪保持期中，则从主站点中仅复制备份以后的更改。 如果不同的主站点中具有冲突的更改，则管理中心站点使用它收到的第一个更改。  

-   **项名称：**SiteServerBackupLocation  

    -   **是否必需：** 否  

    -   **值：**&lt;*PathToSiteServerBackupSet*>  

    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

-   **项名称：**BackupLocation  

    -   **是否必需：**如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4**，并为 **DatabaseRecoveryOptions** 项配置了值 **10**，则需要此项。  

    -   &lt;*PathToSiteDatabaseBackupSet*>  

    -   **详细信息：** 指定站点数据库备份集的路径。  

**选项**  

-   **项名称：**ProductID  

    -   **是否必需：** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **详细信息：**指定 Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 以安装 Configuration Manager 的评估版。  

-   **项名称：**SiteCode  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteCode*>  

    -   **详细信息：**指定三个字母数字字符，以唯一标识层次结构中的站点。 你必须指定在发生故障之前站点使用的站点代码。 有关站点代码限制的详细信息，请参阅此主题中的 [关于站点名称和站点代码](#bkmk_codes) 部分。  

-   **项名称：**SiteName  

    -   **是否必需：** 否  

    -   **值：**&lt;*SiteName*>  

    -   **详细信息：**指定此站点的名称。  

-   **项名称：**SMSInstallDir  

    -   **是否必需：** 是  

    -   &lt;*ConfigMgrInstallationPath*>  

    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。  

-   **项名称：**SDKServer  

    -   **是否必需：** 是  

    -   **值：**&lt;SMS 提供程序的 FQDN>  

    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。 你必须指定在发生故障之前承载 SMS 提供程序的服务器。  

         你可以在初始安装后为站点配置其他 SMS 提供程序。 有关 SMS 提供程序的详细信息，请参阅[为 System Center Configuration Manager 规划 SMS 提供程序](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)。  

-   **项名称：**PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 **0**，则安装程序将下载文件。  

-   **项名称：**PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

-   **项名称：**AdminConsole  

    -   **是否必需：**当 **ServerRecoveryOptions** 设置的值为 **4**时，需要此项。  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装 Configuration Manager 控制台。  

-   **项名称：**JoinCEIP  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **详细信息：** 指定是否加入客户体验改善计划。  

**SQLConfigOptions**  

-   **项名称：**SQLServerName  

    -   **是否必需：** 是  

    -   **值：***SQLServerName*  

    -   **详细信息：**指定服务器或群集实例的名称，它们运行将承载站点数据库的 SQL Server。 你必须指定在发生故障之前承载站点数据库的同一服务器。  

-   **项名称：**DatabaseName  

    -   **是否必需：** 是  

    -   **值：***&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>\&lt;SiteDatabaseName\>*  

    -   **详细信息：**  

         指定要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 你必须指定在发生故障之前使用的同一数据库名称。  

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。  

-   **项名称：**SQLSSBPort  

    -   **是否必需：** 是  

    -   **值：**&lt;*SSBPortNumber*>  

    -   **详细信息：**指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022。 你必须指定在发生故障之前使用的相同 SSB 端口。  

-   **项名称：**SQLDataFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库 .MDB 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .MDB 文件的替代位置。  

-   **项名称：**SQLLogFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库.LDF 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .LDF 文件的替代位置。  

**CloudConnectorOptions**  

-   **项名称：**CloudConnector  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否将在此站点上安装服务连接点。 因为服务连接点只能安装在层次结构的顶层站点上，此值对子主站点必须为 0。  

-   **项名称：**CloudConnecorServer  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;服务连接点服务器 FQDN>  

    -   **详细信息：**指定将承载服务连接点站点系统角色的服务器的 FQDN。  

-   **项名称：**UseProxy  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定服务连接点是否将使用代理服务器。  

-   **项名称：**ProxyName  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;代理服务器 FQDN>  

    -   **详细信息：**指定将用于服务连接点站点系统角色的代理服务器的 FQDN。  

-   **项名称：**ProxyPort  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;*PortNumber*>  

    -   **详细信息：**指定要使用的端口号。  

### <a name="unattended-recovery-for-a-primary-site"></a>主站点的无人参与恢复  
 使用下列详细信息通过无人参与的安装程序脚本文件来恢复主站点。  

**标识**  

-   **项名称：**Action  

    -   **是否必需：** 是  

    -   **值：** RecoverPrimarySite  

    -   **详细信息：**恢复主站点。  

**RecoveryOptions**  

-   **项名称：**ServerRecoveryOptions  

    -   **是否必需：** 是  

    -   **值：** 1、2 或 4  

         1 = 恢复站点服务器和 SQL Server。  

         2 = 仅恢复站点服务器。  

         4 = 仅恢复 SQL Server。  

    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：  

        -   值 = 1：你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

        -   值 = 2：你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

        -   值 = 4：如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置值 **10** ，则需要 **BackupLocation** 项。  

-   **项名称：**DatabaseRecoveryOptions  

    -   **是否必需：**当 ServerRecoveryOptions 设置的值为 **1** 或 **4** 时，需要此项。  

    -   **值：** 10、20、40、80  

         10 = 从备份中还原站点数据库。  

         20 = 使用已通过另一种方法手动恢复的站点数据库。  

         40 = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  

         80 = 跳过数据库恢复。  

    -   **详细信息：**指定安装程序如何恢复 SQL Server 中的站点数据库。  

-   **项名称：**SiteServerBackupLocation  

    -   **是否必需：** 否  

    -   **值：**&lt;*PathToSiteServerBackupSet*>  

    -   **详细信息：**  

         指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。  

-   **项名称：**BackupLocation  

    -   **是否必需：**如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4**，并为 **DatabaseRecoveryOptions** 项配置了值 **10**，则需要此项。  

    -   &lt;*PathToSiteDatabaseBackupSet*>  

    -   **详细信息：** 指定站点数据库备份集的路径。  

**选项**  

-   **项名称：**ProductID  

    -   **是否必需：** 是  

    -   **值：***xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* 或 *Eval*  

    -   **详细信息：**指定 Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 以安装 Configuration Manager 的评估版。  

-   **项名称：**SiteCode  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteCode*>  

    -   **详细信息：**指定三个字母数字字符，以唯一标识层次结构中的站点。 你必须指定在发生故障之前站点使用的站点代码。 有关站点代码限制的详细信息，请参阅此主题中的 [关于站点名称和站点代码](#bkmk_codes) 部分。  

-   **项名称：**SiteName  

    -   **是否必需：** 否  

    -   **值：**&lt;*SiteName*>  

    -   **详细信息：**指定此站点的名称。  

-   **项名称：**SMSInstallDir  

    -   **是否必需：** 是  

    -   &lt;*ConfigMgrInstallationPath*>  

    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。  

-   **项名称：**SDKServer  

    -   **是否必需：** 是  

    -   **值：**&lt;SMS 提供程序的 FQDN>  

    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。 你必须指定在发生故障之前承载 SMS 提供程序的服务器。 你可以在初始安装后为站点配置其他 SMS 提供程序。 有关 SMS 提供程序的详细信息，请参阅[为 System Center Configuration Manager 规划 SMS 提供程序](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)。  

-   **项名称：**PrerequisiteComp  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 下载  

         1 = 已下载  

    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 **0**，则安装程序将下载文件。  

-   **项名称：**PrerequisitePath  

    -   **是否必需：** 是  

    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>  

    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。  

-   **项名称：**AdminConsole  

    -   **是否必需：**当 **ServerRecoveryOptions** 设置的值为 **4**时，需要此项。  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否安装 Configuration Manager 控制台。  

-   **项名称：**JoinCEIP  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不加入  

         1 = 加入  

    -   **详细信息：** 指定是否加入客户体验改善计划。  

**SQLConfigOptions**  

-   **项名称：**SQLServerName  

    -   **是否必需：** 是  

    -   **值：***SQLServerName*  

    -   **详细信息：**指定服务器或群集实例的名称，它们运行将承载站点数据库的 SQL Server。 你必须指定在发生故障之前承载站点数据库的同一服务器。  

-   **项名称：**DatabaseName  

    -   **是否必需：** 是  

    -   **值：**&lt;*SiteDatabaseName*\> 或                               &lt;*InstanceName*\>\\&lt;*SiteDatabaseName*\>

    -   **详细信息：**  

         指定要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 你必须指定在发生故障之前使用的同一数据库名称。  

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。  

-   **项名称：**SQLSSBPort  

    -   **是否必需：** 是  

    -   **值：**&lt;*SSBPortNumber*>  

    -   **详细信息：**指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022。 你必须指定在发生故障之前使用的相同 SSB 端口。  

-   **项名称：**SQLDataFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库 .MDB 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .MDB 文件的替代位置。  

-   **项名称：**SQLLogFilePath  

    -   **是否必需：** 否  

    -   **值：**&lt;数据库.LDF 文件的文件路径>  

    -   **详细信息：**指定创建数据库 .LDF 文件的替代位置。  

**HierarchyExpansionOptions**  

-   **项名称：**CCARSiteServer  

    -   **是否必需：**查看详细信息。  

    -   **值：** &lt;SiteCodeForCentralAdministrationSite>  

    -   **详细信息：**指定主站点加入 Configuration Manager 层次结构时将要附加到的管理中心站点。 如果在发生故障之前主站点已附加到管理中心站点，则此设置为必需。 你必须指定在发生故障之前用于管理中心站点的站点代码。  

-   **项名称：**CASRetryInterval  

    -   **是否必需：** 否  

    -   **值：**&lt;Interval>  

    -   **详细信息：** 指定连接失败后尝试连接到管理中心站点的重试间隔（以分钟为单位）。 例如，如果连接到管理中心站点失败，则主站点将等待你为 **CASRetryInterval**指定的分钟数，然后再次尝试连接。  

-   **项名称：**WaitForCASTimeout  

    -   **是否必需：** 否  

    -   **值：** &lt;Timeout>  

    -   **详细信息：**指定主站点连接到管理中心站点的最大超时值（以分钟为单位）。 例如，如果主站点未能连接到管理中心站点，则在达到“WaitForCASTimeout”  期间之前，主站点将基于“CASRetryInterval”  重新尝试连接到管理中心站点。 你可以指定 0 到 100 的值。  

**CloudConnectorOptions**  

-   **项名称：**CloudConnector  

    -   **是否必需：** 是  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定是否将在此站点上安装服务连接点。 因为服务连接点只能安装在层次结构的顶层站点上，此值对子主站点必须为 0。  

-   **项名称：**CloudConnecorServer  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;服务连接点服务器 FQDN>  

    -   **详细信息：**指定将承载服务连接点站点系统角色的服务器的 FQDN。  

-   **项名称：**UseProxy  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：** 0 或 1  

         0 = 不安装  

         1 = 安装  

    -   **详细信息：**指定服务连接点是否将使用代理服务器。  

-   **项名称：**ProxyName  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;代理服务器 FQDN>  

    -   **详细信息：**指定将用于服务连接点站点系统角色的代理服务器的 FQDN。  

-   **项名称：**ProxyPort  

    -   **是否必需：**当 CloudConnector 等于 1 时需要  

    -   **值：**&lt;*PortNumber*>  

    -   **详细信息：**指定要使用的端口号。  



<!--HONumber=Dec16_HO3-->


