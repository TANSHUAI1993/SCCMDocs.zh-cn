---
title: "服务连接点 | Microsoft Docs"
description: "了解此 Configuration Manager 站点系统角色，并了解和规划其使用范围。"
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e3d41dc1bb732e887d722f39ee86deaf0aae3240
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>关于 System Center Configuration Manager 中的服务连接点

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 服务连接点是一个站点系统角色，为层次结构提供几个重要的功能。 设置服务连接点之前，需了解和规划其使用范围，这可能会影响到设置此站点系统角色的方式：  

-   **使用 Microsoft Intune 管理移动设备** – 此角色替换此前版本的 Configuration Manager 使用的 Windows Intune 连接器，并可通过 Intune 订阅详细信息进行配置。 请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)](../../../../mdm/understand/hybrid-mobile-device-management.md)。  

-   **使用本地 MDM 管理移动设备** – 此角色为你所管理的未连接到 Internet 的本地设备提供支持。 请参阅[在 System Center Configuration Manager 中使用本地基础结构管理移动设备](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

-   **从 Configuration Manager 基础结构上传使用情况数据** – 可以控制上传的详细信息的量和级别。 上载的数据帮助我们：  

    -   主动识别和排除问题  

    -   改进我们的产品和服务  

    -   确定适用于你所使用的 Configuration Manager 版本的 Configuration Manager 更新  

  有关各级别收集的数据，以及安装角色后如何更改收集级别的信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)，然后按照针对你所用的 Configuration Manage 版本的链接进行操作。  

  有关详细信息，请参阅[使用情况数据级别和设置](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)。  

-   **下载适用于你的 Configuration Manager 基础结构的更新** - 基于你所上传的使用情况数据，仅适用于你的基础结构的相关更新可用。  

- **每个层次结构支持此角色的单一实例：**  

 -   此站点系统角色只能安装在层次结构的顶层站点上，即管理中心站点或独立主站点。  

  -   如果将独立主站点扩展到更大的层次结构，则必须从主站点中卸载此角色，然后才可将其安装在管理中心站点上。  


##  <a name="bkmk_modes"></a>操作模式  
 服务连接点支持两种操作模式：  

-   在“联机模式”下，服务连接点每 24 小时会自动检查更新并下载可用于当前基础结构和产品版本的新更新，使其在 Configuration Manager 控制台中可用。  

-   在“脱机模式”下，服务连接点不会连接到 Microsoft 云服务，因此必须手动[使用 System Center Configuration Manager 的服务连接工具](../../../../core/servers/manage/use-the-service-connection-tool.md)导入可用更新。  

安装了服务连接点之后在联机或脱机模式之间进行更改时，随后必须首先重新启动 Configuration Manager SMS_Executive 服务的 SMS_DMP_DOWNLOADER 线程，此更改才会生效。 为此，请使用 Configuration Manager 服务管理器仅重新启动 SMS_Executive 服务的 SMS_DMP_DOWNLOADER 线程。 还可以为 Configuration Manager 重新启动 SMS_Executive 服务（这会重新启动大多数站点组件），或等待诸如站点备份这类计划任务（它会停止，然后稍后会为你重新启动 SMS_Executive 服务）。  

若要使用 Configuration Manager 服务管理器，请在控制台中转至“监视” > “系统状态” > “组件状态”，选择“启动”，然后选择“Configuration Manager 服务管理器”。 在服务管理器中：  

-   在导航窗格中，依次展开站点和“组件”，然后选择要重新启动的组件。  

-   在细节窗格中，右键单击该组件，然后选择“查询”。  

-   确认该组件的状态之后，再次右键单击该组件，选择“停止”。  

-   再次“查询”该组件，以确认它已停止，然后再一次右键单击该组件，并选择“启动”。  

> [!IMPORTANT]  
>  将 Microsoft Intune 订阅添加到服务连接点的过程会自动将站点系统角色设置为联机状态。 使用 Intune 订阅进行设置时，服务连接点不支持脱机模式。  

**当角色安装在远离站点服务器的计算机上：**  

-   站点服务器的计算机帐户必须是承载远程服务连接的计算机上的本地管理员。

-   必须设置承载具有站点系统安装帐户的角色的站点系统服务器。  

-   站点服务器上的分发管理器使用该站点系统安装帐户来传输服务连接点的更新。

##  <a name="bkmk_urls"></a> Internet 访问要求  
若要启用操作，托管服务连接点的计算机以及该计算机与 Internet 之间的任何防火墙必须通过**端口 TCP 443** 和**端口 TCP 443** 与以下 Internet 位置进行通信。 服务连接点也支持使用 Web 代理（具有或不具有身份验证皆可）来使用这些位置。  如果需要配置 Web 代理帐户，请参阅：[System Center Configuration Manager 中的代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。

**更新和维护服务**  

-   *.akamaiedge.net  

-   *.akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10 维护服务**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>安装服务连接点
运行“安装程序”以安装层次结构的顶层站点时，可以选择安装服务连接点。

安装程序运行后，或者重新安装站点系统角色时，请使用“添加站点系统角色”向导或“创建站点系统服务器”向导，以在位于层次结构顶层站点（管理中心站点或独立主站点）的服务器上安装站点系统。 这两个向导都位于控制台的“主页”选项卡中的“管理” > “站点配置” > “服务器和站点系统角色”上。

## <a name="log-files-used-by-the-service-connection-point"></a>供服务连接点使用的日志文件
若要查看有关 Microsoft 上传的信息，请参阅运行服务连接点的计算机上的 **Dmpuploader.log**。  有关下载，包括更新的下载进度，请参阅 **Dmpdownloader.log**。 有关与服务连接点相关的日志的完整列表，请参阅 Configuration Manager 日志文件主题中的[服务连接点](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog)。

还可以使用以下流程图了解有关更新下载和更新到其他网站的复制的过程流和关键日志条目：
 - [流程图 - 下载更新](/sccm/core/servers/manage/download-updates-flowchart)
 - [流程图 - 更新复制](/sccm/core/servers/manage/update-replication-flowchart)
