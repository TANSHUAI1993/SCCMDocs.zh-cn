---
title: "移轉內容 | Microsoft Docs"
description: "將資料移轉至 System Center Configuration Manager 目的地階層時，使用發佈點管理內容。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 25619d91522193178e0415f649ca4b34c94ecc89
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>規劃 System Center Configuration Manager 中的內容部署移轉策略

*適用於：System Center Configuration Manager (最新分支)*

當您主動將資料移轉到 System Center Configuration Manager 目的地階層時，來源與目的地階層中的 Configuration Manager 用戶端皆可繼續存取您在來源階層中部署的內容。 您也可以使用移轉將來源階層中的發佈點升級或重新指派為目的地階層中的發佈點。 當您共用和升級或重新指派發佈點時，此策略可讓您不必針對移轉的用戶端將內容重新部署至目的地階層中的新伺服器。  

雖然您可以在目的地階層中重新建立及發佈內容，但是也可以使用下列選項管理此內容：  

-   將來源階層中的發佈點與目的地階層中的用戶端共用。  

-   將來源階層中的獨立 Configuration Manager 2007 發佈點或 Configuration Manager 2007 次要站台升級成為目的地階層中的發佈點。  

-   將 System Center Configuration Manager 來源階層中的發佈點重新指派至目的地階層中的站台。  

下面各節可幫助您在移轉期間規劃內容部署：  

