---
title: "管理開機映像 - Configuration Manager | Microsoft Docs"
description: "在 Configuration Manager 中，了解如何管理在作業系統部署期間所使用的 Windows PE 開機映像。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: "23"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: cc678c1133b1944f55bcad309cf9ede9f0660b57
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理開機映像

適用於：System Center Configuration Manager (最新分支)

Configuration Manager 中的開機映像是 [Windows PE (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) 映像，在作業系統部署時使用。 開機映像用來以 WinPE 啟動電腦，WinPE 是最低需求的作業系統，內含有限的元件和服務可讓目的地電腦準備好進行 Windows 安裝。  使用以下各節管理開機映像。

## <a name="BKMK_BootImageDefault"></a> 預設開機映像
Configuration Manager 提供兩種預設開機映像：一種支援 x86 平台，另一種支援 x64 平台。 這些映像儲存於：\\\\<伺服器名稱>\SMS_<站台碼>\osd\boot\\<*x64*> 或 <*i386*>。 預設開機映像會根據您所採取的動作更新或重新產生。

針對在下列各節中所描述的任何動作，請考慮下列項目：
- 來源驅動程式物件 (包括驅動程式來源檔案) 必須有效，否則驅動程式將不會新增到站台的開機映像。
- 開機映像若非以預設開機映像為基礎，即使使用相同的 Windows PE 版本，也不會進行修改。
- 您必須將修改的開機映像重新發佈至發佈點。
- 您必須重新建立任何使用已修改開機映像的媒體。
- 如果您不想要自動更新您的自訂/預設開機映像，請勿將其存放在預設位置。

> [!NOTE]
> Configuration Manager 追蹤記錄檔工具會新增至您新增至**軟體程式庫**的所有開機映像中。 當您在 Windows PE 中時，可以從命令提示字元鍵入 **CMTrace** 來啟動 Configuration Manager 追蹤記錄檔工具。  

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>使用 [更新與服務] 來安裝最新版本的 Configuration Manager
從 1702 版開始，在您升級 Windows ADK 版本並使用 [更新與服務] 安裝最新版的 Configuration Manager 時，Configuration Manager 會重新產生預設開機映像。 這包括來自更新的 Windows ADK 的新 Window PE 版本、新版 Configuration Manager 用戶端、驅動程式及自訂等等。不會修改自訂開機映像。

在 1702 版之前，Configuration Manager 會使用用戶端元件、驅動程式、自訂等更新現有的開機映像 (boot.wim)，但不會使用 Windows ADK 的最新版 Windows PE。 您必須手動將開機映像修改為使用新版的 Windows ADK。

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>從 Configuration Manager 2012 升級成 Configuration Manager 最新分支 (CB)
使用安裝程序將 Configuration Manager 2012 升級至 Configuration Manager CB 時，Configuration Manager 會重新產生預設開機映像。 這包括來自更新的 Windows ADK 的新 Window PE 版本、新版 Configuration Manager 用戶端，且所有自訂皆維持不變。 不會修改自訂開機映像。

### <a name="update-distribution-points-with-the-boot-image"></a>使用開機映像更新發佈點
當您在 Configuration Manager 主控台中使用來自 [開機映像] 節點的 [更新發佈點] 動作時，Configuration Manager 會使用用戶端元件、驅動程式及自訂等更新預設開機映像。    

從 Configuration Manager 1706 版開始，您可以選擇在開機映像中重新載入 (來自 Windows ADK 安裝目錄的) 最新版本的 Windows PE。 [更新發佈點] 精靈的 [一般] 頁面會提供站台伺服器上所安裝的 Windows ADK 版本、開機映像中使用 Windows PE 的 Windows ADK 版本，以及 Configuration Manager 用戶端的版本。 您可以使用此資訊來協助決定是否要重新載入開機映像。 此外，當您在 [開機映像] 節點中檢視開機映像時，您也可以利用新的 [用戶端版本] 欄位來了解每個開機映像所使用的 Configuration Manager 用戶端版本為何。    

不會修改自訂開機映像。

##  <a name="BKMK_BootImageCustom"></a> 自訂開機映像  
 如果開機映像是以支援的 Windows ADK 版本中的 Windows PE 版本為基礎，您可以在 Configuration Manager 主控台自訂開機映像或[修改開機映像](#BKMK_ModifyBootImages)。 當站台升級為新版本並安裝新版 Windows ADK 時，自訂開機映像 (不位於預設的開機映像位置) 並不會更新成使用新版 Windows ADK。 發生這種情況時，您將無法再於 Configuration Manager 主控台中自訂開機映像。 不過，它們將如升級之前一樣繼續運作。  

 當開機映像是以和站台上安裝之 Windows ADK 版本不同的版本為基礎時，您必須使用其他方法來自訂開機映像，例如使用 Windows AIK 和 Windows ADK 所含的「部署映像服務與管理」(DISM) 命令列工具。 如需詳細資訊，請參閱[自訂開機映像](customize-boot-images.md)。  

##  <a name="BKMK_AddBootImages"></a> 新增開機映像  

 在站台安裝期間，Configuration Manager 會自動新增以支援的 Windows ADK 版本中的 WinPE 版本為基礎的開機映像。 依據 Configuration Manager 的版本，您或許可以新增以支援的 Windows ADK 版本中不同的 WinPE 版本為基礎的開機映像。  當您嘗試新增包含不受支援 WinPE 版本的開機映像時，會發生錯誤。  

 以下提供支援的 Windows ADK 版本，以及開機映像 (包括可從 Configuration Manager 主控台自訂的開機映像，以及可以使用 DISM 自訂然後新增映像到 Configuration Manager 的開機映像) 所依據的 Windows PE 版本。  

-   **Windows ADK 版本**  

     Windows ADK for Windows 10  

-   **可從 Configuration Manager 主控台自訂之開機映像的 Windows PE 版本**  

     Windows PE 10  

-   **無法從 Configuration Manager 主控台自訂之開機映像的支援 Windows PE 版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有當開機映像以 Windows PE 3.1 為基礎時，您才能將開機映像新增至 Configuration Manager。 請安裝適用於 Windows 7 SP1 的 Windows AIK 補充元件，以便使用適用於 Windows 7 SP1 的 Windows AIK 補充元件 (以 Windows PE 3.1 為基礎) 來升級適用於 Windows 7 的 Windows AIK (以 Windows PE 3 為基礎)。 您可以從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=5188)下載適用於 Windows 7 SP1 的 Windows AIK 補充元件。  

     例如，當您有 Configuration Manager 時，便可從 Configuration Manager 主控台，使用適用於 Windows 10 的 Windows ADK (以 Windows PE 10 為基礎) 來自訂開機映像。 不過，若支援以 Windows PE 5 為基礎的開機映像，您必須從不同的電腦自訂開機映像，並使用與 Windows ADK for Windows 8 一起安裝的 DISM 版本。 接著，您可以將開機映像新增到 Configuration Manager 主控台。 如需自訂開機映像 (新增選用元件和驅動程式)、啟用開機映像的命令支援、將開機映像新增至 Configuration Manager 主控台，以及使用開機映像更新發佈點之步驟的詳細資訊，請參閱[自訂開機映像](customize-boot-images.md)。

 使用下列程序手動新增開機映像。  

#### <a name="to-add-a-boot-image"></a>新增開機映像  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增開機映像]  ，啟動 [新增開機映像精靈]。  

4.  在 [資料來源]  頁面上指定下列選項，然後按 [下一步] 。  

    -   在 [路徑]  方塊中，指定開機映像 WIM 檔案的路徑。  

         指定的路徑必須是使用 UNC 格式的有效網路路徑。 例如︰\\\\<*伺服器名稱*\\<*共用名稱*>\\<*開機映像名稱*>.wim。  

    -   從 [開機映像]  下拉式清單選取開機映像。 如果 WIM 檔包含多個開機映像，請選取適當的映像。  

5.  在 [一般]   頁面指定下列選項，然後按 [下一步] 。  

    -   在 [名稱]  方塊中，為開機映像指定唯一的名稱。  

    -   在 [版本]  方塊中，指定開機映像的版本號碼。  

    -   在 [註解]  方塊中，指定有關如何使用開機映像的簡單描述。  

6.  完成精靈。  

 此時，開機映像會列在 Configuration Manager 主控台的 [開機映像] 節點中。 不過，您必須先將開機映像發佈到發佈點、發佈點群組或與發佈點群組相關聯的集合，才可以使用開機映像部署作業系統。  

> [!NOTE]  
>  當您在 Configuration Manager 主控台中選取 開機映像 節點時，大小 (KB)  欄會顯示每個開機映像解壓縮後的大小。 不過，當 Configuration Manager 透過網路傳送開機映像時，它會傳送映像的壓縮複本，而這個複本的大小通常遠低於 [大小 (KB)] 欄中列出的大小。  

##  <a name="BKMK_DistributeBootImages"></a> 將開機映像發佈至發佈點  
 開機映像發佈至發佈點的方式，與您發佈其他內容的方式相同。 在大部分情況下，您必須在部署作業系統之前，以及建立媒體之前，將開機映像發佈至至少一個發佈點。  

> [!NOTE]  
>  若要使用 PXE 來部署作業系統，請在發佈開機映像之前考慮下列事項：  
>   
>  -   發佈點必須設定為接受 PXE 要求。  
> -   您必須將 x86 啟用 PXE 的開機映像和 x64 啟用 PXE 的開機映像發佈到至少一個啟用 PXE 的發佈點。  
> -   Configuration Manager 會將開機映像發佈到支援 PXE 之發佈點上的 **RemoteInstall** 資料夾。  
>   
>  如需如何使用 PXE 部署作業系統的詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

 如需發佈開機映像的步驟，請參閱 [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。  

##  <a name="BKMK_ModifyBootImages"></a> 修改開機映像  
 您可以新增或移除映像的裝置驅動程式，或編輯與開機映像相關聯的內容。 新增或移除的裝置驅動程式可能包含網路介面卡或大量儲存裝置驅動程式。 修改開機映像時，請考慮下列因素：  

-   您必須先將裝置驅動程式匯入裝置驅動程式類別目錄，並予以啟用，才能將它們新增至開機映像。  

-   修改開機映像時，開機映像不會變更開機映像參考的任何相關聯的封裝。  

-   您對開機映像進行變更之後，必須「更新」  已有開機映像之發佈點上的開機映像，以便提供最新版的開機映像。 如需詳細資訊，請參閱 [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage)。  

 請使用下列程序修改開機映像。  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>修改開機映像的內容  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

3.  選取要修改的開機映像。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容]  以開啟開機映像的 [內容]  對話方塊。  

5.  設定下列其中一個設定以變更開機映像的行為：  

    -   在 [映像]  索引標籤上，如果您已使用外部工具變更開機映像內容，請按一下 [重新載入] 。  

    -   在 [驅動程式]  索引標籤上，新增啟動 WinPE 所需的 Windows 裝置驅動程式。 新增裝置驅動程式時，請考量下列各項：  

        -   選取 [隱藏不符合開機映像架構的驅動程式]，只顯示適用於開機映像架構的驅動程式。 架構是以製造商 .INF 中所報告的架構為依據。  

        -   選取 [隱藏不在儲存體或網路類別中的驅動程式 (針對開機映像)]  ，只顯示儲存體和網路驅動程式，並隱藏開機映像通常不需要的其他驅動程式，例如視訊驅動程式或數據機驅動程式。  

        -   選取 [隱藏未數位簽署的驅動程式]  ，可隱藏未經數位簽署的驅動程式。  

        -   基於最佳做法，除非 WinPE 另有其他驅動程式需求，否則請只新增 NIC 和大型存放驅動程式以加入至開機映像。  

        -   由於 WinPE 已內建許多驅動程式，因此只新增 WinPE 未提供的 NIC 和大型存放驅動程式。  

        -   確定您新增到開機映像中的驅動程式符合開機映像的架構。  

        > [!NOTE]  
        >  您必須將裝置驅動程式匯入驅動程式類別目錄，才能將它們新增至開機映像。 如需如何匯入裝置驅動程式的相關資訊，請參閱[管理驅動程式](manage-drivers.md)。  

    -   在 [自訂]  索引標籤上，選取下列其中一項設定：  

        -   選取 [啟用啟動前置命令]  核取方塊，指定要在工作順序執行前執行的命令。 當啟用啟動前置命令時，您可以指定執行的命令列、是否需要使用支援檔案來執行命令，以及這些支援檔案的來源位置。  

            > [!WARNING]  
            >  您必須在命令列的開頭加上 **cmd /c** 。 如果您未指定 **cmd /c**，命令就不會在執行之後關閉。 部署會繼續等待命令完成，而不會開始執行任何其他已設定的命令或動作。  

            > [!TIP]  
            >  在建立工作順序媒體時，工作順序會將套件識別碼和啟動前置命令列，包括任何工作順序變數的值，寫入執行 Configuration Manager 主控台之電腦上的 CreateTSMedia.log 記錄檔中。 您可以檢閱這個記錄檔來驗證工作順序變數的值。  

        -   設定 [Windows PE 背景]  設定，指定是否要使用預設的 WinPE 背景，或使用自訂背景。  

        -   選取 [啟用命令支援 (僅限測試)]  ，以在部署開機映像時，使用 **F8** 鍵開啟命令提示字元。 這對於在測試部署的同時進行疑難排解非常有用。 不建議在生產部署時使用此設定。  

        -   設定 Windows PE 臨時空間，這是由 WinPE 使用的暫存位置 (RAM 磁碟機)。 例如，當應用程式在 WinPE 中執行且需要寫入暫存檔案時，WinPE 會將檔案重新導向到記憶體的臨時空間，以模擬實際的硬碟。 根據預設，WinPE 會配置 32 MB 的可寫入記憶體。  

    -   在 [資料來源]  索引標籤上，更新下列其中一項設定：  

        -   設定 [映像路徑]  和 [映像索引]  以變更開機映像的來源檔案。  

        -   選取 [按照排程更新發佈點]  以建立更新開機映像的時間排程。  

        -   如果不想要讓此封裝的內容存放在用戶端快取中過久，請選取 [將內容保存在用戶端快取中]  以騰出供其他內容使用的空間。  

        -   選取 [啟用二進位差異複寫]  ，指定當發佈點上的開機映像封裝更新時只發佈變更的檔案。 此設定可使站台間的網路流量降至最低，特別是開機映像套件很大時，而變更相對而言比較小。  

        -   如果開機映像是用在支援 PXE 的部署中，請選取 **[從支援 PXE 的發佈點部署此開機映像]** 。  

            > [!NOTE]  
            >  如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

    -   在 [資料存取]  索引標籤上，選取下列其中一項設定：  

        -   如果要讓用戶端從網路安裝此套件的內容，請設定 [套件共用設定]  。  

        -   設定 [套件更新設定]，指定要讓 Configuration Manager 中斷使用者與發佈點之間連線的方法。 當使用者與發佈點連線時，Configuration Manager 可能無法更新開機映像。  

    -   在 [發佈設定]  索引標籤上，選取下列其中一項設定：  

        -   在 [發佈優先順序] 清單中，指定要讓 Configuration Manager 在將多個套件發佈到相同發佈點時使用的優先順序層級。  

        -   如果要將隨需內容發佈到慣用發佈點，請選取 [將此封裝的內容發佈至慣用發佈點]  。 當啟用此設定時，管理點會在用戶端要求套件的內容，而所要求內容不存在於任何慣用發佈點上時，將內容發佈到所有慣用發佈點。  

        -   設定 [預先設置的發佈點設定]  ，指定如何將開機映像發佈到已啟用預先設置之內容的發佈點。  

            > [!NOTE]  
            >  如需預先設置內容的詳細資訊，請參閱 [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage)。  

    -   在 [內容位置]  索引標籤上，選取發佈點或發佈點群組，並執行下列任何一項動作：  

        -   按一下 [重新發佈]  ，將開機映像再次發佈到選取的發佈點或發佈點群組。  

        -   按一下 [驗證]  ，檢查所選發佈點或發佈點群組上開機映像套件的完整性。  

    -   在 [選用元件] 索引標籤上，指定已新增至 Windows PE 以搭配 Configuration Manager 使用的元件。 如需可用選擇性元件的詳細資訊，請參閱 [WinPE：新增封裝 (選擇性元件參考)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)。  

    -   在 [安全性]  索引標籤上，選取系統管理使用者，並變更該使用者可執行的操作。  

6.  設定這些內容之後，請按一下 [確定] 。  

##  <a name="BKMK_BootImagePXE"></a> 設定開機映像以從支援 PXE 的發佈點部署  
 您必須先設定開機映像，從支援 PXE 的發佈點部署，才能使用開機映像進行 PXE 作業系統部署。  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>設定開機映像以從支援 PXE 的發佈點部署  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [開機映像] 。  

3.  選取要修改的開機映像。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容]  以開啟開機映像的 [內容]  對話方塊。  

