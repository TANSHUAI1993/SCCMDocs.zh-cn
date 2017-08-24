---
title: "准备 Windows Server | Microsoft Docs"
description: "确保计算机满足用作 System Center Configuration Manager 的站点服务器或站点系统服务器的先决条件。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9b97dedb5d2be0bd2e47260033e6e4361467dc4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>准备 Windows Server 以支持 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

在将一台 Windows 计算机作为用于 System Center Configuration Manager 的站点系统服务器使用之前，该计算机必须满足作为站点服务器或站点系统服务器使用的先决条件。  

-   这些先决条件通常包括一个或多个 Windows 功能或角色，通过使用计算机服务器管理器启用它们。  

-   因为在不同的操作系统中启用 Windows 功能和角色的方法是不同的，请参考适用于自己操作系统的文档以获取关于如何设置所用操作系统的详细信息。  

本文中的信息概述了支持 System Center Configuration Manager 站点系统所需的 Windows 配置类型。 有关特定站点系统角色配置的详细信息，请参阅[站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。

##  <a name="BKMK_WinFeatures"></a>Windows 功能和角色  
 在计算机上设置 Windows 功能和角色时，可能需要重新启动计算机以完成该配置。 因此，一个不错的做法是，安装 Configuration Manager 站点或站点系统服务器之前，先确定要承载特定站点系统角色的计算机。
### <a name="features"></a>功能  
 以下 Windows 功能是某些站点系统服务器必需的，且应在该计算机上安装站点系统角色之前进行设置。  

-   **NET Framework**：包括  

    -   ASP.NET  
    -   HTTP 激活  
    -   非 HTTP 激活  
    -   Windows Communication Foundation (WCF) 服务  

    不同的站点系统角色需要不同版本的 .NET Framework。  

    由于.NET Framework 4.0 和更高版本不是向后兼容，无法替换 3.5 及更早版本，在不同的版本被列为必需时，计划在同一台计算机上启用每个版本。  

-   后台智能传输服务 **BITS**：管理点需要 BITS（和自动选择的选项）来支持与托管设备之间的通信。  

-   **BranchCache**：可以通过 BranchCache 来设置分发点以支持使用 BranchCache 的客户端。  

-   **重复数据删除**：可以使用重复数据删除设置分发点并从中获益。  

-   远程差分压缩 **RDC**：每个托管站点服务器或分发点的计算机都需要 RDC。   
    RDC 用于生成包签名和执行签名比较。  

### <a name="roles"></a>角色  
 需要以下 Windows 角色来支持特定功能（例如软件更新和操作系统部署），而最常见的站点系统角色需要 IIS。  

 -   **网络设备注册服务**（在 Active Directory 证书服务之下）：此 Windows 角色是在 Configuration Manager 中使用证书配置文件的先决条件。  

 -   **Web 服务器 IIS**：包括：  
    -   常见 HTTP 功能 >  
        -   HTTP 重定向  
    -   应用程序开发 >  
        -   .NET 扩展性  
        -   ASP.NET  
        -   ISAPI 扩展  
        -   ISAPI 筛选器  
    -   管理工具 >  
        -   IIS 6 管理兼容性  
        -   IIS 6 元数据库兼容性  
        -   IIS 6 Windows Management Instrumentation (WMI) 兼容性  
    -   安全 >  
        -   请求筛选  
        -   Windows 身份验证  

 下列站点系统角色使用一个或多个列出的 IIS 配置：  
    -   应用程序目录 Web 服务点  
    -   应用程序目录网站点  
    -   分发点  
    -   注册点  
    -   注册代理点  
    -   回退状态点  
    -   管理点  
    -   软件更新点  
    -   状态迁移点     

    需要的最低 IIS 版本为随站点服务器的操作系统一起提供的版本。  

    除了这些 IIS 配置之外，可能还需要设置[分发点的 IIS 请求筛选](#BKMK_IISFiltering)。  

-   **Windows 部署服务**：此角色用于操作系统部署。  
-   **Windows Server 更新服务**：部署软件更新时将需要此角色。  

##  <a name="BKMK_IISFiltering"></a>分发点的 IIS 请求筛选  
 默认情况下，IIS 使用请求筛选来阻止 HTTP 或 HTTPS 通信访问多个文件扩展名和文件夹位置。 在分发点上，这会阻止客户端下载含有被阻止的扩展名或文件夹位置的包。  

 如果包源文件含有在 IIS 中被请求筛选配置阻止的扩展名，则必须将请求筛选设置为不阻止这些扩展名。 这可通过在你的分发点计算机上的 IIS 管理器中 [编辑请求筛选功能](https://technet.microsoft.com/library/hh831621.aspx) 来完成。  

 此外，Configuration Manager 将下列文件扩展名用于包和应用程序。 请确保请求筛选配置不会阻止以下文件扩展名：  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

例如，软件部署的源文件可能包含名为 **bin** 的文件夹，或者包含具有 **.mdb** 文件扩展名的文件。  

-   默认情况下，IIS 请求筛选会阻止对这些元素的访问（**bin** 作为隐藏段被阻止，**.mdb** 作为文件扩展名被阻止）。  

-   在分发点上使用默认的 IIS 配置时，使用 BITS 的客户端不能从分发点下载此软件部署，并指示它们正在等待内容。  

-   若要允许客户端下载此内容，请在每个适用的分发点上编辑 IIS 管理器中的“请求筛选”，以允许访问所部署的包和应用程序中的文件扩展名和文件夹。  

> [!IMPORTANT]  
>  对请求筛选器进行编辑会增大计算机的受攻击面。  
>   
>  -   在服务器级别所做的编辑适用于服务器上的所有网站。  
> -   对单独的网站进行的编辑仅适用于该网站。  
>   
>  最佳安全方案是在专用 Web 服务器上运行 Configuration Manager。 如果必须在 Web 服务器上运行其他应用程序，请使用 Configuration Manager 的自定义网站。 有关详细信息，请参阅 [System Center Configuration Manager 中的站点系统服务器网站](../../../core/plan-design/network/websites-for-site-system-servers.md)。  

## <a name="http-verbs"></a>HTTP 谓词
**管理点：**若要确保客户端与管理点通信成功，请确保管理点服务器允许使用以下 HTTP 谓词：  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**分发点：**分发点需要以下 HTTP 谓词：
 - GET
 - HEAD
 - PROPFIND

有关如何配置请求筛选的信息，请参阅 TechNet 上的[IIS 中的配置请求筛选](https://technet.microsoft.com/library/hh831621.aspx#Verbs)或适用于托管管理点的 Windows Server 版本的类似文档。
