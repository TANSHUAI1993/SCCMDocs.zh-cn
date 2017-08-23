---
title: "使用工作順序以管理虛擬硬碟 | Microsoft Docs"
description: "建立和修改 VHD、新增應用程式和軟體更新，並將 VHD 從 Configuration Manager 發行至 System Center Virtual Machine Manager (VMM)。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: f77af4b8fcb193ed44511c0e5eea7290f55dbbf8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>使用工作順序管理 System Center Configuration Manager 中的虛擬硬碟

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中，您可以管理虛擬硬碟 (VHD)，並將您建立的 VHD 從 Configuration Manager 主控台整合至資料中心。 尤其是，您可以建立和修改 VHD、將應用程式和軟體更新新增至 VHD，並將 VHD 從 Configuration Manager 主控台發行至 System Center Virtual Machine Manager (VMM)。  

 請使用下面各節管理 Configuration Manager 中的 VHD。

## <a name="prerequisites"></a>先決條件  
 在您開始之前，請確認下列必要條件：  

-   您用來管理 VHD 的電腦必須執行下列其中一種作業系統：  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   必須在 BIOS 中啟用虛擬化，而且必須在您執行 Configuration Manager 主控台以管理 VHD 的電腦上安裝 Hyper-V。 您可以安裝 Hyper-V 管理工具以協助您測試及疑難排解虛擬硬碟，這同時也是最佳作法。 舉例來說，若要監視 smsts.log 檔案以追蹤工作順序在 Hyper-V 中的進度，您必須先安裝 Hyper-V 管理工具。 如需 Hyper-V 需求的詳細資訊，請參閱 [Hyper-V 安裝必要條件](http://technet.microsoft.com/library/cc731898.aspx)。  

    > [!IMPORTANT]  
    >  建立 VHD 的程序會耗用處理器的時間和記憶體。 因此，建議您從未安裝在站台伺服器上的 Configuration Manager 主控台來管理 VHD。  

-   當您從站台伺服器的遠端電腦管理 VHD 時，站台伺服器必須具有 VHD 檔案所在之資料夾的 [寫入]  存取權限。  

-   確認您用來管理 VHD 的電腦擁有足夠的可用磁碟空間。 VHD 的硬碟空間需求會根據您安裝的作業系統和應用程式而有所不同。  

-   確認您用來管理 VHD 的電腦擁有足夠的記憶體。 在建立 VHD 的程序期間，虛擬機器會設定為使用 2 GB 的記憶體。  

-   在您用來上傳 VHD 至 VMM 的電腦上安裝 System Center Virtual Machine Manager (VMM) 主控台。 您可以將 VMM 主控台安裝在用來管理 VHD 的電腦上，這表示您不再需要安裝 Hyper-V 將 VHD 匯入 VMM。  

    > [!NOTE]  
    >  如果您在開啟 Configuration Manager 主控台時安裝 VMM 主控台，則必須在 VMM 主控台安裝完成之後重新啟動 Configuration Manager 主控台。 否則，Configuration Manager 將無法順利連線至 VMM 管理伺服器以上傳 VHD。  

##  <a name="BKMK_CreateVHDSteps"></a> 建立 VHD 的步驟  
 若要建立 VHD，您必須建立包含建立 VHD 的步驟的工作順序，然後在建立虛擬硬碟精靈中使用該工作順序來建立 VHD。 以下各節提供建立 VHD 的步驟。  

###  <a name="BKMK_CreateTS"></a> 建立 VHD 的工作順序  
 您必須建立工作順序，其中將包含建立 VHD 的步驟。 在建立工作順序精靈中，您可以使用 [安裝現有的映像套件至虛擬硬碟]  選項來完成建立 VHD 的步驟。 舉例來說，精靈會新增下列必要步驟：重新啟動 Windows PE、格式化及分割硬碟、套用作業系統以及將電腦關機。 您無法在完整的作業系統中建立 VHD。 此外，Configuration Manager 必須等待虛擬機器關機之後才能完成套件。 根據預設，精靈在將虛擬機器關機之前會等候 5 分鐘。 在建立工作順序之後，您可以視需要新增其他步驟。  

> [!IMPORTANT]  
>  下列程序會使用 [安裝現有的映像套件至虛擬硬碟]  選項建立工作順序，這會自動包含成功建立 VHD 所需要的步驟。 如果您選擇使用現有的工作順序或手動建立工作順序，請務必將電腦關機的步驟新增至工作順序的結尾。 如果不執行此步驟，則不會刪除暫時虛擬機器，使得建立 VHD 的程序無法完成。 不過，精靈將會完成並報告成功狀態。  

 使用下列程序建立工作順序以建立 VHD：  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>若要建立工作順序以建立 VHD  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，按一下 [安裝現有的映像套件至虛擬硬碟] ，然後按 [下一步] 。  

5.  在 [工作順序資訊]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **工作順序名稱**：指定識別工作順序的名稱。  

    -   **描述**：指定工作順序的描述。  

    -   **開機映像**：指定在目的地電腦上安裝作業系統的開機映像。 如需詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

6.  在 [安裝 Windows]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **映像套件**：指定包含要安裝之作業系統映像的套件。  

    -   **映像**：如果作業系統映像套件包含多個映像，請指定要安裝之作業系統映像的索引。  

    -   **產品金鑰**：指定要安裝之 Windows 作業系統的產品金鑰。 您可以指定編碼的大量授權金鑰和標準產品金鑰。 如果您使用非編碼的產品金鑰，則必須以破折號 (-) 分隔字元，每 5 個字元為一組。 例如： *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **伺服器授權模式**：指定伺服器授權為 [按照基座] 、[按照伺服器] ，或者不指定授權。 如果伺服器授權為 [按照伺服器] ，請同時指定伺服器連線數目上限。  

    -   指定如何處理部署作業系統映像時使用的系統管理員帳戶。  

        -   **隨機產生本機系統管理員密碼，並停用所有支援平台上的帳戶 (建議)**：使用此設定，使精靈可隨機建立本機系統管理員帳戶密碼，並在部署作業系統映像時停用帳戶。  

        -   **啟用帳戶並指定本機系統管理員密碼**：使用此設定，在部署作業系統映像的所有電腦上使用本機系統管理員帳戶的特定密碼。  

7.  在 [設定此網路]  頁面指定下列設定，然後按 [下一步] 。  

    -   **加入工作群組**：指定是否將目的地電腦加入工作群組。  

    -   **加入網域**：指定是否將目的地電腦加入網域。 在 [網域] 中，指定網域名稱。  

        > [!IMPORTANT]  
        >  您可以進行瀏覽，尋找本機樹系中的網域，但是必須指定遠端樹系的網域名稱。  

         您也可以指定組織單位 (OU)。 這是選用設定，會指定要建立電腦帳戶所在 OU 的 LDAP X.500 辨別名稱 (如果帳戶尚未存在)。  

    -   **帳戶**：指定具有加入指定網域權限之帳戶的使用者名稱和密碼。 例如： *網域\使用者* 或 *%變數%*。  

8.  在 [安裝 Configuration Manager] 頁面上，指定在目的地電腦上安裝 Configuration Manager 用戶端套件，然後按 [下一步]。  

9. 在 [安裝應用程式]  頁面上，指定要安裝在目的地電腦上的應用程式，然後按 [下一步] 。 如果您指定多個應用程式，也可以指定工作順序在特定應用程式安裝失敗時繼續執行。  

10. 完成精靈。  

###  <a name="BKMK_CreateVHD"></a> 建立 VHD  
 在建立 VHD 的工作順序之後，請使用建立虛擬硬碟精靈來建立 VHD。  

> [!IMPORTANT]  
>  在執行此程序之前，請確認您符合本主題一開始所列出的必要條件。  

 使用下列程序建立 VHD。  

#### <a name="to-create-a-vhd"></a>若要建立 VHD  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [虛擬硬碟] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立虛擬硬碟]  啟動 [建立虛擬硬碟精靈]。  

    > [!NOTE]  
    >  Hyper-V 必須安裝在執行 Configuration Manager 主控台以管理 VHD 的電腦上，否則就是未啟用 [建立虛擬硬碟] 選項。 如需 Hyper-V 需求的詳細資訊，請參閱 [Hyper-V 安裝必要條件](http://technet.microsoft.com/library/cc731898.aspx)。  

    > [!TIP]  
    >  若要組織您的 VHD，請建立新的資料夾，或在 [虛擬硬碟]  節點下方選取現有的資料夾，然後在資料夾中按一下 [建立虛擬硬碟]  。  

4.  在 [一般]  頁面上指定以下設定，然後按 [下一步] 。  

    -   **名稱**：指定 VHD 的唯一名稱。  

    -   **版本**：指定 VHD 的版本號碼。 這是選擇性的設定。  

    -   **註解**：指定 VHD 的描述。  

    -   **路徑**：指定精靈將用來建立 VHD 檔案的路徑和檔案名稱。  

         您必須以 UNC 格式輸入有效的網路路徑。 例如︰**\\\servername\\<sharename\>\\<filename\>.vhd**。  

        > [!WARNING]  
        >  Configuration Manager 必須具有指定路徑的「寫入」存取權才能建立 VHD。 如果 Configuration Manager 無法存取路徑，則會在站台伺服器的 distmgr.log 檔案中記錄相關錯誤。  

5.  在 [工作順序]  頁面中，指定您在上一節中指定的工作順序，然後按 [下一步] 。  

6.  在 [發佈點]  頁面中，選取一個或多個包含工作順序所需內容的發佈點，然後按 [下一步] 。  

7.  在 [自訂]  頁面上，按 [下一步] 。 建立 VHD 的程序會忽略您在此頁面指定的任何設定。  

8.  在確認這些設定後按 [下一步] 。 精靈隨即會建立 VHD。  

    > [!TIP]  
    >  完成 VHD 建立程序的時間可能不盡相同。 當精靈執行此程序時，您可以監視下列記錄檔以追蹤進度。 記錄檔預設會位於執行 Configuration Manager 主控台的電腦上，並位於 %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog 的路徑。  
    >   
    >  -   **CreateTSMedia.log**：精靈會在建立工作順序媒體時將資訊寫入此記錄檔。 檢閱此記錄檔，追蹤精靈在建立獨立媒體時的進度。  
    > -   **DeployToVHD.log**：精靈會在執行建立 VHD 的程序時將資訊寫入此記錄檔。 檢閱此記錄檔，追蹤精靈在建立獨立媒體之後的所有步驟進度。  
    >   
    >  此外，當作業系統安裝開始時，您可以開啟 Hyper-V Manager (如果您已在電腦上安裝 Hyper-V 管理工具) 並連線至精靈建立的暫時虛擬機器，查看執行中的工作順序。 您可以在虛擬機器上監視 smsts.log 檔案以追蹤工作順序的進度。 如果完成工作順序的步驟發生問題，可使用此記錄檔來協助您疑難排解問題。 硬碟格式化之前，smsts.log 檔案位於 x: \windows\temp\smstslog\smsts.log，硬碟格式化之後位於 c:\\_SMSTaskSequence\Logs\Smstslog\。 在工作順序步驟完成之後，系統會在 5 分鐘之後 (根據預設) 將虛擬機器關機並且予以刪除。  

 在 Configuration Manager 建立 VHD 之後，VHD 會放在 [軟體程式庫] 工作區之 [作業系統部署] 節點下的 Configuration Manager 主控台的 [虛擬硬碟] 節點。  

> [!NOTE]  
>  Configuration Manager 會連線至 VHD 的來源位置，以擷取 VHD 的大小。 如果 Configuration Manager 無法存取 VHD 檔案，VHD 的 [大小 (KB)] 資料行就會顯示 **0**。  

##  <a name="BKMK_ModifyVHDSteps"></a> 修改現有 VHD 的步驟  
 若要修改 VHD，您必須使用修改 VHD 的必要步驟來建立工作順序。 接著，請在修改虛擬硬碟精靈中選取該工作順序。 此精靈會將 VHD 連結到虛擬機器、在 VHD 中執行工作順序，然後更新 VHD 檔案。 以下各節提供修改 VHD 的步驟。  

###  <a name="BKMK_ModifyTS"></a> 建立工作順序以修改 VHD  
 若要修改現有的 VHD，您必須先建立工作順序。 請只選擇修改工作順序所需的步驟。 例如，如果您要新增應用程式到 VHD，請建立自訂工作順序，然後只加入「安裝應用程式」的步驟。  

 請使用下列程序建立工作順序以修改 VHD。  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>建立自訂工作順序以修改 VHD  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序]  啟動 [建立工作順序精靈]。  

4.  在 [建立新的工作順序]  頁面上，選取 [建立新的自訂工作順序] ，然後按 [下一步] 。  

5.  在 [工作順序資訊]  頁面上指定下列設定，然後按 [下一步] 。  

    -   **工作順序名稱**：指定識別工作順序的名稱。  

    -   **描述**：指定工作順序的描述。  

    -   **開機映像**：指定在目的地電腦上安裝作業系統的開機映像。 如需詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

6.  完成精靈。  

 請使用下列程序將工作順序步驟新增到自訂工作順序。  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>新增工作順序步驟到自訂工作順序  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，按一下 [工作順序] ，然後您在前面的程序中建立的自訂工作順序。  

3.  在 [首頁]  索引標籤的 [工作順序]  群組中，按一下 [編輯]  ，啟動匯出工作順序編輯器。  

4.  新增用來修改 VHD 的工作順序步驟。  

5.  按一下 [確定]  ，結束工作順序編輯器。  

###  <a name="BKMK_ModifyVHD"></a> 修改 VHD  
 在建立 VHD 的工作順序之後，請使用修改虛擬硬碟精靈來修改 VHD。  

 請使用下列程序修改 VHD。  

#### <a name="to-modify-a-vhd"></a>修改 VHD  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，按一下 [虛擬硬碟] ，然後選取要修改的 VHD。  

3.  在 [首頁]  索引標籤的 [虛擬硬碟]  群組中，按一下 [修改虛擬硬碟]  ，啟動修改虛擬硬碟精靈。  

    > [!NOTE]  
    >  Hyper-V 必須安裝在執行 Configuration Manager 主控台以管理 VHD 的電腦上，否則就是未啟用 [修改虛擬硬碟] 選項。 如需 Hyper-V 需求的詳細資訊，請參閱 [Hyper-V 安裝必要條件](http://technet.microsoft.com/library/cc731898.aspx)。  

4.  在 [一般]  頁面上，確認下列設定，然後按 [下一步] 。  

    -   **名稱**：指定 VHD 的唯一名稱。  

    -   **版本**：指定 VHD 的版本號碼。 這是選擇性的設定。  

    -   **註解**：指定 VHD 的描述。  

    -   **路徑**：指定建立 VHD 檔案所在的路徑和檔案名稱。 您無法修改這項設定。  

        > [!WARNING]  
        >  Configuration Manager 必須具有指定路徑的「寫入」存取權才能建立 VHD。 如果 Configuration Manager 無法存取路徑，則會在站台伺服器的 distmgr.log 檔案中記錄相關錯誤。  

5.  在 [工作順序]  頁面中，指定您在上一節建立的自訂工作順序，然後按 [下一步] 。  

6.  在 [發佈點]  頁面中，選取一個或多個包含工作順序所需內容的發佈點，然後按 [下一步] 。  

7.  在 [自訂]  頁面上，按 [下一步] 。 修改 VHD 的程序會忽略您在此頁面指定的任何設定。  

8.  在確認這些設定後按 [下一步] 。 精靈隨即會建立已修改的 VHD。  

    > [!TIP]  
    >  完成 VHD 修改程序的時間可能不盡相同。 當精靈執行此程序時，您可以監視下列記錄檔以追蹤進度。 記錄檔預設會位於執行 Configuration Manager 主控台的電腦上，並位於 %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog 的路徑。  
    >   
    >  -   **CreateTSMedia.log**：精靈會在建立工作順序媒體時將資訊寫入此記錄檔。 檢閱此記錄檔，追蹤精靈在建立獨立媒體時的進度。  
    > -   **DeployToVHD.log**：精靈會在執行修改 VHD 的程序時將資訊寫入此記錄檔。 檢閱此記錄檔，追蹤精靈在建立獨立媒體之後的所有步驟進度。  
    >   
    >  此外，您也可以開啟 Hyper-V Manager (如果您已在電腦上安裝 Hyper-V 管理工具) 並連線至精靈建立的暫時虛擬機器，查看執行中的工作順序。 您可以在虛擬機器上監視 smsts.log 檔案以追蹤工作順序的進度。 如果完成工作順序的步驟發生問題，可使用此記錄檔來協助您疑難排解問題。 硬碟格式化之前，smsts.log 檔案位於 x: \windows\temp\smstslog\smsts.log，硬碟格式化之後位於 c:\\_SMSTaskSequence\Logs\Smstslog\。 在工作順序步驟完成之後，系統會在 5 分鐘之後 (根據預設) 將虛擬機器關機並且予以刪除。  

##  <a name="BKMK_ApplyUpdates"></a> 將軟體更新套用至 VHD  
 適用於 VHD 中作業系統的新軟體更新會定期發行。 您可以依指定的排程將適用的軟體更新套用至 VHD。 在您指定的排程上，Configuration Manager 會套用您為 VHD 選取的軟體更新。  

 有關 VHD 的資訊會儲存在站台資料庫中，包括建立 VHD 時已套用的軟體更新。 最初建立時已套用至 VHD 的軟體更新也會儲存在站台資料庫中。 當您啟動精靈將軟體更新套用至 VHD 時，精靈會擷取尚未套用至 VHD 的可用軟體更新清單供您選取。  

 您可以選取 [發生錯誤時仍繼續] 設定，讓 Configuration Manager 繼續套用軟體更新，即使發生錯誤仍然套用一或多個您所選取的軟體更新。  

> [!NOTE]  
>  軟體更新會從站台伺服器上的內容庫複製。  

 請使用下列程序將軟體更新套用至 VHD。  

#### <a name="to-apply-software-updates-to-a-vhd"></a>若要將軟體更新套用至 VHD  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [虛擬硬碟] 。  

3.  選取要套用軟體更新的 VHD。  

4.  在 [首頁]  索引標籤的 [虛擬硬碟]  群組中，按一下 [排程更新]  啟動精靈。  

5.  在 [選擇更新]  頁面上，選取要套用至 VHD 的軟體更新，然後按 [下一步] 。  

6.  在 [設定排程]  頁面上指定下列設定，然後按 [下一步] 。  

    1.  **排程**：指定將軟體更新套用至 VHD 的排程。  

    2.  **發生錯誤時繼續**：選取此選項，即使發生錯誤仍會將軟體更新套用至映像。  

7.  確認 [摘要]  頁面中的資訊，然後按 [下一步] 。  

8.  在 [完成]  頁面上，確認軟體更新已成功套用至作業系統映像。  

##  <a name="BKMK_ImportToVMM"></a> 將 VHD 匯入至 System Center Virtual Machine Manager  
 System Center VMM 是一種虛擬資料中心的管理解決方案，可讓您設定及管理虛擬主機、網路和儲存資源，以在您建立的私人雲端上建立及部署虛擬機器和服務。 在 Configuration Manager 中建立 VHD 之後，您就可以使用 VMM 來匯入和管理 VHD。  

> [!TIP]  
>  將 VHD 上傳至 VMM 之前，請確認 VMM 主控台可成功連線至 VMM 管理伺服器。  

 使用下列程序將 VHD 匯入 VMM。  

#### <a name="to-import-a-vhd-to-vmm"></a>若要將 VHD 匯入 VMM  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [虛擬硬碟] 。  

3.  在 [首頁]  索引標籤的 [虛擬硬碟]  群組中，按一下 [上傳到 Virtual Machine Manager]  以開始上傳到 Virtual Machine Manager 精靈。  

4.  在 [一般]  頁面上，設定下列設定，然後按 [下一步] 。  

    -   **VMM 伺服器名稱**：指定要安裝 VMM 管理伺服器的電腦 FQDN。 精靈會連線至 VMM 管理伺服器以下載伺服器的程式庫共用。  

    -   **VMM 程式庫共用**：在下拉式清單中指定 VMM 程式庫共用。  

    -   **使用未加密的傳輸**：選擇此設定，將 VHD 檔案傳輸至 VMM 管理伺服器且不使用加密。  

5.  在摘要頁面上確認這些設定，然後完成精靈。 上傳 VHD 所需要的時間會根據 VHD 檔案的大小以及 VMM 管理伺服器的網路頻寬而有所不同。  
