---
title: "使用 System Center Configuration Manager 建立工作順序媒體 | Microsoft Docs"
description: "建立工作順序媒體 (例如 CD)，以將作業系統部署至 Configuration Manager 環境中的目的地電腦。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: bd5448d70c2d465347de840cb197d4c33075c90a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立工作順序媒體

*適用於︰System Center Configuration Manager (最新分支)*

您可以使用媒體從參照電腦擷取作業系統映像，也可以將作業系統部署至 System Center Configuration Manager 環境中的目的地電腦。 您所建立的媒體可以是 CD、DVD 組或 USB 快閃磁碟機。  

 如果目的地電腦沒有網路連線或與 Configuration Manager 站台的連線頻寬不足，則大部分會使用媒體在其上部署作業系統。 不過，部署媒體亦可用於啟動現有 Windows 作業系統以外的作業系統部署。 在目的地電腦上沒有作業系統、作業系統處於無法運作狀態，或者系統管理使用者想要重新分割目的地電腦上的硬碟等情況下，二次使用部署媒體就顯得非常重要。  

 部署媒體包括可開機媒體、獨立媒體，以及預先設置的媒體。 部署媒體的內容會依所使用的媒體類型而有所不同。 例如，獨立媒體包含部署作業系統的工作順序，而其他類型的媒體則會從管理點擷取工作順序。  

> [!IMPORTANT]  
>  若要建立工作順序媒體，您必須為執行 Configuration Manager 主控台之電腦上的系統管理員。 如果您不是系統管理員，當您啟動「建立工作順序媒體」精靈時，系統將會提示您輸入系統管理員認證。  

##  <a name="BKMK_PlanCaptureMedia"></a> 作業系統映像的擷取媒體  
 擷取媒體可用於從參照電腦擷取作業系統映像。 擷取媒體包含啟動參照電腦的開機映像，以及擷取作業系統映像的工作順序。 如需如何建立擷取媒體的資訊，請參閱[使用 System Center Configuration Manager 建立擷取媒體](create-capture-media.md)。  

##  <a name="BKMK_PlanBootableMedia"></a> 可開機媒體作業系統部署  
 可開機媒體只包含開機映像、選擇性的[啟動前置命令](../understand/prestart-commands-for-task-sequence-media.md) 和其必要檔案，以及 Configuration Manager 二進位檔。 目的地電腦啟動時會連線至網路，並從網路擷取工作順序、作業系統映像，以及任何其他必要的內容。 由於工作順序不在媒體上，因此不需要重新建立媒體即可變更工作順序或內容。  

> [!IMPORTANT]  
>  可開機媒體上的套件並未加密。 系統管理使用者必須採取適當的安全防護措施 (例如新增媒體密碼)，以確保未經授權的使用者無法存取套件內容。  

 如需如何建立可開機媒體的相關資訊，請參閱[建立可開機媒體](create-bootable-media.md)。  

##  <a name="BKMK_PlanPrestagedMedia"></a> 預先設置的媒體作業系統部署  
 預先設置的媒體可用於在佈建程序之前，將可開機媒體及作業系統映像預先設置到硬碟上。 預先設置的媒體是 Windows 映像格式 (WIM) 檔案，可由廠商或在企業設置中心安裝於未連線 Configuration Manager 環境的裸機電腦。  

 預先設置的媒體包含用於啟動目的地電腦的開機映像，以及將套用於目的地電腦的作業系統映像。 您也可以指定在預先設置的媒體中加入應用程式、套件及驅動程式套件。 媒體中不包含部署作業系統的工作順序。 部署使用預先設置媒體的工作順序時，用戶端會先檢查本機工作順序快取中的有效內容，如果找不到有效內容，或者內容已經過修改，則用戶端會從發佈點下載內容。  

 將電腦交給使用者之前，即需將預先設置的媒體套用至新電腦的硬碟中。 在電腦套用預先設置的媒體後第一次啟動前，電腦會啟動 Windows PE 並連線至管理點，尋找能完成作業系統部署程序的工作順序。  

> [!IMPORTANT]  
>  預先設置媒體上的套件並未加密。 系統管理使用者必須採取適當的安全防護措施 (例如新增媒體密碼)，以確保未經授權的使用者無法存取套件內容。  

 如需如何建立預先設置媒體的相關資訊，請參閱[建立預先設置媒體](create-prestaged-media.md)。  

##  <a name="BKMK_PlanStandaloneMedia"></a> 獨立媒體作業系統部署  
 獨立媒體包含部署作業系統所需的完整內容， 其中包括工作順序和任何其他必要內容。 由於部署作業系統所需的全部內容都儲存在獨立媒體中，因此獨立媒體比其他類型的媒體需要更大的磁碟空間。  

 如需如何建立獨立媒體的相關資訊，請參閱[建立獨立媒體](create-stand-alone-media.md)。  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>使用替 HTTPS 所設定的網站系統時的媒體考量  
 將管理點和發佈點設定為使用 HTTPS 通訊時，必須在主要網站而非管理中心網站建立開機媒體和預先設置的媒體。 此外，判斷要設定動態媒體或以網站為基礎的媒體時，請考量下列幾點：  

-   要將媒體設定為動態媒體，所有主要網站都必須要有用於建立媒體之網站的根 CA。 您可以將根 CA 匯入至階層中的所有主要網站。  

-   若 Configuration Manager 階層中的主要站台使用不同的根 CA，您必須在每個站台上使用以站台為基礎的媒體。  
