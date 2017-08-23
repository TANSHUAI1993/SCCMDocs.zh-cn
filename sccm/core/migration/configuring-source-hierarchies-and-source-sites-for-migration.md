---
title: "移轉來源階層 | Microsoft Docs"
description: "設定來源階層和來源站台，以將資料移轉至 System Center Configuration Manager 環境。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 80c43ab93ee5a2de6bf8d7993dfd46f0005d2df8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>設定來源階層和來源站台以移轉到 System Center Configuration Manager

*適用於：System Center Configuration Manager (最新分支)*

若要讓資料移轉至您的 System Center Configuration Manager 環境，您必須設定支援的 Configuration Manager 來源階層，以及該階層中一或多個包含您想要移轉之資料的來源站台。  

> [!NOTE]  
>  移轉操作會在目的地階層的頂層站台執行。 如果您在使用連線到主要子站台的 Configuration Manager 主控台時設定移轉，您必須預留時間將設定複寫到管理中心網站、啟動以及將狀態複寫回所連線的主要站台。  

 使用下列各節的資訊和程序，指定來源階層並新增其他來源站台。 完成這些程序後，您可以建立移轉作業，並開始將資料從來源階層移轉到目的地階層。  

-   [指定移轉的來源階層](#BKBM_ConfigSrcHierarchy)  

-   [識別來源階層的其他來源站台](#BKBM_ConfigSrcSites)  

##  <a name="BKBM_ConfigSrcHierarchy"></a> 指定移轉的來源階層  
 若要將資料移轉到目的地階層，您必須指定支援的來源階層，該階層內含您要移轉的資料。 根據預設，該階層的頂層站台會成為來源階層的來源站台。 如果您從 Configuration Manager 2007 階層移轉，在從初始來源站台收集資料後，可以設定其他用於移轉的來源站台。 如果您從 System Center 2012 Configuration Manager 或 System Center Configuration Manager 階層移轉，就不需要設定其他從來源階層移轉資料的來源站台。 這是因為 Configuration Manager 的這些版本會使用可在來源階層頂層站台使用的共用資料庫。 共用資料庫含有所有您可以移轉的資訊。  

 使用下列程序指定移轉的來源階層，以及識別 Configuration Manager 2007 階層中的其他來源站台。  

 請使用連線至目的地階層的 Configuration Manager 主控台來執行此程序：  

### <a name="to-configure-a-source-hierarchy"></a>設定來源階層   

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [移轉] ，然後按一下 [來源階層] 。  

3.  在 [首頁]  索引標籤的 [移轉]  群組中，按一下 [指定來源階層] 。  

4.  在 [指定來源階層]  對話方塊中，對於 [來源階層] ，選取 [新增來源階層] 。  

5.  對於**頂層 Configuration Manager 站台伺服器**，輸入支援的來源階層的頂層站台名稱或 IP 位址。  

6.  指定具有下列權限的來源站台存取帳戶：  

    -   來源站台帳戶：來源階層中指定頂層站台之 SMS 提供者的 [讀取]  權限。 發佈點共用及升級需要在來源階層中具有該站台的「修改」和「刪除」權限。

    -   來源站台資料庫帳戶：來源階層中指定頂層站台之 SQL Server 資料庫的 [讀取]  和 [執行]  權限。  

     如果您指定電腦帳戶的用途，Configuration Manager 會使用目的地階層的頂層站台電腦帳戶。 使用此選項時，請確保此帳戶是來源階層頂層站台所在網域中的安全性群組 [分散式 COM 使用者] 的成員。  

7.  若要在來源和目的地階層間共用發佈點，請選取 [啟用來源站台伺服器的發佈點共用]  核取方塊。 如果您此時尚未啟用發佈點共用，可以完成在資料收集後，藉由編輯來源站台的認證來完成此動作。  

8.  按一下 [確定]  儲存設定。 此時會開啟 [資料收集狀態]  對話方塊，並會自動開始收集資料。  

9. 完成資料收集時，請按一下 [關閉]  以關閉 [資料收集狀態]  對話方塊，並完成設定。  

##  <a name="BKBM_ConfigSrcSites"></a> 識別來源階層的其他來源站台  
 當您設定支援的來源階層時，會將該階層的頂層站台自動設定為來源站台，並自動從該站台收集資料。 您應採取的下一個動作，取決於來源階層所執行的 Configuration Manager 版本：  

-   對於 Configuration Manager 2007 來源階層，在完成初始來源站台的資料收集後，您可以開始只從該初始來源站台進行移轉，或者設定來源階層的其他來源站台。 若要移轉只能從子站台使用的資料，請為 Configuration Manager 2007 階層設定其他來源站台。 例如，您可以將其他來源站台設定為，當您要移轉的內容是在來源階層中的子站台建立，而且無法在來源階層的頂層站台使用時，即收集關於該內容的資料。  

-   若為 System Center 2012 Configuration Manager 或 System Center Configuration Manager 來源階層，則不必設定額外的來源站台。 這是因為 Configuration Manager 的這些版本會使用可在來源階層頂層站台使用的共用資料庫。 共用資料庫具有您可以從該來源階層中所有站台移轉的所有資訊。 這使得您可以移轉的資料可以從來源階層的頂層站台使用。  

當您為 Configuration Manager 2007 來源階層設定其他來源站台時，您必須設定從來源階層的頂層到底層的其他來源站台。 您必須將父站台設定為來源站台，才能將其子站台設定為來源站台。  

使用下列程序可設定 Configuration Manager 2007 來源階層的其他來源站台：  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>識別來源階層的其他來源站台 

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [移轉] ，然後按一下 [來源階層] 。  

3.  選擇您要將其設定為來源站台的站台。  

4.  在 [首頁]  索引標籤的 [來源站台]  群組中，按一下 [設定] 。  

5.  在 [來源站台認證]  對話方塊中，針對來源站台存取帳戶指定具有下列權限的帳戶：  

    -   來源站台帳戶：來源階層中指定頂層站台之 SMS 提供者的 [讀取]  權限。 發佈點共用及升級需要在來源階層中具有該站台的「修改」和「刪除」權限。  

    -   來源站台資料庫帳戶：來源階層中指定頂層站台之 SQL Server 資料庫的 [讀取]  和 [執行]  權限。  

    如果您指定電腦帳戶的用途，Configuration Manager 會使用目的地階層的頂層站台電腦帳戶。 使用此選項時，請確保此帳戶是來源階層頂層站台所在網域中的安全性群組 [分散式 COM 使用者] 的成員。  

6.  若要在來源和目的地階層間共用發佈點，請選取 [啟用來源站台伺服器的發佈點共用]  核取方塊。 如果您此時尚未啟用發佈點共用，可以在完成資料收集後，藉由編輯來源站台的認證來完成此動作。  

7. 按一下 [確定]  儲存設定。 此時會開啟 [資料收集狀態]  對話方塊，並會自動開始收集資料。  

8.  當完成資料收集時，可按一下 [關閉]  完成設定。  
