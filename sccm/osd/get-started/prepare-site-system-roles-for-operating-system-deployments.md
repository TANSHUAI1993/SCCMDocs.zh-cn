---
title: "準備作業系統部署的站台系統角色 | Microsoft Docs"
description: "先設定站台系統角色，再於 System Center Configuration Manager 中部署作業系統。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 11c0f169afebdb071fefb5ce300fd1ae3481a94f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 為作業系統部署準備站台系統角色

*適用於：System Center Configuration Manager (最新分支)*

若要在 System Center Configuration Manager 中部署作業系統，您必須先準備下列需要進行特定設定和考量的站台系統角色。

##  <a name="BKMK_DistributionPoints"></a> 發佈點  
 發佈點站台系統角色包含可供用戶端下載的來源檔案 (例如應用程式內容、軟體更新、作業系統映像和開機映像)。 您可以利用頻寬、節流及排程選項控制內容發佈。  

 您的發佈點數量必須足以支援在電腦上進行作業系統部署。 規劃這些發佈點在階層中的位置也十分重要。 您可以在[內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)中找到大部分的規劃資訊。 不過，關於作業系統部署特有的發佈點仍有些額外規劃考量。  

###  <a name="BKMK_AdditionalPlanning"></a> 發佈點的額外規劃考量  
 以下是發佈點的額外規劃考量：  

-   **如何防止不想要的作業系統部署？**  

     Configuration Manager 不會區分站台伺服器與集合中的其他目的地電腦。 如果您將必要的工作順序部署至包含站台伺服器的集合中，該站台伺服器執行工作順序的方式會與該集合中任何其他電腦執行工作順序的方式相同。 請確定作業系統部署所使用的集合包含您想要執行部署的用戶端。  

     您可以管理高風險工作順序部署的行為。 高風險部署會自動安裝於用戶端上，而且可能會造成不需要的結果。 例如，以「必要」用途部署作業系統的工作順序。 若要降低不需要的高風險部署所帶來的風險，您可以設定部署驗證設定。 如需詳細資訊，請參閱[管理高風險部署的設定](../../protect/understand/settings-to-manage-high-risk-deployments.md)。  

-   **同時可以有多少部電腦從單一發佈點接收作業系統映像？**  

     若要估計您需要多少發佈點，請考慮發佈點的處理速度和磁碟 I/O、網路可用頻寬，以及映像封裝大小對於這些資源的影響。 例如，在 100 MB 的乙太網路上，如果不考慮任何其他伺服器資源因素，一個 4 GB 映像套件在一個小時內最多能夠處理 11 台電腦。  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     如果您必須在特定時間範圍內將作業系統部署至特定數量的電腦，請將映像發佈至適量的發佈點。  

-   **是否可以將作業系統部署至發佈點？**  

     您可以將作業系統部署至發佈點，但必須從不同的發佈點接收作業系統映像。  

###  <a name="BKMK_PXEDistributionPoint"></a> 設定發佈點接受 PXE 要求  
 若要將作業系統部署至發出 PXE 開機要求的 Configuration Manager 用戶端，您必須設定一或多個發佈點來接受 PXE 要求。 在您設定發佈點之後，發佈點將會回應 PXE 開機要求，並判斷要採取的適當部署動作。

