---
title: "Hotfix 安裝程式 | Microsoft Docs"
description: "了解何時及如何透過 Hotfix 安裝程式安裝 Configuration Manager 更新。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8ffc7383e895909e6e6c4b8a7875fd5f0df2220e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-hotfix-installer-to-install-updates-for-system-center-configuration-manager"></a>使用 Hotfix 安裝程式來安裝 System Center Configuration Manager 更新

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 的某些更新無法從 Microsoft 雲端服務取得，只能從頻外取得。 用以解決特定問題的有限版本 Hotfix 就是一例。   
當您必須安裝您由 Microsoft 接收的更新 (或 Hotfix)，且該更新具有一個以副檔名 **.exe** (而非 **update.exe**) 結尾的檔案名稱時，您使用包含在該 Hotfix 下載項目中的 Hotfix 安裝程式，直接將該更新安裝至 Configuration Manager 站台伺服器。  

 如果 Hotfix 檔案具有 **.update.exe** 副檔名，請參閱[使用更新註冊工具將 Hotfix 匯入 System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)。  

> [!NOTE]  
>  本主題提供有關如何安裝可更新 System Center Configuration Manager 之 Hofix 的一般指引。 如需特定更新的詳細資訊，請參閱 Microsoft 支援服務提供的對應知識庫 (KB) 文章內容。  

##  <a name="bkmk_Overview"></a> Configuration Manager 的 Hotfix 概觀  
 Configuration Manager 的 Hotfix 類似於其他 Microsoft 產品 (例如 SQL Server) 的 Hotfix，包含了一個個別修正或配套 (修正彙總套件)，且在 Microsoft 知識庫文件有說明。  

 個別更新包含特定 Configuration Manager 版本的單一聚焦更新。  
更新配套包含特定 Configuration Manager 版本的多個更新。  
當更新為配套時，您無法安裝該配套的個別更新。  

 如果您規劃建立部署以在其他電腦上安裝更新，則必須在管理中心網站伺服器或主要站台上安裝更新配套。  

 執行更新配套時，會發生下列情況：  

-   它會從更新配套擷取每個適用元件的更新檔案。  

-   啟動精靈，引導您完成更新及其部署選項的設定程序。  

-   當您完成精靈之後，適用於站台伺服器的更新配套會安裝在站台伺服器上。  

精靈也會建立可用於在其他電腦上安裝更新的部署。 您可以透過支援的部署方法，將更新部署到其他電腦，例如透過軟體部署封裝或 Microsoft System Center Updates Publisher 2011。  

 當執行精靈時，它會在站台伺服器上建立要與 Updates Publisher 2011 搭配使用的 **.cab** 檔。 您也可以選擇設定精靈，同時為軟體部署建立一個或多個封裝。 您可以使用這些部署在元件 (例如用戶端或 Configuration Manager 主控台) 上安裝更新。 您也可在未執行 Configuration Manager 用戶端的電腦上手動安裝更新。  

 Configuration Manager 中的下列三個群組可進行更新：  

-   Configuration Manager 伺服器角色，其包括：  

    -   管理中心網站  

    -   主要網站  

    -   次要網站  

    -   遠端 SMS 提供者  

-   Configuration Manager 主控台  

-   Configuration Manager 用戶端  

> [!NOTE]  
>  **站台系統角色更新** (包括站台資料庫和雲端發佈點的更新) 會由站台元件管理員作為站台伺服器和服務的一部分進行安裝。  
>   
>  不過，更新提取發佈點是由發佈管理員提供，而非站台元件管理員。  

 Configuration Manager 的每個更新配套都是可自我解壓縮 .exe 檔案 (SFX)，其包含在 Configuration Manager 適用元件上安裝更新時所必需的檔案。 通常，SFX 檔案可能包含以下檔案：  

