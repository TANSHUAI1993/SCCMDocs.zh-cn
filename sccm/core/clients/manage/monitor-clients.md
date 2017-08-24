---
title: "监视客户端 - Configuration Manager | Microsoft Docs"
description: "了解有关如何在 System Center Configuration Manager 中监视客户端的详细指南。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: "23"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 08a4d9b29871b49e3118aef949572cef64940f96
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中监视客户端

*适用范围：System Center Configuration Manager (Current Branch)*


 在站点中的 Windows 计算机和设备上安装 System Center Configuration Manager 客户端应用程序后，即可在 Configuration Manager 控制台中监视其运行状况和活动。  

##  <a name="bkmk_about"></a> 关于客户端状态  
 Configuration Manager 提供以下类型的信息作为客户端状态：  

-   **客户端联机状态** - 从 Configuration Manager 1602 版开始，此状态可指示计算机是否处于联机状态。 如果计算机连接到其已分配的管理点，则将其视为联机。  为指示客户端处于联机状态，它将向管理点发送类似 ping 的消息。 如果管理点在 5 分钟左右未收到消息，则将客户端视为处于脱机状态。  

-   **客户端活动** - 此状态将指示客户端是否在最近 7 天内主动使用 Configuration Manager。 如果客户端在 7 天内未请求策略更新、发送检测信号消息或发送硬件清单，则将客户端视为非活动状态。  

