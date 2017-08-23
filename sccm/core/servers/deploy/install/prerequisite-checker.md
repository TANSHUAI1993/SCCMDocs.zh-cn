---
title: "必要條件檢查工具 | Microsoft Docs"
description: "了解如何使用必要條件檢查工具，識別並修正可能封鎖站台或站台系統角色安裝的問題。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f0d44f82a0b6068f8cecc5808774677eccb0f8d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>System Center Configuration Manager 的必要條件檢查工具

*適用對象：System Center Configuration Manager (最新分支)*

 在執行安裝程式來安裝或升級 System Center Configuration Manager 站台前，或在新的伺服器上安裝站台系統角色前，您可以使用要用來確認伺服器整備程度之 Configuration Manager 版本中的這個獨立應用程式 (**Prereqchk.exe**)。 使用必要條件檢查工具，識別並修正可能封鎖站台或站台系統角色安裝的問題。  

> [!NOTE]  
>  在執行安裝程序期間，一律會執行必要條件檢查工具。  

根據預設，在必要條件檢查工具執行時：  

-   它會驗證其執行所在的伺服器。  
-   系統會掃描本機電腦，檢查是否有現有的站台伺服器，並只會執行適用於站台的檢查。  
-   如果未偵測到現有網站，則會執行所有必要條件規則。  
-   它會檢查規則，以確認安裝程序所需的軟體及設定都已安裝。 不過，必要軟體可能會需要未經必要條件檢查工具驗證的額外設定或軟體更新。  
-   因此，它會將其結果記錄在電腦系統磁碟機上的 **ConfigMgrPrereq.log** 檔案中。 記錄檔可能包含未出現在應用程式介面中的其他資訊。  

當您在命令提示字元中執行必要條件檢查工具，並指定特定的命令列選項時：  

-   必要條件檢查工具只會針對您在命令列中指定的站台伺服器或是站台系統，執行相關聯的檢查。  
-   若要檢查遠端電腦，您的使用者帳戶必須具有足以移除電腦的 [系統管理員] 權限。  

如需必要條件檢查工具所執行的檢查詳細資訊，請參閱 [System Center Configuration Manager 的必要條件檢查清單](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)。  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>將必要條件檢查工具複製到另一部電腦  

1.  在 Windows 檔案總管中，前往下列其中一個位置：  

    -   &lt;Configuration Manager 安裝媒體\>\SMSSETUP\BIN\X64  
    -   &lt;Configuration Manager 安裝路徑\>\BIN\X64  

2.  將下列檔案複製到另一部電腦的目的地資料夾：  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>利用預設檢查來執行必要條件檢查工具  

1.  在 Windows 檔案總管中，前往下列其中一個位置：  

    -   &lt;Configuration Manager 安裝媒體\>\SMSSETUP\BIN\X64  
    -   **&lt;Configuration Manager 安裝路徑**\>\BIN\X64**  

2.  執行 **prereqchk.exe** ，以啟動必要條件檢查程式。   
    必要條件檢查工具會偵測現有網站，如果找到的話，會執行升級整備程度檢查。 如果未找到網站，則會執行所有檢查。 [網站類型]  欄提供與規則相關聯的網站伺服器或網站系統資訊。  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>針對所有預設檢查，從命令提示字元執行必要條件檢查工具  

1.  開啟 [命令提示字元] 視窗，並將目錄變更為下列其中一個位置：  

    -   **&lt;Configuration Manager 安裝媒體**\>\SMSSETUP\BIN\X64**  
    -   **&lt;Configuration Manager 安裝路徑**\>\BIN\X64**  

2.  輸入  **prereqchk.exe /LOCAL** 以啟動必要條件檢查程式，並在伺服器上執行所有必要條件檢查。  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>從命令提示字元執行必要條件檢查工具以使用選項  

1.  開啟 [命令提示字元] 視窗，並將目錄變更為下列其中一個位置：  

    -   **&lt;Configuration Manager 安裝媒體**\>\SMSSETUP\BIN\X64**  
    -   **&lt;Configuration Manager 安裝路徑**\>\BIN\X64**  

