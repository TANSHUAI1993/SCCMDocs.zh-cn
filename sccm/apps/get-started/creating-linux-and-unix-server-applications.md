---
title: "建立 Linux 和 UNIX 伺服器應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Linux 和 Unix 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 04/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72ebd8bd29b5ecdd817631e447291c04f49d9808
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-linux-and-unix-server-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Linux 和 UNIX 伺服器應用程式

*適用於：System Center Configuration Manager (最新分支)*

當您針對執行 Linux 和 Unix 的電腦建立和部署應用程式時，請納入下列考量。  

## <a name="general-considerations"></a>一般考量  
 Linux 和 UNIX 的 Configuration Manager 用戶端支援使用套件和程式進行軟體部署。 您可以將 Configuration Manager 應用程式部署至執行 Linux 和 UNIX 的電腦。  

 Linux 和 UNIX 軟體部署的功能包括：  

-   適用於 Linux 和 UNIX 伺服器的軟體安裝，包括下列各項：  

    -   新軟體部署  

    -   已存在於電腦上的程式軟體更新  

    -   作業系統修補程式  

-   原生 Linux 和 UNIX 命令，以及位於 Linux 和 UNIX 伺服器的指令碼  

-   僅限於您在選取 [僅在指定的用戶端平台上] 程式選項時所指定作業系統的部署

-   可控制軟體安裝時機的維護期間

-   可監視部署的部署狀態訊息  

-   用戶端從發佈點下載軟體時，用來節流處理網路使用量的選項  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>部署到 Linux 和 UNIX 電腦以及部署到 Windows 裝置之間的差異
將套件和程式部署到 Linux 和 UNIX 電腦，以及將套件和程式部署到 Windows 裝置之間的主要差異如下：  

|設定|詳細資料|  
|-------------------|-------------|  
|只使用適用於電腦的設定，請勿使用適用於使用者的設定。|Linux 和 UNIX 的 Configuration Manager 用戶端不支援適用於使用者的設定。|  
|將程式設定為從發佈點下載軟體，以及從本機用戶端快取執行程式。|Linux 和 UNIX 的 Configuration Manager 用戶端不支援從發佈點執行軟體。 您必須將設定改為將軟體下載至用戶端再進行安裝。<br /><br /> 根據預設，當 Linux 和 UNIX 的用戶端安裝軟體後，便會從用戶端的快取刪除該軟體。 不過，使用 [將內容保存在用戶端快取中]  設定的套件在軟體安裝後不會從用戶端刪除，並且會保留在用戶端的快取中。<br /><br /> Linux 和 UNIX 的用戶端不支援設定用戶端快取，而用戶端快取的大小上限只受限於用戶端電腦上的可用磁碟空間。|  
|設定供發佈點存取的網路存取帳戶|Linux 和 UNIX 電腦是針對工作群組電腦所設計。 若要從 Configuration Manager 站台伺服器網域的發佈點中存取套件，您必須設定站台的網路存取帳戶。 您必須先將此帳戶指定為軟體發佈元件內容並設定帳戶，才能部署軟體。<br /><br /> 您可以在每一網站設定多個網路存取帳戶。 Linux 和 UNIX 的用戶端可使用每一個設定為「網路存取帳戶」的帳戶。<br /><br /> 如需詳細資訊，請參閱 [Site components for System Center Configuration Manager](../../core/servers/deploy/configure/site-components.md)。|  

 您可以將套件和程式部署至只含 Linux 或 UNIX 用戶端的集合，或者將套件和程式部署至內含不同用戶端類型的集合，例如 [所有系統集合] 。 不過，非 Linux 或非 UNIX 用戶端將不會安裝軟體或報告失敗。  

 當 Linux 和 UNIX 的 Configuration Manager 用戶端接收及執行部署時，會產生狀態訊息。 您可以在 Configuration Manager 主控台中檢視這些狀態訊息，或使用報告監視部署狀態。  

 如需如何使用套件和程式的相關資訊，請參閱[套件和程式](../../apps/deploy-use/packages-and-programs.md)。  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>設定 Linux 和 UNIX 伺服器的套件、程式和部署  
 您可以使用 Configuration Manager 主控台中可用的預設選項，來建立及部署套件和程式。 用戶端不需要唯一的設定。  

 請使用下列各節所提供的資訊來設定套件和程式，以及設定部署。  

### <a name="packages-and-programs"></a>封裝和程式  
 若要建立 Linux 或 UNIX 伺服器的套件和程式，請從 Configuration Manager 主控台使用 [建立套件和程式精靈]。 Linux 和 UNIX 的用戶端支援大部份的套件和程式設定。 但是，並不支援數項設定。 當您建立或設定套件和程式時，請考慮下列各項：  

-   包含目的地電腦所支援的檔案類型。  

