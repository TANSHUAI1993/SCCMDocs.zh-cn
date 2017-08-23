---
title: "修改和取代應用程式 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 應用程式版本及取代應用程式。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 28bea9210c9c58dabbb00a995e78cfedd1738291
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="revise-and-supersede-applications-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中修改和取代應用程式

*適用於：System Center Configuration Manager (最新分支)*

在本主題中，您會學習如何使用 System Center Configuration Manager 應用程式版本，以及如何以新版本取代應用程式。  

##  <a name="application-revisions"></a>應用程式修訂  
 當您針對應用程式或包含在應用程式內的部署類型進行修訂時，Configuration Manager 會建立新的應用程式修訂版。 您可以將每一個應用程式修訂歷程記錄顯示出來。 您也可以檢視其內容、還原之前的應用程式修訂，或刪除舊的修訂。  

### <a name="to-display-an-application-revision-history"></a>顯示應用程式修訂歷程記錄  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式]，然後選擇您要的應用程式。  

3.  在 [首頁] 索引標籤的 [應用程式] 群組中，選擇 [修訂歷程記錄] 以開啟 [應用程式修訂歷程記錄] 對話方塊。  

### <a name="to-view-an-application-revision"></a>檢視應用程式版本  

1.  在 [應用程式修訂歷程記錄] 對話方塊中，選取應用程式修訂，然後選擇 [檢視]。  

2.  在 [內容]  對話方塊中，檢查選取之應用程式的內容。  

    > [!NOTE]  
    >  顯示的應用程式內容是唯讀。  

3.  關閉 [內容]  對話方塊。  

### <a name="to-restore-an-application-revision"></a>還原應用程式版本  

1.  在 [應用程式修訂歷程記錄] 對話方塊中，選取應用程式修訂，然後選擇 [還原]。  

2.  在 [確認修訂還原] 對話方塊中，選擇 [是] 以還原選取的應用程式修訂。  

### <a name="to-delete-an-application-revision"></a>刪除應用程式修訂  

1.  在 [應用程式修訂歷程記錄] 對話方塊中，選取應用程式修訂，然後選擇 [刪除]。  

2.  在 [刪除應用程式修訂] 對話方塊中，選擇 [是]。  

> [!IMPORTANT]  
>  如果應用程式已遭淘汰且沒有參考，您只能刪除目前的應用程式修訂。  

##  <a name="application-supersedence"></a>應用程式取代  
 Configuration Manager 中的應用程式管理功能，可讓您使用取代關聯性來升級或取代現有應用程式。 當您取代應用程式時，可以指定新的部署類型來取代被取代應用程式的部署類型，也可以決定是否要在安裝取代應用程式之前，升級或解除安裝被取代的應用程式。  

> [!IMPORTANT]  
>  選擇解除安裝被取代的部署類型時，無法使用部署至不同集合類型的部署類型取代部署類型。  例如，如果選取解除安裝被取代的部署類型的選項，則部署至使用者集合的部署類型無法取代部署至裝置集合的部署類型。  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>決定要升級或取代應用程式  
 您可在 [應用程式屬性] 對話方塊中的 [指定取代關聯性]  對話方塊，指定要取代或升級應用程式。 取代類型依據您是否核取此對話方塊中的 [解除安裝]  選項而定：  

-   如果您想要更新為同一個應用程式 (具有相同的應用程式識別碼) 的較新版本，請**不要**核取 [解除安裝]。  

-   如果您想要變更為不同的應用程式 (具有不同的應用程式識別碼)，請核取 [解除安裝] 。 您必須移除被取代的應用程式版本。  

### <a name="supersede-dependent-applications"></a>取代相依的應用程式  
 在這個範例中，**主要應用程式**是指您要部署且具有相依性的應用程式。  

 您可以建立取代關聯性，將相依的應用程式更新為新版本。  

1.  確定新的相依應用程式與原始相依應用程式位於主要應用程式的同一個相依性群組中。  

2.  建立可將原始相依應用程式取代為新的相依應用程式的取代關聯性。  

 在主要應用程式的新安裝期間，會安裝新的相依應用程式。 主要應用程式的現有安裝則會使用新的相依應用程式進行更新。  

 最終結果是所有主要應用程式的部署都會使用新的相依應用程式。  

### <a name="further-considerations"></a>進一步考量  

-   您可以為相依的應用程式指定多個取代關聯性。 系統會安裝取代鏈結中最高的相依應用程式。  

-   相依應用程式必須部署到已安裝主要應用程式的裝置中，否則將不會安裝相依的應用程式。  

-   若是主要應用程式的新安裝，當有多個相依性時，相依性順序會決定要安裝哪個版本的相依應用程式。  

### <a name="to-specify-a-supersedence-relationship"></a>指定取代關聯性  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式]，然後選擇要取代其他應用程式的應用程式。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容] 以開啟應用程式名稱 [內容] 對話方塊。  

4.  在 <應用程式名稱\> [內容] 對話方塊的 [取代] 索引標籤中，選擇 [新增]。  

5.  在 [指定取代關聯性]  對話方塊中，按一下 [瀏覽] 。  

6.  在 [選擇應用程式] 對話方塊中，選擇您要取代的應用程式，然後選擇 [確定]。  

7.  在 [指定取代關聯性] 對話方塊中，選取部署類型來取代被取代應用程式的部署類型。  

    > [!NOTE]  
    >  根據預設，新的部署類型不會解除安裝被取代應用程式的部署類型。 這是您要將升級部署至現有應用程式時常用的案例。 選取 [解除安裝]  ，可在安裝新的部署類型之前移除現有部署類型。 如果您決定升級應用程式，務必先在實驗環境中進行測試。  

8.  選擇 [確定] 以關閉 [指定取代關聯性] 對話方塊。  

9. 選擇 [確定] 以關閉 <應用程式名稱\> [內容] 對話方塊。  

### <a name="to-display-applications-that-supersede-the-current-application"></a>顯示取代目前應用程式的應用程式  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫]。  

2.  在 [軟體程式庫] 工作區中，展開 [應用程式管理]、選擇 [應用程式]，然後選擇您要的應用程式。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容] 以開啟 <應用程式名稱\> [內容] 對話方塊。  

4.  在 <應用程式名稱\> [內容] 對話方塊的 [參考] 索引標籤中，從 [取代此應用程式的應用程式] 下拉式清單，選擇 [關聯性類型]。  

5.  檢閱要取代所選應用程式的應用程式清單，然後選擇 [確定] 以關閉 <應用程式名稱\> [內容] 對話方塊。  
