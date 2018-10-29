---
title: 规划站点系统角色
titleSuffix: Configuration Manager"
description: 在规划 Configuration Manager 层次结构时，请考虑站点系统服务器和站点系统角色。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f2c3052337b5c985798c15950a541086587176d1
ms.sourcegitcommit: 19fc4f27667d51502fc9d7d02d164f2837d65dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461301"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>在 Configuration Manager 中规划站点系统服务器和站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

每个安装的 Configuration Manager 站点都包括一个站点服务器，该服务器是一个站点系统服务器。 该站点还可以包括远离站点服务器的计算机上的其他站点系统服务器。 站点系统服务器（站点服务器或远程站点系统服务器）支持 **站点系统角色**。  


##  <a name="bkmk_siteservers"></a> 站点系统服务器  

在计算机上安装站点系统角色时，该计算机将成为站点系统服务器。 在每个站点上，可以安装一个或多个其他站点系统服务器。 不必安装其他站点系统服务器，并可以选择直接在站点服务器计算机上运行所有站点系统角色。 每个站点系统服务器支持一个或多个站点系统角色。 其他服务器可以通过共享站点系统角色在服务器上放置的处理负载，来帮助扩展站点的功能和容量。  

考虑添加站点系统服务器时，请确保服务器满足用于实现所需用途的先决条件。 还要将其添加到具有足够带宽的网络位置，以与预期终结点通信。 这些终结点包括站点服务器、域资源、基于云的位置、站点系统服务器和客户端。  



##  <a name="bkmk_planroles"></a> Site system roles  

在服务器上安装站点系统角色，为站点提供其他功能。 示例包括：  

-   附加的管理点，以便站点支持更多设备，多达站点支持的容量。  

-   附加的分发点，以扩展内容基础结构，提升内容分发到设备的性能。  

-   一个或多个功能特定的站点系统角色。 例如，软件更新点允许你管理托管设备的软件更新。 Reporting Services 点允许你运行报表来监视、了解和共享有关环境的信息。  


不同的 Configuration Manager 站点可以支持很多不同的站点系统角色集。 受支持的站点系统角色集取决于站点类型。 （站点类型包括管理中心站点、主站点或辅助站点。）层次结构的拓扑可以限制某些角色的站点类型。 例如，仅在层次结构的顶层站点支持服务连接点。 顶层站点可能是管理中心站点或独立主站点。 子主站点或辅助站点上不支持此角色。  

安装站点后，可将某些站点系统角色从其在站点服务器上的默认位置移至其他服务器。 例如，管理点或分发点角色默认安装在主站点服务器或辅助站点服务器上。 还可以安装某些站点系统角色的其他实例，以扩展站点的功能，以便满足业务需求。 某些角色是必需的，其他一些则是可选的。  

#### <a name="configuration-manager-site-server"></a>Configuration Manager 站点服务器
此角色标识运行 Configuration Manager 安装程序以安装站点的服务器，或者标识安装辅助站点的服务器。 卸载站点前，无法移动或卸载此角色。  

#### <a name="configuration-manager-site-system"></a>Configuration Manager 站点系统
此角色分配给任意安装站点或者站点系统角色的计算机。 从计算机中删除最后一个站点系统角色之前，无法移动或卸载此角色。  

#### <a name="configuration-manager-component-site-system-role"></a>Configuration Manager 组件站点系统角色
此角色标识运行 SMS Executive 服务实例的站点系统。 必须支持其他角色，例如管理点。 从计算机中删除最后一个适用的站点系统角色之前，无法移动或卸载此角色。  

#### <a name="configuration-manager-site-database-server"></a>Configuration Manager 站点数据库服务器
站点将此角色分配给保留站点数据库实例的站点系统服务器。 只能通过以下方式才能将此角色移动到新服务器：运行安装程序来修改站点以使用其他 SQL Server 实例来托管站点数据库。  

