---
title: 集合最佳实践
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中的集合最佳实践。
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee91fe8b8b5b1c8d737e5818f42fa08e689a7e5a
ms.sourcegitcommit: 670cfed1e47a7a4a73aa4ccb873c6312be3c21ff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71311536"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Configuration Manager 中的集合最佳实践

适用范围：  System Center Configuration Manager (Current Branch)

使用以下 Configuration Manager 中的集合最佳实践。  

## <a name="dont-use-incremental-updates-with-many-collections"></a>请勿将增量更新用于大量集合

如果启用“为此集合使用增量更新”  选项，为多个集合启用此配置时可能导致评估延迟。 在你的层次结构中，阈值为大约 200 个集合。 确切的数目取决于以下因素：  

- 集合总数  

- 在层次结构中添加和更改新资源的频率  

- 层次结构中的客户端数目  

- 层次结构中的集合成员身份规则的复杂性  

## <a name="maintenance-window-size-for-software-updates"></a>软件更新维护时段大小

可为设备集合配置维护时段，以限制 Configuration Manager 可在这些设备上安装软件的次数。 如果你将该维护时段配置得太小，则客户端可能无法安装关键的软件更新，这使客户端容易遭受可由软件更新减轻的攻击。 
 
 > [!Tip] 
 > 规划维护时段时要牢记的重要注意事项：
 > - 默认的软件更新最大运行时间为 60 分钟。
 > - Configuration Manager 评估是否可以安装更新时，它会为最大运行时间增加 5 分钟，以将重启计算在内。
 > - 维护时段的剩余持续时间必须长于软件更新最大运行时间加上 5 分钟之后的值。
 
