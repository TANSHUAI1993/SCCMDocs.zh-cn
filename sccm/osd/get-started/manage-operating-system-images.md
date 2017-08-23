---
title: "管理作業系統映像 | Microsoft Docs"
description: "在 Configuration Manager 中，深入了解儲存在 Windows 映像處理 (WIM) 檔案中的作業系統映像管理方法。"
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
caps.latest.revision: "17"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6953c3834ca303b949f22436010a87b3da9688dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理作業系統映像

*適用對象：System Center Configuration Manager (最新分支)*

Configuration Manager 中的作業系統映像儲存為 Windows 映像 (WIM) 檔案格式，代表經過壓縮的參照檔案和資料夾集合，其為成功在電腦上安裝及設定作業系統所必需。 在所有作業系統部署案例中，您都必須選取作業系統映像。   您可以使用預設的作業系統映像，或從您設定的參照電腦建置作業系統映像。 當您建立參照電腦時，您可以先將作業系統檔案、驅動程式、支援檔案、軟體更新、工具和其他軟體應用程式加入此作業系統，之後再擷取以建立映像檔。 以下提供每個方法的相關資訊。  

 **預設映像**  

 預設作業系統映像 (install.wim) 隨附於 Windows 作業系統安裝檔案。 這個映像是包含一組標準驅動程式的基本作業系統映像。 當您使用預設的作業系統映像時，您可以安裝應用程式，並在使用工作順序步驟安裝作業系統之後，進行其他組態。  預設的作業系統映像位於 <*作業系統來源路徑*>\Sources\install.wim。  

-   **優點**  

    -   映像的大小會小於擷取的映像大小。  

    -   使用工作順序步驟安裝應用程式與組態更具動態。 例如，您可以變更將安裝的應用程式和工作順序中的組態，而不需要重新建立作業系統映像。  

-   **缺點**  

    -   由於應用程式安裝和其他組態會在作業系統安裝完成後進行，所以作業系統安裝可能需要更多的時間。  

 **擷取的映像**  

 若要建立自訂的作業系統映像，您必須建置具備所需作業系統的參照電腦，以及安裝應用程式和設定組態等。然後，您可以從參照電腦擷取作業系統映像，以建立 WIM 檔案。 您可以手動建立參照電腦，也可以使用工作順序將部分或所有建立步驟自動化。   
如需建立自訂之作業系統映像的步驟，請參閱 [Customize operating system images](customize-operating-system-images.md) (使用 System Center Configuration Manager 自訂作業系統映像)。  

-   **優點**  

    -   此種安裝可以比使用預設映像更快。 例如，應用程式可使用擷取的作業系統映像預先安裝，而您稍後將不需使用工作順序步驟安裝應用程式。  

-   **缺點**  

    -   由於應用程式安裝和其他組態會在作業系統安裝完成後進行，所以作業系統安裝可能需要更多的時間。  


##  <a name="BKMK_AddOSImages"></a> 將作業系統映像加入 Configuration Manager  
 在您可以使用作業系統映像之前，必須先將此映像加入 Configuration Manager 站台。 請使用下列程序將作業系統映像加入站台。  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>將作業系統映像加入站台  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [作業系統映像] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增作業系統映像]  啟動 [新增作業系統映像精靈]。  

4.  在 [資料來源]  頁面上，指定作業系統映像的網路路徑。 例如指定 **\\\server\path\OS.WIM**。  

5.  在 [一般]  頁面上指定下列資訊，然後按 [下一步] 。 這項資訊可在新增多個作業系統映像至相同站台時做為識別用途。  

    -   **名稱**：指定映像的名稱。 根據預設，映像的名稱取自 WIM 檔。  

    -   **版本**：指定映像的版本。  

    -   **註解**：指定映像的簡短描述。  

6.  完成精靈。  

 您現在可以將作業系統映像發佈至發佈點。  

