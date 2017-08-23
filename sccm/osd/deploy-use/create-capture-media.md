---
title: "建立擷取媒體 - Configuration Manager | Microsoft Docs"
description: "在 Configuration Manager 中使用 [建立工作順序媒體精靈] 建立擷取媒體，以從參照電腦擷取作業系統映像。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5acf800ff5aebd849e294393337755145a60cca5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立擷取媒體

*適用於︰System Center Configuration Manager (最新分支)*

Configuration Manager 中的擷取媒體可讓您從參照電腦擷取作業系統映像。 請在下述情況使用擷取媒體：  

-   [建立工作順序以擷取作業系統](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> 如何建立擷取媒體  
 使用擷取媒體從參照電腦擷取作業系統映像。 擷取媒體包含啟動參照電腦的開機映像，以及擷取作業系統映像的工作順序。

您可使用 [建立工作順序媒體精靈] 建立擷取媒體。 請確定符合下列所有條件之後再執行精靈：  

|工作|說明|  
|----------|-----------------|  
|開機映像|請考慮下列開機映像相關資訊，將在工作順序中使用開機映像來擷取作業系統：<br /><br /> -   開機映像的架構必須適用於目的地電腦的架構。 例如，x64 目的地電腦可以啟動並執行 x86 或 x64 開機映像。 不過，x86 目的地電腦只能啟動並執行 x86 開機映像。<br />-   確定開機映像包含佈建目的地電腦所需的網路及大型存放驅動程式。|  
|發佈與工作順序相關聯的所有內容|您必須將工作順序所需的所有內容都發佈到至少一個發佈點。 這包括開機映像、作業系統映像，以及其他相關聯的檔案。 精靈會在建立獨立媒體時從發佈點收集資訊。 您必須擁有該發佈點上內容庫的 [讀取]  存取權限。  如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。|  
|準備卸除式 USB 磁碟機|針對卸除式 USB 磁碟機：<br /><br /> 如果您即將使用卸除式 USB 磁碟機，USB 磁碟機必須連接至精靈執行所在的電腦，並作為卸除式裝置讓 Windows 能夠偵測到。 精靈會在建立媒體時直接寫入 USB 磁碟機。|  
|建立輸出資料夾|針對 CD/DVD 組：<br /><br /> 在您執行 [建立工作順序媒體精靈] 建立 CD 或 DVD 組的媒體之前，必須先為精靈所建立的輸出檔案建立資料夾。 針對 CD 或 DVD 組所建立的媒體會做為 .iso 檔直接寫入該資料夾中。|  

 利用下列程序建立擷取媒體。  

#### <a name="to-create-capture-media"></a>若要建立擷取媒體  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [工作順序] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立工作順序媒體]  以啟動 [建立工作順序媒體精靈]。  

4.  在 [選取媒體類型]  頁面上，選取 [擷取媒體] ，然後按 [下一步] 。  

5.  在 [媒體類型]  頁面上，指定媒體是快閃磁碟機還是 CD/DVD 組，然後按一下以設定下列項目：  

    -   如果您選取 [USB 快閃磁碟機] ，請指定要儲存內容的磁碟機。  

    -   如果您選取 [CD/DVD 組] ，請指定媒體容量及輸出檔案的名稱和路徑。 精靈會將輸出檔案寫入此位置。 例如︰**\\\servername\folder\outputfile.iso**  

         如果媒體容量太小，無法儲存整個內容，則會建立多個檔案，而且您必須將內容儲存到多個 CD 或 DVD 上。 需要多個媒體時，Configuration Manager 會在其建立的每個輸出檔案名稱上新增序號。 此外，如果您同時部署應用程式與作業系統，且應用程式無法完全安裝在單一媒體上，Configuration Manager 會將應用程式儲存在多個媒體上。 獨立媒體執行時，Configuration Manager 會提示使用者儲存應用程式的下一個媒體。  

        > [!IMPORTANT]  
        >  如果您選取現有的 .iso 映像，[工作順序媒體精靈] 會在您繼續進行精靈的下一頁時從磁碟機或共用刪除映像。 即使您取消精靈，還是會刪除現有映像。  

     按一下 [下一步] 。  

6.  在 [開機映像]  頁面上指定下列資訊，然後按 [下一步] 。  

    > [!IMPORTANT]  
    >  您指定的開機映像架構必須適合參照電腦的架構。 例如，x64 參照電腦可開機且執行 x86 或 x64 開機映像。 不過，x86 參照電腦只能開機和執行 x86 開機映像。  

    -   在 [開機映像]  方塊中，指定要啟動參照電腦的開機映像。  

    -   在 [發佈點]  方塊中，指定開機映像所在的發佈點。 精靈會從發佈點擷取開機映像，並將其寫入至媒體。  

        > [!NOTE]  
        >  您必須擁有發佈點上內容庫的讀取存取權限。  

7.  完成精靈。  
