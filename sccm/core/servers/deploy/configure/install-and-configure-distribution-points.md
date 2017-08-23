---
title: "管理發佈點 | Microsoft Docs"
description: "裝載您使用發佈點部署至裝置與使用者的內容 (檔案和軟體)。 以下是安裝和設定它們的方法。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4c94e4de5bbfe621492e8682c9424a48eb38196d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 安裝及設定發佈點

*適用對象：System Center Configuration Manager (最新分支)*
 
您可安裝 System Center Configuration Manager 發佈點，來裝載部署至裝置與使用者的內容 (檔案和軟體)。 您也可以建立發佈點群組，以簡化發佈點的管理方式與將內容發佈至發佈點的方式。  

 當您使用安裝精靈來安裝新的發佈點，或透過編輯發佈點內容來管理現有的發佈點內容時，可以進行大部分的發佈點設定。 有一些設定唯有當您在安裝或編輯時才能使用，無法同時適用於這兩種情況：  

-   只有在安裝發佈點時才可用的設定：  

    -   **允許 Configuration Manager 在發佈點電腦上安裝 IIS**

    -   **設定發佈點的磁碟機空間設定**  

-   只有在編輯發佈點內容時才可用的設定：  

    -   **管理發佈點群組關聯性**  

    -   **檢視部署至發佈點的內容**  

    -   **替傳輸到發佈點的資料設定速率限制**  

    -   **替傳輸到發佈點的資料設定排程**  

##  <a name="bkmk_install"></a> 安裝發佈點  
 您必須將網站伺服器指定為發佈點，才能讓用戶端電腦使用內容。 您可以將發佈點網站角色新增至新的網站系統伺服器，或將網站角色新增至現有的網站系統伺服器。  

 當您安裝新的發佈點時，可以使用安裝精靈，逐步引導您完成可用的設定。 開始之前，請考量下列事項：  

-   您必須擁有下列安全性權限，才能建立及設定發佈點。  

    -   [發佈點] 物件的 [讀取]  權限  

    -   [發佈點] 物件的 [複製到發佈點]  權限  

    -   [網站] 物件的 [修改]  權限  

    -   [網站] 物件的 [管理作業系統部署的憑證]  權限  

-   即將裝載發佈點的伺服器上必須安裝 Internet Information Services (IIS)。 在您安裝站台系統角色時，Configuration Manager 可為您安裝並設定 IIS。  

使用下列基本程序來安裝或變更發佈點。 如需可用設定選項的詳細資訊，請參閱本主題的[設定發佈點](#bkmk_configs)一節。  

#### <a name="to-install-a-distribution-point"></a>安裝發佈點  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] >  [站台設定] > [伺服器和站台系統角色]。  

2.  將發佈點站台系統角色新增至新的或現有的站台系統伺服器：  

    -   **新增站台系統伺服器**：在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立站台系統伺服器]。 隨即開啟 [建立網站系統伺服器精靈]。  

    -   **現有的網站系統伺服器**：選擇要安裝發佈點網站系統角色的伺服器。 選擇伺服器時，會在結果窗格中顯示已經安裝在該伺服器上的網站系統角色清單。  

         在 [首頁] 索引標籤的 [伺服器] 群組中，選取 [新增網站系統角色]。 隨即開啟 [新增網站系統角色精靈]。  

3.  在 [一般]  頁面上，指定網站系統伺服器的一般設定。 將發佈點新增到現有的網站系統伺服器時，請確認之前設定的值。  

4.  在 [系統角色選取] 頁面上，在可用角色的清單中選擇 [發佈點]，然後選擇 [下一步]。  

