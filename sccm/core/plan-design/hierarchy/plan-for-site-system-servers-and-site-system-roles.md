---
title: "规划站点系统角色 | Microsoft Docs"
description: "在规划 System Center Configuration Manager 层次结构时，请考虑站点系统服务器和站点系统角色。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3704a2d3b75ed7e0a7f718b681448ab6fc078d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 规划站点系统服务器和站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

每个安装的 System Center Configuration Manager 站点都包括一个站点服务器，该服务器是一个**站点系统服务器**。 该站点还可以包括远离站点服务器的计算机上的其他站点系统服务器。 站点系统服务器（站点服务器或远程站点系统服务器）支持 **站点系统角色**。


##  <a name="bkmk_siteservers"></a> 站点系统服务器  
 在计算机上安装站点系统角色时，该计算机将成为站点系统服务器。 在每个站点上，可以安装一个或多个其他站点系统服务器。 还可以选择不安装其他站点系统服务器并直接在站点服务器计算机上运行所有站点系统角色。 每个站点系统服务器支持一个或多个站点系统角色。 其他服务器可以通过分担站点系统角色加在服务器上的 CPU 处理负载，从而帮助扩展站点的功能和容量。  

 考虑添加站点系统服务器时，请确保服务器满足用于实现所需用途的先决条件。 在具有足够带宽的网路位置上添加该服务器以与所需终结点通信也是个好办法，所需终结点包括站点服务器、域资源、基于云的位置、站点系统服务器和客户端。）  

 如果配置含代理的站点系统服务器供站点系统角色使用，请参阅[可以使用代理服务器的站点系统角色](#bkmk_proxy)。  

##  <a name="bkmk_planroles"></a> Site system roles  
 站点系统角色安装在计算机上，为站点提供其他功能。 示例包括：  

-   附加的管理点，以便站点支持更多设备，多达站点支持的容量。  

-   附加的分发点，以扩展内容基础结构，提升内容分发到设备和用户的性能。  

-   一个或多个功能特定的站点系统角色。 例如，软件更新点可用于管理托管设备的软件更新，或者 Reporting Services 点，可用于运行报表来监视和了解或共享有关部署的信息。  


不同的 Configuration Manager 站点可以支持很多不同的站点系统角色集。 支持的站点系统角色集取决于站点的类型（管理中心站点、主站点，或者辅助站点）。 层次结构的拓扑可以限制某些角色的站点类型。 例如，服务连接点仅在层次结构的顶层站点（可能是管理中心站点或独立主战点）受支持。 子主站点或辅助站点上不支持此角色。  

安装站点后，可将某些站点系统角色从其在站点服务器上的默认位置移至其他服务器。 例如，这对于默认安装在主站点或辅助站点上的管理点或分发点就是适用的。 还可以安装某些站点系统角色的其他实例，以扩展站点的功能（为客户提供更多的服务），以便满足业务需求。 某些角色是必需的，其他一些则是可选的。  

-   **Configuration Manager 站点服务器**。 此角色标识运行 Configuration Manager 安装程序以安装站点的服务器，或者标识安装辅助站点的服务器。 在站点卸载之前，不能移动或卸载此角色。  

-   **Configuration Manager 站点系统**。 此角色分配给任意安装站点或者站点系统角色的计算机。 在从计算机中删除最后一个站点系统角色之前，不能移动或卸载此角色。  

-   **Configuration Manager 组件站点系统角色**。 此角色标识运行 SMS Executive 服务的实例的站点系统，并且是支持其他角色（如管理点）所必需的。 在从计算机中删除最后一个适用的站点系统角色之前，不能移动或卸载此角色。  

-   **Configuration Manager 站点数据库服务器**。 此角色分配给为站点托管站点数据库实例的站点系统服务器。 只能通过修改站点以使用不同的 SQL Server 实例来托管站点数据库，才能将此角色移动到新的服务器。  

-   **SMS 提供程序**。 将 SMS 提供程序角色分配给托管 SMS 提供程序实例（Configuration Manager 控制台和站点数据库之间的接口）的每台计算机。 默认情况下，此角色将在管理中心站点和主站点的站点服务器上自动安装。 可在每个站点安装其他实例以提供其他管理用户的访问权限。  

     若要安装其他提供程序，必须运行 Configuration Manager 安装程序来[管理 SMS 提供程序](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)。 然后在其他计算机上安装其他提供程序。 一台计算机只能安装一个 SMS 提供程序实例，并且该计算机必须与站点服务器位于同一个域。  

-   **应用程序目录 Web 服务点**。 一种站点系统角色，该角色从软件库中向应用程序目录网站提供软件信息。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

-   **应用程序目录网站点**。 一种站点系统角色，该角色从应用程序目录中向用户提供可用软件的列表。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

     如果应用程序目录支持 Internet 上的客户端计算机，最佳安全做法是将应用程序目录网站点安装在外围网络中以实现安全性，并将应用程序目录 Web 服务点安装在 Intranet 上。  

-   **资产智能同步点**。 一种站点系统角色，用于连接到 Microsoft 以下载资产智能目录的信息。 此角色还上传未分类的标题，以便将来可将其纳入目录中。 层次结构仅支持此角色的单一实例，并且它必须位于层次结构的顶层站点（管理中心站点或独立主站点）。 如果将独立主站点扩展到更大的层次结构中，必须从主站点中卸载此角色，然后可将其安装在管理中心站点上。   有关详细信息，请参阅 [System Center Configuration Manager 中的资产智能](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

-   **证书注册点**。 与运行网络设备注册服务的服务器通信的站点系统角色。 此角色管理使用简单证书注册协议 (SCEP) 的设备证书请求。 仅主站点和管理中心站点支持此角色。

     虽然单一证书注册点可为整个层次结构提供功能，但可能会需要在一个站点和同一层次结构中的多个站点中安装此角色的多个实例。 这有助于负载均衡。 当层次结构中存在多个实例时，客户端会随机分配到证书注册点之一。  

     每个证书注册点都需要访问网络设备注册服务的单独实例。 你不能将两个或多个证书注册点配置为使用相同的网络设备注册服务。 此外，证书注册点不能安装在运行网络设备注册服务的同一服务器上。  

- **云管理网关连接点**。 用于与[云管理网关](/sccm/core/clients/manage/setup-cloud-management-gateway)进行通信的站点系统角色。

-   **分发点**。 一种站点系统角色，其中包含供客户端下载的源文件，例如应用程序内容、软件包、软件更新、操作系统映像以及启动映像。 默认情况下，当站点安装时，此角色安装在新主站点和辅助站点的站点服务器计算机上。 管理中心站点上不支持此角色。 你可以在支持的一个站点和同一层次结构中的多个站点中安装此角色的多个实例。 有关详细信息，请参阅 [System Center Configuration Manager 中内容管理的基本概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)和[为 System Center Configuration Manager 管理内容和内容基础结构](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

-   **回退状态点**。 一种站点系统角色，该角色可帮助监视客户端安装并确定因无法与其管理点通信而不受管理的客户端。 尽管仅主站点支持此角色，你可以在一个站点和同一层次结构中的多个站点中安装此角色的多个实例。     


-   **Endpoint Protection 点**。 一种站点系统角色，Configuration Manager 使用该角色来接受 Endpoint Protection 许可条款并为云保护服务配置默认成员身份。 层次结构仅支持此角色的单一实例，并且它必须位于层次结构的顶层站点（管理中心站点或独立主站点）。 如果将独立主站点扩展到更大的层次结构中，必须从主站点中卸载此角色，然后可将其安装在管理中心站点上。 有关详细信息，请参阅 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

-   **注册点**。 一种站点系统角色，该角色使用 Configuration Manager 的 PKI 证书来注册移动设备和 Mac 计算机。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

     如果用户通过使用 Configuration Manager 注册移动设备，并且用户的 Active Directory 帐户位于站点服务器的林不信任的林中，则必须在用户的林中安装注册点。 然后可以对该用户进行身份验证。  

-   **注册代理点**。 一种站点系统角色，用于管理来自移动设备和 Mac 计算机的 Configuration Manager 注册请求。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

     如果支持 Internet 上的移动设备，出于安全考虑，请将注册代理点安装在外围网络中，并将注册点安装在 Intranet 上。  

-   **Exchange Server 连接器**。 有关此角色的信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **管理点**。 一种站点系统角色，该角色向客户端提供策略和服务位置信息，并从客户端接收配置数据。  

    默认情况下，当站点安装时，此角色安装在新主站点和辅助站点的站点服务器计算机上。 主站点支持此角色的多个实例。 辅助站点支持单一管理点，以便为客户端提供本地联系点，从而获取计算机和用户策略（辅助站点上的管理点称为代理管理点）。  

     可以设置管理点支持 HTTP 或 HTTPS，同时支持使用 System Center Configuration Manager 本地移动设备管理进行管理的移动设备。 你可以使用 [System Center Configuration Manager 管理点的数据库副本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)帮助减少管理点在处理来自客户端的请求时放在站点数据库服务器上的 CPU 负载。  

-   **Reporting Services 点**。 与 SQL Server Reporting Services 集成的一种站点系统角色，用于为 Configuration Manager 创建和管理报表。 主站点和管理中心站点上支持此角色，可以在支持的站点中安装此角色的多个实例。 有关详细信息，请参阅[规划 System Center Configuration Manager 中的报告](../../../core/servers/manage/planning-for-reporting.md)。  

-   **服务连接点**。 一种站点系统角色，可以与 Microsoft Intune 和本地 MDM 配合使用以管理移动设备。 此角色还会上传站点的使用情况数据，并需要它以便在 Configuration Manager 控制台中提供 Configuration Manager 更新。 层次结构仅支持此角色的单一实例，并且它必须位于层次结构的顶层站点（管理中心站点或独立主站点）。 如果将独立主站点扩展到更大的层次结构中，必须从主站点中卸载此角色，然后可将其安装在管理中心站点上。 有关详细信息，请参阅[关于 System Center Configuration Manager 服务连接点](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。  

-   **软件更新点**。 与 Windows Server Update Services (WSUS) 集成以便向 Configuration Manager 客户端提供软件更新的站点系统角色。 所有站点都支持此角色：  

    -   在管理中心站点中安装此站点系统以便与 WSUS 同步。  

    -   在子主站点设置此角色的每个实例，以便与管理中心站点同步。  

    -   如果数据在网络上的传输速度较慢，请考虑在辅助站点中安装软件更新点。  

    有关详细信息，请参阅 [System Center Configuration Manager 的软件更新计划](../../../sum/plan-design/plan-for-software-updates.md)。  

-   **状态迁移点**。 在计算机迁移到新操作系统时存储用户状态数据的站点系统角色。 子主站点和辅助站点上均支持此角色。 可以在一个站点和同一层次结构中的多个站点中安装此角色的多个实例。 有关部署操作系统时存储用户状态的详细信息，请参阅[在 System Center Configuration Manager 中管理用户状态](../../../osd/get-started/manage-user-state.md)。  

-   **系统健康验证程序点**。 尽管此站点系统角色将在 Configuration Manager 控制台中保持可见，但不再使用该角色。  

###  <a name="bkmk_proxy"></a> 可以使用代理服务器的站点系统角色  
 某些 Configuration Manager 站点系统角色需要连接到 Internet，当托管该角色的站点系统服务器配置为需要使用代理服务器时，将使用代理服务器。 通常，此连接在安装了站点系统角色的计算机的“系统”上下文中建立。 连接不能使用用于典型用户帐户的代理配置。 如果需要代理服务器来完成与 Internet 的连接，必须将计算机设置为使用代理服务器：  

-   在安装站点系统角色时，可以设置代理服务器。  

-   当使用 Configuration Manager 控制台时，可以添加或修改代理服务器配置。  

-   可使用代理服务器配置的站点系统服务器上的所有站点系统角色均使用相同的代理服务器配置。 如果需要不同的站点系统角色使用不同的代理服务器，你必须将这些站点系统角色安装在不同的站点系统服务器计算机上。  

-   如果修改代理服务器配置，或将新的站点系统角色安装在已有代理服务器配置的计算机上，新的配置会覆盖原始配置。  


有关为站点系统角色设置代理服务器的过程，请参阅[添加 System Center Configuration Manager 的站点系统角色](../../../core/servers/deploy/configure/add-site-system-roles.md)主题。  

下面是可以使用代理服务器的站点系统角色：  

-   **资产智能同步点**。 此站点系统角色连接到 Microsoft，并在承载资产智能同步点的计算机上使用代理服务器配置。  

-   **基于云的分发点**。 当使用基于云的分发点时，用于管理基于云的分发点的主站点必须能够连接到 Microsoft Azure 以设置、监视并将内容分发到分发点。 如果此连接需要代理服务器，必须在主站点服务器上设置代理服务器。 无法在 Azure 中基于云的分发点上设置代理服务器。 有关详细信息，请参阅[在 Microsoft Azure 中为 System Center Configuration Manager 安装基于云的分发点](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)主题的[为管理云服务的主站点配置代理设置](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud)部分。  

-   **Exchange Server 连接器**。 此站点系统角色连接到 Exchange Server，并在承载 Exchange Server 连接器的计算机上使用代理服务器配置。  

-   **软件更新点**。 此站点系统角色可能需要连接到 Microsoft 更新来下载修补程序和同步有关更新的信息。 通常，当设置代理服务器时，该计算机上支持使用代理服务器的每个站点系统角色都会使用该代理服务器。 不需要附加配置。 此情况的例外是软件更新点。 默认情况下，除非在设置软件更新点时还启用了下列选项，否则软件更新点不使用可用代理服务器：  

    -   **同步软件更新时使用代理服务器**  

    -   **使用自动部署规则下载内容时使用代理服务器**  

    > [!TIP]  
    >  必须先在承载软件更新点的站点系统服务器上设置代理服务器，然后才能选择任一选项。 只会为你选择的特定选项使用代理服务器。  

 有关软件更新点的代理服务器的详细信息，请参阅[安装软件更新点](../../../sum/get-started/install-a-software-update-point.md)主题中的“代理服务器设置”部分。  

-   **服务连接点**。 设置为处于联机状态（不脱机）时，此站点系统角色将连接到 Microsoft Intune 和 Microsoft 云服务。  
