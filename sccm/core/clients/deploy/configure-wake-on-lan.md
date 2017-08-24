---
title: "配置 LAN 唤醒 | Microsoft Docs"
description: "在 System Center Configuration Manager 中选择 LAN 唤醒设置。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c920651ba1dc6e0a28df458d28956126ddbaff0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置 LAN 唤醒

*适用范围：System Center Configuration Manager (Current Branch)*

如果要将计算机从休眠状态中唤醒以安装所需的软件（如软件更新、应用程序、任务序列和程序），请指定 System Center Configuration Manager 的 LAN 唤醒设置。

可以使用唤醒代理客户端设置来对 LAN 唤醒进行补充。 但是，要使用唤醒代理，你必须首先为站点启用 LAN 唤醒，并为 LAN 唤醒传输方法指定“仅使用唤醒数据包”  和“单播”  选项。 这种唤醒解决方案也支持临时连接，例如远程桌面连接。

使用第一个过程来针对 LAN 唤醒配置主站点。 然后，使用第二个过程来配置唤醒代理客户端设置。 此第二个过程配置唤醒代理设置的默认客户端设置，以应用于层次结构中的所有计算机。 如果你希望这些设置仅应用于所选计算机，请创建一个自定义设备设置，并将其分配给包含要为唤醒代理配置的计算机的集合。 有关如何创建自定义客户端设置的详细信息，请参阅 [如何在 System Center Configuration Manager 中配置客户端设置](../../../core/clients/deploy/configure-client-settings.md)。

接收唤醒代理客户端设置的计算机可能会将其网络连接暂停 1-3 秒。 发生此情况是因为客户端必须重置网络接口卡以启用客户端上的唤醒代理驱动程序。

> [!WARNING]
> 为了避免网络服务意外中断，请首先在有代表性的隔离网络基础结构上评估唤醒代理。 然后，使用自定义客户端设置将测试范围扩展到若干子网上的所选计算机组。 有关唤醒代理运作方式的详细信息，请参阅[规划如何在 System Center Configuration Manager 中唤醒客户端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。

## <a name="to-configure-wake-on-lan-for-a-site"></a>为站点配置 LAN 唤醒

1. 在 Configuration Manager 控制台中，转到“管理”>“站点配置”>“站点”。
2. 单击要配置的主站点，然后单击“属性”。
3. 单击“LAN 唤醒”选项卡，然后配置针对此站点所需的选项。 要支持唤醒代理，请确保选择“仅使用唤醒数据包”和“单播”。 有关详细信息，请参阅[规划如何在 System Center Configuration Manager 中唤醒客户端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。
4. 单击“确定”，然后为层次结构中的所有主站点重复此过程。

## <a name="to-configure-wake-up-proxy-client-settings"></a>配置唤醒代理客户端设置

1. 在 Configuration Manager 控制台中，转到“管理”>“客户端设置”。
2. 单击“默认客户端设置”，然后单击“属性”。
3. 选择“电源管理”，然后对“启用唤醒代理”选择“是”。
4. 查看并在必要时配置其他唤醒代理设置。 有关这些设置的详细信息，请参阅[电源管理设置](../../../core/clients/deploy/about-client-settings.md#power-management)。
5. 单击“确定”关闭对话框，再单击“确定”关闭“默认客户端设置”对话框。

你可以使用以下 LAN 唤醒报表来监视唤醒代理的安装和配置：

- 唤醒代理部署状态摘要
- 唤醒代理部署状态详细信息

> [!TIP]
> 要测试唤醒代理是否工作，请测试与休眠计算机的连接。 例如，连接到该计算机上的共享文件夹，或尝试通过使用远程桌面连接到该计算机。 如果使用“直接访问”，请通过为当前位于 Internet 上的休眠计算机尝试相同的测试来检查 IPv6 前缀是否工作。
