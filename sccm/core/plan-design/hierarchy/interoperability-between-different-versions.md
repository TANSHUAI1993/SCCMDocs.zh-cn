---
title: "Configuration Manager 版本之間的互通性 | Microsoft Docs"
description: "了解如何避免相同網路中多個 System Center Configuration Manager 階層之間產生衝突。"
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 28593d271603ff9775425327996d844d7ed358cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>System Center Configuration Manager 不同版本之間的互通性

*適用於︰System Center Configuration Manager (最新分支)*

您可在相同網路上安裝及操作多個獨立的 System Center Configuration Manager 階層。 不過，由於不同的 Configuration Manager 階層無法在移轉程序外互通，因此每個階層的設定都需要避免彼此之間發生衝突。 此外，您可以建立特定設定，幫助所管理的資源與正確階層的站台系統互動。  

 下面各節提供在相同網路上使用不同版本 Configuration Manager 的相關資訊：  

-   [System Center Configuration Manager 與產品舊版本之間的互通性](#BKMK_SupConfigInterop)  

-   [Configuration Manager 主控台的互通性](#BKMK_ConsoleInterop)  

-   [混合版本階層中的 Configuration Manager 限制](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> System Center Configuration Manager 與產品舊版本之間的互通性  
 除了從 System Center 2012 Configuration Manager 升級至 System Center Configuration Manager 或從某個 System Center Configuration Manager 版本升級至較新版本 (使用主控台內更新) 的升級程序期間以外，不同版本的站台不能共存於相同階層中。   

 因為您可以部署與現有 System Center 2012 Configuration Manager 站台或階層並存的 System Center Configuration Manager 站台，建議您規劃好以避免任一版本的用戶端嘗試加入另一個版本的站台。

例如，如果兩個或更多個 Configuration Manager 階層有包含相同網路位置的重疊界限 (請參閱[重疊的界限](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries))，則最佳做法是將每個新的用戶端指派給特定站台，而不使用自動站台指派。 如需了解 System Center 2012 Configuration Manager 中自動站台指派的資訊，請參閱[如何將用戶端指派給 System Center Configuration Manager 中的站台](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

 此外，若電腦上裝載來自 System Center Configuration Manager 的站台系統角色，您不能在其上透過 System Center 2012 Configuration Manager 來安裝用戶端；若電腦上裝載來自 System Center 2012 Configuration Manager 的站台系統角色，也不能在其上安裝 System Center Configuration Manager 用戶端。  

 同樣地，不支援下列用戶端和下列虛擬私人網路 (VPN) 連線：  

-   任何 System Center 2012 Configuration Manager 或更早的電腦用戶端版本  

-   任何 System Center 2012 Configuration Manager 或更早的裝置管理用戶端  

-   Windows CE Platform Builder 裝置管理用戶端 (任何版本)  

-   System Center Mobile Device Manager VPN 連線  

###  <a name="BKMK_SupConfigSiteAssignment"></a> 用戶端站台指派考量  
 System Center Configuration Manager 用戶端只能指派給單一主要站台。 在用戶端安裝期間使用自動網站指派將用戶端指派至網站時，若有多個界限群組包含相同的界限，而且界限群組擁有不同的指派的站台，就無法預測實際的用戶端網站指派。  

 如果界限跨多個 Configuration Manager 站台和階層重疊，用戶端可能會指派給非預期的站台，也可能根本不會指派給任何站台。  

 System Center Configuration Manager 用戶端會在完成站台指派之前檢查 Configuration Manager 站台的版本；如果界限重疊，則無法指派給舊版本。 不過，System Center 2012 Configuration Manager 用戶端指派給 System Center Configuration Manager 站台時也可能會有不正確的情況。  

 為避免在兩個階層的界限重疊時不小心將用戶端指派給錯誤的站台，建議您將 Configuration Manager 用戶端安裝參數設為將用戶端指派給特定站台。  

##  <a name="bkmk_mixed"></a> 混合版本階層中的 Configuration Manager 限制  
 有時，升級 System Center Configuration Manager 站台時，不同的站台會有不同的版本。 例如，您可能將管理中心網站升級至新的版本，但因站台維護期間，可能之後才會升級一個或多個主要站台。  

 單一階層中不同的站台執行不同的版本時，部分功能無法使用。 這可能會影響您在 Configuration Manager 主控台中管理 Configuration Manager 物件的方式，以及對用戶端提供的功能。 通常，如果站台或用戶端是執行較舊 Service Pack 版本，可能就無法存取較新版 Configuration Manager 的功能。  

### <a name="limitations-when-upgrading--configuration-manager"></a>升級 Configuration Manager 時的限制  

|物件|詳細資料|  
|------------|-------------|  
|網路存取帳戶|**從 System Center 2012 Configuration Manager 升級至 System Center Configuration Manager 時：**當您從連線至已更新為 System Center Configuration Manager 管理中心網站的 Configuration Manager 主控台，檢視網路存取帳戶詳細資料時，如果主要站台是執行 System Center 2012 Configuration Manager 而這些帳戶在該站台中設定，則主控台不會顯示該帳戶的詳細資料。 主要站台升級至與管理中心網站相同的版本之後，主控台中就可以看到帳戶詳細資料。<br /><br /> **在 System Center Configuration Manager 版本間進行升級時：**當您從連線至已更新為新版 System Center Configuration Manager 管理中心網站的 Configuration Manager 主控台，檢視網路存取帳戶詳細資料時，如果主要站台是執行舊版本而帳戶在該站台中設定，則主控台不會顯示這些帳戶的詳細資料。 主要站台升級至與管理中心網站相同的版本之後，主控台中就可以看到帳戶詳細資料。|  
|作業系統部署的開機映像|**從 System Center 2012 Configuration Manager 升級至 System Center Configuration Manager 時：**當階層的頂層站台升級為 System Center Configuration Manager 時，預設開機映像會自動更新為以 Windows 評定及部署套件 10 (Windows ADK) 為基礎的開機映像。 只有在部署至 System Center Configuration Manager 站台上的用戶端時，才使用這些開機映像。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃作業系統部署互通性](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)。<br /><br /> **在 System Center Configuration Manager 版本間進行升級時：**只要 cm6long 的新版本未更新使用中的 Windows ADK 版本，就不會影響開機映像。|  
|新的工作順序步驟|如果您建立的工作順序使用了舊版未提供但某個 Configuration Manager 版本引進的步驟，可能會遇到下列問題：<br /><br /> -- 當您嘗試從執行舊版 Configuration Manager 的站台編輯工作順序時，發生錯誤。<br /><br /> -- 工作順序在執行舊版 Configuration Manager 用戶端的電腦上不執行。|  
|用戶端對舊版管理點通訊|如果 Configuration Manager 用戶端是透過比用戶端更舊版本的站台來與管理點進行通訊 ，則只能使用舊版 Configuration Manager 支援的功能。 例如，如果您最近升級了 System Center Configuration Manager 站台，並從該站台將內容部署至用戶端，假設此用戶端與尚未升級為該版本的管理點進行通訊，該用戶端就無法使用最新版本的新功能。|  

##  <a name="BKMK_ConsoleInterop"></a> Configuration Manager 主控台的互通性  
 下表提供在混用不同 Configuration Manager 版本的環境中使用 Configuration Manager 主控台的相關資訊。  

|互通性環境|詳細資訊|  
|----------------------------------|----------------------|  
|使用 System Center 2012 Configuration Manager 和 System Center Configuration Manager 的環境|若要管理 Configuration Manager 站台，主控台和主控台連接的站台兩者必須執行相同版本的 Configuration Manager。 例如，您無法使用 System Center 2012 Configuration Manager 主控台來管理 System Center Configuration Manager 站台，反之亦然。<br /><br /> 此外，在同一部電腦上不能安裝 System Center 2012 Configuration Manager 主控台和 System Center Configuration Manager 主控台。|  
|安裝多重 System Center Configuration Manager 版本的環境|System Center Configuration Manager 只支援在電腦上安裝單一 Configuration Manager 主控台。 若要使用不同 System Center Configuration Manager 版本專用的主控台，您必須在不同的電腦上安裝不同的主控台。<br /><br /> 將階層中的站台更新為新版本時，您可以將主控台連線至執行新版本的站台，並檢視該階層中其他站台的資訊。 不過，我們不建議您使用這種設定，因為主控台版本與 Configuration Manager 站台版本之間的差異可能會導致資料問題，而且最新產品版本中所提供的某些功能將無法在主控台中使用。 <br /></br /> 使用版本與站台版本不符的主控台時，無法管理站台。 這樣做可能會造成資料遺失，也可能讓您的站台面臨風險。 舉例來說，使用 1610 版的主控台無法管理執行 1606 版的站台。 |
