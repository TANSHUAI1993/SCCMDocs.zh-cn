---
title: "预发行功能 | Microsoft Docs"
description: "System Center Configuration Manager 中的预发行功能"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: "36"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7b594daeed81ef2d991ad06489f9184a69804117
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的预发行功能
*适用范围：System Center Configuration Manager (Current Branch)*

预发行功能是指 Current Branch 中的功能，用于在生产环境中的早期测试。 这些功能完全受支持，但仍在开发过程中，所以在从预发行类别中划出之前，可能会有所变更。

 若要使用预发行功能，必须在 Configuration Manager 控制台中同意使用预发行功能，然后才可选择并启用它们。  

同意是对每个层次结构执行的一次性操作，不能撤消。 除非你同意，否则不能启用更新随附的新的预发行功能。 启用预发行功能后，将无法关闭。

若要同意，请在控制台中转到“管理” > “站点配置” > “站点”，然后选择“层次结构设置”。 在“常规”选项卡上，选择“同意使用预发行功能”。

 > [!NOTE]
 > 如果在安装较新版本更新之前启用了更新 1602 的预发行功能，即使不同意使用预发行功能，也可使用这些功能。

安装包含预发行功能的更新时，这些功能和此次更新包含的常规功能在“更新与维护服务向导”中可见：
  - **如果同意：** 安装更新时，可以启用更新和维护向导中的预发行功能。 为此，请选择预发行功能，就像选择任何其他功能那样。     

    也可以之后从控制台的“管理” > “更新和服务” > “功能”节点启用预发行功能。 在“功能”节点选择该功能，然后选择“开启”。 除非用户同意，否则此选项为灰显。 （在版本 1702 之前，“更新和服务”在“管理” > “云服务”下。）
  -   **如果不同意：**安装更新时，预发行功能在“更新和服务向导”中可见，但将灰显且不能启用。 安装更新后，可以在“功能”节点中查看这些功能。 但是，在“层次结构设置”中同意后才能启用它们。

如果在独立主站点中同意这样做，并通过安装新的管理中心站点扩展层次结构，则还必须在管理中心站点也同意这样做。

 启用预发行功能时，配置管理器层次结构管理器 (HMAN) 必须在该功能可用之前处理更改。 更改的处理通常是即时的，但根据 HMAN 处理周期，最长需要 30 分钟才能完成。 处理更改后，必须重新启动控制台，然后才能查看与该功能相关的新 UI。

**可以使用以下预发行功能：**

 |功能          |添加为预发行功能 | 添加为完整版功能|  
|------------------|---------------------|---------------------|
| 从 Configuration Manager 控制台创建并运行 PowerShell 脚本 |  [版本 1706](/sccm/apps/deploy-use/create-deploy-scripts)|![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 使用 Configuration Manager 进行 Device Guard 管理 |  [版本 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 在安装应用程序之前检查运行的可执行文件  |   [版本 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 数据仓库服务点  |  [版本 1702](/sccm/core/servers/manage/data-warehouse) |[版本 1706](/sccm/core/servers/manage/data-warehouse)|
| 用于向客户端进行内容分发的对等缓存 |  [版本 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 云管理网关 |  [版本 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 客户端数据源仪表板 |  [版本 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite 连接器  | [版本 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 维护群集感知集合（为服务器组提供服务）| [版本 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|对由 System Center Configuration Manager 管理的电脑进行条件访问 | [版本 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [版本 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |
