---
title: 对 Windows 功能的支持
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 支持的 Windows 和网络功能。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c1b4dbb6986b5e617ae7a8eb2a0264ce799e87ca
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>对 System Center Configuration Manager 中的 Windows 功能和网络的支持

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍 Configuration Manager 对常用 Windows 功能和网络功能的支持。  


##  <a name="bkmk_branchcache"></a> BranchCache  
在分发点上启用 Windows BranchCache 后，可将它用于 Configuration Manager，并将客户端配置为在分布式缓存模式下使用它。

你可以在应用程序的部署类型上、在包和任务序列的部署上配置 BranchCache 设置。  

当满足 BranchCache 的要求后，此功能允许远程位置处的客户端从具有当前内容缓存的本地客户端中获取内容。  

例如，当第一个启用 BranchCache 的客户端从配置为 BranchCache 服务器的分发点请求内容时，客户端将下载内容并对其进行缓存。 然后，此内容可用于请求此内容的同一子网上的客户端。

这些客户端也会缓存内容。 同一子网上的其他客户端无需从分发点下载内容。 该内容分布在多个客户端，以供将来传输。  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>通过 Configuration Manager 支持 BranchCache 的要求
-   **配置分发点**：将 **Windows BranchCache** 功能添加到配置为分发点的站点系统服务器。    
    -   配置为支持 BranchCache 的服务器上的分发点无需其他配置。   
    -   不能将 Windows BranchCache 添加到基于云的分发点。 基于云的分发点支持针对 Windows BranchCache 配置的客户端下载内容。  

-   **配置客户端**：    
    -   必须针对 BranchCache 分布式缓存模式配置可支持 BranchCache 的客户端。  
    -   必须启用用于 BITS 客户端设置的操作系统设置以支持 BranchCache。   <br /> <br />

    有关信息，请参阅 Windows 文档中的[为客户端配置 BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache)。


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Configuration Manager 支持使用 Windows BranchCache 的 OS 版本

|操作系统|支持详细信息|  
|----------------------|---------------------|  
|带 SP1 的 Windows 7|默认情况下支持|  
|Windows 8|默认情况下支持|  
|Windows 8.1|默认情况下支持|  
|Windows 10|默认情况下支持|  
|带 SP2 的 Windows Server 2008|**需要 BITS 4.0**：可使用软件更新或软件分发在 Configuration Manager 客户端上安装 BITS 4.0 版本。 有关详细信息，请参阅 [Windows Management Framework](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits)。<br /><br /> 在此 OS 中，不支持将 BranchCache 客户端功能用于从网络运行的软件分发或 SMB 文件传输。 此外，此操作系统不能将 BranchCache 功能用于基于云的分发点。|  
|Windows Server 2008 R2|默认情况下支持|  
|Windows Server 2012|默认情况下支持|  
|Windows Server 2012 R2|默认情况下支持|  
|Windows Server 2016|默认情况下支持|  

 有关详细信息，请参阅 Windows Server 文档中的 [BranchCache for Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache)。  



##  <a name="bkmk_Workgroups"></a> 工作组中的计算机  
Configuration Manager 提供对工作组中的客户端的支持。  

-   Configuration Manager 支持将客户端从工作组移动到域，或者从域移动到工作组。 有关详细信息，请参阅[如何将客户端部署到 Windows 计算机](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)主题中的[如何在工作组计算机上安装 Configuration Manager 客户端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)。  

> [!NOTE]  
>  尽管工作组中的客户端都受支持，但所有站点系统必须是受支持的 Active Directory 域的成员。  



##  <a name="bkmmk_datadedup"></a> 重复数据删除  
Configuration Manager 在以下操作系统上支持将重复数据删除用于分发点：  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  托管包源文件的卷不能标记为重复数据删除。 存在此限制是因为重复数据删除使用重新分析点。 Configuration Manager 不支持使用有文件存储在重新分析点上的内容源位置。  