5.  在 [資料來源]  索引標籤上，選取 [從支援 PXE 的發佈點部署此開機映像] 。  

    > [!NOTE]  
    >  如需詳細資訊，請參閱[使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

6.  設定這些內容之後，請按一下 [確定] 。  

##  <a name="BKMK_BootImageLanguage"></a> 設定支援多個語言的開機映像部署  
 開機映像與語言無關。 如果您加入來自 Windows PE 選用元件的適當語言支援，並且設定正確的工作順序變數以指定要顯示的語言，您就可以在 WinPE 中使用開機映像以顯示多種語言的工作順序。 不論 Configuration Manager 版本為何，您部署的作業系統語言都與 WinPE 中所顯示的語言無關。 顯示給使用者的語言是根據下列條件決定：  

-   使用者從現有作業系統執行工作順序時，Configuration Manager 會自動使用為使用者所設定的語言。 工作順序因為強制部署期限而自動執行時，Configuration Manager 會使用作業系統的語言。  

-   若為使用 PXE 或媒體的作業系統部署，您可以在 SMSTSLanguageFolder 變數中設定語言識別碼值作為啟動前置命令的一部分。 電腦開機至 WinPE 時，會以您在變數中指定的語言來顯示訊息。 如果存取指定資料夾內的語言資源檔案發生錯誤，或是您沒有設定變數，則會以 Win PE 語言來顯示訊息。  

    > [!NOTE]  
    >  媒體以密碼保護時，提示使用者輸入密碼的文字一律會以 WinPE 的語言顯示。  

 使用下列程序以設定 PXE 或是媒體初始化作業系統部署的 WinPE 語言。  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>若要設定 PXE 或是媒體初始化作業系統部署的 Windows PE 語言  

1.  更新開機映像之前，確認站台伺服器上的正確工作順序資源檔 (tsres.dll) 置於相對應的語言資料夾內。 例如，英文資源檔位於下列位置： <Configuration Manager 安裝資料夾>\OSD\bin\x64\00000409\tsres.dll。  

2.  在啟動前置命令中，將 SMSTSLanguageFolder 環境變數設為適當的語言識別碼。 語言識別碼必須使用十進位而不是十六進位來指定。 例如，若要將語言識別碼設為英文，您應指定 1033 的十進位值，而不是用於資料夾名稱的 00000409 十六進位值。  
