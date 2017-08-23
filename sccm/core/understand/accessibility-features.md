---
title: "協助工具 | Microsoft Docs"
description: "深入了解可供殘障人士使用的 System Center Configuration Manager 功能。"
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: ca518796477dda149a9f4c0ebd65f0a082eab806
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>System Center Configuration Manager 的協助工具功能

*適用對象：System Center Configuration Manager (最新分支)*


System Center Configuration Manager 包含協助殘障人士使用的功能。


## <a name="bkmk_aconsole"></a> Configuration Manager 主控台的協助工具功能  

**1706 版和更新版本的快速鍵和改良功能**

|鍵盤快速鍵|  目的|
|--------|--------|  
|Ctrl + M|將焦點設定在主要 (中央) 窗格上。|
|Ctrl + T|將焦點設定至瀏覽窗格中的最上層節點。 如果焦點已經在該窗格中，則會將焦點設定至您瀏覽的最後一個節點。|
|Ctrl + I|將焦點設定至功能區下的階層連結列。|
|Ctrl + L|將焦點設定至 [搜尋] 欄位 (如果可用)。|
|Ctrl + D|將焦點設定至 [詳細資料] 窗格 (如果可用)。|
|Alt     |在功能區內外切換焦點。|


- 改進當您輸入節點名稱的字母時在瀏覽窗格中的瀏覽。
- 在主要檢視和功能區的鍵盤瀏覽現在是採用循環方式。
- 在詳細資料窗格中的鍵盤瀏覽現在是採用循環方式。 若要返回上一個物件或窗格，請使用 Ctrl + D，然後使用 Shift + TAB。
- 重新整理 [工作區] 檢視之後，焦點會設定至該工作區的主要窗格。
- 修正問題，讓螢幕助讀程式能夠朗讀清單項目的名稱。
- 為頁面上多個控制項新增可存取的名稱，讓螢幕助讀程式能夠朗讀重要資訊。


**下列是適用於所有版本的快速鍵**

- 使用下列鍵盤快速鍵存取工作區：  

|鍵盤快速鍵| 工作區|
|--------|--------|  
|Ctrl + 1| 資產與相容性|
|Ctrl + 2|  軟體程式庫|
|Ctrl + 3|  監視|
|Ctrl + 4|  系統管理|


-   若要存取工作區功能表，請選取 Tab 鍵，直到 [展開/收合] 圖示進入焦點。 接著選取向下鍵以存取工作區功能表。  

-   若要瀏覽工作區功能表，請使用方向鍵。  

-   若要存取工作區中的不同區域，請使用 Tab 鍵和 Shift+Tab 鍵。 若要在工作區的某個區域中瀏覽 (例如功能區)，請使用方向鍵。  

-   若要在焦點位於樹狀節點時存取位址列，請按 Shift+Tab 鍵 3 次。  

-   在精靈或內容頁面中，使用鍵盤快速鍵可在方塊之間移動。 同時選取 Alt 鍵和加底線的字元 (Alt+_) 可選取特定方塊。     

-  若要瀏覽到工作區的不同節點，請輸入節點名稱的第一個字母。 每個按鍵動作都會將游標移至以該字母開頭的下一個節點。 當您使用螢幕助讀程式時，助讀程式會讀出該節點的名稱。

