---
title: "站点先决条件 | Microsoft Docs"
description: "了解如何将 Windows 计算机配置为 System Center Configuration Manager 站点系统服务器。"
ms.custom: na
ms.date: 1/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0b1d2d619d6cdaf36cc22ef461ea1505b5cacc41
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站点和站点系统先决条件

*适用范围：System Center Configuration Manager (Current Branch)*


 基于 Windows 的计算机要求特定配置，以支持用作 System Center Configuration Manager 站点系统服务器。  


 对于某些产品，例如软件更新点的 Windows Server 更新服务 (WSUS)，需要参考产品文档来确定此产品适用的其他先决条件和限制。 此处仅包含直接应用于 Configuration Manager 的配置。   

> [!NOTE]  
>  2016 年 1 月，对 .NET Framework 4.0、4.5 和 4.5.1 的支持过期。 有关详细信息，请参阅 support.microsoft.com 处的 [Microsoft .NET Framework 支持生命周期策略常见问题解答](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)。  

## <a name="bkmk_generalprerewq"></a>常规站点服务器要求和限制
**以下内容适用于所有站点系统服务器：**

-   每个站点系统服务器必须使用 64 位操作系统。 唯一的例外是分发点站点系统角色，它可以安装在某些 32 位操作系统上。  

-   在任意操作系统的 Server Core 安装上，站点系统不受支持。 对此情况的一个例外是分发点站点系统角色支持 Server Core 安装，无需 PXE 或多播支持。  

-   安装站点系统服务器后，不支持进行更改：  

    -   站点系统计算机所在域的域名（也称为**域重命名**）。  

    -   计算机的域成员身份。  

    -   计算机的名称。  

  如果必须更改其中的任何设置，必须首先从计算机中删除站点系统角色，然后在更改完成后再重新安装角色。 如果这会影响站点服务器计算机，则必须卸载站点，然后在更改完成后再重新安装站点。  

-   在 Windows Server 群集实例上，站点系统角色不受支持。 此情况的唯一例外是站点数据库服务器。  

-   不支持更改任意 Configuration Manager 服务的启动类型或“登录身份”设置。 这样做可能会阻止关键服务正常运行。  

##  <a name="bkmk_2012Prereq"></a> Windows Server 2012 和更高版本操作系统的先决条件  
###  <a name="bkmk_2012sspreq"></a>站点服务器：管理中心站点和主站点  
  **Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

-   远程差分压缩  

**Windows ADK：**  

-   安装或升级管理中心站点或主站点之前，必须安装要安装或升级到的 Configuration Manager 版本所需的 Windows 评估和部署工具包 (ADK) 版本。  

    -   1511 版本的 Configuration Manager 需要 Windows ADK 的 Windows 10 RTM (10.0.10240) 版本。  

