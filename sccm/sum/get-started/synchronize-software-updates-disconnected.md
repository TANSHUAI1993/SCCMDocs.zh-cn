---
title: "在沒有網際網路連線的情況下同步處理更新 - Configuration Manager | Microsoft Docs"
description: "在與網際網路中斷連線的頂層軟體更新點上，執行軟體更新同步處理。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
ms.openlocfilehash: fd9c1e9418ff1956c6ef98753e23a293440179be
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>從已中斷連線的軟體更新點同步處理軟體更新  

*適用於：System Center Configuration Manager (最新分支)*

 當頂層站台的軟體更新點與網際網路中斷連線時，您必須使用 WSUSUtil 工具的匯出和匯入功能同步處理軟體更新中繼資料。 您可以選擇不在 Configuration Manager 階層中的現有 WSUS 伺服器作為同步處理來源。 本主題提供如何使用 WSUSUtil 工具的匯出和匯入功能的資訊。  

 若要匯出和匯入軟體更新中繼資料，您必須在指定的匯出伺服器上從 WSUS 資料庫匯出軟體更新中繼資料，然後將儲存在本機的授權條款檔案複製到已中斷連線的軟體更新點，然後將軟體更新中繼資料匯入至已中斷連線之軟體更新點上的 WSUS 資料庫。  

 使用下表識別要匯出軟體更新中繼資料的匯出伺服器。  

|軟體更新點|適用於連線軟體更新點的上游更新來源|適用於已中斷連線的軟體更新點的匯出伺服器|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|管理中心網站|Microsoft Update (網際網路)<br /><br /> 現有的 WSUS 伺服器|使用您在 Configuration Manager 環境中所需的軟體更新分類、產品和語言，選擇與 Microsoft Update 同步處理的 WSUS 伺服器。|  
|獨立主要網站|Microsoft Update (網際網路)<br /><br /> 現有的 WSUS 伺服器|使用您在 Configuration Manager 環境中所需的軟體更新分類、產品和語言，選擇與 Microsoft Update 同步處理的 WSUS 伺服器。|  

 請確認已在選取的匯出伺服器上完成軟體更新同步處理，以確定已同步處理最新的軟體更新中繼資料，再啟動匯出程序。 若要確認軟體更新同步處理是否已順利完成，請使用下列程序。  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>確認是否已順利在匯出伺服器上完成軟體更新同步處理  

1.  開啟 WSUS 管理主控台，並連線至匯出伺服器上的 WSUS 資料庫。  

2.  在 WSUS 管理主控台中，按一下 [同步處理] 。 結果窗格中會顯示軟體更新同步處理次數清單。  

3.  在結果窗格中，找到最新軟體更新同步處理次數，並確認其已順利完成。  

> [!IMPORTANT]  
>  WSUSUtil 工具必須在匯出伺服器的本機上執行，才能匯出軟體更新中繼資料，此工具還必須在已中斷連線的軟體更新點伺服器上執行，以匯入軟體更新中繼資料。 此外，執行 WSUSUtil 工具的使用者必須是每一部伺服器之本機 Administrators 群組成員。  

## <a name="export-process-for-software-updates"></a>軟體更新的匯出程序  
 軟體更新的匯出程序包含兩個主要步驟：將儲存在本機的授權條款檔案複製到已中斷連線的軟體更新點，並從匯出伺服器上的 WSUS 資料庫匯出軟體更新中繼資料。  

 使用下列程序，將本機授權條款中繼資料複製到已中斷連線的軟體更新點。  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>將本機檔案從匯出伺服器複製到已中斷連線的軟體更新點伺服器  

1.  在匯出伺服器上，瀏覽至儲存軟體更新的軟體更新和授權條款的資料夾。 依預設，WSUS 伺服器會將檔案儲存在 <WSUS 安裝磁碟機>\WSUS\WSUS 內容\\中，其中 <WSUS 安裝磁碟機> 是安裝 WSUS 的磁碟機。  

2.  將所有檔案和資料夾從此位置複製到已中斷連線之軟體更新點伺服器上的 WSUSContent 資料夾。  

 在匯出伺服器上使用下列程序，從 WSUS 資料庫匯出軟體更新中繼資料。  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>從匯出伺服器上的 WSUS 資料庫匯出軟體更新中繼資料  

1.  在匯出伺服器上的命令提示字元中，巡覽至包含 WSUSutil.exe 的資料夾。 根據預設，這項工具位於 %*ProgramFiles*%\Update Services\Tools 中。 例如，若工具位於預設位置，請輸入 **cd %ProgramFiles%\Update Services\Tools**。  

2.  輸入下列內容，將軟體更新中繼資料匯出至套件檔案：  

     **wsusutil.exe 匯出**  *packagename*  *logfile*  

     例如：  

     **wsusutil.exe export export.cab export.log**  

     格式摘要如下：WSUSutil.exe 後面接著 export 選項、匯出作業期間建立的匯出 .cab 檔案名稱，以及記錄檔的名稱。 WSUSutil.exe 會從匯出伺服器匯出中繼資料，並建立操作的記錄檔。  

    > [!NOTE]  
    >  套件 (.cab 檔案) 和記錄檔名稱在目前的資料夾中必須是唯一的。  

3.  將匯出套件移至匯入 WSUS 伺服器上包含 WSUSutil.exe 的資料夾。  

    > [!NOTE]  
    >  如果您將套件移至此資料夾，匯入程序會更加容易。 您可以將套件移至任何可存取匯入伺服器的位置，然後在執行 WSUSutil.exe 時指定此位置。  

## <a name="import-software-updates-metadata"></a>匯入軟體更新中繼資料  
 使用下列程序，將軟體更新中繼資料從匯出伺服器匯入至已中斷連線的軟體更新點。  

> [!IMPORTANT]  
>  絕對不可匯入來自任何您不信任之來源所匯出的資料。 如果從不信任來源匯入內容，可能會危及 WSUS 伺服器的安全性。  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>將中繼資料匯入至匯入伺服器的資料庫  

1.  在匯入 WSUS 伺服器上的命令提示字元中，巡覽至包含 WSUSutil.exe 的資料夾。 根據預設，這項工具位於 %*ProgramFiles*%\Update Services\Tools 中。  

2.  輸入下列命令：  

     **wsusutil.exe 匯入**  *packagename*  *logfile*  

     例如：  

     **wsusutil.exe import export.cab import.log**  

     格式摘要如下：WSUSutil.exe 後方接著 import 命令、匯出作業期間建立的套件檔案 (.cab) 名稱、套件檔案的路徑名稱 (如果位於不同的資料夾)，以及記錄檔的名稱。 WSUSutil.exe 會匯入來自匯出伺服器的中繼資料，並建立操作的記錄檔。  

## <a name="next-steps"></a>後續步驟
在您第一次同步處理軟體更新之後，或有新的分類或產品可用之後，必須[設定新的分類和產品](configure-classifications-and-products.md)，使用新的準則來同步處理軟體更新。

使用您需要的準則同步處理軟體更新之後，請[管理軟體更新的設定](manage-settings-for-software-updates.md)。  
