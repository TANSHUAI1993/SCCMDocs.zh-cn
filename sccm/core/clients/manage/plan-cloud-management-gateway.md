---
title: "规划云管理网关 | Microsoft Docs"
description: 
ms.date: 11/22/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1f8fbd8a16548ab2c34f5d3dac2b439f3908cea9
ms.openlocfilehash: e6befef692518a5622250af1c71d517b435f9058

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中规划云管理网关

*适用范围：System Center Configuration Manager (Current Branch)*

从版本 1610 开始，云管理网关提供一种简单的方法来管理 Internet 上的 Configuration Manager 客户端。 云管理网关服务部署到 Microsoft Azure 且需要 Azure 订阅，它使用名为云管理网关连接点的新角色连接到本地 Configuration Manager 基础结构。 服务完全部署并配置好后，客户端可以访问本地 Configuration Manager 站点系统角色，而不管它们是连接到内部专用网络还是 Internet 上。

使用 Configuration Manager 控制台将服务部署到 Azure，添加云管理网关连接点角色，并配置站点系统角色以允许云管理网关通信。 云管理网关服务目前只支持管理点和软件更新点角色。

需要用客户端证书和安全套接字层 (SSL) 证书来进行计算机身份验证和加密不同服务层之间的通信。 通常，客户端计算机通过组策略实施接收客户端证书。 若要加密客户端和托管角色的站点系统服务器之间的通信，需要从 CA 创建自定义 SSL 证书。 除了这两种证书类型，还需要在 Azure 上设置管理证书以允许 Configuration Manager 部署云管理网关服务。

## <a name="requirements-for-cloud-management-gateway"></a>云管理网关的要求

-   运行云管理网关连接点的客户端计算机和站点系统服务器。

-   来自内部 CA 的自定义 SSL 证书 - 用来加密客户端计算机的通信和对云管理网关服务器的标识进行身份验证。

-   云服务的 Azure 订阅。

-   Azure 管理证书 - 用于通过 Azure 对 Configuration Manager 进行身份验证。

## <a name="limitations-of-cloud-management-gateway"></a>云管理网关的限制

-   云管理网关只支持管理点和软件更新点角色。

-   云管理网关目前不支持 Configuration Manager 中的以下功能：

    -   使用客户端推送的客户端部署和升级

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

## <a name="next-steps"></a>后续步骤

[设置云管理网关](setup-cloud-management-gateway.md)



<!--HONumber=Dec16_HO3-->


