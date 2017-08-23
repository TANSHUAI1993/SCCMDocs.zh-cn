---
title: "CD.Latest 資料夾 | Microsoft Docs"
description: "了解從 Configuration Manager 主控台內進行產品更新的新更新程序。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5c39e09b44500fa2f356f83579bb2fb2c1d0e937
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 CD.Latest 資料夾

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 引進新的更新程序，可從 Configuration Manager 主控台內進行產品更新。 為了支援這個 Configuration Manager 的全新更新方法，系統會建立一個名稱為 **CD.Latest** 的新資料夾，此資料夾包含一份適用於您的站台更新版本的 Configuration Manager 安裝檔案。  

從 1606 更新開始，CD.Latest 資料夾包含名為 **Redist** 的資料夾，其中含有安裝程式下載並使用的可轉散發檔案。 這些檔案會與該 CD.Latest 資料夾中找到的 Configuration Manager 檔案版本相符。 當您從 CD.Latest 資料夾執行安裝程式時，必須使用與該版本安裝程式相符的檔案。 若要執行這項操作，您可以指示安裝程式從 Microsoft 下載最新的檔案，或指示安裝程式使用來自 CD.Latest 資料夾隨附之 Redist 資料夾中的檔案。

不過，基準媒體 (例如在 2016 年 10 月發行的基準 1606 版) 不包括 Redist 資料夾。 除非您安裝主控台內更新，否則不會建立 Redist 資料夾。 同時，使用您從基準媒體安裝站台時所使用的 Redist 資料夾。  

> [!TIP]
> 如果您尚未安裝版本 1606，則必須確定所使用的可轉散發套件檔案是最新的。 如果您最近沒有下載可轉散發套件檔案，則可讓安裝程式從 Microsoft 下載。   

 以下是在管理中心網站或主要站台伺服器上建立或更新 [CD.Latest] 資料夾的案例︰  

-   從 Configuration Manager 主控台內安裝更新或 Hotfix︰系統會在 Configuration Manager 安裝資料夾中建立或更新該資料夾。  

-   執行內建的 Configuration Manager 備份工作︰系統會在指定的備份資料夾位置底下建立或更新該資料夾。  

-  從 1606 版開始，當您使用基準媒體 (例如 1606 版和 1702 版) 安裝新的站台時，會建立 CD.Latest 資料夾。

支援使用來自 [CD.Latest] 資料夾的來源檔案進行下列作業：  

1.  **備份及復原：**若要復原站台，您必須使用符合您站台之 CD.Latest 資料夾中的來源檔案。 當您使用內建站台備份工作執行站台備份時，CD.Latest 資料夾會包含為備份的一部分。

    -   **在站台復原過程中重新安裝站台時** ，您是透過備份中包含的 CD.Latest 資料夾來安裝站台。 這會使用與您站台備份和站台資料庫相符的檔案版本來安裝站台。  如果您無法存取正確的 CD.Latest 資料夾版本，您可以透過在實驗室環境中安裝站台，然後更新該站台以符合您想要復原的版本，來取得具有正確檔案版本的 CD.Latest 資料夾。

        > [!IMPORTANT]  
        >  如果沒有正確的 [CD.Latest] 資料夾及其內容可供使用，您就無法復原站台而必須重新安裝。  

    -   當您沒有 [CD.Latest] 資料夾但有正常運作的子主要站台或管理中心網站時，您可以使用該站台做為進行站台復原的參照站台。  

2.  **安裝子主要站台：** 若您要在已安裝一或多個主控台內更新的管理中心網站底下，安裝新的子主要站台，則必須使用安裝程式及來自管理中心網站 CD.Latest 資料夾的來源檔案。 當安裝程式從管理中心網站的 [CD.Latest] 資料夾複本執行時，它會使用與管理中心網站版本相符的安裝來源檔案。 如需詳細資訊，請參閱[使用安裝精靈安裝站台](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)。  

3.  **擴充獨立主要站台：** 藉由安裝新的管理中心網站來擴充獨立主要站台時，您必須使用安裝程式及來自主要站台 CD.Latest 資料夾的來源檔案，來安裝新的管理中心網站。 從主要站台的 [CD.Latest] 資料夾複本執行時，它會使用與主要站台版本相符的安裝來源檔案。 如需詳細資訊，請參閱[使用安裝精靈安裝站台](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)中的[擴充獨立主要站台](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)。

> [!IMPORTANT]  
>  不支援使用已更新的 CD.Latest 來源檔案進行下列作業：  
>   
>  -   為新階層安裝新站台  
>  -   將 Microsoft System Center 2012 Configuration Manager 站台升級至 System Center Configuration Manager
