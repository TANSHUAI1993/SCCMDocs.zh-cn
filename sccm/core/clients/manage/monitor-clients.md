---
title: 监视客户端
titleSuffix: Configuration Manager
description: 了解有关如何在 Configuration Manager 中监视客户端的详细指南
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5dadb6400ad76947ce7ace3228b6f7d95cedc17
ms.sourcegitcommit: 670cfed1e47a7a4a73aa4ccb873c6312be3c21ff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71311549"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>如何在 Configuration Manager 中监视客户端

适用范围：  System Center Configuration Manager (Current Branch)

在站点中的 Windows 设备上安装 Configuration Manager 客户端后，即可在 Configuration Manager 控制台中监视其运行状况和活动。  


## <a name="bkmk_about"></a> 关于客户端状态

Configuration Manager 提供以下类型的信息作为客户端状态：  

- **客户端联机状态**：如果计算机连接到其已分配的管理点，则站点将设备视为联机。  为指示客户端处于联机状态，它将向管理点发送类似 ping 的消息。 如果管理点在 5 分钟后未收到消息，则站点将客户端视为处于脱机状态。   

- **客户端活跃状况**：若客户端在过去的 7 天内曾与 Configuration Manager 通信，则站点将客户端视觉处于活跃状态。  若客户端在未来 7 天内未执行下面的操作，则站点将客户端视为处于非活动状态：   

    - 请求策略更新  
    - 发送检测信号消息  
    - 发送硬件清单  

