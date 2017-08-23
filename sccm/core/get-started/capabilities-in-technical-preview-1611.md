---
title: "Technical Preview 1611 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1611 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5e77ebbfd3f3d573d903fe58024a22feb9884e4a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1611 中的功能

適用於︰System Center Configuration Manager (Technical Preview)



本文介紹 System Center Configuration Manager Technical Preview 1611 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    

**此 Technical Preview 的已知問題：**   
- ***必要條件狀態***︰當您安裝 1611 版時，必要條件的整體狀態可能會顯示為通過但有警告，但未列出哪些必要條件造成警告。 這可能是由以下兩個必要條件所造成：
  - SQL 索引建立記憶體選項
  - 檢查支援的 SQL Server 版本  

 由於這些只是警告，因此可予以略過。

- ***PowerShell***︰當您從 Configuration Manager 主控台連線到 Windows PowerShell 時，您可能會收到下列錯誤︰**Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml 未經過數位簽署**。  

   從 1610 版開始，您可以將特定檔案取代成已簽署的版本來解決此問題。 從 1610 版安裝中的 &lt;安裝目錄>\AdminConsole\bin**\** 資料夾複製具有下列副檔名的所有檔案︰**.psd1**、**.ps1xml** 和 **.psm1**。 將這些檔案貼到 Technical Preview 1611 安裝中的 &lt;安裝目錄>\AdminConsole\bin**\** 資料夾，並覆寫 1611 版檔案。


**以下是您可以使用此版本試用的新功能。**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>預先快取可用的部署和工作順序內容
在此 Technical Preview 中，針對可用的部署和工作順序，您可以選擇使用預先快取功能，讓用戶端在使用者安裝內容之前只下載相關內容。

例如，假設您想要部署 Windows 10 就地升級工作順序、只需要適用於所有使用者的單一工作順序，並有多個架構及 (或) 語言。 在最新分支中，如果您建立可用的部署，然後使用者在軟體中心按一下 [安裝]，此時會下載內容。 這會增加準備開始安裝之前的額外時間。 或者，在最新分支中，如果您建立可用的工作順序部署，工作順序中參考的所有內容都會下載。 這包括所有語言和架構的作業系統升級套件。 如果每個大小約 3 GB，下載套件可能會相當大。

預先快取內容功能可讓您選擇讓用戶端在收到部署時，只下載適用的內容。 因此，當使用者在軟體中心按一下 [安裝] 時，由於內容是在本機硬碟上，因此內容已就緒且安裝會快速開始。

### <a name="to-configure-the-pre-cache-feature"></a>設定預先快取功能

1. 建立特定架構和語言的作業系統升級套件。 在套件的 [資料來源] 索引標籤中指定架構和語言。 針對語言，使用十進位轉換 (例如 1033 是英文的十進位表示，而 0x0409 是十六進位的對等用法)。 如需詳細資訊，請參閱[建立工作順序以升級作業系統](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。

    架構和語言值可用來比對您將在下一個步驟中建立的工作順序步驟條件，以判斷是否應該預先快取作業系統升級套件。
2. 針對不同的語言和架構，建立具有條件式步驟的工作順序。 例如，您可以針對英文版建立類似如下的步驟：

    ![預先快取內容](media/precacheproperties2.png)

    ![預先快取選項](media/precacheoptions2.png)  

3. 部署工作順序。 針對預先快取功能，進行下列設定：
    - 在 [一般] 索引標籤上，選取 「Pre-download content for this task sequence」 (此工作順序的下載前內容)。
    - 在 [部署設定] 索引標籤上，將工作順序的 [目的] 設定為 [可用]。 如果您建立 [必要] 部署，預先快取功能將無法運作。
    - 在 [排程] 索引標籤上，針對 [排程此部署的可用時間] 設定選擇一個未來時間，讓用戶端有足夠的時間預先快取內容，再提供部署給使用者。 例如，您可以將可用時間設定為 3 小時後，以允許有足夠的時間可預先快取內容。  
    - 在 [發佈點] 索引標籤上，設定 [部署選項] 設定。 如果在使用者開始安裝之前未在用戶端預先快取內容，則會使用這些設定。


### <a name="user-experience"></a>使用者經驗
- 當用戶端收到部署原則時，就會開始預先快取內容。 這包括所有參考的內容 (任何其他套件類型)，以及根據您在工作順序中設定的條件只符合用戶端的作業系統升級套件。
- 當使用者可以使用部署時 (部署之 [排程] 索引標籤中的設定)，系統會顯示通知，告知使用者有此新的部署，並在軟體中心顯示此部署。 使用者可以前往軟體中心，然後按一下 [安裝] 開始安裝。
- 如果未完整預先快取內容，則會使用部署之 [部署選項] 索引標籤上指定的設定。 建議在建立部署到部署可供使用者使用之間有足夠的時間，讓用戶端有足夠的時間來預先快取內容。


## <a name="see-also"></a>另請參閱
[System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)
