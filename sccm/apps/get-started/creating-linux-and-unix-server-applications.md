---
title: "创建 Linux 和 UNIX 服务器应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 Linux 和 Unix 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 04/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72ebd8bd29b5ecdd817631e447291c04f49d9808
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-linux-and-unix-server-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Linux 和 UNIX 服务器应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

为运行 Linux 和 UNIX 的计算机创建和部署应用程序时，请考虑以下注意事项。  

## <a name="general-considerations"></a>一般注意事项  
 适用于 Linux 和 UNIX 的 Configuration Manager 客户端支持“使用包和程序的软件部署”。 无法将 Configuration Manager 应用程序部署到运行 Linux 和 UNIX 的计算机。  

 Linux 和 UNIX 软件部署的功能包括：  

-   Linux 和 UNIX 服务器的软件安装包括以下各项：  

    -   新软件部署  

    -   计算机上已有程序的软件更新  

    -   操作系统修补程序  

-   本机 Linux 和 UNIX 命令，以及位于 Linux 和 UNIX 服务器上的脚本  

-   限制为在选择程序选项“仅在指定的客户端平台上”时指定的操作系统的部署

-   用于控制软件安装时间的维护时段

-   用于监视部署的部署状态消息  

-   客户端从分发点下载软件时，用于其限制网络使用的选项  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>部署到 Linux 和 UNIX 计算机与部署到 Windows 设备之间的差异
将包和程序部署到 Linux 和 UNIX 计算机与将包和程序部署到 Windows 设备之间的主要差异如下：  

|配置|详细信息|  
|-------------------|-------------|  
|仅使用适用于计算机的配置，而不要使用适用于用户的配置。|适用于 Linux 和 UNIX 的 Configuration Manager 客户端不支持适用于用户的配置。|  
|将程序配置为从分发点下载软件，并从本地客户端缓存中运行程序。|适用于 Linux 和 UNIX 的 Configuration Manager 客户端不支持从分发点运行软件。 而必须配置软件以下载到客户端，然后进行安装。<br /><br /> 默认情况下，在适用于 Linux 和 UNIX 的客户端安装软件后，将从客户端的缓存中删除该软件。 但是，在软件安装之后，不会从客户端中删除配置了“保留客户端缓存中的内容”  的包，并会将其保留在客户端的缓存中。<br /><br /> 适用于 Linux 和 UNIX 的客户端不支持客户端缓存的配置，并且客户端缓存的最大大小仅受客户端计算机上的可用磁盘空间限制。|  
|为分发点访问配置网络访问帐户|Linux 和 UNIX 计算机设计为工作组计算机。 为了在 Configuration Manager 站点服务器域中访问分发点中的包，必须为站点配置网络访问帐户。 你必须指定此帐户作为软件分发组件属性，并在部署软件之前配置帐户。<br /><br /> 你可以在每个站点配置多个网络访问帐户。 适用于 Linux 和 UNIX 的客户端可使用你配置的每个帐户作为网络访问帐户。<br /><br /> 有关详细信息，请参阅 [Site components for System Center Configuration Manager](../../core/servers/deploy/configure/site-components.md)。|  

 你可以将包和程序部署到仅包含 Linux 或 UNIX 客户端的集合，或者可以将它们部署到包含混合客户端类型的集合，例如“所有系统集合” 。 但是，非 Linux 和非 UNIX 客户端将不安装软件或报告失败。  

 当适用于 Linux 和 UNIX 的 Configuration Manager 客户端接收并运行部署时，它将生成状态消息。 可以在 Configuration Manager 控制台中查看这些状态消息，或通过使用报表来监视部署状态。  

 有关如何使用包和程序的信息，请参阅[包和程序](../../apps/deploy-use/packages-and-programs.md)。  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>为 Linux 和 UNIX 服务器配置包、程序和部署  
 可以使用 Configuration Manager 控制台中提供的默认选项来创建和部署包和程序。 客户端不需要任何唯一的配置。  

 使用下一节中的信息来配置包和程序以及部署。  

### <a name="packages-and-programs"></a>包和程序  
 若要创建适用于 Linux 或 UNIX 服务器的包和程序，请从 Configuration Manager 控制台使用“创建包和程序向导”。 适用于 Linux 和 UNIX 的客户端支持大多数包和程序设置。 但是，有一些设置不受支持。 在创建或配置包和程序时，请考虑以下事项：  

-   包括目标计算机所支持的文件类型。  

