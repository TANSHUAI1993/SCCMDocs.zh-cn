---
title: 监视云管理网关
titleSuffix: Configuration Manager
description: 通过云管理网关 (CMG) 监视客户端和网络流量。
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6b52a97432dd85987dd98f11b0a048b1f730db84
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140671"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中监视云管理网关

适用范围：System Center Configuration Manager (Current Branch)

客户端通过正在运行的云管理网关 (CMG) 连接后，用户可以监视客户端与网络流量以确保了解该服务的执行方式。



## <a name="monitor-clients"></a>监视客户端

通过 CMG 连接的客户端采用与本地客户端相同的方式显示在 Configuration Manager 控制台中。 有关详细信息，请参阅[如何监视客户端](/sccm/core/clients/manage/monitor-clients)。



## <a name="monitor-traffic-in-the-console"></a>在控制台中监视流量

使用 Configuration Manager 控制台监视 CMG 的流量：

1. 转到“管理”工作区，展开“云服务”，然后选择“云管理网关”节点。  

2. 在列表窗格中选择该 CMG。  

3. 在 CMG 连接点及其连接到的站点系统角色的细节窗格中查看流量信息。  



## <a name="set-up-outbound-traffic-alerts"></a>设置出站流量警报

出站流量警报可帮助了解网络流量何时接近 14 天的阈值级别。 在创建 CMG 时，可以设置流量警报。 如果跳过该部分，仍可在服务运行后设置警报。 可随时调整警报设置。

1. 转到“管理”工作区，展开“云服务”，然后选择“云管理网关”节点。  

2. 在列表窗格中选择该 CMG，然后选择功能区中的“属性”。  

3. 转到“警报”选项卡以启用阈值和警报。 以千兆字节 (GB) 为单位指定 14 天的数据阈值。 另指定阈值百分比来引发不同的警报级别。  

4. 完成后选择“确定”。  



## <a name="monitor-logs"></a>监视日志

CMG 在多个日志文件中生成条目。 有关详细信息，请参阅 [Configuration Manager 日志](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)。



## <a name="cloud-management-dashboard"></a>云管理仪表板
<!--1358461--> 从版本 1806 开始，云管理仪表板为 CMG 使用情况提供一个集中视图。 当站点载入到 [Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)以进行云管理时，它还显示有关云用户和设备的数据。  

下面的屏幕截图是云管理仪表板的一部分，显示了两个可用磁贴：  
![云管理仪表板磁贴 CMG 流量和当前联机客户端](media/1358461-cmg-dashboard.png)

在 Configuration Manager 控制台中，转到“监视”工作区。 选择“云管理”节点，并查看仪表板磁贴。  



## <a name="connection-analyzer"></a>连接分析器

从版本 1806 开始，使用实时验证的 CMG 连接分析器为疑难解答提供帮助。 控制台中的实用工具检查该服务的当前状态，以及通过 CMG 连接点通往任何允许 CMG 流量的管理点的通信通道。

1. 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“云服务”并选择“云管理网关”节点。  

2. 选择目标 CMG 实例，然后选择功能区中的“连接分析器”。  

3. 在 CMG 连接分析器窗口中，选择以下选项之一对服务进行身份验证：  

     1. **Azure AD 用户**：使用此选项来模拟与登录到加入 Azure AD 的 Windows 10 设备的云端用户标识相同的通信。 单击“登录”以安全输入此 Azure AD 用户帐户的凭据。  

     2. 客户端证书：使用此选项来模拟与具有[客户端身份验证证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate)的 Configuration Manager 客户端相同的通信。  

4. 选择“启动”以开始分析。 分析器窗口显示结果。 选择一个条目，查看“说明”字段中的更多详细信息。  

