---
title: 应用程序管理规划
titleSuffix: Configuration Manager
description: 实现和配置用于在 Configuration Manager 中部署应用程序的所需依赖关系。
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0c2808bd4fa9501c46012549427e2de4087eb9d
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083386"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>在 Configuration Manager 中规划和配置应用程序管理

*适用于：System Center Configuration Manager (Current Branch)*

使用本文中的信息可帮助实现用于在 Configuration Manager 中部署应用程序的所需依赖关系。  



## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

在运行以下站点系统角色的服务器上，需要安装 IIS：

- 应用程序目录网站点  
- 应用程序目录 Web 服务点  
- 管理点  
- 分发点  

有关此要求的详细信息，请参阅[站点和站点系统角色的先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>移动设备的代码签名应用程序证书

在对应用程序进行代码签名以将其部署到移动设备时，如果使用版本 3 模板（Windows Server 2008，企业版）生成了证书，请勿使用此证书。 此证书模板创建的证书与用于移动设备的 Configuration Manager 应用程序不兼容。

如果使用 Active Directory 证书服务对移动设备应用程序进行代码签名，请勿使用版本 3 证书模板。


### <a name="audit-sign-in-events-for-user-device-affinity"></a>审核登录事件的用户设备相关性  

如果想自动创建用户设备相关性，则需将客户端配置为审核登录事件。

Configuration Manager 客户端从 Windows 的安全事件日志中读取类型为“成功”的登录事件，以确定自动的用户设备相关性。 通过以下两个审核策略，启用这些事件：

- **审核帐户登录事件**
- **审核登录事件**

若要自动在用户和设备之间创建关系，请确保在客户端计算机上启用这两个设置。 可以使用 Windows 组策略来配置这两个设置。

有关用户设备相关性的详细信息，请参阅[将用户和设备同用户设备相关性相链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。  



## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系


### <a name="management-point"></a>管理点

客户端会与管理点联系，以下载客户端策略、查找内容和连接到应用程序目录。 如果客户端无法访问管理点，则无法使用应用程序目录。

> [!Note]  
> 从版本 1806 开始，不再需要应用程序目录角色，即可在软件中心显示用户可用的应用程序。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。<!--1358309-->  
  

### <a name="distribution-point"></a>分发点

在可以将应用程序部署到客户端之前，层次结构中需要有至少一个分发点。 默认情况下，站点服务器在标准安装时启用分发点站点角色。 分发点的数量和位置因环境的特定要求而异。

有关如何安装分发点和管理内容的详细信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  


### <a name="reporting-services-point"></a>Reporting Services 点

若要使用 Configuration Manager 中的报表进行应用程序管理，首先要安装和配置 Reporting Services 点。

有关详细信息，请参阅 [Configuration Manager 中的报告](/sccm/core/servers/manage/reporting)。  


### <a name="client-settings"></a>客户端设置

许多客户端设置都可以控制在客户端上安装应用程序的方式和用户在设备上的体验。 这些客户端设置包括以下组：

- 计算机代理  
- 计算机重启  
- 软件中心  
- 软件部署  
- 用户和设备相关性  

有关详细信息，请参阅下列文章：

- [关于客户端设置](/sccm/core/clients/deploy/about-client-settings)  
- [如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)  


### <a name="security-permissions-for-application-management"></a>应用程序管理的安全权限

- “应用程序作者”安全角色包含创建、更改和停用应用程序所需的权限。  

- “应用程序部署管理员”安全角色包含部署应用程序所需的权限。  

- “应用程序管理员”安全角色具有“应用程序作者”和“应用程序部署管理员”安全角色中的所有权限。  

有关详细信息，请参阅[配置基于角色的管理](/sccm/core/servers/deploy/configure/configure-role-based-administration)。  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>必须安装 APP-V 4.6 SP1 或更高版本的客户端才能运行虚拟应用程序

为了在 Configuration Manager 中创建虚拟应用程序，请在设备上安装 App-V 4.6 SP1 或更高版本。

此外，还要使用在 [Microsoft 支持文章 2645225](https://support.microsoft.com/help/2645225) 中描述的修补程序来更新 App-V 客户端，才能部署虚拟应用程序。  


### <a name="discovered-user-accounts-for-application-catalog"></a>应用程序目录发现的用户帐户

Configuration Manager 必须先发现用户帐户，然后用户才能查看和请求应用程序目录中的应用程序。 有关详细信息，请参阅[运行发现](/sccm/core/servers/deploy/configure/run-discovery)。  


### <a name="application-catalog-web-service-point"></a>应用程序目录 Web 服务点

应用程序目录 Web 服务点是站点系统角色，它向用户访问的应用程序目录网站提供有关软件库中可用的软件的信息。

有关如何配置此站点系统角色的详细信息，请参阅[安装和配置应用程序目录](#bkmk_appcat)。  

> [!Note]  
> 从版本 1806 开始，不再需要应用程序目录 Web 服务点角色，但它仍受支持。<!--1358309-->  
>
> 应用程序目录网站点的 Silverlight 用户体验不再受支持。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  


### <a name="application-catalog-website-point"></a>应用程序目录网站点

应用程序目录网站点是站点系统角色，它向用户提供可用软件的列表。

有关如何配置此站点系统角色的详细信息，请参阅[安装和配置应用程序目录](#bkmk_appcat)。

> [!Note]  
> 从版本 1806 开始，不再需要应用程序目录网站点角色，但它仍受支持。<!--1358309-->  
>
> 应用程序目录网站点的 Silverlight 用户体验不再受支持。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  



## <a name="bkmk_userex"></a> 配置软件中心  

有关配置软件中心和打造软件中心品牌的详细信息，请参阅[规划软件中心](/sccm/apps/plan-design/plan-for-software-center)。


## <a name="bkmk_appcat"></a> 安装和配置应用程序目录  

> [!Note]  
> 从版本 1806 开始，不再需要应用程序目录站点和 Web 服务点角色，但依然受支持。 有关详细信息，请参阅[配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)。  
>
> 应用程序目录网站点的 Silverlight 用户体验不再受支持。 有关详细信息，请参阅[已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。  

> [!IMPORTANT]  
> 在执行这些步骤之前，请确保所有依赖项已就绪。 有关详细信息，请参阅本文以下各节：
>
> - [Configuration Manager 的外部依赖关系](#dependencies-external-to-configuration-manager)  
> - [Configuration Manager 依赖关系](#configuration-manager-dependencies)


### <a name="step-1-web-server-certificate-for-https"></a>步骤 1：HTTPS 的 Web 服务器证书

如果使用 HTTPS 连接，将 Web 服务器证书部署到应用程序目录网站点和应用程序目录 Web 服务点的站点系统服务器。

如果希望客户端使用 Internet 中的应用程序目录，将 Web 服务器证书部署到至少一个管理点。 将其配置为来自 Internet 的客户端连接。

有关证书要求的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  


### <a name="step-2-client-authentication-certificate-for-https"></a>步骤 2：HTTPS 的客户端身份验证证书

如果使用客户端 PKI 证书连接到管理点，请将客户端身份验证证书部署到客户端计算机。 尽管客户端不使用客户端 PKI 证书来连接到应用程序目录，但它们必须连接到管理点，然后才能使用应用程序目录。

在以下情况下，将客户端身份验证证书部署到客户端计算机：

- Intranet 中的所有管理点只接受 HTTPS 客户端连接。
- 客户端从 Internet 连接到应用程序目录。

有关证书要求的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>步骤 3：安装和配置应用程序目录角色

在同个站点安装应用程序目录 Web 服务点和应用程序目录网站角色。 你不必将它们安装在同一服务器上或安装在同一 Active Directory 林中。 但是，应用程序目录 Web 服务点必须位于站点数据库所在的林中。

有关服务器布局的详细信息，请参阅[规划站点系统服务器和站点系统角色](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)。

> [!NOTE]  
> 在主站点上安装应用程序目录。 无法在辅助站点或管理中心站点进行安装。  

在新的站点系统服务器或站点中的现有服务器上安装应用程序目录。 有关一般过程的详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。 在向导中添加站点系统角色或创建站点系统服务器，从列表中选择以下角色：

- **应用程序目录 Web 服务点**  
- **应用程序目录网站点**  

> [!TIP]  
> 如果希望客户端计算机通过 Internet 使用应用程序目录，请指定 Internet 完全限定的域名 (FQDN)。  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>验证这些站点系统角色的安装  

- 状态消息：使用组件“SMS_PORTALWEB_CONTROL_MANAGER”  和“SMS_AWEBSVC_CONTROL_MANAGER” 。  

    例如，“SMS_PORTALWEB_CONTROL_MANAGER”的状态 ID“1015”确认站点组件管理器已成功安装在应用程序目录网站点上。  

- 日志文件：搜索 **SMSAWEBSVCSetup.log** 和 **SMSPORTALWEBSetup.log**。  

    有关详细信息，请搜索 **awebsvcMSI.log** 和 **portlwebMSI.log** 日志文件。  


### <a name="step-4-configure-client-settings"></a>步骤 4：配置客户端设置

如果希望所有用户具有相同设置，请配置默认客户端设置。 否则，请为特定集合配置自定义客户端设置。

有关详细信息，请参阅下列文章：

- [关于客户端设置](/sccm/core/clients/deploy/about-client-settings)  
    - 计算机代理  
    - 计算机重启  
    - 软件中心  
    - 软件部署  
    - 用户和设备相关性  
- [如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)  

Configuration Manager 客户端在下次下载客户端策略时将为设备配置这些设置。 若要为单个客户端触发策略检索，请参阅[如何管理客户端](/sccm/core/clients/manage/manage-clients)。


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>步骤 5：验证应用程序目录是否可正常运行

使用以下过程来验证应用程序目录是否可正常运行。

> [!NOTE]  
> 若要获得应用程序目录用户体验，需安装 Microsoft Silverlight。 如果从浏览器中直接使用应用程序目录，请首先验证计算机上是否安装了 Microsoft Silverlight。  

> [!TIP]  
> 应用程序目录在安装后未正常运行的大多数典型原因都是未满足先决条件。 确认应用程序目录站点系统角色的角色先决条件。 有关详细信息，请参阅[站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。  

在浏览器中，输入应用程序目录网站的地址。 确认网页显示以下三个选项卡：“应用程序目录”、“我的应用程序请求”和“我的设备”。  

为“应用程序目录”使用以下列表中适当的地址，其中 &lt;server&gt; 是计算机名、Intranet FQDN 或 Internet FQDN：  

- HTTPS 客户端连接和默认站点系统角色设置：**https://&lt;server&gt;/CMApplicationCatalog**  

- HTTP 客户端连接和默认站点系统角色设置：**http://&lt;server&gt;/CMApplicationCatalog**  

- HTTPS 客户端连接和自定义站点系统角色设置：**https://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

- HTTP 客户端连接和自定义站点系统角色设置：**http://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

> [!NOTE]  
> 如果你登录到具有域管理员帐户的设备，Configuration Manager 客户端不会显示通知消息。 例如，消息指示新软件可用。  
