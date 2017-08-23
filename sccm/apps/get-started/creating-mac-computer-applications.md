---
title: "建立 Mac 電腦應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Mac 電腦的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: ffd66a4047ec253704e9772e2c3e3a4d9db7c46f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Mac 電腦應用程式

*適用於：System Center Configuration Manager (最新分支)*

當您建立和部署 Mac 電腦的應用程式時，請記住下列考慮。  

> [!IMPORTANT]  
>  本主題中的程序所涵蓋的資訊，與部署應用程式到安裝 Configuration Manager 用戶端的 Mac 電腦有關。 您向 Microsoft Intune 註冊的 Mac 電腦不支援的應用程式部署。  

## <a name="general-considerations"></a>一般考量  
 您可以使用 System Center Configuration Manager 將應用程式部署到執行 Configuration Manager Mac 用戶端的 Mac 電腦。 將軟體部署到 Mac 電腦的步驟，和用來將軟體部署到 Windows 電腦的步驟類似。 不過，在建立及部署由 Configuration Manager 管理之 Mac 電腦的應用程式之前，請考量以下事項：  

-   在將 Mac 應用程式套件部署到 Mac 電腦之前，您必須使用 Mac 電腦上的 **CMAppUtil** 工具，將這些應用程式轉換為 Configuration Manager 可讀取的格式。  

-   Configuration Manager 不支援對使用者部署 Mac 應用程式。 相反地，這些部署必須對裝置進行。 同樣地，針對 Mac 應用程式部署，Configuration Manager 不支援 [部署軟體精靈] 之 [部署設定] 頁面的 [將軟體預先部署至使用者的主要裝置] 選項。  

-   Mac 應用程式支援模擬部署。  

-   您無法將應用程式部署到具備 [可用] 目的之 Mac 電腦 。  

-   對於 Mac 電腦，並不支援部署軟體時傳送喚醒封包這個選項。  

-   Mac 電腦不支援背景智慧型傳送服務 (BITS) 下載應用程式內容。 如果下載應用程式失敗，即會從頭開始重新啟動。  

-   Configuration Manager 不支援建立 Mac 電腦之部署類型時的全域條件。  

## <a name="steps-to-create-and-deploy-an-application"></a>建立及部署應用程式的步驟  
 下表提供用於建立及部署 Mac 電腦之應用程式的步驟、詳細資料和資訊。  

|步驟|詳細資料|  
|----------|-------------|  
|**步驟 1**：備妥 Configuration Manager 的 Mac 應用程式|從 Mac 軟體套件建立 Configuration Manager 應用程式之前，您必須使用 Mac 電腦上的 **CMAppUtil** 工具，將 Mac 軟體轉換為 Configuration Manager**.cmmac** 檔案。|  
|**步驟 2**：建立包含 Mac 軟體的 Configuration Manager 應用程式|使用 [建立應用程式精靈] 建立 Mac 軟體的應用程式。|  
|**步驟 3**：建立 Mac 應用程式的部署類型|只有當您未從應用程式自動匯入本資訊時，才需要此步驟。|  
|**步驟 4**：部署 Mac 應用程式|使用 [部署軟體精靈] 將應用程式部署到 Mac 電腦。|  
|**步驟 5**：監視 Mac 應用程式的部署|監視對 Mac 電腦的成功應用程式部署。|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>建立及部署 Mac 電腦的應用程式補充程序  
 使用下列程序，建立及部署由 Configuration Manager 管理之 Mac 電腦的應用程式。  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>步驟 1：備妥 Configuration Manager 的 Mac 應用程式  
 建立及部署 Configuration Manager 應用程式到 Mac 電腦的程序，和 Windows 電腦適用的部署程序類似。 不過，在建立包含 Mac 部署類型的 Configuration Manager 應用程式之前，您必須使用 **CMAppUtil** 工具備妥應用程式。 此工具會和 Mac 用戶端安裝檔案一起下載。 **CMAppUtil** 工具會收集與應用程式相關的資訊，包括來自下列 Mac 套件的偵測資料：  

-   Apple 磁碟映像檔 (.dmg)  

-   中繼套件檔案 (.mpkg)  

-   Mac OS X 安裝程式套件 (.pkg)  

-   Mac OS X 應用程式 (.app)  

收集到應用程式資訊後， **CMAppUtil** 接著會建立一支副檔名為 **.cmmac**的檔案。 這支檔案包含 Mac 軟體的安裝檔案，以及有關可用於評估是否已安裝應用程式之偵測方法的資訊。 **CMAppUtil** 也可處理 **.dmg** 檔案，其包含多項 Mac 應用程式，並且為每一個應用程式建立不同部署類型。  

