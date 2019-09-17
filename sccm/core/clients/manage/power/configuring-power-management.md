---
title: 配置电源管理
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中设置电源管理。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f76cf68cc007a5cefb323828752186ded62ad5f
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70902914"
---
# <a name="configure-power-management-in-configuration-manager"></a>在 Configuration Manager 中配置电源管理

适用范围：  System Center Configuration Manager (Current Branch)

本文介绍如何在 Configuration Manager 中设置电源管理。

## <a name="enable-and-configure-client-settings"></a>启用并配置客户端设置

此过程配置用于电源管理的默认客户端设置  。 它适用于层次结构中的所有计算机。

如果希望这些设置仅应用于某些计算机，请创建自定义设备客户端设置  。 然后将其分配给包含要进行电源管理的计算机的集合。 有关详细信息，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，选择“客户端设置”节点，然后选择“默认客户端设置”    。

1. 在功能区“主页”  选项卡的“属性”  组中，选择“属性”  。  

1. 选择“电源管理”组  。  

1. 启用客户端设置，允许对设备进行电源管理  。

1. 配置所需的其他客户端设置。 有关详细信息，请参阅[关于客户端设置 - 电源管理](/sccm/core/clients/deploy/about-client-settings#power-management)。  

客户端下一次下载客户端策略时，会配置这些设置。 若要为单个客户端启动策略检索，请参阅[如何管理客户端](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval)。  

## <a name="exclude-computers"></a>排除计算机

你可以阻止计算机集合接收电源管理设置。 如果计算机属于从电源管理设置中排除的任何集合，则该计算机不会应用电源管理设置  。 即使该计算机属于另一个确实应用电源管理设置的集合，此行为也适用。  

可能会出于下列原因要从电源管理中排除计算机：  

- 你的业务要求需要始终开启计算机。  

- 具有不希望应用电源管理设置的计算机控制集合。  

- 某些计算机不能应用电源管理设置。  

- 你想要从电源管理中排除运行 Windows Server 的计算机。  

> [!NOTE]  
> 如果将客户端设置配置为“允许用户从电源管理中排除其设备”，则用户可以使用软件中心从电源管理中排除自己的计算机  。  

要了解已从电源管理中排除了哪些计算机，请运行报表“排除的计算机”  。 有关此报表的详细信息，请参阅[如何监视和规划电源管理](/sccm/core/clients/manage/power/monitor-and-plan-for-power-management#BKMK_Excluded)。  

> [!IMPORTANT]  
> 从电源管理中排除计算机的操作将导致所有电源设置还原为其初始值。 无法将单个电源设置还原为其初始值。  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>如何从电源管理中排除计算机集合  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区，并选择“设备集合”  节点。  

1. 选择要从电源管理中排除的集合。 在功能区“主页”选项卡的“属性”组中，选择“属性”    。  

1. 切换到“电源管理”选项卡，选择“永远不将电源管理设置应用于此集合中的计算机”   。  

## <a name="next-steps"></a>后续步骤

[如何创建并应用电源计划](/sccm/core/clients/manage/power/create-and-apply-power-plans)

[如何监视和计划电源管理](/sccm/core/clients/manage/power/monitor-and-plan-for-power-management)
