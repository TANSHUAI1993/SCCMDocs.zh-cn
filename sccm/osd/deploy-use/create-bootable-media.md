---
title: "建立可開機媒體 - Configuration Manager | Microsoft Docs"
description: "Configuration Manager 中的可開機媒體讓您更容易安裝新版的 Windows 或取代電腦和傳輸設定。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9032698fa12bf453041ea06bf330d3b4687c2a97
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立可開機媒體

*適用於︰System Center Configuration Manager (最新分支)*

Configuration Manager 中的可開機媒體包含開機映像、選擇性的啟動前置命令和相關聯檔案，以及 Configuration Manager 檔案。 針對下列作業系統部署案例，使用預先設置的媒體：  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> 建立可開機媒體  
 當您將可開機媒體開機時，目的地電腦會啟動、連線至網路，並從網路擷取指定的工作順序、作業系統映像，以及任何其他必要的內容。 由於工作順序不在媒體上，因此不需要重新建立媒體即可變更工作順序或內容。 可開機媒體上的套件並未加密。 您必須採取適當的安全防護措施 (例如新增媒體密碼)，以確保未經授權的使用者無法存取套件內容。  

 使用 [建立工作順序媒體精靈] 建立可開機媒體之前，請先確定符合下列所有條件：  

|工作|說明|  
|----------|-----------------|  
|開機映像|請考慮下列開機映像相關資訊，您將在工作順序中使用開機映像來擷取作業系統：<br /><br /> -   開機映像的架構必須適用於目的地電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。<br />-   確定開機映像包含佈建目的地電腦所需的網路及大型存放驅動程式。|  
|建立部署作業系統的工作順序|作為可開機媒體的一部分，您必須指定工作順序以部署作業系統。 如需建立新工作順序的步驟，請參閱[建立工作順序以安裝作業系統](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)。|  
|發佈與工作順序相關聯的所有內容|您必須將工作順序所需的所有內容都發佈到至少一個發佈點。 這包括開機映像，以及其他相關聯的啟動前置檔案。 精靈會在建立可開機媒體時從發佈點收集資訊。 您必須擁有該發佈點上內容庫的 [讀取]  存取權限。  如需詳細資訊，請參閱[關於內容庫](../../core/plan-design/hierarchy/the-content-library.md)。|  
|準備卸除式 USB 磁碟機|針對卸除式 USB 磁碟機：<br /><br /> 如果您即將使用卸除式 USB 磁碟機，USB 磁碟機必須連接至精靈執行所在的電腦，並作為卸除式裝置讓 Windows 能夠偵測到。 精靈會在建立媒體時直接寫入 USB 磁碟機。 獨立媒體使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 的檔案的 USB 快閃磁碟機上建立獨立媒體。|  
|建立輸出資料夾|針對 CD/DVD 組：<br /><br /> 在您執行 [建立工作順序媒體精靈] 建立 CD 或 DVD 組的媒體之前，必須先為精靈所建立的輸出檔案建立資料夾。 針對 CD 或 DVD 組所建立的媒體會做為 .iso 檔直接寫入該資料夾中。|  

 利用下列程序建立可開機媒體。  

### <a name="to-create-bootable-media"></a>若要建立可開機媒體  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序媒體]  以啟動 [建立工作順序媒體精靈]。  

4.  在 [選取媒體類型]  頁面指定下列選項，然後按 [下一步] 。  

    -   選取 [可開機媒體] 。  

    -   如果您只想要允許部署作業系統，而不需要使用者輸入，可以選擇性地選取 [允許自動部署作業系統] 。  

        > [!IMPORTANT]  
        >  當您選取此選項時，就不會提示使用者提供網路組態資訊或選用的工作順序。 不過，如果媒體已設定為使用密碼保護，仍會提示使用者輸入密碼。  

5.  在 [媒體管理]  頁面上指定下列選項，然後按 [下一步] 。  

    -   如果您想要允許管理點根據網站界限的用戶端位置將媒體重新導向至其他管理點，請選取 [動態媒體]  。  

    -   如果只想要讓媒體與指定的管理點連繫，請選取 [以網站為基礎的媒體]  。  

6.  在 [媒體類型]  頁面上，指定媒體是快閃磁碟機還是 CD/DVD 組，然後按一下以設定下列項目：  

    > [!IMPORTANT]  
    >  獨立媒體使用 FAT32 檔案系統。 您無法在內容包含大小超過 4 GB 的檔案的 USB 快閃磁碟機上建立獨立媒體。  

    -   如果您選取 [USB 快閃磁碟機] ，請指定要在其中儲存內容的磁碟機。  

    -   如果您選取 [CD/DVD 組] ，請指定媒體容量及輸出檔案的名稱和路徑。 精靈會將輸出檔案寫入此位置。 例如︰**\\\servername\folder\outputfile.iso**  

         如果媒體容量太小，無法儲存整個內容，則會建立多個檔案，而且您必須將內容儲存到多個 CD 或 DVD 上。 需要多個媒體時，Configuration Manager 會在其建立的每個輸出檔案名稱上新增序號。 此外，如果您同時部署應用程式與作業系統，且應用程式無法完全安裝在單一媒體上，Configuration Manager 會將應用程式儲存在多個媒體上。 獨立媒體執行時，Configuration Manager 會提示使用者儲存應用程式的下一個媒體。  

        > [!IMPORTANT]  
        >  如果您選取現有的 .iso 映像，[工作順序媒體精靈] 會在您繼續進行精靈的下一頁時從磁碟機或共用刪除映像。 即使您取消精靈，還是會刪除現有映像。  

     按一下 [下一步] 。  