1.  將 Mac 軟體安裝套件複製到 Mac 電腦的資料夾，該資料夾是您擷取從 Microsoft 下載中心下載之 **macclient.dmg** 檔案的內容。  

2.  在相同的 Mac 電腦上，開啟終端機視窗，並瀏覽至您擷取 **macclient.dmg** 檔案之內容所在的資料夾。  

3.  瀏覽至 **Tools** 資料夾並輸入下列命令列命令︰  

     **./CMAppUtil** <屬性\>  

     例如，假設您想要將 Apple 磁碟映像檔 **MySoftware.dmg** 的內容 (儲存在使用者的桌面資料夾) 轉換成相同資料夾中的 **cmmac** 檔案。 您也想要為磁碟映像檔中找到的所有應用程式建立 **cmmac** 檔案。 若要這麼做，請使用以下命令列：  

     **./CMApputil –c /Users/** <使用者名稱\> **/Desktop/MySoftware.dmg -o /Users/** <使用者名稱\> **/Desktop -a**  

    > [!NOTE]  
    >  應用程式名稱不能超過 128 個字元。  

     若要設定 **CMAppUtil**的選項，請使用下表中的命令列內容：  

    |屬性|詳細資訊|  
    |--------------|----------------------|  
    |**-h**|顯示可用的命令列內容。|  
    |**-r**|將所提供之 **detection.xml** 檔案的 **.cmmac** 輸出到 **stdout**。 輸出內容包含偵測參數，以及用於建立 **CMAppUtil** 檔案的 **.cmmac** 版本。|  
    |**-c**|指定要轉換的來源檔案。|  
    |**-o**|和 – c 內容搭配使用來指定輸出路徑。|  
    |**-a**|和 – c 內容搭配使用，為磁碟映像檔中的所有應用程式和套件自動建立 .cmmac 檔案。|  
    |**-s**|如果找不到偵測參數，便可略過產生 **detection.xml** ，並在沒有 **.cmmac** 檔案的情況下，強制建立 **detection.xml** 檔案。|  
    |**-v**|連同診斷資訊一併顯示來自 **CMAppUtil** 工具的更詳細輸出。|  

4.  請確定已在您指定的輸出檔案中建立 **.cmmac** 檔案。  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>建立包含 Mac 軟體的 Configuration Manager 應用程式  

使用下列程序，協助您建立由 Configuration Manager 管理之 Mac 電腦的應用程式。  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，按一下 [建立應用程式]。  

4.  在 [建立應用程式精靈]  的 [一般] 頁面上，選取 [從安裝檔案自動偵測此應用程式的相關資訊] 。  

    > [!NOTE]  
    >  如果您要自行指定應用程式相關資訊，請選取 [手動指定應用程式資訊]。 如需如何手動指定此項資訊的詳細資訊，請參閱[如何使用 System Center Configuration Manager 建立應用程式](../../apps/deploy-use/create-applications.md)。  

5.  在 [類型]  下拉式清單中，選取 [Mac OS X] 。  

6.  在 [位置] 欄位中，以 *\\\\伺服器\>\\<共用\>\\<檔案名稱\>* 格式，將 UNC 路徑指定為 Mac 應用程式安裝檔案 (**.cmmac** 檔案)，以偵測應用程式資訊。 或者，選擇 [瀏覽] 以瀏覽並指定安裝檔案位置。  

    > [!NOTE]  
    >  您必須具備包含應用程式之 UNC 路徑的存取權。  

7.  選擇 [下一步]。  

8.  在 [建立應用程式精靈] 的 [匯入資訊] 頁面，檢閱已匯入的資訊。 必要時，可以選擇 [上一步] 返回並修正錯誤。 選擇 [下一步] 繼續進行。  

9. 在 [建立應用程式精靈] 的 [一般資訊] 頁面上，指定有關應用程式的資訊 (例如應用程式名稱、註解、版本，以及選擇性的參考)，幫助您在 Configuration Manager 主控台中參考應用程式。  

    > [!NOTE]  
    >  此頁面可能已有一些應用程式資訊，如果之前有從應用程式安裝檔案取得的話。  

10. 選擇 [下一步]，並檢閱 [摘要] 頁面上的應用程式資訊，然後完成 [建立應用程式精靈]。  

11. 新應用程式會在 Configuration Manager 主控台的 [應用程式] 節點中顯示。  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>步驟 3：建立 Mac 應用程式的部署類型  
 使用下列程序，協助您建立由 Configuration Manager 管理之 Mac 電腦的部署類型。  

> [!NOTE]  
>  如果您已在 [建立應用程式精靈] 中自動匯入應用程式的相關資訊，則可能已建立應用程式的部署類型。  

