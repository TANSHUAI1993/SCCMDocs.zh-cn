---
title: "规划和配置应用程序管理 | Microsoft Docs"
description: "实现和配置用于在 System Center Configuration Manager 中部署应用程序的所需依赖关系。"
ms.custom: na
ms.date: 02/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: "13"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 46cc3fcfd9516cf1c124e24b50d0aac0cb0025dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>规划和配置 System Center Configuration Manager 中的应用程序管理

*适用范围：System Center Configuration Manager (Current Branch)*

使用本文中的信息可帮助实现用于在 System Center Configuration Manager 中部署应用程序的所需依赖关系。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  

|依赖关系|更多信息|  
|------------------|----------------------|  
|在运行应用程序目录网站点、应用程序目录 Web 服务点、管理点和分发点的站点系统服务器上，需要安装 Internet Information Services (IIS)。|有关此要求的详细信息，请参阅[支持的配置](../../core/plan-design/configs/supported-configurations.md)。|  
|Configuration Manager 注册的移动设备|在对应用程序进行代码签名以将其部署到移动设备时，如果使用版本 3 模 (**Windows Server 2008, Enterprise Edition**) 生成了证书，请勿使用此证书。 此证书模板创建的证书与用于移动设备的 Configuration Manager 应用程序不兼容。<br /><br /> 如果使用 Active Directory 证书服务对移动设备应用程序进行代码签名，请勿使用版本 3 证书模板。|  
|如果想自动创建用户设备相关性，必须将客户端配置为审核登录事件。|Configuration Manager 客户端从电脑的安全事件日志中读取类型为“成功”的登录事件，以确定自动的用户设备相关性。  通过以下两个审核策略，启用这些事件：<br>**审核帐户登录事件**<br>**审核登录事件**<br>若要自动在用户和设备之间创建关系，请确保在客户端计算机上启用这两个设置。 可以使用 Windows 组策略来配置这两个设置。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系   

