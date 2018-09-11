---
title: 监视云管理网关
titleSuffix: Configuration Manager
description: 通过云管理网关 (CMG) 监视客户端和网络流量。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 820d8a4241a6d250ce652f95ea47abe015600d4a
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111121"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中监视云管理网关

*适用范围：System Center Configuration Manager (Current Branch)*

客户端通过正在运行的云管理网关连接后，用户可以监视客户端与网络流量以确保了解该服务的执行方式。



## <a name="monitor-clients"></a>监视客户端

通过云管理网关连接的客户端采用与本地客户端相同的方式显示在 Configuration Manager 控制台中。 有关详细信息，请参阅[如何监视客户端](/sccm/core/clients/manage/monitor-clients)。



## <a name="monitor-traffic-in-the-console"></a>在控制台中监视流量

使用 Configuration Manager 控制台监视云管理网关的流量：

1. 转到“管理”>“云服务”>“云管理网关”。

2. 在列表窗格中选择云管理网关。

3. 在云管理网关连接点及其连接到的站点系统角色的细节窗格中查看流量信息。



## <a name="set-up-outbound-traffic-alerts"></a>设置出站流量警报

出站流量警报可帮助了解网络流量何时接近 14 天的阈值级别。 在创建云管理网关时，可以设置流量警报。 如果跳过该部分，仍可在服务运行后设置警报。 可随时调整警报设置。

1. 转到“管理”>“云服务”>“云管理网关”。

2. 在列表窗格中右键单击云管理网关，然后选择“属性”。

3. 单击“警报”选项卡。启用阈值和警报。 以千兆字节 (GB) 为单位指定 14 天的数据阈值。 另指定阈值百分比来引发不同的警报级别。

4. 完成后单击“确定”。



## <a name="monitor-logs"></a>监视日志

云管理网关在多个日志文件中生成条目。 有关详细信息，请参阅 [Configuration Manager 日志](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)。
