---
title: 通过共同管理了解客户端运行状况
titleSuffix: Configuration Manager
description: 从 Azure 门户上的 Intune 维护 Configuration Manager 客户端运行状况的可见性
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6838371a80530d5ab66abd9d8a976af41513e15
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754679"
---
# <a name="client-health-with-co-management"></a>通过共同管理了解客户端运行状况

网络的运行状况直接关系到已联网和未联网设备的运行状况。 Intune 可以与运行不正常的客户端进行通信，即使该客户端不在网络中也是如此。 使用共同管理将此功能与 Configuration Manager 的功能结合起来，以报告 98% 的已知运行状况良好的客户端。 然后，可以实时检测、评估所有客户端，并提供可见性。 Intune 还支持对所有已连接客户端进行符合性升级。

在以下视频中，高级项目经理 Rob York 和产品营销经理 Locky Ainley 将介绍并演示如何使用共同管理了解客户端运行状况：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>优点

评估客户端运行状况是首要任务。 System Center 2012 Configuration Manager 添加了 CCMeval。 此实用程序位于 Configuration Manager 客户端外部。 它提供客户端运行状况监视和自动修正。 但是，此报表依赖于以物理方式或以虚拟方式位于内部网络上的设备。 共同管理有助于解决此问题。

通过共同管理，Intune 可以报告客户端运行状况状态。 它提供有关数据有效性的时间戳信息。 通过此信息可以了解设备是否运行正常、能否连接，能否安装应用，或能否更新到所需的操作系统版本。 

有关此功能的详细概述，请参阅 Ignite 2018 [Configuration Manager 新增功能](https://myignite.techcommunity.microsoft.com/sessions/64591)会话中的视频。

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


当 Configuration Manager 提供安装客户端的设备状态，但实际没有安装时，Intune 可以提供更多信息，而无需连接到客户端。 Intune 中的设备运行状况易于理解。 如果状态不是“运行状况良好”，则会提供建议和后续步骤以进行故障排除和修复。

> [!Note]  
> 计划为未来版本提供以下优势：
> - Configuration Manager 将在 CCMeval 中增加其他功能  
> - 能够更轻松地在 Configuration Manager 和 Intune 中识别可能运行不正常的计算机  
> - 可以在 Intune 中对客户端运行状况数据进行分组  



## <a name="value-proposition"></a>价值主张

借助此功能，现在可以通过 Intune 提供外部数据源。 这便于你在排查大量客户端问题时确定后续步骤。 现在，拉取回客户端数据时，无需创建额外报表或使用其他工具。

如果客户端运行正常，可以随时更新修补程序符合性。 具有更好的修补程序符合性，也就拥有了更高的安全性。



## <a name="configure"></a>配置

若要开始使用此功能，请使用以下步骤：

- 将设备更新到 Windows 10 版本 1709 或更高版本  

- [启用共同管理](/sccm/comanage/how-to-enable)  
    - 无需将任何工作负载切换到 Intune  

- 将 Configuration Manager 站点和客户端更新到版本 1806 或更高版本  


### <a name="review-configuration-manager-client-health-in-intune"></a>在 Intune 中查看 Configuration Manager 客户端运行状况

1. 登录到 [Azure 门户](https://portal.azure.com/)。  

2. 选择“所有服务” > “Intune”。 Intune 位于“监视 + 管理”部分中。  

3. 打开“Microsoft Intune”窗格后，在“帮助与支持”下的菜单中转到“故障排除”页。  

4. 使用“选择用户”选项，在“设备”列表查找特定设备，选中设备以打开设备页。  

5. 共同管理信息显示在设备页的底部。 此信息包括客户端运行状况的以下字段：  
    - **Configuration Manager 代理状态**  
    - **上一个 Configuration Manager 代理签入时间**  

> [!Tip]  
> 已注册 Intune 的设备连接到云服务的频率为：一天连接三次（大约每八小时一次）。 
