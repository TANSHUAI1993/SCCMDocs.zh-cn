---
title: "監視用戶端部署狀態 | Microsoft Docs"
description: "在 System Center Configuration Manager 中監視用戶端部署狀態。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
caps.latest.revision: "11"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3d9d02d8c56aea17e563112f92173c2b56781da6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-client-deployment-status-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中監視用戶端部署狀態

*適用於：System Center Configuration Manager (最新分支)*

在站台之間部署用戶端需要時間，且首次安裝有時候不會成功。 System Center Configuration Manager 主控台可即時報告用戶端部署狀態，讓您隨時掌握用戶端的部署。  

> [!NOTE]  
>  監視用戶端部署最佳且最可靠的方法是使用 Configuration Manager 主控台 (如本文中所述)。 主控台中 **[監視]** 工作區的 **[用戶端狀態]** 區段，提供正確且即時的用戶端部署狀態。 您可以使用其他工具監視用戶端部署，如 Windows Server 中的伺服器管理員，或是 System Center Operations Manager，但您可能會收到來自一般用戶端安裝活動的警示。 因為用戶端安裝程式 (CCMSetup.exe) 在各種環境執行的方式，所以其他工具可能會產生未正確反應用戶端部署狀態的錯誤警示和警告。  

 在主控台的 **[監視]** 工作區中，您可以監視指定集合內用戶端部署的下列狀態︰  

-   相容  

-   進行中  

-   不相容  

-   失敗  

-   不明  

 Configuration Manager 會報告實際執行用戶端或實際執行前用戶端的部署。 Configuration Manager 主控台也提供顯示指定期間內失敗之用戶端部署的圖表，以協助您判斷針對部署進行的疑難排解是否有逐漸改善部署成功率。  

## <a name="to-monitor-client-deployments"></a>監視用戶端部署  

-   在 Configuration Manager 主控台中，按一下 [監視] > [用戶端狀態]。  

-   視您要監視的用戶端版本，按一下 **[實際執行用戶端部署]** 或 **[進入生產階段前用戶端部署]** 。  

-   檢閱用戶端部署狀態和用戶端部署失敗的圖表。  

-   如果您想要變更報告的範圍，請按一下 [瀏覽...]，然後選擇其他集合。  

 若要深入了解進入生產階段前的用戶端部署，請參閱[如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級](../../../core/clients/manage/upgrade/test-client-upgrades.md)。

 > [!NOTE]
 > 在進入生產階段前集合中，裝載站台系統角色之電腦上的部署狀態可能會報告為 [不符合標準]，即使用戶端已成功部署也一樣。 當您將用戶端升階為生產階段時，就會正確報告部署狀態。   

 若要監視部署的用戶端狀態，請參閱[如何在 System Center Configuration Manager 中監視用戶端](../../../core/clients/manage/monitor-clients.md)。  

 您可以使用 Configuration Manager 報告深入了解站台內用戶端的狀態。 如需如何執行報告的詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。  
