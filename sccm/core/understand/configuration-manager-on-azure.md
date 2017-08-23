---
title: "Azure 上的 Configuration Manager | Microsoft Docs"
description: "在 Azure 環境上使用 Configuration Manager 的相關資訊。"
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5276ad999fc871496d79e6efff34d5edc6335380
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Azure 的 Configuration Manager - 常見問題集
*適用對象：System Center Configuration Manager (最新分支)*

下列問題及回答可協助您了解何時使用，以及如何在 Microsoft Azure 上設定 Configuration Manager。

## <a name="general-questions"></a>一般問題
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>我的公司正嘗試將盡可能多的實體伺服器移動至 Microsoft Azure，我可以將 Configuration Manager 伺服器移動至 Azure 嗎？
當然可以，這是支援的案例。  請參閱 [System Center Configuration Manager 的虛擬化環境支援](/sccm/core/plan-design/configs/support-for-virtualization-environments)。

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>太棒了！ 我的環境需要多個站台。 是否所有的子主要站台都應該在 Azure 中，使用管理中心網站或內部部署？ 那次要站台呢？
站台對站台通訊 (檔案型和資料庫複寫) 因裝載在 Azure 中的近距離而得益。 不過，所有用戶端相關的流量都與站台伺服器及站台系統無關。 如果使用無限行動數據方案的 Azure 和內部網路連線快速又穩定，將所有基礎結構裝載在 Azure 中也是一個選項。

但若使用計量付費數據傳輸方案，要考慮可用的頻寬或成本，或 Azure 和內部網路之間的網路連線速度不夠快，或可能不夠穩定，請考慮將特定網站 (和站台系統) 放在內部，然後使用 Configuration Manager 內建的頻寬控制。

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>將 Configuration Manager 放在 Azure 中是 SaaS (軟體即服務) 案例嗎？
否，這是 IaaS (基礎結構即服務)，因為 Configuration Manager 基礎結構伺服器是裝載在 Azure 虛擬機器中。

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>將 Configuration Manager 基礎結構移至 Azure 時應注意哪些部分？
這個問題很棒，以下是進行此決策時最重要的各個部分，本主題會在各節中一一探索︰
1.  網路功能
2.  可用性
3.  效能
4.  成本
5.  使用者體驗

