---
title: "監視移轉 | Microsoft Docs"
description: "了解如何使用 Configuration Manager 主控台來監視移轉工作的進度和成功與否。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 896807ec2c4be2835094a27add59d4cc09e93add
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>規劃在 System Center Configuration Manager 中監視移轉活動

*適用於：System Center Configuration Manager (最新分支)*

藉由 System Center Configuration Manager，您就可以在連線至目的地階層的 Configuration Manager 主控台中監視移轉。 在 Configuration Manager 主控台的 [管理] 工作區中，您可以使用 [移轉] 節點監視移轉工作的進度和成功與否。 您可以檢視每個移轉作業 (可識別已移轉的物件) 的摘要資訊、哪些物件尚未移轉，以及排除在移轉作業之外的物件數目。 您還可以查看與移轉問題相關的詳細資料。  

## <a name="view-migration-progress"></a>檢視移轉進度  
 若要檢視移轉作業的進度，請使用下列任何一項動作：  

-   在 Configuration Manager 主控台的 [管理] 工作區中，展開 [移轉作業] 節點，並選取移轉作業，然後選取 [作業中的物件] 索引標籤。  

-   使用 Configuration Manager 記錄檔檢閱移轉進度，或識別任何問題。 移轉管理員是一種 Configuration Manager 程序，可追蹤移轉動作，並將這些動作記錄在站台伺服器上 **\&lt;安裝路徑\>\\LOGS** 資料夾的 migmctrl.log 檔案中。  

    > [!NOTE]  
    >  如果移轉作業失敗，請盡快檢閱 migmctrl.log 檔案中的詳細資料。 移轉記錄檔項目會持續新增至檔案，並覆寫舊的詳細資料。 如果項目遭到覆寫，您可能無法識別移轉物件所遇到的問題，是否與移轉問題有關。 移轉活動會記錄在階層的頂層站台，不論您在設定移轉時 Configuration Manager 主控台連線到哪個站台。  

-   使用 Configuration Manager 報告。 Configuration Manager 提供多種內建移轉報告，或者您也可以編輯這些報告以符合您的需求。 如需 Configuration Manager 報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。  
