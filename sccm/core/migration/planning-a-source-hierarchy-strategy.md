---
title: "來源階層策略 | Microsoft Docs"
description: "在您的 System Center Configuration Manager 環境中設定移轉作業之前，必須先設定來源階層，並且至少從該階層中的一個來源站台收集資料。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0619de32f859f512ee1c9f5a9c83ef8d04a256ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>規劃 System Center Configuration Manager 中的來源階層策略

適用於：System Center Configuration Manager (最新分支)

在您的 System Center Configuration Manager 環境中設定移轉作業之前，必須先設定來源階層，並且至少從該階層的一個來源站台收集資料。 下列各節可幫助您規劃如何設定來源階層、設定來源站台，以及決定 Configuration Manager 如何從來源階層的來源站台收集資料。 

##  <a name="BKMK_Source_Hierarchies"></a> 來源階層  
來源階層是 Configuration Manager 階層，其中包含您要移轉的資料。 當您設定移轉並且指定來源階層時，會指定來源階層的頂層站台。 此站台也稱為來源站台。 來源階層中您可移轉資料的其他站台也稱為來源站台。  

-   當您設定移轉作業以移轉 Configuration Manager 2007 來源階層的資料時，需要將其設定為從來源階層的一或多個特定來源站台移轉資料。  

-   當您將移轉作業設定為從執行 System Center 2012 Configuration Manager 或更新版本的來源階層移轉資料時，只需要指定頂層站台。  

您一次只能設定一個來源階層。  

-   如果您設定新的來源階層，該階層會自動變成目前的來源階層，取代原本的來源階層。  

-   當您設定來源階層時，必須指定來源階層的頂層站台，而且指定認證供 Configuration Manager 用於連線到該來源站台的 SMS 提供者和站台資料庫。  

-   Configuration Manager 會使用這些認證執行資料收集以擷取來源站台中物件和發佈點的相關資訊。  

-   作為資料收集程序的一部分，會識別出來源階層中的子站台。  

-   如果來源階層是 Configuration Manager 2007 階層，即可將這些其他站台設定為來源站台，每個來源站台皆會有個別的認證。  

雖然您可以連續設定多個來源階層，但是一次仍只能對一個來源階層進行移轉。  

-   如果您在完成從目前的來源階層移轉之前設定其他來源階層，Configuration Manager 會取消任何作用中移轉作業，並且延後針對目前來源階層排定的任何移轉作業。  

-   新設定的來源階層接著就會成為目前來源階層，而不使用原本的來源站台。  

-   接著您可以設定連線認證、其他來源站台以及新來源階層的移轉作業。  

如果您還原非作用中來源階層，而且之前並未使用 [清理移轉資料]，就可以檢視之前為該來源階層設定的移轉作業。 不過，您必須重新設定連線至階層中可用來源站台的認證，然後重新排程未完成的任何移轉作業，才能繼續從該階層移轉。  

> [!CAUTION]  
>  如果您從多個來源階層移轉資料，每個額外的來源階層都必須包含一組唯一的站台碼。  

如需設定來源階層的詳細資訊，請參閱[設定來源階層和來源站台以移轉到 System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)。  

##  <a name="BKMK_Source_Sites"></a> 來源站台  
 來源站台是指來源階層中，擁有您要移轉之資料的站台。 來源階層的頂層站台一律是第一個來源站台。 當移轉從新來源階層的第一個來源站台收集資料時，會探索有關該階層中其他站台的資訊。  

 完成初始來源站台的資料收集後，接著要採取的動作會取決於來源階層的產品版本。  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>執行 Configuration Manager 2007 SP2 的來源站台  
 從 Configuration Manager 2007 SP2 階層的初始來源站台收集資料後，您不需在建立移轉作業之前設定其他來源站台。 不過，您必須將其他站台設定為來源站台，而且 System Center Configuration Manager 必須從這些站台成功收集資料，才能從這些站台移轉資料。  

 若要從其他站台收集資料，您要將每個站台分別設定為來源站台。 這就需要指定將 System Center Configuration Manager 的認證連線到 SMS 提供者和每個來源站台的站台資料庫。 您為來源站台設定認證後，該站台的資料收集程序就會開始。  

 您在 Configuration Manager 2007 SP2 來源階層中設定其他來源站台時，必須從上到下設定來源站台，這表示最後才設定底層站台。 您可以隨時在階層分支中設定來源站台，但是必須先設定一個站台作為來源站台，才能設定任何其子站台作為來源站台。  