## <a name="networking"></a>網路功能
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>那網路需求呢，我應該使用 ExpressRoute 或 Azure VPN 閘道？
網路功能是非常重要的決策。 網路速度和延遲會影響站台伺服器和遠端站台系統與任何站台系統用戶端之間進行通訊的功能。 建議您使用 ExpressRoute。 但 Configuration Manager 對您使用 Azure VPN 閘道沒有任何限制。 您應該仔細從這個基礎結構檢閱您的需求 (效能、修補、軟體發佈、作業系統部署)，再進行您的決定。 每項解決方案都要考慮的事項包括︰

 - **ExpressRoute** (建議選項)
  - 資料中心的自然擴充 (可結合多個資料中心)
  - Azure 資料中心和基礎結構之間的私人連線
  - 不經過公用網際網路
  - 提供穩定性、高速、低延遲、高安全性
  - 提供高達 10 Gbps 的速度和無限行動數據方案選項
 - **VPN 閘道**
  - 站對站/點對站 VPN
  - 流量經過公用網際網路
  - 使用網際網路通訊協定安全性 (IPsec) 和網際網路金鑰交換 (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute 有許多不同的選項，例如無限行動數據與計量付費數據、不同速度的選項及超值的附加元件。 我該選哪一種？
您要根據實作案例以及計劃散發的資料量選取選項。 站台伺服器與發佈點之間的 Configuration Manager 資料傳輸是可以控制的，但是站台伺服器對站台伺服器的通訊無法控制。   當您使用計量付費數據傳輸方案時，將特定網站 (和站台系統) 放在內部部署與使用 [Configuration Manager 內建的頻寬控制](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)有助於控制使用 Azure 的成本。

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>像 Active Directory 網域這樣的安裝需求呢？ 我還需要將站台伺服器加入 Active Directory 網域嗎？
是。 當您移到 Azure 時，[支援的設定](/sccm/core/plan-design/configs/supported-configurations)保持不變，包括安裝 Configuration Manager 的 Active Directory 需求。

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>我知道站台伺服器必須加入 Active Directory 網域，但是可以使用 Azure Active Directory 嗎？
否，目前不支援 Azure Active Directory。 您的站台伺服器仍必須是 [Windows Active Directory 網域](/sccm/core/plan-design/configs/support-for-active-directory-domains)的成員。



## <a name="availability"></a>可用性
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>我將基礎結構移至 Azure 的原因之一是它承諾高可用性。 我可以將像 Azure VM 可用性設定組這樣的高可用性選項，用在 Configuration Manager 要使用的 VM 嗎？
是！ Azure VM 可用性設定組可用於備援的站台系統角色，例如發佈點或管理點。

您也可以將它們用於 Configuration Manager 站台伺服器。 例如，管理中心網站和主要站台全部可位於相同的可用性設定組中，以利確保它們不會同時重新開機。

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>我該如何讓資料庫具有高可用性？ 我可以使用 Azure SQL Database 嗎？ VM 中必須使用 Microsoft SQL Server 嗎？
VM 中必須使用 Microsoft SQL Server。 Configuration Manager 目前不支援 Azure SQL Server。 但是 SQL server 可以使用 AlwaysOn 可用性群組這類的功能。 從 Configuration Manager 1602 版開始建議使用並正式支援 [AlwaysOn 可用性群組](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)。

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Azure 負載平衡器可以和如管理點或軟體更新點這樣的站台系統角色一起使用嗎？
雖然 Configuration Manager 未使用 Azure 負載平衡器測試，但只要是向應用程式開放的功能，應該不會對正常作業有任何負面影響。


## <a name="performance"></a>效能
### <a name="what-factors-affect-performance-in-this-scenario"></a>本案例中影響效能的因素
[Azure VM 的大小與類型](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs)、Azure VM 的磁碟 (建議使用進階儲存體，尤其是 SQL Server)、網路延遲和速度都是最重要的部分。

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>那麼，告訴我更多關於 Azure 虛擬機器的情況吧，我該使用何種大小的 VM？
一般情況下，計算能力 (CPU 和記憶體) 必須符合 [recommended hardware for System Center Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware) (System Center Configuration Manager 的建議硬體)。 但是一般電腦硬體和 Azure VM 之間有一些差異，特別是關係到這些 VM 使用的磁碟時。  您使用的 VM 大小取決於環境的大小，以下提供您一些建議︰
- 凡是大小相當大的生產環境部署，建議使用 “**S**” 類別的 Azure VM。 這是因為它們可以使用進階儲存體磁碟。  非 "S" 類別的 VM 使用 Blob 儲存體，而且一般不會符合可接受生產體驗的必要效能需求。
- 多個進階儲存體磁碟應該用於較高的級別，且與 Windows 磁碟管理主控台中最大的 IOPS 等量。  
- 建議您在初始站台部署期間使用較佳或多個進階磁碟 (例如用 P30 而非 P20，在等量磁碟區用 2xP30 而非 1xP30)。 接著，若站台後來因為額外負載需要增加 VM 大小，您就可以利用較大的 VM 大小來提供的額外 CPU 和記憶體。 您也會有預先準備好的磁碟，可以利用較大的 VM 大小所允許的額外 IOPS 輸送量。



下表列出主要和管理中心網站用於各種大小安裝的初始建議磁碟計數︰

**共置的站台資料庫**：站台伺服器上具有站台資料庫的主要或管理中心網站︰

| 桌面用戶端    |建議的 VM 大小|建議的磁碟|
|--------------------|-------------------|-----------------|
|**最多 25 k**       |   DS4_V2          |2xP30 (等量)  |
|**25 k 到 50 k**      |   DS13_V2         |2xP30 (等量)  |
|**50 k 至 100 k**     |   DS14_V2         |3xP30 (等量)  |


**遠端站台資料庫**：遠端伺服器上具有站台資料庫的主要或管理中心網站︰

| 桌面用戶端    |建議的 VM 大小|建議的磁碟 |
|--------------------|-------------------|------------------|
|**最多 25 k**       | 站台伺服器：F4S </br>資料庫伺服器：DS12_V2 | 站台伺服器：1xP30 </br>資料庫伺服器：2xP30 (等量)  |
|**25 k 到 50 k**      | 站台伺服器：F4S </br>資料庫伺服器：DS13_V2 | 站台伺服器：1xP30 </br>資料庫伺服器：2xP30 (等量)   |
|**50 k 至 100 k**     | 站台伺服器：F8S </br>資料庫伺服器：DS14_V2 | 站台伺服器：2xP30 (等量)   </br>資料庫伺服器：3xP30 (等量)   |

下圖顯示 DS14_V2 上 50k 至 100k 之用戶端的設定範例，其在等量磁碟區中有 3xP30 個磁碟，並有不同的邏輯磁碟區以供 Configuration Manager 安裝和資料庫檔案使用：![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>使用者體驗
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>您提到的使用者體驗是很重要的主要部分之一，為什麼會這樣？
您對網路功能、可用性、效能和 Configuration Manager 站台伺服器位置的決定，都會直接影響您的使用者。 我們相信移至 Azure 應該對您的使用者透明公開，他們才不會在與 Configuration Manager 的日常互動中感受到變化。

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>好，我了解了。 我打算在 Azure 虛擬機器上安裝單一的獨立主要站台，而且希望確保成本低廉。 我是不是也應該將 (遠端) 站台系統 (例如管理點、發佈點和軟體更新點) 放在 Azure 虛擬機器上，還是放在內部部署？
除了從站台伺服器到發佈點的通訊以外，這些網站中伺服器對伺服器的通訊可能會在任何時間發生，並且不會使用任何機制控制網路頻寬的使用。 因為您無法控制站台系統之間的通訊，所以應該考慮與這些通訊相關的任何費用。

網路速度和延遲也是要考慮的其他因素。 速度慢又不穩定的網路會影響站台伺服器和遠端站台系統之間的功能，也會影響站台系統的所有用戶端通訊。 也應該考慮使用指定站台系統的受管理用戶端數目，以及目前正在使用的功能。
一般可以使用一般指引，因為它和 WAN 連結及站台系統有關，可以作為起點。 在理想情況下，Azure 和內部網路之間選取和接收的網路輸送量，和與快速網路連線狀況良好的 WAN 是一致的。

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>內容發佈與內容管理又是如何？ 標準發佈點應該位在 Azure 或內部部署？我應該使用 BranchCache 或內部部署提取發佈點？ 還是應該專用雲端發佈點？
內容管理的方法與站台伺服器和站台系統十分相似。
- 如果使用無限行動數據方案的 Azure 和內部網路連線快速又穩定，將標準發佈點裝載在 Azure 中也是一個選項。
-  如果您使用計量付費數據傳輸方案，而且要考量頻寬成本，或者 Azure 和內部網路之間的網路連線速度不夠快或不穩定，則可能要考慮其他方法。 這些包括尋找內部部署的標準或提取發佈點，以及使用 BranchCache。 使用雲端架構發佈點也是一個選項，但支援的內容類型會有所限制 (例如，不支援軟體更新套件)。

> [!NOTE]
>  如果需要 PXE 支援，則必須使用內部部署發佈點 (標準或提取) 回應開機要求。 [目前不支援在 Azure VM 上執行 WDS](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx)。


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>雖然我可以接受雲端架構發佈點的限制，但我不想將管理點放入 DMZ，即使必須這樣才能支援以網際網路為基礎的用戶端。 我有任何其他選項嗎？
是！ 我們在 Configuration Manager 1610 版推出了[雲端管理閘道器](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)作為發行前版本功能 (這項功能最先是以[雲端 Proxy 服務](/sccm/core/get-started/capabilities-in-technical-preview-1606#a-namecloudproxyacloud-proxy-service-for-managing-clients-on-the-internet)出現在 Technical Preview 1606 版中)。

**雲端管理閘道**可讓您輕鬆管理網際網路上的 Configuration Manager 用戶端。 部署至 Microsoft Azure 且需要 Azure 訂用帳戶的服務，使用稱為雲端管理閘道連接器端點的新角色，連線到內部部署的 Configuration Manager 基礎結構。 在它部署及設定好後，用戶端就可以存取內部部署的 Configuration Manager 站台系統角色，不論它們是連接到內部的私人網路還是網際網路。

您可以在環境中開始使用雲端管理閘道，並提供意見反應，幫助我們改進服務。 如需發行前版本功能的資訊，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkprereleasea-use-pre-release-features-from-updates)。

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>我還聽說你們有另一個稱為「對等快取」的新功能，其在 1610 版中當成發行前版本功能引進。 它和 BranchCache 不一樣嗎？ 我該選哪一種？
是的，它們完全不一樣。 [對等快取](/sccm/core/plan-design/hierarchy/client-peer-cache)是 100% 的原生 Configuration Manager 技術，而 BranchCache 則是 Windows 功能。 兩者對您都很有用，BranchCache 使用廣播尋找所需的內容，而對等快取則使用 Configuration Managers 一般發佈流程和界限群組設定。

任何用戶端都可以設定為對等快取來源。 然後，當管理點提供與內容來源位置有關的用戶端資訊時，它們會提供有該用戶端要求內容的發佈點和對等快取來源的詳細資料。


## <a name="cost"></a>成本
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>好的，請告訴我成本相關訊息。 這是符合我成本效益的解決方案嗎？
很難說，因為每個環境都不同。 最佳做法是使用 Microsoft Azure 價格計算機計算環境成本︰https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>其他資源
**基本概念︰** http://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Azure VM 電腦類型︰**
 - Azure 電腦大小：https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - VM 定價：http://azure.microsoft.com/pricing/details/virtual-machines/  
 - 儲存體定價：http://azure.microsoft.com/pricing/details/storage/

**磁碟效能考量：**    
 - 進階磁碟簡介︰http://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - 進階磁碟詳細資訊︰http://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - 儲存體最大大小和效能目標的便利圖表集︰https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - 進階儲存體幕後玩法的其他簡介 + 大神玩家資料︰http://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**可用性：**
 - Azure IaaS 上線時間 SLA︰https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - 可用性設定組說明︰https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**連線能力：**
 - 快速路由與Azure VPN：http://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - 快速路由定價：http://azure.microsoft.com/pricing/details/expressroute/
 - 快速路由詳細資訊：http://azure.microsoft.com/documentation/articles/expressroute-introduction/

 
