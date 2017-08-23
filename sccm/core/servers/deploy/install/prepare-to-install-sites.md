---
title: "準備安裝站台 | Microsoft Docs"
description: "如果您打算安裝多個 Configuration Manager 站台，閱讀這些資訊有助您節省時間，並避免錯誤。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 829f2d44a9b8d203a5b753ebb6d8f759b1a05111
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>準備安裝 System Center Configuration Manager 站台

*適用於：System Center Configuration Manager (最新分支)*

若要準備一或多個 System Center Configuration Manager 站台的成功部署，請熟悉本文中的詳細資訊。 這些步驟可以節省安裝多個站台期間的時間，並協助防止可能會導致需要重新安裝一或多個站台的錯誤步驟。

> [!TIP]
> 管理 System Center Configuration Manager 站台及階層基礎結構時，「升級」、「更新」及「安裝」等詞彙是用來描述三種不同的概念。 若要了解如何使用每個詞彙，請參閱[關於升級、更新和安裝](/sccm/core/understand/upgrade-update-install)。

## <a name="bkmk_options"></a> 安裝不同類型站台的選項
當您安裝新的 Configuration Manager 站台時，可使用的來源檔案版本取決於已在階層中的站台版本 (如果有的話) 而定， 適用的安裝方法則取決於您想要安裝的站台類型而定。  

