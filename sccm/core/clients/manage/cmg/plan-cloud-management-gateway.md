---
title: 规划云管理网关
titleSuffix: Configuration Manager
description: 规划和设计云管理网关 (CMG)，简化基于 Internet 的客户端管理。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b207ffe95a078c955817d9251da3adbdf4de10d
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中规划云管理网关

*适用范围：System Center Configuration Manager (Current Branch)*
 
<!--1101764-->
云管理网关 (CMG) 提供一种简单的方法来管理 Internet 上的 Configuration Manager 客户端。 将 CMG 部署为 Microsoft Azure 中的云服务，即可管理在 Internet 上漫游的传统客户端，无需其他基础结构。 也不需要将本地基础结构向 Internet 公开。 

> [!Tip]  
> 此功能在 1610 版本中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从 1802 版开始，此功能不再属于预发行功能。  


> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


建立先决条件后，通过在 Configuration Manager 控制台中执行以下三个步骤创建 CMG：
1. 将 CMG 云服务部署到 Azure。
2. 添加 CMG 连接点角色。 
3. 配置服务站点和站点角色。 完成部署和配置后，客户端可无缝访问本地站点角色，无论其位于 Intranet 还是 Internet 上。

本文介绍了关于 CMG 的涵义、如何设计使其符合你的环境以及规划实现的基础知识。 



## <a name="scenarios"></a>方案 

有多种方案受益于 CMG。 以下是一些较常见的方案：  

- 使用 Active Directory 加入域的身份管理传统 Windows 客户端。 这些客户端包括 Windows 7、Windows 8.1 和 Windows 10。 它使用 PKI 证书来保护信道。 管理活动包括：  
    - 软件更新和 Endpoint Protection
    - 清单和客户端状态
    - 符合性设置
    - 到设备的软件分发
    - Windows 10 就地升级任务序列（自版本 1802 起）

- 使用现代身份管理传统 Windows 10 客户端，可以是加入云域的混合 Azure Active Directory (Azure AD) 或纯 Azure Active Directory (Azure AD)。 客户端使用 Azure AD 进行身份验证而不是使用 PKI 证书。 Azure AD 的设置、配置和维护比复杂的 PKI 系统更简单。 管理活动与第一种方案相同，加上：  
    - 到用户的软件分发  

- 通过 Internet 在 Windows 10 设备上安装 Configuration Manager 客户端。 使用 Azure AD 允许设备对 CMG 进行身份验证，以注册和分配客户端。 可手动安装客户端，也可使用其他软件分发方法（如 Microsoft Intune）。  

- 通过共同管理预配新设备。 CMG 不是共同管理所必须的。 但它有助于完成新设备的端到端方案，其中涉及 Windows AutoPilot、Azure AD、Microsoft Intune 和 Configuration Manager。  

### <a name="specific-use-cases"></a>特定用例
在这些方案中，以下特定设备用例可能适用：

- 漫游笔记本电脑等设备  

- 相比通过 WAN 或 VPN，通过 Internet 管理远程/分支办公设备更加便宜、高效。  

- 合并和收购，这可能是将设备加入 Azure AD 并通过 CMG 进行管理的最简单的方法。  

> [!Important]
> 默认情况下，所有客户端都会接收 CMG 的策略，并在其成为基于 Internet 的客户端时开始使用该策略。 可能需要根据适用于组织的方案和用例确定 CMG 的使用范围。 有关详细信息，请参阅[允许客户端使用云管理网关](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway)客户端设置。


## <a name="topology-design"></a>拓扑设计

### <a name="cmg-components"></a>CMG 组件
CMG 部署和操作包括以下组件：  

- Azure 中的“CMG 云服务”对 Configuration Manager 客户端请求进行身份验证并将其转发给 CMG 连接点。  
 
- “CMG 连接点”站点系统角色可实现从本地网络到 Azure 中 CMG 服务的一致且高性能的连接。 它还可将设置发布到 CMG 中，其中包括连接信息和安全设置。 CMG 连接点根据 URL 映射将客户端请求从 CMG 转发到本地角色。

- [服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)站点系统角色运行云服务管理器组件，该组件负责处理所有 CMG 部署任务。 此外，它还可以监视并报告 Azure AD 中的服务运行状况和日志信息。 确保服务连接点处于[联机模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes)。  

- “管理点”站点系统角色按照惯例处理客户端请求。  

- “软件更新点”站点系统角色按照惯例处理客户端请求。  

- “基于 Internet 的客户端”连接到 CMG 以访问本地 Configuration Manager 组件。

- CMG 使用“基于证书的 HTTPS”Web 服务来帮助保护与客户端的网络通信。  