|檔案|詳細資料|  
|----------|-------------|  
|&lt;產品版本\>-QFE-KB&lt;知識庫文章識別碼\>-&lt;平台\>-&lt;語言\>.exe|這是更新檔。 此檔案的命令列由 Updatesetup.exe 管理。<br /><br /> 例如：<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|這個 .msi 包裝函式會管理更新配套的安裝。<br /><br /> 當您執行更新程式時，Updatesetup.exe 會偵測電腦執行時所顯示的語言。 根據預設，更新程式的使用者介面是英文版。 不過，如果顯示語言是受支援的語言，電腦使用者介面便會顯示本機語言。|  
|License_&lt;語言\>.rtf|若適用，每個更新都會包含一個或多個受支援語言所適用的授權檔案。|  
|&lt;產品&updatetype>-&lt;產品版本\>-&lt;知識庫文章識別碼\>-&lt;平台\>.msp|將更新套用至 Configuration Manager 主控台或用戶端時，更新配套會包含個別 Windows Installer 修補 (.msp) 檔案。<br /><br /> 例如：<br /><br /> **Configuration Manager 主控台更新：** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **用戶端更新：**ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

 根據預設，更新配套會將其動作記錄到站台伺服器的 .log 檔案。 記錄檔具有和更新配套相同的名稱，且會寫入 **%SystemRoot%/Temp** 資料夾中。  

 當您執行更新組合時，它會將與更新組合同名的檔案解壓縮到電腦的暫存資料夾，然後再執行 Updatesetup.exe。 Updatesetup.exe 會啟動 [Configuration Manager &lt;產品版本\> &lt;知識庫號碼\> 軟體更新精靈]。  

 適用的更新範圍內，精靈會在站台伺服器上的 System Center Configuration Manager 安裝資料夾下建立一系列的資料夾。 資料夾結構如下所示：   
 **\\\\&lt;伺服器名稱\>\SMS_&lt;站台碼\>\Hotfix\\&lt;知識庫號碼\>\\&lt;更新類型\>\\&lt;平台\>**。  

 下表提供有關資料夾結構中資料夾的詳細資料：  

|資料夾名稱|詳細資訊|  
|-----------------|----------------------|  
|&lt;伺服器名稱\>|這是您執行更新配套所在之站台伺服器的名稱。|  
|SMS_&lt;站台碼\>|這是 Configuration Manager 安裝資料夾的共用名稱。|  
|&lt;知識庫號碼\>|這是此更新配套適用之知識庫文章的識別碼。|  
|&lt;更新類型\>|這些是 Configuration Manager 的更新類型。 精靈會為更新配套中所包含之每一種更新類型，建立個別資料夾。 資料夾名稱代表更新類型。 其包括：<br /><br /> **伺服器**：包括執行 SMS 提供者之站台伺服器、站台資料庫伺服器及電腦的更新。<br /><br /> **用戶端**：包括對 Configuration Manager 用戶端的更新。<br /><br /> **AdminConsole**：包括對 Configuration Manager 主控台的更新<br /><br /> 除了之前的更新類型以外，精靈會建立一個名為 **SCUP**的資料夾。 此資料夾不代表更新類型，而是包含了更新發行者的 .cab 檔。|  
|&lt;平台\>|這是平台特定的資料夾。 該資料夾中包含特定於某種處理器類型的更新檔案。  這些資料夾包括：<br /><br />- x64<br /><br /> - I386|  

##  <a name="bkmk_Install"></a> 如何安裝更新  
 若要安裝更新，您必須先在站台伺服器上安裝更新配套。 當您安裝更新配套時，便會啟動該更新的安裝精靈。 此精靈會執行下列動作：  

-   解壓縮更新檔案  

-   協助您設定部署  

-   在本機電腦的伺服器元件上安裝適用的更新  

在站台伺服器上安裝更新配套後，您可以接著更新 Configuration Manager 的其他元件。 下表說明對這些不同元件的更新動作：  

|元件|指示|  
|---------------|------------------|  
|網站伺服器|當您未選擇將更新配套直接安裝在遠端站台伺服器時，可將更新部署到該遠端站台伺服器。|  
|網站資料庫|對於遠端站台伺服器，如果您未將更新配套直接安裝在遠端站台伺服器，便可將包含更新的伺服器更新部署到站台資料庫。|  
|Configuration Manager 主控台|初始安裝 Configuration Manager 主控台後，您可以在執行主控台的每部電腦上為 Configuration Manager 主控台安裝更新。 在初始安裝主控台期間，您無法修改 Configuration Manager 主控台安裝檔案以套用更新。|  
|遠端 SMS 提供者|為每一個執行於電腦而不是您安裝更新配套所在之站台伺服器的 SMS Provider 執行個體，安裝更新。|  
|Configuration Manager 用戶端|初始安裝 Configuration Manager 用戶端後，您可以在執行用戶端的每部電腦上為 Configuration Manager 用戶端安裝更新。|  

