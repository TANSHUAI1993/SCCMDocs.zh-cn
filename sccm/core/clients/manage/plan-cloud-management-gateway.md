---
title: "规划云管理网关 | Microsoft Docs"
description: 
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a7380ae781447880ffcba0778694ea62e10c4889
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中规划云管理网关

*适用范围：System Center Configuration Manager (Current Branch)*

从版本 1610 开始，云管理网关提供一种简单的方法来管理 Internet 上的 Configuration Manager 客户端。 云管理网关服务会部署到 Microsoft Azure 并需要 Azure 订阅。 会使用一个名为云管理网关连接点的新角色将该服务连接到本地 Configuration Manager 基础结构。 部署并配置好后，客户端可以访问本地 Configuration Manager 站点系统角色，而不管它们是在内部专用网络上还是在 Internet 上。

> [!TIP]  
> 与版本 1610 一起引入，云管理网关是一项预发行功能。 若要启用此功能，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/pre-release-features)。

使用 Configuration Manager 控制台将服务部署到 Azure，添加云管理网关连接点角色，并配置站点系统角色以允许云管理网关通信。 云管理网关服务目前只支持管理点和软件更新点角色。

需要用客户端证书和安全套接字层 (SSL) 证书来进行计算机身份验证和加密不同服务层之间的通信。 通常，客户端计算机通过组策略实施接收客户端证书。 若要加密客户端和托管角色的站点系统服务器之间的通信，需要从 CA 创建自定义 SSL 证书。 还需要在 Azure 上设置管理证书以允许 Configuration Manager 部署云管理网关服务。

## <a name="requirements-for-cloud-management-gateway"></a>云管理网关的要求

-   运行云管理网关连接点的客户端计算机和站点系统服务器。

-   来自内部 CA 的自定义 SSL 证书 - 用来加密客户端计算机的通信和对云管理网关服务器的标识进行身份验证。

-   云服务的 Azure 订阅。

-   Azure 管理证书 - 用于通过 Azure 对 Configuration Manager 进行身份验证。

## <a name="specifications-for-cloud-management-gateway"></a>云管理网关的规范

- 云管理网关的每个实例支持 4,000 个客户端。
- 建议创建至少两个云管理网关的实例，以提高可用性。
- 云管理网关只支持管理点和软件更新点角色。
-   云管理网关目前不支持 Configuration Manager 中的以下功能：

    -   客户端部署
    -   自动站点分配
    -   用户策略
    -   应用程序目录（包括软件审批请求）
    -   完整的操作系统部署 (OSD)
    -   Configuration Manager 控制台
    -   远程工具
    -   报表网站
    -   LAN 唤醒
    -   Mac、Linux 和 UNIX 客户端
    -   Azure 资源管理器
    -   对等缓存
    -   本地移动设备管理

## <a name="cost-of-cloud-management-gateway"></a>云管理网关的费用

>[!IMPORTANT]
>下面提供的费用信息仅用作估算用途。 环境可能具有其他可影响使用云管理网关总费用的变量。

云管理网关使用以下 Microsoft Azure 功能，这些功能会向 Azure 订阅帐户收取费用：

