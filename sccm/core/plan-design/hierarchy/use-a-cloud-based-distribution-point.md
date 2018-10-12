---
title: 云分发点
titleSuffix: Configuration Manager
description: 规划和设计，以通过 Microsoft Azure 和 Configuration Manager 中的云分发点来分发软件内容。
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79b17ba00274459401dc81035833163e75939be0
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601137"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>在 Configuration Manager 中使用云分发点

*适用范围：System Center Configuration Manager (Current Branch)*

云分发点是 Configuration Manager 分发点，在 Microsoft Azure 中作为平台即服务 (PaaS) 托管。 此服务支持以下方案：  

- 向基于 Internet 的客户端提供软件内容，而无需其他本地基础结构  

- 支持云的内容分发系统  

- 减少对传统分发点的需求  


本文将帮助你了解云分发点，规划其使用以及设计实现。 它包括以下部分：
- [功能和优势](#bkmk_features)
- [拓扑设计](#bkmk_topology)
- [惠?](#bkmk_requirements)
- [规范](#bkmk_spec)
- [成本](#bkmk_cost)
- [性能和规模](#bkmk_perf)
- [端口和数据流](#bkmk_dataflow)
- [证书](#bkmk_certs)
- [常见问题 (FAQ)](#bkmk_faq)



## <a name="bkmk_features"></a>功能和优势

### <a name="features"></a>功能

云分发点支持多种功能，本地分发点也提供这些功能：  

-   可以单独或者作为分发点组成员来管理云分发点  

-   可以将云分发点用作回退内容位置  

-   支持基于 Intranet 的客户端和基于 Internet 的客户端  


### <a name="benefits"></a>优点

云分发点具有以下其他优势：  

-   该站点在将内容发送到 Azure 中的云分发点之前对其进行加密。  

-   要满足客户端不断变化的内容请求需求，请在 Azure 中手动扩展云服务。 此操作无需你在 Configuration Manager 中安装和预配其他分发点。  

-   支持从为其他内容技术配置的客户端下载内容，如 Windows BranchCache 和替换内容提供程序。  

-   从版本 1806 开始，使用云分发点作为拉取分发点的源位置。  


## <a name="bkmk_topology"></a>拓扑设计

云分发点部署和操作包括以下组件：  

- Azure 中的“云服务”。 该站点将内容分发到此服务，该服务将其存储在 Azure 云存储中。 管理点根据需要向客户端提供可用源列表中的此内容位置。  

- “管理点”站点系统角色按照惯例处理客户端请求。  

    - 本地客户端通常使用本地管理点。  

    - 基于 Internet 的客户端使用[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)或[基于 Internet 的管理点](/sccm/core/clients/manage/plan-internet-based-client-management)。  

- 云分发点使用“基于证书的 HTTPS”Web 服务来帮助保护与客户端的网络通信。 客户端必须信任此证书。  


### <a name="azure-resource-manager"></a>Azure 资源管理器
<!--1322209-->从版本 1806 起，使用 Azure 资源管理器部署来创建云分发点。 [Azure 资源管理器](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)是一个现代平台，用于以单个实体（称为[资源组](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)）的方式来管理所有解决方案资源。 如果在 Azure 资源管理器中部署云分发点，站点将使用 Azure Active Directory (Azure AD) 进行身份验证并创建必要的云资源。 此现代化部署不需要经典 Azure 管理证书。  

云分发点向导仍提供使用 Azure 管理证书的“经典服务部署”选项。 若要简化资源的部署和管理，Microsoft 建议为所有新的云分发点使用 Azure 资源管理器部署模型。 如果可以，请通过资源管理器重新部署现有云分发点。

Configuration Manager 不会将现有经典云分发点迁移到 Azure 资源管理器部署模型。 使用 Azure 资源管理器部署创建新的云分发点，然后删除经典云分发点。 

> [!IMPORTANT]  
> 此功能不提供对 Azure 云服务提供商 (CSP) 的支持。 Azure 资源管理器中的云发分点部署将继续使用 CSP 不支持的经典云服务。 有关详细信息，请参阅 [Azure CSP 中可用的 Azure 服务](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  


### <a name="hierarchy-design"></a>层次结构设计

创建云分发点的位置取决于哪些客户端需要访问内容。 从版本 1806 开始，有三种类型的云分发点：  

- 经典服务部署：仅在主站点上创建此类型。  

- Azure 资源管理器部署：在主站点或管理中心站点上创建此类型。  

- 云管理网关还可向客户端提供内容。 此功能减少了所需的证书和 Azure VM 的成本。 有关详细信息，请参阅[规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。<!--1358651-->  


要确定是否将云分发点包括在边界组中，请考虑以下行为：  

- 基于 Internet 的客户端不依赖于边界组。 它们只使用面向 Internet 的分发点或云分发点。 如果仅使用云分发点提供这些类型的客户端，则无需将它们包含在边界组中。  

- 如果希望内部网络上的客户端使用云分发点，则它需要与客户端位于同一边界组中。 客户端在其内容源列表中将云分发点的优先级设置为最低，因为从 Azure 外下载内容会产生相关成本。 因此，云分发点通常用作基于 Intranet 的客户端的回退源。 如果需要云优先设计，则设计边界组以满足此业务需求。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)。  


即使在 Azure 的特定区域中安装云分发点，客户端也不会知道 Azure 区域。 它们随机选择云分发点。 如果在多个区域中安装云分发点，并且客户端在内容位置列表中收到多个分发点，则客户端可能不会使用同一 Azure 区域中的云分发点。  


### <a name="backup-and-recovery"></a>备份和恢复  

在层次结构中使用云分发点时，请使用下列信息来帮助你规划备份和恢复：  

- 使用“备份站点服务器”维护任务时，Configuration Manager 会自动包括云分发点的配置。  

- 备份并保存服务器身份验证证书的副本。 如果在 Azure 中使用经典服务部署，也要备份并保存 Azure 管理证书的副本。 将 Configuration Manager 主站点还原到其他服务器时，必须重新导入证书。  



##  <a name="bkmk_requirements"></a>要求

- 需要“Azure 订阅”以承载该服务。  

    - Azure 管理员需参与某些组件的初始创建，具体视设计而定。 此角色不需要 Configuration Manager 中的权限。  

- 站点服务器需要 Internet 访问来部署和管理云服务。  

- 如果使用 Azure 经典部署方法，则需要 Azure 管理证书。 有关详细信息，请参阅以下[证书](#bkmk_certs)部分。   

    > [!TIP]  
    > 从 Configuration Manager 版本 1806 开始，使用 Azure 资源管理器部署模型。 它不需要此管理证书。  

- 如果使用 Azure 资源管理器部署方法，请将 Configuration Manager 与 [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure) 集成。 不需要 Azure AD 用户发现。  

- 服务器身份验证证书。 有关详细信息，请参阅以下[证书](#bkmk_certs)部分。  

    - 若要降低复杂性，Microsoft 建议为服务器身份验证证书使用公共证书提供程序。 执行此操作时，还需要 DNS CNAME 别名，以便客户端解析云服务的名称。  

- 在“云服务”组中，将客户端设置“允许访问云分发点”设置为“是”。 默认情况下，此值设为“否” 。  

- 客户端设备需要“Internet 连接”，并且必须使用 IPv4。  



## <a name="bkmk_spec"></a>规范

- 云分发点支持[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中列出的所有 Windows 版本。  

- 管理员分发以下类型的受支持软件内容：  
    - 应用程序
    - 包
    - OS 升级包
    - 第三方软件更新  

    > [!Important]  
    > 虽然 Configuration Manager 控制台不会阻止将 Microsoft 软件更新分发到云分发点，但需支付 Azure 费用来存储客户端不使用的内容。 基于 Internet 的客户端始终从 Microsoft 更新云服务获取 Microsoft 软件更新内容。 请勿将 Microsoft 软件更新分发到云分发点。    

- 从版本 1806 开始，配置拉取分发点以将云分发点用作源。 有关详细信息，请参阅[关于源分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point#about-source-distribution-points)。<!--1321554-->  


### <a name="deployment-settings"></a>部署设置

- 当使用“需要时通过运行任务序列本地下载内容”部署任务序列时，管理点不包括作为内容位置的云分发点。 使用选项“启动任务序列之前本地下载所有内容”部署任务序列，以便客户端使用云分发点。  

- 云分发点不支持使用“从分发点运行程序”选项进行包部署。 使用部署选项“从分发点下载内容并本地运行”。  


### <a name="limitations"></a>限制  

- 无法将云分发点用于 PXE 或启用多播的部署。  

- 云分发点不支持 App-V 流式处理应用程序。  

- 无法在云分发点上[预安排内容](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)。 管理云分发点的主站点的分发管理器传输所有内容。  

- 无法将云分发点配置为拉取分发点。  



##  <a name="bkmk_cost"></a>成本   
<!--501018-->
> [!IMPORTANT]  
> 以下费用信息仅用作估算用途。 环境可能具有其他可影响使用云分发点总费用的变量。  

Configuration Manager 包括用于帮助控制成本和监视数据访问的以下选项：  

- 控制和监视云服务中存储的内容量。 有关详细信息，请参阅[监视云分发点](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor)。  

- 将 Configuration Manager 配置为在客户端下载的“阈值”达到或超过每月限制时发出通知。 有关详细信息，请参阅[数据传输阈值警报](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_alerts)。   

- 要帮助减少客户端从云分发点传输数据的数量，请使用以下任一对等缓存技术：  
    - Configuration Manager 对等缓存
    - Windows BranchCache
    - Windows 10 传递优化  

   有关详细信息，请参阅[内容管理的基本概念](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)。   


### <a name="components"></a>组件数

云分发点使用以下 Azure 组件，使用这些组件会向 Azure 订阅帐户收费：  

> [!Tip]  
> 从版本 1806 开始，云管理网关还可向客户端提供内容。 此功能通过整合 Azure VM 降低了成本。 有关详细信息，请参阅[云管理网关的成本](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#cost)。  

#### <a name="virtual-machine"></a>虚拟机
- 云分发点使用 Azure 云服务作为平台即服务 (PaaS)。 此服务使用会产生计算成本的虚拟机 (VM)。  

- 每项云分发点服务使用两个标准 A0 VM。  

- 请参阅 [Azure 定价计算器](https://azure.microsoft.com/pricing/calculator/)以帮助确定潜在的费用。

    > [!NOTE]  
    > 虚拟机费用因区域而异。

#### <a name="outbound-data-transfer"></a>出站数据传输
- 所有流入 Azure 的数据均不收费（入口或上传）。 将内容从站点分发到云分发点即上传到 Azure。  

- 根据从 Azure 流出的数据收取费用（出口或下载）。 Azure 外的云分发点数据流包含客户端下载的软件内容。  

- 有关详细信息，请参阅[监视云分发点](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor)。  

- 请参阅 [Azure 带宽定价详细信息](https://azure.microsoft.com/pricing/details/bandwidth/)以帮助确定潜在的费用。 数据传输定价是分层的。 使用得越多，每 GB 支付的费用就越少。  

#### <a name="content-storage"></a>内容存储
- 基于 Internet 的客户端可免费从 Microsoft 更新云服务获取 Microsoft 软件更新内容。 请勿将带有 Microsoft 软件更新的软件更新部署包分发到云分发点。 否则，对于客户端从未使用过的内容，将产生数据存储费用。  

- 根据部署模型，云分发点使用以下标准 BLOB 存储：  

    - 经典部署使用 Azure 异地冗余存储 (GRS)。 有关详细信息，请参阅[异地冗余存储](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs)。  

    - Azure 资源管理器部署使用 Azure 本地冗余存储 (LRS)。 此更改可降低存储帐户的成本。 经典部署不使用 GRS 的其他功能。 有关详细信息，请参阅[本地冗余存储](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs)。  

#### <a name="other-costs"></a>其他成本
- 每个云服务都具有一个动态 IP 地址。 每个不同的云分发点使用新的动态 IP 地址。 为每个云服务添加更多 VM 不会使这些地址增加。  



##  <a name="bkmk_dataflow"></a>端口和数据流   

云分发点有两个主要数据流：  

- 站点服务器连接到 Azure 以设置云分发点服务  

- 客户端连接到云分发点以下载内容  


### <a name="site-server-to-azure"></a>站点服务器到 Azure

无需打开本地网络的任何入站端口。 站点服务器启动与 Azure 和云分发点的所有通信，以部署、更新和管理云服务。 该站点服务器必须能创建到 Microsoft 云的出站连接。 此操作等效于在特定站点上安装分发点站点系统角色。  


### <a name="client-to-cloud-distribution-point"></a>客户端到云分发点

无需打开本地网络的任何入站端口。 基于 Internet 的客户端直接与 Azure 服务进行通信。 内部网络上使用云分发点的客户端必须能够连接 Microsoft 云。 

有关内容位置优先级以及基于 Intranet 的客户端何时使用云分发点的详细信息，请参阅[内容源优先级](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority)。

当客户端将云分发点用作内容位置时：  

1. 管理点为客户端提供访问令牌以及内容源列表。 此令牌有效期为 24 小时，并允许客户端访问云分发点。  

2. 管理点使用云分发点的服务 FQDN 响应客户端的位置请求。 此属性与服务器身份验证证书的公用名相同。  

    如果正在使用域名（如 WallaceFalls.contoso.com），则客户端首先尝试解析此 FQDN。 域的面向 Internet 的 DNS 中需要有一个 CNAME 别名，以便客户端解析 Azure 服务名称（如：WallaceFalls.cloudapp.net）。  

3. 接下来，客户端将 Azure 服务名称（如 WallaceFalls.cloudapp.net）解析为有效的 IP 地址。 应由 Azure DNS 处理此响应。  

4. 此客户端连接到云分发点。 Azure 负载均衡与其中某个 VM 实例的连接。 客户端使用访问令牌进行身份验证。  

5. 云分发点对客户端的访问令牌进行身份验证，然后为客户端提供 Azure 存储中的准确内容位置。  

6. 如果客户端信任云分发点的服务器身份验证证书，则它会连接到 Azure 存储以下载内容。 



##  <a name="bkmk_perf"></a>性能和规模   
<!--494872-->

与任何分发点设计一样，请考虑以下因素：  
- 并发客户端连接数
- 客户端下载内容的大小
- 满足业务需求所允许的时长 

根据[拓扑设计](#bkmk_topology)，如果客户端可为任何给定内容选择多个云分发点，它们自然会在这些云服务中随机化。 如果只将某个内容分发到单个云分发点，并且大量客户端尝试同时下载此内容，则此活动会对该单个云分发点施加更高的负载。 添加其他云分发点还包括单独的 Azure 存储服务。 有关客户端如何与云分发点组件通信以及下载内容的详细信息，请参阅[端口和数据流](#bkmk_dataflow)。  

云分发点使用两个 Azure VM 作为 Azure 存储的前端。 此默认部署可满足大多数客户的需求。 在某些极端情况下，由于存在大量并发客户端连接（例如，150,000 个客户端），Azure VM 的处理能力无法满足客户端请求。 无法调整用于云分发点的 Azure VM 的大小。 虽然无法在 Configuration Manager 中配置云分发点的 VM 实例数，但如有必要，请在 Azure 门户中重新配置云服务。 手动添加更多 VM 实例，或将服务配置为自动缩放。 

> [!Important]  
> 更新 Configuration Manager 时，站点将重新部署云服务。 如果在 Azure 门户中手动重新配置云服务，则实例数将重置为默认值 2。  

Azure 存储服务对于单个文件支持每秒 500 个请求。 单个云分发点的性能测试支持在 24 小时内将单个 100 MB 文件分发到 50,000 个客户端。<!--512106-->  



##  <a name="bkmk_certs"></a>证书  

根据云分发点设计，你需要一个或多个数字证书。  


### <a name="general-information"></a>常规信息
<!--SCCMDocs issue #779--> 云分发点的证书支持以下配置：  

- 4096 位密钥长度  

- 从 1710 版开始，支持第 3 版证书。 有关详细信息，请参阅 [CNG 证书概述](/sccm/core/plan-design/network/cng-certificates-overview)。  

- 从 1802 版开始，使用以下策略配置 Windows 时：系统加密：使用 FIPS 兼容的算法进行加密、哈希处理和签名  

- 从 1802 版开始，支持 TLS 1.2。 有关详细信息，请参阅[加密控制技术参考](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities)。  


### <a name="azure-management-certificate"></a>Azure 管理证书

经典服务部署需要此证书。Azure 资源管理器部署不需要此证书。

如果使用 Azure 经典部署方法，则需要 Azure 管理证书。 有关详细信息，请参阅“云管理网关证书”一文的 [Azure 管理证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate)部分。 Configuration Manager 站点服务器使用此证书对 Azure 进行身份验证，以创建和管理经典部署。  

> [!TIP]  
> 从 Configuration Manager 版本 1806 开始，使用 Azure 资源管理器部署模型。 它不需要此管理证书。  

要降低复杂性，请在所有 Azure 订阅和所有 Configuration Manager 站点中为云分发点和云管理网关的所有经典部署使用相同的 Azure 管理证书。


### <a name="server-authentication-certificate"></a>服务器身份验证证书

所有云分发点部署都需要此证书。

有关详细信息，请参阅 [CMG 服务器身份验证证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate)，并根据需要参阅以下小节：  
- 针对客户端的 CMG 受信任的根证书
- 由公共提供程序颁发的服务器身份验证证书
- 企业 PKI 颁发的服务器身份验证证书

云分发点以与云管理网关相同的方式使用此类型的证书。 客户端还需要信任此证书。 要降低复杂性，Microsoft 建议使用公共提供程序颁发的证书。 

除非使用通配符证书，否则请勿重复使用相同证书。 云分发点和云管理网关的每个实例都需要唯一的服务器身份验证证书。 

有关从 PKI 创建此证书的详细信息，请参阅[部署云分发点的服务证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012)。  



##  <a name="bkmk_faq"></a>常见问题 (FAQ)   

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>客户端是否需要证书才能从云分发点下载内容？

无需客户端身份验证证书。 客户端确实需要信任云分发点使用的服务器身份验证证书。 如果此证书由公共证书提供程序颁发，则大多数 Windows 设备已包含这些提供程序的受信任的根证书。 如果从组织的 PKI 颁发了服务器身份验证证书，那么客户端需要信任整个链中的颁发证书。 此链包括根证书颁发机构和任何中间证书颁发机构。 根据 PKI 设计，此证书可能会增加部署云分发点的复杂性。 要避免此复杂性，Microsoft 建议使用客户端已信任的公共证书提供程序。  


### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>本地客户端可使用云分发点吗？

是。 如果希望内部网络上的客户端使用云分发点，则它需要与客户端位于同一边界组中。 客户端在其内容源列表中将云分发点的优先级设置为最低，因为从 Azure 外下载内容会产生相关成本。 因此，云分发点通常用作基于 Intranet 的客户端的回退源。 如果需要云优先设计，请相应地设计边界组。 有关详细信息，请参阅[配置边界组](/sccm/core/servers/deploy/configure/boundary-groups)。  


### <a name="do-i-need-azure-expressroute"></a>我需要 Azure ExpressRoute 吗？

通过 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 可将本地网络扩展到 Microsoft 云中。 对 Configuration Manager 云分发点而言，ExpressRoute 或其他此类虚拟网络连接不是必需的。  

如果组织使用 ExpressRoute，请从使用 ExpressRoute 的订阅中隔离云分发点的 Azure 订阅。 此配置可确保云分发点不以这种方式意外连接。  


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>我需要维护 Azure 虚拟机吗？

不需要维护。 云分发点的设计使用 Azure 平台即服务 (PaaS)。 通过使用你提供的订阅，Configuration Manager 可创建必要的 VM、存储和网络。 Azure 可保护和更新虚拟机。 与基础结构即服务 (IaaS) 一样，这些 VM 不是本地环境的一部分。 云分发点是将 Configuration Manager 环境扩展到云端的 PaaS。 有关详细信息，请参阅 [PaaS 云服务模型的安全优势](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model)。  


### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>云分发点是否使用 Azure CDN？

Azure 内容分发网络 (CDN) 是一种全球解决方案，可通过在全球各地具有战略意义的物理节点上缓存内容，快速提供高带宽内容。 有关详细信息，请参阅[什么是 Azure CDN？](https://docs.microsoft.com/azure/cdn/cdn-overview)。

Configuration Manager 云分发点当前不支持 Azure CDN。



## <a name="next-steps"></a>后续步骤
[安装云分发点](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)
