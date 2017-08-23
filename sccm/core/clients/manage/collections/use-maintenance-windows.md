---
title: "使用維護期間 | Microsoft Docs"
description: "使用集合和維護期間，在 System Center Configuration Manager 中有效率地管理用戶端。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fa67cf597c73bab47209c9b98539f97e174ae70b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>如何使用 System Center Configuration Manager 的維護視窗

*適用於：System Center Configuration Manager (最新分支)*

維護時段可讓您定義何時可在裝置集合上執行 Configuration Manager 操作。 您可以藉助維護時段，確保用戶端設定變更發生的期間不會影響生產力。  

 下列操作支援維護時段：  

-   軟體部署  

-   軟體更新部署  

-   相容性設定部署和評估  

-   作業系統部署  

-   工作順序部署  

 請設定維護時段的開始日期、開始和完成時間，以及定期模式。 視窗的持續時間上限必須小於 24 小時。 根據預設，部署造成電腦重新啟動的行為不允許出現在維護時段之外，但是您可以覆寫預設值。 維護時段只會影響部署程式執行的時間，而設定在本機上下載及執行的應用程式可以在時段之外下載內容。  

 如果用戶端電腦是維護時段的裝置集合成員，則部署程式只會在允許的執行時間上限未超過針對視窗設定的持續時間時執行。 如果程式執行失敗，將會產生警示，且部署將會在下一次排程的維護視窗有可用時間時重新執行。  

## <a name="using-multiple-maintenance-windows"></a>使用多個維護視窗  
 如果用戶端電腦是具有維護時段之多個裝置集合的成員，則適用下列規則：  

-   如果維護期間未重疊，則會視為兩個獨立的維護期間。  

-   如果維護期間重疊，則會視為包含兩個維護期間所涵蓋時段的單一維護期間。 例如，如果兩個視窗的持續時間各為一小時，其中有 30 分鐘重疊，則維護時段的有效持續時間會是 90 分鐘。  

 當使用者從軟體中心起始應用程式安裝時，應用程式將會立即安裝，而不理會任何維護時段。  

 如果在軟體中心使用者設定的非營業時間裡，有 **必要** 目的的應用程式部署面臨安裝期限，就會安裝應用程式。  

### <a name="how-to-configure-maintenance-windows"></a>如何設定維護視窗  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性]>  [裝置集合]。  

3.  在 [裝置集合] 清單中，選取一個集合。 您無法為 [所有系統]  集合建立維護期間。  

4.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

5.  在 [&lt;集合名稱\> 內容] 對話方塊的 [維護時段] 索引標籤中，選擇新增圖示。  

6.  完成 [&lt;新增\> 排程] 對話方塊。  

7.  從 [將此排程套用至] 下拉式清單中進行選取。  

8.  選擇 [確定]，然後關閉 [&lt;集合名稱\> 內容] 對話方塊。  