1.  在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式]。  

3.  選取應用程式。 然後在 [首頁] 索引標籤的 [應用程式]  群組中，選擇 [建立部署類型] 為此應用程式建立新部署類型。  

    > [!NOTE]  
    >  您也可以從 [建立應用程式精靈] 和 [<應用程式名稱\> 內容] 對話方塊的 [部署類型] 索引標籤，啟動 [建立部署類型精靈]。  

4.  在 [建立部署類型精靈] 的 [一般] 頁面的 [類型] 下拉式清單中，選取 [Mac OS X]。  

5.  在 [位置] 欄位中，以 \\\\<伺服器\>\\<共用\>\\<檔案名稱\> 格式，將 UNC 路徑指定為應用程式安裝檔案 (**.cmmac** 檔案)。 或者，選擇 [瀏覽] 以瀏覽並指定安裝檔案位置。  

    > [!NOTE]  
    >  您必須具備包含應用程式之 UNC 路徑的存取權。  

6.  選擇 [下一步]。  

7.  在 [建立部署類型精靈]  的 [匯入資訊] 頁面，檢閱已匯入的資訊。 必要時，可選擇 [上一步] 返回並修正錯誤。 選擇 [下一步] 以繼續。  

8.  在 [建立部署類型精靈]  的 [一般資訊] 頁面，指定如應用程式名稱、註解和語言等有部署類型可用的應用程式資訊。  

    > [!NOTE]  
    >  此頁面可能已有一些部署類型資訊，如果之前有從應用程式安裝檔案取得的話。  

9. 選擇 [下一步]。  

10. 在 [建立部署類型精靈] 的 [需求] 頁面，可指定在 Mac 電腦上安裝部署類型之前必須先符合哪些條件。  

11. 選擇 [新增] 以開啟 [建立需求] 對話方塊，並增加新的需求。  

    > [!NOTE]  
    >  您也可以將新的需求新增至 [<部署類型名稱\> 內容] 對話方塊的 [需求] 索引標籤。  

12. 從 [類別]  下拉式清單中，選擇此需求用於裝置。  

13. 從 [條件] 下拉式清單中，選取要用於評估 Mac 電腦是否符合安裝需求的條件。 此清單的內容會根據您選取的類別而有所不同。  

14. 從 [運算子] 下拉式清單，選擇將用來比較所選條件和指定值的運算子，以評估使用者或裝置是否符合安裝需求。 可用的運算子會依所選條件而有所不同。  

15. 在 [值] 欄位中，指定將與所選取條件和運算子搭配使用的值，以評估使用者或裝置是否符合安裝需求。 可用的值會依您選取的條件和運算子而有所不同。

16. 選擇 [確定] 以儲存需求規則，然後結束 [建立需求] 對話方塊。  

17. 在 [建立部署類型精靈] 的 [需求] 頁面上，選擇 [下一步]。  

18. 在 [建立部署類型精靈] 的 [摘要]  頁面上 ，檢閱精靈要採取的動作。  必要時，可選擇 [上一步] 返回並變更部署類型設定。 選擇 [下一步] 以建立部署類型。  

19. 在完成 [進度] 頁面之後，檢閱已採取的動作，然後選擇 [關閉] 完成 [建立部署類型精靈]。  

20. 如果從 [建立應用程式精靈] 啟動此精靈，您將會回到 [部署類型] 頁面。  

###  <a name="deploy-the-mac-application"></a>部署 Mac 應用程式  
 將應用程式部署到 Mac 電腦的步驟，和用於將應用程式部署到 Windows 電腦的步驟完全相同，下列差異除外：  

-   不支援對使用者部署應用程式。  

-   不支援具備 [有空]  目的之部署。  

-   [部署軟體精靈] 之 [部署設定] 頁面上的 [將軟體預先部署至使用者的主要裝置] 選項不受支援。  

-   因為 Mac 電腦不支援軟體中心，所以會忽略 [部署軟體精靈] 之 [使用者體驗] 頁面上的 [使用者通知] 設定。  

-   對於 Mac 電腦，並不支援部署軟體時傳送喚醒封包這個選項。  

> [!NOTE]  
>  您可以建立僅包含 Mac 電腦的集合。 若要這麼做，您可建立一個使用查詢規則的集合，然後使用[如何建立查詢](../../core/servers/manage/create-queries.md)主題中的範例 WQL 查詢。  

 如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>步驟 5：監視 Mac 應用程式的部署  
 您可以使用相同程序來監視對 Mac 電腦的應用程式部署，如同您監視對 Windows 電腦的應用程式部署。  

 如需詳細資訊，請參閱[監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  