安裝站台之前，請確定您已規劃階層，並了解您要安裝的站台類型。 如需詳細資訊，請參閱[設計站台階層](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。


### <a name="first-site"></a>第一個站台
您要為階層安裝的第一個站台，是獨立主要站台或管理中心網站。

**安裝媒體**：若要將管理中心網站或獨立主要站台安裝為新階層中的第一個站台，您必須[使用 Configuration Manager 的基準版本](../../../../core/servers/manage/updates.md#bkmk_Baselines)。 請不要使用來自任何站台之 [CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)的已更新來源檔案，來安裝新階層的第一個站台。

**安裝方法**︰您可以使用 [Configuration Manager 安裝精靈](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)來安裝任一種類型的站台，也可以設定指令碼以與[指令式命令列安裝](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md)搭配使用。


### <a name="additional-sites"></a>其他站台
安裝初始站台之後，即可隨時新增更多站台。 您可以使用下列選項來新增站台 (以[支援的限制](../../../../core/plan-design/configs/size-and-scale-numbers.md)為上限)：

|您擁有的站台|您可安裝的其他站台類型|
|---|---|
|管理中心網站|子主要站台|
|子主要站台|次要網站|
|獨立主要網站|次要站台 (您可展開主要站台，將獨立主要站台轉換至子主要站台)|

**安裝媒體**：如果您安裝管理中心網站以在獨立主要站台上進行擴充，或在現有階層中安裝新的子主要站台，則必須使用符合現有一或多個站台版本的安裝媒體 (其中包含原始程式檔)。

> [!IMPORTANT]
> 如果您所安裝的主控台內更新已變更先前安裝站台的版本，請不要使用原始安裝媒體， 而是改成使用更新站台之 [CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)中的來源檔案。 Configuration Manager 要求您使用的來源檔案，必須符合新站台所要連接的現有站台版本。

您必須透過 Configuration Manager 主控台來安裝次要站台。 如此一來，系統一律會使用父主要站台的來源檔案來安裝次要站台。

**安裝方法**：您用來安裝其他站台的方式取決於所要安裝的站台類型而定。
-   **新增管理中心網站**：您可以使用 [Configuration Manager 安裝精靈] 或指令碼命令列，以將新的管理中心網站當成父站台安裝至現有的獨立主要站台。 如需詳細資訊，請參閱[擴充獨立主要站台](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)。
-   **新增子主要站台**：您可以使用 [Configuration Manager 安裝精靈] 或命令列安裝，以將子主要站台新增至管理中心網站下方。
-   **新增次要站台**：您可以使用 Configuration Manager 主控台，以將次要站台當成子站台安裝至主要站台下方。 系統僅支援這種新增次要站台的方法。

## <a name="bkmk_tasks"></a> 要在開始安裝之前完成的一般工作
-   **了解將要用於部署的階層拓撲**    
如需詳細資訊，請參閱[為 System Center Configuration Manager 設計站台階層](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)。  

-   **準備並設定個別伺服器，以符合與 Configuration Manager 搭配使用的必要條件和支援的設定**         
如需詳細資訊，請參閱 [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (站台和站台系統必要條件)。  

-   **安裝和設定 SQL Server 以裝載站台資料庫**     
如需詳細資訊，請參閱 [System Center Configuration Manager 的 SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

-   **準備支援 Configuration Manager 的網路環境**      
如需詳細資訊，請參閱[為 System Center Configuration Manager 設定防火牆、連接埠和網域](../../../../core/plan-design/network/configure-firewalls-ports-domains.md)。  

- **如果您要使用公開金鑰基礎結構 (PKI)，請備妥基礎結構和憑證。**      
如需詳細資訊，請參閱 [Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。

-   **在要當成站台伺服器或站台系統伺服器使用的電腦上安裝最新安全性更新，並在必要時重新啟動電腦。**

## <a name="bkmk_sitecodes"></a>  關於站台名稱及站台碼
站台碼和站台名稱是用來識別和管理 Configuration Manager 階層中的站台。 在 Configuration Manager 主控台中，站台碼和站台名稱的顯示格式為 &lt;站台碼\> - &lt;站台名稱\>。 階層中所使用的每個站台碼都必須是唯一的。 如果針對 Configuration Manager 擴充 Active Directory 架構時，站台正在發行資料，則 Active Directory 樹系中所使用的站台碼必須為唯一代碼 (即使站台碼用於不同的 Configuration Manager 階層中，或站台碼已經用於稍早的 Configuration Manager 安裝亦同)。 請務必仔細規劃您的站台碼和站台名稱以部署階層。

### <a name="specify-a-site-code-and-site-name"></a>指定站台碼和站台名稱
在執行 Configuration Manager 安裝程式期間，系統會提示您輸入管理中心網站、每個主要和次要站台的站台碼和站台名稱以進行安裝。 站台碼必須可唯一識別階層中的每個站台。 由於站台碼會用於資料夾名稱中，因此使用站台碼名稱時，請不要包含下列 Configuration Manager 保留名稱和 Windows 保留名稱：
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuration Manager 安裝程式不會驗證站台碼是否為使用中。

若要在 Configuration Manager 安裝程式執行時，輸入站台的站台碼，您必須輸入三位英數字元。 站台碼僅可使用字母 *A* 到 *Z* 和數字 *0* 到 *9* 的任何組合。 字母或數字的順序不會影響網站間的通訊。 例如，您不需要將主要站台命名為 *ABC*，並將次要站台命名為 *DEF*。

網站名稱是此網站的易記名稱識別項。 您僅可在站台名稱中使用字元 *A* 到 *Z*，*a* 到 *z*，*0* 到 *9* 以及連字號 (*-*)。

> [!IMPORTANT]
> 系統不支援在安裝站台之後變更站台碼或站台名稱。

### <a name="reuse-a-site-code"></a>重複使用站台碼
您不可以在管理中心網站或主要站台中的 Configuration Manager 階層中重複使用站台碼，即使您已經解除安裝原始站台和站台碼亦同。 如果您重複使用站台碼，階層中就會有物件識別碼衝突的風險。 如果 Configuration Manager 階層或 Active Directory 樹系內不再使用次要站台和其站台碼，您可以重複使用該次要站台的站台碼。

## <a name="limits-and-restrictions-for-installed-sites"></a>已安裝站台的限制
安裝站台之前，請務必了解下列站台和站台階層適用的限制︰
-   執行安裝程式之後，若要變更下列站台內容，您必須解除安裝站台，然後使用新的值重新安裝：  
  -   程式檔安裝目錄  
  -   站台碼  
  -   站台描述  
-   當階層包含管理中心網站時：  
  -   Configuration Manager 不支援將子主要站台移出階層來建立獨立主要站台，或將它附加至不同的階層。 相反地，請先解除安裝子主要站台，然後將其重新安裝為新的獨立主要站台，或不同階層之管理中心網站的子站台。  


## <a name="bkmk_optionalsteps"></a>  執行安裝程式前的選擇性步驟
**手動執行[安裝程式下載程式](../../../../core/servers/deploy/install/setup-downloader.md)**

若要下載 Configuration Manager 的更新版安裝檔案，您可以手動執行安裝程式下載程式。 如果執行安裝程式的電腦未連線到網際網路，或您預計要安裝多部站台伺服器時，請考慮使用安裝程式下載程式，以下載安裝程式的必要更新。 下列為其他資訊：
-  安裝程式預設會連線至網際網路，以下載更新版安裝檔案。
-  這些檔案預設會儲存在 Redist 資料夾中。
-  您可以將安裝程式指向您先前儲存這些檔案複本的網路位置。

**手動執行[必要條件檢查工具](../../../../core/servers/deploy/install/prerequisite-checker.md)**

在執行安裝程式並安裝站台之前，以及在伺服器上安裝站台系統角色之前，您可以執行必要條件檢查工具，以找出並修正問題。 必要條件檢查工具有助於確保電腦符合裝載站台或站台系統角色的需求。 下列為其他資訊：
 -  安裝程式預設會執行必要條件檢查工具。
 -  如果發生任何錯誤，即會停止安裝程式，直到解決問題為止。

**識別選擇性連接埠**

您可以識別用於站台系統與用戶端的選擇性連接埠。 下列為其他資訊：
 -  站台系統和用戶端預設會使用預先定義的連接埠進行通訊。
 -  在安裝期間，您可以設定替代連接埠。

 如需詳細資訊，請參閱 [System Center Configuration Manager 中使用的連接埠](../../../../core/plan-design/hierarchy/ports.md)。