2.  輸入 **prereqchk.exe**，並加上一個或多個下列命令列選項。  

    例如，若要檢查主要站台，您可能會使用下列項目：  

       **prereqchk.exe [/NOUI] /PRI /SQL &lt;SQL Server 的 FQDN\> /SDK &lt;SMS 提供者的 FQDN\> [/JOIN &lt;管理中心網站的 FQDN\>] [/MP &lt;管理點的 FQDN\>] [/DP &lt;發佈點的 FQDN\>]**  

    **管理中心網站伺服器：**  

    -   **/NOUI**  

         不需要。 啟動必要條件檢查工具，但不顯示使用者介面。 在命令列中指定任何其他選項之前，必須先指定此選項。  

    -   **/CAS**  

         必要。 確認本機電腦符合管理中心網站的需求。  

    -   **/SQL &lt;*SQL Server 的 FQDN*>**  

         必要。 使用完整網域名稱 (FQDN)；可確認指定的電腦符合讓 SQL Server 裝載 Configuration Manager 站台資料庫的需求。  

    -   **/SDK &lt;*SMS 提供者的 FQDN*>**  

         必要。 確認指定的電腦符合 SMS 提供者的需求。  

    -   **/Ssbport**  

         不需要。 確認防火牆例外狀況有效，可允許 SQL Server Service Broker (SSB) 連接埠上的通訊。 預設 SSB 連接埠為 4022。  

    -   **InstallDir &lt;Configuration Manager 安裝路徑>****  

         不需要。 確認符合站台安裝的最小磁碟空間需求。  

    **主要站台伺服器：**  

    -   **/NOUI**  

        不需要。 啟動必要條件檢查工具，但不顯示使用者介面。 在命令列中指定任何其他選項之前，必須先指定此選項。  

    -   **/PRI**  

         必要。 確認本機電腦符合主要網站的需求。  

    -   **/SQL &lt;*SQL Server 的 FQDN*>**  

         必要。 確認指定的電腦符合讓 SQL Server 裝載 Configuration Manager 站台資料庫的需求。  

    -   **/SDK &lt;*SMS 提供者的 FQDN*>**  

         必要。 確認指定的電腦符合 SMS 提供者的需求。  

    -   **/JOIN &lt;*管理中心網站的 FQDN*>**  

         不需要。 確認本機電腦符合連線至管理中心網站伺服器的需求。  

    -   **/MP &lt;*管理點的 FQDN*>**  

         不需要。 確認指定的電腦符合管理點網站系統角色的需求。 此選項只有在您使用 **/PRI** 選項時才受支援。  

    -   **/DP &lt;*發佈點的 FQDN*>**  

         不需要。 確認指定的電腦符合發佈點網站系統角色的需求。 此選項只有在您使用 **/PRI** 選項時才受支援。  

    -   **/Ssbport**  

         不需要。 確認防火牆例外狀況有效，可允許 SSB 連接埠上的通訊。 預設 SSB 連接埠為 4022。  

    -   **InstallDir &lt;Configuration Manager 安裝路徑>****  

         不需要。 確認符合站台安裝的最小磁碟空間需求。  

    **次要站台伺服器：**  

    -   **/NOUI**  

         不需要。 啟動必要條件檢查工具，但不顯示使用者介面。 在命令列中指定任何其他選項之前，必須先指定此選項。  

    -   **/SEC &lt;*次要站台伺服器的 FQDN*>**  

         必要。 確認指定的電腦符合次要網站的需求。  

    -   **/INSTALLSQLEXPRESS**  

         不需要。 確認可在指定的電腦上安裝 SQL Server Express。  

    -   **/Ssbport**  

         不需要。 確認防火牆例外狀況有效，可允許 SSB 連接埠的通訊。 預設 SSB 連接埠為 4022。  

    -   **/Sqlport**  

         不需要。 確認防火牆例外狀況有效，可允許 SQL Server 服務連接埠的通訊，而且沒有其他具名 SQL Server 執行個體正在使用該連接埠。 預設的連接埠為 1433。  

    -   **InstallDir &lt;Configuration Manager 安裝路徑>****  

         不需要。 確認符合站台安裝的最小磁碟空間需求。  

    -   **/SourceDir**  

         不需要。 確認次要網站的電腦帳戶可以存取裝載安裝程式來源檔案的資料夾。  

   **Configuration Manager 主控台：**  

    -   **/Adminui**  

         必要。 確認本機電腦符合 Configuration Manager 的安裝需求。  

3.  在必要條件檢查工具的使用者介面中，必要條件檢查工具會在 [必要條件結果] 區段中，建立一份找到的問題清單。  

    -   按一下清單中的項目，即可顯示有關如何解決問題的詳細資料。  
    -   您必須在安裝站台伺服器、站台系統或 Configuration Manager 主控台之前，解決清單中所有含 [錯誤] 狀態的項目。  
    -   您也可以在系統磁碟機的根目錄中開啟 **ConfigMgrPrereq.log** 檔案，以檢閱必要條件檢查工具的結果。 記錄檔可能包含未在必要條件檢查工具使用者介面中顯示的其他資訊。  
