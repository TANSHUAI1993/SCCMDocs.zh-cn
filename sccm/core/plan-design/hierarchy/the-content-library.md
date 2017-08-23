---
title: "內容庫 | Microsoft Docs"
description: "了解 System Center Configuration Manager 用來減少整體發佈內容大小的內容庫。"
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fa9f431c00476d71b2b08f92f914d76636d1a27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的內容庫

*適用對象：System Center Configuration Manager (最新分支)*

內容庫是內容的儲存單一版本，而 System Center Configuration Manager 可使用該內容來減少所發佈內容之合併主體的整體大小。 內容庫是存放軟體更新、應用程式、作業系統部署等所有內容檔案的位置。

 - 在**站台伺服器**與每個**發佈點**上自動建立及維護的內容庫複本。

 - 在 Configuration Manager 將內容檔案下載至站台伺服器，或將檔案複製到發佈點之前，Configuration Manager 會先驗證內容庫中是否已存在每個內容檔。
 - 若可使用內容檔，Configuration Manager 並不會複製檔案，而是會建立現有內容檔與應用程式或套件的關聯。

在安裝發佈點的電腦上，可以設定：

- 要建立內容庫的一個或多個磁碟機。
- 每個所使用的磁碟機之優先順序。

當 Configuration Manager 複製內容檔案時，它會複製到優先順序最高的磁碟機，直到該磁碟機的可用空間數少於您指定的下限為止。
- 您可在發佈點安裝期間設定磁碟機設定。
- 完成安裝之後，即無法在發佈點內容中設定磁碟機設定。


如需如何設定發佈點之磁碟機設定的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  


>  [!IMPORTANT]  
>  若要在安裝後將內容庫移至發佈點上的不同位置，請使用 System Center 2012 R2 Configuration Manager Toolkit 中的**內容庫傳輸工具**。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=279566)下載此工具組。  

## <a name="about-the-content-library-on-the-central-administration-site"></a>關於管理中心網站上的內容庫  
 Configuration Manager 預設會在安裝管理中心網站時於站台上建立內容庫。 內容庫將存放於站台伺服器中有最多可用磁碟空間的磁碟機中。 由於您無法在管理中心網站上安裝發佈點，因此無法設定內容庫使用之磁碟機的優先性。 類似於其他站台伺服器上的內容庫和發佈點上的內容庫，當包含內容庫的磁碟機可用磁碟空間不足，內容庫將自動跨越至下個可用的磁碟機。  

 Configuration Manager 在下列案例中會使用管理中心網站上的內容庫︰  

-   在管理中心網站上建立內容時。  

-   當您移轉其他 Configuration Manager 站台的內容時，並將管理中心網站指派為管理內容的站台。  

> [!NOTE]  
>  當您在主要站台建立內容，並將內容發佈至不同的主要站台或不同主要站台之下的次要站台時，管理中心網站會暫時將該內容儲存在管理中心網站上的排程器收件匣中，但不會將該內容新增至其內容庫。  

 使用下列選項在管理中心網站上管理內容庫︰  

-   若要避免將內容庫安裝在特定磁碟機，在建立內容庫之前，請建立一個空白檔案 **no_sms_on_drive.sms**，並將檔案複製到磁碟機的根資料夾。  

-   建立內容庫之後，請使用 System Center 2012 R2 Configuration Manager Toolkit 中的**內容庫傳輸工具**來管理內容庫的位置。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=279566)下載此工具組。  