-   [在來源和目的地階層之間共用發佈點](#About_Shared_DPs_in_Migration)  

-   [規劃升級 Configuration Manager 2007 共用發佈點](#Planning_to_Upgrade_DPs)  

    -   [發佈點升級程序](#BKIMK_UpgradeProcess)  

    -   [規劃升級 Configuration Manager 2007 次要站台](#BKMK_UpgradeSS)  

-   [規劃重新指派 System Center Configuration Manager 發佈點](#BKMK_ReassignDistPoint)  

    -   [發佈點重新指派程序](#BKMK_ReassignProcess)  

-   [移轉內容時內容的擁有權](#About_Migrating_Content)  

##  <a name="About_Shared_DPs_in_Migration"></a> 在來源和目的地階層之間共用發佈點  
在移轉期間，您可以將來源階層的發佈點與目的地階層共用。 您可以使用共用發佈點將移轉自來源階層的內容立即提供給目的地階層中的用戶端，而不需重新建立該內容，然後將它發佈至目的地階層中的新發佈點。 當目的地階層中的用戶端要求部署至您共用之發佈點的內容時，共用發佈點就可做為有效的內容位置提供給用戶端。  

 當來自來源階層的移轉保持作用中，除了目的地階層中用戶端的有效內容位置外，您還可以將發佈點升級或重新指派至目的地階層。 您可以升級 Configuration Manager 2007 共用的發佈點，並重新指派 System Center 2012 Configuration Manager 共用的發佈點。 當您升級或重新指派共用發佈點時，發佈點便會從來源階層移除，並且成為目的地階層中的發佈點。 升級或重新指派共用發佈點之後，您可以在來源階層的移轉完成後繼續使用目的地階層中的發佈點。 如需如何升級共用發佈點的詳細資訊，請參閱[規劃升級 Configuration Manager 2007 共用發佈點](#Planning_to_Upgrade_DPs)。 如需如何重新指派共用發佈點的詳細資訊，請參閱[規劃重新指派 System Center Configuration Manager 發佈點](#BKMK_ReassignDistPoint)。  

 您可以從來源階層中的任何來源站台選擇共用發佈點。 當您共用來源站台的發佈點時，會在該主要站台和每個主要站台之每個符合資格的發佈點上共用子次要站台。 若要符合共用發佈點的資格，裝載發佈點的站台系統伺服器必須設定為使用完整網域名稱 (FQDN)。 會略過所有設定為使用 NetBIOS 名稱的發佈點。  

> [!TIP]  
>  Configuration Manager 2007 不需要您設定站台系統伺服器的 FQDN。  

請利用下列資訊幫助您規劃共用發佈點：  

-   您共用的發佈點必須符合共用發佈點的必要條件。 如需這些必要條件的詳細資訊，請參閱[在 System Center Configuration Manager 中進行移轉的必要條件](../../core/migration/prerequisites-for-migration.md)中的[移轉所需的設定](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations)。  

-   共用發佈點動作是全站台的設定，會共用來源站台及任何子次要站台上所有符合資格的發佈點。 當您啟用發佈點共用時，無法選取個別發佈點進行共用。  

-   目的地階層中的用戶端可接收來源階層透過共用方式發佈至發佈點上的套件內容位置資訊。 若是來自 Configuration Manager 2007 來源階層的發佈點，則會包括子目錄發佈點、伺服器共用上的發佈點及標準發佈點。  

    > [!WARNING]  
    >  如果您變更來源階層，原始來源階層中的共用發佈點就無法使用，也無法做為內容位置提供給目的地階層中的用戶端。 如果您將移轉重新設定為使用原始來源階層，則之前共用的發佈點就會還原為有效的內容位置伺服器。  

-   當您移轉裝載於共用發佈點上的套件時，來源和目的地階層中的套件版本必須維持相同。 如果來源和目的地階層中的套件版本不相同，目的地階層中的用戶端就無法從共用發佈點擷取該內容。 因此，如果您更新來源階層中的套件，則必須先重新移轉套件資料，目的地階層中的用戶端才能從共用發佈點擷取該內容。  

    > [!NOTE]  
    >  當您檢視裝載於共用發佈點上的套件詳細資料時，在下一次資料收集週期完成之前，顯示為來源站台的 [共用發佈點] 索引標籤上的 [已裝載移轉的套件] 的套件數目不會更新。  

-   您可在連線至目的地階層之 Configuration Manager 主控台的 [系統管理] 工作區的 [來源階層] 節點中，檢視共用的發佈點和其內容。  

-   您無法使用 Configuration Manager 2007 來源階層中的共用發佈點來裝載 Microsoft Application Virtualization (App-V) 的套件。 App-V 套件必須移轉和加以轉換，供在目的地階層中的用戶端使用。 不過，您可以使用 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層中的共用發佈點來裝載目的地階層中用戶端的 App-V 套件。  

-   當您共用 Configuration Manager 2007 來源階層中受保護的發佈點時，目的地階層會建立包含該發佈點之受保護網路位置的界限群組。 您無法在目的地階層中變更這個界限群組。 不過，如果您變更 Configuration Manager 2007 來源階層中發佈點的受保護界限資訊，該變更會在下一次資料收集週期完成後反映在目的地階層中。  

    > [!NOTE]  
    >  System Center 2012 Configuration Manager 和 System Center Configuration Manager 站台使用慣用發佈點而不是受保護發佈點的概念。 此情況只適用於 Configuration Manager 2007 來源站台共用的發佈點。  

您要先共用來源站台的發佈點，Configuration Manager 主控台才會顯示符合資格的發佈點。 共用發佈點之後，只會列出成功共用的發佈點。  

已共用發佈點之後，您就可以變更來源階層中任何共用發佈點的設定。 您對發佈點設定所做的變更會在下一次資料收集週期後反映於目的地階層中。 更新後符合共用資格的發佈點會自動共用，而資格不符的發佈點則會停止共用。 例如，您的發佈點可能未設定為使用內部網路 FQDN 且一開始未與目的地階層共用。 您為該發佈點設定 FQDN 之後，下一次資料收集週期就會識別此設定，而發佈點就會與目的地階層共用。  

##  <a name="Planning_to_Upgrade_DPs"></a> 規劃升級 Configuration Manager 2007 共用發佈點  
從 Configuration Manager 2007 來源階層移轉時，您可以升級共用發佈點使其成為 System Center Configuration Manager 發佈點。 您可以升級主要站台和次要站台的發佈點。 升級程序會從 Configuration Manager 2007 階層移除發佈點，並使其成為目的地階層中的站台系統伺服器。 此程序也會將發佈點上的現有內容複製到發佈點電腦上的新位置。 接著升級程序會修改內容的副本，以建立儲存單一版本搭配目的地階層中的內容部署使用。 因此，當您升級發佈點時，不需要重新發佈 Configuration Manager 2007 發佈點上裝載的移轉內容。  

在 Configuration Manager 將內容轉換成單一執行個體存放區後，Configuration Manager 會刪除發佈點電腦上的原始來源內容以釋出磁碟空間。 Configuration Manager 不使用原始來源內容位置。  

並非所有可共用的 Configuration Manager 2007 發佈點都有資格升級至 System Center Configuration Manager。 為符合升級資格，Configuration Manager 2007 發佈點必須符合升級條件。 這些條件包括發佈點安裝所在的站台系統伺服器，以及安裝的 Configuration Manager 2007 發佈點類型。 例如，您無法升級於主要站台的站台伺服器電腦上安裝的任何類型發佈點，但是可以升級次要站台的站台伺服器電腦上安裝的標準發佈點。  

> [!NOTE]  
>  只有在所執行作業系統版本支援目的地階層中之發佈點的電腦上，其 Configuration Manager 2007 共用發佈點才可升級。 例如，雖然您可以共用執行 Windows Vista 之電腦上的 Configuration Manager 2007 發佈點，但是無法升級此共用發佈點，原因是 System Center Configuration Manager 不支援以此作業系統作為發佈點。  

下表列出可升級之每個 Configuration Manager 2007 發佈點類型的支援位置。  

|發佈點類型|不是位於站台伺服器之站台系統電腦上的發佈點|不是位於站台伺服器且裝載其他站台系統角色之站台系統電腦上的發佈點|次要站台伺服器上的發佈點|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|標準發佈點|[是]|否|是|  
|伺服器共用上的發佈點<sup>1</sup>|是|否|否|  
|子目錄發佈點|[是]|否|否|  

 <sup>1</sup> System Center Configuration Manager 不支援伺服器共用作為站台系統，但支援位於伺服器共用上的 Configuration Manager 2007 發佈點升級。 當您升級位於伺服器共用上的 Configuration Manager 2007 發佈點時，發佈點類型會自動轉換成伺服器，而您必須選取發佈點電腦上用來儲存內容儲存單一版本的磁碟機。  

> [!WARNING]  
>  在升級子目錄發佈點之前，請先解除安裝 Configuration Manager 2007 用戶端軟體。 如果您升級的分支發佈點上已安裝 Configuration Manager 2007 用戶端軟體，則先前部署至電腦的內容會從電腦中移除，且發佈點升級會失敗。  

若要在 Configuration Manager 主控台中識別可進行升級的發佈點，請在 [來源階層] 節點中選取來源站台，然後選取 [共用發佈點] 索引標籤。 符合資格的發佈點會在 [符合升級資格]  欄位中顯示 [是]  。  

升級安裝在 Configuration Manager 2007 次要站台伺服器上的發佈點時，會將次要站台從來源階層解除安裝。 雖然此案例稱為次要站台升級，卻只適用於發佈點站台系統角色。 結果是次要站台無法升級，而且會解除安裝。 這會在過去作為次要站台伺服器的電腦上留下目的地階層的發佈點。 如果您打算升級次要站台的發佈點，請參閱本主題的[規劃升級 Configuration Manager 2007 次要站台](#BKMK_UpgradeSS)。  

###  <a name="BKIMK_UpgradeProcess"></a> 發佈點升級程序  
您可以使用 Configuration Manager 主控台，升級您已經與目的地階層共用的 Configuration Manager 2007 發佈點。 當您升級共用的發佈點時，會解除安裝 Configuration Manager 2007 站台的發佈點。 然後，它就會安裝為附加至您在目的地階層中指定的主要或次要站台的發佈點。 升級程序會為儲存在該發佈點上的移轉內容建立副本，然後將此副本轉換成單一執行個體內容存放區。 當 Configuration Manager 將套件轉換成單一執行個體內容存放區時，若該套件的 [從發佈點執行程式] 未設定一或多個公告，就會從發佈點電腦上的 SMSPKG 共用刪除該套件。  

若要升級發佈點，Configuration Manager 會使用設定為從來源站台的 SMS 提供者收集資料的 [來源站台存取帳戶]。 雖然此帳戶只需要站台物件的 [讀取] 權限，即可收集來源站台的資料，它仍必須擁有 [站台] 類別的 [刪除] 和 [修改] 權限，才能在升級期間成功從 Configuration Manager 2007 站台移除發佈點。  

> [!NOTE]  
>  Configuration Manager 一次只能在一個發佈點上，將內容轉換成單一版本儲存。 設定多個發佈點升級時，發佈點會排入佇列等候升級，且一次處理一個。  

升級共用發佈點前，請確認已經移轉所有部署至發佈點的內容。 升級發佈點前未移轉的內容，在升級後就無法在目的地階層中使用。 升級發佈點時，已移轉套件中的內容會轉換成與目的地階層的儲存單一版本相容的格式。  

若要從 Configuration Manager 主控台內升級發佈點，Configuration Manager 2007 站台系統伺服器必須符合以下條件：  

-   發佈點設定和位置皆必須符合升級的資格。  

-   發佈點電腦必須有足夠的磁碟空間，讓內容從 Configuration Manager 2007 內容儲存格式轉換成儲存單一版本格式。 此轉換作業所需的可用磁碟空間相當於儲存在發佈點的最大封裝大小。  

-   發佈點電腦必須執行在目的地階層中支援作為發佈點的作業系統版本。  

    > [!NOTE]  
    >  當 Configuration Manager 檢查發佈點是否適合進行移轉時，不會驗證發佈點電腦的作業系統版本。  

若要升級發佈點，在 [系統管理] 工作區依序展開 [移轉] 和 [來源階層] 節點，然後選取具有要升級之發佈點的站台。 接著，在詳細資料窗格的 [共用發佈點]  索引標籤上選取要升級的發佈點。  

您可以檢視 [符合重新指派資格]  欄位中的狀態，以確認發佈點已經準備好開始升級。  接著，在 Configuration Manager 主控台功能區 [發佈點] 索引標籤上的 [發佈點] 群組中，選取 [重新指派]。 精靈會隨即開啟，您可以用它來完成發佈點的升級。  

升級共用發佈點時，您必須將發佈點指派到您在目的地階層中選定的主要或次要站台。 發佈點升級後，您可以將發佈點作為目的地階層的發佈點來管理，就和您對其他發佈點所做的一樣。  

您可以藉由在 [系統管理] 工作區的 [移轉] 節點下選取 [發佈點移轉] 節點，在 Configuration Manager 主控台中監控發佈點升級的進度。 您也可以檢視在目的地階層的管理中心網站伺服器上 **Migmctrl.log** 中的資訊，或檢視管理已升級發佈點之目的地階層的站台伺服器上 **distmgr.log** 中的資訊。  

> [!NOTE]  
>  當您將發佈點升級至目的地階層時，發佈點站台系統角色就會從 Configuration Manager 2007 來源站台中移除。 不過，在 Configuration Manager 2007 階層中，不會更新已傳送至發佈點的套件。 在 Configuration Manager 2007 主控台中，必須已將套件傳送給發佈點，才能繼續將站台系統電腦列為 [類型] 為 [未知] 的發佈點。 Configuration Manager 2007 套件的後續更新會導致發佈管理員在 distmgr.log 中回報「該站台嘗試在未知站台系統上更新套件」的錯誤。  

若您決定不要升級共用發佈點，還是可以在先前的 Configuration Manager 2007 發佈點上安裝來自目的地階層的發佈點。 您必須先從發佈點電腦解除安裝所有 Configuration Manager 2007 站台系統角色，才能安裝新發佈點。 若這是站台伺服器電腦，則包括 Configuration Manager 2007 站台。 解除安裝 Configuration Manager 2007 發佈點時，部署至發佈點的內容並不會從電腦刪除。  

###  <a name="BKMK_UpgradeSS"></a> 規劃升級 Configuration Manager 2007 次要站台  
 使用移轉來升級 Configuration Manager 2007 次要站台伺服器上裝載的共用發佈點時，Configuration Manager 會將發佈點站台系統角色升級為目的地階層的發佈點。 它也會從來源階層解除安裝次要站台。 結果是 System Center Configuration Manager 發佈點，而不是任何次要站台。  

 若要讓站台伺服器電腦上的發佈點符合升級條件，Configuration Manager 必須能夠解除安裝次要站台和該電腦上的每個站台系統角色。 一般而言，Configuration Manager 2007 伺服器共用上的共用發佈點都符合升級條件。 不過，次要站台伺服器上存在伺服器共用時，該電腦上的次要站台與任何共用發佈點則都不符合升級資格。 這是因為當升級程序嘗試解除安裝次要站台時，會將伺服器共用視為額外的站台系統物件，此程序就無法解除安裝此物件。 在此案例中，您可以在次要站台伺服器上啟用標準發佈點，然後將內容重新發佈到該標準發佈點。 此程序不會佔用網路頻寬，且當此動作完成時，您就可以解除安裝伺服器共用上的發佈點，移除伺服器共用，然後升級發佈點與次要站台。  

 在您升級共用發佈點前，請檢閱 Configuration Manager 2007 中的發佈點設定，以避免升級您還想搭配 Configuration Manager 2007 使用之次要站台上的發佈點。 這是個好方法，因為在升級次要站台伺服器上的共用發佈點後，就會從 Configuration Manager 2007 階層移除站台系統伺服器，之後該階層即無法使用該站台系統伺服器。 移除次要站台時，該次要站台的任何剩餘發佈點皆會遭到孤立。 這代表發佈點變成不受 Configuration Manager 2007 管理，而且也無法再共用或升級。  

> [!WARNING]  
>  當您檢視 Configuration Manager 主控台中的共用發佈點時，不會看到共用發佈點位在遠端站台系統伺服器上或次要站台伺服器上的指示。  

 在遠端網路位置擁有次要站台 (主要用來控制部署至該遠端位置的內容) 時，請考慮升級具備共用發佈點的次要站台。 由於您可以設定將內容發佈至 System Center Configuration Manager 發佈點時的頻寬控制，您可以經常將次要站台升級成發佈點，針對頻寬控制設定發佈點，並避免在目的地階層的網路位置安裝次要站台。  

 升級次要站台伺服器上的共用發佈點的程序，與升級其他共用發佈點相同。 內容會複製及轉換為目的地階層所使用的儲存單一版本。 不過，當您升級次要站台伺服器上的共用發佈點時，升級程序也會解除安裝管理點 (如果有的話)，然後從伺服器解除安裝次要站台。 結果是會從 Configuration Manager 2007 階層移除次要站台。 為了解除安裝次要站台，Configuration Manager 會使用設定來收集來自來源站台資料的帳戶。  

 升級期間，在解除安裝 Configuration Manager 2007 次要站台後，以及開始在目的地階層中安裝發佈點前之間，會發生延遲。 此延遲取決於資料收集週期，最多為 4 個小時。 延遲的目的是為了在開始安裝新的發佈點前，提供解除安裝次要站台的時間。  

 如需如何升級共用發佈點的詳細資訊，請參閱[規劃升級 Configuration Manager 2007 共用發佈點](#Planning_to_Upgrade_DPs)。  

##  <a name="BKMK_ReassignDistPoint"></a> 規劃重新指派 System Center Configuration Manager 發佈點  
 從 System Center 2012 Configuration Manager 的受支援版本移轉至相同版本的階層時，您可以將共用發佈點從來源階層重新指派到目的地階層中的站台。 這與將 Configuration Manager 2007 發佈點升級成目的地階層中發佈點的概念類似。 您可以重新指派主要站台和次要站台的發佈點。 重新指派發佈點的動作會移除來源階層的發佈點，並且使電腦及其發佈點成為您在目的地階層中所選站台的站台系統伺服器。  

 在重新指派發佈點時，您不需要重新發佈裝載在來源站台發佈點上的已移轉內容。 此外，與升級 Configuration Manager 2007 發佈點不同的是，重新指派發佈點的發佈點電腦並不需要有額外的磁碟空間。 這是因為自 System Center 2012 Configuration Manager 開始，發佈點內容會使用單一執行個體存放區格式。 在階層間重新指派發佈點時，不需要轉換發佈點電腦上的內容。  

 若要讓 System Center 2012 Configuration Manager 發佈點符合重新指派的資格，則必須符合下列準則：  

-   共用發佈點必須安裝在電腦上，而非站台伺服器上。  

-   共用發佈點無法與任何額外站台系統角色共置。  

若要在 Configuration Manager 主控台中識別有資格重新指派的發佈點，請在 [來源階層] 節點中選取來源站台，然後選取 [共用發佈點] 索引標籤。 合格發佈點的 [符合重新指派資格] 欄位中會顯示 「是」 (此欄位在 System Center 2012 R2 Configuration Manager 之前的版本中名為 [符合升級資格])。  

###  <a name="BKMK_ReassignProcess"></a> 發佈點重新指派程序  
 您可以使用 Configuration Manager 主控台，從作用中來源階層重新指派您已經共用的發佈點。 重新指派共用發佈點時，會從其來源站台解除安裝發佈點，然後安裝為附加至您在目的地階層中指定之主要或次要站台的發佈點。  

 為重新指派發佈點，目的地階層會使用設定為從來源站台的 SMS 提供者收集資料的 [來源站台存取帳戶]。 如需必要權限和其他必要條件的資訊，請參閱 [Prerequisites for migration in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md) (在 System Center Configuration Manager 中進行移轉的必要條件)。  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>同時移轉多個共用的發佈點
從 1610 版開始，您可以使用 [重新指派發佈點] 同時平行處理 Configuration Manager 程序與最多 50 個共用發佈點的重新指派。 這包括來自執行下列程式的受支援來源站台的共用發佈點︰  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- System Center Configuration Manager (最新分支)

當您重新指派發佈點時，每個發佈點都必須符合升級或重新指派的資格。 無論是升級或重新指派，與動作和程序有關的名稱，取決於來源站台執行的 Configuration Manager 版本。 兩項動作的結果相同︰發佈點會指派給其內容所在的最新分支站台之一。

Configuration Manager 在 1610 版以前，一次只能處理一個發佈點。 現在，只要注意下列幾點，您就可以重新指派多個發佈點，不限數量：  
- 雖然您不能複選要重新指派的發佈點，但當您有多個佇列項目時，Configuration Manager 就會平行處理，而不是等一個完成後再開始下一個。  
- 預設一次最多可以平行處理 50 個發佈點。 第一個發佈點完成重新指派後，Configuration Manager 就會開始處理第 51 個，以此類推。  
- 當您使用 Configuration Manager SDK 時，您可以變更 **SharedDPImportThreadLimit**，調整 Configuration Manager 可以平行處理的重新指派發佈點數目。


##  <a name="About_Migrating_Content"></a> 移轉內容時指派內容的擁有權  
 當您移轉部署的內容時，必須將內容物件指派至目的地階層中的站台。 此站台就會變成目的地階層中該內容的擁有者。 雖然目的地階層的頂層站台是移轉內容中繼資料的站台，但它會是跨網路使用內容原始來源檔案的指派站台。  

 若要將移轉內容時佔用的網路頻寬降到最少，您可以考慮將網路上已封閉之目的地階層中站台的內容擁有權轉換至來源階層的內容位置。 因為關於目的地階層中的內容資訊是全域共用，所有每個站台都可使用。  

 雖然藉由使用資料庫複寫，就能在所有站台上共用內容相關資訊，您指派至主要站台，然後部署到其他主要站台發佈點的內容仍會依照以檔案為基礎的複寫來傳輸。 這項傳輸是透過管理中心網站路由傳送至其他主要站台。 在您將站台指派為內容擁有者時，藉由在移轉前或移轉期間，將您規劃發佈至多個主要站台的套件集中化，就能跨低頻寬網路來降低資料傳輸量。
