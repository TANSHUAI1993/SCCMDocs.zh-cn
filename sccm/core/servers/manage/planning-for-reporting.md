---
title: "規劃報告 | Microsoft Docs"
description: "從安裝詳細資料到安全性和網路頻寬，請務必規劃 Configuration Manager 中的報告。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 119f501057bf44e483be31db20b88326b3d05ebb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的報告規劃

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的報告提供一組工具和資源，可協助您使用 SQL Server Reporting Services 的進階報告功能。 下列各節可協助您規劃 Configuration Manager 中的報告功能。  

##  <a name="BKMK_InstallReportingServicesPoint"></a> 判斷 Reporting Services 點的安裝位置  
 當您在站台中執行 Configuration Manager 報告時，報告即可存取連線站台資料庫中的資訊。 下列章節可協助您判斷 Reporting Services 點的安裝位置，以及應使用的資料來源。  

> [!NOTE]  
>  如需在 Configuration Manager 中規劃站台系統的詳細資訊，請參閱[新增站台系統角色](../deploy/configure/add-site-system-roles.md)。  

###  <a name="BKMK_SupportedSiteServers"></a> 支援的站台系統伺服器  
 您可以將 Reporting Services 點安裝在管理中心網站和主要網站上，也可以安裝在站台中的多個站台系統，以及階層中的其他站台上。 次要站台不支援 Reporting Services 點。 站台中的第一個 Reporting Services 點會設定為預設的報告伺服器。 您可以在站台中新增多個 Reporting Services 點，但 Configuration Manager 報告會主動使用每個站台的預設 Reporting Services 點。 您可以將 Reporting Services 點安裝在站台伺服器或遠端站台系統上。 不過，最佳作法是在遠端站台系統伺服器上使用 Reporting Services。  

###  <a name="BKMK_DataReplication"></a> 資料複寫的考量  
 Configuration Manager 會將複寫資料分類為全域資料或站台資料。 全域資料是指系統管理員使用者所建立並複寫至階層中所有站台的物件，但次要站台只能接收全域資料子集。 全域資料的範例包括軟體部署、軟體更新、集合，以及以角色為基礎的系統管理安全性範圍。 站台資料是指 Configuration Manager 主要站台和用戶端回報至主要站台時建立的作業資訊。 網站資料會複寫到管理中心網站，但不會複寫到其他主要網站。 網站資料範例包括硬體清查資料、狀態訊息、警示，以及以查詢為基礎之集合的結果。 站台資料只會出現在管理中心站台，以及產生資料的主要站台。  

 考量下列因素可以協助您決定 Reporting Services 點的安裝位置：  

-   以管理中心網站資料庫為報告資料來源的 Reporting Services 點，可以存取 Configuration Manager 階層中的所有全域資料和站台資料。 如果您所需要的報告必須包含階層中多個站台的站台資料，請考慮將 Reporting Services 點安裝在管理中心網站中的站台系統上，並且以管理中心網站的資料庫為報告資料來源。  

-   以主要站台資料庫為報告資料來源的 Reporting Services 點只能存取本機主要站台和任何子次要站台的全域資料和站台資料。 Configuration Manager 階層中其他主要站台的站台資料不會複寫至主要站台，因此 Reporting Services 無法存取該資料。 如果您需要的報告必須包含特定主要站台的站台資料，或是全域資料，但您不希望報告使用者存取其他主要站台的站台資料，請將 Reporting Services 點安裝在主要站台的站台系統中，並且以主要站台的資料庫為報告資料來源。  

###  <a name="BKMK_NetworkBandwidth"></a> 網路頻寬考量  
 同一個站台中的站台系統伺服器會使用伺服器訊息區 (SMB)、HTTP 或 HTTPS 彼此通訊 (因站台設定而有所不同)。 由於這些通訊未受管理，隨時可能發生，而且不受網路頻寬控制，請先檢閱可用的網路頻寬再將 Reporting Services 點角色安裝在站台系統中。  

> [!NOTE]  
>  如需規劃站台系統的詳細資訊，請參閱[新增站台系統角色](../deploy/configure/add-site-system-roles.md)。  

##  <a name="BKMK_RoleBaseAdministration"></a> 規劃以角色為基礎之系統管理的報告  
 報告的安全性與 Configuration Manager 中的其他物件類似，您可以指派安全性角色和權限給系統管理使用者。 系統管理使用者只能執行和修改他們擁有相關安全性權限的報告。 若要在 Configuration Manager 主控台中執行報告，您必須具有 [站台] 權限的 [讀取] 權限，以及針對特定物件設定的權限。  

 不過，與 Configuration Manager 中其他物件不同的是，在 Configuration Manager 主控台中設定系統管理員使用者的安全性權限後，也必須在 Reporting Services 中設定。 當您在 Configuration Manager 主控台中設定安全性權限時，Reporting Services 點會連線至 Reporting Services，並且設定適當的報告權限。 例如，[軟體更新管理員]  安全性角色擁有與其相關聯的 [執行報告]  和 [修改報告]  權限。 只獲得 [軟體更新管理員]  角色指派的系統管理員使用者，只能執行和修改軟體更新報告。 Configuration Manager 主控台不會顯示其他物件的報告。 未與特定 Configuration Manager 安全物件建立任何關聯性的報告是例外。 就這些報告而言，系統管理員使用者必須擁有 [站台]  的 [讀取]  權限才能執行報告，而要有 [站台]  的 [修改]  權限才能修改報告。  

 針對以角色為基礎的系統管理，已完全啟用報告。 包含於 Configuration Manager 的所有報告資料，會依照執行報告之系統管理使用者權限進行篩選。 具特定角色的系統管理使用者，只能檢視針對其角色定義的資訊。  

 如需報告安全性權限的詳細資訊，請參閱[設定報告](configuring-reporting.md)。  

 如需 Configuration Manager 中規劃站台系統的詳細資訊，請參閱[設定以角色為基礎的系統管理](../deploy/configure/configure-role-based-administration.md)。  

## <a name="next-steps"></a>後續步驟  
 下列其他主題可協助您規劃 Configuration Manager 中的報告功能：  

-   [System Center Configuration Manager 中報告的必要條件](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [System Center Configuration Manager 的報告最佳做法](../../../core/servers/manage/best-practices-for-reporting.md)  
