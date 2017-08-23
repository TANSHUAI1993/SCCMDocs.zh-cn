---
title: "語言套件 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中可用的語言支援。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 47da3c531289ddf13d357bde8bbda85d79ed2803
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="language-packs-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的語言套件

*適用於：System Center Configuration Manager (最新分支)*

本主題提供 System Center Configuration Manager 的語言支援技術詳細資料。  

## <a name="BKMK_SupLanguagePacks"></a> 支援的作業系統語言  
 在管理中心網站和主要站台安裝**伺服器語言套件**或**用戶端語言套件**，即可安裝下列各表中顯示語言的支援。 在站台安裝程序期間，您可以從可用的語言套件檔案中選取要在該站台支援的伺服器和用戶端語言。

 當您執行安裝程式時，語言套件檔案會作為必要條件和可轉散發檔案下載的一部分下載。 您也可以先使用[安裝程式下載程式](setup-downloader.md)下載這些檔案，然後再執行安裝程式。   

 請使用下表對應地區設定識別碼與要在伺服器或用戶端電腦上支援的語言。 如需地區設定識別碼的詳細資訊，請參閱 [Microsoft 指派的地區設定識別碼](http://go.microsoft.com/fwlink/p/?LinkId=252609)。  

### <a name="server-languages"></a>伺服器語言  

|伺服器語言|地區設定識別碼 (LCID)|三個字母的代碼|  
|---------------------|------------------------|-----------------------|  
|英文 (預設值)|0409|ENU|  
|中文 (繁體，香港特別行政區)|0c04|ZHH|  
|中文 (簡體)|0804|CHS|  
|中文 (繁體，台灣)|0404|CHT|  
|捷克文|0405|CSY|  
|荷蘭文 - 荷蘭|0413|NLD|  
|法文|040c|FRA|  
|德文|0407|DEU|  
|匈牙利文|040e|HUN|  
|義大利文 - 義大利|0410|ITA|  
|日文|0411|JPN|  
|韓文|0412|KOR|  
|波蘭文|0415|PLK|  
|葡萄牙文 - 巴西|0416|PTB|  
|葡萄牙文 - 葡萄牙|0816|PTG|  
|俄文|0419|RUS|  
|西班牙文 - 西班牙|0c0a|ESN|  
|瑞典文|041d|SVE|  
|土耳其文|041f|TRK|  

### <a name="client-languages"></a>用戶端語言  

|用戶端語言|地區設定識別碼 (LCID)|三個字母的代碼|  
|---------------------|------------------------|-----------------------|  
|英文 (預設值)|0409|ENG|  
|中文 (繁體，香港特別行政區)|0c04|ZHH|  
|中文 - 簡體|0804|CHS|  
|中文 (繁體，台灣)|0404|CHT|  
|捷克文|0405|CSY|  
|丹麥文|0406|DAN|  
|荷蘭文 - 荷蘭|0413|NLD|  
|芬蘭文|040b|FIN|  
|法文|040c|FRA|  
|德文|0407|DEU|  
|希臘文|0408|ELL|  
|匈牙利文|040e|HUN|  
|義大利文 - 義大利|0410|ITA|  
|日文|0411|JPN|  
|韓文|0412|KOR|  
|挪威文|0414|NOR|  
|波蘭文|0415|PLK|  
|葡萄牙文 (巴西)|0416|PTB|  
|葡萄牙文 (葡萄牙)|0816|PTG|  
|俄文|0419|RUS|  
|西班牙文 - 西班牙|0c0a|ESN|  
|瑞典文|041d|SVE|  
|土耳其文|041f|TRK|  

### <a name="mobile-device-client-languages"></a>行動裝置用戶端語言  
 新增行動裝置語言支援時，所有支援的行動裝置用戶端語言皆包含在內。 您不能選取行動裝置支援的個別語言套件。  

### <a name="identify-installed-language-packs"></a>識別已安裝的語言套件  
若要識別 Configuration Manager 用戶端執行電腦所安裝的語言套件，請在電腦登錄中尋找已安裝語言套件的地區設定識別碼 (LCID)。 在下列位置可取得這項詳細資訊：

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

您可以使用硬體清查收集這項資訊，然後再建立用於檢視語言詳細資料的自訂報告。 如需收集自訂硬體清查的資訊，請參閱[如何在 System Center Configuration Manager 中設定硬體清查](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)。 如需建立報告的相關資訊，請參閱 [System Center Configuration Manager 中的報告作業和維護](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md)主題中的[管理 Configuration Manager 報告](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports)一節。  