#### <a name="sms-provider"></a>SMS 提供程序
站点将此角色分配给托管 SMS 提供程序实例的每台计算机。 该提供程序是 Configuration Manager 控制台和站点数据库之间的接口。 默认情况下，此角色将在管理中心站点和主站点的站点服务器上自动安装。 在每个站点安装其他实例，以提供对其他管理用户或冗余的访问权限。  

若要安装其他提供程序，运行 Configuration Manager 安装程序来[管理 SMS 提供程序](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider)。 然后在其他计算机上安装其他提供程序。 仅在计算机上安装 SMS 提供程序的一个实例。 计算机必须位于站点服务器所在的同一域中。  

#### <a name="application-catalog-web-service-point"></a>应用程序目录 Web 服务点
一种站点系统角色，该角色从软件库中向应用程序目录网站提供软件信息。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

#### <a name="application-catalog-website-point"></a>应用程序目录网站点
一种站点系统角色，该角色从应用程序目录中向用户提供可用软件的列表。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

如果应用程序目录支持 Internet 上的客户端计算机，为提高安全性，请将应用程序目录网站点安装在外围网络中。 然后将应用程序目录 Web 服务点安装在 Intranet 上。  

#### <a name="asset-intelligence-synchronization-point"></a>资产智能同步点
一种站点系统角色，用于连接到 Microsoft 以下载资产智能目录的信息。 此角色还上传未分类的标题，以便将来 Microsoft 可将它们纳入目录中。 层次结构仅支持其顶层站点中此角色的单个实例。 如果将独立主站点扩展为更大的层次结构，请从主站点卸载此角色。 然后将其安装在管理中心站点。 

有关详细信息，请参阅 [Configuration Manager 中的资产智能](/sccm/core/clients/manage/asset-intelligence/introduction-to-asset-intelligence)。  

#### <a name="certificate-registration-point"></a>证书注册点
与运行网络设备注册服务的服务器通信的站点系统角色 (NDES)。 此角色管理使用简单证书注册协议 (SCEP) 的设备证书请求。 仅主站点和管理中心站点支持此角色。

虽然单一证书注册点可为整个层次结构提供功能，但可能会需要在一个站点和同一层次结构中的多个站点中安装此角色的多个实例。 此设计有助于负载均衡。 当层次结构中存在多个实例时，客户端会随机分配到证书注册点之一。  

每个证书注册点都需要访问单独的 NDES 实例。 无法将两个或多个证书注册点配置为使用同一 NDES 实例。 此外，请勿在运行 NDES 的同一服务器上安装证书注册点。  

#### <a name="cloud-management-gateway-connection-point"></a>云管理网关连接点
用于与[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)进行通信的站点系统角色。  

#### <a name="data-warehouse-service-point"></a>数据仓库服务点
使用数据仓库服务点存储和报告 Configuration Manager 环境中的长期历史数据。 有关详细信息，请参阅[数据仓库](/sccm/core/servers/manage/data-warehouse)。  

#### <a name="distribution-point"></a>分发点
包括客户端要下载的源文件的站点系统角色，例如： 
- 应用程序内容
- 软件包
- 软件更新
- OS 映像
- 启动映像  

