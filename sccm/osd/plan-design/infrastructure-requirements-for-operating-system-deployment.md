---
title: "作業系統部署的基礎結構需求 | Microsoft Docs"
description: "在使用 System Center 2012 Configuration Manager 作業系統部署之前，請務必先了解外部相依性及產品的相依性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 167e639cdb9995fd743787cc9fbf364ec70f6ed9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>System Center Configuration Manager 中作業系統部署的基礎結構需求

*適用於：System Center Configuration Manager (最新分支)*

System Center 2012 Configuration Manager 中的作業系統部署具有外部相依性和產品中的相依性。 使用下列章節可協助您做好作業系統部署的準備。  

##  <a name="BKMK_ExternalDependencies"></a> Configuration Manager 外部的相依性  
 以下為在 Configuration Manager 中部署作業系統所需之外部工具、安裝套件及作業系統的資訊。  

### <a name="windows-adk-for-windows-10"></a>Windows ADK for Windows 10  
 Windows ADK 是一組工具和文件，支援設定及部署 Windows 作業系統。 Configuration Manager 會使用 Windows ADK 自動化 Windows 安裝、擷取 Windows 映像、進行使用者設定檔和資料移轉等作業。  

 下列 Windows ADK 功能必須安裝到階層中頂層網站的站台伺服器、階層中每個主要站台的站台伺服器，以及 SMS 提供者站台系統伺服器上：  

-   使用者狀態移轉工具 (USMT) <sup>1</sup>  

-   Windows 部署工具  

-   Windows 預先安裝環境 (Windows PE)

如需可搭配不同 Configuration Manager 版本使用的 Windows 10 ADK 版本清單，請參閱[對 Windows 10 用戶端的支援](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)。

 <sup>1</sup> USMT 在 SMS 提供者站台系統伺服器上並不需要。  

> [!NOTE]  
>  您必須先在每一部要裝載管理中心網站和主要站台伺服器的電腦上手動安裝 Windows ADK，再安裝 Configuration Manager 站台。  

 如需詳細資訊，請參閱：  

