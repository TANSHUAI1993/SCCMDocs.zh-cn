---
title: 服务连接点
titleSuffix: Configuration Manager
description: 了解此 Configuration Manager 站点系统角色，并了解和规划其使用范围。
ms.date: 08/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f1173a8bec0ab05c3519d04430adddab129389b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499113"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>关于 Configuration Manager 中的服务连接点

适用范围：System Center Configuration Manager (Current Branch)

服务连接点是一个站点系统角色，为层次结构提供几个重要的功能。 设置服务连接点之前，需了解和规划它的使用范围。 规划使用可能会影响设置此站点系统角色的方式：  

- **使用 Microsoft Intune 管理移动设备**：此角色替换此前版本的 Configuration Manager 使用的 Windows Intune 连接器，并可通过 Intune 订阅详细信息进行配置。 有关详细信息，请参阅[混合移动设备管理 (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management)。  

- **使用本地 MDM 管理移动设备**：此角色为你所管理的未连接到 Internet 的本地设备提供支持。 有关详细信息，请参阅[使用本地基础结构管理移动设备](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)。  

- **从 Configuration Manager 基础结构上传使用情况数据**：可以控制上传的详细信息的级别或数量。 上传的数据有助于：  

    - 主动识别和排除问题  

    - 改进我们的产品和服务  

    - 确定适用于你所使用的 Configuration Manager 版本的 Configuration Manager 更新  

    有关各级别收集的数据，以及安装角色后如何更改收集级别的详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。 然后跟踪你所用 Configuration Manage 版本的链接。  

    有关详细信息，请参阅[使用情况数据级别和设置](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage)。  

- **下载适用于 Configuration Manager 基础结构的更新**：基于所上传的使用情况数据，仅适用于基础结构的相关更新可用。  

- **每个层次结构支持此角色的单一实例**：  

    - 此站点系统角色只能安装在层次结构的顶层站点上，即管理中心站点或独立主站点。  

    - 如果将独立主站点扩展到更大的层次结构，则必须从主站点中卸载此角色，然后才可将其安装在管理中心站点上。  


##  <a name="bkmk_modes"></a>操作模式  
服务连接点支持两种操作模式：  

- 在联机模式下，服务连接点每 24 小时自动检查一次是否有更新。 它会自动下载可用于当前基础结构和产品版本的更新，使其在 Configuration Manager 控制台中可用。  

- 在“脱机模式”下，服务连接点不会连接到 Microsoft 云服务。 要手动导入可用更新，请使用[服务连接工具](/sccm/core/servers/manage/use-the-service-connection-tool)。  

安装了服务连接点之后，如果在联机或脱机模式之间进行更改，必须首先重新启动 Configuration Manager SMS_Executive 服务的 SMS_DMP_DOWNLOADER 线程，此更改才会生效。 可使用 Configuration Manager 服务管理器仅重新启动 SMS_Executive 服务的 SMS_DMP_DOWNLOADER 线程。 也可以重新启动 Configuration Manager 的 SMS_Executive 服务，从而重新启动大多数站点组件。 或者可以等待计划任务（如站点备份）停止，然后为你重新启动 SMS_Executive 服务。  

若要使用 Configuration Manager 服务管理器，请在控制台中转至“监视” > “系统状态” > “组件状态”，选择“启动”，然后选择“Configuration Manager 服务管理器”。 在服务管理器中：  

- 在导航窗格中，依次展开站点和“组件”，然后选择要重新启动的组件。  

- 在细节窗格中，右键单击该组件，然后选择“查询”。  

- 确认该组件的状态之后，再次右键单击该组件，选择“停止”。  

- 再次查询组件，确认它已停止。 再次右键单击该组件，然后选择“开始”。  

> [!IMPORTANT]  
> 将 Microsoft Intune 订阅添加到服务连接点的过程会自动将站点系统角色设置为联机状态。 使用 Intune 订阅进行设置时，服务连接点不支持脱机模式。  

**当角色安装在远离站点服务器的计算机上：**  

- 站点服务器的计算机帐户必须是承载远程服务连接的计算机上的本地管理员。

- 必须设置承载具有站点系统安装帐户的角色的站点系统服务器。  

- 站点服务器上的分发管理器使用该站点系统安装帐户来传输服务连接点的更新。

##  <a name="bkmk_urls"></a> Internet 访问要求  
若要启用操作，托管服务连接点的计算机以及该计算机与 Internet 之间的任何防火墙必须通过 HTTPS 的传出端口“TCP 443”和 HTTP 的传出端口“TCP 80”与以下 Internet 位置传递通信。 服务连接点也支持使用 Web 代理（具有或不具有身份验证皆可）来使用这些位置。 如果需要配置 Web 代理帐户，请参阅：[代理服务器支持](/sccm/core/plan-design/network/proxy-server-support)。

> [!TIP]  
> 服务连接点在连接到 go.microsoft.com 或 manage.Microsoft.com 时使用 Microsoft Intune 服务。 存在以下已知问题：如果未在服务连接点上安装 Baltimore CyberTrust 根证书、该证书已过期或损坏，则 Intune 连接器会遇到连接问题。 有关详细信息，请参阅 [服务连接点不下载更新](https://support.microsoft.com/help/3187516)。  

#### <a name="updates-and-servicing"></a>更新和服务

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

#### <a name="microsoft-intune"></a>Microsoft Intune

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

#### <a name="windows-10-servicing"></a>Windows 10 维护服务

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

#### <a name="azure-services"></a>Azure 服务

- `management.azure.com`  

## <a name="install-the-service-connection-point"></a>安装服务连接点
运行“安装程序”以安装层次结构的顶层站点时，可以选择安装服务连接点。

安装程序运行后，或者重新安装站点系统角色时，请使用“添加站点系统角色”向导或“创建站点系统服务器”向导，以在位于层次结构顶层站点（管理中心站点或独立主站点）的服务器上安装站点系统。 这两个向导都位于控制台的“主页”选项卡中的“管理” > “站点配置” > “服务器和站点系统角色”上。



## <a name="log-files-used-by-the-service-connection-point"></a>供服务连接点使用的日志文件
若要查看有关 Microsoft 上传的信息，请参阅运行服务连接点的计算机上的 **Dmpuploader.log**。  有关下载，包括更新的下载进度，请参阅 **Dmpdownloader.log**。 有关与服务连接点相关的日志的完整列表，请参阅 Configuration Manager 日志文件文章中的[服务连接点](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog)。

还可以使用以下流程图了解有关更新下载和更新到其他网站的复制的过程流和关键日志条目：
- [流程图 - 下载更新](/sccm/core/servers/manage/download-updates-flowchart)
- [流程图 - 更新复制](/sccm/core/servers/manage/update-replication-flowchart)
