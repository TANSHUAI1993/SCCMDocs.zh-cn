---
title: "管理點資料庫複本 | Microsoft Docs"
description: "使用資料庫複本，以減少管理點對站台資料庫伺服器造成的 CPU 負載。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 130c053c9f2a1817dd85b1f3c01285aab19d59cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="database-replicas-for-management-points-for-system-center-configuration-manager"></a>System Center Configuration Manager 的管理點資料庫複本

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 主要站台可以使用資料庫複本，減少管理點在服務來自用戶端的要求時，對站台資料庫伺服器造成的 CPU 負載。  

-   管理點使用資料庫複本時，該管理點會從裝載資料庫複本的 SQL Server 電腦要求資料，而不會從站台資料庫伺服器要求資料。  

-   如此有助於減少站台資料庫伺服器上的 CPU 處理需求，方法是卸載與用戶端相關的常用處理工作。  用戶端常用處理工作的範例，包括有大量經常提出用戶端原則要求的用戶端之站台。  


##  <a name="bkmk_Prepare"></a> 準備使用資料庫複本  
**有關管理點的資料庫複本：**  

-   複本是站台資料庫的部分複本，其會複寫到另一個 SQL Server 執行個體：  

    -   主要站台為該站台的每個管理點，支援專用資料庫複本 (次要站台不支援資料庫複本)  

    -   相同站台的多個管理點單可使用單一個資料庫複本  

    -   只要每個管理點都在個別 SQL Server 執行個體中執行，SQL Server 就可以裝載多個資料庫複本，供不同的管理點使用  

-   為了此一目的，複本會將固定排程的站台資料庫複本，從該站台資料庫伺服器所發佈的資料，進行同步處理。  

-   可以將管理點設定為安裝管理點時使用複本，或稍後重新設定先前所安裝的管理點，以使用資料庫複本。  

-   請定期監視站台資料庫伺服器與每部資料庫複本伺服器，以確保彼此之間進行複寫，且資料庫複本伺服器的效能，可以滿足您所需的站台與用戶端效能。  

**資料庫複本的必要條件：**  

