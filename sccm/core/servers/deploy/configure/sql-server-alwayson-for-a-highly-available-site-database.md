---
title: SQL Server Always On | Microsoft Docs
description: "規劃以將 SQL Server AlwaysOn 可用性群組與 SCCM 搭配使用。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c746365238e1255d73387a9496521bb03a56b21b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>準備將 SQL Server AlwaysOn 可用性群組與 Configuration Manager 搭配使用

*適用於︰System Center Configuration Manager (最新分支)*

準備 System Center Configuration Manager 以使用 SQL Server Always On 可用性群組作為站台資料庫的高可用性與災害復原解決方案。  
Configuration Manager 支援在下列位置使用可用性群組：
-     在主要站台和管理中心網站。
-     內部部署環境或 Microsoft Azure 中。

當您在 Microsoft Azure 中使用可用性群組時，可以使用「Azure 可用性設定組」來進一步提升站台資料庫的可用性。 如需 Azure 可用性集合的詳細資訊，請參閱 [管理虛擬機器的可用性](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)。

>  [!Important]   
>  在您繼續操作之前，必須先熟悉 SQL Server 和 SQL Server 可用性群組的設定。 接下來的資訊會參考 SQL Server 文件庫和程序。

## <a name="supported-scenarios"></a>支援的案例
以下是將可用性群組與 Configuration Manager 搭配使用的支援案例。 如需每個案例的詳細資料和程序，請參閱[設定 Configuration Manager 的可用性群組](/sccm/core/servers/deploy/configure/configure-aoag)。


