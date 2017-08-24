---
title: "1602 的清单 | Microsoft Docs"
description: "了解从 System Center Configuration Manager 版本 1511 更新为版本 1602 之前需要执行的操作。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
caps.latest.revision: "13"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3e0de56b7a592b105e6a61b3d6654b1d0142584d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 安装更新 1602 的清单

*适用范围：System Center Configuration Manager (Current Branch)*

从 System Center Configuration Manager 版本 1511 更新为版本 1602 之前，请查看以下信息和清单以了解在开始更新之前要执行的操作。  

 **关于安装更新 1602：**  

 只能在层次结构的顶层站点上安装更新 1602。 这意味着你需要从管理中心站点（如果有）或从独立主站点启动安装。  

-   管理中心站点完成更新安装之后，子主站点会自动安装更新。 可以使用维护时段控制站点安装更新的时间。 从 1602 更新发布开始，维护时段重命名为服务时段。 有关详细信息，请参阅[站点服务器的服务时段](/sccm/core/servers/manage/service-windows)。  

-   在主父站点完成更新安装之后，必须从 Configuration Manager 控制台中手动更新辅助站点。 不支持辅助站点服务器的自动更新。  

站点服务器安装更新时，站点服务器上安装的站点系统角色和远程计算机上安装的那些角色会自动更新。 因此，安装更新之前，请确保每个站点系统服务器满足使用新更新版本进行操作的任何新的先决条件。  

更新完成后首次使用 Configuration Manager 控制台时，系统会提示更新该控制台。 为此，必须在承载该控制台的计算机上运行 Configuration Manager 安装程序，并选择用于更新该控制台的选项。 我们建议不要延迟将更新安装到该控制台。  

 **清单：**  

 **确保所有站点都运行支持的 System Center Configuration Manager 版本：**层次结构中的每个站点服务器都必须运行 System Center Configuration Manager 版本 1511，然后才能开始安装更新 1602。  

 **查看站点系统服务器上安装的 Microsoft.NET 版本：**站点安装更新 1602 时，如果尚未安装 .NET Framework 4.5 或更高版本，则 Configuration Manager 会在承载以下站点系统角色之一的每台计算机上自动安装 .NET Framework 4.5.2：  

-   注册代理点  

-   注册点  

-   管理点  

-   服务连接点  