-   [給 IT 專業人員，適用於 Windows 10 的 Windows ADK 案例](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [下載適用於 Windows 10 的 Windows ADK](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Windows 10 的支援](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>使用者狀態移轉工具 (USMT)  
 Configuration Manager 會使用包含 USMT 10 來源檔案的 USMT 套件來擷取使用者狀態，並在作業系統部署過程中將其還原。 Configuration Manager 安裝程式會自動在頂層站台建立 USMT 套件。 USMT 10 可以從 Windows 7、Windows 8、Windows 8.1 及 Windows 10 擷取使用者狀態。 USMT 10 發佈於適用於 Windows 10 的 Windows 評定及部署套件 (Windows ADK) 中。  

 如需詳細資訊，請參閱：  

-   [USMT 10 的常見移轉案例](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [管理使用者狀態](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE 用於開機映像，以啟動電腦。 它是提供有限服務的 Windows 作業系統，會在預先安裝和部署 Windows 作業系統的過程中使用。 以下提供 Configuration Manager 版本、支援的 Windows ADK 版本，以及開機映像 (包括可從 Configuration Manager 主控台自訂的開機映像，以及可以使用 DISM 自訂然後新增映像到指定 Configuration Manager 版本的開機映像) 所依據的 Windows PE 版本。  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager 1511 版  
 以下提供支援的 Windows ADK 版本，以及開機映像 (包括可從 Configuration Manager 主控台自訂的開機映像，以及可以使用 DISM 自訂然後新增映像到指定 Configuration Manager 版本的開機映像) 所依據的 Windows PE 版本。  

-   **Windows ADK 版本**  

     Windows ADK for Windows 10  

-   **可從 Configuration Manager 主控台自訂之開機映像的 Windows PE 版本**  

     Windows PE 10  

-   **無法從 Configuration Manager 主控台自訂之開機映像的支援 Windows PE 版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有當開機映像以 Windows PE 3.1 為基礎時，您才能將開機映像新增至 Configuration Manager。 請安裝適用於 Windows 7 SP1 的 Windows AIK 補充元件，以便使用適用於 Windows 7 SP1 的 Windows AIK 補充元件 (以 Windows PE 3.1 為基礎) 來升級適用於 Windows 7 的 Windows AIK (以 Windows PE 3 為基礎)。 您可以從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=5188)下載適用於 Windows 7 SP1 的 Windows AIK 補充元件。  

     例如，當您有 Configuration Manager 時，便可從 Configuration Manager 主控台，使用適用於 Windows 10 的 Windows ADK (以 Windows PE 10 為基礎) 來自訂開機映像。 不過，若支援以 Windows PE 5 為基礎的開機映像，您必須從不同的電腦自訂開機映像，並使用與 Windows ADK for Windows 8 一起安裝的 DISM 版本。 接著，您可以將開機映像新增到 Configuration Manager 主控台。 如需自訂開機映像 (新增選用元件和驅動程式)、啟用開機映像的命令支援、將開機映像新增至 Configuration Manager 主控台，以及使用開機映像更新發佈點之步驟的詳細資訊，請參閱[自訂開機映像](../get-started/customize-boot-images.md)。 如需開機映像的詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
您必須安裝下列 WSUS 4.0 Hotfix：
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) 的 WSUS 4.0 為 Windows 10 服務所必須，該服務使用軟體更新基礎結構以取得 Windows 10 功能升級。 當您具有 WSUS 3.2 時，您必須使用工作順序升級 Windows 10。 如需詳細資訊，請參閱[管理 Windows 即服務](../deploy-use/manage-windows-as-a-service.md)。  
  - [Hotfix 3159706](https://support.microsoft.com/kb/3159706) 是使用 Windows 10 服務，將電腦升級為 Windows 10 年度更新版與後續版本的必要項目。 若要安裝此 Hotfix，您必須採取支援文章所述的手動步驟。 如需詳細資訊，請參閱[管理 Windows 即服務](../deploy-use/manage-windows-as-a-service.md)。


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>站台系統伺服器上的網際網路資訊服務 (IIS)  
 發佈點、狀態移轉點和管理點需要 IIS。 如需此項需求的詳細資訊，請參閱[站台和站台系統必要條件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-deployment-services-wds"></a>Windows 部署服務 (WDS)  
 以下情況需要 WDS：PXE 部署、使用多點傳送將部署的頻寬最佳化，以及映像的離線服務。 若遠端伺服器上安裝提供者，則您必須在站台伺服器和遠端提供者上安裝 WDS。 如需詳細資訊，請參閱本主題中的 [Windows 部署服務](#BKMK_WDS) 。  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>動態主機設定通訊協定 (DHCP)  
 DHCP 是 PXE 部署所需。 您必須具備作用中主機與正常運作 DHCP 伺服器，才能使用 PXE 部署作業系統。 如需 PXE 部署的詳細資訊，請參閱[透過網路來使用 PXE 部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>支援的作業系統和硬碟設定  
 在您部署作業系統時，如需 Configuration Manager 所支援的作業系統版本和硬碟設定詳細資訊，請參閱[支援的作業系統](#BKMK_SupportedOS)及[支援的磁碟設定](#BKMK_SupportedDiskConfig)。  

### <a name="windows-device-drivers"></a>Windows 裝置驅動程式  
 您在目的地電腦上安裝作業系統以及使用開機映像執行 Windows PE 時，可以使用 Windows 裝置驅動程式。 如需裝置驅動程式的詳細資訊，請參閱[管理驅動程式](../get-started/manage-drivers.md)。  

##  <a name="BKMK_InternalDependencies"></a> Configuration Manager 相依性  
 以下為 Configuration Manager 作業系統部署必要條件的資訊。  

### <a name="operating-system-image"></a>作業系統映像  
 Configuration Manager 中的作業系統映像儲存為 Windows 映像 (WIM) 檔案格式，代表經過壓縮的參照檔案和資料夾集合，其為成功在電腦上安裝及設定作業系統所必需。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  

### <a name="driver-catalog"></a>驅動程式類別目錄  
 若要部署裝置驅動程式，您必須匯入裝置驅動程式、啟用它，並且在 Configuration Manager 用戶端可以存取的發佈點上提供該驅動程式。 如需驅動程式類別目錄的詳細資訊，請參閱[管理驅動程式](../get-started/manage-drivers.md)。  

### <a name="management-point"></a>管理點  
 管理點會在用戶端電腦和 Configuration Manager 站台之間傳送資訊。 用戶端會使用管理點執行完成作業系統部署所需的任何工作順序。  

 如需工作順序的詳細資訊，請參閱[自動化工作的規劃考量](planning-considerations-for-automating-tasks.md)。  

### <a name="distribution-point"></a>發佈點  
 發佈點在大部分部署中用來儲存部署作業系統所使用的資料，例如作業系統映像或裝置驅動程式套件。 工作順序通常會從發佈點擷取資料來部署作業系統。  

 如需安裝發佈點及管理內容之方式的詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="pxe-enabled-distribution-point"></a>啟用 PXE 的發佈點  
 若要部署起始 PXE 的部署，您必須設定發佈點以接收來自用戶端的 PXE 要求。 如需如何為發佈點的詳細資訊，請參閱[設定發佈點](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe)。  

### <a name="multicast-enabled-distribution-point"></a>啟用多點傳送的發佈點  
 若要使用多點傳送最佳化作業系統部署，您必須設定發佈點支援多點傳送。 如需如何為發佈點的詳細資訊，請參閱[設定發佈點](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast)。   

### <a name="state-migration-point"></a>狀態移轉點  
 當您擷取及還原並存與重新整理部署所需的使用者狀態資料時，必須設定狀態移轉點，才能在另一部電腦上還原使用者狀態資料。  

 如需如何設定狀態移轉點的詳細資訊，請參閱 [狀態移轉點](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

 如需擷取及還原使用者狀態方式的資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

### <a name="service-connection-point"></a>服務連接點  
 當您使用 Windows 作為服務 (WaaS) 來部署 Windows 10 最新分支時，您必須有已安裝的服務連接點。 如需詳細資訊，請參閱[管理 Windows 即服務](../deploy-use/manage-windows-as-a-service.md)。  

### <a name="reporting-services-point"></a>Reporting Services 點  
 若要使用 Configuration Manager 報告進行作業系統部署，您必須安裝及設定 Reporting Services 點。 如需詳細資訊，請參閱[報告](../../core/servers/manage/reporting.md)。  

### <a name="security-permissions-for-operating-system-deployments"></a>作業系統部署的安全性權限  
 [作業系統部署管理員]  安全性角色是內建的角色，無法變更。 不過，您可以複製角色、進行變更，然後將變更儲存為新的自訂安全性角色。 以下是直接套用至作業系統部署的權限：  

-   **開機映像套件**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

-   **裝置驅動程式**：建立、刪除、修改、修改資料夾、修改報告、移動物件、讀取、執行報告  

-   **驅動程式套件**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

-   **作業系統映像**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

-   **作業系統安裝套件**：建立、刪除、修改、修改資料夾、移動物件、讀取、設定安全性範圍  

-   **工作順序套件**：建立、建立工作順序媒體、刪除、修改、修改資料夾、修改報告、移動物件、讀取、執行報告、設定安全性範圍  

 如需有關自訂安全性角色的詳細資訊，請參閱 [建立自訂安全性角色](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)。  

### <a name="security-scopes-for-operating-system-deployments"></a>作業系統部署的安全性範圍  
 使用安全性範圍可提供管理使用者存取作業系統部署中所使用可保護物件的權限，例如作業系統及開機映像、驅動程式套件及工作順序套件。 如需詳細資訊，請參閱 [安全性範圍](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)。  

##  <a name="BKMK_WDS"></a> Windows 部署服務  
 Windows 部署服務 (WDS) 必須與您設定支援 PXE 或多點傳送的部署點安裝在同一部伺服器上。 WDS 已包含在伺服器的作業系統中。 對於 PXE 部署而言，WDS 是執行 PXE 開機的服務。 安裝並啟用 PXE 的發佈點時，Configuration Manager 會將提供者安裝到使用 WDS PXE 開機功能的 WDS 中。  

> [!NOTE]  
>  如果伺服器需要重新啟動，則 WDS 安裝可能會失敗。 

 其他必須納入考慮的 WDS 設定包括下列：  

-   系統管理員必須是 Local Administrators 群組成員，才能在伺服器上安裝 WDS。  

-   WDS 伺服器必須是 Active Directory 網域成員，或是 Active Directory 網域的網域控制站。 所有 Windows 網域和樹系設定皆支援 WDS。  

-   若遠端伺服器上安裝提供者，則您必須在站台伺服器和遠端提供者上安裝 WDS。  

###  <a name="BKMK_WDSandDHCP"></a> 當您在同一部伺服器上有 WDS 和 DHCP 時的考量  
 如果您規劃在執行 DHCP 的伺服器上共同裝載發佈點，請考慮以下設定問題。  

-   您必須擁有一部具作用中範圍之正在運作的 DHCP 伺服器 Windows 部署服務使用 PXE，其需要 DHCP 伺服器。  

-   DHCP 和 Windows 部署服務都需要連接埠號碼 67。 如果共同裝載 Windows 部署服務和 DHCP，您就可以將 DHCP 或為 PXE 設定的發佈點移到另外的伺服器。 您也可使用下列程序，將 Windows Deployment Services 伺服器設定為在不同的連接埠上接聽。  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>將 Windows 部署服務伺服器設定為在不同的連接埠上接聽  

    1.  修改下列登錄機碼：  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  將登錄值設定為： **UseDHCPPorts = 0**  

    3.  若要讓新設定生效，可在伺服器執行下列命令：  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   執行 Windows 部署服務時需要 DNS 伺服器。  

-   必須在 Windows 部署服務伺服器上開啟下列 UDP 連接埠。  

    -   連接埠 67 (DHCP)  

    -   連接埠 69 (TFTP)  

    -   連接埠 4011 (PXE)  

    > [!NOTE]  
    >  此外，如果在伺服器上需要 DHCP 授權，您需要在伺服器上開啟 DHCP 用戶端連接埠 68。  

##  <a name="BKMK_SupportedOS"></a> 支援的作業系統  
 在[支援的用戶端和裝置作業系統](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)中，列為支援之用戶端作業系統的所有 Windows 作業系統，皆可支援作業系統部署。  

##  <a name="BKMK_SupportedDiskConfig"></a> 支援的磁碟設定  
 下表顯示支援 Configuration Manager 作業系統部署之參照電腦和目的地電腦的硬碟設定組合。  

|參照電腦硬碟設定|目的地電腦硬碟設定|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁碟|基本磁碟|  
|動態磁碟上的簡單磁碟區|動態磁碟上的簡單磁碟區|  

 Configuration Manager 僅支援從已設定簡單磁碟區的電腦擷取作業系統映像。 不支援下列硬碟設定：  

-   合併磁碟區  

-   等量磁碟區 (RAID 0)  

-   鏡像磁碟區 (RAID 1)  

-   同位檢查磁碟區 (RAID 5)  

 下表顯示不支援 Configuration Manager 作業系統部署之參照和目的地電腦上的其他硬碟設定。  

|參照電腦硬碟設定|目的地電腦硬碟設定|  
|------------------------------------------------|--------------------------------------------------|  
|基本磁碟|動態磁碟|  

## <a name="next-steps"></a>後續步驟
[準備作業系統部署](../get-started/prepare-for-operating-system-deployment.md)