|依赖关系|更多信息|  
|------------------|----------------------|  
|管理点|客户端会与管理点联系，以下载客户端策略、查找内容和连接到应用程序目录。<br /><br /> 如果客户端无法访问管理点，则无法使用应用程序目录。|  
|分发点|在可以将应用程序部署到客户端之前，层次结构中必须有至少一个分发点。 默认情况下，站点服务器在标准安装时启用分发点站点角色。 分发点的数量和位置将因企业的特定要求而异。<br /><br /> 若要深入了解如何安装分发点和管理内容，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|客户端设置|许多客户端设置都可以控制在客户端上安装应用程序的方式和用户在客户端上的体验。 这些客户端设置包括：<br /><br /><ul><li>计算机代理</li><li>计算机重新启动</li><li>软件部署</li><li>用户和设备相关性</li></ul> 有关这些客户端设置的详细信息，请参阅[关于客户端设置](../../core/clients/deploy/about-client-settings.md)。<br /><br /> 若要了解如何配置客户端设置，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。|  
|对于应用程序目录：<br /><br /> 发现的用户帐户|用户必须先被 Configuration Manager 发现，然后才能查看和请求应用程序目录中的应用程序。 有关详细信息，请参阅[运行发现](/sccm/core/servers/deploy/configure/run-discovery)。|  
|必须安装 APP-V 4.6 SP1 或更高版本的客户端才能运行虚拟应用程序|为了能够在 Configuration Manager 中创建虚拟应用程序，客户端计算机必须安装 App-V 4.6 SP1 或更高版本的客户端。<br /><br /> 还必须使用在知识库[文章 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) 中描述的修补程序来更新 App-V 客户端，才能部署虚拟应用程序。|  
|应用程序目录 Web 服务点|应用程序目录 Web 服务点是站点系统角色，它向应用程序目录网站提供有关软件库中可用的软件的信息。<br /><br /> 若要深入了解如何配置此站点系统角色，请参阅本文中的[配置软件中心和应用程序目录（仅适用于 Windows 电脑）](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only)。|  
|应用程序目录网站点|应用程序目录网站点是站点系统角色，它向用户提供可用软件的列表。<br /><br /> 若要深入了解如何配置此站点系统角色，请参阅本文中的[配置软件中心和应用程序目录（仅适用于 Windows 电脑）](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only)。|  
|Reporting Services 点|为了能够使用 Configuration Manager 中的报表进行应用程序管理，必须首先安装和配置 Reporting Services 点。<br /><br /> 有关详细信息，请参阅 [System Center Configuration Manager 中的报表](../../core/servers/manage/reporting.md)。|  
|应用程序管理的安全权限|必须具有以下安全权限才能管理应用程序。<br /><br /> “应用程序作者”安全角色包含前面列出的在 Configuration Manager 中创建、更改和停用应用程序所需的权限。<br /><br /> **若要部署应用程序，请执行以下操作：**<br /><br /> “应用程序部署管理员”安全角色包含前面列出的在 Configuration Manager 中部署应用程序所需的权限。<br /><br /> “应用程序管理员”安全角色具有“应用程序作者”和“应用程序部署管理员”安全角色中的所有权限。<br /><br /> 有关详细信息，请参阅[配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>配置软件中心和应用程序目录（仅适用于 Windows PC）  

 在 System Center Configuration Manager 中，对于用户如何更改设置、浏览应用程序和安装应用程序，现在有两个选项：  

-   **新的软件中心** - 新的软件中心具有新式外观。 并且本应仅出现在依赖于 Silverlight 的应用程序目录中的应用（用户可用的应用）现在将出现在“应用程序”选项卡下的软件中心。 应用程序目录仍然可以通过软件中心的“安装状态”选项卡下的链接进行访问。  

     你可以通过启用客户端设置“计算机代理” **计算机代理** > **使用新的软件中心**。  

    > [!IMPORTANT]  
    >  虽然不再需要连接到应用程序目录，但仍必须配置应用程序目录网站点和应用程序目录 Web 服务点，该内容将在下一节中详细介绍。  

-   **以前的软件中心和应用程序目录** - 默认情况下，用户会继续连接到以前版本的软件中心并连接到应用程序目录（需要 Silverlight 启用的 Web 浏览器）来浏览可用的应用程序。  

 无论你选择使用哪个版本，当你在 Windows 电脑上安装 Configuration Manager 客户端时，都会自动安装软件中心。  

    > [!TIP]  
    >  用户看到的软件中心的版本取决于 Configuration Manager 客户端设置。 这样便能根据部署到集合的自定义客户端设置，灵活地控制使用哪个版本。 

    > [!IMPORTANT]
    > 在未来几个月，我们将删除以前版本的软件中心，并且它将不再可用。
    > 你可以通过启用客户端设置“计算机代理” **计算机代理** > **使用新的软件中心**。 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>安装和配置应用程序目录及软件中心的步骤  

> [!IMPORTANT]  
>  执行这些步骤以前，请确保已满足之前所列的所有先决条件。  

|步骤|详细信息|更多信息|  
|-----------|-------------|----------------------|  
|**步骤 1：** 如果你将使用 HTTPS 连接，请确保已将 Web 服务器证书部署到站点系统服务器。|将 Web 服务器证书部署到将运行应用程序目录网站点和应用程序目录 Web 服务点的站点系统服务器。<br /><br /> 此外，如果希望客户端从 Internet 中使用应用程序目录，请将 Web 服务器证书部署到至少一个管理点站点系统服务器，并针对来自 Internet 的客户端连接对其进行配置。|有关证书要求的详细信息，请参阅 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。|  
|**步骤 2：** 如果你将使用客户端 PKI 证书连接到管理点，请将客户端身份验证证书部署到客户端计算机。|尽管客户端不使用客户端 PKI 证书来连接到应用程序目录，但它们必须连接到管理点，然后才能使用应用程序目录。 在以下情况下，你必须将客户端身份验证证书部署到客户端计算机：<br /><br /><ul><li>Intranet 中的所有管理点只接受 HTTPS 客户端连接。</li><li>客户端将从 Internet　连接到应用程序目录。</li></ul>|有关证书要求的详细信息，请参阅 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。|  
|**步骤 3：** 安装和配置应用程序目录 Web 服务点和应用程序目录网站。|必须将这两个站点系统角色安装在同一站点中。 你不必将它们安装在同一站点系统服务器上或安装在同一 Active Directory 林中。 但是，应用程序目录 Web 服务点必须位于站点数据库所在的林中。|有关站点系统角色布局的详细信息，请参阅[规划站点系统服务器和站点系统角色](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)。<br /><br /> 要配置应用程序目录 Web 服务点和应用程序目录网站点，请参阅**步骤 3：安装和配置应用程序目录站点系统角色**。|  
|**步骤 4：** 为应用程序目录和软件中心配置客户端设置。|如果希望所有用户具有相同设置，请配置默认客户端设置。 否则，请为特定集合配置自定义客户端设置。|有关客户端设置的详细信息，请参阅[关于客户端设置](../../core/clients/deploy/about-client-settings.md)。<br /><br /> 若要详细了解如何配置这些客户端设置，请参阅**步骤 4：为应用程序目录和软件中心配置客户端设置**。|  
|**步骤 5：** 验证应用程序目录是否可正常运行。|可以从浏览器或软件中心中直接使用应用程序目录。|请参阅**步骤 5：验证应用程序目录是否可正常运行**。|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>用于安装和配置应用程序目录和软件中心的补充过程  
 如果上表中的步骤需要执行补充过程，请使用以下信息。  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>步骤 3：安装和配置应用程序目录站点系统角色  
 这些过程为应用程序目录配置站点系统角色。 请选择以下两个过程之一，具体取决于是安装新站点系统服务器还是使用现有站点系统服务器：  

> [!NOTE]  
>  应用程序目录不能安装在辅助站点或管理中心站点上。  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>安装和配置应用程序目录站点系统：新建站点系统服务器  

1.  在 Configuration Manager 控制台中，选择“管理” > “站点配置” > “服务器和站点系统角色”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建站点系统服务器”。  

4.  在“常规”页上，指定站点系统的常规设置，然后选择“下一步”。  

    > [!TIP]  
    >  如果希望客户端计算机通过 Internet 使用应用程序目录，请指定 Internet 完全限定的域名 (FQDN)。  

5.  在“系统角色选择”页上，从可用角色列表选择“应用程序目录 Web 服务点”和“应用程序目录网站点”，然后选择“下一步”。  

6.  完成该向导。  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>安装和配置应用程序目录站点系统：现有站点系统服务器  

1.  在 Configuration Manager 控制台中，选择“管理” > “站点配置” > “服务器和站点系统角色”，然后选择要用于应用程序目录的服务器。  

3.  在“主页”选项卡上的“服务器”组中，选择“添加站点系统角色”。  

4.  在“常规”页上，指定站点系统的常规设置，然后选择“下一步”。  

    > [!TIP]  
    >  如果希望客户端计算机通过 Internet 使用应用程序目录，请指定 Internet 完全限定的域名 (FQDN)。  

5.  在“系统角色选择”页上，从可用角色列表选择“应用程序目录 Web 服务点”和“应用程序目录网站点”，然后选择“下一步”。  

6.  完成该向导。  

7. 通过使用状态消息和查看日志文件来验证这些站点系统角色的安装：  

    状态消息：使用组件“SMS_PORTALWEB_CONTROL_MANAGER”  和“SMS_AWEBSVC_CONTROL_MANAGER” 。  

    例如，“SMS_PORTALWEB_CONTROL_MANAGER”的状态 ID“1015”确认站点组件管理器已成功安装在应用程序目录网站点上。  

    日志文件：搜索 **SMSAWEBSVCSetup.log** 和 **SMSPORTALWEBSetup.log**。  

    有关详细信息，请搜索 **awebsvcMSI.log** 和 **portlwebMSI.log** 日志文件。  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>步骤 4：为应用程序目录和软件中心配置客户端设置  
 此过程为应用程序目录和软件中心配置将适用于层次结构中的所有设备的默认客户端设置。 如果希望这些设置仅适用于某些设备，则可以创建自定义客户端设置并将其部署到一个集合，该集合中的设备具有特定设置。 若要深入了解如何创建自定义设备设置，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)一文中的[如何创建和部署自定义客户端设置](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings)部分。  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置” > “默认客户端设置”。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”。  

