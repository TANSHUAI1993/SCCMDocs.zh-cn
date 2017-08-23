---
title: "支援的 SQL Server 版本 | Microsoft Docs"
description: "取得裝載 System Center Configuration Manager 站台資料庫的 SQL Server 版本和設定需求。"
ms.custom: na
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: "21"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b35e45b9514297e2f9ce405a3244462ed735f39f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 SQL Server 版本支援

適用於：System Center Configuration Manager (最新分支)

每個 System Center Configuration Manager 站台都必須有支援的 SQL Server 版本和設定，才能裝載站台資料庫。  

##  <a name="bkmk_Instances"></a> SQL Server 執行個體和位置  
 **管理中心網站和主要站台：**  
站台資料庫必須使用完整的 SQL Server 安裝。  

 SQL Server 可以位於：  

-   站台伺服器電腦。  
-   站台伺服器的遠端電腦。  

以下是支援的執行個體：  

-   SQL Server 預設或具名執行個體。  
-   多個執行個體設定。  
-   SQL Server 叢集。 請參閱[使用 SQL Server 叢集裝載站台資料庫](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)。
-   SQL Server AlwaysOn 可用性群組。 此選項需要 Configuration Manager 1602 或更新版本。 如需詳細資訊，請參閱[適用於 System Center Configuration Manager 之高可用性站台資料庫的 SQL Server AlwaysOn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)。


 **次要站台：**  
 站台資料庫可以使用預設的完整 SQL Server 安裝執行個體，或是使用 SQL Server Express。  

 SQL Server 必須位於站台伺服器電腦上。  

 **支援上的限制**   
 不支援下列設定：
 -   網路負載平衡 (NLB) 叢集設定中的 SQL Server 叢集
 -   叢集共用磁碟區 (CSV) 上的 SQL Server 叢集
 -   SQL Server 資料庫鏡像技術以及點對點複寫

僅支援將 SQL Server 異動複寫用於將物件複寫至設定為使用[資料庫複本](https://technet.microsoft.com/library/mt608546.aspx)的管理點。  

##  <a name="bkmk_SQLVersions"></a> 支援的 SQL Server 版本  
 在具有多個站台的階層中，只要符合下列條件，不同站台就可以使用不同版本的 SQL Server 來裝載站台資料庫：
 -  Configuration Manager 支援您使用的 SQL Server 版本。
 -  您所使用的 SQL Server 版本仍受 Microsoft 支援。
 -  SQL Server 支援這兩種 SQL Server 版本之間的複寫。  例如，[SQL Server 不支援 SQL Server 2008 R2 和 SQL Server 2016 之間的複寫 (英文)](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication)。



 除非另有指定，否則以下是 System Center Configuration Manager 所有現用版本支援的 SQL Server 版本。 如果新增新 SQL Server 版本或 Service Pack 的支援，則會註明新增該支援的 Configuration Manager 版本。 同樣地，如果支援已被取代，則請查看受影響之 Configuration Manager 版本的相關詳細資料。   

針對特定 SQL Server Service Pack 的支援包括累積至該 Service Pack 的更新，除非某個累積更新會中斷針對該 Service Pack 基準版本的回朔。 沒有註明 Service Pack 版本時，支援所針對的是沒有 Service Pack 的特定 SQL Server 版本。 在未來，如果針對該版本發行 Service Pack，將會在支援新的 Service Pack 版本之前，宣告個別的支援聲明。


> [!IMPORTANT]  
>  當您在管理中心網站針對資料庫使用 SQL Server Standard 時，您會限制一個階層所能支援的用戶端總數。 請參閱 [Size and scale numbers](../../../core/plan-design/configs/size-and-scale-numbers.md) (大小與縮放比例)。

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1：Standard、Enterprise  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要站台  
-   次要站台  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016：Standard、Enterprise  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要站台  
-   次要站台  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2：Standard、Enterprise  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要站台  
-   次要站台



### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1：Standard、Enterprise  
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要站台  
-   次要站台


### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3：Standard、Enterprise  
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要站台  
-   次要站台  

<!-- Support for this service pack version has been dropped by Microsoft    
### SQL Server 2012 SP2: Standard, Enterprise   
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   A central administration site  
-   A primary site  
-   A secondary site  
-->

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3：Standard、Enterprise、Datacenter     
  [從 1702 版開始](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database)，不支援此版本的 SQL Server。  
 當您使用 1702 之前的 Configuration Manager 版本時，仍支援此版本的 SQL Server。

在受到您的 Configuration Manager 版本支援的情況下，您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   管理中心網站  
-   主要站台
-   次要站台



### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：
-   次要站台

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：
-   次要站台


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要站台  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要站台  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
您可以針對下列各項使用這個不含最低累計更新版本的 SQL Server 版本：  

-   次要站台  

<!-- Support for this service pack version has been dropped by Microsoft   
### SQL Server 2012 Express SP2   
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   A secondary site  
-->


##  <a name="bkmk_SQLConfig"></a> 必要的 SQL Server 組態  
 以下是您用於站台資料庫的所有 SQL Server 安裝 (包括 SQL Server Express) 的必要設定。 如果 Configuration Manager 在安裝次要站台時一併安裝 SQL Server Express，就會自動為您建立這些設定。  

 **SQL Server 架構版本：**  
 Configuration Manager 需要 64 位元版本的 SQL Server 才能裝載站台資料庫。  

 **資料庫定序：**  
 在每個站台，用於站台和站台資料庫的 SQL Server 執行個體都必須使用下列定序： **SQL_Latin1_General_CP1_CI_AS**。  

 Configuration Manager 支援此定序的兩種例外狀況，以符合用於中國以 GB18030 定義的標準。 如需詳細資訊，請參閱 [System Center Configuration Manager 的多語系支援](../../../core/plan-design/hierarchy/international-support.md)。  

 **SQL Server 功能：**  
 只有 **Database Engine Services** 功能為每個站台伺服器所需。  

 Configuration Manager 資料庫複寫不需要 **SQL Server 複寫**功能。 不過，如果您使用 [System Center Configuration Manager 的管理點資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)，則需要此 SQL Server 設定。  

 **Windows 驗證：**  
 Configuration Manager 需要 **Windows 驗證**來驗證資料庫連線。  

 **SQL Server 執行個體：**  
 您必須為每個站台使用專用的 SQL Server 執行個體。 可以是 **具名執行個體** 或 **預設執行個體**。  

 **SQL Server 記憶體：**  
 使用 SQL Server Management Studio 並設定 [伺服器記憶體選項] 底下的 [最小伺服器記憶體]，即可保留 SQL Server 的記憶體。 如需如何設定固定記憶體容量的詳細資訊，請參閱 [如何：設定固定的記憶體容量 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759)。  

-   **針對與站台伺服器安裝在相同電腦上的資料庫伺服器：**請將 SQL Server 記憶體限制在可用可定址系統記憶體的 50% 到 80%。  

-   **針對專用資料庫伺服器 (站台伺服器的遠端)：**請將 SQL Server 記憶體限制在可用可定址系統記憶體的 80% 到 90%。  

-   **針對為每個使用中 SQL Server 執行個體的緩衝集區所保留的記憶體：**  

    -   針對管理中心網站：最少設定 8 GB。  
    -   針對主要站台：最少設定 8 GB。  
    -   針對次要站台：最少設定 4 GB。  

**SQL 巢狀觸發程序：**  
 必須啟用[SQL 巢狀觸發程序](http://go.microsoft.com/fwlink/?LinkId=528802) 。  

 **SQL Server CLR 整合**  
  站台資料庫會要求啟用 SQL Server 通用語言執行平台 (CLR)。 當 Configuration Manager 安裝時，會自動啟用此功能。 如需 CLR 的詳細資訊，請參閱 [SQL Server CLR 整合簡介](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)。  

##  <a name="bkmk_optional"></a> 選擇性的 SQL Server 組態  
 下列組態可選擇性用於使用完整 SQL Server 安裝的各個資料庫。  

 **SQL Server 服務：**  
 您可以將 SQL Server 服務設為執行時使用：  

-   **網域本機使用者**帳戶：  

    -   這是最佳做法，可能需要您手動註冊該帳戶的服務主體名稱 (SPN)。  

-   執行 SQL Server 的電腦**本機系統**帳戶：  

    -   使用本機系統帳戶簡化組態程序。  
    -   當您使用本機系統帳戶時，Configuration Manager 會自動註冊 SQL Server 服務的 SPN。  
    -   請注意，針對 SQL Server 服務使用本機系統帳戶不是 SQL Server 最佳做法。  

當執行 SQL Server 的電腦不使用其本機系統帳戶執行 SQL Server 服務時，您必須在 Active Directory 網域服務中，設定執行 SQL Server 服務之帳戶的 SPN (若是使用系統帳戶，將會自動為您登錄 SPN)。

如需站台資料庫 SPN 的資訊，請參閱[修改您的 System Center Configuration Manager 基礎結構](../../../core/servers/manage/modify-your-infrastructure.md)主題中的[管理站台資料庫伺服器的 SPN](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN)。  

如需如何變更 SQL Server 服務所用帳戶的資訊，請參閱[如何：變更 SQL Server 的服務啟動帳戶 (SQL Server 設定管理員)](http://go.microsoft.com/fwlink/p/?LinkId=237661)。  

**SQL Server Reporting Services：**  
需要有 SQL Server Reporting Services 才能安裝可讓您執行報告的 Reporting Services 點。  

> [!IMPORTANT]  
> 從舊版升級 SQL Server 之後，您可能會看到下列錯誤︰「報表產生器不存在」。    
> 若要解決這個錯誤，您必須重新安裝 Reporting Services 點站台系統角色。

**SQL Server 連接埠：**  
如為 SQL Server 資料庫引擎和站台間複寫通訊，可以使用預設 SQL Server 連接埠設定或指定自訂連接埠：  

-   **站台間通訊**使用 SQL Server Service Broker，其預設使用連接埠 TCP 4022。  
-   SQL Server 資料庫引擎與不同 Configuration Manager 站台系統角色之間的**站台內通訊**，預設會使用連接埠 TCP 1433。 下列網站系統角色會直接與 SQL Server 資料庫通訊：  

    -   管理點  
    -   SMS 提供者的電腦  
    -   Reporting Services 點  
    -   網站伺服器  

當執行 SQL Server 的電腦裝載來自多個站台的資料庫時，每個資料庫都必須使用不同的 SQL Server 執行個體。 此外，每個執行個體都必須設定為使用一組唯一的連接埠。  

> [!WARNING]  
>  Configuration Manager 不支援動態連接埠。 由於 SQL Server 具名執行個體預設使用動態連接埠連線至資料庫引擎，因此，當您使用具名執行個體時，必須手動設定要用於網站間通訊的靜態連接埠。  

如果在執行 SQL Server 的電腦上啟用防火牆，請確定將其設定為允許您的部署正在使用之連接埠，以及與 SQL Server 通訊的電腦之間的任何網路位置所使用的連接埠。  

如需如何將 SQL Server 設為使用特定連接埠的範例，請參閱 SQL Server TechNet 文件庫中的 [如何：將伺服器設為在特定 TCP 連接埠上接聽 (SQL Server 組態管理員)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 。  

## <a name="upgrade-options-for-sql-server"></a>SQL Server 的升級選項
如果需要升級您的 SQL Server 版本，建議使用下列方法 (依複雜度由低到高排列)。
1. [就地升級 SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (建議選項)。
2. 在新的電腦上安裝新的 SQL Server 版本，然後[使用 Configuration Manager 安裝程式的資料庫移動](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)選項，將您的站台伺服器指向新的 SQL Server。
3. 使用[備份及復原](/sccm/protect/understand/backup-and-recovery)。
