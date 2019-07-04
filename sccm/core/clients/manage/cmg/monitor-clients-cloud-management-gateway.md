---
title: 监视云管理网关
titleSuffix: Configuration Manager
description: 通过云管理网关 (CMG) 监视客户端和网络流量。
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d184118e0e99231a9160322740ab7690488a28a5
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286769"
---
# <a name="monitor-cloud-management-gateway"></a>监视云管理网关

适用范围：  System Center Configuration Manager (Current Branch)

客户端通过正在运行的云管理网关 (CMG) 连接后，用户可以监视客户端与网络流量以确保了解该服务的执行方式。


## <a name="monitor-clients"></a>监视客户端

通过 CMG 连接的客户端采用与本地客户端相同的方式显示在 Configuration Manager 控制台中。 有关详细信息，请参阅[如何监视客户端](/sccm/core/clients/manage/monitor-clients)。


## <a name="monitor-traffic-in-the-console"></a>在控制台中监视流量

使用 Configuration Manager 控制台监视 CMG 的流量：

1. 转到“管理”工作区，展开“云服务”，然后选择“云管理网关”节点    。  

2. 在列表窗格中选择该 CMG。  

3. 在 CMG 连接点及其连接到的站点系统角色的细节窗格中查看流量信息。 这些统计信息说明了进入这些角色的客户端请求。 这些请求包括策略、位置、注册、内容、清单和客户端通知。<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>设置出站流量警报

出站流量警报可帮助了解网络流量何时接近 14 天的阈值级别。 在创建 CMG 时，可以设置流量警报。 如果跳过该部分，仍可在服务运行后设置警报。 可随时调整警报设置。

1. 转到“管理”工作区，展开“云服务”，然后选择“云管理网关”节点    。  

2. 在列表窗格中选择该 CMG，然后选择功能区中的“属性”  。  

3. 转到“警报”选项卡以启用阈值和警报  。 以千兆字节 (GB) 为单位指定 14 天的数据阈值。 另指定阈值百分比来引发不同的警报级别。  

4. 完成后选择“确定”  。  


## <a name="monitor-logs"></a>监视日志

CMG 在多个日志文件中生成条目。 有关详细信息，请参阅 [Configuration Manager 日志](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)。


## <a name="cloud-management-dashboard"></a>云管理仪表板

<!--1358461-->
从版本 1806 开始，云管理仪表板为 CMG 使用情况提供一个集中视图。 当站点载入到 [Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)以进行云管理时，它还显示有关云用户和设备的数据。  

下面的屏幕截图是云管理仪表板的一部分，显示了两个可用磁贴：  
![云管理仪表板磁贴 CMG 流量和当前联机客户端](media/1358461-cmg-dashboard.png)

在 Configuration Manager 控制台中，转到“监视”  工作区。 选择“云管理”  节点，并查看仪表板磁贴。  


## <a name="connection-analyzer"></a>连接分析器

从版本 1806 开始，使用实时验证的 CMG 连接分析器为疑难解答提供帮助。 控制台中的实用工具检查该服务的当前状态，以及通过 CMG 连接点通往任何允许 CMG 流量的管理点的通信通道。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“云服务”并选择“云管理网关”节点   。  

2. 选择目标 CMG 实例，然后选择功能区中的“连接分析器”  。  

3. 在 CMG 连接分析器窗口中，选择以下选项之一对服务进行身份验证：  

     1. **Azure AD 用户**：使用此选项来模拟与登录到加入 Azure AD 的 Windows 10 设备的云端用户标识相同的通信。 单击“登录”  以安全输入此 Azure AD 用户帐户的凭据。  

     2.  客户端证书：使用此选项来模拟与具有[客户端身份验证证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth)的 Configuration Manager 客户端相同的通信。  

4. 选择“启动”以开始分析  。 分析器窗口显示结果。 选择一个条目，查看“说明”字段中的更多详细信息。  


## <a name="bkmk_stop"></a> 超过阈值时停止 CMG

<!--3735092-->
从版本 1902 起，当数据传输总量超过限制时，Configuration Manager 现可停止 CMG 服务。 使用[警报](#set-up-outbound-traffic-alerts)，来在使用量达到警告或严重级别时触发通知。 此选项将关闭云服务，以帮助降低由于使用量陡升而意外导致的 Azure 成本。

> [!Important]  
> 即便服务未运行，仍会产生与云服务相关的成本。 停止该服务不会消除所有相关的 Azure 成本。 若要删除云服务的所有成本，请[删除 CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg)。  
>
> CMG 服务停止后，基于 Internet 的客户端不能与 Configuration Manager 通信。  

数据传输总量（传出量）包括来自云服务和存储帐户的数据。 该数据来自以下流：

- CMG 到客户端  
- CMG 到站点，包括 CMG 日志文件  
- 存储帐户到客户端（如果对内容启用 CMG）  

有关这些数据流的详细信息，请参阅 [CMG 端口和数据流](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow)。

存储警报阈值是独立的。 该警报监视 Azure 存储实例的容量。

在控制台中选择“云管理网关”节点中的 CMG 实例时，可在详细信息窗格中查看数据传输总量  。

Configuration Manager 每六分钟检查一次阈值。 如果使用量突然陡升，Configuration Manager 可能最多需要六分钟来检测是否超出阈值，并在超出时停止该服务。

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>在超过阈值时停止云服务的流程

1. [设置出站流量警报](#set-up-outbound-traffic-alerts)。  

2. 在 CMG 属性窗口的“警报”选项卡上，启用选项“超过关键阈值时停止此服务”。    

若要测试此功能，请暂时降低以下任一值：  

- 出站数据传输的 14 天阈值 (GB)  。 默认值为 `10000`。  

- 引发关键警报的阈值百分比  。 默认值为 `90`。  