此安装可以将站点系统服务器置于重启挂起状态，并向 Configuration Manager 组件状态查看器报告错误。 此外，服务器上的 .NET 应用程序可能会遇到随机故障，直到重启服务器。  

 有关详细信息，请参阅[站点和站点系统先决条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

 **查看站点和层次结构状态，并确认没有未解决的问题：** 更新站点之前，请解决远程计算机上安装的站点服务器、站点数据库服务器和站点系统角色的所有操作问题。 由于现有的操作问题，站点更新可能会失败。  

有关详细信息，请参阅 [使用 System Center Configuration Manager 的警报和状态系统](../../../core/servers/manage/use-alerts-and-the-status-system.md)。  

 **查看站点之间的文件和数据复制：**  确保站点之间的文件和数据库复制正常运行并且处于最新状态。 延迟或积压工作可能会阻止顺利、成功更新。    

对于数据库复制，可以在开始更新之前，使用复制链接分析器来帮助解决问题。    

 有关详细信息，请参阅 [System Center Configuration Manager 中的监视层次结构和复制基础结构](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md)主题中的[关于复制链接分析器](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)。  

 **为承载站点、站点数据库服务器和远程站点系统角色的计算机上的操作系统安装所有合适的关键更新：**为 Configuration Manager 安装更新之前，请为每个适用的站点系统安装任何关键更新。 如果安装的更新需要重启，请在开始升级之前重启合适的计算机。  

 **在主站点上禁用管理点数据库副本：**Configuration Manager 无法成功更新启用了管理点数据库副本的主站点。 禁用数据库复制，然后：  

-   创建站点数据库的备份以测试数据库升级。  

-   为 Configuration Manager 安装更新。  

有关详细信息，请参阅 [System Center Configuration Manager 管理点的数据库副本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

 **重新配置使用 NLB 的软件更新点：**Configuration Manager 无法更新使用网络负载平衡 (NLB) 群集来承载软件更新点的站点。  如果为软件更新点使用 NLB 群集，请使用 Windows PowerShell 删除 NLB 群集。    

 有关详细信息，请参阅 [System Center Configuration Manager 的软件更新计划](../../../sum/plan-design/plan-for-software-updates.md)。  

 **在站点上的更新安装过程中，禁用每个站点上的所有站点维护任务：**安装更新之前，请禁用可能会在升级过程进行时运行的任何站点维护任务。 这些任务包括（但不限于）以下：  

-   备份站点服务器  

-   删除过期的客户端操作  

-   删除过期的发现数据  

站点数据库维护任务在更新安装过程中运行时，更新安装可能会失败。 在禁用任务之前，请记录该任务的计划，以便可以在安装更新之后恢复其配置。  

 有关详细信息，请参阅 [System Center Configuration Manager 的维护任务](../../../core/servers/manage/maintenance-tasks.md)和 [System Center Configuration Manager 维护任务参考](../../../core/servers/manage/reference-for-maintenance-tasks.md)。  

 **在管理中心站点和主站点上创建站点数据库备份：**更新站点之前，请备份站点数据库，以确保具有用于灾难恢复的成功备份。   

有关详细信息，请参阅 [System Center Configuration Manager 的备份和恢复](../../../protect/understand/backup-and-recovery.md)。  

 **备份自定义 Configuration.mof 文件：**如果使用自定义 Configuration.mof 文件定义与硬件清单一起使用的数据类，则在更新站点之前创建此文件的备份。 更新之后，将此文件还原到版本 1602 站点。 更新站点时，当前文件会覆盖为文件的原始（默认值）版本。 有关使用此文件的详细信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

 **在最近的站点数据库备份副本上测试数据库升级：**更新 System Center Configuration Manager 管理中心站点或主站点之前，请在站点数据库副本上测试站点数据库升级过程。  

-   应该对站点数据库升级过程进行测试，因为在升级站点时，站点数据库可能会被修改。  

-   虽然测试数据库升级不是必需的，但它可以在生产数据库受到影响之前先行识别升级的问题。  

-   失败的站点数据库升级可能会使站点数据库无法运行，并且可能需要进行站点恢复以还原功能。  

-   虽然在层次结构的站点之间共享了站点数据库，但是，请在升级每个合适的站点之前计划在该站点上测试数据库。  

-   如果在主站点上对管理点使用数据库副本，请在创建站点数据库备份之前禁用复制。  

Configuration Manager 不支持辅助站点备份，也不支持辅助站点数据库的测试升级。   
请勿在生产站点数据库上运行测试数据库升级。 执行此任务会升级站点数据库，并可能导致你的站点无法运行。 有关详细信息，请参阅**安装控制台内部更新前**中的[步骤 2：在安装更新前测试数据库升级](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2)。  

 **规划客户端试点：**安装更新客户端的更新后，可以在新的客户端更新部署和升级所有活动的客户端之前在预生产中对其进行测试。   

 若要利用此选项，在开始安装更新之前必须配置站点，以支持预生产的自动升级。 有关详细信息，请参阅[在 System Center Configuration Manager 中升级客户端](../../../core/clients/manage/upgrade/upgrade-clients.md)和   
[如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

 **计划使用维护时段控制站点服务器安装更新的时间：**可以使用维护时段定义一个时间段，在此时间段可安装该站点的更新。 这可以帮助你控制层次结构中的站点安装更新的时间。   

从 1602 更新发布开始，维护时段重命名为服务时段。 有关详细信息，请参阅[站点服务器的服务时段](/sccm/core/servers/manage/service-windows)。  

 **运行安装程序先决条件检查程序：**安装更新 1602 之前，可以独立于更新安装来运行先决条件检查程序。 在站点上安装更新时，会再次运行必备组件检查程序。  

有关详细信息，请参阅 [System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)主题中的**步骤 3：安装更新之前运行先决条件检查程序**。  

> [!IMPORTANT]  
>  必备组件检查程序作为更新安装的一部分运行或独立运行时，该过程会更新某些用于站点维护任务的产品源文件。 因此，在运行先决条件检查程序之后且安装 1602 更新之前，如果需要执行站点维护任务，可从站点服务器上的 CD.Latest 文件夹运行 **Setupwfe.exe**（Configuration Manager 安装程序）。  

 **更新站点：** 现已准备好可以为层次结构开始更新安装。 我们建议计划在正常业务时间之外为每个站点安装更新，此时安装更新的过程以及其重新安装站点组件和站点系统角色的操作对业务运营的影响最小。

有关详细信息，请参阅 [ System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)。  

## <a name="see-also"></a>另请参阅  
 [System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)