-   有关此要求的详细信息，请参阅[操作系统部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

**Visual C++ Redistributable：**  

-   Configuration Manager 在安装站点服务器的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   管理中心站点和主站点需要适用的可再发行文件的 x86 和 x64 版本。  

###  <a name="bkmk_2012secpreq"></a>站点服务器：辅助站点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

-   远程差分压缩  

**Visual C++ Redistributable：**  

-   Configuration Manager 在安装站点服务器的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   辅助站点仅需要 x64 版本。  

**默认站点系统角色：**  

-   默认情况下，辅助站点将安装**管理点**和**分发点**。  

-   请确保辅助站点服务器满足这些站点系统角色的先决条件。  

###  <a name="bkmk_2012dbpreq"></a>数据库服务器  
**远程注册表服务：**  

-   在安装 Configuration Manager 站点的过程中，必须在托管站点数据库的计算机上启用远程注册表服务。  

**SQL Server：**  

-   在安装管理中心站点或主站点之前，必须要安装受支持的 SQL Server 版本以托管站点数据库。  

-   在安装辅助站点之前，可以安装受支持的 SQL Server 版本。  

-   如果选择让 Configuration Manager 将 SQL Server Express 作为辅助站点安装的一部分安装，请确保计算机满足运行 SQL Server Express 的要求。  

###  <a name="bkmk_2012smsprovpreq"></a> SMS 提供程序服务器  
**Windows ADK：**  

-   安装 SMS 提供程序实例的计算机必须具备要安装或升级到的 Configuration Manager 版本所需的 Windows ADK 版本。  

    -   1511 版本的 Configuration Manager 需要 Windows ADK 的 Windows 10 RTM (10.0.10240) 版本。  

-   有关此要求的详细信息，请参阅[操作系统部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

###  <a name="bkmk_2012acwspreq"></a>应用程序目录网站点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2：  

    -   ASP.NET 4.5  

**IIS 配置：**  

-   常见 HTTP 功能：  

    -   默认文档  

    -   静态内容  

-   应用程序开发：  

    -   ASP.NET 3.5（和自动选择的选项）  

    -   ASP.NET 4.5（和自动选择的选项）  

    -   .NET Extensibility 3.5  

    -   .NET Extensibility 4.5  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

###  <a name="bkmk_2012ACwsitepreq"></a>应用程序目录 Web 服务点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2：  

    -   ASP.NET 4.5：  

        -   HTTP 激活（和自动选择的选项）  

**IIS 配置：**  

-   常见 HTTP 功能：  

    -   默认文档  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

-   应用程序开发：  

    -   ASP.NET 3.5（和自动选择的选项）  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5（和自动选择的选项）  

    -   .NET Extensibility 4.5  

**计算机内存：**  

-   托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

-   当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

###  <a name="bkmk_2012AIpreq"></a>资产智能同步点  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2012crppreq"></a>证书注册点  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2：  

    -   HTTP 激活  

**IIS 配置：**  

-   应用程序开发：  

    -   ASP.NET 3.5（和自动选择的选项）  

    -   ASP.NET 4.5（和自动选择的选项）  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

    -   IIS 6 WMI 兼容性  

###  <a name="bkmk_2012dppreq"></a>分发点  
**Windows Server 角色和功能：**  

-   远程差分压缩  

**IIS 配置：**  

-   应用程序开发：  

    -   ISAPI 扩展  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

    -   IIS 6 WMI 兼容性  

**PowerShell：**  

-   在安装分发点之前，需要在 Windows Server 2012 或更高版本上安装 PowerShell 3.0 或 4.0。  

**Visual C++ Redistributable：**  

-   Configuration Manager 在托管分发点的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   安装的版本取决于计算机平台（x86 或 x64）。  

**Microsoft Azure：**  

-   可以使用 Microsoft Azure 中的云服务来托管分发点。  

**支持 PXE 或多播：**  

-   安装和配置 Windows 部署服务 (WDS) Windows Server 角色。  

    > [!NOTE]  
    >  当配置分发点以在运行 Windows Server 2012 或更高版本的服务器上支持 PXE 或多播时，将自动安装和配置 WDS。  

> [!NOTE]  
> 分发点站点系统角色不需要后台智能传输服务 (BITS)。 在分发点计算机上配置 BITS 时，不使用分发点计算机上的 BITS 来辅助通过使用 BITS 的客户端下载内容。  

###  <a name="bkmk_2012EPPpreq"></a> Endpoint Protection 点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1（或更高版本）  

###  <a name="bkmk_2012Enrollpreq"></a>注册点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5（或更高版本）  

-   .NET Framework 4.5.2：  

     此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 当挂起对 .NET Framework 的重启时，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

    -   HTTP 激活（和自动选择的选项）  

    -   ASP.NET 4.5  


**IIS 配置：**  

-   常见 HTTP 功能：  

    -   默认文档  

-   应用程序开发：  

    -   ASP.NET 3.5（和自动选择的选项）  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5（和自动选择的选项）  

    -   .NET Extensibility 4.5  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

**计算机内存：**  

-   托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

-   当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

###  <a name="bkmk_2012EnrollProxpreq"></a>注册代理点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5（或更高版本）  

-   .NET Framework 4.5.2  

     此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 当挂起对 .NET Framework 的重启时，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

**IIS 配置：**  

-   常见 HTTP 功能：  

    -   默认文档  

    -   静态内容  

-   应用程序开发：  

    -   ASP.NET 3.5（和自动选择的选项）  

    -   ASP.NET 4.5（和自动选择的选项）  

    -   .NET Extensibility 3.5  

    -   .NET Extensibility 4.5  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

**计算机内存：**  

-   托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

-   当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

###  <a name="bkmk_2012FSPpreq"></a>回退状态点  
需要带有以下添加内容的默认 IIS 配置：  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

###  <a name="bkmk_2012MPpreq"></a>管理点  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

-   BITS 服务器扩展（和自动选择的选项），或后台智能传输服务 (BITS)（和自动选择的选项）  

**IIS 配置：**  

-   应用程序开发：  

    -   ISAPI 扩展  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

    -   IIS 6 WMI 兼容性  

###  <a name="bkmk_2012RSpoint"></a> Reporting Services 点  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services：**  

-   必须安装并配置至少一个 SQL Server 实例以在安装 Reporting Services 点之前支持 SQL Server Reporting Services。  

-   用于 SQL Server Reporting Services 的实例可以是用于站点数据库的同一实例。  

-   此外，只要其他 System Center 产品不具有对共享 SQL Server 实例的限制，则你使用的实例可与其他 System Center 产品共享。  

###  <a name="bkmk_SCPpreq"></a>服务连接点  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

     此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 当挂起对 .NET Framework 的重启时，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

**Visual C++ Redistributable：**  

-   Configuration Manager 在托管分发点的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   站点系统角色需要 x64 版本。  

###  <a name="bkmk_2012SUPpreq"></a>软件更新点  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

需要默认 IIS 配置。

**Windows Server 更新服务：**  

-   安装软件更新点之前，必须在计算机上安装 Windows 服务器角色 Windows Server 更新服务。  

-   有关详细信息，请参阅 [System Center Configuration Manager 的软件更新计划](../../../sum/plan-design/plan-for-software-updates.md)。  

### <a name="state-migration-point"></a>状态迁移点  
需要默认 IIS 配置。  

##  <a name="bkmk_2008"></a> Windows Server 2008 R2 和 Windows Server 2008 的先决条件  
如 [Microsoft 支持生命周期](https://support.microsoft.com/lifecycle)中的详细信息所述，Windows Server 2008 和 Windows Server 2008 R2 现处于外延支持，不再处于主流支持。 若要详细了解将来对这些操作系统作为具有 Configuration Manager 的站点系统服务器的支持，请参阅 [System Center Configuration Manager 的已删除和已弃用的功能](../../../core/plan-design/changes/removed-and-deprecated-features.md)。  

**下列内容适用于所有 .NET Framework 要求：**  

-   在安装站点系统角色之前，安装完整版的 .NET Framework。 有关示例，请参阅 [Microsoft .NET Framework 4 （独立安装程序）](http://go.microsoft.com/fwlink/p/?LinkId=193048)。 .NET Framework 4 Client Profile 不足以满足这一要求。  

**下列内容适用于所有 Windows Communication Foundation (WCF) 激活要求：**  

-   可以在站点系统服务器上将 WCF 激活配置为 .NET Framework Windows 功能的一部分。 例如，在 Windows Server 2008 R2 上运行“添加功能向导”以在该服务器上安装其他功能。 在“选择功能”页上，依次展开“NET Framework 3.5.1 功能”、“WCF 激活”，然后选中“HTTP 激活”和“非 HTTP 激活”复选框来启用这些选项。  

###  <a name="bkmk_2008sspreq"></a>站点服务器：管理中心站点和主站点  
**.NET Framework：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

**Windows 功能：**  

-   远程差分压缩  

**Windows ADK：**  

-   安装或升级管理中心站点或主站点之前，必须安装正在安装或升级到的 Configuration Manager 版本所需的 Windows ADK 版本。  

    -   1511 版本的 Configuration Manager 需要 Windows ADK 的 Windows 10 RTM (10.0.10240) 版本。  

-   有关此要求的详细信息，请参阅[操作系统部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

**Visual C++ Redistributable：**  

-   Configuration Manager 在安装站点服务器的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   管理中心站点和主站点需要适用的可再发行文件的 x86 和 x64 版本。  

###  <a name="bkmk_2008secpreq"></a>站点服务器：辅助站点  
**.NET Framework：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

**Visual C++ Redistributable：**  

-   Configuration Manager 在安装站点服务器的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   辅助站点仅需要 x64 版本。  

**默认站点系统角色：**  

-   默认情况下，辅助站点将安装**管理点**和**分发点**。  

-   请确保辅助站点服务器满足这些站点系统角色的先决条件。  

###  <a name="bkmk_2008dbpreq"></a>数据库服务器  
**远程注册表服务：**  

-   在安装 Configuration Manager 站点的过程中，必须在托管站点数据库的计算机上启用远程注册表服务。  

**SQL Server：**  

-   在安装管理中心站点或主站点之前，必须要安装受支持的 SQL Server 版本以托管站点数据库。  

-   在安装辅助站点之前，可以安装受支持的 SQL Server 版本。  

-   如果选择让 Configuration Manager 将 SQL Server Express 作为辅助站点安装的一部分安装，请确保计算机满足运行 SQL Server Express 的要求。  

###  <a name="bkmk_2008smsprovpreq"></a> SMS 提供程序服务器  
**Windows ADK：**  

-   安装 SMS 提供程序实例的计算机必须具备要安装或升级到的 Configuration Manager 版本所需的 Windows ADK 版本。  

    -   1511 版本的 Configuration Manager 需要 Windows ADK 的 Windows 10 RTM (10.0.10240) 版本。  

-   有关此要求的详细信息，请参阅[操作系统部署的基础架构要求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

###  <a name="bkmk_2008acwspreq"></a>应用程序目录网站点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

**IIS 配置：**

需要带有以下添加内容的默认 IIS 配置：  

-   常见 HTTP 功能：  

    -   静态内容  

    -   默认文档  

-   应用程序开发：  

    -   ASP.NET（和自动选择的选项）  

         在某些情况下（如安装 .NET Framework 4.5.2 版本之后，安装或重新配置 IIS 时），必须显式启用 ASP.NET 4.5 版本。 例如，在运行 .NET Framework 版本 4.0.30319 的 64 位计算机上，运行以下命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

###  <a name="bkmk_2008ACwsitepreq"></a>应用程序目录 Web 服务点  
**.NET Framework：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

**Windows Communication Foundation (WCF) 激活：**  

-   HTTP 激活  

-   非 HTTP 激活  

**IIS 配置：**

需要带有以下添加内容的默认 IIS 配置：  

-   应用程序开发：  

    -   ASP.NET（和自动选择的选项）  

         在某些情况下（如安装 .NET Framework 4.5.2 版本之后，安装或重新配置 IIS 时），必须显式启用 ASP.NET 4.5 版本。 例如，在运行 .NET Framework 版本 4.0.30319 的 64 位计算机上，运行以下命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

**计算机内存：**  

-   托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

-   当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

###  <a name="bkmk_2008AIpreq"></a>资产智能同步点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2008crppreq"></a>证书注册点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

-   HTTP 激活  

**IIS 配置：**

需要带有以下添加内容的默认 IIS 配置：  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

    -   IIS 6 WMI 兼容性  

###  <a name="bkmk_2008dppreq"></a>分发点  
**IIS 配置：**

可使用默认 IIS 配置或自定义配置。 若要使用自定义 IIS 配置，必须启用 IIS 的以下选项：  

-   应用程序开发：  

    -   ISAPI 扩展  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

    -   IIS 6 WMI 兼容性  

使用自定义 IIS 配置时，可以删除不需要的选项，如下所示：  

-   常见 HTTP 功能：  

    -   HTTP 重定向  

-   IIS 管理脚本和工具  

**Windows 功能：**  

-   远程差分压缩  

**Visual C++ Redistributable：**  

-   Configuration Manager 在托管分发点的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   安装的版本取决于计算机平台（x86 或 x64）。  

**Microsoft Azure：**  

-   可以使用 Azure 中的云服务来托管分发点。  

**支持 PXE 或多播：**  

-   安装和配置 Windows 部署服务 (WDS) Windows Server 角色。  

    > [!NOTE]  
    >  当配置分发点以在运行 Windows Server 2012 或更高版本的服务器上支持 PXE 或多播时，将自动安装和配置 WDS。  

> [!NOTE]  
> 分发点站点系统角色不需要后台智能传输服务 (BITS)。 在分发点计算机上配置 BITS 时，不使用分发点计算机上的 BITS 来辅助通过使用 BITS 的客户端下载内容。  


###  <a name="bkmk_2008EPPpreq"></a> Endpoint Protection 点  
**.NET Framework：**  

-   .NET Framework 3.5 SP1（或更高版本）  

###  <a name="bkmk_2008Enrollpreq"></a>注册点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

     安装此站点系统角色时，如果服务器未安装受支持的 .NET Framework 版本，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 当挂起对 .NET Framework 的重启时，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

**Windows Communication Foundation (WCF) 激活：**  

-   HTTP 激活  

-   非 HTTP 激活  

**IIS 配置：**

需要带有以下添加内容的默认 IIS 配置：  

-   应用程序开发：  

    -   ASP.NET（和自动选择的选项）  

         在某些情况下（如安装 .NET Framework 4.5.2 版本之后，安装或重新配置 IIS 时），必须显式启用 ASP.NET 4.5 版本。 例如，在运行 .NET Framework 版本 4.0.30319 的 64 位计算机上，运行以下命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**计算机内存：**  

-   托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

-   当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

###  <a name="bkmk_2008EnrollProxpreq"></a>注册代理点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

     安装此站点系统角色时，如果服务器未安装受支持的 .NET Framework 版本，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 当挂起对 .NET Framework 的重启时，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

**Windows Communication Foundation (WCF) 激活：**  

-   HTTP 激活  

-   非 HTTP 激活  

**IIS 配置：**

需要带有以下添加内容的默认 IIS 配置：  

-   应用程序开发：  

    -   ASP.NET（和自动选择的选项）  

         在某些情况下（如安装 .NET Framework 4.5.2 版本之后，安装或重新配置 IIS 时），必须显式启用 ASP.NET 4.5 版本。 例如，在运行 .NET Framework 版本 4.0.30319 的 64 位计算机上，运行以下命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**计算机内存：**  

-   托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

-   当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

###  <a name="bkmk_2008FSPpreq"></a>回退状态点  
**IIS 配置：**

需要带有以下添加内容的默认 IIS 配置：  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

###  <a name="bkmk_2008MPpreq"></a>管理点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

**IIS 配置：**

可使用默认 IIS 配置或自定义配置。 每个你启用以支持移动设备的管理点都需要 ASP.NET 的其他 IIS 配置（和其自动选择的选项）。

在某些情况下（如安装 .NET Framework 4.5.2 版本之后，安装或重新配置 IIS 时），必须显式启用 ASP.NET 4.5 版本。 例如，在运行 .NET Framework 版本 4.0.30319 的 64 位计算机上，运行以下命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  


若要使用自定义 IIS 配置，必须启用 IIS 的以下选项：  

-   应用程序开发：  

    -   ISAPI 扩展  

-   安全性：  

    -   Windows 身份验证  

-   IIS 6 管理兼容性：  

    -   IIS 6 元数据库兼容性  

    -   IIS 6 WMI 兼容性  


使用自定义 IIS 配置时，可以删除不需要的选项，如下所示：  

-   常见 HTTP 功能：  

    -   HTTP 重定向  

-   IIS 管理脚本和工具  

**Windows 功能：**  

-   BITS 服务器扩展（和自动选择的选项），或后台智能传输服务 (BITS)（和自动选择的选项）  

###  <a name="bkmk_2008RSpoint"></a> Reporting Services 点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services：**  

-   必须安装并配置至少一个 SQL Server 实例以在安装 Reporting Services 点之前支持 SQL Server Reporting Services。  

-   用于 SQL Server Reporting Services 的实例可以是用于站点数据库的同一实例。  

-   此外，只要其他 System Center 产品不具有对共享 SQL Server 实例的限制，则你使用的实例可与其他 System Center 产品共享。  

###  <a name="bkmk_2008SCPpreq"></a>服务连接点  
**.NET Framework：**  

-   .NET Framework 4.5.2  

     安装此站点系统角色时，如果服务器未安装受支持的 .NET Framework 版本，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 当挂起对 .NET Framework 的重启时，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

**Visual C++ Redistributable：**  

-   Configuration Manager 在托管分发点的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

-   站点系统角色需要 x64 版本。  

###  <a name="bkmk_2008SUPpreq"></a>软件更新点  
**.NET Framework：**  

-   .NET Framework 3.5 SP1（或更高版本）  

-   .NET Framework 4.5.2  

**IIS 配置：**

需要默认 IIS 配置。  

**Windows Server 更新服务：**  

-   安装软件更新点之前，必须在计算机上安装 Windows 服务器角色 Windows Server 更新服务。  

-   有关详细信息，请参阅 [System Center Configuration Manager 的软件更新计划](../../../sum/plan-design/plan-for-software-updates.md)。

###  <a name="bkmk_2008SMPpreq"></a>状态迁移点  
**IIS 配置：**

需要默认 IIS 配置。  
