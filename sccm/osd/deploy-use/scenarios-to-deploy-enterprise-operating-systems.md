---
title: "部署企業作業系統的案例 | Microsoft Docs"
description: "了解使用 System Center Configuration Manager 部署企業作業系統的多種案例。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
caps.latest.revision: "11"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b1bea8b1b890f7c96a432835d28ad840a9b6873d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 部署企業作業系統的案例

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 提供下列作業系統部署案例：  

-   [升級至最新版本的 Windows](upgrade-windows-to-the-latest-version.md)：這個案例會升級目前執行 Windows 7、Windows 8、Windows 8.1 或 Windows 10 電腦的作業系統。 升級程序會保留電腦上的應用程式、設定和使用者資料。 因為沒有外部相依性 (如 Windows ADK)，所以這個程序比傳統的作業系統部署更快、更有彈性。  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)：這個案例會分割及格式化 (抹除) 現有的電腦，並在其上安裝新的作業系統。 您可以在安裝作業系統之後，移轉設定和使用者資料。  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)：這個案例會在新電腦上安裝作業系統。 這是全新的作業系統安裝，不包含任何設定或使用者資料移轉。  

-   [取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)：這個案例會在新電腦上安裝作業系統。 您也可以將舊電腦的設定和使用者資料移轉至新電腦。  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>在部署作業系統映像之前的考慮事項  
 有某些項目，您應該在部署作業系統之前先加以考慮。  

### <a name="operating-system-image-size"></a>作業系統映像大小  
 作業系統映像可能非常大。 例如，Windows 7 的映像大小為 3 GB 以上。 同時部署作業系統的映像大小和電腦數目，會影響網路效能和可用頻寬。 確定您會測試網路效能以進一步評估映像部署可能造成的影響，以及完成部署所需的時間。 下列為會對網路效能造成影響的 Configuration Manager 活動：將映像發佈到發佈點、將映像從某個站台發佈到另一個站台，以及將映像下載到 Configuration Manager 用戶端。  

 同時，請確定您已在裝載作業系統映像之發佈點上，規劃足夠的磁碟儲存空間。  

### <a name="client-cache-size"></a>用戶端快取大小  
 當 Configuration Manager 用戶端下載內容時，它們會自動使用背景智慧型傳送服務 (BITS) (如果可用)。 當您部署安裝作業系統的工作順序時，可以在部署時設定一個選項，使 Configuration Manager 用戶端先將完整的映像下載至本機快取，再執行工作順序。  

 一般情況下，當 Configuration Manager 用戶端必須下載作業系統映像 (或任何其他套件)，但快取中沒有足夠空間時，用戶端會檢查其他快取中的套件，以判斷刪除任一或所有最舊套件是否會釋放足夠的磁碟空間來容納映像。 如果刪除封裝後仍沒有足夠的可用磁碟空間，則用戶端不會下載映像，部署也會失敗。 如果快取具有已設定為必須保存在快取中的大型封裝，則會發生此情況。 如果刪除封裝可以在快取中釋放足夠的可用磁碟空間，用戶端便會刪除這些封裝，然後下載映像至快取。  

 Configuration Manager 用戶端上的預設快取大小，可能不足以容納大部分的作業系統映像部署。 如果您想要將完整映像下載至用戶端快取，您必須調整目的地電腦上的 Configuration Manager 用戶端快取大小，以容納您要部署的映像大小。  

 如需詳細資訊，請參閱 [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)。  

## <a name="task-sequence-deployments"></a>工作順序部署  
 您建立的工作順序可以透過下列其中一種方式，將作業系統映像部署至 Configuration Manager 用戶端電腦：  

-   先將映像及其內容從發佈點下載至 Configuration Manager 用戶端快取，然後再進行安裝。  

-   立即從發佈點安裝映像及其內容。  

-   視需要從發佈點安裝映像及其內容  

 根據預設，當您建立工作順序的部署時，會先將映像下載至 Configuration Manager 用戶端快取，然後再進行安裝。 如果您選擇在執行映像前將映像下載至 Configuration Manager 用戶端快取，且工作順序包含重新分割硬碟的步驟，則重新分割步驟會失敗，因為分割硬碟時會清除 Configuration Manager 用戶端快取的內容。 如果工作順序必須重新分割硬碟，您必須在部署工作順序時使用 [從發佈點執行程式]   選項，以從發佈點執行映像安裝。  

 如需詳細資訊，請參閱 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  
