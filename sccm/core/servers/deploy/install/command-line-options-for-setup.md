---
title: 安装程序的命令行选项
titleSuffix: Configuration Manager
description: 创建自动化脚本，以从命令行安装 Configuration Manager。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6b49f05708f824c16dd90cbb9c872f49ab484de8
ms.sourcegitcommit: e0d303d87c737811c2d3c40d01cd3d260a5c7bde
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69974713"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Configuration Manager 安装程序的命令行选项

适用范围：  System Center Configuration Manager (Current Branch)

使用以下信息从命令行配置脚本或安装 Configuration Manager。  

## <a name="bkmk_setup"></a>适用于安装程序的命令行选项

请从站点服务器上的 Configuration Manager 安装路径的 `\BIN\X64` 目录运行安装程序。

### `/DEINSTALL`

卸载站点。 请从站点服务器计算机中运行安装程序。  

### `/DONTSTARTSITECOMP`

安装站点，但会阻止站点组件管理器服务启动。 直到站点组件管理器服务启动之后，该站点才会处于活动状态。 站点组件管理器负责在站点安装和启动 SMS_Executive 服务以及其他进程。 站点安装完成之后，如果启动站点组件管理器服务，则它将安装 SMS_Executive 服务以及站点运行所需的其他进程。  

### `/HIDDEN`

在安装过程中隐藏用户界面。 仅在与 **/SCRIPT** 选项结合时使用此选项。 无人参与的脚本文件必须提供所有必需的选项，否则安装将失败。  

### `/NOUSERINPUT`

在安装过程中禁用用户输入，但会显示安装向导。 仅在与 **/SCRIPT** 选项结合时使用此选项。 无人参与的脚本文件必须提供所有必需的选项，否则安装将失败。  

### `/RESETSITE`

运行站点重置，该操作将重置站点的数据库和服务帐户。

有关详细信息，请参阅[运行站点重置](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset)。  

### `/TESTDBUPGRADE`

对站点数据库的备份运行测试，以确保该数据库可以升级。

> [!IMPORTANT]  
> 不要在生产站点数据库上运行此命令行选项。 在生产站点数据库上运行此命令行选项将升级站点数据库，并可能导致站点不可操作。

#### <a name="usage"></a>用法

提供站点数据库的实例名称和数据库名称。 如果仅指定数据库名称，安装程序将使用默认实例名称。  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

运行站点的无人参与升级。 指定产品密钥，包括短划线 (`-`)。 此外，指定以前下载的安装程序先决条件文件的路径。  

有关安装程序的先决条件文件的详细信息，请参阅[安装程序下载程序](/sccm/core/servers/deploy/install/setup-downloader)。  

#### <a name="usage"></a>用法

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

运行无人参与的安装。 使用带有此选项的安装程序初始化文件。 有关如何运行无人参与的安装程序的详细信息，请参阅[使用命令行安装站点](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites)。  

#### <a name="usage"></a>用法

`/SCRIPT <setup script path>`

### `/SDKINST`

在指定计算机上安装 SMS 提供程序。 为 SMS 提供程序计算机提供完全限定的域名 (FQDN)。 有关 SMS 提供程序的详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。  

#### <a name="usage"></a>用法

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

在指定计算机上卸载 SMS 提供程序。 提供 SMS 提供程序计算机的 FQDN。  

#### <a name="usage"></a>用法

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