-   定義目的地電腦適用的命令列。  

-   請記住，不支援與使用者互動的設定。  

下表列出不支援的套件和程式內容：  

|套件和程式內容|行為|詳細資訊|  
|----------------------------------|--------------|----------------------|  
|套件共用設定：<br /><br /> - 所有選項|產生錯誤且軟體安裝失敗|用戶端不支援這項設定。 用戶端必須改為使用 HTTP 或 HTTPS 下載軟體，然後從其本機快取執行命命列。|  
|套件更新設定：<br /><br /> - 中斷使用者與發佈點的連線|忽略設定|用戶端不支援這項設定。|  
|作業系統部署設定：<br /><br /> - 所有選項|忽略設定|用戶端不支援這項設定。|  
|報告：<br /><br /> - 使用套件內容進行狀態 MIF 比對<br /><br /> - 使用這些欄位進行狀態 MIF 比對|忽略設定|用戶端不支援使用狀態 MIF 檔案。|  
|**執行**：<br /><br /> - 所有選項|忽略設定|用戶端永遠會執行沒有使用者介面的套件。<br /><br /> 用戶端會忽略 [執行] 的所有設定選項。|  
|執行之後：<br /><br />- Configuration Manager 會重新啟動電腦<br /><br /> - 程式控制重新啟動<br /><br /> - Configuration Manager 會將使用者登出|產生錯誤且軟體安裝失敗|不支援系統重新啟動設定及使用者特定的設定。<br /><br /> 使用 [不需要任何動作]  設定以外的其他設定時，用戶端會產生錯誤，並繼續進行軟體安裝，不會採取任何動作。|  
|程式可執行：<br /><br /> - 只有在使用者登入時|產生錯誤且軟體安裝失敗|不支援使用者特定的設定。<br /><br /> 設定此選項時，用戶端會產生錯誤，且軟體安裝失敗。<br /><br /> 此時會忽略其他選項，並繼續軟體安裝。|  
|執行模式：<br /><br /> - 以使用者的權限執行|忽略設定|不支援使用者特定的設定。<br /><br /> 不過，用戶端支援以系統管理權限執行的設定。<br /><br /> 當您指定 [以系統管理權限執行] 時，Configuration Manager 用戶端會使用其根認證。<br /><br /> 此設定不會產生錯誤或記錄檔項目。 不過，當用戶端產生 [程式可執行] = [只有在使用者登入時] 的必要條件設定錯誤時，軟體安裝會失敗。|  
|允許使用者檢視程式安裝，並與其互動|忽略設定|不支援使用者特定的設定。<br /><br /> 此時會忽略此設定，並繼續軟體安裝。|  
|磁碟機模式：<br /><br /> - 所有選項|忽略設定|由於內容永遠會下載到用戶端並於本機執行，因此不支援此設定。|  
|先執行其他程式|產生錯誤且軟體安裝失敗|不支援遞迴程式安裝。<br /><br /> 當程式設定為先執行其他程式時，軟體安裝會失敗，且不會啟動其他程式安裝。|  
|當此程式指派給電腦時：<br /><br /> - 針對登入的每個使用者執行一次|忽略設定|不支援使用者特定的設定。<br /><br /> 不過，用戶端支援針對電腦執行一次的設定。<br /><br /> 此設定不會產生錯誤或記錄檔項目，因為已針對 [程式可執行]  = **只有在使用者登入時**。|  
|抑制程式通知|忽略設定|用戶端尚未實作使用者介面。<br /><br /> 選取此項設定時，會忽略此設定，且會繼續軟體安裝。|  
|在部署此程式的電腦上停用此程式|忽略設定|不支援此設定，且不影響軟體的安裝。|  
|允許在未部署此程式的情況下，從安裝套件工作順序安裝此程式||用戶端不支援工作順序。<br /><br /> 不支援此設定，且不影響軟體的安裝。|  
|Windows Installer：<br /><br /> - 所有選項|忽略設定|用戶端不支援 Windows Installer 檔案或設定。|  
|OpsMgr 維護模式：<br /><br /> - 所有選項|忽略設定|用戶端不支援這項設定。|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>將軟體部署到 Linux 或 UNIX 伺服器
 若要使用套件和程式將軟體部署至 Linux 或 UNIX 伺服器，您可以從 Configuration Manager 主控台使用 [部署軟體精靈]。 Linux 和 UNIX 的用戶端支援大部分的部署設定。 但是，不支援數項設定。 當您部署軟體時，請考量下列狀況：  

-   您必須在至少一個與針對內容位置所設定之界限群組相關聯的發佈點上佈建套件。  

-   接收此部署的 Linux 和 UNIX 的用戶端，必須能夠從其網路位置存取此發佈點。  

