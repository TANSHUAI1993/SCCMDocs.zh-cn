---
title: "使用 System Center Configuration Manager 建立預先設置的媒體 | Microsoft Docs"
description: "在 System Center Configuration Manager 中建立預先設置的媒體，以簡化數個案例中的 Windows 部署。"
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 33abf3853d912d423e427db4d35fb4a16167164e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立預先設置的媒體

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中預先設置的媒體是 Windows 映像格式 (WIM) 檔案，可由廠商或在企業設置中心安裝於未連線 Configuration Manager 環境的裸機電腦。  
預先設置的媒體包含用於啟動目的地電腦的開機映像，以及將套用於目的地電腦的作業系統映像。 您也可以指定在預先設置的媒體中加入應用程式、套件及驅動程式套件。 媒體中不包含部署作業系統的工作順序。 將電腦交給使用者之前，即需將預先設置的媒體套用至新電腦的硬碟中。 針對下列作業系統部署案例，使用預先設置的媒體：  

-   [建立 OEM 原廠或本機 Depot 的映像](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [部署 Windows to Go](deploy-windows-to-go.md)  

 在電腦套用預先設置媒體後第一次啟動時，電腦會啟動 Windows PE 並連線至管理點，尋找能完成作業系統部署程序的工作順序。 您可以指定在預先設置的媒體中加入應用程式、封裝及驅動程式封裝。 部署使用預先設置媒體的工作順序時，精靈會先檢查本機工作順序快取中的有效內容，如果找不到有效內容，或者內容已經過修改，則精靈會從發佈點下載內容。  

##  <a name="BKMK_CreatePrestagedMedia"></a> 如何建立預先設置的媒體  
 使用 [建立工作順序媒體精靈] 建立預先設置的媒體之前，請先確定符合下列所有條件：  

|工作|說明|  
|----------|-----------------|  
|開機映像|請考慮下列開機映像相關資訊，您將在工作順序中使用開機映像來擷取作業系統：<br /><br /> -   開機映像的架構必須適用於目的地電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。<br />-   確定開機映像包含佈建目的地電腦所需的網路及大型存放驅動程式。|  
|建立部署作業系統的工作順序|作為預先設置媒體的一部分，您必須指定工作順序以部署作業系統。<br /><br /> -   如需建立新工作順序的步驟，請參閱[建立工作順序以安裝作業系統](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md)。<br />-   如需工作順序的詳細資訊，請參閱[管理工作順序以自動化工作](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)。|  
|發佈與工作順序相關聯的所有內容|您必須將工作順序所需的所有內容都發佈到至少一個發佈點。 這包括開機映像、作業系統映像，以及其他相關聯的檔案。 精靈會在建立獨立媒體時從發佈點收集資訊。 您必須擁有該發佈點上內容庫的 [讀取]  存取權限。  如需詳細資訊，請參閱[關於內容庫](../../core/plan-design/hierarchy/the-content-library.md)。|  
|目的電腦上的硬碟機|目的地電腦的硬碟機必須先格式化，再將預先設置的媒體分段安裝至電腦的硬碟機上。 如果在套用媒體時硬碟機未進行格式化，部署作業系統的工作順序在嘗試啟動目的地電腦時將會失敗。|  

> [!NOTE]  
>  [建立工作順序媒體精靈] 會在媒體上設定下列工作順序變數條件：**_SMSTSMediaType = OEMMedia**。 您可以在工作順序中使用這個條件。  

 利用下列程序建立預先設置的媒體。  

#### <a name="to-create-prestaged-media"></a>建立預先設置的媒體  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序媒體]  以啟動 [建立工作順序媒體精靈]。  

4.  在 [選取媒體類型]  頁面上指定下列資訊，然後按 [下一步] 。  

    -   選取 [預先設置的媒體] 。  

    -   如果您想要允許作業系統在不需使用者輸入的情況下進行部署，便可選取 [允許自動部署作業系統] 。 當您選取此選項時，系統不會提示使用者輸入網路設定資訊或選用的工作順序。 不過，如果媒體已設定為使用密碼保護，仍會提示使用者輸入密碼。  

5.  在 [媒體管理]  頁面上指定下列資訊，然後按 [下一步] 。  

    -   如果您想要允許管理點根據網站界限的用戶端位置將媒體重新導向至其他管理點，請選取 [動態媒體]  。  

    -   如果只想要讓媒體與指定的管理點連繫，請選取 [以網站為基礎的媒體]  。  

6.  在 [媒體內容]   頁面上指定下列資訊，然後按 [下一步] 。  

    -   **建立者**：指定媒體的建立者。  

    -   **版本**：指定媒體的版本號碼。  

    -   **註解**：指定媒體用途的唯一描述。  

    -   **媒體檔案**：指定輸出檔案的名稱和路徑。 精靈會將輸出檔案寫入此位置。 例如︰**\\\伺服器名稱\資料夾\outputfile.wim**  

7.  在 [安全性]  頁面指定下列資訊，然後按 [下一步] 。  

    -   選取 [啟用未知電腦支援] 核取方塊，可讓媒體將作業系統部署至未受 Configuration Manager 管理的電腦。 這類電腦在 Configuration Manager 資料庫中沒有任何相關記錄。  如需詳細資訊，請參閱[準備未知電腦部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

    -   選取 [使用密碼保護媒體]  核取方塊並輸入強式密碼，可幫助保護媒體不受未經授權的存取。 當您指定密碼時，使用者必須提供密碼才能使用預先設置的媒體。  

        > [!IMPORTANT]  
        >  為安全起見，請一律指定密碼，協助保護預先設置媒體。  

    -   對於 HTTP 通訊，請選取 [建立自我簽署媒體憑證] ，然後指定憑證的開始日和到期日。  

    -   對於 HTTPS 通訊，請選取 [匯入 PKI 憑證] ，然後指定要匯入的憑證及其密碼。  

         如需開機映像所使用之此用戶端憑證的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    -   **使用者裝置親和性**：若要在 Configuration Manager 中支援使用者為中心的管理，請指定要如何讓媒體為使用者與目的地電腦建立關聯。 如需作業系統部署如何支援使用者裝置親和性的詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

        -   如果要讓媒體自動為使用者與目的地電腦建立關聯，請指定 [允許自動核准使用者裝置親和性]  。 此功能是以作業系統部署工作順序的動作為基礎。 在此案例中，工作順序會在將作業系統部署至目的地電腦時，為指定的使用者和目的地電腦建立關聯性。  

        -   如果您希望媒體在授與核准後讓使用者與目的地電腦產生關聯，請指定 [允許使用者親和性等待系統管理員核准]  。 此功能是以部署作業系統的工作順序範圍為基礎。 在此案例中，工作順序會建立指定的使用者與目的地電腦之間的關聯性，但是會等候系統管理使用者核准，才部署作業系統。  

        -   如果您不希望媒體讓使用者與目的地電腦產生關聯，請指定 [不允許使用者裝置親和性]  。 在此案例中，工作順序在部署作業系統時，就不會將使用者與目的地電腦產生關聯。  

8.  在 [工作順序]  頁面上，指定目的地電腦要執行的工作順序。 工作順序所參照的內容會顯示在 [此工作順序參照下列內容] 中。 確認內容，然後按一下 [下一步] 。  

9. 在 [開機映像]  頁面上指定下列資訊，然後按 [下一步] 。  

    > [!IMPORTANT]  
    >  已發佈之開機映像的架構，必須適用於目的地電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。  

    -   在 [開機映像]  方塊中，指定要啟動目的地電腦的開機映像。 如需詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

    -   在 [發佈點]  方塊中，指定開機映像所在的發佈點。 精靈會從發佈點擷取開機映像，並將其寫入至媒體。  

        > [!NOTE]  
        >  您必須擁有發佈點上內容庫的 [讀取]  存取權限。 如需詳細資訊，請參閱[關於內容庫](../../core/plan-design/hierarchy/the-content-library.md)。  

    -   如果您在此精靈的 [媒體管理]  頁面中選取 [以站台為基礎的媒體]  ，請在 [管理點]  方塊中指定主要站台的管理點。  

    -   如果在精靈的 [媒體管理]  頁面中選取了 [動態媒體]  ，請在 [相關聯的管理點]  方塊中指定要使用的主要站台管理點，以及初始通訊的優先順序。  

10. 在 [映像]  頁面上指定下列資訊，然後按 [下一步] 。  

    -   在 [映像套件]  方塊中，指定作業系統映像。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  

    -   如果套件包含多個作業系統映像，請在 [映像索引]  方塊中指定要部署的映像。  

    -   在 [發佈點]  方塊中，指定作業系統映像套件所在的發佈點。 精靈會從發佈點擷取作業系統映像，並將其寫入至媒體。  

11. 在 [自訂]  頁面指定下列資訊，然後按 [下一步] 。  

    -   指定工作順序用於部署作業系統的變數。  

    -   指定您要在工作順序執行前執行的啟動前置命令。 啟動前置命令是在執行工作順序以安裝作業系統前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 如需媒體之啟動前置命令的詳細資訊，請參閱[工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        >  在建立工作順序媒體時，工作順序會將套件識別碼和啟動前置命令列 (包括任何工作順序變數的值) 寫入執行 Configuration Manager 主控台之電腦的 CreateTSMedia.log 記錄檔中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

12. 完成精靈。  

## <a name="next-steps"></a>後續步驟
[部署企業作業系統的案例](scenarios-to-deploy-enterprise-operating-systems.md)
