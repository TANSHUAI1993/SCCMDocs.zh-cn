---
title: "System Center Configuration Manager 應用程式的管理工作 | Microsoft Docs"
description: "管理 System Center Configuration Manager 應用程式和部署類型。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72f99f0c90951f80de3d6e5ed8786d3fa482107e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>System Center Configuration Manager 應用程式的管理工作

*適用於：System Center Configuration Manager (最新分支)*

請使用本文的資訊，協助管理 System Center Configuration Manager 應用程式和部署類型。  

如需建立應用程式和部署類型的說明，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。  

> [!IMPORTANT]  
>  依應用程式類型或部署類型而定，有些管理選項可能無法使用。  

##  <a name="manage-applications"></a>管理應用程式  
 在 [軟體程式庫] 工作區中，展開 [應用程式管理] > [應用程式]，然後依序選擇欲管理的應用程式和管理工作。  

|工作|詳細資料|  
|----------|-------------|  
|**管理存取帳戶**|開啟 [管理存取帳戶]  對話方塊，您可以在其中指定允許與選取的應用程式相關聯之內容存取的層級。|  
|**建立預先設置的內容檔案**|開啟 [建立預先設置的內容檔案精靈]  以協助您管理將內容發佈至遠端發佈點的作業。 如果排程和節流無法為遠端發佈點提供有效的解決方案，您可以在發佈點上預先設置內容。<br /><br /> 請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|**修訂歷程記錄**|開啟 [應用程式修訂歷程記錄] 對話方塊，即可在其中檢視此應用程式的修訂內容、刪除舊的應用程式修訂版本，以及還原此應用程式的舊版本。<br /><br /> 請參閱[如何修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)。|  
|**建立部署類型**|開啟 [建立部署類型精靈]，即可使用此精靈將新的部署類型新增至選取的應用程式。<br /><br /> 請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|**更新統計資料**|更新 [監視]  工作區中顯示在 [部署]  節點裡的資訊，這項資訊與此應用程式的部署有關。<br /><br /> 請參閱[從 System Center Configuration Manager 主控台監視應用程式](../../apps/deploy-use/monitor-applications-from-the-console.md)。|  
|**恢復**|恢復之前使用 [淘汰] 管理工作所淘汰掉的應用程式。|  
|**Retire**|淘汰應用程式後，就不能再部署該應用程式，但不會刪除該應用程式及其部署。 此選項不會移除此應用程式安裝在用戶端電腦上的現有複本。 對該應用程式的任何修訂內容將會在 60 天後從 Configuration Manager 中刪除。 不過，系統並不會移除該應用程式已經安裝的複本。<br /><br /> 若要刪除應用程式，必須先淘汰該應用程式、刪除所有部署、移除其他部署對該應用程式的參考，然後刪除該應用程式的所有修訂版本。<br /><br /> 請參閱[修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)。|  
|**匯出**|開啟 [匯出應用程式精靈]，此精靈可讓您將選取的應用程式匯出成 .zip 檔案，之後再進行封存或安裝於另一個站台。 如果您選擇匯出應用程式內容，系統會建立一個包含該內容的資料夾。<br /><br /> 您也可以匯出應用程式相依性、取代關聯性和條件，以及應用程式的內容及其相依性。<br /><br /> Windows PowerShell Cmdlet **Export-CMApplication** 可執行相同的功能。 如需詳細資訊，請參閱 Microsoft System Center 2012 Configuration Manager SP1 Cmdlet 參考文件中的 [Export-CMApplication](http://go.microsoft.com/fwlink/p/?LinkID=258880)。|  
|**刪除**|刪除目前選取的應用程式。<br /><br /> 如果某個應用程式有相依的應用程式、作用中的部署，或者相依的工作順序，您就不能刪除該應用程式。|  
|**模擬部署**|開啟 [模擬應用程式部署精靈]  ，您不需要安裝或解除安裝應用程式，即可在此精靈中測試該應用程式在電腦中的部署結果。<br /><br /> 請參閱[模擬應用程式部署](../../apps/deploy-use/simulate-application-deployments.md)。|  
|**部署**|開啟 [部署軟體精靈]  ，您可以在此精靈中將選取的應用程式部署至階層中的電腦集合。<br /><br /> 請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。|  
|**發佈內容**|開啟 [發佈內容精靈]  ，在此精靈中，您可以將選取的應用程式內容複製到階層中的發佈點。<br /><br /> 請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|**檢視關聯性**|會顯示一個圖表，其中包含所選應用程式與其他應用程式之間的關聯性。 選擇下列其中一項：<br><br><ul><li>**相依性** – 顯示相依於所選應用程式的應用程式，以及所選應用程式相依的應用程式。</li><li>**取代** – 顯示由所選應用程式取代的應用程式，以及將所選應用程式取代的應用程式。</li><li>**全域條件** – 顯示此應用程式所參考的全域條件。</li></ol><br /> 請參閱[修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)及[建立全域條件](../../apps/deploy-use/create-global-conditions.md)。|  

##  <a name="manage-deployment-types"></a>管理部署類型  
 在 [軟體程式庫] 工作區中，展開 [應用程式管理]，再選擇 [應用程式]，然後選擇具有您要管理之部署類型的應用程式。 在詳細資料窗格中，選擇 [部署類型] 索引標籤，然後依序選擇您要管理的部署類型以及管理工作。  

|工作|詳細資料|  
|----------|-------------|  
|**增加優先順序**|增加所選部署類型的優先順序。 部署類型是依順序評估的。 當部署類型符合指定需求時，就會加以執行，而不會再評估優先順序清單上的其他部署類型。|  
|**降低優先順序**|降低所選部署類型的優先順序。|  
|**刪除**|刪除選取的部署類型。<br><br>如果某個部署類型正由其他應用程式中的部署類型所參考，您就不能將其刪除。<br>若要刪除部署類型，您必須移除此部署類型在其他部署類型中的所有相依性。<br>如果應用程式具有的部署類型會參考您要刪除的部署類型，則必須移除這所有應用程式的舊有修訂版本。|  
|**更新內容**|重新整理所選部署類型的內容。<br /><br /> 當您針對具有虛擬應用程式的部署類型啟動此精靈時，會一併啟動 [更新內容精靈]。 此精靈可讓您變更所選虛擬應用程式的發佈選項和需求規則。 如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。<br /><br /> 當您重新整理部署類型的內容時，會建立新的應用程式修訂版本。 這可能會導致用戶端裝置更新為新的應用程式。|  
