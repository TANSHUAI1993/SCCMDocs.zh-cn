---
title: 集合最佳实践
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中获取集合的最佳实践。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be96b106424c6340a27b015a06e0c3d06e3257d6
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890184"
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中集合的最佳实践

适用范围：  System Center Configuration Manager (Current Branch)

使用以下 System Center Configuration Manager 中集合的最佳实践。  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>不要为大量集合使用增量更新  
 如果启用“为此集合使用增量更新”  选项，为多个集合启用此配置时可能导致评估延迟。 在你的层次结构中，阈值为大约 200 个集合。 确切的数目取决于以下因素：  

-   集合总数  

-   在层次结构中添加和更改新资源的频率  

-   层次结构中的客户端数目  

-   层次结构中的集合成员身份规则的复杂性  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>确保维护时段足够大以部署关键的软件更新  
 可为设备集合配置维护时段，以限制 Configuration Manager 可在这些设备上安装软件的次数。 如果你将该维护时段配置得太小，则客户端可能无法安装关键的软件更新，这使客户端容易遭受可由软件更新减轻的攻击。  