> [!NOTE]  
>  本節提供的資訊僅適用於擁有 Microsoft 產品美國地區授權的使用者。 如果您在美國以外地區取得本產品，可以使用軟體套件隨附的子公司資訊卡，或者瀏覽 [Microsoft 協助工具網站](http://go.microsoft.com/fwlink/?LinkId=8431)，取得 Microsoft 支援服務的連絡資訊。 您可以與您所在地區的子公司連絡，了解本節所述的產品及服務類型是否已於當地銷售。 協助工具的相關資訊另有其他語言版本，包括日文及法文。  

##  <a name="bkmk_ahelp"></a> Configuration Manager 說明的協助工具功能  
 Configuration Manager 說明包含可讓手部缺陷、視力不佳或其他殘障等使用者方便使用的功能。  

|若要執行這項操作|使用此鍵盤快速鍵|  
|----------------|--------------------------------|  
|顯示 [說明] 視窗。|F1|  
|將游標移到 [說明] 主題窗格和瀏覽窗格 ([目錄] 、[搜尋] 和 [索引]  等索引標籤) 之間。|F6|  
|在瀏覽窗格中切換索引標籤 (例如 [內容]、[搜尋] 及 [索引])。|ALT + 索引標籤的底線字母|  
|選取下一個隱藏的文字或超連結。|索引標籤|  
|選取上一個隱藏的文字或超連結。|Shift+Tab|  
|執行所選 [全部顯示]、[全部隱藏]、隱藏文字或超連結的動作。|Enter 鍵|  
|顯示可用於存取任何 [說明] 工具列命令的 [選項]  功能表。|Alt+O|  
|隱藏或顯示包含 [目錄]、[搜尋] 和 [索引] 等索引標籤的窗格。|Alt+O，然後選取 T 鍵|  
|顯示先前檢視過的主題。|Alt+O，然後選取 B 鍵|  
|顯示先前顯示過之系列主題中的下一個主題。|Alt+O，然後選取 F 鍵|  
|回到指定的首頁。|Alt+O，然後選取 H 鍵|  
|防止 [說明] 視窗開啟 [說明] 主題，例如防止網頁進行下載。|Alt+O，然後選取 S 鍵|  
|開啟 Windows Internet Explorer 的 [網際網路選項]  對話方塊，您可以在此對話方塊中變更協助工具設定。|Alt+O，然後選取 I 鍵|  
|重新整理主題，例如連結的網頁。|Alt+O，然後選取 R 鍵|  
|列印書籍中的所有主題，或者只列印所選的主題。|Alt+O，然後選取 P 鍵|  
|關閉 [說明] 視窗。|Alt+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>變更 [說明] 主題的外觀  

1.  若要準備自訂 [說明] 中的色彩、字型樣式和字型大小，請開啟 [說明] 視窗。  

2.  依序選擇 [選項] 和 [網際網路選項]。  

3.  選擇 [一般] 索引標籤中的 [協助工具]。 選擇 [略過網頁上指定的色彩]、[略過網頁上指定的字型樣式] 及 [略過網頁上指定的字型大小]。 您也可以選擇使用在自己的樣式表中所指定的設定。  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>變更說明中的背景或文字色彩  

1.  開啟 [說明] 視窗。  

2.  依序選擇 [選項] 和 [網際網路選項]。  

3.  選擇 [一般] 索引標籤中的 [協助工具]。 接著選擇 [略過網頁上指定的色彩]。 您也可以選擇使用在自己的樣式表中所指定的設定。  

4.  若要自訂 [說明] 中使用的色彩，請在 [一般] 索引標籤上，選擇 [色彩]。 取消選取 [使用 Windows 色彩] 方塊，然後選擇要使用的字型和背景色彩。  

    > [!NOTE]  
    >  如果變更 [說明] 視窗中 [說明] 主題的背景色彩，這項變更也會影響 Windows Internet Explorer 中網頁的背景色彩。  

#### <a name="to-change-the-font-in-help"></a>變更說明中的字型  

1.  開啟 [說明] 視窗。  

2.  依序選擇 [選項] 和 [網際網路選項]。  

3.  選擇 [一般] 索引標籤中的 [協助工具]。 若要使用 Windows Internet Explorer 中所使用的設定，請選擇 [略過網頁上指定的字型樣式] 和 [略過網頁上指定的字型大小]。 您也可以選擇使用在自己的樣式表中所指定的設定。  

4.  若要自訂 [說明] 中使用的字型樣式，請在 [一般] 索引標籤中選擇 [字型]，然後選擇您要使用的字型樣式。  

    > [!NOTE]  
    >  如果變更 [說明] 視窗中 [說明] 主題的字型，這項變更也會影響 Windows Internet Explorer 中網頁的字型。  
