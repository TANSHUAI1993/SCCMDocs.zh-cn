---
title: 传递优化网络内缓存
titleSuffix: Configuration Manager
description: 将 Configuration Manager 分发点用作传递优化的本地缓存服务器
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 55daf45df3216b205dd1242017eb1ddefb128530
ms.sourcegitcommit: 84a6f31797490eeda73bd4f3656ba27741df3030
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71343821"
---
# <a name="delivery-optimization-in-network-cache-in-configuration-manager"></a>Configuration Manager 中的传递优化网络内缓存

适用范围：  System Center Configuration Manager (Current Branch)

<!--3555764-->

从版本 1906 开始，可以在分发点上安装传递优化网络内缓存 (DOINC) 服务器。 通过将此内容缓存在本地，你的客户端可以从传递优化功能中受益，但你可帮助保护 WAN 链接。

此缓存服务器充当由传递优化下载的内容的按需透明缓存。 使用客户端设置以确保此服务器仅提供给本地 Configuration Manager 边界组的成员。

此缓存独立于 Configuration Manager 分发点内容。 如果选择和分发点角色一样的驱动，它将单独存储内容。

> [!Note]  
> 传递优化网络内缓存服务器是一项安装于 Windows Server 的应用程序，目前仍在开发。  


## <a name="how-it-works"></a>工作原理

当你配置客户端以使用传递优化网络内缓存服务器时，它们不再从 Internet 请求 Microsoft 云托管内容。 客户端从安装在分发点上的 DOINC 服务器请求此内容。 DOINC 服务器使用 IIS 功能的应用程序请求路由 (ARR) 缓存此内容。 然后，缓存服务器可快速响应对同一内容的任何未来请求。 如果 DOINC 服务器不可用，或者尚未缓存内容，客户端将从 Internet 下载内容。 客户端还使用传递优化，因此从其网络中的对等端下载部分内容。

![DOINC 的工作原理示意图](media/3555764-delivery-optimization-in-network-cache.png)

1. 客户端检查更新并获取内容分发网络 (CDN) 的地址。

2. Configuration Manager 在客户端上配置传递优化 (DO) 设置，其中包括缓存服务器名称。

3. 客户端 A 从 DO 缓存服务器请求内容。

4. 如果缓存不包含该内容，则 DO 缓存服务器从 CDN 获取该内容。

5. 如果缓存服务器无法响应，客户端将从 CDN 下载该内容。

6. 客户端使用 DO 从对等方获取内容的片段。


## <a name="prerequisites-and-limitations"></a>先决条件和限制

- 具有以下配置的本地分发点  ：

    - 运行 Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 或 Windows Server 2019

    - 在端口 80 上启用默认网站

    - 请勿预安装 IIS [应用程序请求路由](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) 功能。 DOINC 安装 ARR 并配置其设置。 Microsoft 不能保证 DOINC 的 ARR 配置不会与服务器上同时使用此功能的其他应用程序发生冲突。

    - 分发点需要具有 Internet 连接才能访问 Microsoft 云。 特定 URL 可以基于特定于云的内容而不同。 有关详细信息，请参阅 [Internet 访问要求](/sccm/core/plan-design/network/internet-endpoints)。

- 运行 Windows 10 版本 1709 或更高版本的客户端


## <a name="enable-doinc"></a>启用 DOINC

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点”节点   。

1. 选择本地分发点，然后在功能区中选择“属性”  。

1. 在分发点角色的属性中的“常规”选项卡中，配置以下设置  ：  

    1. 启用选项“使此分发点用作传递优化网络内缓存服务器”   

        查看并接受许可条款。

    2. **要使用的本地驱动器**：选择要用于缓存的磁盘。 “自动”是默认值，使用可用空间最多的磁盘。<sup>[备注 1](#bkmk_note1)</sup>   

        > [!Note]  
        > 可以在以后更改此驱动器。 除非将缓存内容复制到新驱动器，否则会丢失任何缓存内容。

    3. **磁盘空间**：选择要保留的磁盘空间 (GB)，或占磁盘总空间的百分比。 默认情况下，此值为 100 GB。

        > [!Note]  
        > 默认缓存大小对于大多数客户来说应该已足够。 可以在以后调整缓存大小。

    4. **禁用网络内缓存服务器时保留缓存**：如果删除缓存服务器并启用此选项，服务器会将缓存内容存储在磁盘上。  

1. 在客户端设置的“传递优化”组中，配置“使 Configuration Manage 管理的设备能够对下载的内容使用传递优化网络内缓存服务器 (Beta)”设置   。  

### <a name="bkmk_note1"></a> 注释 1：关于驱动器选择

如果选择“自动”，则 Configuration Manager 安装 DOINC 组件时，将优先采用 no_sms_on_drive.sms 文件   。 例如，分发点具有 `C:\no_sms_on_drive.sms` 文件。 即使 C: 驱动器具有的可用空间最多，Configuration Manager 也会将 DOINC 配置为使用另一个驱动器进行缓存。

如果选择已具有 no_sms_on_drive.sms 文件的特定驱动器，则 Configuration Manager 将忽略该文件  。 将 DOINC 配置为使用该驱动器是一个明确的意图。 例如，分发点具有 `F:\no_sms_on_drive.sms` 文件。 将分发点属性显式配置为使用 F: 驱动器时，Configuration Manager 将 DOINC 配置为将 F: 驱动器用于缓存  。

在安装 DOINC 后更改驱动器：

- 手动将分发点属性配置为使用特定的驱动器号。

- 如果设置为自动，请首先创建 no_sms_on_drive.sms 文件  。 然后对分发点属性进行一些更改，以触发配置更改。

## <a name="verify"></a>验证

客户端下载云托管的内容时，它们使用安装在分发点上的缓存服务器中的传递优化。 云托管的内容包括以下类型：

- Microsoft Store 应用
- 按需 Windows 功能，例如语言
- 如果启用[适用于企业的 Windows 更新策略](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)：Windows 10 功能和质量更新
- 对于[共同管理工作负载](/sccm/comanage/workloads)：
    - 适用于企业的 Windows 更新：Windows 10 功能和质量更新
    - Office 即点即用应用：Office 应用和更新
    - 客户端应用：Microsoft Store 应用和更新
    - Endpoint Protection：Windows Defender 定义更新

在 Windows 10 版本 1809 或更高版本中，使用 Get-DeliveryOptimizationStatus Windows PowerShell cmdlet 验证此操作  。 在 cmdlet 输出中，查看 BytesFromCacheServer 值  。 有关详细信息，请参阅[监视传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization)。

如果缓存服务器返回任何 HTTP 故障，则传递优化客户端退回到原始云源。

有关详细信息，请参阅 [Configuration Manager 中的传递优化网络内缓存故障排除](/sccm/core/servers/deploy/configure/troubleshoot-delivery-optimization-in-network-cache)。

## <a name="see-also"></a>另请参阅

[通过传递优化来优化 Windows 10 更新](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)

[Configuration Manager 中的传递优化网络内缓存故障排除](/sccm/core/servers/deploy/configure/troubleshoot-delivery-optimization-in-network-cache)
