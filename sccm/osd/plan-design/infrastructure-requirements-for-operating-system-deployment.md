---
title: "操作系统部署的基础结构要求 | Microsoft Docs"
description: "使用 System Center 2012 Configuration Manager 部署操作系统前，确保已了解外部依赖关系和产品依赖关系。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 167e639cdb9995fd743787cc9fbf364ec70f6ed9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的操作系统部署的基础架构要求

*适用范围：System Center Configuration Manager (Current Branch)*

System Center 2012 Configuration Manager 中的操作系统部署具有外部依赖关系和产品内依赖关系。 使用以下部分的内容帮助你准备操作系统的部署。  

##  <a name="BKMK_ExternalDependencies"></a> Configuration Manager 的外部依赖关系  
 下面提供了有关在 Configuration Manager 中部署操作系统所需的外部工具、安装工具包和操作系统的信息。  

### <a name="windows-adk-for-windows-10"></a>适用于 Windows 10 的 Windows ADK  
 Windows ADK 是一组工具和文档，为 Windows 操作系统的配置和部署提供支持。 Configuration Manager 使用 Windows ADK 来自动完成 Windows 安装、捕获 Windows 映像、迁移用户配置文件和数据，诸如此类。  

 必须在层次结构的顶层站点的站点服务器上、层次结构中每个主站点的站点服务器上以及 SMS 提供程序站点系统服务器上安装 Windows ADK 的以下功能：  

-   用户状态迁移工具 (USMT) <sup>1</sup>  

-   Windows 部署工具  

-   Windows 预安装环境 (Windows PE)

有关可对不同版本 Configuration Manager 使用的 Windows 10 ADK 版本列表，请参阅[对作为客户端的 Windows 10 的支持](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)。

 <sup>1</sup> SMS 提供程序站点系统服务器上不需要 USMT。  

> [!NOTE]  
>  在安装 Configuration Manager 站点之前，必须在每台计算机上手动安装 Windows ADK，这些计算机将托管管理中心站点或主站点服务器。  

 有关详情，请参阅：  

