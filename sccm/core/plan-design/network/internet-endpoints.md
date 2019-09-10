---
title: Internet 访问要求
titleSuffix: Configuration Manager
description: 了解允许使用 Configuration Manager 功能的完整功能的 Internet 终结点。
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11241176abade1233a6fbdbe2ee3bdd0e3219e48
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243572"
---
# <a name="internet-access-requirements"></a>Internet 访问要求

某些 Configuration Manager 功能依赖 Internet 连接来获取完整功能。 如果组织使用防火墙或代理设备限制与 Internet 的网络通信，请确保允许使用这些终结点。

<!-- SCCMDocs-pr #3403 -->

## <a name="bkmk_scp"></a>服务连接点

这些配置适用于托管服务连接点的计算机以及该计算机与 Internet 之间的任何防火墙。 它们都必须允许通过 HTTPS 的传出端口“TCP 443”和 HTTP 的传出端口“TCP 80”与以下 Internet 位置传递通信   。

服务连接点支持使用 Web 代理（具有或不具有身份验证皆可）来使用这些位置。 有关详细信息，请参阅[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。

有关服务连接点的详细信息，请参阅[关于服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。

其他 Configuration Manager 功能可能需要来自服务连接点的其他终结点。 有关详细信息，请参阅本文中的其他部分。

> [!TIP]  
> 服务连接点在连接到 `go.microsoft.com` 或 `manage.microsoft.com` 时使用 Microsoft Intune 服务。 存在以下已知问题：如果未在服务连接点上安装 Baltimore CyberTrust 根证书、该证书已过期或损坏，则 Intune 连接器会遇到连接问题。 有关详细信息，请参阅 [KB 3187516：服务连接点不下载更新](https://support.microsoft.com/help/3187516)。  

### <a name="a-namebkmk_scp-updates-updates-and-servicing"></a><a name="bkmk_scp-updates"/> 更新和维护服务

有关该功能的详细信息，请参阅 [Configuration Manager 的更新和服务](/sccm/core/servers/manage/updates)。

> [!Tip]  
> 为[管理见解](/sccm/core/servers/manage/management-insights)规则（即，将站点连接到 Microsoft 云来实现 Configuration Manager 更新）启用这些终结点  。

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="microsoft-intune"></a>Microsoft Intune

有关该功能的详细信息，请参阅[使用 Configuration Manager 和 Microsoft Intune 的混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

### <a name="windows-10-servicing"></a>Windows 10 维护服务

有关该功能的详细信息，请参阅[管理 Windows 即服务](/sccm/osd/deploy-use/manage-windows-as-a-service)。

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure 服务

有关该功能的详细信息，请参阅[配置用于 Configuration Manager 的 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。

- `management.azure.com`  


## <a name="co-management"></a>共同管理

如果将 Windows 10 设备注册到 Microsoft Intune 以进行共同管理，请确保这些设备可以访问 Intune 所需的终结点。 有关详细信息，请参阅 [Microsoft Intune 的终结点](https://docs.microsoft.com/intune/intune-endpoints)。


## <a name="microsoft-store-for-business"></a>适用于企业的 Microsoft Store

如果将 Configuration Manager 与[适用于企业的 Microsoft Store](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) 集成，请确保服务连接点和目标设备能够访问云服务。 有关详细信息，请参阅[适用于企业的 Microsoft Store 代理配置](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)。


## <a name="bkmk_cloud"></a> 云服务

<!-- SCCMDocs-pr #3402 -->

本部分介绍以下功能：

- 云管理网关 (CMG)
- 云分发点 (CDP)
- Azure Active Directory (Azure AD) 集成
- 基于 Azure AD 的发现

对于 CMG/CDP 服务部署，  服务连接点需要访问：

- 特定的 Azure 终结点因环境而异，具体取决于配置。 Configuration Manager 将这些终结点存储在站点数据库中。 查询 SQL Server 中的 AzureEnvironments 表以获取 Azure 终结点的列表  。  

 CMG 连接点需要访问以下服务终结点：

- ServiceManagementEndpoint: `https://management.core.windows.net/`  

- StorageEndpoint: `blob.core.windows.net` 和 `table.core.windows.net`

对于通过 Configuration Manager 控制台和客户端进行的 Azure AD 令牌检索：  

- ActiveDirectoryEndpoint `https://login.microsoftonline.com/`  

对于 Azure AD 用户发现，  服务连接点需要访问：

- 1810 版及更早版本：Azure AD Graph 终结点 `https://graph.windows.net/`  

- 1902 版及更高版本：Microsoft Graph 终结点 `https://graph.microsoft.com/`

云管理点 (CMG) 连接点站点系统支持使用 Web 代理。 有关配置代理的此角色的详细信息，请参阅[代理服务器支持](proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 CMG 连接点仅需要连接到 CMG 服务终结点。 它不需要访问其他 Azure 终结点。

有关 CMG 的详细信息，请参阅 [CMG 规划](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。


## <a name="bkmk_sum"></a>软件更新

允许活动的软件更新点访问以下终结点，以便 WSUS 和自动更新可以与 Microsoft Update 云服务通信：  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

有关软件更新的详细信息，请参阅[规划软件更新](/sccm/sum/plan-design/plan-for-software-updates)。

### <a name="intranet-firewall"></a>Intranet 防火墙

在以下情况下，你可能需要将终结点添加到两个站点系统之间的防火墙：

- 如果子站点具有软件更新点
- 如果站点上具有基于 Internet 的远程活动软件更新点

#### <a name="software-update-point-on-the-child-site"></a>子站点上的软件更新点

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  


## <a name="manage-office-365"></a>管理 Office 365

如果使用 Configuration Manager 部署和更新 Office 365，请允许以下终结点：

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` - 同步 Office 365 客户端更新的软件更新点

- `config.office.com` - 为 Office 365 部署创建自定义配置


## <a name="configuration-manager-console"></a>Configuration Manager 控制台

具有 Configuration Manager 控制台的计算机需要访问以下 Internet 终结点获取特定功能：

### <a name="in-console-feedback"></a>控制台内反馈

- `http://petrol.office.microsoft.com`

有关此功能的详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#product-feedback)。

### <a name="community-workspace-documentation-node"></a>“社区”工作区、“文档”节点

- `https://aka.ms`

- `https://raw.githubusercontent.com`

有关此控制台节点的详细信息，请参阅[使用 Configuration Manager 控制台](/sccm/core/servers/manage/admin-console)。

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>“监视”工作区、“站点层次结构”节点

如果你使用  “地理视图”，则允许访问以下终结点：

- `http://maps.bing.com`


## <a name="desktop-analytics"></a>桌面分析

有关桌面分析云服务所需终结点的详细信息，请参阅[启用数据共享](/sccm/desktop-analytics/enable-data-sharing#endpoints)。


## <a name="microsoft-public-ip-addresses"></a>Microsoft 公共 IP 地址

有关 Microsoft IP 地址范围的详细信息，请参阅 [Microsoft 公共 IP 空间](https://www.microsoft.com/download/details.aspx?id=53602)。 这些地址会定期更新。 服务没有粒度，可以使用这些范围内的任何 IP 地址。


## <a name="see-also"></a>另请参阅

- [Configuration Manager 中使用的端口](/sccm/core/plan-design/hierarchy/ports)

- [Configuration Manager 中的代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)
