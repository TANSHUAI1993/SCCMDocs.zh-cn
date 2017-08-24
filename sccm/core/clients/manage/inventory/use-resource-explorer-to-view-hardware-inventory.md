---
title: "查看硬件清单 | Microsoft Docs | 资源浏览器"
description: "使用资源浏览器查看 System Center Configuration Manager 中的硬件清单。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: "7"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>如何使用资源浏览器来查看 System Center Configuration Manager 中的硬件清单

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的资源浏览器查看从层次结构中的客户端收集的硬件清单的相关信息。  

> [!NOTE]  
>  资源浏览器不会显示数据的硬件清单周期已在运行之前客户端上您要连接到任何库存量。  

 资源浏览器具有与硬件清单相关的以下部分：  

-   **硬件** - 包含从指定客户端设备收集的最新的硬件清单。  **工作站状态**具有设备上次执行硬件清单的日期和时间。  

-   **硬件历史记录** - 包含自上次执行硬件清单以来已更改的清单项的历史记录。 每项都包含一个“当前”节点以及一个或多个 *<date\>* 节点。 可以将当前节点中的信息与某个历史节点相比较，以查找已更改的项。  

    > [!NOTE]  
    >  Configuration Manager 会按“删除过期的清单历史记录”站点维护任务中指定的天数保留硬件清单历史记录  

> [!NOTE]  
>  若要了解如何在运行 Linux 和 UNIX 的客户端查看硬件清单，请参阅 [如何在 System Center Configuration Manager 中监视 Linux 和 UNIX 服务器的客户端](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md)。  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>如何从 Configuration Manager 控制台运行资源浏览器  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “设备”，或打开显示设备的任何集合。  

3.  选择包含想要查看的清单的计算机，然后在“主页”选项卡 >“设备”组中，选择“启动” >  “资源浏览器”。   

4.  右键单击“资源浏览器”窗口右窗格中的任意项，然后选择“属性”以打开 *<item name\>*“属性”对话框，以可读性更强的格式查看收集的清单信息。  