7.  在 [安全性]  頁面上指定下列選項，然後按 [下一步] 。  

    -   選取 [啟用未知電腦支援] 核取方塊，可讓媒體將作業系統部署至未受 Configuration Manager 管理的電腦。 這類電腦在 Configuration Manager 資料庫中沒有任何相關記錄。  

         未知電腦包括：  

        -   未安裝 Configuration Manager 用戶端的電腦  

        -   未匯入 Configuration Manager 的電腦  

        -   Configuration Manager 未探索到的電腦  

    -   選取 [使用密碼保護媒體]  核取方塊並輸入強式密碼，可幫助保護媒體不受未經授權的存取。 當您指定密碼時，使用者必須提供該密碼才能使用可開機媒體。  

        > [!IMPORTANT]  
        >  基於安全性最佳作法，一律指派密碼保護可開機媒體。  

    -   對於 HTTP 通訊，請選取 [建立自我簽署媒體憑證] ，然後指定憑證的開始日和到期日。  

    -   對於 HTTPS 通訊，請選取 [匯入 PKI 憑證] ，然後指定要匯入的憑證及其密碼。  

         如需開機映像所使用之此用戶端憑證的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    -   **使用者裝置親和性**：若要在 Configuration Manager 中支援使用者為中心的管理，請指定要如何讓媒體為使用者與目的地電腦建立關聯。 如需作業系統部署如何支援使用者裝置親和性的詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

        -   如果要讓媒體自動為使用者與目的地電腦建立關聯，請指定 [允許自動核准使用者裝置親和性]  。 此功能是以作業系統部署工作順序的動作為基礎。 在此案例中，工作順序會在將作業系統部署至目的地電腦時，為指定的使用者和目的地電腦建立關聯性。  

        -   如果您希望媒體在授與核准後讓使用者與目的地電腦產生關聯，請指定 [允許使用者親和性等待系統管理員核准]  。 此功能是以部署作業系統的工作順序範圍為基礎。  在此案例中，工作順序會建立指定的使用者與目的地電腦之間的關聯性，但是會等候系統管理使用者核准，才部署作業系統。  

        -   如果您不希望媒體讓使用者與目的地電腦產生關聯，請指定 [不允許使用者裝置親和性]  。 在此案例中，工作順序在部署作業系統時，就不會將使用者與目的地電腦產生關聯。  

8.  在 [開機映像]  頁面指定下列選項，然後按 [下一步] 。  

    > [!IMPORTANT]  
    >  已發佈之開機映像的架構，必須適用於目的地電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。  

    -   在 [開機映像]  方塊中，指定要啟動目的地電腦的開機映像。  

    -   在 [發佈點]  方塊中，指定開機映像所在的發佈點。 精靈會從發佈點擷取開機映像，並將其寫入至媒體。  

        > [!NOTE]  
        >  您必須擁有發佈點上內容庫的 [讀取]  存取權限。  

    -   如果在精靈 [媒體管理]  頁面上建立了以站台為基礎的可開機媒體，請在 [管理點]  方塊中，指定來自主要網站的管理點。  

    -   如果在精靈的 [媒體管理]  頁面中建立了動態可開機媒體，請在 [相關聯的管理點] 中指定要使用的主要站台管理點，以及初始通訊的優先順序。  

9. 在 [自訂]  頁面上指定下列選項，然後按 [下一步] 。  

    -   指定工作順序用於部署作業系統的變數。  

    -   指定您要在工作順序執行前執行的啟動前置命令。 啟動前置命令是在執行工作順序以安裝作業系統前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 如需詳細資訊，請參閱[工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        >  在建立工作順序媒體時，工作順序會將套件識別碼和啟動前置命令列 (包括任何工作順序變數的值) 寫入執行 Configuration Manager 主控台之電腦的 CreateTSMedia.log 記錄檔中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

         您也可以選取 [包含啟動前置命令的檔案]  核取方塊，將任何啟動前置命令所需的檔案加入。  

10. 完成精靈。  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>從網路共用在 USB 磁碟機上建立可開機媒體
本節的資訊可協助您在 USB 快閃磁碟機未連線到執行 Configuration Manager 主控台的電腦時，在 USB 快閃磁碟機上建立可開機媒體。 若要在 USB 磁碟機上建立可開機媒體，您可以建立工作順序開機媒體、掛接 ISO，並從 ISO 傳輸檔案到 USB 磁碟機。

1. [建立工作順序開機媒體](#to-create-task-boobable-media)。 在 [媒體類型] 頁面上，選取 [CD/DVD 組]。 精靈會將輸出檔案寫入您指定的位置。 例如︰**\\\伺服器名稱\資料夾\outputfile.iso**。  
2. 準備卸除式 USB 磁碟機。 磁碟機必須格式化、清空且可開機。
3. 從共用位置掛接 ISO，並將檔案從 ISO 傳送到 USB 磁碟機。

## <a name="next-steps"></a>後續步驟  
[透過網路使用可開機媒體部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  