管理在以前已安装站点上安装的语言。 提供包含语言设置的语言脚本文件的位置。 有关详细信息，请参阅[用于管理语言的命令行选项](#bkmk_Lang)部分。  

#### <a name="usage"></a>用法

`/MANAGELANGS <Language script path>`


## <a name="bkmk_Lang"></a> 用于管理语言的命令行选项

### <a name="identification"></a>标识

- **密钥名称：** 操作  

    - **必需：** 是  

    - **值：** `ManageLanguages`  

    - **详细信息：** 管理站点处的服务器、客户端和移动客户端语言支持。  

### <a name="options"></a>选项

- **密钥名称：** AddServerLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的服务器语言。 默认情况下使用英语。  

- **密钥名称：** AddClientLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定可供客户端计算机使用的语言。 默认情况下使用英语。  

- **密钥名称：** DeleteServerLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定将不再可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的要删除的语言。 默认情况下使用英语，因此无法删除它。  

- **密钥名称：** DeleteClientLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定将不再可用于客户端计算机的要删除的语言。 默认情况下使用英语，因此无法删除它。  

- **密钥名称：** MobileDeviceLanguage  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否安装移动设备客户端语言。  

- **密钥名称：** PrerequisiteComp  

    - **必需：** 是  

    - **值：**

        - `0` = 下载  

        - `1` = 已下载  

    - **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 `0`，则安装程序将下载文件。  

- **密钥名称：** PrerequisitePath  

    - **必需：** 是  

    - **值：**  <安装程序先决条件文件的路径  >  

    - **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件  。  


## <a name="bkmk_Unattended"></a>无人参与安装程序脚本文件项

使用下列部分来帮助你为无人参与安装程序创建脚本。 列表显示：

- 可用的安装程序脚本密钥及其对应的值
- 如果需要
- 它们用于的安装类型
- 密钥的简短说明

### <a name="unattended-install-for-a-central-administration-site-cas"></a>管理中心站点 (CAS) 的无人参与安装

使用下列详细信息通过无人参与的安装程序脚本文件来安装 CAS。  

#### <a name="identification"></a>标识

- **密钥名称：** 操作  

    - **必需：** 是  

    - **值：** `InstallCAS`  

    - **详细信息：** 安装 CAS。  

- **密钥名称：** CDLatest  

    - **必需：** 是，仅在使用 CD.Latest 文件夹中的介质时。

    - **值：**

        - `1` = 使用 CD.Latest 中的介质

        - 除 1 之外的任何值 = 不使用 CD.Latest 介质

    - **详细信息：** 安装或恢复主站点或 CAS 后，运行 CD.Latest 文件夹中的安装程序，包括此密钥和值。 该值将告知安装程序当前在使用 CD.Latest 中的介质。

#### <a name="options"></a>选项

- **密钥名称：** ProductID  

    - **必需：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 带短划线的有效产品密钥

        - `Eval` = 安装 Configuration Manager 的评估版

    - **详细信息：** 指定 Configuration Manager 安装产品密钥，包括短划线。

- **密钥名称：** 站点代码  

    - **必需：** 是  

    - **值：**  <站点代码  >，例如 `ABC`

    - **详细信息：** 指定三个字母数字字符，用于唯一标识层次结构中的站点。  

- **密钥名称：** SiteName  

    - **必需：** 是  

    - **值：**  <*站点名称*>  

    - **详细信息：** 指定此站点的名称。  

- **密钥名称：** SMSInstallDir  

    - **必需：** 是  

    - **值：**  <*Configuration Manager 安装路径*>  

    - **详细信息：** 指定 Configuration Manager 程序文件的安装文件夹。  

- **密钥名称：** SDKServer  

    - **必需：** 是  

    - **值：**  <*SMS 提供程序 FQDN*>  

    - **详细信息：** 指定托管 SMS 提供程序的服务器的 FQDN。 你可以在初始安装后为站点配置其他 SMS 提供程序。  

- **密钥名称：** PrerequisiteComp  

    - **必需：** 是  

    - **值：**

        - `0` = 下载  

        - `1` = 已下载  

    - **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 `0`，则安装程序将下载文件。  

- **密钥名称：** PrerequisitePath  

    - **必需：** 是  

    - **值：**  <安装程序先决条件文件的路径  >  

    - **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件  。  

- **密钥名称：** AdminConsole  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否要安装 Configuration Manager 控制台。  

- **密钥名称：** JoinCEIP  

    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

    - **必需：** 是  

    - **值：**

        - `0` = 不联接  

        - `1` = 联接  

    - **详细信息：** 指定是否要加入客户体验改善计划 (CEIP)。  

- **密钥名称：** AddServerLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的服务器语言。 默认情况下使用英语。  

- **密钥名称：** AddClientLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定可供客户端计算机使用的语言。 默认情况下使用英语。  

- **密钥名称：** DeleteServerLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 修改安装后的站点。 指定将不再可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的要删除的语言。 默认情况下使用英语，因此无法删除它。  

- **密钥名称：** DeleteClientLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 修改安装后的站点。 指定将不再可用于客户端计算机的要删除的语言。 默认情况下使用英语，因此无法删除它。  

- **密钥名称：** MobileDeviceLanguage  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否安装移动设备客户端语言。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **密钥名称：** SQLServerName  

    - **必需：** 是  

    - **值：**  <*SQL Server 名称*>  

    - **详细信息：** 指定正在运行 SQL Server 以托管站点数据库的服务器或群集实例的名称。  

- **密钥名称：** DatabaseName  

    - **必需：** 是  

    - **值：**  <*站点数据库名称*> 或 <*实例名称*>\\<*站点数据库名称*>  

    - **详细信息：** 指定要创建的 SQL Server 数据库的名称，或在安装程序安装 CAS 数据库时要使用的 SQL Server 数据库的名称。  

        > [!IMPORTANT]  
        > 如果未使用默认实例，则指定实例名称和站点数据库名称。  

- **密钥名称：** SQLSSBPort  

    - **必需：** 否  

    - **值：**  <*SSB 端口号*>  

    - **详细信息：** 指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 默认情况下，SSB 使用 TCP 端口 4022，但也可以使用不同的端口。  

- **密钥名称：** SQLDataFilePath  

    - **必需：** 否  

    - **值：**  <数据库 .mdb 文件的路径  >  

    - **详细信息：** 指定创建数据库 .mdb 文件的备用位置。  

- **密钥名称：** SQLLogFilePath  

    - **必需：** 否  

    - **值：**  <*数据库.ldf 文件的路径*>  

    - **详细信息：** 指定创建数据库 .ldf 文件的备用位置。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **密钥名称：** CloudConnector  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否在此站点上安装服务连接点。 因为只能在层次结构的顶层站点上安装服务连接点，因此，请将子主站点的此值设置为 `1`。  

- **密钥名称：** CloudConnectorServer  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <服务连接点服务器 FQDN  >  

    - **详细信息：** 指定将承载服务连接点站点系统角色的服务器的 FQDN。  

- **密钥名称：** UseProxy  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定服务连接点是否使用代理服务器。  

- **密钥名称：** ProxyName  

    - **必需：** 当 UseProxy 等于 1 时需要   

    - **值：**  <代理服务器 FQDN  >  

    - **详细信息：** 指定服务连接点使用的代理服务器的 FQDN。  

- **密钥名称：** ProxyPort  

    - **必需：** 当 UseProxy 等于 1 时需要   

    - **值：**  <*端口号*>  

    - **详细信息：** 指定要用于代理端口的端口号。  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **密钥名称：** SAActive

    - **必需：** 否

    - **值：**

        - `0` = 没有软件保障

        - `1` = 软件保障处于有效状态

    - **详细信息：** 指定是否具有有效的软件保障。 有关详细信息，请参阅[产品和许可常见问题解答](/sccm/core/understand/product-and-licensing-faq)。

- **密钥名称：** CurrentBranch

    - **必需：** 否

    - **值：**

        - `0` = 安装 LTSB

        - `1` = 安装 Current Branch

    - **详细信息：** 指定是使用 Configuration Manager Current Branch，还是 Long-Term Servicing Branch (LTSB)。 有关详细信息，请参阅[我应使用 Configuration Manager 的哪一个分支？](/sccm/core/understand/which-branch-should-i-use)。

### <a name="unattended-install-for-a-primary-site"></a>主站点的无人参与安装

使用下列详细信息通过无人参与的安装程序脚本文件来安装主站点。  

#### <a name="identification"></a>标识

- **密钥名称：** 操作  

    - **必需：** 是  

    - **值：** `InstallPrimarySite`  

    - **详细信息：** 安装主站点。  

- **密钥名称：** CDLatest  

    - **必需：** 是，仅在使用 CD.Latest 文件夹中的介质时。

    - **值：**

        - `1` = 使用 CD.Latest 中的介质

        - 除 1 之外的任何值 = 不使用 CD.Latest 介质

    - **详细信息：** 安装或恢复主站点或 CAS 后，运行 CD.Latest 文件夹中的安装程序，包括此密钥和值。 该值将告知安装程序当前在使用 CD.Latest 中的介质。

#### <a name="options"></a>选项

- **密钥名称：** ProductID  

    - **必需：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 带短划线的有效产品密钥

        - `Eval` = 安装 Configuration Manager 的评估版

    - **详细信息：** 指定 Configuration Manager 安装产品密钥，包括短划线。

- **密钥名称：** 站点代码  

    - **必需：** 是  

    - **值：**  <*站点代码*>  

    - **详细信息：** 指定三个字母数字字符，用于唯一标识层次结构中的站点。  

- **密钥名称：** SiteName  

    - **必需：** 是  

    - **值：**  <*站点名称*>  

    - **详细信息：** 指定此站点的名称。  

- **密钥名称：** SMSInstallDir  

    - **必需：** 是  

    - **值：**  <*Configuration Manager 安装路径*>

    - **详细信息：** 指定 Configuration Manager 程序文件的安装文件夹。  

- **密钥名称：** SDKServer  

    - **必需：** 是  

    - **值：**  <*SMS 提供程序 FQDN*>  

    - **详细信息：** 指定托管 SMS 提供程序的服务器的 FQDN。 你可以在初始安装后为站点配置其他 SMS 提供程序。  

- **密钥名称：** PrerequisiteComp  

    - **必需：** 是  

    - **值：**

        - `0` = 下载  

        - `1` = 已下载  

    - **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 `0`，则安装程序将下载文件。  

- **密钥名称：** PrerequisitePath  

    - **必需：** 是  

    - **值：**  <安装程序先决条件文件的路径  >  

    - **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件  。  

- **密钥名称：** AdminConsole  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否要安装 Configuration Manager 控制台。  

- **密钥名称：** JoinCEIP  

    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

    - **必需：** 是  

    - **值：**

        - `0` = 不联接  

        - `1` = 联接  

    - **详细信息：** 指定是否加入 CEIP。  

- **密钥名称：** ManagementPoint  

    - **必需：** 否  

    - **值：**  <*管理点站点服务器 FQDN*>  

    - **详细信息：** 指定托管管理点站点系统角色的服务器的 FQDN。  

- **密钥名称：** ManagementPointProtocol  

    - **必需：** 否  

    - **值：** `HTTPS` 或 `HTTP`  

    - **详细信息：** 指定要用于管理点的协议。  

- **密钥名称：** DistributionPoint  

    - **必需：** 否  

    - **值：**  <*分发点站点服务器 FQDN*>  

    - **详细信息：** 指定托管分发点站点系统角色的服务器的 FQDN。  

- **密钥名称：** DistributionPointProtocol  

    - **必需：** 否  

    - **值：** `HTTPS` 或 `HTTP`  

    - **详细信息：** 指定要用于分发点的协议。  

- **密钥名称：** RoleCommunicationProtocol  

    - **必需：** 是  

    - **值：** `EnforceHTTPS` 或 `HTTPorHTTPS`  

    - **详细信息：** 指定是将所有站点系统配置为仅接受来自客户端的 HTTPS 通信，还是为每个站点系统角色配置通信方法。 如果选择 `EnforceHTTPS`，则客户端必须具有有效的公钥基础结构 (PKI) 证书，以进行客户端身份验证。  

- **密钥名称：** ClientsUsePKICertificate  

    - **必需：** 是  

    - **值：**

        - `0` = 不使用  

        - `1` = 使用  

    - **详细信息：** 指定客户端是否使用客户端 PKI 证书与站点系统角色通信。  

- **密钥名称：** AddServerLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的服务器语言。 默认情况下使用英语。  

- **密钥名称：** AddClientLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 指定可供客户端计算机使用的语言。 默认情况下使用英语。  

- **密钥名称：** DeleteServerLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 修改安装后的站点。 指定将不再可用于 Configuration Manager 控制台、报告和 Configuration Manager 对象的要删除的语言。 默认情况下使用英语，因此无法删除它。  

- **密钥名称：** DeleteClientLanguages  

    - **必需：** 否  

    - **值：** DEU、FRA、RUS、CHS、JPN、CHT、CSY、ESN、HUN、ITA、KOR、NLD、PLK、PTB、PTG、SVE、TRK 或 ZHH  

    - **详细信息：** 修改安装后的站点。 指定将不再可用于客户端计算机的要删除的语言。 默认情况下使用英语，因此无法删除它。  

- **密钥名称：** MobileDeviceLanguage  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否安装移动设备客户端语言。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **密钥名称：** SQLServerName  

    - **必需：** 是  

    - **值：**  <*SQL Server 名称*>  

    - **详细信息：** 指定运行 SQL Server 以托管站点数据库的服务器或群集实例的名称。  

- **密钥名称：** DatabaseName  

    - **必需：** 是  

    - **值：**  <*站点数据库名称*> 或 <*实例名称*>\\<*站点数据库名称*>  

    - **详细信息：** 指定要创建的 SQL Server 数据库的名称，或者安装主站点数据库时要使用的 SQL Server 数据库的名称。  

        > [!IMPORTANT]  
        > 如果未使用默认实例，则指定实例名称和站点数据库名称。  

- **密钥名称：** SQLSSBPort  

    - **必需：** 否  

    - **值：**  <*SSB 端口号*>  

    - **详细信息：** 指定 SQL Server 使用的 SSB 端口。 默认情况下，SSB 使用 TCP 端口 4022，但也可以使用不同的端口。  

- **密钥名称：** SQLDataFilePath  

    - **必需：** 否  

    - **值：**  <数据库 .mdb 文件的路径  >  

    - **详细信息：** 指定创建数据库 .mdb 文件的备用位置。  

- **密钥名称：** SQLLogFilePath  

    - **必需：** 否  

    - **值：**  <*数据库.ldf 文件的路径*>  

    - **详细信息：** 指定创建数据库 .ldf 文件的备用位置。  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **密钥名称：** CCARSiteServer  

    - **必需：** 否  

    - **值：**  <*管理中心站点 FQDN*>  

    - **详细信息：** 指定主站点加入 Configuration Manager 层次结构时要附加到的 CAS。 在安装过程中指定 CAS。  

- **密钥名称：** CASRetryInterval  

    - **必需：** 否  

    - **值：**  <间隔（以分钟为单位）  >  

    - **详细信息：** 指定在连接失败后尝试连接到 CAS 的重试间隔（以分钟为单位）。 例如，如果连接到 CAS 失败，则主站点将等待你为  CASRetryInterval 值指定的分钟数，然后重新尝试连接。  

- **密钥名称：** WaitForCASTimeout  

    - **必需：** 否  

    - **值：**  <超时（从 0 分钟到 100 分钟）  >  

    - **详细信息：** 指定主站点连接到 CAS 的最大超时值（以分钟为单位）。 例如，如果主站点无法连接到 CAS，则主站点根据 CASRetryInterval  值重试与 CAS 的连接，直到达到 WaitForCASTimeout  时间段。 可以指定从 `0` 到 `100` 之间的一个值。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **密钥名称：** CloudConnector  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否在此站点上安装服务连接点。 因为只能在层次结构的顶层站点上安装服务连接点，请将子主站点的此值设置为 `0`。  

- **密钥名称：** CloudConnectorServer  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <服务连接点服务器 FQDN\>   

    - **详细信息：** 指定将承载服务连接点站点系统角色的服务器的 FQDN。  

- **密钥名称：** UseProxy  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定服务连接点是否使用代理服务器。  

- **密钥名称：** ProxyName  

    - **必需：** 当 UseProxy 等于 1 时需要   

    - **值：**  <代理服务器 FQDN  >  

    - **详细信息：** 指定服务连接点使用的代理服务器的 FQDN。  

- **密钥名称：** ProxyPort  

    - **必需：** 当 UseProxy 等于 1 时需要   

    - **值：**  <*端口号*>  

    - **详细信息：** 指定要用于代理端口的端口号。  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **密钥名称：** SAActive

    - **必需：** 否

    - **值：**

        - `0` = 没有软件保障

        - `1` = 软件保障处于有效状态

    - **详细信息：** 指定是否具有有效的软件保障。 有关详细信息，请参阅[产品和许可常见问题解答](/sccm/core/understand/product-and-licensing-faq)。

- **密钥名称：** CurrentBranch

    - **必需：** 否

    - **值：**

        - `0` = 安装 LTSB

        - `1` = 安装 Current Branch

    - **详细信息：** 指定是使用 Configuration Manager Current Branch，还是 Long-Term Servicing Branch (LTSB)。 有关详细信息，请参阅[我应使用 Configuration Manager 的哪一个分支？](/sccm/core/understand/which-branch-should-i-use)。

### <a name="unattended-recovery-for-a-cas"></a>CAS 的无人参与恢复

使用下列详细信息通过无人参与的安装程序脚本文件来恢复 CAS。  

#### <a name="identification"></a>标识

- **密钥名称：** 操作  

    - **必需：** 是  

    - **值：** `RecoverCCAR`  

    - **详细信息：** 恢复 CAS。  

- **密钥名称：** CDLatest  

    - **必需：** 是，仅在使用 CD.Latest 文件夹中的介质时。

    - **值：**

        - `1` = 使用 CD.Latest 中的介质

        - 除 1 之外的任何值 = 不使用 CD.Latest 介质

    - **详细信息：** 安装或恢复主站点或 CAS 后，运行 CD.Latest 文件夹中的安装程序，包括此密钥和值。 该值将告知安装程序当前在使用 CD.Latest 中的介质。

#### <a name="recoveryoptions"></a>RecoveryOptions

- **密钥名称：** ServerRecoveryOptions  

    - **必需：** 是  

    - **值：**

        - `1` = 恢复站点服务器和 SQL Server

        - `2` = 仅恢复站点服务器

        - `4` = 仅恢复 SQL Server  

    - **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 根据指定的值，还需要以下选项：  

        - 1  或 2  ：要使用站点备份来恢复站点，请为 SiteServerBackupLocation  指定值。 如果未指定值，安装程序会重新安装站点，而不是从备份集还原站点。  

        - **4**：如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。  

- **密钥名称：** DatabaseRecoveryOptions  

    - **必需：** 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。  

    - **值：**

        - `10` = 从备份还原站点数据库。  

        - `20` = 使用已通过另一种方法手动恢复的站点数据库。  

        - `40` = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 站点通过从其他站点复制来恢复全局数据和站点数据。  

        - `80` = 跳过数据库恢复。  

    - **详细信息：** 指定安装程序如何恢复 SQL Server 中的站点数据库。  

- **密钥名称：** ReferenceSite  

    - **必需：** 当 **DatabaseRecoveryOptions** 设置的值为 **40**时，需要此项。  

    - **值：**  <*引用站点 FQDN*>  

    - **详细信息：** 如果数据库备份早于更改跟踪保持期，或者在没有备份的情况下恢复站点时，则指定 CAS 用于恢复全局数据的引用主站点。  

        如果未指定引用站点，并且备份早于更改跟踪保持期，则会使用 CAS 中的还原数据重新初始化所有主站点。  

        如果未指定引用站点，并且备份在更改跟踪保持期中，则从主站点中仅复制备份以后的更改。 如果不同的主站点中具有冲突的更改，则 CAS 将使用它收到的第一个更改。  

- **密钥名称：** SiteServerBackupLocation  

    - **必需：** 否  

    - **值：**  <*到站点服务器备份集的路径*>  

    - **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，安装程序会重新安装站点，而不是从备份集还原站点。  

- **密钥名称：** BackupLocation  

    - **必需：** 如果为 ServerRecoveryOptions 项配置了值 1 或 4，并为 DatabaseRecoveryOptions 项配置了值 10，则需要此项      。  

    - **值：**  <*到站点数据库备份集的路径*>  

    - **详细信息：** 指定站点数据库备份集的路径。  

#### <a name="options"></a>选项

- **密钥名称：** ProductID  

    - **必需：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 带短划线的有效产品密钥

        - `Eval` = 安装 Configuration Manager 的评估版

    - **详细信息：** 指定 Configuration Manager 安装产品密钥，包括短划线。

- **密钥名称：** 站点代码  

    - **必需：** 是  

    - **值：**  <*站点代码*>  

    - **详细信息：** 指定三个字母数字字符，用于唯一标识层次结构中的站点。 指定在发生故障之前站点使用的站点代码。

- **密钥名称：** SiteName  

    - **必需：** 否  

    - **值：**  <*站点名称*>  

    - **详细信息：** 指定此站点的名称。  

- **密钥名称：** SMSInstallDir  

    - **必需：** 是  

    - **值：**  <*Configuration Manager 安装路径*>  

    - **详细信息：** 指定 Configuration Manager 程序文件的安装文件夹。  

- **密钥名称：** SDKServer  

    - **必需：** 是  

    - **值：**  <*SMS 提供程序 FQDN*>  

    - **详细信息：** 指定托管 SMS 提供程序的服务器的 FQDN。 指定在发生故障之前托管 SMS 提供程序的服务器。  

        在初始安装后，你可以为站点配置其他 SMS 提供程序。 有关 SMS 提供程序的详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。  

- **密钥名称：** PrerequisiteComp  

    - **必需：** 是  

    - **值：**

        - `0` = 下载  

        - `1` = 已下载  

    - **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 0  ，则安装程序将下载文件。  

- **密钥名称：** PrerequisitePath  

    - **必需：** 是  

    - **值：**  <安装程序先决条件文件的路径>   

    - **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件  。  

- **密钥名称：** AdminConsole  

    - **必需：** 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否要安装 Configuration Manager 控制台。  

- **密钥名称：** JoinCEIP  

    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

    - **必需：** 是  

    - **值：**

        - `0` = 不联接  

        - `1` = 联接  

    - **详细信息：** 指定是否加入 CEIP。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **密钥名称：** SQLServerName  

    - **必需：** 是  

    - **值：**  <*SQL Server 名称*>  

    - **详细信息：** 指定正在运行 SQL Server 并托管站点数据库的服务器或群集实例的名称。 指定在发生故障之前托管站点数据库的同一服务器。  

- **密钥名称：** DatabaseName  

    - **必需：** 是  

    - **值：**  <*站点数据库名称*> 或 <*实例名称*>\\<*站点数据库名称*>  

    - **详细信息：** 指定要创建的 SQL Server 数据库的名称，或者安装 CAS 数据库时要使用的 SQL Server 数据库的名称。 指定在发生故障之前使用的同一数据库名称。  

        > [!IMPORTANT]  
        > 如果未使用默认实例，则指定实例名称和站点数据库名称。  

- **密钥名称：** SQLSSBPort  

    - **必需：** 是  

    - **值：**  <*SSB 端口号*>  

    - **详细信息：** 指定 SQL Server 使用的 SSB 端口。 默认情况下，SSB 使用 TCP 端口 4022。 指定在发生故障之前使用的相同 SSB 端口。  

- **密钥名称：** SQLDataFilePath  

    - **必需：** 否  

    - **值：**  <数据库 .mdb 文件的路径  >  

    - **详细信息：** 指定创建数据库 .mdb 文件的备用位置。  

- **密钥名称：** SQLLogFilePath  

    - **必需：** 否  

    - **值：**  <*数据库.ldf 文件的路径*>  

    - **详细信息：** 指定创建数据库 .ldf 文件的备用位置。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **密钥名称：** CloudConnector  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否在此站点上安装服务连接点。 因为只能在层次结构的顶层站点上安装服务连接点，所以子主站点的此值必须为 0  。  

- **密钥名称：** CloudConnectorServer  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <服务连接点服务器 FQDN>   

    - **详细信息：** 指定将承载服务连接点站点系统角色的服务器的 FQDN。  

- **密钥名称：** UseProxy  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定服务连接点是否使用代理服务器。  

- **密钥名称：** ProxyName  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <代理服务器 FQDN  >  

    - **详细信息：** 指定服务连接点使用的代理服务器的 FQDN。  

- **密钥名称：** ProxyPort  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <*端口号*>  

    - **详细信息：** 指定要用于代理端口的端口号。  

### <a name="unattended-recovery-for-a-primary-site"></a>主站点的无人参与恢复

使用下列详细信息通过无人参与的安装程序脚本文件来恢复主站点。  

#### <a name="identification"></a>标识

- **密钥名称：** 操作  

    - **必需：** 是  

    - **值：** `RecoverPrimarySite`  

    - **详细信息：** 恢复主站点。  

- **密钥名称：** CDLatest  

    - **必需：** 是，仅在使用 CD.Latest 文件夹中的介质时。

    - **值：**

        - `1` = 使用 CD.Latest 中的介质

        - 除 1 之外的任何值 = 不使用 CD.Latest 介质

    - **详细信息：** 安装或恢复主站点或 CAS 后，运行 CD.Latest 文件夹中的安装程序，包括此密钥和值。 该值将告知安装程序当前在使用 CD.Latest 中的介质。

#### <a name="recoveryoptions"></a>RecoveryOptions

- **密钥名称：** ServerRecoveryOptions  

    - **必需：** 是  

    - **值：**

        - `1` = 恢复站点服务器和 SQL Server

        - `2` = 仅恢复站点服务器

        - `4` = 仅恢复 SQL Server  

    - **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 根据指定的值，还需要以下选项：  

        - 1  或 2  ：要使用站点备份来恢复站点，请为 SiteServerBackupLocation  指定值。 如果未指定值，安装程序会重新安装站点，而不是从备份集还原站点。  

        - **4**：如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。  

- **密钥名称：** DatabaseRecoveryOptions  

    - **必需：** 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。  

    - **值：**

        - `10` = 从备份还原站点数据库。  

        - `20` = 使用已通过另一种方法手动恢复的站点数据库。  

        - `40` = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 站点通过从其他站点复制来恢复全局数据和站点数据。  

        - `80` = 跳过数据库恢复。  

    - **详细信息：** 指定安装程序如何恢复 SQL Server 中的站点数据库。  

- **密钥名称：** SiteServerBackupLocation  

    - **必需：** 否  

    - **值：**  <*到站点服务器备份集的路径*>  

    - **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，安装程序会重新安装站点，而不是从备份集还原站点。  

- **密钥名称：** BackupLocation  

    - **必需：** 如果为 ServerRecoveryOptions 项配置了值 1 或 4，并为 DatabaseRecoveryOptions 项配置了值 10，则需要此项      。  

    - **值：**  <*到站点数据库备份集的路径*>  

    - **详细信息：** 指定站点数据库备份集的路径。  

#### <a name="options"></a>选项

- **密钥名称：** ProductID  

    - **必需：** 是  

    - **值：**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>` = 带短划线的有效产品密钥

        - `Eval` = 安装 Configuration Manager 的评估版

    - **详细信息：** 指定 Configuration Manager 安装产品密钥，包括短划线。

- **密钥名称：** 站点代码  

    - **必需：** 是  

    - **值：**  <*站点代码*>  

    - **详细信息：** 指定三个字母数字字符，用于唯一标识层次结构中的站点。 指定在发生故障之前站点使用的站点代码。

- **密钥名称：** SiteName  

    - **必需：** 否  

    - **值：**  <*站点名称*>  

    - **详细信息：** 指定此站点的名称。  

- **密钥名称：** SMSInstallDir  

    - **必需：** 是  

    - **值：**  <*Configuration Manager 安装路径*>  

    - **详细信息：** 指定 Configuration Manager 程序文件的安装文件夹。  

- **密钥名称：** SDKServer  

    - **必需：** 是  

    - **值：**  <*SMS 提供程序 FQDN*>  

    - **详细信息：** 指定托管 SMS 提供程序的服务器的 FQDN。 指定在发生故障之前托管 SMS 提供程序的服务器。 在初始安装后，你可以为站点配置其他 SMS 提供程序。 有关 SMS 提供程序的详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。  

- **密钥名称：** PrerequisiteComp  

    - **必需：** 是  

    - **值：**

        - `0` = 下载  

        - `1` = 已下载  

    - **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 0  ，则安装程序将下载文件。  

- **密钥名称：** PrerequisitePath  

    - **必需：** 是  

    - **值：**  <安装程序先决条件文件的路径>   

    - **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件  。  

- **密钥名称：** AdminConsole  

    - **必需：** 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否要安装 Configuration Manager 控制台。  

- **密钥名称：** JoinCEIP  

    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

    - **必需：** 是  

    - **值：**

        - `0` = 不联接  

        - `1` = 联接  

    - **详细信息：** 指定是否加入 CEIP。  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **密钥名称：** SQLServerName  

    - **必需：** 是  

    - **值：**  <*SQL Server 名称*>  

    - **详细信息：** 指定运行 SQL Server 以托管站点数据库的服务器或群集实例的名称。 指定在发生故障之前托管站点数据库的同一服务器。  

- **密钥名称：** DatabaseName  

    - **必需：** 是  

    - **值：**  <*站点数据库名称*> 或 <*实例名称*>\\<*站点数据库名称*>

    - **详细信息：** 指定要创建的 SQL Server 数据库的名称，或者安装 CAS 数据库时要使用的 SQL Server 数据库的名称。 指定在发生故障之前使用的同一数据库名称。  

        > [!IMPORTANT]  
        > 如果未使用默认实例，则指定实例名称和站点数据库名称。  

- **密钥名称：** SQLSSBPort  

    - **必需：** 是  

    - **值：**  <*SSB 端口号*>  

    - **详细信息：** 指定 SQL Server 使用的 SSB 端口。 默认情况下，SSB 使用 TCP 端口 4022。 指定在发生故障之前使用的相同 SSB 端口。  

- **密钥名称：** SQLDataFilePath  

    - **必需：** 否  

    - **值：**  <数据库 .mdb 文件的路径  >  

    - **详细信息：** 指定创建数据库 .mdb 文件的备用位置。  

- **密钥名称：** SQLLogFilePath  

    - **必需：** 否  

    - **值：**  <*数据库.ldf 文件的路径*>  

    - **详细信息：** 指定创建数据库 .ldf 文件的备用位置。  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **密钥名称：** CCARSiteServer  

    - **必需：** 查看详情。  

    - **值：**  <CAS 的站点代码  >  

    - **详细信息：** 指定主站点加入 Configuration Manager 层次结构时要附加到的 CAS。 如果在发生故障之前主站点已附加到 CAS，则此设置为必需。 指定在发生故障之前 CAS 使用的站点代码。  

- **密钥名称：** CASRetryInterval  

    - **必需：** 否  

    - **值：**  <间隔（以分钟为单位）  >  

    - **详细信息：** 指定在连接失败后尝试连接到 CAS 的重试间隔（以分钟为单位）。 例如，如果连接到 CAS 失败，则主站点将等待你为  CASRetryInterval 值指定的分钟数，然后再次尝试连接。  

- **密钥名称：** WaitForCASTimeout  

    - **必需：** 否  

    - **值：**  <超时（以分钟为单位）  >  

    - **详细信息：** 指定主站点连接到 CAS 的最大超时值（以分钟为单位）。 例如，如果主站点无法连接到 CAS，则主站点根据 CASRetryInterval  值重试与 CAS 的连接，直到达到 WaitForCASTimeout  时间段。 可以指定 `0` 到 `100` 之间的一个值。  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **密钥名称：** CloudConnector  

    - **必需：** 是  

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定是否在此站点上安装服务连接点。 因为只能在层次结构的顶层站点上安装服务连接点，子主站点的此值必须为 `0`。  

- **密钥名称：** CloudConnectorServer  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <服务连接点服务器 FQDN>   

    - **详细信息：** 指定将承载服务连接点站点系统角色的服务器的 FQDN。  

- **密钥名称：** UseProxy  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**

        - `0` = 不安装  

        - `1` = 安装  

    - **详细信息：** 指定服务连接点是否使用代理服务器。  

- **密钥名称：** ProxyName  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <代理服务器 FQDN  >  

    - **详细信息：** 指定服务连接点使用的代理服务器的 FQDN。  

- **密钥名称：** ProxyPort  

    - **必需：** 当 CloudConnector 等于 1 时需要   

    - **值：**  <*端口号*>  

    - **详细信息：** 指定要用于代理端口的端口号。  
