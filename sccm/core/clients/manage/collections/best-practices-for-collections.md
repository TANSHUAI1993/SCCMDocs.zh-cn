---
title: "集合最佳做法 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中集合的最佳做法。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: "4"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fd62af3910c0745e0f1105417701b894e10cbbac
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 中集合的最佳做法

適用於：System Center Configuration Manager (最新分支)

請針對 System Center Configuration Manager 中的集合使用下列最佳做法。  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>針對大量集合請勿使用累加式更新  
 如果您啟用 [針對此集合使用累加式更新]  選項，這項組態可能會在針對許多集合啟用時，導致評估延遲。 臨界值約為階層中的 200 個集合。 確切數目則取決於下列因素：  

-   集合總數  

-   階層中新增資源和變更資源的頻率  

-   階層中的用戶端數目  

-   階層中集合成員資格規則的複雜性  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>請確定維護期間值大到足以部署重要的軟體更新  
 您可以設定用於裝置集合的維護期間，以限制 Configuration Manager 可以在這些裝置上安裝軟體的次數。 如果您將維護期間設定得太小，則用戶端可能無法安裝重要的軟體更新，導致用戶端容易遭受攻擊，因為安裝軟體更新可降低攻擊機率。  
