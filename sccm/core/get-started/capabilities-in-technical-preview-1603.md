---
title: "Technical Preview 1603 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1603 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: dee2b4ce042bb4a434bb019e17a6b16e2807945c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1603 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1603 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 或者，當您使用 System Center Technical Preview 5 時，此版本會安裝成 System Center Configuration Manager Technical Preview 的基準版本。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

 **此 Technical Preview 的已知問題：**  

-   此版本包含先前所發行功能的更新，但並未導入新功能。 因此，如果您先前已升級到 1602 並啟用 1602 包含的所有功能，「更新精靈」的 [功能] 頁面將會是空白的。  

-   在您的站台伺服器更新到 Technical Preview 1603 之後，用戶端也必須一併更新到 1603 版本，才能使用任何遠端控制功能。  

 **以下是您可以使用此版本試用的新功能。**  

##  <a name="BKMK_SC1603"></a> 軟體中心的增強功能  

### <a name="new-tiled-view-for-apps"></a>新的應用程式並排顯示檢視  
 使用者現在可以在「軟體中心」的 [應用程式] 索引標籤中，於應用程式清單或應用程式並排顯示檢視之間做選擇。  

### <a name="select-multiple-updates-in-software-center"></a>在軟體中心中選取多個更新  
 在「軟體中心」的 [更新] 索引標籤中，您現在可以選取多個更新或選取 [全部更新]，以開始同時安裝多個更新。  

##  <a name="BKMK_RC1603"></a> 對遠端控制的改進  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>限制遠端控制工作階段中的共用剪貼簿存取  
 您現在可以啟用新的遠端工具用戶端設定 「Prompt user for shared clipboard file transfer permission」 (提示使用者提供共用剪貼簿檔案傳輸權限)，以限制對遠端控制工作階段中共用剪貼簿的存取。  

 啟用時，共用遠端工作階段的使用者必須先將權限授與該工作階段的檢視者，該檢視者才能透過共用剪貼簿將檔案從該工作階段傳輸到其本機電腦。  

 這會如同先前一樣為使用者增加一層保護，如果檢視者獲授與使用者電腦的完整控制權，他們將能以該使用者完全無法察覺的方式，使用共用剪貼簿將檔案從工作階段傳輸到其本機電腦。  

##  <a name="BKMK_RamDiskTFTP"></a> 自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊大小和視窗大小  
 在 1603 Technical Preview 中，您可以為支援 PXE 的發佈點自訂 RamDisk TFTP 區塊大小和視窗大小。 如果您已自訂網路，可能會導致開機映像下載因發生逾時錯誤而失敗，因為區塊或視窗大小太大。 自訂 RamDisk TFTP 區塊大小和視窗大小可讓您在使用 PXE 來滿足特定的網路需求時，將 TFTP 流量最佳化。   
您將需要在您的環境中測試自訂的設定，以確定最有效率的設定是哪一個。  

-   **TFTP 區塊大小**︰區塊大小是伺服器傳送給下載檔案之用戶端的資料封包大小 (如 RFC 2347 所述)。 區塊大小越大，伺服器傳送的封包就越少，因此伺服器與用戶端之間的來回延遲也較少。 不過，較大的區塊大小會導致封包分散，而大多數 PXE 用戶端實作並不支援分散的封包。  

-   **TFTP 視窗大小**：TFTP 針對每個傳送的資料區塊都會要求一個認可 (ACK) 封包。 伺服器在收到上一個區塊的 ACK 封包之前，不會傳送順序中的下一個區塊。 TFTP 視窗化是「Windows 部署服務」中的一項功能，可讓您定義填滿視窗所需的資料區塊數量。 伺服器會以背對背的方式傳送資料區塊，直到填滿視窗為止，然後用戶端會傳送 ACK 封包。 增加此視窗大小可降低用戶端與伺服器之間的來回延遲數，並縮短下載開機映像所需的整體時間。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

-   我可以自訂支援 PXE 之發佈點的相關 RamDisk TFTP 視窗大小。  

-   我可以自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊大小。  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>修改 RamDisk TFTP 視窗大小  

-   新增支援 PXE 之發佈點的下列相關登錄機碼以自訂 RamDisk TFTP 視窗大小：  

     **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    名稱：RamDiskTFTPWindowSize  

     **類型**：REG_DWORD  

     **值**：&lt;自訂視窗大小\>  

 預設值為 1 (1 個資料區塊填滿視窗)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>修改 RamDisk TFTP 區塊大小  

-   新增支援 PXE 之發佈點的下列相關登錄機碼以自訂 RamDisk TFTP 視窗大小：  

     **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    名稱：RamDiskTFTPBlockSize  

     **類型**：REG_DWORD  

     **值**：&lt;自訂區塊大小\>  

 預設值為 4096 (4k)。  
