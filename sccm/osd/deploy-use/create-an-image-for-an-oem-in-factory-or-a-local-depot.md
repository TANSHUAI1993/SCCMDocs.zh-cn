---
title: "建立 OEM 原廠或本機 Depot 的映像 | Microsoft Docs"
description: "使用預先設置的媒體部署，以減少將作業系統部署至尚未完全佈建的電腦時的網路流量。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 07aba04fb1b845e389a5f75b115d536136c1569c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 OEM 原廠或本機 Depot 的映像

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的預先設置媒體部署可讓您將作業系統部署至尚未完全佈建的電腦。 預先設置的媒體是 Windows 映像格式 (WIM) 檔案，可由廠商 (OEM) 或在企業設置中心安裝於未連線 Configuration Manager 環境的裸機電腦。 之後，在 Configuration Manager 環境中，電腦會使用媒體所提供的開機映像啟動，並在預先設置的媒體上執行雜湊檢查確定它有效，然後電腦會連線至站台管理點取得能完成下載程序的可用工作順序。


這種部署方法能夠減少網路流量，因為開機映像和作業系統映像皆已儲存在目的地電腦上。 您可以指定在預先設置媒體中包含應用程式、套件和驅動程式套件。 在電腦上安裝作業系統之後，會先檢查本機工作順序快取的應用程式、套件或驅動程式套件；如果找不到內容或是有所修改，則會從預先設置媒體中設定的發佈點下載內容，然後再進行安裝。  

 您可以在下列作業系統部署案例中使用預先設置的媒體：  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)  

 完成任一作業系統部署案例中的步驟，然後使用下列章節準備和建立預先設置的媒體。  

## <a name="configure-deployment-settings"></a>設定部署設定  
 當您使用預先設置的媒體啟動作業系統部署程序時，必須將部署設定為要對媒體提供作業系統。 您可以在 [部署軟體精靈] 的 [部署設定]  頁面上設定此項目，或是在部署的內容之 [部署設定]  索引標籤上設定此項目。  如果是 [供下列項目使用]  設定，請設定下列其中之一：  

-   **Configuration Manager 用戶端、媒體與 PXE**  

-   **僅媒體與 PXE**  

-   **僅媒體與 PXE (隱藏)**  

## <a name="create-the-prestaged-media"></a>建立預先設置的媒體  
 建立預先設置的媒體檔案以傳送給 OEM 或本機 Depot。 如需詳細資訊，請參閱 [Create prestaged media with System Center Configuration Manager](create-prestaged-media.md)。  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>傳送預先設置的媒體檔案給 OEM 或本機 Depot  
 傳送媒體給 OEM 或本機 Depot 以預先設置電腦。 預先設置的媒體檔案會套用到電腦上的格式化硬碟。  

## <a name="start-the-computer-to-install-the-operating-system"></a>啟動電腦以安裝作業系統  
 預先設置的媒體檔案會套用至電腦。 當第一次啟動電腦時，就會開始作業系統安裝程序。  