4.  查看并配置与用户通知、应用程序目录和软件中心相关的设置。 例如：  

    1.  “计算机代理” 组：  

        -   **默认应用程序目录网站点**  

        -   **向 Internet Explorer 受信任的站点区域添加默认应用程序目录网站**  

        -   **软件中心中显示的组织名称**  

            > [!TIP]  
            >  要指定显示在应用程序目录中的组织名称并配置网站主题，请使用应用程序目录网站属性上的“自定义”选项卡。  

        -   **使用新的软件中心** - 借助新的软件中心，用户可以浏览和安装可用的应用而无需访问应用程序目录（需要 Silverlight 启用的 Web 浏览器），如果要使用新的软件中心，请设置为“是”。  

        -   **安装权限**  

        -   **显示关于新部署的通知**  

    2.  “电源管理” 组：  

        -   **允许用户从电源管理中排除其设备**  

    3.  “远程工具” 组：  

        -   **用户可以在软件中心内更改策略或通知设置**  

    4.  “用户和设备相关性” 组：  

        -   **允许用户定义其主要设备**  

    > [!NOTE]  
    >  有关客户端设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../core/clients/deploy/about-client-settings.md)。  

5.  选择“确定”可关闭“默认客户端设置”对话框。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 若要为单个客户端启动策略检索，请参阅[如何管理客户端](../../core/clients/manage/manage-clients.md)。

