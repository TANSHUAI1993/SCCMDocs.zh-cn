---
title: 如何使用资源浏览器
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的资源浏览器来查看硬件清单。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc4958e83c73da91aa31fb8ac0e1b84375218ac9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128198"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>如何使用 Configuration Manager 中的资源浏览器来查看硬件清单

适用范围：System Center Configuration Manager (Current Branch)

使用 Configuration Manager 中的资源浏览器查看有关硬件清单的信息。 该站点从层次结构中的客户端收集此信息。  

> [!Tip]  
>  在要连接的客户端上运行硬件清单周期之前，资源浏览器不会显示任何数据。  



## <a name="overview"></a>概述

资源浏览器具有与硬件清单相关的以下部分：  

- **硬件**：显示从指定客户端设备收集的最新硬件清单。  

    - “工作站状态”节点显示设备中最新硬件清单的时间和日期。  

- **硬件历史记录**：自上次硬件清单周期以来已更改的清单项的历史记录。  

    - 展开项可查看“当前”节点以及具有历史日期的一个或多个节点。 将当前节点中的信息与某个历史节点比较，以查看更改的项。  

> [!NOTE]  
> 默认情况下，Configuration Manager 删除已处于非活动状态 90 天的硬件清单数据。 在“删除过期的清单历史记录”站点维护任务中调整此天数。 有关详细信息，请参阅[维护任务](/sccm/core/servers/manage/maintenance-tasks)。  



## <a name="bkmk_open"></a> 如何打开资源浏览器   

1.  在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”节点。 还可以在“设备集合”节点中选择任何集合。  

2.  选择设备。 在功能区的“开始”选项卡和“设备”组中，单击“开始”，然后选择“资源浏览器”。   

> [!Tip]  
> 在资源浏览器中，右键单击右侧结果窗格中的项以执行其他操作。 单击“属性”，以不同格式查看该项目。  



## <a name="bkmk_bigint"></a> 大整数值的用法
<!--1357880--> 在 Configuration Manager 版本 1802 及更早版本中，硬件清单对大于 4,294,967,296 (2^32) 的整数有限制。 对于诸如以字节为单位的硬盘大小之类的属性，可以达到此限制。 管理点不会处理超过此限制的整数值，因此数据库中不会存储任何值。 

从版本 1806 开始，此限制增加到 18,446,744,073,709,551,616 (2^64)。 

对于值不变的属性（如总磁盘大小），可能在升级站点后不会立即看到值。 大多数硬件清单为增量报表。 客户端仅发送更改的值。 若要解决此行为，请将另一个属性添加到同一个类。 此操作会导致客户端更新已更改类中的所有属性。 



## <a name="see-also"></a>另请参阅

有关如何在运行 Linux 和 UNIX 的客户端查看硬件清单的信息，请参阅 [如何监视 Linux 和 UNIX 服务器的客户端](/sccm/core/clients/manage/monitor-clients-for-linux-and-unix-servers)。  

资源浏览器还显示软件清单。 有关详细信息，请参阅[如何使用资源浏览器来查看软件清单](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory)。