> [!IMPORTANT]  
>  [Windows Deployment Services](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) 必須安裝在所有已啟用 PXE 的發佈點上。  

 利用下列程序修改現有的發佈點，讓它能夠接受 PXE 要求。 如需有關安裝新發佈點方式的資訊，請參閱 [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>修改現有發佈點以接受 PXE 要求  

1.  在 Configuration Manager 主控台中，按一下 [系統管理]，並展開 [概觀]，然後按一下 [發佈點]。  

2.  選取要設定的發佈點，然後在 **[首頁]** 索引標籤的 **[內容]** 群組中，按一下 **[內容]**。  

3.  在發佈點的內容頁上，按一下 [PXE]  索引標籤。 選取 **[為用戶端啟用 PXE 支援]**啟用此發佈點的 PXE。  

4.  按一下 **[檢閱 PXE 所需的連接埠]** 對話方塊中的 **[是]** ，確認您想要啟用 PXE。 Configuration Manager 自動在 Windows 防火牆上設定預設連接埠。 如果您使用不同的防火牆，則必須手動設定連接埠。  

    > [!NOTE]  
    >  如果在同一部伺服器上安裝 WDS 和 DHCP，您必須設定 WDS 接聽不同的連接埠 (因為 DHCP 接聽相同的連接埠)。 如需詳細資訊，請參閱[當您在同一部伺服器上有 WDS 和 DHCP 時的考量](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP)。  

5.  選取 **[允許此發佈點回應傳入的 PXE 要求]** 來啟用 WDS，以回應傳入的 PXE 服務要求。 您可以使用此設定來啟用和停用服務，而不需移除發佈點上的 PXE 功能。  

6.  若要將作業系統部署到不受 Configuration Manager 管理的電腦上，請選取 [啟用未知電腦支援]。  

7.  選取 **[電腦使用 PXE 時需要密碼]**，然後指定強式密碼為您的 PXE 部署提供額外的安全性。  

8.  在 **[使用者裝置親和性]** 清單中，選擇發佈點讓使用者與 PXE 部署的目的地電腦產生關聯的方式。  

    -   選取 **[不使用使用者裝置親和性]**，使用者與目的地電腦就不會產生關聯。  

    -   選取 [手動核准允許使用者裝置親和性]  ，會在使用者與目的地電腦產生關聯之前等候管理使用者核准。  

    -   選取 [自動核准允許使用者裝置親和性]  ，會自動將使用者與目的地電腦產生關聯，而不等候核准。  

     如需詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

9. 指定發佈點從所有網路介面或從特定網路介面回應 PXE 要求。 如果選擇讓發佈點回應特定的網路介面，請提供每個網路介面的 MAC 位址。  

10. 指定使用多個啟用 PXE 的發佈點時，發佈點回應電腦要求之前的延遲時間 (以秒為單位)。  

11. 按一下 [確定]  更新發佈點的內容。  

###  <a name="BKMK_RamDiskTFTP"></a> 自訂支援 PXE 之發佈點的相關 RamDisk TFTP 區塊大小和視窗大小  
您可以為支援 PXE 的發佈點自訂 RamDisk TFTP 區塊大小，而從 Configuration Manager 1606 版開始，也可以自訂視窗大小。 如果您已自訂網路，可能會導致開機映像下載因發生逾時錯誤而失敗，因為區塊或視窗大小太大。 自訂 RamDisk TFTP 區塊大小和視窗大小可讓您在使用 PXE 來滿足特定的網路需求時，將 TFTP 流量最佳化。   
您將需要在您的環境中測試自訂的設定，以確定最有效率的設定是哪一個。  

-   **TFTP 區塊大小**︰區塊大小是伺服器傳送給下載檔案之用戶端的資料封包大小 (如 RFC 2347 所述)。 區塊大小越大，伺服器傳送的封包就越少，因此伺服器與用戶端之間的來回延遲也較少。 不過，較大的區塊大小會導致封包分散，而大多數 PXE 用戶端實作並不支援分散的封包。  

-   **TFTP 視窗大小**：TFTP 針對每個傳送的資料區塊都會要求一個認可 (ACK) 封包。 伺服器在收到上一個區塊的 ACK 封包之前，不會傳送順序中的下一個區塊。 TFTP 視窗化是「Windows 部署服務」中的一項功能，可讓您定義填滿視窗所需的資料區塊數量。 伺服器會以背對背的方式傳送資料區塊，直到填滿視窗為止，然後用戶端會傳送 ACK 封包。 增加此視窗大小可降低用戶端與伺服器之間的來回延遲數，並縮短下載開機映像所需的整體時間。  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>修改 RamDisk TFTP 視窗大小  

-   新增支援 PXE 之發佈點的下列相關登錄機碼以自訂 RamDisk TFTP 視窗大小：  

     **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    名稱：RamDiskTFTPWindowSize  

     **類型**：REG_DWORD  

     **值**：&lt;自訂視窗大小>  

 預設值為 1 (1 個資料區塊填滿視窗)  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>修改 RamDisk TFTP 區塊大小  

-   新增支援 PXE 之發佈點的下列相關登錄機碼以自訂 RamDisk TFTP 視窗大小：  

     **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    名稱：RamDiskTFTPBlockSize  

     **類型**：REG_DWORD  

     **值**：&lt;自訂區塊大小>  

 預設值為 4096 (4k)。  


###  <a name="BKMK_DPMulticast"></a> 設定發佈點支援多點傳送  
 多點傳送是一種網路最佳化方法，如果可能有多個用戶端同時下載同一個作業系統映像，即可以在發佈點上使用這種方法。 使用多點傳送時，多部電腦可以同時下載由發佈點多點傳送的作業系統映像，不需由發佈點一一透過個別連線傳送資料複本至每個用戶端。 您至少必須設定一個發佈點才能支援多點傳送。 如需詳細資訊，請參閱[使用多點傳送透過網路來部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

 您必須將發佈點設定為支援多點傳送，才能部署作業系統。 利用下列程序，將現有的發佈點修改為支援多點傳送。 如需如何安裝新發佈點的資訊，請參閱[安裝和設定發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。

#### <a name="to-enable-multicast-for-a-distribution-point"></a>啟用發佈點的多點傳送  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [概觀] ，然後選取 [發佈點]  節點。  

3.  選取您要用來多點傳送作業系統映像的發佈點。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  選取 [多點傳送]  索引標籤，並設定下列選項：  

    -   **啟用多點傳送**：您必須選取這個選項，讓發佈點支援多點傳送。  

    -   **多點傳送連線帳戶**：指定連線到站台資料庫的帳戶。  

    -   **多點傳送位址設定**：指定用於將資料傳送至目的地電腦的 IP 位址。 根據預設，IP 位址可從啟用發佈多點傳送位址的 DHCP 伺服器取得。 根據網路環境不同，您可以指定介於 239.0.0.0 和 239.255.255.255 之間的 IP 位址範圍。  

        > [!IMPORTANT]  
        >  要求作業系統映像的目的地電腦，必須可以存取這些 IP 位址。 這表示目的地電腦和站台伺服器之間的路由器和防火牆，必須設定為允許多點傳送流量。  

    -   **UDP 連接埠範圍**：指定要將資料傳送至目的地電腦的 UDP 連接埠範圍。  

        > [!IMPORTANT]  
        >  要求作業系統映像的目的地電腦，必須可以存取這些連接埠。 這表示目的地電腦和站台伺服器之間的路由器和防火牆，必須設定為允許多點傳送流量。  

    -   **啟用排程多點傳送**：指定 Configuration Manager 如何控制於何時開始將作業系統部署至目的地電腦。 按一下 [啟用排程多點傳送] ，然後選取下列選項。  

         在 [工作階段啟動延遲] 方塊中，指定在回應第一個部署要求前 Configuration Manager 等待的分鐘數。  

         在 [最小工作階段大小] 方塊中，指定必須接收到多少要求，Configuration Manager 才會開始部署作業系統。  

    -   **傳送速率**：選取下載資料至目的地電腦的傳送速率。  

    -   **用戶端上限**：指定可以從此發佈點下載作業系統的目的地電腦數目上限。  

6.  按一下 [ **確定**]。  

##  <a name="BKMK_StateMigrationPoints"></a> 狀態移轉點  
 狀態移轉點會儲存在某台電腦上擷取到的使用者狀態資料，再將資料還原至另一台電腦。 不過，當您擷取同一部電腦的作業系統部署使用者設定時 (例如您在此重新整理作業系統之目的地電腦的部署)，您可以選擇使用永久連結將資料儲存在同一部電腦，還是使用狀態移轉點。 進行部分電腦部署時，若要建立狀態存放區，Configuration Manager 會自動在狀態存放區和目的地電腦之間建立關聯。 規劃狀態移轉點時，請考慮下列因素。  

### <a name="user-state-size"></a>使用者狀態的大小  
 使用者狀態的大小會直接影響狀態移轉點的磁碟儲存體及移轉時的網路效能。 請考慮使用者狀態的大小以及要移轉的電腦數量。 另外也請一併考慮要從電腦移轉哪些設定。 例如，如果已經將 [我的文件]  備份到伺服器中，那麼您在部署映像時也許就不需要移轉該資料夾。 避免沒有必要的移轉可以盡可能減少使用者狀態的整體大小，同時也能降低使用者狀態大小對於網路效能及狀態移轉點磁碟儲存體可能造成的影響。  

### <a name="user-state-migration-tool"></a>使用者狀態移轉工具  
 若要在部署作業系統期間擷取及還原使用者狀態，您必須使用指向 USMT 來源檔案的使用者狀態移轉工具 (USMT) 套件。 Configuration Manager 會在 Configuration Manager 主控台的 [軟體程式庫] > [應用程式管理] > [套件] 中自動建立這個套件。 Configuration Manager 使用 Windows 評定及部署套件 (Windows ADK) 發佈的 USMT 10.0 來擷取某個作業系統的使用者狀態，然後在另一個作業系統上還原它。  

 如需不同的 USMT 10.0 移轉案例描述，請參閱 [常見移轉案例](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)。  

### <a name="retention-policy"></a>保留原則  
 當您設定狀態移轉點時，可以指定存放在移轉點之使用者狀態資料的保存時間長度。 存放在移轉點之使用者狀態的保存時間長度取決於以下兩項考慮因素：  

-   所存放的資料對於磁碟儲存體的影響。  

-   可能必須保存該資料，預防日後出現必須再次移轉該資料的需求。  

 狀態移轉會發生在兩個階段中：擷取資料以及還原資料。 擷取資料時會收集使用者狀態資料，並將其儲存在狀態移轉點中。 還原資料時，則會從狀態移轉點擷取使用者狀態資料、寫入目的地電腦中，然後再由 [釋放狀態存放區]  工作順序分階段釋放所存放的資料。 保留計時器會在釋放資料後啟動。 如果選取立即刪除移轉資料的選項，會在釋放使用者狀態後隨即將其刪除。 如果選取在特定期限內保留資料的選項，則會在釋放狀態資料起經過一段特定時間後將其刪除。 您所設定的保留期間越久，需要的磁碟空間越大。  

### <a name="select-drive-to-store-user-state-migration-data"></a>選取儲存使用者狀態移轉資料的磁碟機  
 設定狀態移轉點時，必須在伺服器上指定用於存放使用者狀態移轉資料的磁碟機。 您需從固定的磁碟機清單中選取磁碟機。 不過，其中部分磁碟機可能代表不可寫入磁碟機，例如光碟機或非網路共用磁碟機。 此外，某些磁碟機代號可能無法對應於電腦中的任何磁碟機。 設定狀態移轉點時必須指定可寫入的共用磁碟機。  

### <a name="configure-a-state-migration-point"></a>設定狀態移轉點  
 您可以使用下列方法，將狀態移轉點設定為儲存使用者狀態資料：  

-   使用 [建立站台系統伺服器精靈]  ，為狀態管理點建立新的站台系統伺服器。  

-   使用 [新增站台系統角色精靈]  ，將狀態移轉點新增至現有伺服器。  

 當您使用這些精靈時，系統會提示您為狀態移轉點提供下列資訊：  

-   用於儲存使用者狀態資料的資料夾。  

-   狀態移轉點上可儲存資料的用戶端數目上限。  

-   狀態移轉點用於儲存使用者狀態資料的最小可用空間。  

-   角色的刪除原則。 您可以指定是要在還原於電腦後立刻刪除使用者狀態資料，或是在將使用者資料還原到電腦後的特定天數後再將其刪除。  

-   狀態移轉點是否只回應還原使用者狀態資料的要求。 當您啟用此選項時，將無法使用狀態移轉點來儲存使用者狀態資料。  

 如需安裝站台系統角色的步驟，請參閱[新增站台系統角色](../../core/servers/deploy/configure/add-site-system-roles.md)。  