- 基于 Internet 的客户端使用“PKI 证书或 Azure AD”进行标识和身份验证。  

- [云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)按需向基于 Internet 的客户端提供内容。  


### <a name="azure-resource-manager"></a>Azure 资源管理器
<!-- 1324735 -->
从版本 1802 起，可使用 Azure 资源管理器部署来创建 CMG。 [Azure 资源管理器](/azure/azure-resource-manager/resource-group-overview)是一个现代平台，用于以单个实体（称为[资源组](/azure/azure-resource-manager/resource-group-overview#resource-groups)）的方式来管理所有解决方案资源。 如果在 Azure 资源管理器中部署 CMG，站点将使用 Azure Active Directory (Azure AD) 进行身份验证并创建必要的云资源。 此现代化部署不需要经典 Azure 管理证书。  

CMG 向导仍提供使用 Azure 管理证书的“经典服务部署”选项。 要简化资源的部署和管理，建议为所有新的 CMG 实例使用 Azure 资源管理器部署模型。 如果可以，请通过资源管理器重新部署现有 CMG 实例。 有关详细信息，请参阅[修改 CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg)。

> [!IMPORTANT]  
> 此功能不提供对 Azure 云服务提供商 (CSP) 的支持。 Azure 资源管理器中的 CMG 部署将继续使用 CSP 不支持的经典云服务。 有关详细信息，请参阅 [Azure CSP 中可用的 Azure 服务](/azure/cloud-solution-provider/overview/azure-csp-available-services)。 


### <a name="hierarchy-design"></a>层次结构设计

在层次结构的顶层站点创建 CMG。 如果该站点为管理中心站点，则可在子级主站点创建 CMG 连接点。 云服务管理器组件位于服务连接点上，该连接点也位于管理中心站点上。 如有需要，此设计可在不同主站点上共享该服务。

可在 Azure 中创建多个 CMG 服务，并且可创建多个 CMG 连接点。 多个 CMG 连接点提供从 CMG 到本地角色的客户端流量负载均衡。 要减少网络延迟，请将关联的 CMG 分配到与主站点相同的地理区域。

 > [!Note]  
 > 基于 Internet 的客户端和 CMG 不属于任何边界组。

其他因素（如要管理的客户端数量）也会影响 CMG 的设计。 有关详细信息，请参阅[性能和规模](#performance-and-scale)。

#### <a name="example-1-standalone-primary-site"></a>示例 1：独立主站点

在纽约总部，Contoso 在本地数据中心内有一个独立的主站点。 
- 他们会在美国东部 Azure 区域创建 CMG 以减少网络延迟。 
- 他们会创建两个 CMG 连接点，这两个连接点都与单个 CMG 服务相关联。  

当客户端漫游到 Internet 时，他们就会与美国东部 Azure 区域的 CMG 通信。 CMG 通过这两个 CMG 连接点转发此通信。

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>示例 2：具有站点特定的 CMG 的层次结构

在西雅图总部，Fourth Coffee 在本地数据中心有一个管理中心站点。 一个主站点位于同一数据中心，另一主站点位于其巴黎的欧洲主办事处。 
- 在管理中心站点上，他们会创建两个 CMG 服务：
     - 一个是美国西部 Azure 区域的 CMG。
     - 一个是欧洲西部 Azure 区域的 CMG。
- 在西雅图的主站点上，他们会创建一个与美国西部 CMG 关联的 CMG 连接点。
- 在巴黎的主站点上，他们会创建一个与欧洲西部 CMG 关联的 CMG 连接点。

当西雅图的客户端漫游到 Internet 时，他们就会与美国西部 Azure 区域的 CMG 通信。 CMG 将此通信转发给西雅图的 CMG 连接点。

同样，当巴黎的客户端漫游到 Internet 时，他们就会与欧洲西部 Azure 区域的 CMG 通信。 CMG 将此通信转发给巴黎的 CMG 连接点。 当巴黎的用户前往位于西雅图的公司总部时，他们的电脑会继续与欧洲西部 Azure 区域的 CMG 通信。 

 > [!Note]  
 > Fourth Coffee 考虑在与美国西部 CMG 关联的巴黎主站点上创建另一个 CMG 连接点。 此后巴黎的客户不管是在哪里都能使用两个 CMG。 虽然此配置有助于实现流量负载均衡并提供服务冗余，但当巴黎的客户与美国 CMG 通信时，这也会造成延迟。 Configuration Manager 客户端目前无法识别其地理区域，因此请不要选择地理位置更靠近的 CMG。 客户端会随机使用可用的 CMG。



## <a name="requirements"></a>要求

- 承载 CMG 的 Azure 订阅。  

    - Azure 管理员需参与某些组件的初始创建，具体视设计而定。 此角色不需要 Configuration Manager 中的权限。  

- 至少一个承载 CMG 连接点的本地 Windows 服务器。 可将此角色与其他 Configuration Manager 站点系统角色归置在一起。  

- 服务连接点必须处于[联机模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes)。   

- 用于 CMG 的[服务器身份验证证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate)。  

- 如果使用 Azure 经典部署方法，则必须使用 [Azure 管理证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate)。  

    > [!TIP]  
    > 从 Configuration Manager 版本 1802 起，推荐使用 **Azure 资源管理器**部署模型。 它不需要此管理证书。  

- 可能需要其他证书，具体取决于客户端操作系统版本和身份验证模型。 有关详细信息，请参阅 [CMG 证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)。  

    - 从 1802 版起，必须将所有启用了 CMG 的[**管理点配置为使用 HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https)。  

- 对于 Windows 10 客户端可能需要与 Azure AD 集成。 有关详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。  

- 客户端必须使用 IPv4。  



## <a name="specifications"></a>规格

- CMG 支持[客户端和设备支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中列出的所有 Windows 版本。  

- CMG 只支持管理点和软件更新点角色。  

- CMG 不支持仅与 IPv6 地址通信的客户端。<!--495606-->  

- 使用网络负载均衡器的软件更新点不适用于 CMG。 <!--505311-->  

- 从版本 1802 起，使用 Azure 资源模型的 CMG 部署不启用对 Azure 云服务提供程序 (CSP) 的支持。 Azure 资源管理器中的 CMG 部署将继续使用 CSP 不支持的经典云服务。 有关详细信息，请参阅 [Azure CSP 中可用的 Azure 服务](/azure/cloud-solution-provider/overview/azure-csp-available-services)  


### <a name="support-for-configuration-manager-features"></a>Configuration Manager 功能支持
下表列出了 CMG 对 Configuration Manager 的功能支持：


|功能  |支持  |
|---------|---------|
| 软件更新     | ![支持](media/green_check.png) |
| Endpoint Protection     | ![支持](media/green_check.png) |
| 硬件和软件清单     | ![支持](media/green_check.png) |
| 客户端状态和通知     | ![支持](media/green_check.png) |
| 运行脚本     | ![支持](media/green_check.png) |
| 符合性设置     | ![支持](media/green_check.png) |
| 客户端安装</br>（带 Azure AD 集成）     | ![支持](media/green_check.png)  (1706) |
| 软件分发（以设备为目标）     | ![支持](media/green_check.png) |
| 软件分发（以用户为目标，必需）</br>（带 Azure AD 集成）     | ![支持](media/green_check.png)  (1710) |
| 软件分发（以用户为目标，可用）</br>（[所有要求](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)） | ![支持](media/green_check.png)  (1802) |
| Windows 10 就地升级任务序列     | ![支持](media/green_check.png)  (1802) |
| 任何其他任务序列方案     | ![不支持](media/Red_X.png) |
| 客户端推送     | ![不支持](media/Red_X.png) |
| 自动站点分配     | ![不支持](media/Red_X.png) |
| 应用程序目录     | ![不支持](media/Red_X.png) |
| 软件批准请求     | ![不支持](media/Red_X.png) |
| Configuration Manager 控制台     | ![不支持](media/Red_X.png) |
| 远程工具     | ![不支持](media/Red_X.png) |
| 报表网站     | ![不支持](media/Red_X.png) |
| LAN 唤醒     | ![不支持](media/Red_X.png) |
| Mac、Linux 和 UNIX 客户端     | ![不支持](media/Red_X.png) |
| 对等缓存     | ![不支持](media/Red_X.png) |
| 本地 MDM     | ![不支持](media/Red_X.png) |


|项|
|--|
|![支持](media/green_check.png) = 所有受支持的 Configuration Manager 版本的 CMG 都支持此功能  |
|![支持](media/green_check.png) (YYMM) = 自 Configuration Manager YYMM 版起，CMG 支持此功能  |
|![不支持](media/Red_X.png) ＝ CMG 不支持此功能 |



## <a name="cost"></a>成本

>[!IMPORTANT]  
>以下费用信息仅用作估算用途。 环境可能具有其他会影响使用 CMG 总费用的变量。

CMG 使用以下 Azure 组件，使用这些组件会向 Azure 订阅帐户收费：

#### <a name="virtual-machine"></a>虚拟机

- CMG 使用 Azure 云服务作为平台即服务 (PaaS)。 此服务使用会产生计算成本的虚拟机 (VM)。  

- 在 Configuration Manager 1706 版中，CMG 使用标准的 A2 VM。  

- 自 Configuration Manager 1710 版起，CMG 使用标准的 A2 V2 VM。  

- 你可以选择有多少 VM 实例支持 CMG。 默认为 1 个，最多 16 个。 创建 CMG 时会设置此数字，随后可根据需要进行更改，缩放服务。

- 若要详细了解支持客户端所需的 VM 数量，请参阅[性能和规模](#performance-and-scale)。

- 请参阅 [Azure 定价计算器](https://azure.microsoft.com/pricing/calculator/)以帮助确定潜在的费用。

    > [!NOTE]  
    > 虚拟机费用因区域而异。

#### <a name="outbound-data-transfer"></a>出站数据传输

- 根据从 Azure 流出的数据收取费用（出口或下载）。 所有流入 Azure 的数据均不收费（入口或上传）。 CMG 数据从 Azure 流出，包括策略到客户端、客户端通知和由 CMG 转发到站点的客户端响应。 这些响应包括库存报表、状态消息和符合性状态。  

- 即使没有任何客户端与 CMG 进行通信，某些后台通信也会使 CMG 和本地站点之间出现网络流量。  

- 在 Configuration Manager 控制台中查看出站数据传输 (GB)。 有关详细信息，请参阅[监视 CMG 上的客户端](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)。  

- 请参阅 [Azure 带宽定价详细信息](https://azure.microsoft.com/pricing/details/bandwidth/)以帮助确定潜在的费用。 数据传输定价是分层的。 使用得越多，每 GB 支付的费用就越少。  

- 出于估算目的，可假设基于 Internet 的每个客户端每月大约耗费 100－300 MB。 预计默认客户端配置使用的数据会更少。 预计高性能客户端配置使用的数据会更多。 实际使用情况可能会有所不同，具体取决于客户端设置的配置。  

   > [!NOTE]  
   > 执行其他操作（例如，部署软件更新或应用程序）时，从 Azure 传输的出站数据量会增加。

#### <a name="content-storage"></a>内容存储

- 基于 Internet 的客户端可免费从 Windows 更新获取 Microsoft 软件更新内容。 不要将包含 Microsoft 更新内容的更新包分发到云分发点，否则可能会造成存储和数据出口成本。  

- 对于任何其他必要内容（例如应用程序或第三方软件更新），必须分发到基于云的分发点。 目前，将内容发送给客户端时，CMG 仅支持基于云的分发点。  

- 有关详细信息，请参阅使用[基于云的分发](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution)的成本。  

#### <a name="other-costs"></a>其他成本

- 每个云服务都具有一个动态 IP 地址。 每个不同的 CMG 都使用新的动态 IP 地址。 为每个 CMG 添加更多 VM 不会使这些地址增加。  



## <a name="performance-and-scale"></a>性能和规模

有关 CMG 规模的详细信息，请参阅[调整大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)。

以下建议有助于提高 CMG 的性能：

- 如果可能，在同一网络区域中配置 CMG、CMG 连接点和 Configuration Manager 站点服务器，以减少延迟。  

- 目前，Configuration Manager 客户端和 CMG 之间的连接无法感知区域。  

- 为实现服务的高可用性，请为每个站点创建至少两个 CMG 服务和两个 CMG 连接点。  

- 可以添加更多 VM 实例，将 CMG 扩展为支持更多客户端。 Azure 负载均衡器可控制客户端与服务的连接。  

- 创建更多的 CMG 连接点，在它们之间分配负载。 CMG 以轮询机制的方式将流量分发到其连接的 CMG 连接点。  

- 客户端数量超过受支持的数量导致 CMG 处于高负载状态时，它仍可处理请求，但可能会有延迟。  


> [!Note]  
> 虽然 Configuration Manager 对 CMG 连接点的客户端数量没有硬性限制，但 Windows Server 的默认最大 TCP 动态端口范围为 16384。 如果 Configuration Manager 站点通过一个 CMG 连接点管理超过 16384 个客户端，则必须增加 Windows 服务器的限制。 所有客户端都为客户端通知保留一个通道，该通道在 CMG 连接点上开放有一个端口。 有关如何使用 netsh 命令来增加此限制的详细信息，请参阅[Microsoft 支持文章 929851](https://support.microsoft.com/help/929851)。



## <a name="ports-and-data-flow"></a>端口和数据流

无需打开本地网络的任何入站端口。 服务连接点和 CMG 连接点可启动与 Azure 和 CMG 的所有通信。 这两个站点系统角色必须能够创建到 Microsoft 云的出站连接。 服务连接点部署并监视 Azure 中的服务，因此必须处于联机模式。 CMG 连接点可连接到 CMG 以管理 CMG 和本地站点系统角色间的通信。

下图是一个基本的 CMG 概念数据流：![CMG 数据流](media/cmg-data-flow.png)
   1. 服务连接点通过 HTTPS 端口 443 连接到 Azure。 它使用 Azure AD 或 Azure 管理证书进行身份验证。 服务连接点在 Azure 中部署 CMG。 CMG 使用服务器身份验证证书创建 HTTPS 云服务。  

   2. CMG 连接点通过 TCP-TLS 或 HTTPS 连接到 Azure 中的 CMG。 它使连接处于开放状态，并为将来的双向通信建立通道。   

   3. 客户端通过 HTTPS 端口 443 连接到 CMG。 它使用 Azure AD 或客户端身份验证证书进行身份验证。  

   4. CMG 通过现有连接将客户端通信转发到本地 CMG 连接点。 无需打开任何入站防火墙端口。  

   5. CMG 连接点将客户端通信转发到本地管理点和软件更新点。  

### <a name="required-ports"></a>所需端口
此表列出了所需网络端口和协议。 客户端是启动连接的设备，需要出站端口。 服务器是接受连接的设备，需要入站端口。 

| 客户端  | 协议 | 端口  | 服务器  | 说明  |
|---------|---------|---------|---------|---------|
| 服务连接点     | HTTPS | 443        | Azure        | CMG 部署 |
| CMG 连接点     |  TCP-TLS | 10140-10155        | CMG 服务        | 建立 CMG 通道的首选协议<sup>1</sup> |
| CMG 连接点     | HTTPS | 443        | CMG 服务       | 回退，将 CMG 通道构建为只有一个 VM 实例<sup>2</sup> |
| CMG 连接点     |  HTTPS   | 10124-10139     | CMG 服务       | 回退，将 CMG 通道构建为有连两个或以上的 VM 实例<sup>3</sup> |
| 客户端     |  HTTPS | 443         | CMG        | 常规客户端通信 |
| CMG 连接点      | HTTPS 或 HTTP | 443 或 80         | 管理点</br>（版本 1706 或 1710） | 本地流量，端口取决于管理点配置 |
| CMG 连接点      | HTTPS | 443      | 管理点</br>（版本 1802） | 本地流量必须经由 HTTPS |
| CMG 连接点      | HTTPS 或 HTTP | 443 或 80         | 软件更新点 | 本地流量，端口取决于软件更新点配置 |

<sup>1</sup> CMG 连接点先尝试与每个 CMG VM 实例建立长期 TCP-TLS 连接。 它会连接到端口 10140 上的第一个 VM 实例。 第二个 VM 实例使用端口 10141，直到端口 10155 上的第十六个实例。 TCP TLS 连接性能最佳，但不支持 Internet 代理。 如果 CMG 连接点无法通过 TCP-TLS 进行连接，则会回退到 HTTPS<sup>2</sup>。  

<sup>2</sup> 如果 CMG 连接点无法通过 TCP-TLS 连接到 CMG<sup>1</sup>，则会通过仅用于一个 VM 实例的 HTTPS 443 连接到 Azure 网络负载均衡器。  

<sup>3</sup> 如果有两个或多个 VM 实例，则 CMG 连接点将为第一个 VM 实例使用 HTTPS 10124，而不是 HTTPS 443。 它会连接到 HTTPS 10125 上的第二个 VM 实例，直到 HTTPS 端口 10139 上的第十六个 VM 实例。


### <a name="internet-access-requirements"></a>Internet 访问要求

CMG 连接点站点系统支持使用 Web 代理。 有关配置代理的此角色的详细信息，请参阅[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server)。 CMG 连接点需要连接到以下终结点：  

- 特定的 Azure 终结点因环境而异，具体取决于配置。 Configuration Manager 将这些终结点存储在站点数据库中。 查询 SQL Server 中的 AzureEnvironments 表以获取 Azure 终结点的列表。  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- 对于通过 Configuration Manager 控制台和客户端进行的 Azure AD 令牌检索：ActiveDirectoryEndpoint (https://login.microsoftonline.com/)  

- 对于 Azure AD 用户发现：AAD Graph 终结点 (https://graph.windows.net/)  



## <a name="next-steps"></a>后续步骤

- [云管理网关的证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [云管理网关的安全和隐私](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [云管理网关的大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [有关云管理网关的常见问题解答](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [设置云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