-   [面向 IT 专业人员的适用于 Windows 10 方案的 Windows ADK](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [下载适用于 Windows 10 的 Windows ADK](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [支持 Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>用户状态迁移工具 (USMT)  
 Configuration Manager 使用包含 USMT 10 源文件的 USMT 包在操作系统部署过程中捕获和还原用户状态。 位于顶层站点的 Configuration Manager 安装程序将自动创建 USMT 包。 USMT 10 可以捕获 Windows 7、Windows 8、Windows 8.1 和 Windows 10 中的用户状态。 在适用于 Windows 10 的 Windows 评估和部署工具包 (Windows ADK) 中分发 USMT 10。  

 有关详情，请参阅：  

-   [USMT 10 的常见迁移方案](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [管理用户状态](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE 用于引导映像以启动计算机。 它是一种提供有限服务的 Windows 操作系统，在 Windows 操作系统的预安装和部署过程中使用。 下面提供了 Configuration Manager 的版本、受支持的 Windows ADK 版本、启动映像所基于的 Windows PE 版本（可在 Configuration Manager 控制台中自定义），以及启动映像所基于的 Windows PE 版本（可使用 DISM 自定义，然后将映像添加到 Configuration Manager 指定版本）。  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager 版本 1511  
 下面提供了受支持的 Windows ADK 版本、可在 Configuration Manager 控制台中自定义的启动映像所基于的 Windows PE 版本，以及可使用 DISM 自定义，然后将映像添加到 Configuration Manager 的启动映像所基于的 Windows PE 版本。  

-   **Windows ADK 版本**  

     适用于 Windows 10 的 Windows ADK  

-   **可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 版本**  

     Windows PE 10  

-   **不可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 支持版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有当启动映像基于 Windows PE 3.1 时才能将该映像添加到 Configuration Manager 中。 安装适用于 Windows 7 SP1 的 Windows AIK 补充，以使用适用于 Windows 7 SP1（基于 Windows PE 3.1）的 Windows AIK 补充升级适用于 Windows 7（基于 Windows PE 3）的 Windows AIK。 你可以从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充。  

     例如，如果具有 Configuration Manager，则可以利用 Configuration Manager 控制台自定义适用于 Windows 10 的 Windows ADK 中的启动映像（基于 Windows PE 10）。 但是，当支持基于 Windows PE 5 的启动映像时，你必须在不同的计算机中自定义它们，并使用随适用于 Windows 8 的 Windows ADK 一起安装的 DISM 版本。 然后，可以向 Configuration Manager 控制台添加启动映像。 有关自定义启动映像（添加可选组件和驱动程序）、对启动映像启用命令支持、将启动映像添加到 Configuration Manager 控制台中，以及使用启动映像更新分发点的步骤的详细信息，请参阅[自定义启动映像](../get-started/customize-boot-images.md)。 有关启动映像的详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
必须安装以下 WSUS 4.0 修补程序：
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) 的 WSUS 4.0，它使用软件更新基础架构来获取 Windows 10 功能的升级。 如果你使用的是 WSUS 3.2，则必须使用任务序列来升级 Windows 10。 有关详细信息，请参阅[管理 Windows 即服务](../deploy-use/manage-windows-as-a-service.md)。  
  - 如果要使用 Windows 10 维护服务将计算机升级到 Windows 10 Anniversary Update，必须提供[修补程序 3159706](https://support.microsoft.com/kb/3159706)对于子序列版本也是如此。 支持文章中描述有手动操作步骤，必须按照这些步骤安装此修补程序。 有关详细信息，请参阅[管理 Windows 即服务](../deploy-use/manage-windows-as-a-service.md)。


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>站点系统服务器上的 Internet 信息服务 (IIS)  
 分发点、状态迁移点和管理点均需要 IIS。 有关此要求的详细信息，请参阅[站点和站点系统角色的先决条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-deployment-services-wds"></a>Windows 部署服务 (WDS)  
 PXE 部署需要 WDS，当你使用多播在部署中优化带宽以及将其用于脱机维护映像时，也需要 WDS。 如果在远程服务器上安装提供程序，则必须在站点服务器和远程提供程序上安装 WDS。 有关详细信息，请参阅本主题中的 [Windows 部署服务](#BKMK_WDS) 。  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>动态主机配置协议 (DHCP)  
 DHCP 是 PXE 部署所必需的。 你必须有正常运行的 DHCP 服务器（带有活动主机）才能使用 PXE 部署操作系统。 有关 PXE 部署的详细信息，请参阅[使用 PXE 通过网络部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>支持的操作系统和硬盘配置  
 有关部署操作系统时 Configuration Manager 所支持的操作系统版本和硬盘配置的详细信息，请参阅[支持的操作系统](#BKMK_SupportedOS)和[支持的硬盘配置](#BKMK_SupportedDiskConfig)。  

### <a name="windows-device-drivers"></a>Windows 设备驱动程序  
 当你在目标计算机上安装操作系统，以及使用启动映像来运行 Windows PE 时，可以使用 Windows 设备驱动程序。 有关设备驱动程序的详细信息，请参阅[管理驱动程序](../get-started/manage-drivers.md)。  

##  <a name="BKMK_InternalDependencies"></a> Configuration Manager 依赖关系  
 下面提供了有关 Configuration Manager 操作系统部署先决条件的信息。  

### <a name="operating-system-image"></a>操作系统映像  
 Configuration Manager 中的操作系统映像以 Windows 映像 (WIM) 文件格式存储，代表在计算机上成功安装和配置操作系统所需的引用文件和文件夹的压缩集合。 有关详细信息，请参阅[管理操作系统映像](../get-started/manage-operating-system-images.md)。  

### <a name="driver-catalog"></a>驱动程序目录  
 要部署设备驱动程序，必须导入并启用该设备驱动程序，然后使其在 Configuration Manager 客户端可访问的分发点上可用。 有关驱动程序目录的详细信息，请参阅[管理驱动程序](../get-started/manage-drivers.md)。  

### <a name="management-point"></a>管理点  
 管理点在客户端计算机和 Configuration Manager 站点之间传输信息。 客户端使用管理点来运行完成操作系统部署所需的任何任务序列。  

 有关任务序列的详细信息，请参阅[计划自动执行任务时的考虑事项](planning-considerations-for-automating-tasks.md)。  

### <a name="distribution-point"></a>分发点  
 分发点在大多数部署中使用，存储用于部署操作系统的数据，例如操作系统映像或设备驱动程序包。 任务序列通常从分发点中检索数据来部署操作系统。  

 有关如何安装分发点和管理内容的详细信息，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="pxe-enabled-distribution-point"></a>已启用 PXE 的分发点  
 要部署 PXE 启动的部署，你必须将分发点配置为接受来自客户端的 PXE 请求。 有关如何配置分发点的详细信息，请参阅[配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe)。  

### <a name="multicast-enabled-distribution-point"></a>启用多播的分发点  
 要使用多播优化操作系统部署，你必须配置分发点以支持多播。 有关如何配置分发点的详细信息，请参阅[配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast)。   

### <a name="state-migration-point"></a>状态迁移点  
 在为并排部署和全新部署捕获和还原用户状态数据时，你必须配置状态迁移点以便将用户状态数据存储在另一台计算机上。  

 有关如何配置状态迁移点的详细信息，请参阅 [状态迁移点](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

 有关如何捕获和还原用户状态的信息，请参阅[管理用户状态](../get-started/manage-user-state.md)。  

### <a name="service-connection-point"></a>服务连接点  
 使用 Windows 即服务 (WaaS) 部署 Windows 10 当前分支时，必须已安装服务连接点。 有关详细信息，请参阅[管理 Windows 即服务](../deploy-use/manage-windows-as-a-service.md)。  

### <a name="reporting-services-point"></a>Reporting Services 点  
 如果针对操作系统部署需使用 Configuration Manager 报表，则必须安装和配置 Reporting Services 点。 有关详细信息，请参阅[报表](../../core/servers/manage/reporting.md)。  

### <a name="security-permissions-for-operating-system-deployments"></a>操作系统部署的安全权限  
 “操作系统部署管理员”  安全角色是一个无法更改的内置角色。 不过，你可以复制该角色，进行更改，然后将这些更改保存为一个新的自定义安全角色。 下面是一些直接应用于操作系统部署的权限：  

-   **启动映像包**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

-   **设备驱动程序**：创建、删除、修改、修改文件夹、修改报表、移动对象、读取、运行报表  

-   **驱动程序包**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

-   **操作系统映像**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

-   **操作系统安装包**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

-   **任务序列包**：创建、创建任务序列介质、删除、修改、修改文件夹、修改报表、移动对象、读取、运行报表、设置安全作用域  

 有关自定义安全角色的详细信息，请参阅 [创建自定义安全角色](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)。  

### <a name="security-scopes-for-operating-system-deployments"></a>操作系统部署的安全作用域  
 使用安全作用域来向管理用户提供对操作系统部署中所使用的安全对象（例如操作系统和启动映像、驱动程序包以及任务序列包）的访问权限。 有关详细信息，请参阅 [安全作用域](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)。  

##  <a name="BKMK_WDS"></a> Windows 部署服务  
 必须在配置为支持 PXE 或多播的分发点所在的服务器上安装 Windows 部署服务 (WDS)。 WDS 包括在服务器的操作系统中。 对于 PXE 部署，WDS 是执行 PXE 启动的服务。 如果为 PXE 安装和启用了分发点，则 Configuration Manager 会将一个使用 WDS PXE 启动功能的提供程序安装到 WDS 中。  

> [!NOTE]  
>  如果服务器需要重启，则 WDS 的安装可能会失败。 

 必须考虑的其他 WDS 配置包括下列各项：  

-   服务器上的 WDS 安装要求管理员是“本地管理员”组的成员。  

-   WDS 服务器必须是 Active Directory 域或 Active Directory 域的域控制器的成员。 所有 Windows 域和林配置都支持 WDS。  

-   如果在远程服务器上安装提供程序，则必须在站点服务器和远程提供程序上安装 WDS。  

###  <a name="BKMK_WDSandDHCP"></a> WDS 和 DHCP 在同一个服务器上时的注意事项  
 如果计划在运行 DHCP 的服务器上共同承载分发点，请考虑以下配置问题。  

-   必须具有正常运行的 DHCP 服务器和活动作用域。 Windows 部署服务使用需要 DHCP 服务器的 PXE。  

-   DHCP 和 Windows 部署服务都需要端口号 67。 如果共同承载 Windows 部署服务和 DHCP，则可以将为 PXE 配置的 DHCP 或分发点移动到单独的服务器。 或者可以使用以下过程将 Windows 部署服务服务器配置为侦听其他端口。  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>将 Windows 部署服务服务器配置为侦听其他端口  

    1.  修改下面的注册表项：  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  将注册表值设置为： **UseDHCPPorts = 0**  

    3.  为了使新配置生效，请在服务器上运行以下命令：  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   运行 Windows 部署服务需要 DNS 服务器。  

-   必须在 Windows 部署服务服务器上打开以下 UDP 端口。  

    -   端口 67 (DHCP)  

    -   端口 69 (TFTP)  

    -   端口 4011 (PXE)  

    > [!NOTE]  
    >  此外，如果服务器上需要 DHCP 授权，则需要在服务器上打开 DHCP 客户端端口 68。  

##  <a name="BKMK_SupportedOS"></a> 支持的操作系统  
 所有 Windows 操作系统（在[客户端和设备支持的操作系统](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)中列为受支持的操作系统）都支持用于操作系统部署。  

##  <a name="BKMK_SupportedDiskConfig"></a> 支持的磁盘配置  
 下表显示了引用计算机和目标计算机上 Configuration Manager 操作系统部署支持的硬盘配置组合。  

|引用计算机硬盘配置|目标计算机硬盘配置|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁盘|基本磁盘|  
|动态磁盘上的简单卷|动态磁盘上的简单卷|  

 Configuration Manager 仅支持从配置有简单卷的计算机捕获操作系统映像。 不支持下列硬盘配置：  

-   跨区卷  

-   带区卷 (RAID 0)  

-   镜像卷 (RAID 1)  

-   奇偶校验卷 (RAID 5)  

 下表显示了引用计算机和目标计算机上不支持用于 Configuration Manager 操作系统部署的其他硬盘配置。  

|引用计算机硬盘配置|目标计算机硬盘配置|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁盘|动态磁盘|  

## <a name="next-steps"></a>后续步骤
[准备操作系统部署](../get-started/prepare-for-operating-system-deployment.md)