5.  如需後續的精靈頁面，請參閱[設定發佈點](#bkmk_configs)一節中的資訊。  

     例如，如果您想將發佈點安裝為提取發佈點，可選擇 [啟用此發佈點以便從其他發佈點提取內容]，然後配置提取發佈點所需的其他設定。  

6.  在您完成精靈後，會將發佈點網站角色新增至網站系統伺服器。  

#### <a name="to-change-a-distribution-point"></a>變更發佈點  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] >  [發佈點]，然後選取您要設定的發佈點。  

2.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

3.  在編輯發佈點的內容時，請使用[設定發佈點](#bkmk_configs)一節中的資訊。  

4.  完成想要的變更後，請儲存您的設定並關閉發佈點內容。  

##  <a name="bkmk_manage"></a> 管理發佈點群組  
 發佈點群組提供內容發佈的發佈點邏輯群組。 您可使用這些群組，從跨越多個站台的發佈點中心位置來管理與監視內容。 請注意以下事項：

-   您可以從階層內的任何站台新增一個或多個發佈點到發佈點群組。  

-   您也可以將發佈點新增至一個以上的發佈點群組。  

-   在您將內容發佈至發佈點群組時，Configuration Manager 會將內容發佈至所有屬於發佈點群組成員的發佈點。  

-   若您在初始內容發佈之後，將發佈點新增至發佈點群組，Configuration Manager 會自動將內容發佈至該新發佈點成員。  

-   您也可建立集合與發佈點群組的關聯。 發佈內容到集合時，Configuration Manager 會判斷與集合相關的發佈點群組。 然後，內容會發佈到發佈點群組成員的所有發佈點。  

    > [!NOTE]  
    >  將內容發佈至集合後，若您再將該集合與新的發佈點群組建立關聯性，則必須將內容重新發佈至該集合，才能將該內容發佈至新的發佈點群組。  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>建立和設定新的發佈點群組  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [發佈點群組]。  

2.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立群組]。  

3.  輸入發佈點群組的名稱和描述。  

4.  在 [集合] 索引標籤上，選擇 [新增]，選取要與發佈點群組產生關聯的集合，然後選擇 [確定]。  

5.  在 [成員] 索引標籤上，選擇 [新增]，選取要新增為發佈點群組成員的發佈點，然後選擇 [確定]。  

6.  選擇 [確定]，建立發佈點群組。  

#### <a name="to-add-distribution-points-and-associate-collections-with-an-existing-distribution-point-group"></a>新增發佈點並為集合與現有發佈點群組建立關聯  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [發佈點群組]。  

2.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

3.  在 [集合] 索引標籤上，選擇 [新增] 以選取要與發佈點群組產生關聯的集合，然後選擇 [確定]。  

4.  在 [成員] 索引標籤上，選擇 [新增] 以選取要新增為發佈點群組成員的發佈點，然後選擇 [確定]。  

5.  按一下 [確定]，儲存對發佈點群組的變更。  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>將選取的發佈點新增至新的發佈點群組  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [發佈點]，然後選取要新增至新發佈點群組的發佈點。  

2.  在 [首頁] 索引標籤的 [發佈點] 群組中，展開 [新增選取的項目]，然後選擇 [將選取的項目新增至新的發佈點群組]。  

3.  輸入發佈點群組的名稱和描述。  

4.  在 [集合] 索引標籤上，選擇 [新增] 以選取要與發佈點群組產生關聯的集合，然後選擇 [確定]。  

5.  在 [成員] 索引標籤上，確認要讓 Configuration Manager 將列出的發佈點新增為發佈點群組的成員。 選擇 [新增] 新增發佈點，然後選擇 [確定]。  

6.  選擇 [確定]，建立發佈點群組。  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>將選取的發佈點新增至現有發佈點群組  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [發佈點]，然後選取要新增至新發佈點群組的發佈點。  

2.  在 [首頁] 索引標籤的 [發佈點] 群組中，展開 [新增選取的項目]，然後選擇 [將選取的項目新增至現有的發佈點群組]。  

3.  在 [可用的發佈點群組] 中，選取要新增選取的發佈點做為其成員的發佈點群組，然後選擇 [確定]。  

##  <a name="bkmk_configs"></a> 設定發佈點  
 個別發佈點會支援各種不同的設定。 不過，並非所有的發佈點類型都支援所有的組態。 例如，雲端式發佈點不支援針對 PXE 或多點傳送所啟用的內容部署。 您可以在下列主題中找到特定限制的相關資訊：  

-   [使用雲端架構發佈點搭配 System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [使用提取發佈點搭配 System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

下節描述在安裝新的發佈點或編輯現有發佈點的內容時，您可以選取的設定。  

### <a name="general"></a>一般  
 設定一般的發佈點設定：  

-   **在 Configuration Manager 需要時安裝並設定 IIS**：如果伺服器尚未安裝 IIS，選擇此設定可讓 Configuration Manager 進行安裝與設定。 必須在所有發佈點上安裝 IIS。 如果未在伺服器上安裝 IIS，且您未選擇此設定，則必須先安裝 IIS 才能順利安裝發佈點。  

    > [!NOTE]  
    >  此選項只有在安裝新的發佈點時才可用。  

- **啟用並設定此發佈點的 BranchCache**：選擇此設定可讓 Configuration Manager 設定發佈點伺服器上的 Windows BranchCache。 如需搭配 System Center Configuration Manager 使用 Windows BranchCache 的詳細資訊，請參閱＜System Center Configuration Manager 中的 Windows 功能和網路支援＞中的 [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache)。

-   **設定用戶端裝置與發佈點的通訊方式**：使用 HTTP 和 HTTPS 有其各自的優點和缺點。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的內容管理基本概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)的「內容管理的安全性最佳做法」。  

-   **允許用戶端以匿名方式連線**：此設定會指定發佈點是否允許從 Configuration Manager 用戶端匿名連線至內容庫。  

    > [!IMPORTANT]  
    >  若您未使用此設定，用戶端上的 Windows Installer 應用程式的修復可能會失敗。  
    >   
    >  當您在 Configuration Manager 用戶端上部署 Windows Installer 應用程式時，Configuration Manager 會將檔案下載至用戶端的本機快取。 檔案最後會在安裝完成時移除。
    >  
    >  Configuration Manager 用戶端會使用相關聯發佈點上之內容庫的內容路徑，更新已安裝之 Windows Installer 應用程式的 Windows Installer 來源檔案。 稍後，若您在 Configuration Manager 用戶端上從 [新增或移除程式] 啟動修復動作，MSIExec 會嘗試使用匿名使用者來存取內容路徑。  
    >   
    >  不過，您可以安裝 Microsoft 知識庫文章 [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) 中所述的更新，然後修改登錄機碼來變更此行為。  
    >   
    >  在用戶端上安裝更新後，如果您未選擇 [允許用戶端以匿名方式連線] 設定，MSIExec 就會使用登入的使用者帳戶存取內容路徑。  

-   **針對發佈點建立自我簽署的憑證，或匯入公開金鑰基礎結構 (PKI) 用戶端憑證**：憑證具有下列用途：  

    -   在發佈點傳送狀態訊息前，向管理點驗證發佈點。  

    -   勾選 [PXE 設定] 頁面上的 [為用戶端啟用 PXE 支援] 方塊時，會將憑證傳送至執行 PXE 開機的電腦，如此才能在部署作業系統期間連線至管理點。  

    網站中的所有管理點都設定為使用 HTTP 時，會建立自我簽署憑證。 管理點設定為使用 HTTPS 時，則匯入 PKI 用戶端憑證。  

    若要匯入憑證，請瀏覽至具有 PKI 憑證的公開金鑰加密標準 (PKCS #12) 檔案，其應符合下列 Configuration Manager 需求：  

    -   預期用途必須包含用戶端驗證。  

    -   必須啟用私密金鑰才能匯出。  

    > [!TIP]  
    >  對於憑證主體或主體別名 (SAN) 並無特定需求，您可以針對多個發佈點使用同一個憑證。  

     如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

     如需此憑證的部署範例，請參閱[為 System Center Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)中的「部署發佈點的用戶端憑證」一節。  

-   **啟用此發佈點供預先設置的內容使用**：選擇此設定以啟用此發佈點供預先設置的內容使用。 選取此設定時，您可以設定當您發佈內容時的發佈行為。 您可以選擇一律執行下列其中一項︰

 - 在發佈點上預先設置內容。
 - 預先設置套件的初始內容，不過在內容有所更新時，使用一般內容發佈程序。
 - 為套件的內容使用一般內容發佈程序。  

### <a name="drive-settings"></a>磁碟機設定  

> [!NOTE]  
>  這些選項只有在安裝新的發佈點時才可用。  

指定發佈點的磁碟機設定。 您可以為內容庫設定最多兩部磁碟機，以及為套件共用設定兩部磁碟機。 當前兩部磁碟機達到設定的磁碟機空間保留時，Configuration Manager 可以使用其他磁碟機。 [磁碟機設定]  頁面可設定磁碟機的優先順序，以及保留在每部磁碟機上的可用磁碟空間數量。  

-   **磁碟機空間保留 (MB)**：您為此設定所設的值，可在 Configuration Manager 選擇不同磁碟機並繼續對該磁碟進行複製程序前，判斷磁碟機上的可用空間數量。 內容檔案可以跨越多個磁碟機。  

-   **內容位置**：指定內容庫和封裝共用的內容位置。 Configuration Manager 會將內容複製到主要內容位置，直到可用空間量達到 [磁碟機空間保留 (MB)] 指定的值為止。 根據預設，內容位置會設定為 [自動] 。 主要內容位置會設定為在安裝時擁有最多磁碟空間的磁碟機，而次要位置則會指派給擁有第二多可用磁碟空間的磁碟機。 當主要和次要磁碟機都達到磁碟機空間保留的設定時，Configuration Manager 會選取其他具備最多可用磁碟空間的磁碟機，然後繼續進行複製程序。  

> [!NOTE]  
>  為避免 Configuration Manager 在特定磁碟機上進行安裝，請建立名為 **no_sms_on_drive.sms** 的空檔案，並將它複製到磁碟機的根資料夾，再安裝發佈點。  

### <a name="pull-distribution-point"></a>提取發佈點  
當您選擇 [啟用此發佈點以便從其他發佈點提取內容] 時，會變更電腦取得您發佈至發佈點之內容的行為方式。 該發佈點會變成提取發佈點。  

針對每個您設定的提取發佈點，您必須指定提取發佈點取得內容的一個或多個來源發佈點：  

-   選擇 [新增]，然後選取一或多個可用的發佈點作為來源發佈點。  

-   選擇 [移除]，將做為來源發佈點的已選取發佈點移除。  

-   使用箭號按鈕，調整當提取發佈點嘗試傳送內容時，提取發佈點連絡來源發佈點的順序。 首先連絡的是最低值的發佈點。  

### <a name="pxe"></a>PXE  
指定是否要在發佈點上啟用 PXE。 當您啟用 PXE 時，Configuration Manager 會視需要在伺服器上安裝 Windows 部署服務。 Windows 部署服務是一項執行 PXE 開機以安裝作業系統的服務。 在您完成精靈以建立發佈點後，Configuration Manager 會在 Windows 部署服務中安裝一個使用 PXE 開機功能的提供者。  

當您選擇 [為用戶端啟用 PXE 支援] 時，請設定下列設定：  

-   **允許此發佈點回應傳入的 PXE 要求**：指定是否要啟用 Windows 部署服務，使其回應 PXE 服務要求。 使用此方塊可啟用和停用服務，而不需移除發佈點上的 PXE 功能。  

-   **啟用未知電腦支援**：指定是否要針對 Configuration Manager 未管理的電腦啟用支援。  

-   **電腦使用 PXE 時需要密碼**：若要為您的 PXE 部署提供其他安全性，請指定強式密碼。  

-   **使用者裝置親和性**：指定您希望發佈點如何為 PXE 部署的使用者與目的地電腦建立關聯。 選擇下列其中一個選項：  

    -   **允許自動核准使用者裝置親和性**：選擇此設定以自動為使用者與目的地電腦建立關聯，不需要等待核准。  

    -   **允許使用者親和性等待系統管理員核准**：選擇此設定以等待系統管理使用者核准後，使用者才能與目的地電腦建立關聯。  

    -   **不允許使用者裝置親和性**：選擇此設定以指定使用者不可與目的地電腦建立關聯。  

     如需使用者裝置親和性的詳細資訊，請參閱 [System Center Configuration Manager 的連結使用者和裝置與使用者裝置親和性](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

-   **網路介面**：指定發佈點從所有網路介面或從特定網路介面回應 PXE 要求。 如果發佈點回應特定網路介面，您必須提供每個網路介面的 MAC 位址。  

-   **指定 PXE 伺服器回應延遲 (秒)**：指定當發佈點上使用多個已啟用 PXE 的發佈點時，發佈點在回應電腦要求前的延遲時間 (以秒為單位)。 根據預設，Configuration Manager PXE 服務點會先回應網路 PXE 的要求。  

> [!NOTE]  
>  您可以使用 PXE 通訊協定來啟動 Configuration Manager 用戶端電腦的作業系統部署。 Configuration Manager 會使用已啟用 PXE 的發佈點站台角色，來起始作業系統部署程序。 啟用 PXE 的發佈點必須經過設定才能：
>
> 1. 回應 Configuration Manager 用戶端在網路上提出的 PXE 開機要求。
> 2. 與 Configuration Manager 基礎結構互動，以判斷要採取的適當部署動作。  

### <a name="multicast"></a>多點傳送  
指定是否要在發佈點上啟用多點傳送。 當您啟用多點傳送時，Configuration Manager 會視需要在伺服器上安裝 Windows 部署服務。  

當您勾選 [啟用多點傳送來同時傳送資料到多個用戶端] 方塊時，請設定下列設定：  

-   **多點傳送連線帳戶**：指定當您針對多點傳送設定 Configuration Manager 資料庫連線時所要使用的帳戶。  

-   **多點傳送位址設定**：指定用於將資料傳送至目的地電腦的 IP 位址。 根據預設，IP 位址可從啟用發佈多點傳送位址的 DHCP 伺服器取得。 根據網路環境不同，您可以指定介於 239.0.0.0 到 239.255.255.255 之間的 IP 位址範圍。  

    > [!IMPORTANT]  
    >  要求作業系統映像的目的地電腦，必須可以存取這些 IP 位址。 確認路由器和防火牆允許目的地電腦和網站伺服器之間的多點傳送流量。  

-   **多點傳送的 UDP 連接埠範圍**：指定使用者資料包通訊協定 (UDP) 連接埠的範圍，其可用於傳送資料至目的地電腦。  

    > [!IMPORTANT]  
    >  要求作業系統映像的目的地電腦必須可以存取 UDP 連接埠。 確認路由器和防火牆允許目的地電腦和網站伺服器之間的多點傳送流量。  

-   **用戶端傳送速率**：選取用於下載資料至目的地電腦的傳送速率。  

-   **用戶端上限**：指定可以從此發佈點下載作業系統的目的地電腦數目上限。  

-   **啟用排程多點傳送**：指定 Configuration Manager 如何控制於何時開始將作業系統部署至目的地電腦。 設定下列選項：  

    -   **工作階段啟動延遲 (分鐘)**：指定 Configuration Manager 在回應第一個部署要求前等待的分鐘數。  

    -   **工作階段大小上限 (用戶端)**：指定必須接收到多少要求，Configuration Manager 才會開始部署作業系統。  

> [!NOTE]  
>  多點傳送部署會藉由同時傳送資料至多個 Configuration Manager 用戶端，而不是透過獨立連線傳送資料的複本至各個用戶端，以保留網路頻寬。 如需如何使用多點傳送部署作業系統的詳細資訊，請參閱[利用 System Center Configuration Manager 使用多點傳送透過網路來部署 Windows](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

### <a name="group-relationships"></a>群組關聯性  

> [!NOTE]  
>  這些選項只有在編輯先前安裝之發佈點的內容時才可用。  

管理成員包含此發佈點的發佈點群組。  

若要新增此發佈點做為現有發佈點群組的成員，請選擇 [新增]。 在 [新增至發佈點群組] 對話方塊的清單中選取現有發佈點群組，然後選擇 [確定]。  

若要從發佈點群組移除此發佈點，請在清單中選取發佈點，然後選擇 [移除]。  

### <a name="content"></a>Content  

> [!NOTE]  
>  這些選項只有在編輯先前安裝之發佈點的內容時才可用。  

管理已發佈至發佈點的內容。 [部署套件] 區段會提供發佈至此發佈點的套件清單。 您可以從清單中選取套件，並執行下列動作：  

-   **驗證**：開始驗證套件中內容檔案完整性的程序。 若要檢視內容驗證程序的結果，請在 [監視] 工作區中展開 [發佈狀態]，然後選擇 [內容狀態] 節點。  

-   **重新發佈**：將套件中的所有內容複製到發佈點，並且覆寫現有檔案。 通常您會使用此動作修復套件中的內容檔案。  

-   **移除**：從發佈點移除套件的內容檔案。  

### <a name="content-validation"></a>內容驗證  
指定是否設定排程驗證發佈點上內容檔案的完整性。 當您依照排程啟用內容驗證時，Configuration Manager 會於排程的時間啟動程序，並驗證發佈點上的所有內容。 您也可以設定內容驗證優先順序。 根據預設，優先順序會設為 [最低] 。  

若要檢視內容驗證程序的結果，請在 [監視] 工作區中展開 [發佈狀態]，然後選擇 [內容狀態] 節點。 每個套件類型的內容 (例如，應用程式、軟體更新套件和開機映像) 都會顯示。  

> [!WARNING]  
>  雖然您是使用電腦的本機時間來指定內容驗證排程，但 Configuration Manager 主控台會使用 UTC 來顯示排程。  

### <a name="boundary-group"></a>界限群組  
管理擁有此指派之發佈點的界限群組。 您可以將界限群組關聯到發佈點。 部署內容期間，用戶端必須存在於與發佈點關聯的界限群組之中，才能將界限群組當成內容的來源位置使用。

此外：

- 在 1610 版之前，您可以勾選 [允許用戶端使用此網站系統做為內容的後援來源位置] 方塊，讓位於這些界限群組以外的用戶端進行後援，並在沒有其他發佈點可用時，使用發佈點作為內容的來源位置。 如需界限群組的詳細資訊，請參閱 [1511、1602 及 1606 版的界限群組](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606)。 如需慣用發佈點，請參閱 [System Center Configuration Manager 中的內容管理基本概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)。

- 使用 1610 版或更新版本，您可以設定界限群組「關聯性」，其定義用戶端可以後援以尋找內容的時機和界限群組。 如需詳細資訊，請參閱[界限群組](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)。


### <a name="schedule"></a>排程  

> [!NOTE]  
>  這些選項只有在編輯先前安裝之發佈點的內容時才可用。  

> [!TIP]  
>  只有在編輯在網站伺服器電腦之遠端發佈點的內容時，才能使用此索引標籤。  

 指定是否設定排程，以限制 Configuration Manager 可將資料傳送至發佈點的時間。  

> [!IMPORTANT]  
>  排程是以傳送端網站的時區為依據，而不是發佈點。  

若要限制資料，請選取期間，然後選擇下列其中一個 [可用性] 設定：  

-   **對所有優先順序開放**：指定 Configuration Manager 可不受限制地傳送資料至發佈點。  

-   **允許中高優先順序**：指定 Configuration Manager 僅將中優先順序和高優先順序的資料傳送至發佈點。  

-   **僅允許高優先順序**：指定 Configuration Manager 僅將高優先順序的資料傳送至發佈點。  

-   **已關閉**：指定 Configuration Manager 不會傳送任何資料至發佈點。  

您可以依優先順序限制資料，或是關閉所選取期間的連線。  

### <a name="rate-limits"></a>速率限制  

> [!NOTE]  
>  這些選項只有在編輯先前安裝之發佈點的內容時才可用。  

> [!TIP]  
>  只有在編輯在網站伺服器電腦之遠端發佈點的內容時，才能使用此索引標籤。  

指定是否設定速率限制，控制 Configuration Manager 將內容傳送至發佈點時使用的網路頻寬。 您可以選擇下列選項：  

-   **傳送至此目的地時無限制**：該選項指定 Configuration Manager 可不受速率限制地傳送內容至發佈點。  

-   **脈衝模式**：該選項指定傳送至發佈點的資料區塊大小。 您也可以指定傳送每個資料區塊之間的時間延遲。 如果您必須經由非常低頻寬的網路連線傳送資料至發佈點，請使用此選項。 例如，您可能限制每五秒傳送 1 KB 的資料，無論於特定時間的連結速度或其使用情形為何。  

-   **限制為指定的每小時最大傳送速率**：指定此設定會讓網站僅使用您設定的時間百分比傳送資料至發佈點。 使用此選項時，Configuration Manager 不會識別網路的可用頻寬，而是會細分可傳送資料的時間。 然後資料會傳送一小段時間，下一個時間片段則不傳送資料。 例如，如果最大速率設為 **50%**，則 Configuration Manager 會在傳輸某個時段的資料之後，於一段相等時段內停止傳送資料。 不會管理實際資料量大小 (或資料區塊大小)。 只會管理傳送資料的時間長度。  