- **客户端检查**：Configuration Manager 客户端在设备上运行的定期评估的状态。 评估将检查设备状态，并修正所发现的某些问题。 有关详细信息，请参阅[客户端运行状况检查](#BKMK_ClientHealth)。  

     在运行 Windows 7 的设备上，客户端检查将作为计划任务运行。 在更高版本的操作系统版本上，客户端检查将在 Windows 维护时段自动运行。  

     你可以将修正配置为不在特定设备（例如关键业务服务器）上运行。 若还想要评估其他项目，请使用 Configuration Manager 符合性设置来监视额外的配置。 有关符合性设置的详细信息，请参阅[规划和配置符合性设置](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings)。  

- **已停用**：站点已标记设备记录，以删除设备。 为同一个设备执行的新注册分配到了层次结构中的同一个或其他主站点时，会发生此行为。 站点再次运行站点维护任务“删除过期的发现数据”时，它将删除这些设备。 <!-- SCCMDocs issue #1418 -->  

- **已过时**：站点已发现同一个硬件 ID 的新设备记录，因此它将旧记录标记为“已过时”。 报告不会为同一个设备的过时记录多次计数。 你仍然可以使策略面向过时设备。 在过时记录保持 90 天的非活动状态后，如果站点未获得它的检测信号，则在站点运行站点维护任务“删除过时的客户端发现数据”时会将过时设备删除。 


## <a name="bkmk_indStatus"></a> 监视单个客户端

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。 选择“设备”节点，或从“设备集合”下选择一个集合。    

    每行开头的图标将指示设备的联机状态：  

    |||  
    |-|-|  
    |![客户端的联机状态图标](../../../core/clients/manage/media/online-status-icon.png)|设备处于联机状态|  
    |![客户端的脱机状态图标](../../../core/clients/manage/media/offline-status-icon.png)|设备处于脱机状态|  
    |![客户端的未知状态图标](../../../core/clients/manage/media/unknown-status-icon.png)|联机状态未知|  
    |![未安装客户端](../../../core/clients/manage/media/client-not-installed.png)|设备未安装客户端|  

2. 若要获得详细的联机状态，请将客户端联机状态信息添加到设备视图。 右键单击列标题，选择想要添加的联机状态字段：

    - **设备联机状态**：指示客户端当前是联机还是脱机。 （此状态与图标表示的信息相同。）  

    - **上次联机时间**：表示客户端联机状态更改为联机时的时间  

    - **上次脱机时间**：表示状态更改为脱机时的时间  

3. 从列表窗格选择单个客户端，从详细信息窗格查看详细状态。 此信息包括客户端活动和客户端检查状态。  


## <a name="bkmk_health"></a>客户端运行状况仪表板

<!--3599209-->
可部署软件更新和其他应用，以帮助保护环境，但这些部署只能到达正常运行的客户端。 运行不正常的 Configuration Manager 客户端会对总体符合性产生不利影响。 根据分母来确定客户端运行状况可能有难度：在管理范围内总共应该有多少设备？ 例如，如果发现 Active Directory 中的所有系统，即便部分记录用于已停用的计算机，但此过程仍会使分母增大。

从 1902 版开始，可在环境中查看具有 Configuration Manager 客户端运行状况信息的仪表板。 查看客户端运行状况、方案运行状况和常见错误。 按多个属性筛选视图，以查看按 OS 和客户端版本列出的所有潜在问题。

在 Configuration Manager 控制台中，转到“监视”  工作区。 展开“客户端状态”，然后选择“客户端运行状况仪表板”节点   。

![客户端运行状况仪表板屏幕截图](media/3599209-client-health-dashboard.png)

> [!Tip]  
> 没有对 ccmeval 的更改。  

默认情况下，客户端运行状况仪表板显示在线客户端和在过去三天内处于活动状态的客户端。 因此，你在此仪表板中看到的数字可能与其他客户端运行状况历史源中的数字不同。 例如，“客户端状态”  下的其他节点或客户端状态类别中的报表。

### <a name="filters"></a>筛选器

在仪表板的顶部，有一组筛选器，用于调整仪表板中显示的数据。

- **集合**：默认情况下，仪表板显示“所有系统”  集合中的设备。 从列表中选择设备集合，以将视图限定为特定集合中的设备子集。  

- **联机或脱机**：默认情况下，仪表板仅显示联机客户端。 此状态来自每五分钟更新一次客户端状态的客户端通知通道。 有关详细信息，请参阅[关于客户端状态](/sccm/core/clients/manage/monitor-clients#bkmk_about)。  

- **活动 \# 天数**：默认情况下，仪表板显示过去三天处于活动状态的客户端。  

- **仅限故障**：将视图限定为仅报告客户端运行状况为故障的设备。  

    > [!Tip]  
    > 将此筛选器与客户端版本和 OS 版本磁贴配合使用。 有关详细信息，请参阅[版本磁贴](#version-tiles)。

### <a name="client-health-percentage"></a>客户端运行状况百分比

此磁贴显示层次结构中总体的客户端运行状况。

运行正常的 Configuration Manager 客户端具有以下属性：

- Online  
- 主动发送数据  
- 传递所有客户端运行状况评估检查  

有关详细信息，请参阅[关于客户端状态](/sccm/core/clients/manage/monitor-clients#bkmk_about)。

运行正常的客户端可成功与站点通信。 它根据客户端设置中定义的计划报告所有数据。

选择此图表的一段，以深入了解设备列表视图。

### <a name="version-tiles"></a>版本磁贴

有两个磁贴按 Configuration Manager 客户端版本和 OS 版本显示客户端运行状况。 更改筛选器时（例如“仅限故障”），这些磁贴非常有用  。 它们可以帮助突出显示特定版本中的问题是否一致。 使用此信息来帮助你做出升级决策。

选择这些图表的一段，以深入了解设备列表视图。

### <a name="scenario-health"></a>方案运行状况

此条形图显示了以下核心方案的总体运行状况：

- 客户端策略
- 检测信号发现
- 硬件清单
- 软件清单
- 状态消息

使用选择器来调整图表中特定方案的重点。

以下两栏将始终显示：

- **组合(全部)** ：所有方案的组合 (AND)  
- **组合(任意)** ：至少一个方案 (OR)

> [!Tip]  
> 方案运行状况不会根据客户端设置的配置进行度量。 这些值可能会根据每个设备策略的结果集的不同而不同。 使用以下步骤调整方案运行状况评估周期：
>
> - 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“客户端状态”节点   。  
> - 在功能区中，选择“客户端状态设置”  。  
>
> 默认情况下，如果客户端在 7 天内未发送特定于方案的数据，则 Configuration Manager 会将此情况视为运行不正常  。

### <a name="top-10-client-health-failures"></a>最常见的 10 个“客户端运行状况”故障

此图表列出了环境中最常见的故障。 这些错误来自 Windows 或 Configuration Manager。

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="bkmk_allStatus"></a> 监视所有客户端的状态

1. 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“客户端状态”节点   。 查看整个站点内客户端活动和客户端检查的总体统计信息。 通过选择不同的集合来更改信息的范围。  

2. 若要向下钻取所报告的统计信息的详情，请选择所报告的信息的名称。 例如，“已通过客户端检查或没有关于它的任何结果的活动客户端”。  然后查看单个客户端的信息。  

3. 选择“客户端活动”  以查看对 Configuration Manager 站点中客户端活动进行描述的图表。  

4. 选择“客户端检查”  以查看对 Configuration Manager 站点中客户端检查的状态进行描述的图表。  

    配置警报，当客户端检查结果或客户端活动降至指定百分比以下时通知你。 此外，当修正在指定百分比的客户端上失败时，站点也可以向你发出通知。 有关详细信息，请参阅[如何配置客户端状态](/sccm/core/clients/deploy/configure-client-status)。  


## <a name="BKMK_ClientHealth"></a> 客户端运行状况检查

客户端检查运行以下检查和修正：  

|客户端检查|修正操作|更多信息|  
|------------------|------------------------|----------------------|  
|验证最近是否运行了客户端检查|运行客户端检查|检查在过去三天中是否至少运行了一次客户端检查。|  
|验证是否已安装客户端必备组件|安装客户端必备组件|检查是否安装了客户端必备组件。 阅读客户端安装文件夹中的 ccmsetup.xml 文件以发现必备组件。|  
|WMI 存储库完整性测试|重新安装 Configuration Manager 客户端|检查 WMI 中是否存在 Configuration Manager 客户端条目。|  
|验证客户端服务是否正在运行|启动客户端（SMS 代理主机）服务|无更多信息|  
|WMI 事件接收器测试。|重新启动客户端服务|检查与 Configuration Manager 相关的 WMI 事件接收器是否丢失|  
|验证 Windows Management Instrumentation (WMI) 服务是否存在|无修正|无更多信息|  
|验证是否正确安装了客户端|重新安装客户端|无更多信息|  
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
|验证 Windows 8 设备上的 Windows 更新服务启动类型是自动还是手动|将服务启动类型重置为手动|无更多信息|  
|请验证客户端（SMS 代理主机）服务是否存在。|无修正|无更多信息|  
|验证 Configuration Manager 远程控制服务启动类型是自动还是手动|将服务启动类型重置为自动|无更多信息|  
|验证 Configuration Manager 远程控制服务是否正在运行|启动远程控制服务|无更多信息|  
|验证唤醒代理服务（ConfigMgr 唤醒代理）是否正在运行|启动 ConfigMgr 唤醒代理服务|仅当“电源管理”时进行此客户端检查  ：在受支持的客户端操作系统上，将“启用唤醒代理”客户端设置设置为“是”   。|  
|验证唤醒代理服务（ConfigMgr 唤醒代理）启动类型是否为自动|将 ConfigMgr 唤醒代理服务启动类型重置为自动|仅当“电源管理”时进行此客户端检查  ：在受支持的客户端操作系统上，将“启用唤醒代理”客户端设置设置为“是”   。|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>客户端部署日志文件

有关客户端部署和管理操作使用的日志文件的详细信息，请参阅[日志文件](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)。
