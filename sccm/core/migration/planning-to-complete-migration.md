---
title: "完成移轉 | Microsoft Docs"
description: "了解在來源階層不再包含資料之後，如何完成移轉至 System Center Configuration Manager 目的地階層。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: eb1d2e320df02b26423ed4341d5bd1568b9444ad
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-to-complete-migration-in-system-center-configuration-manager"></a>規劃在 System Center Configuration Manager 中完成移轉

適用於：System Center Configuration Manager (最新分支)

藉由 System Center Configuration Manager，當來源階層不再包含您想要移轉至目的地階層的資料時，即可完成移轉程序。 完成移轉包括下列一般步驟：  

-   請確定您需要的資料已經移轉。 完成來源階層的移轉之前，請確定您已成功移轉來源階層的全部資源，其也是目的地階層所需的資源。 其可包括資料和用戶端。  

-   停止收集來源站台的資料。 若要完成來源階層的移轉，您必須先停止收集來源站台的資料。  

-   清理移轉資料。 停止收集來源階層中所有來源站台的資料後，您就可以從目的地階層之資料庫移除移轉程序和來源階層的相關資料。  

-   解除委任來源階層。 當完成來源階層的移轉，而且該階層不再包含您管理的資源後，您就可以解除委任來源階層中的站台，並可將相關基礎結構從您的環境移除。 如需如何解除委任站台和來源階層的詳細資訊，請參閱該 Configuration Manager 版本的文件。  

使用以下各節內容有助於規劃藉由停止資料收集和清理移轉資料的方式，完成來源階層的移轉：  

-   [規劃停止收集資料](#Plan_to_Stop_Data_Gath)  

-   [規劃清理移轉資料](#Plan_to_clean_up)  

##  <a name="Plan_to_Stop_Data_Gath"></a> 規劃停止收集資料  
 完成資料收集和清理移轉資料之前，您必須停止從來源階層的每一個來源站台收集資料。 若要停止從每一個來源站台收集資料，您必須執行底層來源站台上的 [停止收集資料]  命令，然後在每一個父站台重複處理程序。 來源階層的頂層站台必須是停止收集資料的最後一個站台。 在父站台執行此命令之前，您必須停止每一個子站台的資料收集。 通常，您只會在即將完成移轉程序時，停止收集資料。  

 停止從來源站台收集資料後，來自該站台的共用發佈點不再充當目的地階層中用戶端的內容位置。 因此，要確定目的地階層中用戶端所需存取的任何移轉內容仍可使用，只需使用以下其中一個選項即可：  

-   在目的地階層中，將內容發佈到至少一個發佈點。  

-   在您停止從來源站台收集資料前，請升級或重新指派需要內容的共用發佈點。 如需升級或重新指派共用發佈點的詳細資訊，請參閱[規劃 System Center Configuration Manager 中的內容部署移轉策略](../../core/migration/planning-a-content-deployment-migration-strategy.md)中適用的各節。  

停止從來源階層中的每一個來源站台收集資料後，就可以清理移轉資料。 直到清理移轉資料之前，每一個已執行或已排程執行的移轉作業仍可在 Configuration Manager 主控台存取。  

如需來源站台和資料收集的詳細資訊，請參閱[規劃 System Center Configuration Manager 中的來源階層策略](../../core/migration/planning-a-source-hierarchy-strategy.md)。  

##  <a name="Plan_to_clean_up"></a> 規劃清理移轉資料  
 完成移轉所需的最後一個步驟是清理移轉資料。 停止收集來源階層中每一個來源站台的資料後，可使用 [清理移轉資料]  命令。 此選用動作會從目的地階層的資料庫，移除目前來源階層的相關資料。  

 當您清理移轉資料時，大多數和移轉相關的資料會從目的地階層的資料庫移除。 不過，會保留移轉物件的詳細資料。 有了這些詳細資料，您就可以使用 [移轉] 工作區重新設定包含已移轉之資料的來源階層，以繼續該來源階層的移轉，或檢閱物件及先前移轉之物件的站台擁有權。  