-   **客户端检查** - 此状态将指示计算机上运行的 Configuration Manager 客户端的定期评估是否成功。  评估将检查计算机状态，并修正所发现的某些问题。 有关详细信息，请参阅 [客户端检查进行的检查和修正](#BKMK_ClientHealth)。  

     在运行 Windows 7 的计算机上，客户端检查将作为计划任务运行。 在更高版本的操作系统上，客户端检查将在 Windows 维护时段自动运行。  

     你可以将修正配置为不在特定计算机（例如关键业务服务器）上运行。 此外，如果想要评估其他项，则可以使用 Configuration Manager 符合性设置提供全面的解决方案，以监视组织中计算机的总体健康状况、活动和符合性。 有关符合性设置的详细信息，请参阅[在 System Center Configuration Manager 中规划和配置符合性设置](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

##  <a name="bkmk_indStatus"></a> 监视单个客户端的状态  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “设备”或者在“设备集合”下选择一个集合。  

     从 Configuration Manager 1602 版开始，每行开头的图标将指示设备的联机状态：  

    |||  
    |-|-|  
    |![客户端的联机状态图标](../../../core/clients/manage/media/online-status-icon.png)|设备处于联机状态。|  
    |![客户端的脱机状态图标](../../../core/clients/manage/media/offline-status-icon.png)|设备处于脱机状态。|  
    |![客户端的未知状态图标](../../../core/clients/manage/media/unknown-status-icon.png)|联机状态未知。|  
    |![未安装客户端](../../../core/clients/manage/media/client-not-installed.png)|设备上未安装客户端。|  

2.  若要查看更详细的联机状态，可以通过右键单击列标题，然后单击你想添加的联机状态字段，将客户端联机状态信息添加到设备视图。 可以添加的列如下  

    -   **设备联机状态** 将指示客户端当前是联机还是脱机。 （与图标表示的信息相同）。  

    -   **上次联机时间** 表示客户端联机状态更改为联机时的时间。  

    -   **上次脱机时间** 表示状态更改为脱机时的时间。  

3.  单击列表窗格中的单个客户端可以在详细信息窗格中查看更多状态，包括有关客户端活动和客户端检查的信息。  

##  <a name="bkmk_allStatus"></a> 监视所有客户端的状态  

1.  在 Configuration Manager 控制台中，单击“监视” > “客户端状态”。 在控制台的此页面中，可查看整个站点内客户端活动和客户端检查的总体统计信息。  还可通过选择不同的集合来更改信息的范围。  

2.  若要深入探究所报告统计信息的详细信息，请单击所报告信息的名称（例如**已通过客户端检查或无结果的活动客户端**）并查看有关该客户端的信息。  

3.  单击“客户端活动”以查看对 Configuration Manager 站点中客户端活动进行描述的图表。  

4.  单击“客户端检查”以查看对 Configuration Manager 站点中客户端检查的状态进行描述的图表。  

 你可以将警报配置为在以下情况下通知你：客户端检查结果或客户端活跃状况低于集合中客户端的指定百分比，或者修正针对指定百分比的客户端失败。 有关如何配置客户端状态的信息，请参阅[如何在 System Center Configuration Manager 中配置客户端状态](../../../core/clients/deploy/configure-client-status.md)。  

##  <a name="BKMK_ClientHealth"></a> 客户端检查进行的检查和修正  
 客户端检查可以执行以下检查和修正。  

|客户端检查|修正操作|更多信息|  
|------------------|------------------------|----------------------|  
|验证最近是否运行了客户端检查|运行客户端检查|检查在过去三天中是否至少运行了一次客户端检查。|  
|验证是否已安装客户端必备组件|安装客户端必备组件|检查是否安装了客户端必备组件。 阅读客户端安装文件夹中的 ccmsetup.xml 文件以发现必备组件。|  
|WMI 存储库完整性测试|重新安装 Configuration Manager 客户端|检查 WMI 中是否存在 Configuration Manager 客户端条目。|  
|验证客户端服务是否正在运行|启动客户端（SMS 代理主机）服务|无更多信息|  
|WMI 事件接收器测试。|重新启动客户端服务|检查与 Configuration Manager 相关的 WMI 事件接收器是否丢失|  
|验证 Windows Management Instrumentation (WMI) 服务是否存在|无修正|无更多信息|  
|验证是否正确安装了客户端|重新安装客户端|无更多信息|  
|WMI 存储库读取和写入测试|重新启动 WMI 存储库，然后重新安装 Configuration Manager 客户端|仅在运行 Windows Server 2003、Windows XP（64 位）或更早版本的计算机上执行此客户端检查的修正。|  
|验证反恶意软件服务的启动类型是否为自动|将服务启动类型重置为自动|无更多信息|  
|验证反恶意软件服务是否正在运行|启动反恶意软件服务|无更多信息|  
|验证 Windows 更新服务启动类型是自动还是手动|将服务启动类型重置为自动|无更多信息|  
|验证客户端服务（SMS 代理主机）启动类型是否为自动|将服务启动类型重置为自动|无更多信息|  
|验证 Windows Management Instrumentation (WMI) 服务是否正在运行。|启动 Windows Management Instrumentation 服务|无更多信息|  
|验证 Microsoft SQL CE 数据库是否正常|重新安装 Configuration Manager 客户端|无更多信息|  
|Microsoft 策略平台 WMI 完整性测试|修复 Microsoft 策略平台|无更多信息|  
|验证 Microsoft 策略平台服务是否存在|修复 Microsoft 策略平台|无更多信息|  
|验证 Microsoft 策略平台服务启动类型是否为手动|将服务启动类型重置为手动|无更多信息|  
|验证是否存在后台智能传输服务|无修正|无更多信息|  
|验证后台智能传输服务启动类型是自动还是手动|将服务启动类型重置为自动|无更多信息|  
|验证网络检查服务启动类型是否为手动|将服务（如果已安装）启动类型重置为手动|无更多信息|  
|验证 Windows Management Instrumentation (WMI) 服务启动类型是否为自动|将服务启动类型重置为自动|无更多信息|  
|验证 Windows 8 计算机上的 Windows 更新服务启动类型是自动还是手动|将服务启动类型重置为手动|无更多信息|  
|请验证客户端（SMS 代理主机）服务是否存在。|无修正|无更多信息|  
|验证 Configuration Manager 远程控制服务启动类型是自动还是手动|将服务启动类型重置为自动|无更多信息|  
|验证 Configuration Manager 远程控制服务是否正在运行|启动远程控制服务|无更多信息|  
|验证客户端 WMI 提供程序是否正常|重新启动 Windows Management Instrumentation 服务|仅在运行 Windows Server 2003、Windows XP（64 位）或更早版本的计算机上执行此客户端检查的修正。|  
|验证唤醒代理服务（ConfigMgr 唤醒代理）是否正在运行|启动 ConfigMgr 唤醒代理服务|仅当“电源管理” 时进行此客户端检查：在受支持的客户端操作系统上，将“启用唤醒代理”  客户端设置设置为“是”  。|  
|验证唤醒代理服务（ConfigMgr 唤醒代理）启动类型是否为自动|将 ConfigMgr 唤醒代理服务启动类型重置为自动|仅当“电源管理” 时进行此客户端检查：在受支持的客户端操作系统上，将“启用唤醒代理”  客户端设置设置为“是”  。|  

## <a name="client-deployment-log-files"></a>客户端部署日志文件
有关客户端部署和管理操作使用的日志文件的信息，请参阅 [System Center Configuration Manager 中的日志文件](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)。
