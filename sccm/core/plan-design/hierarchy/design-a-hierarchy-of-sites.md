---
title: "設計站台階層 - Configuration Manager | Microsoft Docs"
description: "了解 System Center Configuration Manager 可用的拓撲和管理選項，以便您可以規劃站台階層。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: "22"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4710b1b89eb50cb7bcf4c4ee50c12a96b6561bc9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 設計站台階層

*適用於：System Center Configuration Manager (最新分支)*

在安裝第一個新的 System Center Configuration Manager 階層站台前，最好了解可用的 Configuration Manager 拓撲、可用的站台類型及彼此的關聯性，以及每個站台類型提供的管理範圍。
然後，在考量可減少需要安裝之站台數目的內容管理選項之後，您可以有效率地提供您目前業務需求的拓撲規劃，稍後再擴充以管理未來的成長。  

> [!NOTE]
> 在規劃新的 Configuration Manager 安裝時，請注意[版本資訊]( /sccm/core/servers/deploy/install/release-notes)，其中詳細說明使用中版本的目前問題。 此版本資訊適用於 Configuration Manager 的所有分支。  不過，當您使用 [Technical Preview 分支]( /sccm/core/get-started/technical-preview)時，會在每一版的 Technical Preview 文件中發現只有該分支才會出現的問題。  

##  <a name="bkmk_topology"></a> 階層拓樸  
 階層拓撲從單一獨立主要站台與管理中心網站之階層的頂層 (頂層) 站台連線的主要和次要站台的群組。   類型的主要驅動程式，而且階層中所使用站台的計數通常是必須支援的裝置數目及類型，如下所示：   

 **獨立的主要站台**︰當單一主要站台可以支援所有裝置和使用者的管理時，請使用獨立的主要站台 (請參閱[調整大小和縮放數字](/sccm/core/plan-design/configs/size-and-scale-numbers))。 當公司的不同地理位置可順利由單一主要站台服務時，此拓撲也會成功。  您可以使用慣用的管理點和仔細規劃的內容基礎結構，以利管理網路流量 (請參閱 [System Center Configuration Manager 的內容管理基本概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md))。  

 這種拓撲的優點包括︰  

-   簡化管理負荷。  

-   簡化用戶端站台指派及探索可用資源及服務。  

-   消除站台間資料庫複寫所引起的可能延遲。

-   透過管理中心網站將獨立主要階層展開為較大階層的選項。 這可讓您稍後安裝新的主要站台，以擴展您的部署規模。  


**有一或多個子主要站台的管理中心網站︰** 需要多個主要站台支援管理所有的裝置和使用者時，請使用此拓撲。  當您需要使用多個單一主要站台時所需。 這種拓撲的優點包括︰  


-   支援最多 25 個主要站台，讓您擴展階層的規模。  

-   除非您重新安裝您的站台，否則將一律使用管理中心網站。 這是永久選項。 您無法中斷連結子主要站台以作為獨立主要站台。

 下列各節可協助您了解何時使用特定站台或內容管理選項，來取代其他站台。  

##  <a name="BKMK_ChooseCAS"></a> 判斷何時要使用管理中心網站。  
 使用管理中心網站設定全階層設定，並監視階層中的所有網站及物件。 此站台類型不會直接管理用戶端，但會協調站台間的資料複寫，包括整個階層的站台和用戶端的設定。  

**使用下列資訊，協助您決定何時要安裝管理中心網站：**  

-   管理中心網站是階層中的頂層站台。  

-   當您設定具有一個以上主要站台的階層時，必須安裝管理中心網站。 如果您立即需要兩個或兩個以上的主要站台，請先安裝管理中心網站。 當您已經擁有主要站台，並想要接著安裝管理中心網站時，必須[擴充獨立主要站台](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand)以安裝管理中心網站。 

-   管理中心網站只支援使用主要站台作為子站台。  

-   管理中心網站自身則不能被指派任何用戶端。  

-   管理中心網站不支援直接支援用戶端的站台系統角色，例如管理點及發佈點。  

-   使用連線到管理中心網站的 Configuration Manager 主控台時，您可以管理階層中的所有用戶端，以及針對任何子站台執行站台管理工作。 這可以包括安裝管理點或在子主要或次要站台的其他站台系統角色。  

