---
title: "预发行功能 | Microsoft Docs"
description: "System Center Configuration Manager 中的预发行功能"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: c164ae7ca17a3a7d96b010f41b5ecf72ab34976b
ms.lasthandoff: 03/04/2017


---
# <a name="pre-release-feaures-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的预发行功能
*适用范围：System Center Configuration Manager (Current Branch)*

 预发行功能是指 Current Branch 中随附的功能，用于在生产环境中的早期测试。 这些功能不应被视为可进行生产，但可以在生产环境中使用。

 若要使用预发行功能，必须在 Configuration Manager 控制台中同意使用预发行功能，然后才可选择并启用它们。  

同意是对每个层次结构执行的一次性操作，不能撤消。 除非你同意，否则不能启用更新随附的新的预发行功能。

若要同意，请在控制台中转到“管理” > “站点配置” > “站点”，然后选择“层次结构设置”。 在“常规”选项卡上，选择“同意使用预发行功能”。

 > [!NOTE]
 > 如果之前启用了更新 1602 的预发行功能，在安装较新版本更新之前，即使不同意使用预发行功能，也可使用这些功能。

安装包含预发行功能的更新时，这些功能和此次更新包含的常规功能在“更新与维护服务向导”中可见：
  - **如果同意：** 安装更新时，可以启用更新和维护向导中的预发行功能。 为此，请选择预发行功能，就像选择任何其他功能那样。     

    也可以之后从控制台的“管理” > “云服务” > “更新和维护服务” > “功能”节点启用预发行功能。 在“功能”节点选择该功能，然后选择“开启”。 （除非用户同意，否则此选项为灰显。）  
  -   **如果不同意：**安装更新时，预发行功能在“更新与维护服务向导”中可见，但将灰显且不能启用。 安装更新之后，可以在“功能”节点中查看这些功能，但在“层次结构设置”中同意这样做之前不能启用它们。

如果在独立主站点中同意这样做，并通过安装新的管理中心站点扩展层次结构，则还必须在管理中心站点也同意这样做。

**可以使用以下预发行功能：**

 |功能          |添加为预发行功能 | 添加为完整版功能|  
|------------------|---------------------|---------------------|
| 数据仓库服务点  |  [版本 1702](/sccm/core/servers/manage/data-warehouse) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 用于向客户端进行内容分发的对等缓存 |  [版本 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 云管理网关 |  [版本 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 客户端数据源仪表板 |  [版本 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite 连接器  | [版本 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| 维护群集感知集合（为服务器组提供服务）| [版本 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|对由 System Center Configuration Manager 管理的电脑进行条件访问 | [版本 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![尚未发行](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |

