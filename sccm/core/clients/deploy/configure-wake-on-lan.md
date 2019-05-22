---
title: 配置 LAN 唤醒
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中选择 LAN 唤醒设置。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59d99a3e3626be111e927dae8651d2e01364ccf5
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083146"
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置 LAN 唤醒

适用范围：System Center Configuration Manager (Current Branch)

若要将计算机从休眠状态唤醒，请指定 System Center Configuration Manager 的“LAN 唤醒”设置。

## <a name="bkmk_wol-1810"></a> 自版本 1810 起的 LAN 唤醒
<!--3607710-->
自 Configuration Manager 1810 起，有一种新方法可用来唤醒休眠计算机。 可以在 Configuration Manager 控制台中唤醒客户端，即使客户端与站点服务器不在同一子网中，也不例外。 如果你需要执行维护或查询设备，则不会受到处于睡眠状态的远程客户端的限制。 站点服务器使用客户端通知通道来标识同一远程子网上已唤醒的其他客户端，然后使用这些客户端发送 LAN 唤醒请求（幻数据包）。 使用客户端通知通道有助于避免可能会导致路由器关闭端口的 MAC 漂移。 可以同时启用新[旧版本](#bkmk_wol-previous)的 LAN 唤醒。

### <a name="limitations"></a>限制

- 目标子网中必须至少有一个客户端处于唤醒状态。
- 此功能不支持以下网络技术：
   - IPv6
   - 802.1x 网络身份验证
    >[!NOTE]
    > 802.1x 网络身份验证可能支持其他配置，具体视硬件及其配置而定。
- 仅当你通过“唤醒”客户端通知向计算机发出通知时，计算机才会唤醒。
    - 若要在最后期限到来时唤醒，使用的是旧版 LAN 唤醒。
    -  如果旧版本未启用，使用“使用 LAN 唤醒来唤醒客户端以执行必需部署”或“发送唤醒数据包”设置创建的部署不会发生客户端唤醒。  


### <a name="security-role-permissions"></a>安全角色权限

- 集合类别下的“通知资源”

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>自版本 1810 起，将客户端配置为使用 LAN 唤醒

以前必须在网络适配器的属性中手动启用 LAN 唤醒客户端。 Configuration Manager 1810 新增客户端设置“允许网络唤醒”。 请配置和部署此设置，而不是修改网络适配器的属性。

1. 在“管理”下，转到“客户端设置”。
1. 选择要编辑的客户端设置，或新建要部署的自定义客户端设置。 有关详细信息，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。
1. 在“电源管理”客户端设置下，为“允许网络唤醒”设置选择“启用”。 若要详细了解此设置，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#power-management)。

4. 自 Configuration Manager 1902 起，新版 LAN 唤醒使用你为“LAN 唤醒端口号(UDP)”[客户端设置](/sccm/core/clients/deploy/about-client-settings#power-management)指定的自定义 UDP 端口。 新版和旧版 LAN 唤醒共用此设置。
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>自 1810 起，使用客户端通知来唤醒客户端
 
可以唤醒一个客户端或集合中的任何多个休眠客户端。 对于集合中已唤醒的设备，不会对它们执行任何操作。 只有处于休眠状态的客户端，才会收到 LAN 唤醒请求。 若要详细了解如何向客户端发出唤醒通知，请参阅[客户端通知](/sccm/core/clients/manage/client-notification)。

- **若要唤醒一个客户端：** 请右键单击此客户端，转到“客户端通知”，再选择“唤醒”。

   ![控制台中的客户端唤醒通知](media/wol-wake-up-client-notification.png)

- **若要唤醒集合中所有处于休眠状态的客户端：** 请右键单击设备集合，转到“客户端通知”，再选择“唤醒”。
   - 无法对内置集合执行此操作。
   - 如果集合中既有休眠客户端，也有已唤醒客户端，只有处于休眠状态的客户端，才会收到 LAN 唤醒请求。  

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>仅启用新版 LAN 唤醒会发生什么

如果你仅启用新版 LAN 唤醒，只有“唤醒”客户端通知处于启用状态。 如果任务序列、软件分发或软件更新安装等部署的最后期限到来，不会向客户端发送通知。 休眠计算机重新联机后，它会在向管理点签入时反映在控制台中。

自 Configuration Manager 版本 1902 起，可以指定 LAN 唤醒端口。 新版和旧版 LAN 唤醒共用此设置。

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>同时启用两个版本的 LAN 唤醒会发生什么

同时启用两个版本的 LAN 唤醒后，不仅可以使用“唤醒”客户端通知，还能在最后期限到来时唤醒。 客户端通知功能与传统 LAN 唤醒略有不同。 有关客户端通知工作原理的简要说明，请参阅[自版本 1810 起的 LAN 唤醒](#bkmk_wol-1810)部分。 新客户端设置“允许网络唤醒”会将 NIC 属性更改为允许 LAN 唤醒。 你不再需要为添加到环境中的新计算机手动更改它。 LAN 唤醒的其他所有功能都没有改变。

自版本 1902 起，“唤醒”客户端通知使用现有的“LAN 唤醒端口号(UDP)”设置。


## <a name="bkmk_wol-previous"></a> 版本 1806 及更低版本的 LAN 唤醒

如果要将计算机从休眠状态中唤醒以安装所需的软件（如软件更新、应用程序、任务序列和程序），请指定 System Center Configuration Manager 的 LAN 唤醒设置。

可以使用唤醒代理客户端设置来对 LAN 唤醒进行补充。 但是，要使用唤醒代理，你必须首先为站点启用 LAN 唤醒，并为 LAN 唤醒传输方法指定“仅使用唤醒数据包”  和“单播”  选项。 这种唤醒解决方案也支持临时连接，例如远程桌面连接。

使用第一个过程来针对 LAN 唤醒配置主站点。 然后，使用第二个过程来配置唤醒代理客户端设置。 此第二个过程配置唤醒代理设置的默认客户端设置，以应用于层次结构中的所有计算机。 如果你希望这些设置仅应用于所选计算机，请创建一个自定义设备设置，并将其分配给包含要为唤醒代理配置的计算机的集合。 有关如何创建自定义客户端设置的详细信息，请参阅 [如何在 System Center Configuration Manager 中配置客户端设置](../../../core/clients/deploy/configure-client-settings.md)。

接收唤醒代理客户端设置的计算机可能会将其网络连接暂停 1-3 秒。 发生此情况是因为客户端必须重置网络接口卡以启用客户端上的唤醒代理驱动程序。

> [!WARNING]
> 为了避免网络服务意外中断，请首先在有代表性的隔离网络基础结构上评估唤醒代理。 然后，使用自定义客户端设置将测试范围扩展到若干子网上的所选计算机组。 有关唤醒代理运作方式的详细信息，请参阅[规划如何在 System Center Configuration Manager 中唤醒客户端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>使用版本 1806 及更低版本为站点配置 LAN 唤醒的具体步骤

 若要使用 LAN 唤醒，必须为层次结构中的每个站点都启用它。

1. 在 Configuration Manager 控制台中，转到“管理”>“站点配置”>“站点”。
2. 单击要配置的主站点，然后单击“属性”。
3. 单击“LAN 唤醒”选项卡，然后配置针对此站点所需的选项。 要支持唤醒代理，请确保选择“仅使用唤醒数据包”和“单播”。 有关详细信息，请参阅[规划如何在 System Center Configuration Manager 中唤醒客户端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。
4. 单击“确定”，然后为层次结构中的所有主站点重复此过程。

![在站点属性中启用 LAN 唤醒](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>配置唤醒代理客户端设置

1. 在 Configuration Manager 控制台中，转到“管理”>“客户端设置”。
2. 单击“默认客户端设置”，然后单击“属性”。
3. 选择“电源管理”，然后对“启用唤醒代理”选择“是”。
4. 查看并在必要时配置其他唤醒代理设置。 若要详细了解这些设置，请参阅[电源管理设置](../../../core/clients/deploy/about-client-settings.md#power-management)。
5. 单击“确定”关闭对话框，再单击“确定”关闭“默认客户端设置”对话框。

你可以使用以下 LAN 唤醒报表来监视唤醒代理的安装和配置：

- 唤醒代理部署状态摘要
- 唤醒代理部署状态详细信息

> [!TIP]
> 要测试唤醒代理是否工作，请测试与休眠计算机的连接。 例如，连接到该计算机上的共享文件夹，或尝试通过使用远程桌面连接到该计算机。 如果使用“直接访问”，请通过为当前位于 Internet 上的休眠计算机尝试相同的测试来检查 IPv6 前缀是否工作。
