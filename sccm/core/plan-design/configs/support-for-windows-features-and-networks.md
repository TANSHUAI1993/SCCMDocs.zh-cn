---
title: "Windows 功能的支援 | Microsoft Docs"
description: "了解 System Center Configuration Manager 所支援的 Windows 和網路功能。"
ms.custom: na
ms.date: 3/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e040552dab21ba9a71e06a78f6acc2ffe1b0eb61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Windows 功能和網路支援

*適用於：System Center Configuration Manager (最新分支)*

本主題識別一般 Windows 和網路功能的 System Center Configuration Manager 支援。  


##  <a name="bkmk_branchcache"></a> BranchCache  
若您在發佈點上啟用 BranchCache，可以搭配使用 Windows BranchCache 與 Configuration Manager，並將用戶端設為以分散式快取模式使用 BranchCache。

您可以在應用程式的部署類型上、封裝的部署上、以及針對工作序列設定 BranchCache 設定。  

當符合 BranchCache 需求時，此功能可讓位於遠端位置的用戶端從具有目前內容快取的本機用戶端取得內容。  

例如，當第一台啟用 BranchCache 的用戶端電腦從設定為 BranchCache 伺服器的發佈點要求內容時，用戶端電腦會下載並快取內容。 此內容接著會提供給相同子網路上要求此相同內容的用戶端使用。

這些用戶端也會快取內容。 後續相同子網路上的用戶端若用這種方式，就不需要從發佈點下載內容，之後要傳送時會透過多個用戶端發佈內容。  

**支援 BranchCache 與 Configuration Manager 的需求：**  
-   **設定發佈點：**  
    請將 **Windows BranchCache** 功能加入設定為發佈點的站台系統伺服器。    

    -   在設定為支援 BranchCache 的伺服器上，其發佈點不需要額外的設定。   
    -   您無法將 Windows BranchCache 新增至雲端架構的發佈點，但雲端架構的發佈點支援針對 Windows BranchCache 設定的用戶端，透過其下載內容。  

-   **設定用戶端：**    
    -   可支援 BranchCache 的用戶端必須針對 BranchCache 分散式快取模式進行設定。  
    -   必須啟用 BITS 用戶端設定的作業系統設定，才能支援 BranchCache。   <br /> <br />
        
    如需如何將用戶端資訊設為支援 BranchCache 的資訊，請參閱 [Configure BranchCache for Windows 10 updates](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache) (設定 Windows 10 更新的 BranchCache) 中的[設定用戶端](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache#configure-clients-for-branchcache)一節。


**Configuration Manager 支援下列使用 Windows BranchCache 的用戶端作業系統：**  

|作業系統|支援詳細資料|  
|----------------------|---------------------|  
|Windows 7 SP1|預設支援|  
|Windows 8|預設支援|  
|Windows 8.1|預設支援|  
|Windows 10|預設支援|  
|Windows Server 2008 SP2|**需要 BITS 4.0**：您可以使用軟體更新或軟體發佈，在 Configuration Manager 用戶端上安裝 BITS 4.0 版本。 如需 BITS 4.0 版的詳細資訊，請參閱 [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979)。<br /><br /> 在此作業系統上，從網路上執行、或針對 SMB 檔案傳輸執行的軟體發佈不支援 BranchCache 用戶端功能。 此外，此作業系統無法搭配雲端式發佈點使用 BranchCache 功能。|  
|Windows Server 2008 R2|預設支援|  
|Windows Server 2012|預設支援|  
|Windows Server 2012 R2|預設支援|  

 如需 BranchCache 的詳細資訊，請參閱 Windows Server 文件中的 [BranchCache for Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) 。  

##  <a name="bkmk_Workgroups"></a> 工作群組中的電腦  
Configuration Manager 會針對工作群組中的用戶端提供支援。  

-   Configuration Manager 支援將用戶端從工作群組移到網域，或從網域移到工作群組。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)主題中的[如何在工作群組電腦上安裝 Configuration Manager 用戶端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)。  

> [!NOTE]  
>  雖然工作群組中的用戶端會受到支援，但所有站台系統都必須是受支援 Active Directory 網域的成員。  


##  <a name="bkmmk_datadedup"></a> 重複資料刪除  
Configuration Manager 支援在下列作業系統上，對發佈點使用重複資料刪除：  

