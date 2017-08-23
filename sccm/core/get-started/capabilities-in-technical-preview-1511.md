---
title: "Technical Preview 1511 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1511 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: d0bde2c085cc9b330bc772e68081d629ca9e2f11
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1511-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1511 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1511 版中可用的功能。 此版本是 Technical Preview 的基準安裝，可供您用來安裝新的 Technical Preview 站台，或從舊版 Technical Preview 升級。   安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](/sccm/core/get-started/technical-preview) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

以下是您可以使用此版本試用的新功能。  

##  <a name="BKMK_WUfB"></a> 與 Windows 10 中的 Windows Update for Business 整合  
 Configuration Manager 現在能夠區分透過 Windows Update for Business (WUfB) 直接連線的 Windows 10 電腦，以及連線至 WSUS 以取得 Windows 10 更新與升級的電腦。  如果電腦是透過 WUfB 連線，則可以依照系統管理使用者透過群組原則或 MDM 原則設定的頻率來管理更新和升級，並可以直接從 WUfB 安裝這些更新/升級。    
如果電腦是透過 WUfB 連線，Configuration Manager 將無法報告相容性狀態 (包括 Windows Update 或定義更新)。 此外，Configuration Manager 無法將 Microsoft Update 或協力廠商更新部署到這些電腦。  

 **這個案例的必要條件：**  

-   Windows 10 Desktop Pro 或 Windows 10 Enterprise Edition 1511 版或更新版本。  

-   要透過 [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx)進行管理的電腦。  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

1.  如果之前已啟用 Windows Update 代理程式，請將其停用以免對 WSUS 進行掃描。   
    您可以設定登錄機碼 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** ，指出電腦要對 WSUS 或 Windows Update 進行掃描。  當值為 2 時，它不會對 WSUS 進行掃描。  

2.  請注意 Configuration Manager 資源總管之 [Windows Update] 節點下的新屬性 **UseWUServer** 。  

3.  根據透過 WUfB 連線以取得更新和升級之所有電腦的 **UseWUServer** 屬性，建立集合。  

4.  建立用戶端代理程式設定，以停用軟體更新工作流程，並將設定部署至直接連線到 WUfB 的電腦集合。  

5.  透過 WUfB 管理的電腦會在相容性狀態中顯示 [不明]  ，而且不會計入整體相容性百分比的一部分。  

##  <a name="BKMK_Office365ProPlus"></a> 透過 System Center Configuration Manager 管理 Office 365 ProPlus 用戶端更新  
 Configuration Manager 現在能夠使用 Configuration Manager 軟體更新管理工作流程，來管理 Office 365 桌面用戶端更新。    
當 Microsoft 發佈 Windows Server Updates Services (WSUS) 的新 Office 365 桌面用戶端更新時，如果 Office 365 更新已設定為類別目錄同步作業的一部分，Configuration Manager 便能將更新同步處理至其類別目錄。  Configuration Manager 站台伺服器會下載 Office 365 用戶端更新，並將套件發佈至 Configuration Manager 發佈點。  Configuration Manager 用戶端接著會通知 Office 365 桌面用戶端於何處取得更新，以及何時開始更新安裝程序。  

**這個案例的必要條件：**  

### <a name="try-it-out"></a>試試看！  
 請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

1.  您可以將 Office 365 更新同步處理至 Configuration Manager 站台伺服器，並從 Configuration Manager 主控台進行檢視。  

2.  您可以核准並成功部署 Office 365 更新。  

3.  您可以下載並成功將 Office 365 更新部署到用戶端。  

4.  您可以使用主控台中的監視或報告功能，來確認 Office 365 更新是否相容。  

 如需詳細步驟，請參閱 [透過 System Center Configuration Manager Technical Preview 管理 Office 365 用戶端更新](https://technet.microsoft.com/library/mt628083.aspx)。  

##  <a name="BKMK_AlwasyOn"></a> 支援適用於高可用性資料庫的 SQL Server AlwaysOn  
 Configuration Manager 現在支援使用 SQL Server AlwaysOn 可用性群組來裝載站台資料庫。  當您安裝新的站台時，您可以指示安裝程式使用可用性群組，而不是一般 SQL Server 執行個體。  

> [!NOTE]  
>  若要成功設定及使用可用性群組，您必須熟悉 SQL Server 可用性群組的設定，並嚴格參考 SQL Server 文件庫中提供的文件和程序。  

設定及使用可用性群組的高階程序包括：  

1.  設定 SQL Server 中的可用性群組。  

2.  安裝新的 Configuration Manager 站台，並在安裝期間透過指定群組端點，來指示站台使用可用性群組。  

**這個案例的必要條件：**  

-   需要 Configuration Manager Technical Preview 支援的 SQL Server 版本  

-   您必須建立並設定 SQL Server 可用性群組，再安裝 Configuration Manager  

-   可用性群組必須有一個主要複本，而且最多可以有兩個同步次要複本  

-   可用性群組至少必須有一個端點  

-   您必須具有可用性群組中每部 SQL Server 都能存取的網路位置。 這個位置可供安裝程式用來設定可用性群組，並會在安裝完成之後加以移除。  

**本版的已知問題：**  

-   您無法將新的複本成員成功新增至站台資料庫中已在使用中的可用性群組。 相反地，您必須在新增複本成員之後重新安裝站台。  

-   在這個案例中，您可能需要在管理點伺服器上安裝 **SQL Server 2012 原生用戶端** ([從 SQL Server 2012 功能套件](http://www.microsoft.com/download/details.aspx?id=29065))。 如此可避免發生 SQL 連線錯誤 (記錄在管理點伺服器上的 **mp_getauth.log** 中)。  

### <a name="try-it-out"></a>試試看！  
請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

-   我可以安裝主要站台，該站台使用專為 SQL AlwaysOn 可用性群組所設定的資料庫伺服器  

-   我可以將 SQL AlwaysOn 可用性群組容錯移轉至群組中的新複本，而且主要站台仍可運作  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>針對 Configuration Manager 設定 SQL Server AlwaysOn  
 使用下列程序先建立及設定可用性群組，然後再安裝使用可用性群組的新 Configuration Manager 站台。  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>建立 SQL Server AlwaysOn 可用性群組  
[建立 SQL Server 可用性群組](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) 的程序記載於 SQL Server 文件庫中。  當您建立可用性群組時，請確定符合使用 Configuration Manager 的下列需求：  

-   最多三個成員：  

    -   一個主要複本和最多兩個次要複本  

    -   次要複本必須同步。  

        > [!TIP]  
        >  建議將次要複本設定成唯讀。 如此一來，您便能使用次要複本來執行報告等功能，同時保持主要複本執行站台作業的效能。  

-   至少一個端點。 當您安裝 Configuration Manager 站台時，會使用這個端點的虛擬名稱。  

    > [!TIP]  
    >  雖然這個群組可以包含多個端點，但是 Configuration Manager 只能使用一個端點。  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>安裝使用可用性群組的 Configuration Manager 站台  
若要安裝使用 SQL Server 可用性群組的站台：  

1.  在 Configuration Manager 安裝程式提示時，取代下列項目：  

    -   **SQL Server 名稱**：輸入建立可用性群組時所設定端點的虛擬名稱。 這個虛擬名稱應該是完整 DNS 名稱，例如 **&lt;端點伺服器\>.fabrikam.com**。  

    -   **執行個體**：這個值應該保留空白。 這個組態中沒有執行個體。  

    -   **資料庫**：輸入您在可用性群組的主要複本上所建立的資料庫名稱。  

2.  接下來，您必須提供群組中每部 SQL Server 都能存取的網路位置：  

    -   每部 SQL Server 上的電腦帳戶和服務帳戶都需要此位置的完全控制存取權限。  

    -   您只能在安裝期間使用這個位置，並且可以在安裝完成並安裝站台之後取消共用或刪除這個位置。  

3.  提供這項資訊之後，使用您的一般程序和組態來完成安裝。  

##  <a name="BKMK_ClusterServerUpdates"></a> 提供伺服器叢集服務  
您可以立即建立包含叢集中伺服器的集合，然後設定將更新部署到叢集時所要使用的叢集設定。 您可以控制任何指定時間在線上的伺服器百分比，並設定預先部署和部署後 PowerShell 指令碼來執行自訂動作。  

**本版的已知問題：**  

-   不會提供可檢查叢集伺服器之軟體更新部署狀態的報告。  

-   [叢集設定]  頁面上已停用維護順序選項，無法在本版中使用。  

### <a name="try-it-out"></a>試試看！  
請嘗試完成下列工作，然後使用本主題頂端附近的意見反應資訊，告訴我們工作的成效：  

-   我可以建立代表伺服器叢集的集合。 針對這項測試，您可以將收集成員資格規則設定為這個集合中有兩部電腦。  

-   我在提供叢集服務的任何時間點，只能指定叢集中 50% 的伺服器處於離線狀態。 使用程序中的範例指令碼來指定預先部署和部署後指令碼。  

-   將更新部署到這個集合。 檢閱 C:\temp 中的 start.txt 和 end.txt 檔案，並確認叢集中伺服器上的部署開始和結束時間。 如需詳細資訊，請檢閱 UpdatesDeployment.log 檔案。  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>若要建立伺服器叢集的集合  

1.  [建立裝置集合](https://technet.microsoft.com/library/gg712295.aspx)以包含叢集中的伺服器。  

2.  在 [資產與相容性] 工作區中，按一下 [裝置集合]，再以滑鼠右鍵按一下包含叢集伺服器的集合，然後按一下 [內容]。  

3.  在 [一般] 索引標籤上，選取 「All devices are part of the same server cluster」 (所有裝置都屬於相同的伺服器叢集)，然後按一下 [設定]。  

4.  在 [叢集設定] 頁面上，選取在安裝軟體更新時可以同時設為離線的伺服器百分比。 不論您提供的百分比為何，有可能一次只有一部叢集伺服器離線。 選取一次要服務幾部伺服器時，Configuration Manager 會無條件捨去成整數。 例如，如果您選擇 51%，且叢集中有 4 部伺服器，則相同時間內會將 2 部伺服器設為離線。  

5.  指定是否要使用預先部署 (節點清空) 指令碼或部署後 (節點繼續) 指令碼。  

    > [!TIP]  
    >  以下是可將目前時間寫入文字檔案之預先部署和部署後指令碼的測試範例：  
    >   
    >  **預先部署**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **部署後**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>若要將軟體更新部署至伺服器叢集  

1.  [部署軟體更新](https://technet.microsoft.com/library/gg712304.aspx)至伺服器叢集集合。  

2.  [監視軟體更新部署](https://technet.microsoft.com/library/gg712304.aspx)。  
