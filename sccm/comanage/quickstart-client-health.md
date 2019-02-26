---
title: 通过共同管理的客户端运行状况
titleSuffix: Configuration Manager
description: 维护 Configuration Manager 客户端运行状况： 从 Azure 门户上 Intune 的可见性
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754679"
---
# <a name="client-health-with-co-management"></a>通过共同管理的客户端运行状况

你的网络的运行状况直接连接到和移出该设备的运行状况。 Intune 可以与不正常的客户端通信，即使它不在网络上。 使用共同管理将此功能与报告回 98%的已知健康的客户端配置管理器的功能相结合。 然后可以检测、 评估和所有客户端的实时提供可见性。 Intune 还将添加所需的符合性升级跨所有连接的客户端的支持。

在以下视频中，高级项目经理 Rob York 和产品营销经理 Locky Ainley 讨论和演示通过共同管理的客户端运行状况：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>优点

评估客户端运行状况是头等大事。 System Center 2012 Configuration Manager 添加**CCMeval**。 此实用程序是外部的 Configuration Manager 客户端。 它提供客户端运行状况监视和自动修正。 但是，此报表依赖于以物理方式在设备上或几乎在您的内部网络上。 共同管理有助于解决此问题。

通过共同管理，Intune 可以报告上的客户端运行状况状态。 它提供数据的有效性的时间戳信息。 此信息将告诉您如果您的设备为正常运行、 连接、 无法安装应用程序，或者可以将更新为所需的 OS 生成。 

有关此功能的详细概述，请参阅此视频[What's New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) Ignite 2018 的会话。

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


在 Configuration Manager 提供设备状态的客户端已安装，但它不是，Intune 可以提供详细信息，而无需连接到客户端。 在 Intune 中的设备运行状况信息很容易理解。 如果状态而不是**正常**，它提供的建议和进行故障排除和修复此错误的后续步骤。

> [!Note]  
> 为未来的版本规划了以下优势：
> - 配置管理器将包括其他功能集成到 CCMeval  
> - 将很容易地识别在 Configuration Manager 和 Intune 可能不正常的机器  
> - 您可以在 Intune 中的客户端运行状况数据进行分组  



## <a name="value-proposition"></a>价值主张

使用此功能，现在已使用 Intune 的外部数据源。 它允许您以大量的客户端问题进行故障排除时确定下一步。 现在不需要创建其他报表或使用其他工具来拉回客户端的数据。

健康的客户端后，随时更新修补程序符合性。 更好的修补程序符合性意味着更高的安全性。



## <a name="configure"></a>配置

若要开始使用此功能，请使用以下步骤：

- 设备更新到 Windows 10 版本 1709年或更高版本  

- [启用共同管理](/sccm/comanage/how-to-enable)  
    - 无需任何工作负荷切换到 Intune  

- 更新 Configuration Manager 站点和客户端*版本 1806年*或更高版本  


### <a name="review-configuration-manager-client-health-in-intune"></a>在 Intune 中查看 Configuration Manager 客户端运行状况

1. 登录到 [Azure 门户](https://portal.azure.com/)。  

2. 选择**所有服务** > **Intune**。 Intune 位于**监视 + 管理**部分。  

3. 打开后**Microsoft Intune**窗格中，在下面的菜单**帮助和支持**，转到**故障排除**页。  

4. 使用**选择用户**选项，请查找特定设备造成**设备**列表，然后选择它以打开设备页。  

5. 在设备页的底部显示共同管理信息。 此信息包括客户端运行状况的以下字段：  
    - **配置管理器代理状态**  
    - **在时间中的最后一个 Configuration Manager 代理检查**  

> [!Tip]  
> 已注册 Intune 的设备连接到云服务一天三次，大约每 8 小时。 