> [!NOTE]  
>  只有 Configuration Manager 2007 SP2 階層中的主要站台才支援移轉作業。  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>執行 System Center 2012 Configuration Manager 或更新版本的來源站台  
 從 System Center 2012 Configuration Manager 或更新版本階層的初始來源站台收集資料後，您不需要設定該來源階層中的其他來源站台。 原因是不同於 Configuration Manager 2007，這些版本的 Configuration Manager 是使用共用資料庫，而共用資料庫可讓您識別所有可用物件，然後從初始來源站台進行移轉。  

 當您設定存取帳戶來收集資料時，可能需要將「來源站台 SMS 提供者帳戶」存取權授與來源階層中的多部電腦。 當來源站台支援 SMS 提供者各自位於不同電腦上的多個執行個體時，可能會需要進行此動作。 資料收集開始時，目的地階層的頂層站台會連絡來源階層中的頂層站台，以識別該站台的 SMS 提供者位置。 只會識別 SMS 提供者的第一個執行個體。 如果資料收集程序無法在識別的位置存取 SMS 提供者，程序就會失敗，而且不會嘗試連線到執行該站台之 SMS 提供者執行個體的其他電腦。  

##  <a name="BKMK_Data_Gathering"></a> 資料收集  
 在您指定來源階層、設定來源階層中各個其他來源站台的認證，或共用來源站台的發佈點之後，Configuration Manager 隨即開始從來源站台收集資料。  

 接著資料收集程序會依照簡單的排程自行重複，以便與來源站台中的任何資料變更保持同步。 根據預設，程序每四小時重複一次。 您可以編輯來源站台的 [內容]，來變更此週期的排程。 初始資料收集程序必須檢閱 Configuration Manager 資料庫中的所有物件，而且可能需要較長的時間才能完成。 後續資料收集程序只會識別資料變更，而且完成所需的時間較短。  

 為了收集資料，目的地階層中的頂層站台會連線到來源站台的 SMS 提供者和站台資料庫，以擷取物件清單和發佈點。 這些連線都是使用來源站台存取帳戶。 如需收集資料所需設定的資訊，請參閱[在 System Center Configuration Manager 中進行移轉的必要條件](../../core/migration/prerequisites-for-migration.md)。  

 您可以使用 Configuration Manager 主控台中的 [立即收集資料] 和 [停止收集資料] 來開始和停止資料收集程序。  

 您因某種原因對來源站台使用 [停止收集資料] 之後，必須重新設定站台的認證，才能再次從該站台收集資料。 除非您重新設定來源站台，否則 Configuration Manager 無法識別該站台的新物件或之前所移轉物件的變更。  

> [!NOTE]  
>  您將獨立主要站台擴充為擁有管理中心網站的階層之前，必須停止所有資料收集。 您可以在站台擴充完成後，重新設定資料收集。  

### <a name="gather-data-now"></a>主控台中的 [立即收集資料]  
 對某個站台執行初始資料收集程序後，此程序會自行重複，以識別自上一次資料收集週期之後已更新的物件。 您也可以使用 Configuration Manager 主控台中的 [立即收集資料] 動作立即開始程序，以及重設下一個週期的開始時間。  

 來源站台的資料收集程序成功完成後，您可以共用來源站台的發佈點，並且設定移轉作業從該站台移轉資料。 資料收集是一個重複的移轉程序，會繼續執行直到您變更來源階層，或使用 [停止收集資料] 結束該站台的資料收集程序。  

### <a name="stop-gathering-data"></a>和 [停止收集資料]  
 如果您不再想要讓 Configuration Manager 識別該站台中新的或變更的物件，可以使用 [停止收集資料] 來結束來源站台的資料收集程序。 此動作也會阻止 Configuration Manager 將來源中的任何共用發佈點，作為您所移轉內容的內容位置，提供給目的地階層中的用戶端。  

 若要停止從每個來源站台收集資料，您必須在底層來源站台執行 [停止收集資料]，然後在每個父站台重複此程序。 來源階層的頂層站台必須是停止收集資料的最後一個站台。 您必須先在每個子站台上停止收集資料，才能在父站台上執行此動作。 通常，您只會在即將完成移轉程序時，停止收集資料。  

 停止收集來源站台的資料後，之前從站台收集的物件和集合相關資訊仍可在設定新的移轉作業時使用。 不過，您看不見任何新物件或集合，也看不見對現有物件所做的變更。 如果您重新設定來源站台並再次開始收集資料，就會看見有關之前所移轉物件的資訊和狀態。  