默认情况下，安装新主站点或辅助站点时，此角色安装在站点服务器上。 管理中心站点上不支持此角色。 在支持的站点和同一层次结构中的多个站点中安装此角色的多个实例。 有关详细信息，请参阅[内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)和[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  

#### <a name="endpoint-protection-point"></a>Endpoint Protection 点
一种站点系统角色，Configuration Manager 使用该角色来接受 Endpoint Protection 许可条款并为云保护服务配置默认成员身份。 层次结构仅支持必须位于顶层站点的此角色的单个实例。 如果将独立主站点扩展到更大的层次结构中，请从主站点中卸载此角色，然后可将其安装在管理中心站点上。 有关详细信息，请参阅 [Configuration Manager 中的 Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection)。  

#### <a name="enrollment-point"></a>注册点
一种站点系统角色，该角色使用 Configuration Manager 的 PKI 证书来注册移动设备和 macOS 计算机。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

如果用户通过使用 Configuration Manager 注册移动设备，并且用户的 Active Directory 帐户位于站点服务器的林不信任的林中，则在用户的林中安装注册点。 然后，Configuration Manager 可对用户进行身份验证。  

#### <a name="enrollment-proxy-point"></a>注册代理点
一种站点系统角色，用于管理来自移动设备和 macOS 计算机的 Configuration Manager 注册请求。 尽管仅主站点支持此角色，你可以在一个站点或同一层次结构中的多个站点中安装此角色的多个实例。  

在 Internet 上支持移动设备时，请在外围网络中安装注册代理点，并在 Intranet 上安装一个代理点。   

#### <a name="exchange-server-connector"></a>Exchange Server 连接器
有关此角色的信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  

#### <a name="fallback-status-point"></a>回退状态点
站点系统角色，可帮助你监视客户端安装。 它标识由于无法与其管理点通信而未受管理的客户端。 尽管仅主站点支持此角色，你可以在一个站点和同一层次结构中的多个站点中安装此角色的多个实例。     

#### <a name="management-point"></a>管理点
一种站点系统角色，该角色向客户端提供策略和服务位置信息。 它还从客户端接收配置数据。  

默认情况下，安装新主站点或辅助站点时，此角色安装在站点服务器上。 主站点支持此角色的多个实例。 辅助站点支持单一管理点。 也称为代理管理点，辅助站点上的此角色为客户端提供本地联系点以获取计算机和用户策略。  

设置管理点以支持 HTTP 或 HTTPS。 它们还支持使用 Configuration Manager 本地移动设备管理 (MDM) 进行管理的移动设备。 为帮助减少管理点在为客户端提供服务请求时对站点数据库服务器的处理负载，请使用[管理点的数据库副本](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)。  

#### <a name="reporting-services-point"></a>Reporting Services 点
与 SQL Server Reporting Services 集成的一种站点系统角色，用于为 Configuration Manager 创建和管理报表。 主站点和管理中心站点上支持此角色，可以在支持的站点中安装此角色的多个实例。 有关详细信息，请参阅[规划报表](/sccm/core/servers/manage/planning-for-reporting)。  

#### <a name="service-connection-point"></a>服务连接点
站点系统角色，用于从站点上传使用情况数据，并且需要在控制台中提供 Configuration Manager 更新。 此角色还有助于使用 Microsoft Intune 和本地 MDM 管理移动设备。 层次结构仅支持位于层次结构顶层站点的此角色的单个实例。 如果将独立主站点扩展到更大的层次结构中，请从主站点中卸载此角色，然后可将其安装在管理中心站点上。 有关详细信息，请参阅[关于服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。  

#### <a name="software-update-point"></a>软件更新点
与 Windows Server Update Services (WSUS) 集成以便向 Configuration Manager 客户端提供软件更新的站点系统角色。 所有站点都支持此角色：  

-   在管理中心站点中安装此站点系统以便与 WSUS 同步。  

-   在子主站点设置此角色的每个实例，以便与管理中心站点同步。  

-   如果数据在网络上的传输速度较慢，请考虑在辅助站点中安装软件更新点。  

有关详细信息，请参阅[规划软件更新](/sccm/sum/plan-design/plan-for-software-updates)。  

#### <a name="state-migration-point"></a>状态迁移点
将计算机迁移到新操作系统时，此站点系统角色会存储用户状态数据。 子主站点和辅助站点上均支持此角色。 在站点和同一层次结构中的多个站点中安装此角色的多个实例。 有关在部署 OS 时存储用户状态的详细信息，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  



## <a name="next-steps"></a>后续步骤

某些 Configuration Manager 站点系统角色需要连接到 Internet。 如果环境需要 Internet 流量才能使用代理服务器，请配置这些站点系统角色以使用代理。 有关详细信息，请参阅[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。  