有关详细信息，请参阅 Configuration Manager 团队博客上的 [Configuration Manager 分发点和 Windows Server 2012 重复数据删除](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/)和 Windows Server 文档中的[重复数据删除概述](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview)。  



##  <a name="bkmk_DA"></a> DirectAccess  
Configuration Manager 支持使用 DirectAccess 功能在客户端和站点服务器系统之间进行通信。  

-   当满足了 DirectAccess 的所有要求后，它允许 Internet 上的 Configuration Manager 客户端与其分配的站点通信，就好像在 Intranet 上一样。  

-   对于服务器启动的操作，例如远程控制和客户端推送安装，启动计算机必须运行 IPv6。 所有介入的网络设备都必须支持该协议。  

Configuration Manager 在 DirectAccess 上不支持以下功能：  

-   操作系统部署  

-   Configuration Manager 站点之间的通信  

-   同一站点中的 Configuration Manager 站点系统服务器间的通信  



##  <a name="bkmk_dualboot"></a> 双引导计算机  
 Configuration Manager 不能在单台计算机上管理多个操作系统。 如果某台计算机上有多个操作系统要管理，则调整站点的发现和客户端安装方法，确保仅在必须管理的操作系统上安装 Configuration Manager 客户端。  



##  <a name="bkmk_IPv6"></a> Internet 协议版本 6  
 除 Internet 协议版本 4 (IPv4) 之外，Configuration Manager 还支持 Internet 协议版本 6 (IPv6)，以下情况例外：  

|函数| 对 IPv6 支持的例外|  
|--------------|-------------------------------|  
|基于云的分发点|支持 Microsoft Azure 和基于云的分发点需要 IPv4。|  
|云管理网关|支持 Microsoft Azure 和云管理网关需要 IPv4。|  
|由 Microsoft Intune 和 Microsoft 服务连接器注册的移动设备|支持由 Microsoft Intune 和 Microsoft 服务连接器注册的移动设备需要 IPv4。|  
|网络发现|配置 DHCP 服务器以在“网络发现”中搜索时需要 IPv4。|  
|OS 部署|支持 OS 部署需要 IPv4。 |  
|唤醒代理通信|支持客户端唤醒代理数据包需要 IPv4。|  
|Windows CE|在 Windows CE 设备上支持 Configuration Manager 客户端需要 IPv4。|  



##  <a name="bkmk_NAT"></a> 网络地址转换  
 Configuration Manager 不支持网络地址转换 (NAT)，除非站点支持位于 Internet 上的客户端且客户端检测到它连接到 Internet。 有关基于 Internet 的客户端管理的详细信息，请参阅[基于 Internet 的客户端管理计划](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md)。  



##  <a name="bkmk_storage"></a> 专用存储技术  
 Configuration Manager 与在安装了 Configuration Manager 组件的操作系统版本的 Windows 硬件兼容列表上经过认证的任何硬件配合使用。

站点服务器角色需要 NTFS，以便 Configuration Manager 可以设置目录和文件权限。 Configuration Manager 假定它具有逻辑驱动器的完整所有权。 在不同计算机上运行的站点系统不能在任何存储技术上共享逻辑分区。 但是，每台计算机可以使用共享存储设备的同一物理分区上的单独逻辑分区。  

 ### <a name="support-considerations"></a>支持注意事项

-   **存储区域网络**：只要将受支持的基于 Windows 的服务器直接连接至 SAN 托管的卷，就支持存储区域网络 (SAN)。  

-   **单实例存储**：Configuration Manager 不支持在启用了单实例存储 (SIS) 的卷上配置分发点包和签名文件夹。  

     此外，在启用了 SIS 的卷上不支持 Configuration Manager 客户端的缓存。  

-   **可移动磁盘驱动器**：Configuration Manager 不支持在可移动磁盘驱动器上安装 Configuration Manager 站点系统或客户端。  