> [!NOTE]  
>  您只能將更新部署到執行 Configuration Manager 用戶端的電腦上手動安裝更新。  

 如果您重新安裝用戶端、Configuration Manager 主控台或 SMS 提供者，則也必須重新安裝這些元件的更新。  

 使用以下各節資訊，在 Configuration Manager 的每一個元件上安裝更新。  

###  <a name="bkmk_servers"></a> 更新伺服器  
 伺服器的更新，可包含適用於 **站台**、 **site database**以及執行 **SMS 提供者**之執行個體電腦的更新：  

####  <a name="bkmk_site"></a> 更新站台  
 若要更新 Configuration Manager 站台，您可以將更新配套直接安裝在站台伺服器上，也可在將更新配套安裝到不同站台後，將更新部署到站台伺服器。  

 當您將更新安裝在站台伺服器上時，更新安裝程序會管理用以套用更新 (例如更新站台系統角色) 的其他必要動作。 唯一的例外是站台資料庫。 下一節內容包含有關如何更新站台資料庫的資訊。  

####  <a name="bkmk_database"></a> 更新站台資料庫  
 若要更新站台資料庫，安裝程序會在站台資料庫執行一支名為 **update.sql** 的檔案。 您可以將更新程序設定為可自動更新站台資料庫，或可稍後手動更新站台資料庫。  

 **自動更新站台資料庫**  

 在站台伺服器上安裝更新配套時，您可以選擇在安裝伺服器更新時，自動更新站台資料庫。 這個決定僅適用於安裝更新配套所在的站台伺服器，不適用於為了在遠端站台伺服器安裝更新而建立的部署。  

> [!NOTE]  
>  當您選擇自動更新站台資料庫時，無論資料庫是位於站台伺服器或在遠端電腦上，該程序都會更新資料庫。  

> [!IMPORTANT]  
>  在更新站台資料庫之前，可建立站台資料庫的備份。 您無法解除安裝對站台資料庫的更新。 如需如何建立 Configuration Manager 備份的相關資訊，請參閱 [System Center Configuration Manager 備份和復原](../../../protect/understand/backup-and-recovery.md)。  

 **手動更新站台資料庫**  

 如果您選擇在站台伺服器上安裝更新配套時不自動更新站台資料庫，伺服器更新就不會在執行更新配套的站台伺服器上修改資料庫。 然而，使用為軟體部署而建立之套件或所安裝之套件的部署，永遠會更新站台資料庫。  

> [!WARNING]  
>  當更新作業將更新程式納入站台伺服器和站台資料庫時，直到站台伺服器和站台資料庫完成更新後，更新才能正常運作。 在將更新套用到站台資料庫之前，該站台都處於不受支援狀態。  

 **手動更新站台資料庫：**  

1.  請在站台伺服器上，依序停止 SMS_SITE_COMPONENT_MANAGER 服務和 SMS_EXECUTIVE 服務。  

2.  關閉 Configuration Manager 主控台。  

3.  在該站台的資料庫上執行名為 **update.sql** 的更新指令碼。 如需如何執行指令碼以更新 SQL Server 資料庫的相關資訊，請參閱用於站台資料庫伺服器之 SQL Server 版本的文件。  

4.  重新啟動在先前步驟中已停止的服務。  

5.  安裝更新配套時，它會將 **update.sql** 擷取到站台伺服器的下列位置：**\\\\&lt;伺服器名稱\>\SMS_&lt;站台碼\>\Hotfix\\&lt;知識庫號碼\>\update.sql**  