-   當您使用管理中心網站時，管理中心網站是您唯一可以在階層中查看所有站台資料的位置。 此資料包括清查資料及狀態訊息等資訊。  

-   若要從管理中心網站設定整個階層的探索作業，請指派要在個別站台執行的探索方法。  

-   若要管理整個階層的安全性，您可以指派不同的安全性角色、安全性範圍與集合給不同的系統管理使用者。 這些設定可套用到階層中的各個站台。  

-   您可以設定檔案複寫和資料庫複寫，以控制階層中各站台間的通訊。 這包括排定站台資料的資料庫複寫，以及管理站台間檔案資料傳輸的頻寬。  

##  <a name="BKMK_ChoosePriimary"></a> 判斷何時使用主要站台。  
 使用主要站台管理用戶端。 您可以安裝主要站台，作為管理中心網站底下的子主要站台，或是作為新階層的第一個站台。 安裝成階層中第一個站台的主要站台會建立獨立主要站台。 子主要站台和獨立主要站台都支援以次要站台作為主要站台的子站台。  

 針對下列任何一種理由，考慮使用主要站台：  

-   管理裝置和使用者。  

-   增加可以使用單一階層來管理的裝置數目。  

-   提供其他的連線點，以進行部署的系統管理。  

-   符合組織的管理需求。 例如，您可能會在遠端位置安裝主要站台，以管理透過低頻寬網路傳送的部署內容。 不過，透過 System Center Configuration Manager，您可以在將資料傳輸到發佈點時使用網路頻寬節流的選項。 該項內容管理功能可以取代安裝其他站台的需求。  


**使用下列資訊，協助您決定何時要安裝主要站台：**  

-   主要站台可以是獨立主要站台或是較大階層中的子主要站台。 當主要站台是含管理中心網站之階層的成員時，站台會使用資料庫複寫在站台之間複寫資料。 除非您需要支援的用戶端和裝置數目超過單一主要站台可支援的數目，否則請考慮安裝獨立主要站台。  安裝獨立主要站台之後，您可以展開它，以回報至新的管理中心網站來擴展部署的規模。  

-   主要站台僅支援使用管理中心網站作為父站台。  

-   主要站台不僅支援使用次要站台作為子站台，也支援多個次要子站台。  

-   主要站台負責處理所指派用戶端的所有用戶端資料。  

-   主要站台使用資料庫複寫，直接與其管理中心網站進行通訊 (當安裝新的站台時自動設定)。  

##  <a name="BKMK_ChooseSecondary"></a> 判斷何時使用次要站台。  
 使用次要站台管理在低頻寬網路上部署內容與用戶端資料的傳輸。  

 您可經由管理中心網站或次要站台的直接父主要站台來管理次要站台。 次要站台必須連結到主要站台，並且您無法在還未解除安裝的狀況下，將其移至不同的父站台，然後重新安裝為新主要站台下的子站台。

不過，您可以在兩個對等次要站台間路由內容，協助管理以檔案為基礎的部署內容複寫。 為將用戶端資料移轉到主要站台上，次要站台會使用以檔案為基礎的複寫。 次要站台也會使用資料庫複寫，以與其父主要站台進行通訊。  

 若套用以下任何一種狀況，請考量安裝次要站台：  

-   您不需要有針對系統管理使用者的本機連線點。  

-   您必須管理將部署內容移轉到階層中較低的站台。  