-      [建立要與 Configuration Manager 搭配使用的可用性群組](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)。
-     [設定站台以使用可用性群組](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)。
-     [在裝載站台資料庫的可用性群組中新增或移除同步的複本成員](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members)。
-     [設定非同步認可複本](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (需要 Configuration Manager 1706 版或更新版本)。
-     [從非同步認可複本復原站台](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (需要 Configuration Manager 1706 版或更新版本)。
-     [將站台資料庫從可用性群組移到獨立 SQL Server 的預設或具名執行個體](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)。


## <a name="prerequisites"></a>先決條件
下列先決條件適用於所有案例。 如果有其他先決條件適用於特定案例，將會針對該案例詳述那些先決條件。   

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager 帳戶和權限
**站台伺服器對複本成員的存取：**   
站台伺服器的電腦帳戶必須是具備可用性群組成員身分之每部電腦上的 **「本機系統管理員」** 群組成員。

### <a name="sql-server"></a>SQL Server
**版本 (Version)：**  
可用性群組中的每個複本都必須執行您 Configuration Manager 版本所支援的 SQL Server 版本。 只要 SQL Server 支援，可用性群組的不同節點便可執行不同版本的 SQL Server。

**版本 (Edition)：**  
您必須使用 SQL Server *Enterprise* Edition。

**帳戶：**  
每個 SQL Server 執行個體都可在網域使用者帳戶 (**服務帳戶**) 或非網域帳戶下執行。 群組中的每個複本可以有不同的設定。 依據 [SQL Server 最佳做法](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd)，請使用具有最低可能權限的帳戶。

-   若要為 SQL Server 2016 設定「服務帳戶」和權限，請參閱 MSDN 上的[設定 Windows 服務帳戶和權限](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)。
-   若要使用非網域帳戶，您必須使用憑證。 如需詳細資訊，請參閱[使用資料庫鏡像端點憑證 (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql)。


如需詳細資訊，請參閱[為 Always On 可用性群組建立資料庫鏡像端點](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell)。

### <a name="availability-group-configurations"></a>可用性群組設定
**複本成員：**  
-   可用性群組必須有一個主要複本。
-   在 1706 版之前，您最多可以有兩個同步次要複本。
-   從 1706 版開始，您在可用性群組中可使用的複本數量和類型，與您所使用 SQL Server 版本所支援的複本數量和類型相同。

    您可以使用非同步認可複本來復原您的同步複本。 如需有關如何完成此操作的資訊，請參閱＜備份與復原＞主題中的[站台資料庫復原選項]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption)。
    > [!CAUTION]  
    > Configuration Manager 不支援容錯移轉成使用非同步認可複本作為您的站台資料庫。
由於 Configuration Manager 並不會驗證非同步認可複本的狀態來確認它是否為最新版，並且[這類複本在設計上即可能不同步]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes)，因此使用非同步認可複本作為站台資料庫將可能讓您站台和資料的完整性面臨風險。

每個複本成員必須：
-   使用 **[預設執行個體]**  
    從 1702 版開始，您可以使用「具名執行個體」。

-     將 [主要角色的連接] 設定為 [是]
-     將 [可讀取次要] 設定為 [是]  
-     針對 **[手動容錯移轉]**做設定      

    >  [!TIP]
    >  設定為 [自動容錯移轉] 時，Configuration Manager 支援使用可用性群組同步複本。 不過，在下列情況下必須設定 [手動容錯移轉]：
    >  -  您執行安裝程式來指定使用可用性群組中的站台資料庫。
    >  -  當您安裝任何 Configuration Manager 更新 (不僅僅是適用於站台資料庫的更新) 時。  

**複本成員位置：**  
可用性群組中的所有複本都必須裝載在內部部署環境或 Microsoft Azure 中。 不支援含有內部部署成員和 Azure 中成員的群組。     

當您在 Azure 中設定可用性群組，而該群組位於內部或外部負載平衡器之後時，您必須開啟下列預設連接埠，才能讓安裝程式存取每個複本：   

-     RCP 端點對應程式 - **TCP 135**   
-     伺服器訊息區 - **TCP 445**  
    *您可以在資料庫移動完成之後移除此連接埠。從 1702 版開始，已不再需要此連接埠。*
-     SQL Server Service Broker - **TCP 4022**
-     透過 TCP 的 SQL - **TCP 1433**   

在安裝程式執行完成之後，下列連接埠必須仍然可供存取：
-     SQL Server Service Broker - **TCP 4022**
-     透過 TCP 的 SQL - **TCP 1433**

從 1702 版開始，您可以使用自訂連接埠來進行這些設定。 相同的連接埠必須供端點使用，在可用性群組中的所有複本上也必須使用這些連接埠。


**接聽程式：**   
可用性群組至少必須有一個 **可用性群組接聽程式**。 當您將 Configuration Manager 設定為使用可用性群組中的站台資料庫時，將會使用此接聽程式的虛擬名稱。 雖然一個可用性群組可以包含多個接聽程式，但是 Configuration Manager 只能使用一個接聽程式。 如需詳細資訊，請參閱[建立或設定可用性群組接聽程式 (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)。

**檔案路徑：**   
當您執行 Configuration Manager 安裝程式來設定讓站台使用可用性群組中的資料庫時，每部次要複本伺服器都必須具有 SQL Server 檔案路徑，且此路徑與在目前主要複本上找到之站台資料庫檔案的檔案路徑相同。
-   如果相同的路徑不存在，安裝程式就無法新增可用性群組執行個體作為站台資料庫的新位置。
-   此外，本機 SQL Server 服務帳戶必須具備此資料夾的「完全控制」權限。

只有當您使用安裝程式來指定可用性群組中的資料庫執行個體時，次要複本伺服器才需要此檔案路徑。 在安裝程式完成可用性群組中站台資料庫的設定之後，您可以從次要複本伺服器刪除不使用的路徑。

例如，請考慮下列案例：
-   您建立一個使用三部 SQL Server 的可用性群組。

-   您的主要複本伺服器是 SQL Server 2014 的全新安裝。 根據預設，資料庫 .MDF 和 .LDF 檔案會儲存在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA。

-   您的兩個次要複本伺服器已從舊版升級至 SQL Server 2014，並保留原始的檔案路徑來儲存下列位置的資料庫檔案︰C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA。

-   嘗試將站台資料庫移至這個可用性群組之前，您必須在每個次要複本伺服器上建立下列檔案路徑 (即使次要複本並不會使用這個檔案位置)︰C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (這與主要複本上使用的路徑相同)。

-   接著，您需將該伺服器上新建立之檔案位置的完全控制存取權，授與每個次要複本上的 SQL Server 服務帳戶。

-   現在，您即可成功執行 Configuration Manager 安裝程式，來設定讓站台使用可用性群組中的站台資料庫。

**設定新複本上的資料庫：**   
 您必須為每個複本的資料庫進行下列設定：
-   [CLR 整合] 必須為 [已啟用]
-     [最大文字複寫大小] 必須為 *2147483647*
-     資料庫擁有者必須為 [SA 帳戶]
-     [TRUSTWORTY] 必須為 [ON]
-     [Service Broker] 必須為 [已啟用]

您只能在主要複本上進行這些設定。 若要設定次要複本，您必須先將主要複本容錯移轉成次要複本，以讓次要複本成為新的主要複本。   

請視需要使用 SQL Server 文件來協助您進行這些設定。 例如，請參閱 SQL Server 文件中的 [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) 或 [CLR 整合](/sql/relational-databases/clr-integration/clr-integration-enabling)。

### <a name="verification-script"></a>驗證指令碼
您可以執行下列指令碼來驗證主要複本及次要複本的資料庫設定。 您必須先將次要複本變更為主要複本，才能修正次要複本上的問題。

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:

## <a name="limitations-and-known-issues"></a>限制與已知問題
下列限制適用於所有案例。   

**不支援基本可用性群組：**  
[基本可用性群組](https://msdn.microsoft.com/library/mt614935.aspx)是在 SQL Server 2016 Standard Edition 中引進，這些群組不支援對次要複本的讀取存取，而這是與 Configuration Manager 搭配使用的一項需求。

**裝載額外可用性群組的 SQL Server︰**   
在 Configuration Manager 1610 版之前，當 SQL Server 上的可用性群組除了您用於 Configuration Manager 的群組之外還裝載一或多個可用性群組時，每個這些額外可用性群組中的每個複本在您執行 Configuration Manager 安裝程式或安裝 Configuration Manager 的更新時，必須都已做好下列設定：
-   **[手動容錯移轉]**
-   **[允許任何唯讀連線]**

**不支援的資料庫使用：**
-   **Configuration Manager 僅支援可用性群組中的站台資料庫：**不支援下列資料庫：
    -   報表資料庫
    -   WSUS 資料庫
-   **既存的資料庫：**您無法使用在複本上建立的新資料庫。 反之，當您設定可用性群組時，必須將現有 Configuration Manager 資料庫的複本還原至主要複本。

**ConfigMgrSetup.log 中的安裝程式錯誤：**  
當您執行安裝程式來將站台資料庫移至可用性群組時，安裝程式會嘗試處理可用性群組之次要複本上的資料庫角色，並記錄錯誤，如下所示：
-   錯誤︰SQL Server 錯誤：[25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server] 無法更新資料庫 "CM_AAA"，因為資料庫處於唯讀狀態。 Configuration Manager 安裝程式 2016 年 1 月 21 日下午 4:54:59 7344 (0x1CB0)  

您可以放心地忽略這些錯誤。

## <a name="changes-for-site-backup"></a>站台備份的變更
**備份資料庫檔案：**  
當站台資料庫在可用性群組中執行時，您應該執行內建的「備份站台伺服器」維護工作，以備份常用的 Configuration Manager 設定和檔案。 不過，請勿使用該備份所建立的 .MDF 或 .LDF 檔案， 應改為使用 SQL Server 來直接備份這些資料庫檔案。

**交易記錄檔：**  
站台資料庫的復原模型必須設定為 [完整] \(在可用性群組中使用時的需求)。 使用此設定時，請規劃以監視及維護站台資料庫交易記錄檔的大小。 在完整復原模式下，必須等到建立資料庫或交易記錄檔的完整備份之後，才會強行寫入交易。 如需詳細資訊，請參閱 SQL Server 文件中的 [SQL Server 資料庫的備份與還原](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)。

## <a name="changes-for-site-recovery"></a>站台復原的變更
如果至少有一個可用性群組節點仍然可運作，您便可以使用 [略過資料庫復原 (如果資料庫未受到影響，則使用此選項)] 站台復原選項。

 當可用性群組的所有節點都已遺失時，您則必須先重新建立可用性群組，才能復原站台。 Configuration Manager 無法重建或還原可用性節點。 在重新建立群組並已還原及重新設定備份之後，您便可以使用 [略過資料庫復原 (如果資料庫未受到影響，則使用此選項)] 站台復原選項。

如需詳細資訊，請參閱 [System Center Configuration Manager 備份和復原](/sccm/protect/understand/backup-and-recovery)。

## <a name="changes-for-reporting"></a>報告的變更
**安裝 Reporting Services 點：**  
Reporting Services 點不支援使用可用性群組的接聽程式虛擬名稱，或是將 Reporting Services 資料庫裝載在 SQL Server Always On 可用性群組中：
-   根據預設，Reporting Services 點安裝會將 [站台資料庫伺服器名稱] 設定為指定成接聽程式的虛擬名稱。 請將此名稱變更為指定可用性群組中複本的電腦名稱和執行個體。
-   若要在某個複本節點離線時，卸載報告負載並提升可用性，請考慮在每個複本節點上安裝額外的 Reporting Services 點，並將每個 Reporting Services 點設定為指向自己的電腦名稱。

當您在可用性群組的每個複本上安裝 Reporting Services 點時，報告功能將一律可以連線到作用中的報告點伺服器。

**切換主控台所使用的 Reporting Services 點：**  
若要執行報告，請在主控台中移至 [監視] > [概觀] > [報告] > [報告]，然後選擇 [報告選項]。 在 [報告選項] 對話方塊中，選取所需的 Reporting Services 點。

## <a name="next-steps"></a>後續步驟
在您了解使用可用性群組時所需的先決條件、限制及對一般工作所做的變更之後，請參閱[設定 Configuration Manager 的可用性群組](/sccm/core/servers/deploy/configure/configure-aoag)，以了解安裝及設定站台以使用可用性群組的程序。
