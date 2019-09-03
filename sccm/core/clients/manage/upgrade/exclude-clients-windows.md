---
title: 排除 Windows 客户端升级
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中排除 Windows 客户端升级。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a16bc859006b0253459259d354a68e2ff1dec83
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110156"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>了解如何在 Configuration Manager 中排除客户端升级

适用范围：  System Center Configuration Manager (Current Branch)

可排除客户端集合，使其不自动安装更新的客户端版本。 可将此排除用于在升级客户端时需特别注意的计算机集合。 排除集合中的客户端会忽略安装更新客户端软件的请求。

此排除适用于以下方法：

- 自动升级
- 基于软件更新的升级
- 登录脚本
- 组策略

> [!NOTE]
> 尽管用户界面声明无法通过任何方法升级客户端，但仍有两种方法可用于替代这些设置。 使用客户端请求安装或手动客户端安装来替代此配置。 有关详细信息，请参阅[如何升级排除的客户端](#bkmk_override)。

## <a name="bkmk_exclude"></a> 配置排除

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“站点配置”  ，选择“站点”  节点，然后选择功能区中的“层次结构设置”  。

2. 切换到“客户端升级”  选项卡。

3. 选择该选项以“排除指定客户端升级”  。 然后选择要排除的“排除集合”  。 只能选择排除单个集合。

4. 选择“确定”  以关闭并保存配置。

![用于自动升级排除的设置](media/automatic_upgrade_exclusion.png)

客户端处于排除的集合更新策略后，它们不会自动安装客户端更新。 有关详细信息，请参阅[如何升级 Windows 计算机的客户端](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers)。

> [!NOTE]
> 已排除的客户端仍会下载和运行 Ccmsetup，但不会升级。

从排除集合中删除客户端后，直到下一个自动升级循环，该客户端才会自动升级。

## <a name="bkmk_override"></a> 如何升级已排除的客户端

如果设备属于从升级中排除的集合，则仍可使用以下方法之一升级该客户端：

- **客户端请求安装**：Ccmsetup 允许客户端请求安装，因为这是用户的直接意图。 借助此方法，用户可以升级客户端，而无需将其从集合中删除，也不会从排除中删除整个集合。

- **手动客户端安装**：通过使用以下 Ccmsetup 命令行参数来手动升级已排除的客户端：/IgnoreSkipUpgrade 

    如果尝试在不使用此参数的情况下手动升级排除集合中的客户端，客户端将不会升级。 有关详细信息，请参阅[如何手动安装 Configuration Manager 客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)。

## <a name="see-also"></a>另请参阅

- [升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients)

- [如何部署客户端到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)

- [扩展互操作性客户端](/sccm/core/understand/interoperability-client)
