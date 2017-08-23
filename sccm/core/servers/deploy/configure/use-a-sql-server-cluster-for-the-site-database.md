---
title: "SQL Server 叢集 | Microsoft Docs"
description: "使用 SQL Server 叢集來裝載 System Center Configuration Manager 站台資料庫。 包含所支援選項的相關資訊。"
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 53f119bbb1f8827a9c23c8b747840350bbb92790
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>針對 System Center Configuration Manager 站台資料庫使用 SQL Server 叢集

*適用於：System Center Configuration Manager (最新分支)*


 您可以使用 SQL Server 叢集來裝載 System Center Configuration Manager 站台資料庫。 站台資料庫是伺服器叢集唯一支援的站台系統角色。  

> [!IMPORTANT]  
>  成功設定 SQL Server 叢集遵循 SQL Server 文件庫中所提供的文件和程序。  

 叢集可以提供容錯移轉支援，並改善站台資料庫的可靠性。 不過，它未提供額外的處理或負載平衡好處。 事實上，因為站台伺服器必須先尋找作用中的 SQL Server 叢集節點，才能連線到站台資料庫，所以效能可能會因此而降低。  

 安裝 Configuration Manager 之前，必須先準備 SQL Server 叢集，以支援 Configuration Manager。 (請參閱本節後面的先決條件)。  

 在 Configuration Manager 安裝期間，會在 Microsoft Windows Server 叢集的每個實體電腦節點上安裝 Windows 磁碟區陰影複製服務寫入器。 這支援**備份站台伺服器**維護工作。  

 安裝站台之後，Configuration Manager 會每小時檢查叢集節點有無變更。 Configuration Manager 會自動管理所偵測到會影響 Configuration Manager 元件安裝 (例如節點容錯移轉或新增 SQL Server 叢集的節點) 的變更。  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>使用 SQL Server 容錯移轉叢集的支援選項

用作站台資料庫的 SQL Server 容錯移轉叢集支援下列選項︰

-   單一執行個體叢集  

-   多個執行個體的組態  

-   多個作用中的節點  

-   具名執行個體或預設執行個體  

請注意下列先決條件：  

-   站台資料庫相對於站台伺服器而言，必須是遠端的資料庫 (叢集不得包含站台系統伺服器)。  

-   您必須將站台伺服器的電腦帳戶新增至叢集中每部伺服器的 [本機系統管理員] 群組。  

-   若要支援 Kerberos 驗證，必須為每個 SQL Server 叢集節點的網路連線啟用 **TCP/IP** 網路通訊協定。 **具名管道** 並非必要，但可用於疑難排解 Kerberos 驗證問題。 網路通訊設定是在 [SQL Server 組態管理員] 的 [SQL Server 網路組態] 下設定。  

-   若是使用 PKI，請參閱＜Configuration Manager 的 PKI 憑證需求＞中所述有關您為站台資料庫使用 SQL Server 叢集時的特定憑證需求。  

請考慮下列限制：  

-   **安裝及組態：**  

    -   次要站台無法使用 SQL Server 叢集。  

    -   當您指定 SQL Server 叢集時，無法使用用於為站台資庫指定非預設檔案位置的選項。  

-   **SMS 提供者：**  

    -   不支援在 SQL Server 叢集或以叢集 SQL Server 節點身分執行的電腦上，安裝 SMS 提供者的執行個體。  

-   **資料複寫選項：**  

    -   若要使用**分散式檢視**，將無法使用 SQL Server 叢集裝載站台資料庫。  

-   **備份及復原：**  

    -   Configuration Manager 不支援為使用具名執行個體的 SQL Server 叢集執行 Data Protection Manager (DPM) 備份。 不過，它確實支援在使用預設 SQL Server 執行個體的 SQL Server 叢集上執行 DPM 備份。  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>準備站台資料庫的叢集 SQL Server 執行個體  

以下是完成以準備站台資料庫的主要工作︰

-   建立虛擬 SQL Server 叢集，以便在現有的 Windows Server 叢集環境裝載站台資料庫。 如需安裝和設定 SQL Server 叢集的特定步驟，請參閱 SQL Server 版本的相關文件。 例如，若您使用的是 SQL Server 2008 R2，請參閱 [安裝 SQL Server 2008 R2 容錯移轉叢集](http://go.microsoft.com/fwlink/p/?LinkId=240231)。  

-   您可以在 SQL Server 叢集中不想讓 Configuration Manager 安裝站台元件之每一部電腦的每個磁碟機根資料夾中放置檔案。 此檔案應該命名為 **NO_SMS_ON_DRIVE.SMS**。 Configuration Manager 預設會在每個實體節點上安裝一些元件，以支援備份等作業。  

-   將站台伺服器的電腦帳戶新增至 Windows Server 叢集節點電腦的 [本機系統管理員]  群組。  

-   在虛擬 SQL Server 執行個體中，將 **sysadmin** SQL Server 角色指派給要執行 Configuration Manager 安裝程式的使用者帳戶。  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>使用叢集 SQL Server 安裝新的站台  
 若要安裝使用叢集站台資料庫的站台，除了下列幾個步驟之外，請遵循您安裝站台時的正常程序執行 Configuration Manager 安裝程式：  

-   在 [資料庫資訊]  頁面上，指定要裝載站台資料庫之虛擬 SQL Server 叢集執行個體的名稱。 此虛擬執行個體會取代執行 SQL Server 之電腦的名稱。  

    > [!IMPORTANT]  
    >  當您輸入輸入虛擬 SQL Server 叢集執行個體的名稱時，請勿輸入 Windows Server 叢集所建立的虛擬 Windows Server 名稱。 若是使用虛擬 Windows Server 名稱，站台資料庫將會安裝在作用中 Windows Server 叢集節點的本機硬碟上。 若該節點失敗，將會造成容錯移轉失敗。  
