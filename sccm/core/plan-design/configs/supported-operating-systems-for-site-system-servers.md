---
title: 支持的站点系统服务器
titleSuffix: Configuration Manager
description: 了解可用来托管 Configuration Manager 站点或站点系统角色的 Windows 版本。
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd8e815ab57730ad2186a7e75cd51f21012383a
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236168"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Configuration Manager 站点系统服务器支持的操作系统

*适用范围：System Center Configuration Manager (Current Branch)*


本文详细介绍了可用于托管 Configuration Manager 站点或站点系统角色的 Windows 版本。


将本文中的信息和以下文章中的信息一起使用：
-   [用于 Configuration Manager 的推荐硬件](/sccm/core/plan-design/configs/recommended-hardware)
-   [用于 Configuration Manager 的站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [用于 Configuration Manager 的大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="bkmk_2016"></a> Windows Server 2016：标准版和数据中心版

使用 Configuration Manager 版本 1606 的更新汇总 1 ([KB3186654](https://support.microsoft.com/help/3186654))，此 OS 版本支持以下角色：

#### <a name="site-servers"></a>站点服务器

-   管理中心站点  
-   主站点  
-   辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

-   应用程序目录 Web 服务点  
-   应用程序目录网站点  
-   资产智能同步点  
-   证书注册点  
-   云管理网关连接点  
-   数据仓库服务点  
-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  
-   Endpoint Protection 点  
-   注册点  
-   注册代理点  
-   回退状态点  
-   管理点
-   Reporting Services 点  
-   服务连接点  
-   站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   软件更新点  
-   状态迁移点



## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>站点系统服务器

-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 (x64)：标准版和数据中心版  

#### <a name="site-servers"></a>站点服务器

-   管理中心站点  
-   主站点  
-   辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

-   应用程序目录 Web 服务点  
-   应用程序目录网站点  
-   资产智能同步点  
-   证书注册点  
-   云管理网关连接点  
-   数据仓库服务点  
-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  
-   Endpoint Protection 点  
-   注册点  
-   注册代理点  
-   回退状态点  
-   管理点
-   Reporting Services 点  
-   服务连接点  
-   站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   软件更新点  
-   状态迁移点  



## <a name="bkmk_2012"></a> Windows Server 2012 (x64)：标准版和数据中心版  

#### <a name="site-servers"></a>站点服务器

-   管理中心站点  
-   主站点  
-   辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

-   应用程序目录 Web 服务点  
-   应用程序目录网站点  
-   资产智能同步点  
-   证书注册点  
-   云管理网关连接点  
-   数据仓库服务点  
-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  
-   Endpoint Protection 点  
-   注册点  
-   注册代理点  
-   回退状态点  
-   管理点
-   Reporting Services 点  
-   服务连接点  
-   站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
-   SMS_Provider  
-   软件更新点  
-   状态迁移点  



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 SP1 (x64)：标准版、企业版和数据中心版  

根据 [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)中的详细信息，Windows Server 2008 R2 现处于外延支持，不再处于主流支持。 有关这些操作系统以后对 Configuration Manager 的站点系统服务器的支持情况的详细信息，请参阅[已弃用的服务器操作系统](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)。  

站点服务器或大多数站点系统角色不支持此 OS。 分发点站点系统角色（包括拉取分发点）以及 PXE 和多播仍然支持它。

#### <a name="site-system-servers"></a>站点系统服务器
-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  

    - 此 OS 上的分发点支持 PXE 和多播。  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 SP2（x86、x64）：标准版、企业版和数据中心版  

根据 [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)中的详细信息，Windows Server 2008 现处于外延支持，不再处于主流支持。 有关这些操作系统以后对 Configuration Manager 的站点系统服务器的支持情况的详细信息，请参阅[已弃用的服务器操作系统](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems)。  

除分发点和拉取分发点外，站点服务器或站点系统角色均不支持此 OS。 继续使用 OS 作为分发点，直到此支持被宣布弃用或者此 OS 的扩展支持期到期为止。 有关详细信息，请参阅 [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)（在 Windows Server 2008 上安装 System Center Configuration Manager CB 和 LTSB 失败）。

#### <a name="site-system-servers"></a>站点系统服务器
-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  

    -   此 OS 上的分发点支持 PXE 和多播。  

    -   此 OS 上的分发点不支持 EFI 模式下客户端计算机的网络启动。 支持具有 BIOS 或具有旧模式下的 EFI 启动的客户端计算机。  



## <a name="bkmk_win10"></a> Windows 10（x86、x64）：专业版和企业版  

#### <a name="site-system-servers"></a>站点系统服务器

-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  

    -   使用默认 Windows 部署服务的 PXE 不支持此 OS 上的分发点。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  

    -   此 OS 版本上的分发点不支持多播。  



## <a name="bkmk_win81"></a> Windows 8.1（x86、x64）：专业版和企业版  

#### <a name="site-system-servers"></a>站点系统服务器

-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  

    -   使用默认 Windows 部署服务的 PXE 不支持此 OS 上的分发点。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  

    -   此 OS 版本上的分发点不支持多播。  



## <a name="bkmk_win7sp1"></a> Windows 7 SP1（x86、x64）：专业版、企业版和旗舰版  

#### <a name="site-system-servers"></a>站点系统服务器

-   分发点 <sup>[说明 1](#bkmk_note1)</sup>  

    -   使用默认 Windows 部署服务的 PXE 不支持此 OS 上的分发点。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  

    -   此 OS 版本上的分发点不支持多播。  



## <a name="bkmk_core1803"></a> Windows Server（版本 1803）的服务器核心安装
<!--503702-->从 Configuration Manager 1802 开始，支持将 [Windows Server（版本 1803）](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803)用作具有以下限制的分发点：  

  -   仅支持 x64 位版本。  

  -   此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  



## <a name="bkmk_core1709"></a> Windows Server（版本 1709）的服务器核心安装

从 Configuration Manager 1710 开始，支持将 [Windows Server（版本 1709）](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709)用作具有以下限制的分发点：  

  -   仅支持 x64 位版本。  

  -   此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  



## <a name="bkmk_core2016"></a> Windows Server 2016 的服务器核心安装

使用 Configuration Manager 版本 1606 的更新汇总 1 ([KB3186654](https://support.microsoft.com/help/3186654))，此 OS 版本支持用作具有以下限制的分发点：  

  -   仅支持 x64 位版本。  

  -   此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  



## <a name="bkmk_core2012r2"></a> Windows Server 2012 R2 的服务器核心安装  

支持将 Windows Server 2012 R2 的 Server Core 安装用作具有以下限制的分发点：  

-   仅支持 x64 位版本。

-   此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。  



## <a name="bkmk_core2012"></a> Windows Server 2012 的服务器核心安装  

支持将 Windows Server 2012 的 Server Core 安装用作具有以下限制的分发点：  

-   仅支持 64 位版本。  

-   此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点。 有关详细信息，请参阅[安装和配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。



## <a name="general-notes"></a>一般说明

#### <a name="bkmk_note1"></a> 说明 1：分发点
分发点支持多种不同的配置，每种配置都有不同的要求。 在某些情况下，这些配置不仅支持在服务器上安装，而且支持在客户端操作系统上安装。 有关详细信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  

#### <a name="bkmk_note2"></a> 说明 2：站点数据库服务器
只读域控制器 (RODC) 上不支持站点数据库服务器。 有关详细信息，请参阅 Microsoft 支持文章：[在域控制器上安装 SQL Server 时可能会遇到问题](https://support.microsoft.com/help/2032911)。 

此外，任何域控制器上都不支持辅助站点服务器。  