-   定义适合于在目标计算机上使用的命令行。  

-   请记住，不支持与用户交互的设置。  

下表列出了不受支持的包和程序属性：  

|包和程序属性|行为|更多信息|  
|----------------------------------|--------------|----------------------|  
|包共享设置：<br /><br /> - 所有选项|生成错误，并且软件安装失败|客户端不支持此配置。 相反，客户端必须通过使用 HTTP 或 HTTPS 下载软件，然后从其本地缓存中运行命令行。|  
|包更新设置：<br /><br /> - 断开用户与分发点的连接|忽略设置|客户端不支持此配置。|  
|操作系统部署设置：<br /><br /> - 所有选项|忽略设置|客户端不支持此配置。|  
|报表：<br /><br /> - 将包属性用于状态 MIF 匹配<br /><br /> - 将这些字段用于状态 MIF 匹配|忽略设置|客户端不支持使用状态 MIF 文件。|  
|**运行**：<br /><br /> - 所有选项|忽略设置|客户端始终不带用户界面运行包。<br /><br /> 客户端忽略适用于“运行”的所有配置选项。|  
|运行之后:<br /><br />- Configuration Manager 重启计算机<br /><br /> - 程序控制重启<br /><br /> - Configuration Manager 注销用户|生成错误，并且软件安装失败|不支持系统重启设置和特定于用户的设置。<br /><br /> 如果在使用除“不需要任何操作”  设置之外的任何其他设置，则客户端将生成错误并继续软件安装，而不进行任何操作。|  
|程序可以运行：<br /><br /> - 仅当用户登录时|生成错误，并且软件安装失败|不支持特定于用户的设置。<br /><br /> 如果配置了此选项，客户端将生成错误并使软件安装失败。<br /><br /> 将忽略其他选项，并且软件安装将继续。|  
|运行模式：<br /><br /> - 使用用户的权限运行|忽略设置|不支持特定于用户的设置。<br /><br /> 但是，客户端支持使用管理权限运行的配置。<br /><br /> 当指定“使用管理权限运行”时，Configuration Manager 客户端使用其根凭据。<br /><br /> 此设置不会生成错误或日志条目。 而在客户端对于“程序可以运行” = “仅当用户登录时”的先决条件配置生成错误时，软件安装将失败。|  
|允许用户查看程序安装并与之交互|忽略设置|不支持特定于用户的设置。<br /><br /> 将忽略此配置，并且软件安装将继续。|  
|驱动器模式：<br /><br /> - 所有选项|忽略设置|由于会始终将内容下载到客户端并以本地方式运行，因此不支持此设置。|  
|首先运行其他程序|生成错误，并且软件安装失败|不支持递归程序安装。<br /><br /> 当某个程序配置为先运行另一个程序时，软件安装将失败，并且不会启动其他程序安装。|  
|当此程序分配到计算机时：<br /><br /> - 为每个登录用户运行一次|忽略设置|不支持特定于用户的设置。<br /><br /> 但是，客户端支持为计算机运行一次的配置。<br /><br /> 此设置不生成错误或日志条目，因为已经为设置为“仅当用户登录时”  = **仅当用户登录时**。|  
|取消程序通知|忽略设置|客户端不实现用户界面。<br /><br /> 如果选择了此配置，则会将其忽略，并且软件安装将继续。|  
|在部署此程序的计算机上禁用此程序|忽略设置|不支持此设置，并且此设置不影响软件的安装。|  
|允许在不部署的情况下从“安装包”任务序列安装此程序。||客户端不支持任务序列。<br /><br /> 不支持此设置，并且此设置不影响软件的安装。|  
|Windows Installer：<br /><br /> - 所有选项|忽略设置|客户端不支持 Windows Installer 文件或设置。|  
|OpsMgr 维护模式：<br /><br /> - 所有选项|忽略设置|客户端不支持此配置。|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>将软件部署到 Linux 或 UNIX 服务器
 若要使用包和程序将软件部署到 Linux 或 UNIX 服务器中，可以从 Configuration Manager 控制台使用“部署软件向导”。 适用于 Linux 和 UNIX 的客户端支持大多数部署设置。 但是，有一些设置不受支持。 在部署软件时，请考虑以下事项：  

-   你必须在与针对内容位置配置的边界组关联的至少一个分发点上设置包。  

-   接收此部署的适用于 Linux 和 UNIX 的客户端必须能够从其网络位置访问此分发点。  

-   适用于 Linux 和 UNIX 的客户端从分发点下载包，并在本地计算机上运行程序。  

-   适用于 Linux 和 UNIX 的客户端无法从共享文件夹中下载包。 它从启用了 IIS 的分发点（支持 HTTP 或 HTTPS）下载包。  

 下表列出了不受支持的部署的属性：  

|部署属性|行为|更多信息|  
|-------------------------|--------------|----------------------|  
|部署设置 – 目的：<br /><br /> - 可用<br /><br /> - 必需|忽略设置|不支持特定于用户的设置。<br /><br /> 但是，客户端支持“必需” 设置，该设置强制实施计划的安装时间，但不支持在该计划的时间之前进行手动安装。|  
|发送唤醒数据包|忽略设置|客户端不支持此配置。|  
|分配计划：<br /><br /> - 登录<br /><br /> - 注销|生成错误，并且软件安装失败|不支持特定于用户的设置。<br /><br /> 但是，客户端支持“尽快” 设置。|  
|通知设置：<br /><br /> - 允许用户独立于分配运行程序|忽略设置|客户端不实现用户界面。|  
|如果已达到计划的分配时间，则允许在维护时段之外执行以下活动：<br /><br /> - 系统重启(如果要求完成安装)|生成错误|客户端不支持系统重启。|  
|适用于快速（LAN）网络的部署选项：<br /><br /> - 从分发点运行程序|生成错误，并且软件安装失败|客户端无法从分发点运行软件，而是必须下载程序，之后它才能运行。|  
|适用于慢速或不可靠网络边界或者内容的回退源位置的部署选项：<br /><br /> - 允许客户端与同一子网上的其他客户端共享内容|忽略设置|客户端不支持在对等方之间共享内容。|  

 有关内容位置的详细信息，请参阅[为 System Center Configuration Manager 管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

 有关如何创建部署的详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>管理从分发点下载软件的网络带宽  
 Linux 和 UNIX 客户端支持在从分发点下载软件时控制网络带宽。  

 客户端使用你在 Configuration Manager 中配置为客户端设置的后台智能传输 (BITS) 设置，但不实施 BITS。 相反，为了限制网络带宽的使用，客户端将控制软件下载的 HTTP 请求块大小和块间延迟。  

 若要配置客户端以使用网络带宽控制，请为“后台智能传输”  配置客户端设置，然后将这些设置应用于客户端计算机。 为了使用带宽控制，客户端必须接收以下设置配置为“是”的“后台智能传输”客户端设置：  

-   **限制 BITS 后台传输的最大网络带宽**  

 客户端支持下列后台智能传输配置：  

    -   **限制时段开始时间**  

    -   **限制时段结束时间**  

    -   **限制时段期间的最大传输速率(Kbps)**  

    -   **限制时段外的最大传输速率(Kbps)**  

下列后台智能传输配置不受支持，适用于 Linux 和 UNIX 的客户端将忽略这些设置：  

-   **允许 BITS 在限制时段外下载**  

 如果从分发点将软件下载到客户端的过程中断，适用于 Linux 和 UNIX 的客户端不会恢复下载。 而是会重启整个软件包的下载。  

##  <a name="configure-operations-for-software-deployments"></a>配置软件部署的操作  
 与 Windows 客户端类似，适用于 Linux 和 UNIX 的 Configuration Manager 客户端在轮询和检查新策略时发现新软件部署。 客户端检查新策略的频率取决于客户端设置。 你可以配置维护时段以控制何时进行软件部署。  

 你可以使用包属性、程序属性和部署属性来配置针对 Linux 和 UNIX 服务器的软件部署。  

 当客户端接收部署的策略时，它将提交状态消息。 它还会在开始安装软件以及安装完成或失败时提交状态消息。  

 用于软件部署的程序使用根凭据运行，适用于 Linux 和 UNIX 的 Configuration Manager 客户端将使用该凭据运行。 程序命令的退出代码用于确定成功或失败。 退出代码 0（零）被视为成功。 此外，当日志级别设置为 INFO 或 TRACE 时，会将“stdout”  （标准输出流）和“stderr”  （标准错误流）复制到日志文件。  

> [!TIP]  
>  如果你要部署的软件位于 Linux 或 UNIX 服务器可访问的网络文件系统 (NFS) 共享上，则无需使用分发点来下载包。 相反，当你创建包时，不要选中“此包包含源文件” 复选框。 然后，当你配置程序时，请指定适当的命令行以直接访问 NFS 装入点上的包。  
