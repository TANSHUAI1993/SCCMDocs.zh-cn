---
title: OSD 基础结构要求
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的 OS 部署的外部依赖关系和产品依赖关系及要求
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03ec9c046e1b32f137777f15393b5d26b49e5520
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236151"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Configuration Manager 中的 OS 部署的基础结构要求

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的 OS 部署包含外部依赖关系和产品内的依赖关系。 使用本文可帮助你为 OS 部署准备基础结构。  



##  <a name="BKMK_ExternalDependencies"></a> Configuration Manager 的外部依赖关系  

此部分介绍在 Configuration Manager 中部署操作系统所需的外部工具、安装工具包和 OS 版本。  

### <a name="windows-adk-for-windows-10"></a>适用于 Windows 10 的 Windows ADK  

Windows 评估和部署工具包 (ADK) 是一组工具和文档，为 Windows 的配置和部署提供支持。 Configuration Manager 使用 Windows ADK 自动执行诸如安装 Windows、捕获映像以及迁移用户配置文件和数据之类的操作。  

有关详细信息，请参阅下列文章：  

- [面向 IT 专业人员的适用于 Windows 10 方案的 Windows ADK](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [下载适用于 Windows 10 的 Windows ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

- [支持 Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


#### <a name="site-systems"></a>站点系统
Windows ADK 是以下站点系统服务器的先决条件：

- 层次结构中顶层站点的站点服务器  

- 层次结构中每个主站点的站点服务器  

- SMS 提供程序的每个实例  


> [!NOTE]  
> 在安装 Configuration Manager 站点之前，请在每个站点服务器上手动安装 Windows ADK。  

#### <a name="windows-adk-features"></a>Windows ADK 功能
安装 Windows ADK 的以下功能：  

-   用户状态迁移工具 (USMT)  

    > [!Note]  
    > SMS 提供程序上不需要 USMT。

-   Windows 部署工具  

-   Windows 预安装环境 (Windows PE)  

    > [!Important]  
    > 从 Windows 10 版本 1809 开始，Windows PE 是单独的安装程序。 但是功能上没有任何区别。<!--SCCMDocs-pr issue 2908-->  

有关可用于不同 Configuration Manager 版本的 Windows 10 ADK 版本的列表，请参阅[对 Windows 10 的支持](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)。


### <a name="user-state-migration-tool-usmt"></a>用户状态迁移工具 (USMT)  

Configuration Manager 使用包含 USMT 10 源文件的 USMT 包在 OS 部署过程中捕获和还原用户状态。 位于顶层站点的 Configuration Manager 安装程序将自动创建 USMT 包。 USMT 10 可从 Windows 7、Windows 8、Windows 8.1 和 Windows 10 中捕获用户状态。  

有关详细信息，请参阅下列文章：  

- [USMT 10 的常见迁移方案](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [管理用户状态](/sccm/osd/get-started/manage-user-state)  


### <a name="windows-pe"></a>Windows PE  

Windows PE 用于引导映像以启动计算机。 它是一种提供有限服务的 Windows 版本，在 Windows 的预安装和部署过程中会使用这些服务。 以下列表包含适用于 Configuration Manager Current Branch 的 Windows ADK 受支持版本：  

#### <a name="windows-adk-version"></a>Windows ADK 版本  
适用于 Windows 10 的 Windows 评估和部署工具包。 有关详细信息，请参阅[对 Windows 10 的支持](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)。

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>可从 Configuration Manager 控制台自定义的启动映像的 Windows PE 版本  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>不可从 Configuration Manager 控制台自定义的启动映像的受支持的 Windows PE 版本  
Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

<sup>1</sup> 只有当启动映像基于 Windows PE 3.1 时才能将该映像添加到 Configuration Manager。 安装适用于 Windows 7 SP1 的 Windows AIK 补充，以使用适用于 Windows 7 SP1（基于 Windows PE 3.1）的 Windows AIK 补充升级适用于 Windows 7（基于 Windows PE 3）的 Windows AIK。 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充程序。  

例如，如果具有 Configuration Manager，则可以利用 Configuration Manager 控制台自定义适用于 Windows 10 的 Windows ADK 中的启动映像（基于 Windows PE 10）。 但是，当支持基于 Windows PE 5 的启动映像时，必须从不同的计算机对它们进行自定义，并使用随用于 Windows 8 的 Windows ADK 一起安装的 DISM 版本。 然后将启动映像添加到 Configuration Manager 控制台。 有关自定义启动映像（添加可选组件和驱动程序）、对启动映像启用命令支持、将启动映像添加到 Configuration Manager 控制台中，以及使用启动映像更新分发点的步骤的详细信息，请参阅[自定义启动映像](/sccm/osd/get-started/customize-boot-images)。 有关启动映像的详细信息，请参阅[管理启动映像](/sccm/osd/get-started/manage-boot-images)。  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

软件更新点需要 WSUS 才能在 OS 部署期间安装软件更新。 有关详细信息，请参阅[安装和配置软件更新点](/sccm/sum/get-started/install-a-software-update-point)。


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>站点系统服务器上的 Internet 信息服务 (IIS)  

分发点、状态迁移点和管理点均需要 IIS。 有关详细信息，请参阅[站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。  


### <a name="windows-deployment-services-wds"></a>Windows 部署服务 (WDS)  

在版本 1802 及更早的版本中，PXE 部署需要使用 WDS。 从版本 1806 开始，可在没有 WDS 的分发点上启用 PXE。 有关详细信息，请参阅本文中的 [Windows 部署服务](#BKMK_WDS)。 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>动态主机配置协议 (DHCP)  

DHCP 是 PXE 部署所必需的。 你必须有正常运行的 DHCP 服务器（带有活动主机）才能使用 PXE 部署操作系统。 有关 PXE 部署的详细信息，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>支持的操作系统和硬盘配置  

若要详细了解部署操作系统时 Configuration Manager 所支持的 OS 版本和硬盘配置，请参阅[支持的操作系统](#BKMK_SupportedOS)和[支持的磁盘配置](#BKMK_SupportedDiskConfig)。  


### <a name="windows-device-drivers"></a>Windows 设备驱动程序  

在目标计算机上安装 OS 时，可以使用 Windows 设备驱动程序。 在启动映像中运行 Windows PE 时也可使用。 有关详细信息，请参阅[管理驱动程序](/sccm/osd/get-started/manage-drivers)。  



##  <a name="BKMK_InternalDependencies"></a> Configuration Manager 依赖关系  

此部分介绍 Configuration Manager OS 部署先决条件。  


### <a name="os-image"></a>OS 映像  

Configuration Manager 中的 OS 映像以 Windows 映像 (WIM) 文件格式存储。 它们表示引用文件和文件夹的压缩集合。 这些映像是在计算机上成功安装和配置 OS 所必需的。 有关详细信息，请参阅[管理 OS 映像](/sccm/osd/get-started/manage-operating-system-images)。  


### <a name="driver-catalog"></a>驱动程序目录  

若要部署设备驱动程序，请导入并启用该设备驱动程序，然后使其在 Configuration Manager 客户端可访问的分发点上可用。 有关驱动程序目录的详细信息，请参阅[管理驱动程序](/sccm/osd/get-started/manage-drivers)。  


### <a name="management-point"></a>管理点  

管理点用于在客户端和 Configuration Manager 站点之间传输信息。 客户端使用管理点运行任务序列，以完成 OS 部署。 有关任务序列的详细信息，请参阅[计划自动执行任务时的考虑事项](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)。  


### <a name="distribution-point"></a>分发点  

大多数部署使用分发点存储用于部署 OS 的数据，例如映像或驱动程序包。 任务序列通常从分发点中检索数据来部署 OS。 有关如何安装分发点和管理内容的详细信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。  


### <a name="pxe-enabled-distribution-point"></a>已启用 PXE 的分发点  

若要部署 PXE 启动的部署，请将分发点配置为接受来自客户端的 PXE 请求。 有关详细信息，请参阅[配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)。


### <a name="multicast-enabled-distribution-point"></a>启用多播的分发点  

若要使用多播优化 OS 部署，请将分发点配置为支持多播。 有关详细信息，请参阅[配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-multicast)。   


### <a name="state-migration-point"></a>状态迁移点  

在为并排部署和全新部署捕获和还原用户状态数据时，请配置状态迁移点以便将用户状态数据存储在另一台计算机上。  

有关如何配置状态迁移点的详细信息，请参阅 [状态迁移点](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_StateMigrationPoints)。  

若要详细了解如何捕获和还原用户状态，请参阅[管理用户状态](/sccm/osd/get-started/manage-user-state)。  


### <a name="reporting-services-point"></a>Reporting Services 点  

要将 Configuration Manager 报表用于 OS 部署，请安装并配置报表点。 有关详细信息，请参阅[报表](/sccm/core/servers/manage/reporting)。  


### <a name="security-permissions-for-os-deployments"></a>OS 部署的安全权限  

“操作系统部署管理员”安全角色是一个无法更改的内置角色。 不过，你可以复制该角色，进行更改，然后将这些更改保存为一个新的自定义安全角色。 下面是一些直接应用于 OS 部署的权限：  

- **启动映像包**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

- **设备驱动程序**：创建、删除、修改、修改文件夹、修改报表、移动对象、读取、运行报表  

- **驱动程序包**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

- **操作系统映像**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

- **操作系统升级包**：创建、删除、修改、修改文件夹、移动对象、读取、设置安全作用域  

- **任务序列包**：创建、创建任务序列介质、删除、修改、修改文件夹、修改报表、移动对象、读取、运行报表、设置安全作用域  

有关详细信息，请参阅[创建自定义安全角色](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)。  


### <a name="security-scopes-for-os-deployments"></a>OS 部署的安全作用域  

安全作用域用于向管理用户提供对 OS 部署中所使用的安全对象（例如 OS 和启动映像、驱动程序包以及任务序列包）的访问权限。 有关详细信息，请参阅 [安全作用域](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope)。  



##  <a name="BKMK_WDS"></a> Windows 部署服务  

在版本 1802 及更早的版本中，必须在配置为支持 PXE 或多播的分发点所在的服务器上安装 Windows 部署服务 (WDS)。 WDS 包括在服务器 OS 中。 对于 PXE 部署，WDS 是执行 PXE 启动的服务。 如果为 PXE 安装和启用了分发点，则 Configuration Manager 会将一个使用 WDS PXE 启动功能的提供程序安装到 WDS 中。  

从版本 1806 开始，可在没有 WDS 的分发点上启用 PXE。 如需获取更多详细信息，请查看[安装并配置分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe)中的“启用无 Windows 部署服务的 PXE 响应程序”选项。


> [!NOTE]  
>  如果服务器需要重启，则 WDS 的安装可能会失败。 


### <a name="wds-requirements"></a>WDS 要求  

-   服务器上的 WDS 安装要求管理员是本地管理员组的成员。  

-   WDS 服务器必须是 Active Directory 域或 Active Directory 域的域控制器的成员。 所有 Windows 域和林配置都支持 WDS。  

-   如果提供程序安装在远程服务器上，请在站点服务器和远程提供程序上安装 WDS。  


###  <a name="BKMK_WDSandDHCP"></a> WDS 和 DHCP 在同一个服务器上时的注意事项  

如果计划在运行 DHCP 的服务器上共同托管分发点，请考虑以下配置问题：  

-   必须具有正常运行的 DHCP 服务器和活动作用域。 WDS 使用需要 DHCP 服务器的 PXE。  

-   DNS 服务器是运行 WDS 所必需的。  

-   必须在 WDS 服务器上打开下列 UDP 端口：  

    -   端口 67 (DHCP)  

    -   端口 69 (TFTP)  

    -   端口 4011 (PXE)  

    > [!NOTE]  
    >  如果服务器上需要 DHCP 授权，则需要在服务器上打开 DHCP 客户端端口 68。  

-   DHCP 和 WDS 都需要端口号 67。 如果共同托管 WDS 和 DHCP，则可以将为 PXE 配置的 DHCP 或分发点移动到单独的服务器。 或者可以使用以下过程将 WDS 服务器配置为侦听其他端口。  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>将 WDS 服务器配置为侦听其他端口  

1.  修改下面的注册表项：  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  将注册表值 **UseDHCPPorts** 设置为 **0**。  

3.  为了使新配置生效，请在服务器上运行以下命令：  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  



##  <a name="BKMK_SupportedOS"></a> 支持的操作系统  

OS 部署支持所有在[客户端和设备支持的 操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中列为受支持客户端的 Windows 操作系统。  



##  <a name="BKMK_SupportedDiskConfig"></a> 支持的磁盘配置  

下表显示了引用计算机和目标计算机上 Configuration Manager OS 部署支持的硬盘配置组合：  

|引用计算机硬盘配置|目标计算机硬盘配置|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁盘|基本磁盘|  
|动态磁盘上的简单卷|动态磁盘上的简单卷|  

Configuration Manager 仅支持从配置有简单卷的计算机捕获 OS 映像。 不支持下列硬盘配置：  

-   跨区卷  

-   带区卷 (RAID 0)  

-   镜像卷 (RAID 1)  

-   奇偶校验卷 (RAID 5)  

下表显示了引用计算机和目标计算机上 Configuration Manager OS 部署不支持的其他硬盘配置。  

|引用计算机硬盘配置|目标计算机硬盘配置|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁盘|动态磁盘|  



## <a name="next-steps"></a>后续步骤

- [为 OS 部署准备站点系统角色](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [准备进行 OS 部署](/sccm/osd/get-started/prepare-for-operating-system-deployment)
