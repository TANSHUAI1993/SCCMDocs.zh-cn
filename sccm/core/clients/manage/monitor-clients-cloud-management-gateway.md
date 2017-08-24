---
title: "监视云管理网关 - Configuration Manager | Microsoft Docs"
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: daa0790995dc13ec2c78ae2d98a9eb38c0bcf8ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中监视云管理网关

*适用范围：System Center Configuration Manager (Current Branch)*

从版本 1610 起，客户端通过正在运行的云管理网关服务连接后，用户可以监视客户端与网络流量以确保了解该服务的执行方式。

## <a name="monitor-clients"></a>监视客户端

通过云管理网关服务连接的客户端采用与本地客户端相同的方式显示在 Configuration Manager 控制台中。 有关详细信息，请参阅[如何监视客户端](monitor-clients.md)。

## <a name="monitor-traffic-in-the-console"></a>在控制台中监视流量

可以使用 Configuration Manager 控制台监视云管理网关的流量：

1. 转到“管理”>“云服务”>“云管理网关”。

2. 在“列表”窗格中选择“云管理网关服务”。

3. 在云管理网关连接角色及其连接到的站点系统角色的“详细信息”窗格中查看流量信息。

## <a name="set-up-outbound-traffic-alerts"></a>设置出站流量警报

出站流量警报可帮助了解流量何时接近 14 天（2 周）的阈值级别。 可以选择在创建云管理网关服务时设置流量警报。 如果跳过该部分，仍可在服务运行后设置警报。 还可以随时调整警报设置。

1. 转到“管理”>“云服务”>“云管理网关”。

2. 在“列表”窗格中右键单击“云管理网关服务”，然后选择“属性”。

3. 单击“警报”选项卡，然后选择打开（或关闭）阈值和警报。 然后指定 14 天阈值（以 GB 为单位）以及引发不同警报级别的阈值百分比。

4. 完成后单击“确定”。

## <a name="monitor-logs"></a>监视日志

云管理网关服务在多个日志文件中生成条目。 有关详细信息，请参阅 [Configuration Manager 日志](/sccm/core/plan-design/hierarchy/log-files)。