-   **SQL Server 需求：**  

    -   裝載資料庫複本的 SQL Server，必須符合和站台資料庫伺服器相同的需求。 但複本伺服器並不需要和站台資料庫伺服器執行相同的 SQL Server 版本，只要執行支援的 SQL Server 版本即可。 如需詳細資訊，請參閱 [System Center Configuration Manager 的 SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md)。  

    -   裝載複本資料庫的電腦上之 SQL Server Service，必須以 **System** 帳戶的身分執行。  

    -   裝載站台資料庫與裝載資料庫複本的 SQL Server，都必須要安裝 **SQL Server Replication** 。  

    -   站台資料庫必須 **發佈** 資料庫複本，且每個遠端資料庫複本伺服器，都必須 **訂閱** 已發佈的資料。  

    -   裝載站台資料庫與裝載資料庫複本的 SQL Server，都必須設定為支援 2 GB 的 **文字複寫大小上限** 。 如需有關如何為 SQL Server 2012 進行設定的範例，請參閱 [Configure the max text repl size Server Configuration Option (設定最大文字複寫大小伺服器設定選項)](http://go.microsoft.com/fwlink/p/?LinkId=273960)。  

-   **自我簽署憑證：** 若要設定資料庫複本，您必須在資料庫複本伺服器上建立自我簽署憑證，並讓使用該資料庫複本伺服器的每個管理點，都能使用此憑證。  

    -   該憑證會自動提供給安裝在資料庫複本伺服器上的管理點使用。  

    -   若要將此憑證提供給遠端管理點使用，必須匯出該憑證，再接著將其加入遠端管理點上的 **受信任的人員** 憑證存放區。  

-   **用戶端通知：** 若要為管理點支援資料複本的用戶端通知，必須為 **SQL Server Service Broker**設定站台資料庫伺服器與資料庫複本伺服器之間的通訊。 此作業需要：  

    -   為每個資料庫設有其他資料庫的相關資訊  

    -   在安全通訊的兩個資料庫之間交換憑證  

**使用資料庫複本時的限制：**  

-   當您的站台設定為發佈資料庫複本時，應使用下列程序取代一般的指導方針：  

    -   [解除安裝發佈資料庫複本的站台伺服器](#BKMK_DBReplicaOps_Uninstall)  

    -   [移動發佈資料庫複本的站台伺服器資料庫](#BKMK_DBReplicaOps_Move)  

-   **升級至 System Center Configuration Manager**：將站台從 System Center 2012 Configuration Manager 升級到 System Center Configuration Manager 之前，您必須停用管理點的資料庫複本。  升級站台之後，可為管理點重新設定資料庫複本。  

-   **單一 SQL Server 上的多個複本**：若將資料庫複本伺服器設定成要為管理點裝載多個資料庫複本 (每個複本都必須位於個別的執行個體上)，您必須使用經過修改的組態指令碼 (來自下一節的步驟 4)，以避免覆寫先前在該伺服器上設定的資料庫複本所使用的自我簽署憑證。  

##  <a name="BKMK_DBReplica_Config"></a> 設定資料庫複本  
若要設定資料庫複本，必須完成下列步驟：  

-   [步驟 1 - 設定站台資料庫伺服器以發佈資料庫複本](#BKMK_DBReplica_ConfigSiteDB)  

-   [步驟 2 - 設定資料庫複本伺服器](#BKMK_DBReplica_ConfigSrv)  

-   [步驟 3 - 設定要使用資料庫複本的管理點](#BKMK_DBReplica_ConfigMP)  

-   [步驟 4 - 設定資料庫複本伺服器的自我簽署憑證](#BKMK_DBReplica_Cert)  

-   [步驟 5 - 設定資料庫複本伺服器的 SQL Server Service Broker](#BKMK_DBreplica_SSB)  

###  <a name="BKMK_DBReplica_ConfigSiteDB"></a> 步驟 1 - 設定站台資料庫伺服器以發佈資料庫複本  
 使用下列程序作為範例，以引導您在 Windows Server 2008 R2 電腦上設定網站資料庫伺服器來發佈資料庫複本。 如果您有不同的作業系統版本，請參考您的作業系統文件並視需要調整您在此程序中的步驟。  

##### <a name="to-configure-the-site-database-server"></a>設定網站資料庫伺服器  

1.  在網站資料庫伺服器上，設定 SQL Server Agent 為自動啟動。  

2.  在網站資料庫伺服器上，以 **ConfigMgr_MPReplicaAccess**的名稱建立本機使用者群組。 您必須將您在此網站上使用的每個資料庫複本伺服器的電腦帳戶新增到此群組中，使這些資料庫複本伺服器與已發佈的資料庫複本同步。  

3.  在網站資料庫伺服器上，以 **ConfigMgr_MPReplica**的名稱設定檔案共用。  

4.  將下列權限新增至 **ConfigMgr_MPReplica** 共用：  

    > [!NOTE]  
    >  如果 SQL Server Agent 使用的帳戶與本機系統帳戶不同，請使用以下清單中的該帳戶名稱來取代 SYSTEM。  

    -   **共用權限**：  

        -   SYSTEM： **寫入**  

        -   ConfigMgr_MPReplicaAccess： **讀取**  

    -   **NTFS 共用權限**：  

        -   SYSTEM： **完全控制**  

        -   ConfigMgr_MPReplicaAccess：**讀取**、**讀取與執行**、**列出資料夾內容**  

5.  使用 **SQL Server Management Studio** 以連線至站台資料庫並執行下列預存程序進行查詢： **spCreateMPReplicaPublication**  

當完成預存程序時，網站資料庫伺服器會設定為發佈資料庫複本。  

###  <a name="BKMK_DBReplica_ConfigSrv"></a> 步驟 2 - 設定資料庫複本伺服器  
資料庫複本伺服器是執行 SQL Server 的電腦，並裝載網站資料庫的複本供管理點使用。 資料庫複本伺服器會依照固定排程，與網站資料庫伺服器發佈的資料庫複本同步處理其資料庫的複本。  

資料庫複本伺服器必須符合與網站資料庫伺服器相同的需求。 不過，資料庫複本伺服器執行的 SQL Server 版本可以與網站資料庫伺服器使用的版本不同。 如需 SQL Server 支援版本的資訊，請參閱 [System Center Configuration Manager 的 SQL Server 版本支援](../../../../core/plan-design/configs/support-for-sql-server-versions.md)主題。  

> [!IMPORTANT]  
>  SQL Server Service 在裝載複本資料庫的電腦上必須以系統帳戶的身分執行。  

使用下列程序作為範例，以引導您在 Windows Server 2008 R2 電腦上設定資料庫複本伺服器。 如果您有不同的作業系統版本，請參考您的作業系統文件並視需要調整您在此程序中的步驟。  

##### <a name="to-configure-the-database-replica-server"></a>設定資料庫複本伺服器  

1.  在資料庫複本伺服器上，設定 SQL Server Agent 為自動啟動。  

2.  在資料庫複本伺服器上，使用 [SQL Server Management Studio]  以連線至本機伺服器，然後瀏覽至 [複寫]  資料夾，按一下 [本機訂閱] 並選取 [新增訂閱]  以啟動 [新增訂閱精靈] ：  

    1.  在 [發行集]  頁面的 [發行者]  清單方塊中，選取 [尋找 SQL Server 發行者] 並輸入網站資料庫伺服器的名稱，然後按一下 [連接] 。  

    2.  選取 [ConfigMgr_MPReplica] ，然後按 [下一步] 。  

    3.  在 [散發代理程式位置]  頁面中，選取 [在訂閱者端執行每一個代理程式 (提取訂閱)] ，然後按 [下一步] 。  

    4.  在 [訂閱者]  頁面上，執行以下其中一項：  

        -   從資料庫複本伺服器選取現有的資料庫供資料庫複本使用，然後按一下 [確定] 。  

        -   選取 [新增資料庫]  為資料庫複本建立新的資料庫。 在 [新增資料庫]  頁面上，指定資料庫名稱，然後按一下 [確定] 。  

    5.  按 [下一步]  以繼續。  

    6.  在 [散發代理程式安全性] 頁面中，在對話方塊的 [訂閱者連接] 資料列中按一下內容按鈕 [(....)]，然後設定連接的安全性設定。  

        > [!TIP]  
        >  內容按鈕 [(.…)] 位於顯示方塊的第四欄中。  

        **安全性設定：**  

        -   設定執行散發代理程式處理的帳戶 (處理帳戶)：  

            -   如果 SQL Server Agent 以本機系統身分執行，請選取 [以 SQL Server Agent 服務帳戶執行 (這不是建議的安全性最佳作法)。]   

            -   如果您使用不同帳戶來執行 SQL Server Agent，請選取 [以下列 Windows 帳戶執行] ，然後設定該帳戶。 您可以指定 Windows 帳戶或 SQ Server 帳戶。  

            > [!IMPORTANT]  
            >  您必須將執行散發代理程式權限的帳戶授與發行者進行提取訂閱。 如需設定這些權限的資訊，請參閱 SQL Server TechNet 文件庫中的 [Distribution Agent Security (散發代理程式安全性)](http://go.microsoft.com/fwlink/p/?LinkId=238463) 。  

        -   針對 [連接到散發者] ，請選取 [藉由模擬處理帳戶] 。  

        -   針對 [連接到訂閱者] ，請選取 [藉由模擬處理帳戶] 。  

         在設定連接安全性設定之後，請按一下 [確定]  儲存設定，然後按 [下一步] 。  

    7.  在 [同步排程]  頁面的 [代理程式排程]  清單方塊中，選取 [定義排程] ，然後設定 [新增作業排程] 。 設定 [每日] 的頻率，並每隔 [5 分鐘] 重複一次，將持續時間設為 [沒有結束日期] 。 按 [下一步]  儲存排程，然後再按一次 [下一步]  。  

    8.  在 [精靈動作]  頁面中，選取 [建立訂閱] 的核取方塊，然後按 [下一步] 。  

    9. 在 [完成精靈]  頁面中，按一下 [完成] ，然後按一下 [關閉]  以完成精靈。  

3.  完成 [新增訂閱精靈] 之後，立即使用 **SQL Server Management Studio** 來連線到資料庫複本伺服器資料庫，然後執行下列查詢以啟用 TRUSTWORTHY 資料庫屬性：  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4.  檢閱同步處理狀態以確認訂閱是否成功：  

    -   在訂閱者電腦上：  

        -   在 [SQL Server Management Studio] 中，連線至資料庫複本伺服器並展開 [複寫] 。  

        -   展開 [本機訂閱] ，以滑鼠右鍵按一下網站資料庫發行的訂閱，然後選取 [檢視同步處理的狀態] 。  

    -   在發行者電腦上：  

        -   在 [SQL Server Management Studio] 中，連線至網站資料庫電腦，以滑鼠右鍵按一下 [複寫]  資料夾，然後選取 [啟動複寫監視器] 。  

5.  若要啟用資料庫複本的 Common Language Runtime (CLR) 整合，請使用 **SQL Server Management Studio** 以連線至資料庫複本伺服器上的資料庫複本，並執行下列預存程序進行查詢： **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6.  針對使用資料庫複本伺服器的每個管理點，將管理點電腦帳戶新增至該資料庫複本伺服器上的本機 [Administrators]  群組。  

    > [!TIP]  
    >  此步驟對於在資料庫複本伺服器上執行的管理點來說並非必要。  

 資料庫複本現在已備妥可供管理點使用。  

###  <a name="BKMK_DBReplica_ConfigMP"></a> 步驟 3 - 設定要使用資料庫複本的管理點  
 您可以在主要網站上設定管理點，使您在安裝管理點角色時可使用資料庫複本，或者您可以重新設定現有的管理點來使用資料庫複本。  

 使用下列資訊來設定管理點以使用資料庫複本：  

-   **若要設定新的管理點：** 在您用來安裝管理點的精靈 [管理點資料庫]  頁面上，選取 [使用資料庫複本] ，並為裝載資料庫複本的電腦指定 FQDN。 接下來，在 [ConfigMgr 網站資料庫名稱] 中指定資料庫複本在該電腦上的資料庫名稱。  

-   **若要設定之前安裝的管理點**：開啟管理點的內容頁面，選取 [管理點資料庫]  索引標籤，選取 [使用資料庫複本] ，然後為裝載資料庫複本的電腦指定 FQDN。 接下來，在 [ConfigMgr 網站資料庫名稱] 中指定資料庫複本在該電腦上的資料庫名稱。  

-   **針對會使用資料庫複本的每個管理點**，您必須手動將管理點伺服器的電腦帳戶加入資料庫複本的 **db_datareader** 角色。  

除了設定管理點以使用資料庫複本伺服器以外，您還必須在管理點的 [IIS]  中啟用 [Windows 驗證]  ：  

1.  開啟 [Internet Information Services (IIS) 管理員] 。  

2.  選取管理點使用的網站，並開啟 [驗證] 。  

3.  將 [Windows 驗證]  設為 [已啟用] ，然後關閉 [Internet Information Services (IIS) 管理員] 。  

###  <a name="BKMK_DBReplica_Cert"></a> 步驟 4 - 設定資料庫複本伺服器的自我簽署憑證  
 您必須在資料庫複本伺服器上建立自我簽署憑證，並且讓使用該資料庫複本伺服器的每個管理點都能使用此憑證。  

 該憑證會自動提供給安裝在資料庫複本伺服器上的管理點使用。 不過，您必須先匯出憑證，然後將其新增至遠端管理點上的 [受信任的人] 憑證存放區中，遠端管理點才能使用此憑證。  

 使用下列程序作為範例，以引導您在 Windows Server 2008 R2 電腦的資料庫複本伺服器上設定自我簽署憑證。 如果您有不同的作業系統版本，請參考您的作業系統文件並視需要調整您在這些程序中的步驟。  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>設定資料庫複本伺服器的自我簽署憑證  

1.  在資料庫複本伺服器上，使用系統管理權限開啟 PowerShell 命令提示，然後執行下列命令： **set-executionpolicy UnRestricted**  

2.  複製下列 PowerShell 指令碼並使用 **CreateMPReplicaCert.ps1**的名稱另存新檔。 將此檔案的複本置於資料庫複本伺服器的系統磁碟分割的根資料夾中。  

    > [!IMPORTANT]  
    >  如果要在單一 SQL Server 上設定多個資料庫複本，針對您所設定的每個後續複本，針對此程序，您都必須使用此指令碼的已修改版本。 請參閱  [單一的 SQL Server 上的其他資料庫複本補充指令碼](#bkmk_supscript)。  

    ```  
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  在資料庫複本伺服器上，執行已套用至 SQL Server 設定中的下列命令：  

    -   若是 SQL Server 預設執行個體：以滑鼠右鍵按一下檔案 [CreateMPReplicaCert.ps1]  ，並選取 [用 PowerShell 執行] 。 當指令碼執行時會建立自我簽署憑證，並設定 SQL Server 以使用憑證。  

    -   若是 SQL Server 的具名執行個體：使用 PowerShell 以執行命令 **%path%\CreateMPReplicaCert.ps1 xxxxxx** ，其中 **xxxxxx** 是 SQL Server 執行個體的名稱。  

    -   指令碼完成後，請確認 SQL Server Agent 正在執行。 否則，請重新啟動 SQL Server Agent。  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>若要設定遠端管理點使用資料庫複本伺服器的自我簽署憑證  

1.  在資料庫複本伺服器上執行下列步驟將伺服器自我簽署憑證匯出：  

    1.  依序按一下 [開始] 與 [執行] ，然後輸入 **mmc.exe**。 在空白主控台中，按一下 [檔案] ，然後按一下 [新增/移除嵌入式管理單元] 。  

    2.  在 [新增或移除嵌入式管理單元]  對話方塊中，從 [可用的嵌入式管理單元]  清單中選取 [憑證] ，然後按一下 [新增] 。  

    3.  在 [憑證嵌入式管理單元]  對話方塊中，選取 [電腦帳戶] ，然後按 [下一步] 。  

    4.  在 [選取電腦]  對話方塊中，確定選取 [本機電腦: (執行這個主控台的電腦)]  ，然後按一下 [完成] 。  

    5.  在 [新增或移除嵌入式管理單元]  對話方塊中，按一下 [確定] 。  

    6.  在主控台中，依序展開 [憑證 (本機電腦)] 和 [個人] ，然後選取 [憑證] 。  

    7.  以滑鼠右鍵按一下易記名稱為 [ConfigMgr SQL Server Identification Certificate] 的憑證，按一下 [所有工作] ，然後選取 [匯出] 。  

    8.  使用預設選項完成 [憑證匯出精靈]  ，然後以 [.cer]  副檔名儲存憑證。  

2.  在管理點電腦上執行下列步驟，將資料庫複本伺服器的自我簽署憑證新增至管理點上的 [受信任的人] 憑證存放區。  

    1.  重複上述步驟 1.a 到 1.e， 在管理點電腦上設定**憑證**嵌入式MMC。  

    2.  在主控台中，依序展開 [憑證 (本機電腦)] 和 [受信任的人] ，以滑鼠右鍵按一下 [憑證] ，選取 [所有工作] ，然後選取 [匯入]  ，啟動 [憑證匯入精靈] 。  

    3.  在 [匯入檔案]  頁面上，選取步驟 1.h 中儲存的憑證，然後按 [下一步] 。  

    4.  在 [憑證存放區]  頁面上，選取 [將所有憑證放入以下的存放區] ，並將 [憑證存放區]  設為 [受信任的人] ，然後按 [下一步] 。  

    5.  按一下 [完成]  關閉精靈，並完成管理點上的憑證設定。  

###  <a name="BKMK_DBreplica_SSB"></a> 步驟 5 - 設定資料庫複本伺服器的 SQL Server Service Broker  
若要針對管理點支援資料複本的用戶端通知，您必須針對 SQL Server Service Broker 設定網站資料庫伺服器與資料庫複本伺服器之間的通訊。 您會需要設定每個資料庫中有關其他資料庫的資訊，以及在兩個資料庫之間交換憑證以進行安全通訊。  

> [!NOTE]  
>  資料庫複本伺服器必須先成功完成網站資料庫伺服器的初次同步處理，您才能使用下列程序。  

 下列程序不會修改 SQL Server 中設定用於網站資料庫伺服器，或資料庫複本伺服器的 Service Broker 連接埠。 此程序會設定每個資料庫使用正確的 Service Broker 連接埠與其他資料庫進行通訊。  

 利用下列程序設定網站資料庫伺服器和資料庫複本伺服器的 Service Broker。  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>若要設定資料庫複本的 Service Broker  

1.  使用 **SQL Server Management Studio** 連接至資料庫複本伺服器資料庫，然後執行下列查詢，啟用資料庫複本伺服器上的 Service Broker：**ALTER DATABASE &lt;複本資料庫名稱\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2.  接著在資料庫複本伺服器上，設定用戶端通知所使用的 Service Broker 並匯出 Service Broker 憑證。 若要執行這項操作，請執行以單一動作設定 Service Broker 並匯出憑證的 SQL Server 預存程序。 當您執行預存程序時，必須指定資料庫複本伺服器的 FQDN、資料庫複本資料庫的名稱，並指定匯出憑證檔案的位置。  

     執行下列查詢，以在資料庫複本伺服器上設定必要的詳細資料，並匯出資料庫複本伺服器的憑證：**EXEC sp_BgbConfigSSBForReplicaDB '&lt;複本 SQL Server FQDN\>', '&lt;複本資料庫名稱\>', '&lt;憑證備份檔案路徑\>'**  

    > [!NOTE]  
    >  如果資料庫複本伺服器不是位於預設 SQL Server 執行個體上，您在這個步驟除了指定複本資料庫名稱之外，還必須指定執行個體名稱。 若要執行這項操作，請將 **&lt;複本資料庫名稱\>** 取代為 **&lt;執行個體名稱\\複本資料庫名稱\>**。  

     從資料庫複本伺服器匯出憑證後，將憑證副本放至主網站資料庫伺服器上。  

3.  使用 [SQL Server Management Studio]  連接至主網站資料庫。 連接至主網站資料庫後，執行查詢匯入憑證，並指定資料庫複本伺服器上正在使用的 Service Broker 連接埠、資料庫複本伺服器的 FQDN，以及資料庫複本資料庫的名稱。 這樣就會將主網站資料庫設定為使用 Service Broker 與資料庫複本伺服器的資料庫進行通訊。  

     執行下列查詢，以從資料庫複本伺服器匯入憑證，並指定必要的詳細資料：**EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;SQL Service Broker 連接埠\>', '&lt;憑證檔案路徑\>', '&lt;複本 SQL Server FQDN\>', '&lt;複本資料庫名稱\>'**  

    > [!NOTE]  
    >  如果資料庫複本伺服器不是位於預設 SQL Server 執行個體上，您在這個步驟除了指定複本資料庫名稱之外，還必須指定執行個體名稱。 若要執行這項操作，請將 **&lt;複本資料庫名稱\>** 取代為 **\執行個體名稱\\複本資料庫名稱\>**。  

4.  接著，在站台資料庫伺服器上，執行下列命令，以匯出站台資料庫伺服器的憑證：**EXEC sp_BgbCreateAndBackupSQLCert '&lt;憑證備份檔案路徑\>'**  

     從網站資料庫伺服器匯出憑證後，將憑證副本放至資料庫複本伺服器上。  

5.  使用 [SQL Server Management Studio]  連接至資料庫複本伺服器資料庫。 連接至資料庫複本伺服器資料庫後，執行查詢匯入憑證，並指定主網站的網站碼及網站資料庫伺服器上正在使用的 Service Broker 連接埠。 這樣就會將資料庫複本伺服器設定為使用 Service Broker 與主網站的資料庫進行通訊。  

     執行下列查詢，以從站台資料庫伺服器匯入憑證：**EXEC sp_BgbConfigSSBForRemoteService '&lt;站台碼\>', '&lt;SQL Service Broker 連接埠\>', '&lt;憑證檔案路徑\>'**  

 完成網站資料庫及資料庫複本資料庫的設定後經過幾分鐘，主網站的通知管理員就會建立從主網站資料庫到資料庫複本的用戶端通知 Service Broker 交談。  

###  <a name="bkmk_supscript"></a> 單一的 SQL Server 上的其他資料庫複本補充指令碼  
 當您使用步驟 4 中的指令碼，設定 SQL Server (已有預計要繼續使用的資料庫複本) 上資料庫複本伺服器的自我簽署憑證時，必須使用經過修改的原始指令碼版本。 下列修改內容可避免指令碼刪除伺服器上現有的憑證，同時建立易記名稱不重複的後續憑證。  編輯原始的指令碼，如下所示：  

-   將指令碼項目 **# Delete existing cert if one exists** 與 **# Create the new cert**之間的指令碼項目，標為註解以避免執行。 若要執行此作業，請加入  **#**  作為適用的每一行之第一個字元。  

-   為每個使用此指令碼進行設定的後續資料庫複本，更新憑證的易記名稱。  若要執行此作業，請編輯行 **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** ，並以新名稱取代 **ConfigMgr SQL Server Identification Certificate** ，像是  **ConfigMgr SQL Server Identification Certificate1**。  

##  <a name="BKMK_DBReplicaOps"></a> 管理資料庫複本組態  
 當您在網站上使用資料庫複本時，請使用以下各節中的資訊以補充解除安裝資料庫複本、解除安裝使用資料庫複本的網站，或是將網站資料庫移至新的 SQL Server 安裝的程序。 當您利用下面各節的資訊刪除發佈時，請使用指引刪除用於資料庫複本之 SQL Server 版本的交易複寫。 例如，若您使用 SQL Server 2008 R2，請參閱 [如何：刪除發行集 (複寫 Transact-SQL 程式設計)](http://go.microsoft.com/fwlink/p/?LinkId=273934)。  

> [!NOTE]  
>  在您還原為資料庫複本設定的網站資料庫之後，必須先重新設定每個資料庫複本並重建發佈及訂閱，才能使用資料庫複本。  

###  <a name="BKMK_UninstallDbReplica"></a> 解除安裝資料庫複本  
 您針對管理點使用資料庫複本時，可能需要解除安裝資料庫複本一段時間，然後再重新設定它以供使用。 例如，將 Configuration Manager 站台升級為新的 Service Pack 之前，必須先移除資料庫複本。 網站升級完成後，您就可以還原資料庫複本以供使用。  

 利用下列步驟解除安裝資料庫複本。  

1.  在 Configuration Manager 主控台的 [系統管理] 工作區中，展開 [站台設定]，然後選取 [伺服器和站台系統角色]，接著在詳細資料窗格中選取站台系統伺服器，且該伺服器裝載的管理點使用您要解除安裝的資料庫複本。  

2.  在 [網站系統角色]  窗格中，用滑鼠右鍵按一下 [管理點]  並選取 [內容] 。  

3.  在 [管理點資料庫]  索引標籤上選取 [使用網站資料庫]  ，設定管理點使用網站資料庫而不是資料庫複本。 然後按一下 [確定]  儲存設定。  

4.  接著使用 [SQL Server Management Studio]  執行下列工作：  

    -   刪除網站伺服器資料庫上的資料庫複本發佈。  

    -   刪除資料庫複本伺服器上的資料庫複本訂閱。  

    -   刪除資料庫複本伺服器上的複本資料庫。  

    -   停用網站資料庫伺服器上的發行與散發。 若要停用發行與散發，請以滑鼠右鍵按一下 [複寫] 資料夾，然後按一下 [停用發行與散發] 。  

5.  在網站資料庫伺服器上刪除發佈、訂閱、複本資料庫及停用發佈後，資料庫複本便已解除安裝。  

###  <a name="BKMK_DBReplicaOps_Uninstall"></a> 解除安裝發佈資料庫複本的站台伺服器  
 解除安裝發佈資料庫複本的網站之前，請先利用下列步驟清除發佈及任何訂閱。  

1.  使用 [SQL Server Management Studio]  刪除網站伺服器資料庫中的資料庫複本發佈。  

2.  使用 [SQL Server Management Studio]  刪除裝載此網站所使用資料庫複本的每一部遠端 SQL Server 上的資料庫複本訂閱。  

3.  解除安裝網站。  

###  <a name="BKMK_DBReplicaOps_Move"></a> 移動發佈資料庫複本的站台伺服器資料庫  
 將網站資料庫移至新電腦時，請利用下列步驟：  

1.  使用 [SQL Server Management Studio]  刪除網站伺服器資料庫中的資料庫複本發佈。  

2.  使用 [SQL Server Management Studio]  刪除此網站上每部資料庫複本伺服器中的資料庫複本訂閱。  

3.  將資料庫移至新的 SQL Server 電腦。 如需詳細資訊，請參閱 [Modify the site database configuration](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) 主題中的 [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) 一節。  

4.  重建網站資料庫伺服器上的資料庫複本發佈。 如需詳細資訊，請參閱本主題的 [步驟 1 - 設定站台資料庫伺服器以發佈資料庫複本](#BKMK_DBReplica_ConfigSiteDB) 。  

5.  重建每一部資料庫複本伺服器上的資料庫複本訂閱。 如需詳細資訊，請參閱本主題的 [步驟 2 - 設定資料庫複本伺服器](#BKMK_DBReplica_ConfigSrv) 。  
