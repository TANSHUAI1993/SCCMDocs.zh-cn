---
title: 客户端的站点系统角色
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中确定客户端的站点系统角色。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c13385a4c0f7b36cac1f67b1a8ceacbec6819631
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68533792"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>为 Configuration Manager 客户端确定站点系统角色

适用范围：  System Center Configuration Manager (Current Branch)

本文可帮助确定部署 Configuration Manager 客户端所需的站点系统角色。

有关在层次结构中何处安装这些角色的详细信息，请参阅[设计站点层次结构](/sccm/core/plan-design/hierarchy/design-a-hierarchy-of-sites)。  

有关如何安装和配置这些角色的详细信息，请参阅[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。  

## <a name="management-point"></a>管理点

默认情况下，所有 Windows 客户端计算机都使用分发点安装 Configuration Manager 客户端。 它们可以在分发点不可用时回退到管理点。 但是，如果使用 CCMSetup 命令行属性 `/source:<Path>`，则可以通过替代来源在计算机上安装 Windows 客户端。 例如，在 Internet 上安装客户端时，可能会执行此操作。 另一种情况是当你想要避免在客户端安装期间在计算机与管理点之间发送网络数据包时。 发生这种情况是因为防火墙会阻止所需的端口，或者因为你具有低带宽连接。 但是，所有客户端都必须与管理点进行通信，才能分配给站点以及由 Configuration Manager 来管理。  

有关客户端命令行属性的详细信息，请参阅[关于客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。  

在层次结构中安装多个管理点时，客户端会根据其林成员身份和网络位置自动连接到某个点。 无法在辅助站点中安装多个管理点。  

用 Configuration Manager 注册的 Mac 计算机客户端和移动设备客户端始终需要用于客户端安装的管理点。 此管理点必须在主站点中，必须配置为支持移动设备，并且必须接受来自 Internet 的客户端连接。 这些客户端无法使用辅助站点中的管理点或者无法连接到其他主站点中的管理点。  

## <a name="distribution-point"></a>分发点

在 Windows 计算机上安装 Configuration Manager 客户端不需要分发点。 默认情况下，Configuration Manager 使用分发点在 Windows 计算机上安装客户端源文件。 它可以回退到从管理点下载这些文件。 分发点并不用于安装 Configuration Manager 注册的移动设备客户端，但如果你安装移动设备旧客户端，则会使用分发点。 如果在 OS 部署过程中安装 Configuration Manager 客户端，则会在分发点中存储和检索 OS 映像。

虽然安装大多数 Configuration Manager 客户端可能不需要分发点，但在客户端上安装诸如应用程序和软件更新之类的软件却需要分发点。  

## <a name="fallback-status-point"></a>回退状态点

回退状态点可用于监视 Windows 计算机的客户端部署。 还可以标识因无法与管理点通信而不受管理的 Windows 计算机客户端。

以下客户端类型不使用回退状态点：

- Mac 计算机
- Configuration Manager 注册的移动设备
- 使用 Exchange Server 连接器管理的移动设备

监视客户端活跃状况和客户端运行状况不需要回退状态点。  

回退状态点始终通过 HTTP 与客户端通信，HTTP 使用未经过身份验证的连接并以明文形式发送数据。 此行为会使回退状态点易受到攻击，特别是在与基于 Internet 的客户端管理一起使用时。 为了帮助减小攻击面，始终将服务器专用于运行回退状态点。 不要在生产环境中的同一服务器上安装其他站点系统角色。  

如果以下所有条件都适用，请安装回退状态点：  

- 你想将 Windows 计算机中的客户端通信错误发送给站点，即使这些客户端计算机无法与管理点通信也不例外。  

- 你想要使用 Configuration Manager 客户端部署报表，这些报表显示回退状态点发送的数据。  

- 此站点系统角色具有专用服务器，并且采取了其他安全措施来帮助保护服务器不受攻击。  

- 使用回退状态点的好处大于与未经过身份验证的连接以及通过 HTTP 流量进行的明文传输关联的安全风险。  

如果使用未经过身份验证的连接以及明文传输运行网站的安全风险大于确定客户端通信问题的好处，则不安装回退状态点。  

## <a name="reporting-services-point"></a>Reporting Services 点

Configuration Manager 提供了许多报表，以帮助你在 Configuration Manager 控制台中监视客户端的安装、分配和管理。 一些客户端部署报表需要将客户端分配到回退状态点。  

部署客户端不需要报表。 可以在 Configuration Manager 控制台中查看某些部署信息，也可以使用客户端日志文件获取详细信息。 但是，客户端报表提供了有价值的信息来帮助监视客户端部署并对其进行故障排除。  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>注册点和注册代理点

Configuration Manager 需要注册点和注册代理点以注册移动设备以及注册 Mac 计算机的证书。 在以下情况下，不需要这些站点系统角色：

- 计划使用 Exchange Server 连接器管理移动设备
- 为 Windows CE 安装移动设备旧客户端
- 在 Mac 计算机上独立于 Configuration Manager 请求和安装客户端证书

## <a name="application-catalog"></a>应用程序目录

> [!Important]  
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 从版本 1906 开始，更新后的客户端自动使用管理点进行用户可用应用程序部署。 仍然无法安装新的应用程序目录角色。 在 2019 年 10 月 31 日之后的第一个当前分支版本中，应用程序目录角色不再受支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)
> - [已删除和已弃用的功能](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)  

## <a name="cloud-management-gateway-connector-point"></a>云管理网关连接点

如果你设置了[云管理网关](/sccm/core/clients/manage/setup-cloud-management-gateway)以便[在 Internet 上管理客户端](/sccm/core/clients/manage/manage-clients-internet)，则需要云管理网关连接点。