-   Windows Server 2012  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  裝載封裝來源檔案的磁碟區不能標示進行重複資料刪除。 這是因為重複資料刪除會使用重新分析點，且 Configuration Manager 不支援使用其檔案儲存在重新分析點上的內容來源位置。  

如需詳細資訊，請參閱 Configuration Manager 小組部落格上的 [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) (Configuration Manager 發佈點和 Windows Server 2012 重複資料刪除)，以及 Windows Server TechNet 文件庫中的[重複資料刪除概觀](http://technet.microsoft.com/library/hh831602.aspx)。  

##  <a name="bkmk_DA"></a> DirectAccess  
Configuration Manager 支援 Windows Server 2008 R2 及更新版本中的 DirectAccess 功能，以進行用戶端與站台伺服器系統之間的通訊。  

-   滿足 DirectAccess 的所有需求時，DirectAccess 即可讓網際網路上的 Configuration Manager 用戶端與指派的站台通訊，就彷彿它們位於內部網路上。  

-   對於伺服器起始的動作，例如遠端控制和用戶端推入安裝，起始的電腦 (例如站台伺服器) 必須執行 IPv6，且所有中間的網路裝置都必須支援此通訊協定。  

Configuration Manager 不支援透過 DirectAccess 進行下列作業：  

-   部署作業系統  

-   Configuration Manager 站台之間的通訊  

-   站台內 Configuration Manager 站台系統伺服器之間的通訊  

##  <a name="bkmk_dualboot"></a> 雙重開機電腦  
 Configuration Manager 無法在單一電腦上管理多個作業系統。 如果必須管理的電腦上有多個作業系統，請調整使用的探索與安裝方法，以確保 Configuration Manager 用戶端只安裝在必須管理的作業系統上。  

##  <a name="bkmk_IPv6"></a> 網際網路通訊協定第 6 版  
 Configuration Manager 除了網際網路通訊協定第 4 版 (IPv4) 之外，也支援網際網路通訊協定第 6 版 (IPv6)，但下列例外狀況除外：  

|功能| IPv6 支援的例外狀況|  
|--------------|-------------------------------|  
|雲端架構的發佈點|需要 IPv4 才能支援 Microsoft Azure 與雲端式發佈點。|  
|由 Microsoft Intune 與 Microsoft 服務連接器註冊的行動裝置|需要 IPv4 才能支援由 Microsoft Intune 與 Microsoft 服務連接器註冊的行動裝置。|  
|網路探索|當您設定 DHCP 伺服器以搜尋網路探索時需要 IPv4。|  
|作業系統部署|支援作業系統部署時需要 IPv4。|  
|喚醒 proxy 通訊|支援用戶端喚醒 proxy 封包時需要 IPv4。|  
|Windows CE|支援 Windows CE 裝置上的 Configuration Manager 用戶端時需要 IPv4。|  

##  <a name="bkmk_NAT"></a> 網路位址轉譯  
 除非站台支援位於網際網路上的用戶端，且用戶端偵測到它已連線到網際網路，否則 Configuration Manager 不支援網路位址轉譯 (NAT)。 如需以網際網路為基礎之用戶端管理的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃管理以網際網路為基礎的用戶端](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md)。  

##  <a name="bkmk_storage"></a> 專門儲存體技術  
 Configuration Manager 可以與硬體搭配運作，但硬體必須是安裝 Configuration Manager 元件之作業系統版本的 Windows 硬體相容性清單上已通過認證的硬體。

站台伺服器角色需要 NTFS 檔案系統，以便設定目錄和檔案權限。 因為 Configuration Manager 假設它有完整的邏輯磁碟機擁有權，所以在不同電腦上執行的站台系統無法共用任何儲存技術上的邏輯磁碟分割。 不過，每一部電腦可以在共用存放裝置的相同實體磁碟分割上，使用不同的邏輯磁碟分割。  

 **支援注意事項：**  

-   **存放區域網路**：當支援的 Windows 伺服器直接連線到存放區域網路 (SAN) 裝載的磁碟區時，即支援 SAN。  

-   **儲存單一版本**：Configuration Manager 不支援在具有儲存單一版本 (SIS) 功能的磁碟區上設定發佈點套件和簽章資料夾。  

     此外，在已啟用 SIS 的磁碟區上也不支援 Configuration Manager 用戶端的快取。  

-   **卸除式磁碟機**：Configuration Manager 不支援在卸除式磁碟機上安裝 Configuration Manager 站台系統或用戶端。  