##  <a name="BKMK_DistributeBootImages"></a> 將作業系統映像發佈至發佈點  
 作業系統映像發佈至發佈點的方式，與您發佈其他內容的方式相同。 在大部分情況下，您必須在部署作業系統之前，將作業系統映像發佈至至少一個發佈點。 如需發佈作業系統映像的步驟，請參閱 [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

##  <a name="BKMK_OSImagesApplyUpdates"></a> 將軟體更新套用至作業系統映像  
 適用於作業系統映像中作業系統的新軟體更新會定期發行。 在您可將軟體更新套用至映像之前，必須先使軟體更新基礎結構就緒、已成功同步處理軟體更新，並已將軟體更新下載至站台伺服器上的內容庫。 如需詳細資訊，請參閱 [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (部署軟體更新)。  

 您可以依指定的排程將適用的軟體更新套用至映像。 依照您指定的排程，Configuration Manager 會將您選取的軟體更新套用至作業系統映像，然後選擇性地將更新映像發佈至發佈點。 有關作業系統映像的資訊會儲存在站台資料庫中，包括匯入時已套用的軟體更新。 最初新增時已套用至映像的軟體更新也會儲存在站台資料庫中。 當您啟動精靈將軟體更新套用至作業系統映像時，精靈會擷取尚未套用至映像的可用軟體更新清單供您選取。 Configuration Manager 會從站台伺服器上的內容庫複製軟體更新，並將此軟體更新套用至作業系統映像。  

 利用下列程序將軟體更新套用至作業系統映像。  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>將軟體更新套用至作業系統映像  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [作業系統映像] 。  

3.  選取要套用軟體更新的作業系統映像。  

4.  在 [首頁]  索引標籤的 [作業系統映像]  群組中，按一下 [排程更新]  啟動精靈。  

5.  在 [選擇更新]  頁面上，選取要套用至作業系統映像的軟體更新，然後按 [下一步] 。  

6.  在 [設定排程]  頁面上指定下列設定，然後按 [下一步] 。  

    1.  **排程**：指定將軟體更新套用至作業系統映像的排程。  

    2.  **發生錯誤時繼續**：選取此選項，即使發生錯誤仍會將軟體更新套用至映像。  

    3.  **將映像發佈至發佈點**：選取此選項，在套用軟體更新之後更新發佈點上的作業系統映像。  

7.  確認 [摘要]  頁面中的資訊，然後按 [下一步] 。  

8.  在 [完成]  頁面上，確認軟體更新已成功套用至作業系統映像。  

##  <a name="BKMK_OSImageMulticast"></a> 準備多點傳送部署的作業系統映像  
 使用多點傳送部署，以允許多部電腦同時下載作業系統映像。 此映像檔由發佈點多點傳送至用戶端，而不是讓發佈點透過個別連線，傳送映像複本至每個用戶端。 當您選擇[使用多點傳送透過網路來部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) 作業系統部署方法時，必須將作業系統映像套件設定為支援多點傳送，然後將其發佈到啟用多點傳送的發佈點。 利用下列程序，為現有的作業系統映像套件設定多點傳送選項。  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>將作業系統映像套件修改為使用多點傳送  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [作業系統映像] 。  

3.  選取您要發佈至支援多點傳送之發佈點的作業系統映像。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  選取 [發佈設定]  索引標籤，並設定下列選項：  

    -   **允許透過多點傳送來傳送此套件 (僅適用於 WinPE)**：您必須針對 Configuration Manager 選取此選項，才能同時部署作業系統映像。  

    -   **加密多點傳送套件**：指定是否要在將映像傳送至發佈點前，先對映像進行加密。 如果套件包含敏感資訊，請使用此選項。 如果映像未加密，套件的內容會以純文字在網路上傳送，並且可能會被未經授權的使用者讀取。  

    -   **僅透過多點傳送傳送此套件**：指定是否只要在多點傳送工作階段期間，讓發佈點部署映像。  

         如果您選取 [僅透過多點傳送傳送此套件] ，則必須同時指定 [執行工作順序以視需要將內容下載到本機]  作為作業系統映像的部署選項。 您可以在部署作業系統映像時指定映像的部署選項，或者稍後再編輯部署的內容以指定這些選項。 這些部署選項位於部署物件 [內容]  頁面的 [發佈點]  索引標籤上。  

6.  按一下 [ **確定**]。  