-   虚拟机

    -   云管理网关当前需要 Standard\_A2 虚拟机。 在创建服务时，可以选择支持服务的 VM 数量（默认值为 1 个）。

    -   出于估算目的，可假设 Azure Standard\_A2 虚拟机可同时支持大约 2,000 个基于 Internet 的客户端。

    -   请参阅 [Azure 定价计算器](https://azure.microsoft.com/en-us/pricing/calculator/)以帮助确定潜在的费用。

      >[!NOTE]
      >虚拟机费用因区域而异。

-   出站数据传输

    -   流出服务之外的数据会产生费用... 请参阅 [Azure 带宽定价详细信息](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)以帮助确定潜在的费用。

    -   出于估算目的，可假设基于 Internet 的客户端每隔一小时执行策略刷新，每个客户端每月大约耗费 100 MB。

    >[!NOTE]
    > 通过云管理网关执行其他支持的操作（例如，部署软件更新或应用程序）将增加从 Azure 传输的出站数据量。

-   内容存储

    -   使用云管理网关管理的基于 Internet 的客户端将从 Windows 更新获取软件更新内容，且不收取任何费用。

    -   任何其他必需的内容（例如，应用程序）都必须分发到基于云的分发点。 云管理网关目前只支持从云分发点向客户端发送内容。

    - 有关更多详细信息，请参阅使用[基于云的分发](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution)的费用。

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>有关云管理网关 (CMG) 的常见问题解答

### <a name="why-use-the-cloud-management-gateway"></a>为什么要使用云管理网关？

使用此角色可以在 Configuration Manager 控制台中通过三步来简化基于 Internet 的客户端管理。

1. 使用[创建云管理网关](/sccm/core/clients/manage/setup-cloud-management-gateway)向导将 CMG 部署到 Azure。
2. 配置[云管理网关连接点](/sccm/core/servers/deploy/configure/install-site-system-roles)站点系统角色。
3. [配置云管理网关流量角色](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic)（如管理点和软件更新点）。

### <a name="how-does-the-cloud-management-gateway-work"></a>云管理网关的工作方式是什么？

- 云管理网关连接点可一致实现从 Internet 到云管理网关的高性能连接。
- Configuration Manager 将设置发布到 CMG 中，其中包括连接信息和安全设置。
- CMG 验证 Configuration Manager 客户端请求，然后将请求转发到云管理网关连接点。 这些请求根据 URL 映射转发给公司网络中的各个角色。

### <a name="how-is-the-cloud-management-gateway-deployed"></a>如何部署云管理网关？

服务连接点上的云服务管理器组件负责处理所有 CMG 部署任务。 此外，它还可以监视并报告 Azure AD 中的服务运行状况和日志信息。

#### <a name="certificate-requirements"></a>证书要求

必须有以下证书，才能保护 CMG：

- **管理证书** - 这可以是包括自签名证书在内的任何证书。 可以使用上载到 Azure AD 中的公共证书或导入 Configuration Manager 的[含私钥的 PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)，从而使用 Azure AD 进行身份验证。
- **Web 服务证书** - 建议使用公共 CA 证书来获取客户端的本机信任。 必须在公共 DNS 注册机构中创建 CName。 不支持使用通配符证书。
- **上载到 CMG 中的根/SubCA 证书** - CMG 需要对客户端 PKI 证书进行全链验证。 如果使用企业 CA 颁发客户端 PKI 证书，且 Internet 上没有其根或从属 CA，那么就必须将其上载到 CMG 中。

#### <a name="deployment-process"></a>部署过程

部署过程分为两个阶段：

- 部署云服务
    - 上载 [Azure 服务定义架构](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef) 文件
    - 上载 [Azure 服务配置架构](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg) 文件。
- 在 Azure AD 服务器上设置 CMG 组件，然后在 Internet Information Services (IIS) 中配置终结点、HTTP 处理程序和服务

如果更改 CMG 的配置，则会启动配置 CMG 部署。

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>云管理网关是如何帮助确保安全性的？

CMG 通过以下方式帮助确保安全性：

- 接受和管理来自 CMG 连接点的连接，包括使用内部证书和连接 ID 进行相互 SSL 身份验证。
- 接受和转发客户端请求
    - 对客户端 PKI 证书使用相互 SSL 身份验证，预先对连接进行身份验证。
    - 证书信任列表检查客户端 PKI 证书的根。 可以在站点属性的客户端通信设置中指定此设置。 此外，还可以执行相同的验证作为客户端的管理点。
    - 验证收到的 URL
    - 筛选收到的 URL，以检查任何正在连接的 CMG 连接点是否都能为 URL 请求提供服务。  
    - 检查每个发布终结点的内容长度。
    - 使用“轮询机制”在同一站点中均衡 CMG 连接点之间的负载。

- 保护 CMG 连接点
    - 一致生成与正在连接的 CMG 的所有虚拟实例的 HTTP/TCP 连接。 每分钟检查和维护一次连接。
    - 使用内部证书对 CMG 进行相互 SSL 身份验证。
    - 根据 URL 映射转发 HTTP 请求。
    - 报告连接状态，以显示管理服务运行状况。
    - 每 5 分钟报告一次每个终结点的终结点流量。

- 确保面向客户端的发布终结点 Configuration Manager 角色（如管理点和软件更新点）在 IIS 中托管终结点，从而为客户端请求提供服务。 发布到 CMG 的每个终结点都有对应的 URL 映射。
外部 URL 是客户端在与 CMG 进行通信时使用的 URL。
内部 URL 是用于将请求转发给内部服务器的 CMG 连接点。

#### <a name="example"></a>例如：
在管理点上启用 CMG 通信时，Configuration Manager 会在内部为每个管理点服务器（如 ccm_system、ccm_incoming 和 sms_mp）创建一组 URL 映射。
管理点 ccm_system 终结点的外部 URL 可能如下所示：**https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**。
URL 对每个管理点都是唯一的。 然后，Configuration Manager 客户端会将启用了 CMG 的 MP 名称（如 **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>**）放入其 Internet 管理点列表中。
所有已发布的外部 URL 都会自动上载到 CMG 中，以便 CMG 可以进行 URL 筛选。 所有 URL 映射都会复制到 CMG 连接点，以便连接点可以根据客户端请求外部 URL 将请求转发给内部服务器。

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>云管理网关使用哪些端口？

- 在本地网络上，不需要使用任何入站端口。 部署 CMG 后将会自动在 CMG 上创建各种端口。
- 除了端口 443，CMG 连接点还需要使用一些出站端口。

|||||
|-|-|-|-|
|数据流|服务器|服务器端口|客户端|
|CMG 部署|Azure|443|Configuration Manager 服务连接点|
|生成 CMG 通道|CMG|VM 实例：1 端口：443<br>VM 实例：N（N>=2 且 N<= 16） 端口：10124~N 10140~N|CMG 连接点|
|从客户端到 CMG|CMG|443|客户端|
|从 CMG 连接器到站点角色（目前为管理点和软件更新点）|站点角色|在站点角色上配置的协议/端口|CMG 连接点|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>如何提升云管理网关的性能？

- 如果可能，在同一网络区域中配置 CMG、CMG 连接点和 Configuration Manager 站点服务器，以减少延迟。
- 目前，Configuration Manager 客户端和 CMG 之间的连接无法感知区域。
- 为了提高可用性，建议每个站点至少有 2 个 CMG 虚拟实例和 2 个 CMG 连接点
- 可以添加更多的 VM 实例，将 CMG 扩展为支持更多客户端。 它们由 Azure AD 负载均衡器进行负载均衡。
- 创建更多的 CMG 连接点，在它们之间分配负载。 CMG 将通过“轮询机制”将流量分配给其正在连接的 CMG 连接点。
- 在 1702 版本中，每个 CMG VM 实例支持 6000 个客户端。 当 CMG 通道处于高负载状态时，请求仍会得到处理，但耗时可能会比平时长。

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>如何监视云管理网关？

若要排查部署问题，请使用 **CloudMgr.log** 和 **CMGSetup.log**。
若要排查服务运行状况问题，请使用 **CMGService.log** 和 **SMS_CLOUD_PROXYCONNECTOR.log**。
若要排查客户端流量问题，请使用 **CMGHttpHandler.log**、**CMGService.log** 和 **SMS_CLOUD_PROXYCONNECTOR.log**。

有关所有 CMG 相关日志文件的列表，请参阅 [Configuration Manager 中的日志文件](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>后续步骤

[设置云管理网关](setup-cloud-management-gateway.md)
