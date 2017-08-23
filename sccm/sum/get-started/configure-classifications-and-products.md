---
title: "設定要同步處理的分類和產品 | Microsoft Docs"
description: "請遵循下列步驟，在 Configuration Manager 主控台中設定要同步處理的分類和產品。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 2da61e6e06850b36543b9fd41bd9a7d2368006fb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>設定要同步處理的分類和產品  

*適用對象：System Center Configuration Manager (最新分支)*


> [!NOTE]  
>  本節中的程序僅適用於頂層站台。  

 根據您在軟體更新點元件內容中指定的設定，Configuration Manager 在同步處理期間會擷取軟體更新中繼資料。 第一次同步處理軟體更新後，或發行新產品和分類時，您必須移至 [內容] 選取新的項目。 利用下列程序設定要同步處理的分類和產品。  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>若要設定要同步處理的分類和產品  

1.  在 **Configuration Manager** 主控台中，瀏覽至 [管理] > [站台設定] > [站台]。

2. 選取管理中心網站或獨立主要站台。  

3.  在 [首頁]  索引標籤的 [設定]  群組中，按一下 [設定站台元件] ，然後按一下 [軟體更新點] 。

4.  在 [分類]  索引標籤上，指定要同步處理其軟體更新的軟體更新分類。  

    > [!NOTE]  
    >  每個軟體更新都利用有助於組織不同類型更新的更新分類來加以定義。 在同步處理程序期間，將會同步處理指定分類的軟體更新中繼資料。 Configuration Manager 提供了同步處理下列更新分類之軟體更新的功能：  
    >   
    > - **重大更新：**針對特定問題指定廣為發行的更新，以解決重大、與安全性無關的錯誤。  
    > - **定義更新：**將更新指定至病毒或其他定義檔案。  
    > - **Feature Pack**：指定產品版本範圍以外的新產品功能，以及一般包含在下一個完整產品版本的功能。  
    > - **安全性更新：**針對產品特定、與安全相關的問題，指定廣為發行的更新。  
    > - **Service Pack：**指定適用於應用程式的累計 Hotfix 集。 這些 Hotfix 可能包含安全性更新、重大更新、軟體更新等。  
    > - **工具：**指定有助於完成一或多項工作的公用程式或功能。  
    > - **更新彙總套件：**指定封裝在一起以便於部署的累計 Hotfix 集。 這些 Hotfix 可能包含安全性更新、重大更新、更新等。 更新彙總套件一般處理特定領域，例如安全性或產品元件。  
    > - **更新：**指定給目前已安裝的應用程式或檔案的更新。  
    > - **升級**︰指定 Windows 10 特性與功能的升級。 軟體更新點和站台至少必須執行 WSUS 4.0 搭配 [Hotfix 3095113](https://support.microsoft.com/kb/3095113)，才能取得**升級**分類。    
    >       

    > [!NOTE]    
    > 從 Configuration Manager 1706 版開始，您也可以選取 [包含 Microsoft Surface 驅動程式與韌體更新] 核取方塊，以同步處理 Microsoft Surface 驅動程式。 所有軟體更新點必須都執行 Windows Server 2016，才能順利同步處理 Surface 驅動程式。     
    >    
    > 這是發行前版本功能。 發行前版本功能會包含在產品內，以便在生產環境中進行早期測試，但不應視為生產環境就緒。 您必須開啟這項功能才能使用。 如需詳細資訊，請參閱[使用發行前版本功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

5.  在 [產品]  索引標籤上，指定要同步處理其軟體更新的產品，然後按一下 [關閉] 。  

    > [!NOTE]  
    >  各個軟體更新的中繼資料會針對適用的更新定義產品。 產品即為特定版本的作業系統或應用程式 (例如 Windows Server 2012)。 而產品系列則是指衍生出個別產品的基礎作業系統或應用程式。 產品系列的範例有 Windows，Windows Server 2012 就是其中的成員。 您可以指定產品系列或產品系列中的個別產品。 您選取的產品越多，同步處理軟體更新的時間就越長。  
    >   
    >  當軟體更新套用到多項產品，而且至少已選取其中一項產品進行同步處理時，所有的產品都會顯示於 Configuration Manager 主控台，即使未選取某些產品。 例如，如果 Windows Server 2012 是您唯一選取的作業系統，而軟體更新套用至 Windows 8 和 Windows Server 2012，則這兩項產品都會顯示在 Configuration Manager 主控台中。  

    > [!IMPORTANT]  
    >  Configuration Manager 儲存了一份產品及產品系列清單，您第一次安裝軟體更新點時就是在這份清單中選擇。 在您完成軟體更新同步處理之前，可能無法選取在 Configuration Manager 發行後發行的產品和產品系列，因為同步處理會更新可供您選擇的可用產品和產品系列清單。  

## <a name="next-steps"></a>後續步驟
開始軟體更新同步處理，根據新準則擷取軟體更新。 如需詳細資訊，請參閱[同步處理軟體更新](synchronize-software-updates.md)。