####  <a name="bkmk_provider"></a> 更新執行 SMS 提供者的電腦  
 安裝包含 SMS 提供者更新的更新配套後，必須將更新部署至每台執行 SMS 提供者的電腦。 唯一的例外是先前安裝在站台伺服器 (用來安裝更新配套) 上的 SMS 提供者執行個體。 站台伺服器上的本機 SMS 提供者執行個體會在您安裝更新配套時更新。  

 如果移除電腦上的 SMS 提供者之後再重新安裝，則必須在該電腦上重新安裝 SMS 提供者更新。  

###  <a name="BKMK_clients"></a> 更新用戶端  
 當您安裝包含 Configuration Manager 用戶端更新的更新時，會提供您使用更新安裝自動升級用戶端的選項，或者稍後手動升級用戶端。 如需用戶端自動升級的詳細資訊，請參閱 [如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](https://technet.microsoft.com/library/mt627885.aspx)之 Hotfix 的一般指引。  

 您可以使用更新發行者或軟體部署套件來部署更新，也可選擇在每個用戶端上手動安裝更新。 如需如何使用部署安裝更新的詳細資訊，請參閱本主題中的 [部署 Configuration Manager 的更新](#BKMK_Deploy) 一節。  

> [!IMPORTANT]  
>  安裝用戶端更新且更新配套包含伺服器更新時，請務必同時在接受用戶端指派的主要站台上安裝伺服器更新。  

若要手動安裝用戶端更新，您必須在每個 Configuration Manager 用戶端上執行 **Msiexec.exe**，並且參照特定平台的用戶端更新 .msp 檔案。  

 例如，您可以使用下列命令列更新用戶端。 這個命令列會在用戶端電腦上執行 MSIEXEC，並且參照更新組合在站台伺服器上解壓縮的 .msp 檔：**msiexec.exe /p \\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;知識庫號碼\>\Client\\&lt;平台\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="BKMK_console"></a> 更新 Configuration Manager 主控台  
 若要更新 Configuration Manager 主控台，您必須在主控台安裝完成後，在執行主控台的電腦上安裝更新。  

> [!IMPORTANT]  
>  如果您安裝 Configuration Manager 主控台的更新，並且更新配套包含伺服器更新，請務必同時在使用 Configuration Manager 主控台的站台上安裝伺服器更新。  

如果您更新的電腦執行 Configuration Manager 用戶端：  

-   您可以使用部署來安裝更新。 如需如何使用部署安裝更新的詳細資訊，請參閱本主題中的 [部署 Configuration Manager 的更新](#BKMK_Deploy) 一節。  

-   如果您直接登入用戶端電腦，則可以互動方式執行安裝。  

-   您可以在每部電腦上手動安裝更新。 若要手動安裝 Configuration Manager 主控台更新，您必須在每部執行 Configuration Manager 主控台的電腦上執行 Msiexec.exe，並參照 Configuration Manager 主控台更新 .msp 檔案。  

例如，您可以使用下列命令列更新 Configuration Manager 主控台。 這個命令列會在電腦上執行 MSIEXEC，並且參照更新組合在站台伺服器上解壓縮的 .msp 檔：**msiexec.exe /p \\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;知識庫號碼\>\AdminConsole\\&lt;平台\>\\&lt;msp\> /L\*v &lt;logfile\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="BKMK_Deploy"></a> 部署 Configuration Manager 的更新  
 當您在站台伺服器上安裝更新配套後，可以使用下列三種方法之一，將更新部署至其他電腦。  

###  <a name="BKMK_DeploySCUP"></a> 使用 Updates Publisher 2011 安裝更新  
 當您在站台伺服器上安裝更新配套時，安裝精靈會針對「更新發行者」建立類別目錄檔案，您可以用來將更新部署至適用的電腦。 精靈一律會建立此類別目錄，即使您選取 **[Use package and program to deploy this update (使用套件和程式部署此更新)]**之 Hotfix 的一般指引。  

 Updates Publisher 的類別目錄名稱為 **SCUPCatalog.cab**，且可在執行更新配套的電腦的下列位置找到：**\\\\&lt;ServerName\>\SMS_&lt;SiteCode\>\Hotfix\\&lt;知識庫號碼\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
>  由於 SCUPCatalog.cab 檔案是利用站台伺服器專用的更新配套安裝路徑建立的，因此不能在其他站台伺服器上使用。  

 完成精靈之後，可以將類別目錄匯入 Updates Publisher，然後使用 Configuration Manager 軟體更新來部署更新。 如需 Updates Publisher 的相關資訊，請參閱 System Center 2012 TechNet 文件庫中的 [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkID=83449)。  

 請使用下列程序將 SCUPCatalog.cab 檔案匯入更新發行者並發行更新。  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>將更新匯入至發行者 2011  

1.  啟動 Updates Publisher 主控台，然後按一下 [匯入]。  

2.  在匯入軟體更新類別目錄精靈的 [匯入類型]  頁面中，選取 [指定欲匯入之類別目錄的路徑] ，然後指定 SCUPCatalog.cab 檔案。  

3.  按 [下一步] ，然後再次按 [下一步]  。  

4.  在 [安全性警告 - 目錄驗證]  對話方塊中，按一下 [接受] 。 完成後關閉精靈。  

5.  在 Updates Publisher 主控台中，選取您要部署的更新，然後按一下 [發行]。  

6.  在發行軟體更新精靈的 [發行選項]  頁面中，選取 [完整內容] 再按 [下一步] 。  

7.  完成精靈以發行更新。  

###  <a name="BKMK_DeploySWDist"></a> 使用軟體部署安裝更新  
 當您在主要站台或管理中心網站的站台伺服器上安裝更新配套時，您可以設定安裝精靈來建立軟體部署的更新套件。 接著您可以將每個套件部署至欲更新的電腦集合。  

 若要建立軟體部署套件，請在精靈的 [設定軟體更新部署]  頁面中，選取欲更新之每種更新套件類型旁的核取方塊。 可用類型可以包含伺服器、Configuration Manager 主控台和用戶端。 您每選取一種更新類型，都會為該類型建立一個獨立套件。  

> [!NOTE]  
>  伺服器套件包含下列元件的更新：  
>   
>  -   網站伺服器  
>  -   SMS 提供者  
>  -   網站資料庫  

 接下來，在精靈的 [設定軟體更新部署方法]  頁面中，選取 [我將使用軟體發佈] 選項。 此選項會引導精靈建立軟體部署套件。  

 精靈結束後，您可以在 [軟體程式庫] 工作區之 [套件] 節點上的 Configuration Manager 主控台中檢視精靈所建立的套件。 接著，您可以使用標準程序將軟體套件部署至 Configuration Manager 用戶端。 套件在用戶端上執行時，會將更新安裝至用戶端電腦上可用的 Configuration Manager 元件。  

 如需如何將套件部署至 Configuration Manager 用戶端的相關資訊，請參閱 [System Center Configuration Manager 中的套件和程式](../../../apps/deploy-use/packages-and-programs.md)。  

###  <a name="BKMK_DeployCollections"></a> 建立用於將更新部署到 Configuration Manager 的集合  
 您可以將特定更新部署至可用的用戶端。 下列資訊可協助您為 Configuration Manager 的不同元件建立裝置集合。  

|Configuration Manager 的元件|指示|  
|----------------------------------------|------------------|  
|管理中心網站伺服器|建立直接成員資格查詢，並且新增管理中心網站伺服器電腦。|  
|所有主要站台伺服器|建立直接成員資格查詢，並且新增每台主要站台伺服器電腦。|  
|所有次要站台伺服器|建立直接成員資格查詢，並且新增每台次要站台伺服器電腦。|  
|所有 x 86 用戶端|使用下列查詢準則建立集合：<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"**|  
|所有 x64 用戶端|使用下列查詢準則建立集合：<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"**|  
|所有執行 Configuration Manager 主控台的電腦|建立直接成員資格查詢，並且新增每台電腦。|  
|執行 SMS 提供者執行個體的遠端電腦|建立直接成員資格查詢，並且新增每台電腦。|  

> [!NOTE]  
>  若要更新站台資料庫，請將更新部署至該站台的站台伺服器。  

 如需如何建立集合的資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../core/clients/manage/collections/create-collections.md)。  