-   您必須管理傳送到階層中較高站台的用戶端資訊。  

 如果您不想安裝次要站台，又有用戶端位於遠端位置，請考慮使用 Windows BranchCache，或安裝用來進行頻寬控制與排程的發佈點。 您可以搭配或不搭配次要站台，使用這些內容管理選項，不過它們可以幫助您減少必須安裝的站台和伺服器數量。 如需 Configuration Manager 中內容管理選項的資訊，請參閱[判斷何時要使用內容管理選項](#BKMK_ChooseSecondaryorDP)。  


**使用下列資訊，協助您決定何時要安裝次要站台：**  

-   若沒有本機 SQL Server 執行個體可用，次要站台會在站台安裝期間自動安裝 SQL Server Express。  

-   安裝次要站台是從 Configuration Manager 主控台中起始，而不是直接在電腦上執行安裝程式。  

-   次要站台使用站台資料庫中資訊的子集，以減少父主要站台與次要站台間資料庫複寫所複寫的資料量。  

-   次要站台支援將以檔案為基礎的內容路由至有一般父主要站台的其他次要站台。  

-   安裝次要站台時會自動部署位於次要站台伺服器上的管理點和發佈點。  

##  <a name="BKMK_ChooseSecondaryorDP"></a> 判斷何時要使用內容管理選項。  
 如果您有用戶端位於遠端位置，請考慮使用一個或多個內容管理選項，不要使用主要或次要站台。 在您使用 Windows BRanchCache、設定頻寬控制的發佈點，或手動將內容複製到發佈點 (預先設置內容) 時，您經常可以移除安裝一個站台的需求。  


**若適用以下任一狀況，請考慮部署發佈點，而不要安裝另一個站台。**  

-   您的網路頻寬足以讓遠端位置的用戶端電腦與管理點進行通訊，以下載用戶端原則，以及傳送清查、回報狀態和探索資訊。  

-   背景智慧型傳送服務 (BITS) 並不會為您的網路需求提供足夠的頻寬控制。  

 如需 Configuration Manager 內容管理選項的詳細資訊，請參閱 [System Center Configuration Manager 中的內容管理基本概念](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

##  <a name="bkmk_beyond"></a> 階層拓撲之外  
 除了初始階層拓撲外，請考慮階層中不同站台 (站台系統角色) 提供哪些服務或功能，以及您的基礎結構如何管理階層範圍設定和功能。 下列常見考量事項涵蓋在不同的主題中。 這些可能會影響階層設計或受到階層設計所影響，因此十分重要：  

-   當準備[使用 System Center Configuration Manager 管理電腦和裝置](/sccm/core/clients/manage/manage-clients)時，請考量您管理的裝置是位於內部部署、雲端中還是包含使用者擁有的裝置 (BYOD)。  亦請考量您要如何管理受多種管理選項支援的裝置，例如可以直接由 Configuration Manager 管理或透過與 Microsoft Intune 整合的 Windows 10 電腦。  

-   了解可用的網路基礎結構可能會如何影響遠端位置間的資料流程 (請參閱[準備 System Center Configuration Manager 的網路環境](/sccm/core/plan-design/network/configure-firewalls-ports-domains))。 也要考量您管理的使用者和裝置的所在位置，以及他們透過您公司的網域還是網際網路存取您的基礎結構。  

-   規劃內容基礎結構，有效率地將所部署的資訊 (檔案和應用程式) 發佈到您管理的裝置上 (請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md))。  

-   決定打算使用哪些 [System Center Configuration Manager 的特色與功能](../../../core/plan-design/changes/features-and-capabilities.md)、需要的站台系統角色或 Windows 基礎結構，以及要部署在多個站台階層中的哪些站台才能最有效率地使用網路和伺服器資源。  

-   考量資料和裝置的安全性，包括 PKI 的使用。 請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  


**檢閱下列站台特定設定的資源︰**  

-   [規劃 System Center Configuration Manager 的 SMS 提供者](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [規劃 System Center Configuration Manager 的站台資料庫](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [為 System Center Configuration Manager 規劃站台系統伺服器和站台系統角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [在 System Center Configuration Manager 中規劃安全性](../../../core/plan-design/security/plan-for-security.md)  

-   部署站台內的內容時[Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) 。  


**請考量下列跨越站台和階層的設定：**  

-   適用於站台和階層的 [System Center Configuration Manager 高可用性選項](/sccm/protect/understand/high-availability-options)

-   [擴充 System Center Configuration Manager 的 Active Directory 架構](../../../core/plan-design/network/extend-the-active-directory-schema.md)，並設定站台來[發佈 System Center Configuration Manager 的站台資料](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [System Center Configuration Manager 中站台間的資料傳輸](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [System Center Configuration Manager 以角色為基礎之系統管理的基礎](../../../core/understand/fundamentals-of-role-based-administration.md)
