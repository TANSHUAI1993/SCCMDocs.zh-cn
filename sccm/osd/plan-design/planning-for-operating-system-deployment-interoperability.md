---
title: "規劃作業系統部署互通性 | Microsoft Docs"
description: "了解單一階層中不同 System Center Configuration Manager 站台使用不同版本時的互通性問題。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中規劃作業系統部署互通性

*適用於：System Center Configuration Manager (最新分支)*

單一階層中不同 System Center Configuration Manager 站台使用不同版本時，部分 Configuration Manager 功能會無法使用。 通常，執行舊版的站台或用戶端無法存取新版 Configuration Manager 的功能。 如需詳細資訊，請參閱 [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)。  

 當您升級階層中的頂層站台以及階層中執行舊版 Configuration Manager 的其他站台時，請考慮下列各項：  

-   用戶端安裝套件  

    -   預設用戶端安裝套件的來源會自動升級，而階層中所有發佈點會更新為新的用戶端安裝套件，即使發佈點位於舊版的階層站台也一樣。  

    -   執行新版本的用戶端無法指派至尚未升級為新版本的站台。 指派會在管理點遭到封鎖。  

-   開機映像  

    -   當頂層站台升級至最新版的 Configuration Manager 時，預設開機映像 (x86 和 x64) 會自動更新為使用 Windows PE 10 且以 Windows ADK for Windows 10 為基礎的開機映像。 與預設開機映像相關聯的檔案會隨最新版的 Configuration Manager 檔案更新。 自訂開機映像不會自動更新。 您必須手動更新包含舊版 Windows PE 的自訂開機映像。  

    -   若您的站台階層包含採用不同 Configuration Manager 版本的站台，請避免使用動態媒體。 請改用以站台為基礎的媒體來連絡特定管理點，直到所有站台升級為相同的 Configuration Manager 版本的站台。  

    -   確認最新版 Configuration Manager 開機映像是否包含所需的自訂項目，然後以最新版的 Configuration Manager 和新的開機映像更新站台中所有的發佈點。  

-   使用者狀態移轉工具 (USMT)  

    -   當頂層站台升級至最新版的 Configuration Manager 時，預設的 USMT 套件會自動更新為最新版本。 自訂的 USMT 套件不會自動更新。 您必須手動更新這些套件。  

-   新的工作順序步驟  

    -   新版的 Configuration Manager 會定期引入新的工作順序步驟。 當您依新步驟將工作順序部署到舊版的用戶端時，工作順序步驟會失敗。 請先確定目標集合中的用戶端已更新為新版本，再依新步驟部署工作順序。  

-   作業系統部署媒體  

    -   當站台更新為新版本時，所有媒體 (可開機、擷取、預先設置及獨立的) 都必須使用新的 Configuration Manager 用戶端套件來更新。  

-   作業系統部署的協力廠商擴充功能  

    -   當作業系統部署具有協力廠商延伸模組，且您有不同版本的 Configuration Manager 站台或 Configuration Manager 用戶端時，這是一個混合階層，延伸模組可能會發生問題。  

 當您主動升級階層中的站台時，請使用下列章節內容幫助您進行作業系統部署。  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>混合階層中的最新版 Configuration Manager 站台  
 當您將站台升級為最新版 Configuration Manager 時，參照預設用戶端安裝套件的工作順序會自動開始部署最新的 Configuration Manager 用戶端版本。 參照自訂用戶端安裝套件的工作順序會繼續部署該自訂套件中包含的用戶端版本 (可能是舊版的 Configuration Manager 用戶端)，而且必須升級以避免工作順序部署失敗。 若您的工作順序設定為使用自訂用戶端安裝套件，則必須將工作順序步驟更新為使用最新版 Configuration Manager 的用戶端安裝套件，或將自訂套件更新為使用最新的 Configuration Manager 用戶端安裝來源。  

> [!IMPORTANT]  
>  請勿將參照最新 Configuration Manager 用戶端安裝套件的工作順序，部署到舊版 Configuration Manager 站台的用戶端。 當指派給舊版 Configuration Manager 站台的用戶端升級為最新的 Configuration Manager 用戶端版本時，Configuration Manager 會封鎖舊版 Configuration Manager 站台的用戶端。 因此，用戶端將不再指派給任何站台，並且維持未受管理狀態，直到您手動將用戶端指派給最新的 Configuration Manager 站台，或在電腦上再次安裝舊版的 Configuration Manager 用戶端。  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>混合階層中的舊版 Configuration Manager  
 當管理中心網站升級為最新版 Configuration Manager 之後，您必須執行下列步驟，以確保部署到指派給舊版 Configuration Manager 站台 (尚未升級為最新版的 Configuration Manager) 之用戶端的作業系統部署工作順序，不會讓用戶端處於未受管理狀態。  

-   只在 Configuration Manager 站台中建立用來部署至用戶端的工作順序。 同樣地，您要建立一份工作順序，用來部署至最新版 Configuration Manager 站台的用戶端，然後修改此工作順序，以便將它部署至舊版 Configuration Manager 站台的用戶端。 接著設定工作順序參照使用舊版 Configuration Manager 用戶端安裝來源的自訂用戶端安裝套件。 如果沒有參照舊版 Configuration Manager 用戶端安裝來源的自訂用戶端安裝套件，則必須手動建立一份。  
