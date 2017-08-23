---
title: "建立工作順序以升級作業系統 | Microsoft Docs"
description: "System Center Configuration Manager 中的工作順序可以將作業系統從 Windows 7 或更新版本自動升級至 Windows 10。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 4a3c69edc85a4ea7501510b6b3f12c72ad3a24ff
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立工作順序以升級作業系統

適用於：System Center Configuration Manager (最新分支)

使用 System Center Configuration Manager 中的工作順序，將目的地電腦上的作業系統從 Windows 7 或更新版本自動升級至 Windows 10，或是從 Windows Server 2012 或更新版本升級至 Windows Server 2016。 您建立的工作順序，會參考要安裝在目的地電腦上的作業系統映像，以及其他任何內容，例如應用程式或要安裝的軟體更新。 升級作業系統的工作順序是[將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)案例的一部分。  

##  <a name="BKMK_UpgradeOS"></a> 建立工作順序以升級作業系統  
 若要升級電腦上的作業系統，您可以建立工作順序，並在 [建立工作順序精靈] 中選取 [從升級套件升級作業系統]。 該精靈會加入升級作業系統、套用軟體更新以及安裝應用程式的步驟。 建立工作順序之前，必須備妥下列事項：    

-   **必要**  

     - Configuration Manager 主控台中必須有[作業系統升級套件](../get-started/manage-operating-system-upgrade-packages.md)。
     - 當您升級到 Windows Server 2016 時，必須在 [升級作業系統] 工作順序步驟中選取 [忽略任何可解除的相容性訊息] 設定，否則升級會失敗。

-   **必要 (如果有用到)**  

    -   [軟體更新](../../sum/get-started/synchronize-software-updates.md)必須在 Configuration Manager 主控台中進行同步處理。  

    -   Configuration Manager 主控台中必須新增[應用程式](../../apps/deploy-use/create-applications.md)。  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>建立升級作業系統的工作順序  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，按一下 [從升級套件升級作業系統] ，然後按一下 [下一步] 。  

5.  在 [工作順序資訊]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **工作順序名稱**：指定識別工作順序的名稱。  

    -   **描述**：指定工作順序所執行工作之說明。  