-   Linux 和 UNIX 的用戶端會從發佈點下載套件，並在本機電腦上執行程式。  

-   Linux 和 UNIX 的用戶端無法從共用資料夾下載套件。 它會從啟用 IIS 的發佈點 (支援 HTTP 或 HTTPS) 下載套件。  

 下表列出不支援的部署內容：  

|部署內容|行為|詳細資訊|  
|-------------------------|--------------|----------------------|  
|部署設定 – 目的：<br /><br /> - 可用<br /><br /> - 必要|忽略設定|不支援使用者特定的設定。<br /><br /> 不過，用戶端支援 [必要] 設定 (該設定會強制執行排程的安裝時間)，但不支援在排程時間前進行手動安裝。|  
|傳送喚醒封包|忽略設定|用戶端不支援這項設定。|  
|指派排程：<br /><br /> - logon<br /><br /> - logoff|產生錯誤且軟體安裝失敗|不支援使用者特定的設定。<br /><br /> 不過，用戶端支援 [盡快] 設定。|  
|通知設定：<br /><br /> - 允許使用者不論指派均執行程式|忽略設定|用戶端尚未實作使用者介面。|  
|到了排程指派時間時，便允許在維護期間以外執行下列活動：<br /><br /> - 系統重新啟動 (如果是完成安裝所需)|產生錯誤|用戶端不支援系統重新啟動。|  
|高速 (LAN) 網路的部署選項：<br /><br /> - 從發佈點執行程式|產生錯誤且軟體安裝失敗|用戶端無法從發佈點執行軟體，必須改為先下載程式才能執行。|  
|網路速度慢或不可靠之網路界限的部署選項，或內容的後援來源位置：<br /><br /> - 允許用戶端與同一個子網路上的其他用戶端共用內容|忽略設定|用戶端不支援在對等網路間共用內容。|  

 如需內容位置的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

 如需如何建立部署的詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>管理從發佈點下載軟體的網路頻寬  
 Linux 和 UNIX 用戶端支援從發佈點下載軟體時的網路頻寬控制。  

 用戶端會使用您設定為 Configuration Manager 之用戶端設定的背景智慧型傳送 (BITS) 設定，但未實作 BITS。 不過，為了節流處理網路頻寬的使用，用戶端會控制用於軟體下載的 HTTP 要求區塊大小及區塊間延遲。  

 若要設定讓用戶端使用網路頻寬控制功能，您可設定 [背景智慧型傳送]  的用戶端設定，然後將設定值套用到用戶端電腦。 若要使用頻寬控制功能，用戶端必須接收 [背景智慧型傳送]，並將下列設定設為 [是]：  

-   **限制 BITS 背景傳送的最大網路頻寬**  

 用戶端支援下列 [背景智慧型傳送] 的設定：  

    -   **節流時段開始時間**  

    -   **節流時段結束時間**  

    -   **節流時段的最大傳輸速率 (Kbps)**  

    -   **節流時段以外的最大傳輸速率 (Kbps)**  

下列 [背景智慧型傳送] 的設定未受支援，且遭到 Linux 和 UNIX 的用戶端忽略：  

-   **允許在節流時段以外進行 BITS 下載**  

 如果中斷從發佈點將軟體下載到用戶端的作業，Linux 和 UNIX 的用戶端就不會繼續下載， 反而會重新開始下載整個軟體套件。  

##  <a name="configure-operations-for-software-deployments"></a>軟體部署的設定作業  
 類似於 Windows 用戶端，Linux 和 UNIX 的 Configuration Manager 用戶端會在輪詢及檢查新原則時，探索新的軟體部署。 用戶端檢查新原則的頻率，取決於用戶端設定。 您可以設定維護期間來控制軟體部署的時機。  

 您可以使用套件內容、程式內容和部署內容，設定 Linux 和 UNIX 伺服器的軟體部署。  

 當用戶端接收到部署的原則時，會提交狀態訊息。 用戶端也會在其啟動軟體安裝時以及安裝完成或失敗時，提交狀態訊息。  

 使用 Linux 和 UNIX 的 Configuration Manager 用戶端所執行的根認證，執行軟體部署的程式。 程式命令的結束代碼，可用於判斷成功或失敗。 結束代碼為 0 (零) 視為成功。 此外， **stdout** (標準輸出資料流) 和 **stderr** (標準錯誤資料流) 會在記錄層級設定為 INFO 或 TRACE 時複製到記錄檔。  

> [!TIP]  
>  如果您要部署的軟體位於 Linux 或 UNIX 伺服器可以存取的網路檔案系統 (NFS) 共用，則不需要使用發佈點來下載套件。 不過，當您建立套件時，請勿選取 [此套件包含來源檔案] 核取方塊。 接著，當您在設定程式時，請指定適當的命令列以直接存取 NFS 掛接點上的套件。  
