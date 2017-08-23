---
title: "使用 System Center Configuration Manager 部署 Windows To Go | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中佈建 Windows To Go，建立從外部磁碟機開機的 Windows To Go 工作區。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a8b1a42c43438553cfbb62328bed933378bb344c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-windows-to-go-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 部署 Windows To Go

*適用於：System Center Configuration Manager (最新分支)*

本主題說明在 System Center Configuration Manager 中佈建 Windows To Go 的步驟。 Windows To Go 是 Windows 8 的企業版功能，可用於建立 Windows To Go 工作區，無論電腦執行哪一種作業系統，只要符合 Windows 7 或 Windows 8 的憑證需求，就可以從以 USB 連接的外部磁碟機啟動 Windows To Go 工作區。 Windows To Go 工作區可以使用企業應用於桌上型電腦和膝上型電腦的映像，管理方法也相同。  

 如需 Windows To Go 的詳細資訊，請參閱 [Windows To Go 功能概觀](http://go.microsoft.com/fwlink/p/?LinkId=263433)。  

## <a name="provision-windows-to-go"></a>佈建 Windows To Go  
 Windows To Go 是儲存在 USB 連接的外部磁碟機中的作業系統。 佈建 Windows To Go 磁碟機的方式與佈建其他作業系統部署的方式相似。 不過，由於 Windows To Go 的設計是以使用者為中心，而且是具高度機動性的解決方案，因此必須運用稍微不同的方法佈建這些磁碟機。  

 就高層級而言，Windows To Go 是分為兩個階段的部署，可讓您設定 Windows To Go 裝置及用於部署作業系統的預先設置內容。 您可以在盡量不影響使用者及縮短使用者電腦停機時間的情況下完成這項部署。 預先設置電腦後，您必須完成佈建程序，確保電腦準備就緒，可供使用者使用。 佈建程序與目前的作業系統部署程序相似。 以下列出預先設置內容和佈建 Windows To Go 的一般工作流程：  

1.  [佈建 Windows To Go 的必要條件](#BKMK_Prereqs)  

2.  [建立預先設置的媒體](#BKMK_CreatePrestagedMedia)  

3.  [建立 Windows To Go Creator 套件](#BKMK_CreatePackage)  

4.  [更新工作順序以啟用 Windows To Go 的 BitLocker](#BKMK_UpdateTaskSequence)  

5.  [部署 Windows To Go Creator 套件和工作順序](#BKMK_Deployments)  

6.  [使用者執行 Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager 設定與設置 Windows To Go 磁碟機](#BKMK_ConfigureStageDrive)  

8.  [使用者登入 Windows 8](#BKMK_UserLogsIn)  

###  <a name="BKMK_Prereqs"></a> 佈建 Windows To Go 的必要條件  
 佈建 Windows To Go 之前，必須在 Configuration Manager 中完成下列步驟：  

-   **將開機映像發佈至發佈點**  

     建立預先設置媒體之前，您必須將開機映像發佈至發佈點。  

    > [!NOTE]  
    >  開機映像可用來將作業系統安裝到您 Configuration Manager 環境中的目的地電腦。 開機映像中包含某個 Windows PE 版本，會安裝作業系統以及任何其他必要的裝置驅動程式。 Configuration Manager 提供兩種開機映像：一種支援 x86 平台，另一種支援 x64 平台。 您也可以自行建立開機映像。 如需詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

-   **將 Windows 8 作業系統映像發佈至發佈點**  

     建立預先設置媒體之前，必須將 Windows 8 作業系統映像發佈至發佈點。  

    > [!NOTE]  
    >  作業系統映像均為 WIM 格式的檔案，代表經過壓縮的參照檔案和資料夾集合，必須要有 WIM 檔案，才能成功地在電腦上安裝及設定作業系統。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  

-   **建立部署 Windows 8 的工作順序**  

     您必須建立用於部署 Windows 8 的工作順序，當您建立預先設置媒體時將參照此工作順序。 如需詳細資訊，請參閱[管理工作順序，將工作自動化](manage-task-sequences-to-automate-tasks.md)。  

###  <a name="BKMK_CreatePrestagedMedia"></a> 建立預先設置的媒體  
 預先設置的媒體包含用於啟動目的地電腦的開機映像，以及將套用於目的地電腦的作業系統映像。 您可以使用開機映像啟動以預先設置媒體佈建的電腦。 之後，該電腦可以執行現有的作業系統部署工作順序，以安裝完整的作業系統部署。 媒體中不包含部署作業系統的工作順序。  

 除了作業系統映像和開機映像之外，您還可以在預先設置階段新增應用程式和裝置驅動程式之類的內容。 這樣可以縮短部署作業系統所需的時間，並且可以減少網路流量，因為內容已經存放在磁碟機中了。  

 利用下列程序建立預先設置媒體。  

#### <a name="to-create-prestaged-media"></a>建立預先設置的媒體  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序媒體]  以啟動 [建立工作順序媒體精靈]。  

4.  在 [選取媒體類型]  頁面上指定下列資訊，然後按 [下一步] 。  

    -   選取 [預先設置的媒體] 。  

    -   選取 [允許自動部署作業系統]  ，在不需使用者互動的情況下開機進入 Windows To Go 部署。  

        > [!IMPORTANT]  
        >  搭配使用此選項和 SMSTSPreferredAdvertID 自訂變數 (會在此程序中稍後設定)，不需使用者互動，而且電腦會在偵測到 Windows To Go 磁碟機時自動開機進入 Windows To Go 部署。 如果媒體已設定密碼保護，仍然會提示使用者輸入密碼。 如果使用 [允許自動部署作業系統]  設定，但未設定 SMSTSPreferredAdvertID 變數，當您部署工作順序時便會出現錯誤。  

5.  在 [媒體管理]  頁面上指定下列資訊，然後按 [下一步] 。  

    -   如果您想要允許管理點根據網站界限的用戶端位置將媒體重新導向至其他管理點，請選取 [動態媒體]  。  

    -   如果只想要讓媒體與指定的管理點連繫，請選取 [以網站為基礎的媒體]  。  

6.  在 [媒體內容]   頁面上指定下列資訊，然後按 [下一步] 。  

    -   **建立者**：指定媒體的建立者。  

    -   **版本**：指定媒體的版本號碼。  

    -   **註解**：指定媒體用途的唯一描述。  

    -   **媒體檔案**：指定輸出檔案的名稱和路徑。 精靈會將輸出檔案寫入此位置。 例如︰**\\\伺服器名稱\資料夾\outputfile.wim**  

7.  在 [安全性]  頁面指定下列資訊，然後按 [下一步] 。  

    -   選取 [啟用未知電腦支援]，可讓媒體將作業系統部署至未受 Configuration Manager 管理的電腦。 Configuration Manager 資料庫中沒有這些電腦的記錄。 未知電腦包括：  

        -   未安裝 Configuration Manager 用戶端的電腦  

        -   未匯入 Configuration Manager 的電腦  

        -   Configuration Manager 未探索到的電腦  

    -   選取 [使用密碼保護媒體]  ，然後輸入強式密碼，協助防範他人未經授權存取媒體。 當您指定密碼時，使用者必須提供密碼才能使用預先設置的媒體。  

        > [!IMPORTANT]  
        >  為安全起見，請一律指定密碼，協助保護預先設置媒體。  

        > [!NOTE]  
        >  使用密碼保護預先設置媒體時，即使媒體的設定為 [允許自動部署作業系統]  ，仍然會提示使用者輸入密碼。  

    -   對於 HTTP 通訊，請選取 [建立自我簽署媒體憑證] ，然後指定憑證的開始日和到期日。  

    -   對於 HTTPS 通訊，請選取 [匯入 PKI 憑證] ，然後指定要匯入的憑證及其密碼。  

         如需開機映像所使用之此用戶端憑證的詳細資訊，請參閱 [PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    -   **使用者裝置親和性**：若要在 Configuration Manager 中支援使用者為中心的管理，請指定要如何讓媒體為使用者與目的地電腦建立關聯。 如需作業系統部署如何支援使用者裝置親和性的詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

        -   如果要讓媒體自動為使用者與目的地電腦建立關聯，請指定 [允許自動核准使用者裝置親和性]  。 此功能是以作業系統部署工作順序的動作為基礎。 在此案例中，工作順序會在將作業系統部署至目的地電腦時，為指定的使用者和目的地電腦建立關聯性。  

        -   如果您希望媒體在授與核准後讓使用者與目的地電腦產生關聯，請指定 [允許使用者親和性等待系統管理員核准]  。 此功能是以部署作業系統的工作順序範圍為基礎。 在此案例中，工作順序會建立指定的使用者與目的地電腦之間的關聯性，但是會等候系統管理使用者核准，才部署作業系統。  

        -   如果您不希望媒體讓使用者與目的地電腦產生關聯，請指定 [不允許使用者裝置親和性]  。 在此案例中，工作順序在部署作業系統時，就不會將使用者與目的地電腦產生關聯。  

8.  在 [工作順序]  頁面中，指定您在上一節中建立的 Windows 8 工作順序。  

9. 在 [開機映像]  頁面上指定下列資訊，然後按 [下一步] 。  

    > [!IMPORTANT]  
    >  已發佈之開機映像的架構，必須適用於目的地電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。 若是在 EFI 模式下的 Windows 8 認證電腦，必須使用 x64 開機映像。  

    -   **開機映像**：指定用於啟動目的地電腦的開機映像。  

    -   **發佈點**：指定裝載開機映像的發佈點。 精靈會從發佈點擷取開機映像，並將其寫入至媒體。  

        > [!NOTE]  
        >  系統管理使用者必須具備 [讀取]  存取權限，才能存取發佈點上的開機映像內容。 如需詳細資訊，請參閱[管理帳戶以存取內容](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)。  

    -   如果您在此精靈的 [媒體管理]  頁面中選取 [以站台為基礎的媒體]  ，請在 [管理點]  方塊中指定從主要站台進行管理的管理點。  

    -   如果在精靈的 [媒體管理]  頁面中選取了 [動態媒體]  ，請在 [相關聯的管理點]  方塊中指定欲使用的主要站台管理點，以及初始通訊的優先順序。  

10. 在 [映像]  頁面上指定下列資訊，然後按 [下一步] 。  

    -   **映像封裝**：指定包含 Windows 8 作業系統映像的封裝。  

    -   **映像索引**：指定封裝包含多個作業系統映像時應部署的映像。  

    -   **發佈點**：指定裝載開機映像封裝的發佈點。 精靈會從發佈點擷取作業系統映像，並將其寫入至媒體。  

        > [!NOTE]  
        >  系統管理使用者必須具備 [讀取]  存取權限，才能存取發佈點上的作業系統映像內容。 如需詳細資訊，請參閱[管理帳戶以存取內容](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)。  

11. 在 [選取應用程式]  頁面中，指定要包含在媒體檔案中的應用程式內容，然後按 [下一步] 。  

12. 在 [選取套件]  頁面中，指定其他要包含在媒體檔案中的套件內容，然後按 [下一步] 。  

13. 在 [選取驅動程式套件]  頁面中，指定要包含在媒體檔案中的驅動程式套件內容，然後按 [下一步] 。  

14. 在 [發佈點]  頁面中，選取一個或多個包含工作順序所需內容的發佈點，然後按 [下一步] 。  

15. 在 [自訂]  頁面指定下列資訊，然後按 [下一步] 。  

    -   **變數**：指定工作順序用於部署作業系統的變數。 若為 Windows To Go，使用 SMSTSPreferredAdvertID 變數可利用下列格式自動選取 Windows To Go 部署：  

         SMSTSPreferredAdvertID = {*DeploymentID*}，其中 DeploymentID 是與您將用於完成 Windows To Go 磁碟機佈建程序之工作順序的部署識別碼。  

        > [!TIP]  
        >  搭配使用此變數和設為自動執行的工作順序 (會在此程序中稍後設定)，不需使用者互動，而且電腦會在偵測到 Windows To Go 磁碟機時自動開機進入 Windows To Go 部署。 如果媒體已設定密碼保護，仍然會提示使用者輸入密碼。  

    -   **啟動前置命令**：指定您要在工作順序執行前執行的啟動前置命令。 啟動前置命令可以是在執行工作順序以安裝作業系統前，能夠在 Windows PE 中與使用者互動的指令碼或可執行檔。 針對 Windows To Go 部署，設定下列各項：  

        -   **OSDBitLockerPIN**：Windows To Go 的 BitLocker 需要使用複雜密碼。 在啟動前置命令中設定 **OSDBitLockerPIN** 變數，以便為 Windows To Go 磁碟機設定 BitLocker 複雜密碼。  

            > [!WARNING]  
            >  為 BitLocker 啟用複雜密碼後，使用者必須在每次電腦開機至 Windows To Go 磁碟機時輸入複雜密碼。  

        -   **SMSTSUDAUsers**：指定目的地電腦的主要使用者。 使用此變數收集使用者名稱，然後再使用該使用者名稱，為使用者和裝置建立關聯。 如需詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

            > [!TIP]  
            >  若要擷取使用者名稱，您可以在啟動前置命令中建立一個輸入方塊，讓使用者輸入他們的使用者名稱，然後再以該值設定變數。 例如，您可以新增以下行列至啟動前置命令指令碼檔案中：  
            >   
            >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
            >   
            >  `env("SMSTSUDAUsers") = UserID`  

         如需如何建立指令碼檔案作為啟動前置命令的詳細資訊，請參閱[工作順序媒體的啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md)。  

16. 完成精靈。  

    > [!NOTE]  
    >  精靈可能需要很長的時間才能完成預先設置的媒體檔案。  

###  <a name="BKMK_CreatePackage"></a> 建立 Windows To Go Creator 套件  
 進行 Windows To Go 部署期間，您必須建立套件以部署預先設置的媒體檔案。 套件必須包含可以設定 Windows To Go 磁碟機，以及將預先設置的媒體解壓縮到磁碟機的工具。 利用下列程序建立 Windows To Go Creator 套件。  

#### <a name="to-create-the-windows-to-go-creator-package"></a>建立 Windows To Go Creator 套件  

1.  在裝載 Windows To Go Creator 套件檔案的伺服器上，為套件來源檔案建立來源資料夾。  

    > [!NOTE]  
    >  站台伺服器的電腦帳戶，必須擁有來源資料夾的 **讀取** 存取權限。  

2.  將您在 [Create prestaged media](#BKMK_CreatePrestagedMedia) 一節中建立的預先設置的媒體檔案，複製到套件來源資料夾。  

3.  將 Windows To Go Creator 工具 (WTGCreator.exe) 複製到套件來源資料夾。 建立者工具可於下列位置的任何主要站台伺服器取得：<*ConfigMgrInstallationFolder*>\OSD\Tools\WTG\Creator。  

4.  使用 [建立套件和程式精靈] 建立套件和程式。  

5.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

6.  在 [軟體程式庫]  工作區中，展開 [應用程式管理] ，然後按一下 [套件] 。  

7.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立套件] 。  

8.  在 [套件]  頁面上，指定套件的名稱和描述。 例如，輸入 **Windows To Go** 作為封裝名稱，並指定 **Package to configure a Windows To Go drive using System Center Configuration Manager** 作為封裝描述。  

9. 選取 [此套件包含來源檔案] ，指定您在步驟 1 中建立的套件來源資料夾路徑，然後按 [下一步] 。  

10. 在 [程式類型]  頁面上，選取 [標準程式] ，然後按 [下一步] 。  

11. 在 [標準程式]  頁面上，指定下列各項：  

    -   **名稱**：指定程式的名稱。 例如，輸入 **Creator** 作為程式名稱。  

    -   **命令列**：輸入 **WTGCreator.exe /wim:PrestageName.wim**，其中 PrestageName 是預先設置的檔案名稱，該檔案已由您建立且複製到 Windows To Go Creator 封裝的封裝來源資料夾中。  

         您可以選擇新增下列選項：  

        -   **enableBootRedirect**：命令列選項，用於將 Windows To Go 啟動選項變更為允許開機重新導向。 當您使用此選項時，電腦將會從 USB 開機，不需要變更電腦韌體的開機順序，或讓使用者在啟動期間從開機選項中選取選項。 如果偵測到 Windows To Go 磁碟機，電腦會開機至該磁碟機。  

    -   **執行**：指定 [一般]  ，根據系統和程式預設值執行程式。  

    -   **程式可執行**：指定程式是否只能在使用者登入時執行。  

    -   **執行模式**：指定程式是否要以登入的使用者權限執行，或是以系統管理權限執行。 Windows To Go Creator 需要使用提升的權限來執行。  

    -   選取 [允許使用者檢視程式安裝並與其互動] ，然後按 [下一步] 。  

12. 在 [需求] 頁面中，指定下列項目：  

    -   **平台需求**：選取適用的 Windows 8 平台以允許佈建。  

    -   **預估的磁碟空間**：指定 Windows To Go Creator 的封裝來源資料夾大小。  

    -   **允許的執行時間上限 (分鐘)**：指定程式預期在用戶端電腦上執行的時間上限。 根據預設，此值設為 120 分鐘。  

        > [!IMPORTANT]  
        >  如果使用維護期間作為此程式執行的集合，則若 [允許的執行時間上限]  比排程的維護期間長，便會發生衝突。 如果執行時間上限設為 [未知] ，則會在維護期間啟動，但會在維護期間關閉後繼續執行直到完成或失敗為止。 如果您將執行時間上限設定為超過任何維護期間的特定時間長度 (未設定 [未知])，則該程式將不會執行。  

        > [!NOTE]  
        >  如果此值設定為 [未知]，Configuration Manager 會將允許的執行時間上限設定為 12 小時 (720 分鐘)。  

        > [!NOTE]  
        >  如果超過執行時間上限 (由使用者設定，或設定為預設值)，Configuration Manager 會在選取 [以系統管理權限執行]，且未在 [標準程式] 頁面選取 [允許使用者檢視程式安裝並與其互動] 時，停止程式。  

     按 [下一步]  ，並且完成精靈。  

###  <a name="BKMK_UpdateTaskSequence"></a> 更新工作順序以啟用 Windows To Go 的 BitLocker  
 Windows To Go 可在未使用 TPM 的外部可開機磁碟機上，啟用 BitLocker。 因此，您必須使用不同的工具來設定 Windows To Go 磁碟機上的 BitLocker。 若要啟用 BitLocker，您必須在執行 **設定 Windows 和 ConfigMgr** 步驟後，新增動作至工作順序。  

> [!NOTE]  
>  Windows To Go 的 BitLocker 需要使用複雜密碼。 在 [Create prestaged media](#BKMK_CreatePrestagedMedia) 步驟中，您可使用 OSDBitLockerPIN 變數在啟動前置命令中設定複雜密碼。  

 利用下列程序更新 Windows 8 工作順序，以啟用 Windows To Go 的 BitLocker。  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>更新 Windows 8 工作順序以啟用 BitLocker  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [應用程式管理] ，然後按一下 [套件] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立套件] 。  

4.  在 [套件]  頁面上，指定套件的名稱和描述。 例如，輸入 **BitLocker for Windows To Go** 作為封裝名稱，並指定 **Package to update BitLocker for Windows To Go** 作為封裝描述。  

5.  選取 [此套件包含來源檔案] ，指定 Windows To Go 的 BitLocker 工具，然後按 [下一步] 。 BitLocker 工具可於下列位置的任何 Configuration Manager 主要站台伺服器取得：<Configuration Manager 安裝資料夾>\OSD\Tools\WTG\BitLocker\  

6.  在 [程式類型]  頁面上，選取 [不建立程式] 。  

7.  按 [下一步]  ，並且完成精靈。  

8.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

9. 在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

10. 選取您在預先設置媒體中參照的 Windows 8 工作順序。  

11. 在 [首頁]  索引標籤的 [工作順序]  群組中，按一下 [編輯] 。  

12. 按一下 [設定 Windows 和 ConfigMgr]  步驟，按一下 [新增] 和 [一般] ，然後按一下 [執行命令列] 。 [執行命令列] 步驟會加在 [設定 Windows 和 ConfigMgr] 步驟之後。  

13. 在 [執行命令列]  步驟的 [內容]  索引標籤上，新增下列各項：  

    1.  **名稱**：指定命令列的名稱，例如 **Enable BitLocker for Windows To Go**。  

    2.  **命令列**：i386\osdbitlocker_wtg.exe /Enable /pwd:< *None&#124;AD*>  

         參數：  

        -   /pwd:<None&#124;AD> - 指定 BitLocker 密碼復原模式。 如果您在命令列中使用 /Enable 參數，便需使用此參數。  

             選取 [AD]  設定 BitLocker 磁碟機加密，將受到 BitLocker 保護的磁碟機備份復原資訊備份到 Active Directory 網域服務 (AD DS)。 備份受 BitLocker 保護磁碟機的復原密碼，可讓系統管理使用者在磁碟機遭到鎖定時復原該磁碟機。 這麼做可確定屬於企業的加密資料，永遠可由經授權的使用者進行存取。 當您指定 [無] 時，使用者必須負責保存復原密碼或復原金鑰的複本。 如果使用者遺失該資訊或在離開組織前忘了將磁碟機解密，系統管理員便無法輕易存取磁碟機。  

        -   /wait:<TRUE&#124;FALSE> - 指定是否要等完成加密後，再完成工作順序。  

    3.  選取 [套件] ，然後指定您在此程序開始時所建立的套件。  

    4.  在 [選項]  索引標籤上，新增下列條件：  

        -   條件 = Task Sequence Variable  

        -   變數 = _SMSTSWTG  

        -   條件 = Equals  

        -   值 = True  

    > [!NOTE]  
    >  可能是在新命令列步驟之後的 [啟用 BitLocker]  步驟，不會用來啟用 Windows To Go 的 BitLocker。 不過，您可以在工作順序中保留此步驟，以便在不使用 Windows To Go 磁碟機的 Windows 8 部署中使用。  

###  <a name="BKMK_Deployments"></a> 部署 Windows To Go Creator 套件和工作順序  
 Windows To Go 是一個混合部署程序。 因此，您必須部署 Windows To Go Creator 套件和 Windows 8 工作順序。 利用下列程序完成部署程序。  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>部署 Windows To Go Creator 套件  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [應用程式管理] ，然後按一下 [套件] 。  

3.  選取您在 [建立 Windows To Go Creator 套件](#BKMK_CreatePackage) 步驟建立的 Windows To Go 套件。  

4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。  

5.  在 [一般]  頁面上，指定以下設定：  

    1.  **軟體**：確認已選取 Windows To Go 封裝。  

    2.  **集合**：按一下 [瀏覽]  以選取要部署 Windows To Go 封裝的集合。  

    3.  **使用與此集合相關聯的預設發佈點群組**：如果您想要將封裝內容儲存在集合預設發佈點群組中，請選取此選項。 如果您還沒有為所選的集合及發佈點群組建立關聯，將無法使用此選項。  

6.  在 [內容]  頁面按一下 [新增]  ，然後選取要部署與此套件及程式相關聯之內容的發佈點或發佈點群組。  

7.  在 [部署設定]  頁面上，針對部署類型選取 [可用]  ，然後按 [下一步] 。  

8.  在 [排程] 上，設定此套件和程式的部署時間，或可供用戶端裝置使用的時間。  

     此頁面上的選項會因部署動作設定為 [可用]  或 [必要] 而有所不同。  

9. 在 [排程] 上，設定下列設定，然後按 [下一步] 。  

    1.  **排程此部署的可用時間**：指定可在目的地電腦上執行封裝和程式的日期和時間。 當您選取 [UTC] 時，此設定可確保套件及程式會根據目的地電腦的當地時間，於相同的時間 (而不是不同的時間) 提供給多部目的地電腦使用。  

    2.  **排程此部署的到期時間**：指定目的地電腦上封裝和程式到期的日期和時間。 當您選取 [UTC] 時，此設定可確保工作順序會根據目的地電腦的當地時間，於相同的時間 (而不是不同的時間) 在目的地電腦上到期。  

10. 在精靈的 [使用者經驗]  頁面上，指定以下資訊：  

    -   **軟體安裝**：允許在任何已設定的維護期間以外的時間安裝軟體。  

    -   **系統重新啟動 (如果是完成安裝所需)**：允許在軟體安裝需要時，於設定的維護期間以外的時間重新啟動裝置。  

    -   **Embedded 裝置**：將封裝和程式部署到啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝封裝和程式，並於稍後再認可變更，或是在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。  

11. 在 [發佈點]  頁面上，指定下列資訊：  

    -   **部署選項** ：指定 [從發佈點下載內容並在本機執行] 。  

    -   **允許用戶端與同一個子網路上的其他用戶端共用內容**：選取這個選項，以允許用戶端從已下載且快取內容的網路上的其他用戶端下載內容以降低網路的負載。 此選項會利用 Windows BranchCache，可以在執行 Windows Vista SP2 以及更新版本的電腦上使用。  

    -   **允許用戶端使用內容的後援來源位置**：指定是否允許用戶端進行後援，並且在內容於慣用好發佈點上不可用時，使用非慣用發佈點作為內容的來源位置。  

12. 完成精靈。  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>若要部署 Windows 8 工作順序  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  選取您在 [Prerequisites to provision Windows To Go](#BKMK_Prereqs) 步驟中所建立的 Windows 8 工作順序。  

4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。  

5.  在 [一般]  頁面上，指定以下設定：  

    1.  **工作順序**：確認選取了 Windows 8 工作順序。  

    2.  **集合**：按一下 [瀏覽]  以選取包含使用者可能佈建 Windows To Go 之所有裝置的集合。  

        > [!IMPORTANT]  
        >  如果您在 [Create prestaged media](#BKMK_CreatePrestagedMedia) 一節中所建立的預先設置媒體使用 SMSTSPreferredAdvertID 變數，您可以將工作順序佈建到 **所有系統** 集合並且指定 [內容]  頁面上的 [僅限 Windows PE (隱藏)]  設定。 由於工作順序已經隱藏，因此僅可供媒體使用。  

    3.  **使用與此集合相關聯的預設發佈點群組**：如果您想要將封裝內容儲存在集合預設發佈點群組中，請選取此選項。 如果您還沒有為所選的集合及發佈點群組建立關聯，將無法使用此選項。  

6.  在 [部署設定]  頁面上，設定下列設定，然後按 [下一步] 。  

    -   **目的**：選取 [可用] 。 部署工作順序至使用者時，使用者會看見工作順序發佈在「應用程式類別目錄」中，並且可依需求要求該工作順序。 如果部署工作順序至裝置，則使用者會看見工作順序列在「軟體中心」中，並且可依需求安裝該工作順序。  

    -   **提供給下列項目使用**：指定工作順序是否可以使用 Configuration Manager 用戶端、媒體或 PXE。  

        > [!IMPORTANT]  
        >  為自動工作順序部署使用 [僅媒體和 PXE (隱藏)]  設定。 選取 [允許自動部署作業系統]  並將 SMSTSPreferredAdvertID 變數設為預先設置媒體的一部分，以在偵測到 Windows To Go 磁碟時自動開機至 Windows To Go 部署而不需要使用者互動。 如需這些預先設置媒體設定的詳細資訊，請參閱 [Create prestaged media](#BKMK_CreatePrestagedMedia) 一節。  

7.  在 [排程]  頁面上，設定下列設定，然後按 [下一步] 。  

    1.  **排程此部署的可用時間**：指定工作順序可在目的地電腦上執行的日期和時間。 選取 [UTC] 時，此設定可確保工作順序以目的地電腦的本機時間為根據，在同一時間而非不同時間內由多個目的地電腦使用。  

    2.  **排程此部署的到期時間**：指定工作順序在目的地電腦上的到期日期和時間。 當您選取 [UTC] 時，此設定可確保工作順序會根據目的地電腦的當地時間，於相同的時間 (而不是不同的時間) 在目的地電腦上到期。  

8.  在 [使用者經驗]  頁面上，指定下列資訊：  

    -   **顯示工作順序進度**：指定 Configuration Manager 用戶端是否顯示工作順序進度。  

    -   **軟體安裝**：指定是否允許使用者在排程時間後，於設定的維護期間之外安裝軟體。  

    -   **系統重新啟動 (如果是完成安裝所需)**：允許在軟體安裝需要時，於設定的維護期間以外的時間重新啟動裝置。  

    -   **Embedded 裝置**：將封裝和程式部署到啟用寫入篩選器的 Windows Embedded 裝置時，您可以指定在暫時重疊上安裝封裝和程式，並於稍後再認可變更，或是在安裝期限或維護期間認可變更。 當您在安裝期限或維護期間認可變更時，需要重新啟動裝置才能保存裝置的變更。  

    -   **以網際網路為基礎的用戶端**：指定是否允許工作順序在網際網路型用戶端上執行。 此設定不支援如安裝作業系統等軟體的作業。 此選項僅適用於在標準作業系統內執行作業的一般指令碼式工作順序。  

9. 在 [警示]  頁面上，指定您想要這項工作順序部署的警示設定，然後按 [下一步] 。  

10. 在 [發佈點]  頁面上，指定下列資訊，然後按 [下一步] 。  

    -   **部署選項**：選取 [執行工作順序以視需要將內容下載到本機] 。  

    -   **當沒有本機發佈點可用時，使用遠端發佈點**：指定用戶端是否可在速度慢且不可靠的網路上使用發佈點來下載工作順序所需要的內容。  

    -   **允許用戶端使用內容的後援來源位置**：
        - *在 1610 版之前*，您可以選取 [允許內容的後援來源位置] 核取方塊，讓位於這些界限群組以外的用戶端回復，並在沒有其他發佈點可用時，將發佈點當成內容的來源位置使用。
        - *從 1610 版開始*，您無法再設定 [允許內容的後援來源位置]。  相反地，您可以設定界限群組之間的關聯性，以決定用戶端何時可以開始搜尋其他界限群組中的有效內容來源位置。 

11. 完成精靈。  

###  <a name="BKMK_UserExperience"></a> 使用者執行 Windows To Go Creator  
 部署 Windows To Go 套件與 Windows 8 工作順序後，使用者就可使用 Windows To Go Creator。 如果 Windows To Go Creator 已部署到裝置，使用者可以前往軟體類別目錄或是「軟體中心」並執行 Windows To Go Creator。 下載建立程式套件後，工作列上會顯示閃爍的圖示。 使用者可按一下圖示並使用顯示的對話方塊來選取 Windows To Go 磁碟以進行佈建 (除非使用了磁碟命令列選項)。 如果磁碟不符合 Windows To Go 的需求或是如果磁碟沒有足夠的可用磁碟空間以安裝映像，建立程式就會顯示錯誤訊息。 使用者可以確認將從確認頁面套用的磁碟與映像。 建立程式設定並將內容預先設置到 Windows To Go 磁碟的同時，程式會顯示進度對話方塊。 預先設置作業完成後，建立程式會顯示提示以重新啟動電腦並開機至 Windows To Go 磁碟。  

> [!NOTE]  
>  如果您並未在 [Create a Windows To Go Creator package](#BKMK_CreatePackage) 一節中啟用開機重新導向作為建立程式的一部分，系統可能會要求使用者在每次系統重新啟動時手動開機至 Windows To Go 磁碟。  

###  <a name="BKMK_ConfigureStageDrive"></a> Configuration Manager 設定與設置 Windows To Go 磁碟機  
 電腦重新啟動至 Windows To Go 磁碟後，磁碟將開機至 Windows PE 並連線至管理點以取得原則來完成作業系統部署。 Configuration Manager 設定與設置磁碟機。 Configuration Manager 設置磁碟後，使用者可以重新啟動電腦以結束佈建程序 (例如加入網域或安裝應用程式)。 此程序對於任何預先設置媒體來說皆為相同。  

###  <a name="BKMK_UserLogsIn"></a> 使用者登入 Windows 8  
 Configuration Manager 完成佈建程序並顯示 Windows 8 鎖定螢幕後，使用者即可登入作業系統。  