6.  在 [升級 Windows 作業系統]  頁面上，指定下列設定，然後再按一下 [下一步] 。  

    -   **升級套件**：指定包含作業系統升級來源檔案的升級套件。 查看 [內容]  窗格的資訊，可確認已選取正確的升級套件。 如需詳細資訊，請參閱[管理作業系統升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

    -   **版本索引**：如果套件中有多個作業系統版本索引，請選取所需的版本索引。 依預設，會選取第一個項目。  

    -   **產品金鑰**：指定要安裝之 Windows 作業系統的產品金鑰。 您可以指定編碼的大量授權金鑰和標準產品金鑰。 如果您使用未編碼的產品金鑰，則每五個字元為一組，之間必須以破折號 (-) 來分隔。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*。 當大量授權版本進行升級時，不需要產品金鑰。 只有在零售版的 Windows 版本升級時，才需要產品金鑰。  

    -   **忽略任何可解除的相容性訊息**：如果是升級到 Windows Server 2016，請選取此選項。 如果您未選取此設定，則工作順序將會失敗，因為 Windows 安裝程式會等待使用者按一下 Windows 應用程式相容性對話方塊中的 [確認]。   

7.  在 [包含更新]  頁面上，指定要安裝必要的軟體更新、所有軟體更新或不安裝軟體更新，然後按 [下一步] 。 如果您指定安裝軟體更新，Configuration Manager 只會將目標軟體更新安裝至目的地電腦為其成員的集合。  

8.  在 [安裝應用程式]  頁面上，指定要安裝在目的地電腦上的應用程式，然後按 [下一步] 。 如果您指定多個應用程式，也可以指定工作順序在特定應用程式安裝失敗時繼續執行。  

9. 完成精靈。  



## <a name="configure-pre-cache-content"></a>設定預先快取內容
從 1702 版開始，針對工作順序的可用部署，您可以選擇使用預先快取功能，讓用戶端在使用者安裝內容之前只下載相關內容。
> [!TIP]  
> 隨版本 1702 引進的預先快取是發行前版本功能。 若要啟用它，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

例如，假設您想要部署 Windows 10 就地升級工作順序、只需要適用於所有使用者的單一工作順序，並有多個架構及 (或) 語言。 在版本 1702 之前，如果您建立可用的部署，然後使用者在軟體中心按一下 [安裝]，此時會下載內容。 這會增加準備開始安裝之前的額外時間。 此外，您可以下載工作順序中參照的所有內容。 這包括所有語言和架構的作業系統升級套件。 如果每個大小約 3 GB，則下載套件可能會相當大。

預先快取內容可讓您選擇允許用戶端在一收到部署時，就只下載適用的內容。 因此，當使用者在軟體中心按一下 [安裝] 時，由於內容是在本機硬碟上，因此內容已就緒且安裝會快速開始。

### <a name="to-configure-the-pre-cache-feature"></a>設定預先快取功能

1. 建立特定架構和語言的作業系統升級套件。 在套件的 [資料來源] 索引標籤中指定架構和語言。 針對語言，使用十進位轉換 (例如 1033 是英文的十進位表示，而 0x0409 是十六進位的對等用法)。 如需詳細資訊，請參閱[建立工作順序以升級作業系統](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。

    架構和語言值可用來比對您將在下一個步驟中建立的工作順序步驟條件，以判斷是否應該預先快取作業系統升級套件。
2. 針對不同的語言和架構，建立具有條件式步驟的工作順序。 例如，您可以針對英文版建立類似如下的步驟：

    ![預先快取內容](../media/precacheproperties2.png)

    ![預先快取選項](../media/precacheoptions2.png)  

3. 部署工作順序。 針對預先快取功能，進行下列設定：
    - 在 [一般] 索引標籤上，選取 「Pre-download content for this task sequence」 (此工作順序的下載前內容)。
    - 在 [部署設定] 索引標籤上，將工作順序的 [目的] 設定為 [可用]。 如果您建立 [必要] 部署，預先快取功能將無法運作。
    - 在 [排程] 索引標籤上，針對 [排程此部署的可用時間] 設定選擇一個未來時間，讓用戶端有足夠的時間預先快取內容，再提供部署給使用者。 例如，您可以將可用時間設定為 3 小時後，以允許有足夠的時間可預先快取內容。  
    - 在 [發佈點] 索引標籤上，設定 [部署選項] 設定。 如果在使用者開始安裝之前未在用戶端預先快取內容，則會使用這些設定。


### <a name="user-experience"></a>使用者經驗
- 當用戶端收到部署原則時，就會開始預先快取內容。 這包括所有參考的內容 (任何其他套件類型)，以及根據您在工作順序中設定的條件只符合用戶端的作業系統升級套件。
- 當使用者可以使用部署時 (部署之 [排程] 索引標籤中的設定)，系統會顯示通知，告知使用者有此新的部署，並在軟體中心顯示此部署。 使用者可以前往軟體中心，然後按一下 [安裝] 開始安裝。
- 如果未完整預先快取內容，則會使用部署之 [部署選項] 索引標籤上指定的設定。 建議在建立部署到部署可供使用者使用之間有足夠的時間，讓用戶端有足夠的時間來預先快取內容。



## <a name="download-package-content-task-sequence-step"></a>下載套件內容的工作順序步驟  
 在下列案例中的 [升級作業系統] 步驟之前，可以使用[下載套件內容](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)步驟：  

-   您使用可同時搭配 x86 和 x64 平台使用的單一升級工作順序。 若要執行此作業，請在 **準備升級** 群組中加入兩個 **下載套件內容** 步驟，這些步驟設有條件，可偵測用戶端架構，僅下載適用的作業系統升級套件。 將每個 **下載套件內容** 步驟設定為使用相同的變數，並使用該變數來代表 **升級作業系統** 步驟中的媒體路徑。  

-   若要動態下載適用的驅動程式套件，請使用兩個 **下載套件內容** 步驟，並設定條件來偵測每個驅動程式套件適用的硬體類型。 將每個 [下載封裝內容]  步驟設定成使用相同的變數，並使用這個變數來表示 [升級作業系統]  步驟之 [驅動程式] 區段中的 [分段內容]  值。  

   > [!NOTE]
   > 有多個套件時，Configuration Manager 會在變數名稱後面加上數值尾碼。 例如，如果您指定 %mycontent% 變數作為自訂變數，這會是所有參照內容儲存位置的根目錄 (可以是多個套件)。 當您在後續步驟 (例如 [升級作業系統]) 中參考此變數時，會使用加上數值尾碼的變數。 在這個範例中，%mycontent01% 或 %mycontent02% 中的數字會與套件在這個步驟中列出的順序對應。

## <a name="optional-post-processing-task-sequence-steps"></a>選擇性的後續處理工作順序步驟  
 建立工作順序之後，可新增其他步驟來解除安裝出現已知相容性問題的應用程式，或新增重新啟動電腦之後要執行的後續處理動作，如此即已成功升級為 Windows 10。 在工作順序的後續處理群組中新增下列其他步驟。  

> [!NOTE]  
>  因為這個工作順序並非線性順序，所以根據是否成功升級用戶端電腦，或者是否必須將用戶端電腦復原成啟動所用的作業系統版本，會出現不同的步驟，而可能影響工作順序的結果。  

## <a name="optional-rollback-task-sequence-steps"></a>選擇性的復原工作順序步驟  
 重新啟動電腦之後若升級程序出錯，安裝程式會將升級復原為先前的作業系統，而工作順序會繼續執行復原群組中的任何步驟。 建立工作順序之後，可對復原群組新增選擇性的步驟。  

## <a name="folder-and-files-removed-after-computer-restart"></a>在重新啟動電腦之後移除的資料夾和檔案  
 如果將作業系統升級至 Windows 10 的工作順序以及工作順序中的所有其他步驟完成，則除非重新啟動電腦，否則不會移除後置處理和復原指令碼。  這些指令檔未包含機密資訊。  