#### <a name="how-to-customize-software-center-branding"></a>如何自定义软件中心品牌

根据以下规则应用软件中心的自定义品牌：

1. 如果未安装应用程序目录网站点站点服务器角色，则软件中心将显示“计算机代理”客户端设置（软件中心中显示的“组织名称”）中指定的组织名称。 有关说明，请参阅[如何配置客户端设置](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/configure-client-settings)。
2. 如果已安装应用程序目录网站点站点服务器角色，则软件中心将显示在应用程序目录网站点站点服务器角色属性中指定的组织名称和颜色。 有关详细信息，请参阅[应用程序目录网站点的配置选项](https://docs.microsoft.com/en-us/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website)。
3. 如果已配置 Microsoft Intune 订阅且已连接到 Configuration Manager，则软件中心将显示 Intune 订阅属性中指定的组织名称、颜色和公司徽标。 有关详细信息，请参阅 [Configuring the Microsoft Intune subscription](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription)。

> [!IMPORTANT]  
>  软件中心品牌与 Intune 服务每 14 天同步一次，因此在 Intune 中所做的更改显示在 Configuration Manager 以前，可能会有延迟。

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>步骤 5：验证应用程序目录是否可正常运行  
 使用以下过程来验证应用程序目录是否可正常运行。 可以从浏览器或软件中心中直接使用应用程序目录。  

> [!NOTE]  
>  应用程序目录需要 Microsoft Silverlight，后者将为 Configuration Manager 客户端先决条件自动安装。 如果通过使用未安装 Configuration Manager 客户端的计算机从浏览器中直接使用应用程序目录，请首先验证计算机上是否安装了 Microsoft Silverlight。  

> [!TIP]  
>  应用程序目录在安装后未正常运行的大多数典型原因都是未满足先决条件。 确认应用程序目录站点系统角色的站点系统角色先决条件。 可以使用[支持的配置](../../core/plan-design/configs/supported-configurations.md)一文实现此目标。  

> [!NOTE]  
>  如果使用域管理员帐户登录，将不会显示来自于 Configuration Manager 客户端的通知消息（如指示新软件可用的消息）。  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>从浏览器中直接使用应用程序目录  

-   在浏览器中，输入应用程序目录网站的地址，并确认网页显示以下三个选项卡：“应用程序目录”、“我的应用程序请求”和“我的设备”。  

     为应用程序目录选用以下列表中适当的地址，其中 &lt;server&gt; 是计算机名、Intranet FQDN 或 Internet FQDN：  

    -   HTTPS 客户端连接和默认站点系统角色设置：**https://&lt;server&gt;/CMApplicationCatalog**  

    -   HTTP 客户端连接和默认站点系统角色设置：**http://&lt;server&gt;/CMApplicationCatalog**  

    -   HTTPS 客户端连接和自定义站点系统角色设置：**https://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

    -   HTTP 客户端连接和自定义站点系统角色设置：**http://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>从软件中心（不适用于新版本软件中心）使用应用程序目录  

1.  在客户端计算机上，选择“开始” > “所有程序” > “Microsoft System Center 2012” > “Configuration Manager” > “软件中心”。  

2.  如果之前为软件中心配置了组织名称作为客户端设置，请确认此名称按指定方式显示。  

3.  选择“从应用程序目录中查找其他应用程序”，并确认页面显示以下三个选项卡：“应用程序目录”、“我的应用程序请求”和“我的设备”。  

> [!WARNING]  
>  安装了应用程序目录站点系统角色后，从软件中心选择“从应用程序目录中查找其他应用程序”链接时，将不会立即看到应用程序目录。 在客户端下一次下载其客户端策略后，或在安装了应用程序目录站点系统角色后最多 25 个小时内，将可以从软件中心中使用应用程序目录。  
