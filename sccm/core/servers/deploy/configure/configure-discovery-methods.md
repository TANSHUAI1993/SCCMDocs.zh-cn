---
title: "設定探索 | Microsoft Docs"
description: "設定在 Configuration Manager 站台上執行的探索方法，以尋找您可以從網路基礎結構與 Active Directory 管理的資源。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 34a539ceaea6b070f81a28d2c0a9ce388e26cfeb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>設定 System Center Configuration Manager 的探索方法

*適用於︰System Center Configuration Manager (最新分支)*


設定在 System Center Configuration Manager 站台上執行的探索方法，以尋找您可以從網路基礎結構與 Active Directory 管理的資源。 這需要您啟用及設定搜尋環境要使用的每個方法。 (您也可以使用與啟用相同的程序停用方法。)唯一的例外是活動訊號探索和伺服器探索︰  

-   根據預設，安裝 Configuration Manager 主要站台時，即已啟用活動訊號探索，並已設定依基本排程執行。 讓活動訊號探索保持啟用狀態是個不錯的想法，因為這樣能確保裝置的探索資料記錄 (DDR) 是最新的。 如需活動訊號探索的詳細資訊，請參閱[活動訊號相關訊息](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。  

-   伺服器探索是自動的探索方法，它能尋找作為站台系統的電腦。 不過您無法設定或停用。  

**啟用可設定的探索方法︰**  
 > [!NOTE]  
 > 下列資訊不適用於 Azure Active Directory 使用者探索。 請參閱本主題後面的[設定 Azure AD 使用者探索](#azureaadisc)。

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  為您要啟用探索的站台選取探索方法。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]，然後在 [一般] 索引標籤上勾選 [啟用 &lt;探索方法\>] 方塊。  

     如果此方塊已勾選，取消勾選方塊即可停用探索方法。  

4.  選擇 [確定] 儲存設定。  


##  <a name="BKMK_ConfigADForestDisc"></a> 設定 Active Directory 樹系探索  
若要完成 Active Directory 樹系探索的設定，您必須在下面兩個位置進行設定：  

-   在 [探索方法] 節點中，您可以︰

    - 啟用此探索方法。
    - 設定輪詢排程。
    - 選取探索是否要為 Active Directory 站台和它發現的子網路自動建立界限。  

-   在 [Active Directory 樹系] 節點中，您可以︰

    - 新增您想要探索的樹系。
    - 針對 Active Directory 站台和該樹系中的子網路啟用探索。
    - 配置讓 Configuration Manager 站台將其站台資訊發佈至樹系的設定。
    - 指派帳戶以當做每個樹系的 Active Directory 樹系帳戶。  

利用下列程序啟用 Active Directory 樹系探索，以及設定個別樹系搭配 Active Directory 樹系探索使用。  

#### <a name="to-enable-active-directory-forest-discovery"></a>若要啟用 Active Directory 樹系探索  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  為您要設定探索的站台選取 [Active Directory 樹系探索] 方法。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  在 [一般] 索引標籤上，勾選方塊以啟用探索。 您也可以在現在設定探索，稍後再返回啟用探索。  

5.  指定選項以建立所探索位置的站台界限。  

6.  指定探索執行的排程。  

7.  當您完成設定此站台的 Active Directory 樹系探索時，選擇 [確定] 儲存設定。  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>若要設定 Active Directory 樹系探索的樹系  

1.  在 [系統管理] 工作區中，選擇 [Active Directory 樹系]。 如果 Active Directory 樹系探索之前已執行，您會在結果窗格中看見每個探索到的樹系。 當 Active Directory 樹系探索執行時，會探索本機樹系和任何信任的樹系。 只有不受信任的樹系必須手動新增。  

    -   若要設定先前探索到的樹系，請在結果窗格中選取樹系。 然後在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容] 以開啟該樹系內容。 繼續進行步驟 3。  

    -   若要設定未列出的新樹系，請在 [首頁] 索引標籤的 [建立] 群組中，選擇 [新增樹系] 開啟 [新增樹系] 對話方塊。 繼續進行步驟 3。  

2.  在 [一般] 索引標籤上，完成您要探索之樹系的設定，然後指定 [Active Directory 樹系帳戶]。  

    > [!NOTE]  
    >  Active Directory 樹系探索需要通用帳戶，才能探索及發佈至不受信任的樹系。 如果您未使用網站伺服器的電腦帳戶，就只能選取通用帳戶。  

3.  如果您打算讓站台將站台資料發佈至此樹系，可在 [發佈] 索引標籤上完成發佈至此樹系的設定。  

    > [!NOTE]  
    >  如果您讓站台發佈至樹系，必須為 Configuration Manager 延伸該樹系的 Active Directory 架構。 Active Directory 樹系帳戶必須具有該樹系中系統容器的完全控制權限。  

4.  當您完成此樹系的設定以搭配使用 Active Directory 樹系探索時，選擇 [確定] 儲存設定。  

##  <a name="BKMK_ConfigADDiscGeneral"></a> 設定電腦、使用者或群組的 Active Directory 探索  
 使用以下各節中的資訊設定電腦、使用者或群組的探索。 您將使用這些探索方法︰  

-   Active Directory 群組探索  

-   Active Directory 系統探索  

-   Active Directory 使用者探索  

> [!NOTE]  
>  本節中的資訊不適用於 Active Directory 樹系探索。  

 雖然每一種探索方法各自獨立，但是有一些類似的選項。 如需這些設定選項的詳細資訊，請參閱[群組、系統和使用者探索的共用選項](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared)。  

> [!WARNING]  
>  每一種探索方法的 Active Directory 輪詢可能產生相當大的網路流量。 請考慮將每一種探索方法排程在此網路流量不會對網路之業務使用造成負面影響的時段。  

#### <a name="to-configure-active-directory-group-discovery"></a>若要設定 Active Directory 群組探索  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  為您要設定探索的站台選擇 [Active Directory 群組探索] 方法。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  在 [一般] 索引標籤上，勾選方塊以啟用探索。 您也可以在現在設定探索，稍後再返回啟用探索。  

5.  選擇 [新增] 設定探索範圍，選擇 [群組] 或 [位置]，然後在 [新增群組] 或 [新增 Active Directory 位置] 對話方塊中完成下列設定：  

    1.  為此探索範圍指定 [名稱]  。  

    2.  指定要搜尋的 [Active Directory 網域]  或 [位置]  ：  

        -   如果您選擇 [群組]，請指定一個或多個要探索的 Active Directory 群組。  

        -   如果您選擇 [位置]，請指定 Active Directory 容器做為要探索的位置。 您也可以針對此位置啟用 Active Directory 子容器的遞迴搜尋。  

    3.  指定用來搜尋此探索範圍的 [Active Directory 群組探索帳戶]  。  

    4.  選擇 [確定] 儲存探索範圍設定。  

6.  針對您要定義的每個額外的探索範圍重複步驟 6。  

7.  在 [輪詢排程]  索引標籤上，設定完整探索輪詢排程和差異探索。  

8.  您可以選擇性地在 [選項] 索引標籤上設定選項，從探索中篩選出或排除過時的電腦記錄，以及探索發佈群組的成員資格。  

    > [!NOTE]  
    >  根據預設，Active Directory 群組探索只會探索安全性群組的成員資格。  

9. 當您完成設定此站台的 Active Directory 群組探索時，選擇 [確定] 儲存設定。  

#### <a name="to-configure-active-directory-system-discovery"></a>若要設定 Active Directory 系統探索  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  為您要設定探索的站台選取方法。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  在 [一般] 索引標籤上，勾選方塊以啟用探索。 您也可以在現在設定探索，稍後再返回啟用探索。  

5.  選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif) 以指定新的 Active Directory 容器。 在 [Active Directory 容器] 對話方塊方塊中，完成下列設定︰  

    1.  指定要搜尋的一個或多個位置。  

    2.  針對每個位置指定變更搜尋行為的選項。  

    3.  針對每個位置指定要做為 [Active Directory 探索帳戶] 使用的帳戶。  

        > [!TIP]  
        >  您可以針對指定的每個位置，設定一組探索選項和一個唯一的 Active Directory 探索帳戶。  

    4.  選擇 [確定] 儲存 Active Directory 容器設定。  

6.  在 [輪詢排程]  索引標籤上，設定完整探索輪詢排程和差異探索。  

7.  您可以選擇性地在 [Active Directory 屬性]  索引標籤上，針對您要探索的電腦設定其他 Active Directory 屬性。 預設物件屬性也會列出。  

8.  您可以選擇性地在 [選項] 索引標籤上設定選項，從探索中篩選出或排除過時的電腦記錄。  

9. 當您完成設定此站台的 Active Directory 系統探索時，選擇 [確定] 儲存設定。  

#### <a name="to-configure-active-directory-user-discovery"></a>若要設定 Active Directory 使用者探索  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  為您要設定探索的站台選擇 [Active Directory 使用者探索] 方法。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  在 [一般] 索引標籤上，勾選方塊以啟用探索。 您也可以在現在設定探索，稍後再返回啟用探索。  

5.  選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif) 以指定新的 Active Directory 容器。 在 [Active Directory 容器] 對話方塊方塊中，完成下列設定︰  

    1.  指定要搜尋的一個或多個位置。  

    2.  針對每個位置指定變更搜尋行為的選項。  

    3.  針對每個位置指定要做為 [Active Directory 探索帳戶] 使用的帳戶。  

        > [!NOTE]  
        >  您可以針對指定的每個位置，設定一組唯一的探索選項和一個唯一的 Active Directory 探索帳戶。  

    4.  選擇 [確定] 儲存 Active Directory 容器設定。  

6.  在 [輪詢排程]  索引標籤上，設定完整探索輪詢排程和差異探索。  

7.  您可以選擇性地在 [Active Directory 屬性]  索引標籤上，針對您要探索的電腦設定其他 Active Directory 屬性。 預設物件屬性也會列出。  

8.  當您完成設定此站台的 Active Directory 使用者探索時，選擇 [確定] 儲存設定。  

## <a name="azureaadisc"></a>設定 Azure AD 使用者探索
從 1706 版開始，當您將 Configuration Manager 連線至 [Azure 訂用帳戶與 Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) 時，可以設定 Azure Active Directory 使用者探索。

Azure AD 使用者探索可設定為*雲端管理*的一部分。 *設定要與 Configuration Manager 搭配使用的 Azure 服務*主題的[建立要與 Configuration Manager 搭配使用的 Azure Web 應用程式](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp)中有詳細的程序說明。




##  <a name="BKMK_ConfigHBDisc"></a> 設定活動訊號探索  
 根據預設，活動訊號探索會在您安裝 Configuration Manager 主要站台時啟用。 因此，您只需要在不想使用每七天的預設值時，設定用戶端將活動訊號探索資料記錄傳送至管理點的排程即可。  

> [!NOTE]  
>  如果在相同站台上，用戶端推入安裝和 [清除安裝旗標]  的站台維護工作都啟用，請將活動訊號探索的排程設為少於 [清除安裝旗標]  站台維護工作的 [用戶端重新探索期間]  。 如需站台維護工作的詳細資訊，請參閱 [Maintenance tasks for System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md) (System Center Configuration Manager 的維護工作)。  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>若要設定活動訊號探索排程  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  針對您要設定活動訊號探索的站台選擇 [活動訊號探索]。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  設定用戶端提交活動訊號探索資料記錄的頻率，然後選擇 [確定] 儲存設定。  

##  <a name="BKMK_ConfigNetworkDisc"></a> 設定網路探索  
 使用以下各節中的資訊可幫助您設定網路探索。  

###  <a name="BKMK_AboutConfigNetworkDisc"></a> 關於設定網路探索  
 在您設定網路探索之前，必須先瞭解下列資訊：  

-   可用的網路探索層級  

-   可用的網路探索選項  

-   限制網路上的網路探索  

如需詳細資訊，請參閱[關於網路探索](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork)。  

 下面各節提供有關一般網路探索設定的資訊。 您可以設定同一次探索執行期間使用的其中一項或多項設定。 如果您使用多項設定，則必須針對可能影響探索結果的互動進行規劃。  

 例如，您可能想要探索所有使用特定 SNMP 社群名稱的簡易網路管理通訊協定 (SNMP) 裝置。 此外，針對同一次探索執行，您可能會停用特定子網路上的探索。 當探索執行時，網路探索不會在已停用的子網路上探索所指定社群名稱的 SNMP 裝置。  

####  <a name="BKMK_DetermineNetTopology"></a> 判斷您的網路拓撲  
 您可以使用拓撲專屬探索對應您的網路。 此類探索不會探索潛在用戶端。 拓撲專屬網路探索依賴 SNMP。  

 對應網路拓撲時，您必須設定 [網路探索內容] 對話方塊中 [SNMP] 索引標籤上的 [躍點數上限]。 只需幾個躍點，便有助於控制探索執行時所使用的網路頻寬。 進一步探索網路時，您可以增加躍點數以深入瞭解您的網路拓撲。  

 瞭解網路拓撲之後，您便可以在藉由可用設定限制網路探索可搜尋之網路區段的同時，將網路探索的其他內容設定為探索潛在用戶端及其作業系統。  

####  <a name="BKMK_LimitBySubnet"></a> 使用子網路限制搜尋  
 您可以將網路探索設定為在探索執行期間搜尋特定子網路。 根據預設，網路探索會搜尋執行探索的伺服器子網路。 您設定與啟用的其他任何子網路，只能套用於 SNMP 和動態主機設定通訊協定 (DHCP) 搜尋選項。 當網路探索搜尋網域時，並不會受到子網路設定的限制。  

 如果您在 [網路探索內容]  對話方塊中的 [子網路]  索引標籤上指定一個或多個子網路，則只會搜尋標記為 [已啟用]  的子網路。  

 當您停用子網路時，該子網路便會從探索排除，並且會套用以下條件：  

-   SNMP 為主的查詢無法在子網路上執行。  

-   DHCP 伺服器不會用位於子網路的資源清單來回覆。  

-   網域為主的查詢可以探索位於子網路的資源。  

####  <a name="BKMK_SearchByDomain"></a> 搜尋特定網域  
 您可以將網路探索設定為在探索執行期間，搜尋特定網域或一組網域。 根據預設，網路探索會搜尋執行探索的本機伺服器網域。  

 如果您在 [網路探索內容]  對話方塊中的 [網域]  索引標籤上指定一個或多個網域，則只會搜尋標記為 [已啟用]  的網域。  

 當您停用子網路時，該網路便會從探索排除，並且會套用以下條件：  

-   網路探索不會查詢該網域中的網域控制站。  

-   SNMP 為主的查詢仍可在網域中的子網路上執行。  

-   DHCP 伺服器仍可用位於網域中的資源清單來回覆。  

####  <a name="BKMK_LimitBySNMPname"></a> 使用 SNMP 群體名稱限制搜尋  
 您可以將網路探索設定為在探索執行期間，搜尋特定 SNMP 群體或一組群體。 預設為設定 [公用]  群體名稱以供使用。  

 網路探索會使用群體名稱來存取等於 SNMP 裝置的路由器。 路由器會提供網路探索有關其他路由器，以及連結至第一個路由器的子網路的資訊。  

> [!NOTE]  
>  SNMP 群體名稱和密碼類似。 網路探索只能從您已為其指定群體名稱的 SNMP 裝置取得資訊。 各個 SNMP 裝置皆可擁有自己的群體名稱，但是通常數個裝置會共用相同的群體名稱。 此外，多數的 SNMP 裝置皆有預設的 [公用] 群體名稱。 不過，有些組織會從其裝置刪除 [公用] 群體名稱，以當作安全預防措施。  

 如果 [網路探索內容] 對話方塊中的 [SNMP] 索引標籤上顯示多個 SNMP 群體，則網路探索會按照這些群體顯示的順序進行搜尋。 請確定最常使用的名稱位於清單頂端，如此有助於將嘗試使用不同名稱連絡裝置所產生的網路流量減到最低。  

> [!NOTE]  
>  除了使用 SNMP 群體名稱之外，您也可以指定特定 SNMP 裝置的 IP 位址或可解析名稱。 您可以在 [網路探索內容] 對話方塊的 [SNMP 裝置] 索引標籤上進行。  

####  <a name="BKMK_SearchByDHCP"></a> 搜尋特定的 DHCP 伺服器  
 您可以將網路探索設定為使用特定 DHCP 伺服器或多個伺服器，在探索執行期間探索 DHCP 用戶端。  

 網路探索會搜尋您在 [網路探索內容]  對話方塊中的 [DHCP]  索引標籤上指定的各個 DHCP 伺服器。 如果執行探索的伺服器是租用 DHCP 伺服器的 IP 位址，您可以勾選 [包含設定站台伺服器使用的 DHCP 伺服器] 方塊，將探索設定為搜尋該 DHCP 伺服器。  

> [!NOTE]  
>  若要成功設定網路探索中的 DHCP 伺服器，您的環境必須支援 IPv4。 您不能將網路探索設定為在原生 IPv6 環境中使用 DHCP 伺服器。  

###  <a name="BKMK_HowToConfigNetDisc"></a> 如何設定網路探索  
 使用以下程序，先只探索您的網路拓撲，然後使用一個或多個可用的網路探索選項，將網路探索設定為探索潛在用戶端。  

##### <a name="to-determine-your-network-topology"></a>判斷您的網路拓撲  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  針對您要執行網路探索的站台選擇 [網路探索]。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

    -   在 [一般] 索引標籤上，勾選 [啟用網路探索] 方塊，然後從 [探索類型] 選項選擇 [拓撲]。  

    -   在 [子網路] 索引標籤上，勾選 [搜尋本機子網路] 方塊。  

        > [!TIP]  
        >  如果您知道組成網路的特定子網路，您可以取消勾選 [搜尋本機子網路] 方塊，然後使用 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif) 新增您要搜尋的特定子網路。 若是大型網路，通常最好是一次只搜尋一個或兩個子網路，如此才能將網路頻寬的使用量減到最少。  

    -   在 [網域] 索引標籤上，勾選 [搜尋本機網域] 方塊。  

    -   在 [SNMP]  索引標籤上，使用 [躍點數上限]  下拉式清單指定網路探索可用多少路由器躍點對應您的拓撲。  

        > [!TIP]  
        >  當您首次對應網路拓撲時，只要設定幾個路由器躍點就能將網路頻寬的使用量減到最少。  

4.  在 [排程] 索引標籤上，選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif) 以設定執行網路探索的排程。  

    > [!NOTE]  
    >  您不能將不同的探索設定指派至個別的網路探索排程。 每次執行網路探索時，皆會使用目前的探索設定。  

5.  選擇 [確定] 接受設定。 網路探索會在排定的時間執行。  

##### <a name="to-configure-network-discovery"></a>設定網路探索  

1.  在 Configuration Manager 主控台中選擇 [管理] > [階層設定]，然後選擇 [探索方法]。  

2.  針對您要執行網路探索的站台選擇 [網路探索]。  

3.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

4.  在 [一般] 索引標籤上，勾選 [啟用網路探索] 方塊，然後從 [探索類型] 選項選取您要執行的探索類型。  

5.  若要將探索設定為搜尋子網路，請選擇 [子網路] 索引標籤，然後設定以下一個或多個選項：  

    -   若要在執行探索的本機電腦子網路上執行探索，請勾選 [搜尋本機子網路] 方塊。  

    -   若要搜尋特定子網路，請確認子網路列在 [要搜尋的子網路] 中，且 [搜尋] 值為 [已啟用]：  

        1.  如果未列出子網路，請選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif)。 在 [新增子網路指派] 對話方塊中，輸入 [子網路] 與 [遮罩] 資訊，然後選擇 [確定]。 預設為啟用新的子網路以進行搜尋。  

        2.  若要變更所列子網路的 [搜尋] 值，請選取子網路，然後選擇 [切換] 圖示，將值切換為 [停用] 或 [啟用]。  

6.  若要將探索設定為搜尋網域，請選擇 [網域] 索引標籤，然後設定以下一個或多個選項：  

    -   若要在執行探索的電腦網域上執行探索，請勾選 [搜尋本機網域] 方塊。  

    -   若要搜尋特定網域，請確認網域列在 [網域] 中，且 [搜尋] 值為 [已啟用]：  

        1.  如果未列出網域，請選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif)。 在 [網域內容] 對話方塊中輸入 [網域] 資訊，然後選擇 [確定]。 預設為啟用新的網域以進行搜尋。  

        2.  若要變更所列網域的 [搜尋] 值，請選取網域，然後選擇 [切換] 圖示，將值切換為 [停用] 或 [啟用]。  

7.  若要將探索設定為搜尋 SNMP 裝置的特定 SNMP 群體名稱，請選擇 [SNMP] 索引標籤，然後設定以下一個或多個選項：  

    -   若要將 SNMP 群體名稱新增至 [SNMP 群體名稱] 清單，請選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif)。 在 [新增 SNMP 群體名稱] 對話方塊中，指定 SNMP 群體的 [名稱]，然後選擇 [確定]。  

    -   若要移除 SNMP 群體名稱，請選取該群體名稱，然後選擇 [刪除] 圖示 ![[刪除] 圖示](media/Disc_delete_Icon.gif)。  

    -   若要調整 SNMP 群體名稱的搜尋順序，請選取群體名稱，然後選擇 [將項目往上移] 圖示 ![[上移] 圖示](media/Disc_moveUp_Icon.gif) 或 [將項目往下移] 圖示 ![[下移] 圖示](media/Disc_moveDown_Icon.gif)。 執行探索時，會以由上向下的順序搜尋群體名稱。 請謹記下列重點。

        > [!NOTE]  
        >  網路探索會使用 SNMP 群體名稱來存取等於 SNMP 裝置的路由器。 路由器會通知網路探索有關其他路由器，以及連結至第一個路由器的子網路。  

        -   SNMP 群體名稱和密碼類似。  

        -   網路探索只能從您已為其指定群體名稱的 SNMP 裝置取得資訊。  

        -   各個 SNMP 裝置皆可擁有自己的群體名稱，但是通常數個裝置會共用相同的群體名稱。  

        -   多數的 SNMP 裝置皆有預設的 [公用] 群體名稱。 如果您不知道其他任何群體名稱，可以使用該名稱。 不過，有些組織會從其裝置刪除 [公用]  群體名稱，以當作安全預防措施。  

8.  若要設定 SNMP 使用的路由器躍點數上限，請選擇 [SNMP] 索引標籤，然後從 [躍點數上限] 下拉式清單選取躍點數。  

9. 若要設定 SNMP 裝置，請選擇 [SNMP 裝置] 索引標籤。 如果未列出裝置，請選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif)。 在 [新增 SNMP 裝置] 對話方塊中，指定 SNMP 裝置的 IP 位址或裝置名稱，然後選擇 [確定]。  

    > [!NOTE]  
    >  如果指定裝置名稱，Configuration Manager 必須能夠將 NetBIOS 名稱解析為 IP 位址。  

10. 若要將探索設定為查詢 DHCP 用戶端的特定 DHCP 伺服器，請選擇 [DHCP] 索引標籤，然後設定以下一個或多個選項：  

    -   若要在執行探索的電腦上查詢 DHCP 伺服器，請勾選 [永遠使用站台伺服器的 DHCP 伺服器] 方塊。  

        > [!NOTE]  
        >  若要使用此選項，伺服器必須租用 DHCP 伺服器的 IP 位址，且無法使用靜態 IP 位址。  

    -   若要查詢特定 DHCP 伺服器，請選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif)。 在 [新增 DHCP 伺服器] 對話方塊中，指定 DHCP 伺服器的 IP 位址或伺服器名稱，然後選擇 [確定]。  

        > [!NOTE]  
        >  如果指定伺服器名稱，Configuration Manager 必須能夠將 NetBIOS 名稱解析為 IP 位址。  

11. 若要設定探索執行的時間，請選擇 [排程] 索引標籤，然後選擇 [新增] 圖示 ![[新增] 圖示](media/Disc_new_Icon.gif)，設定執行網路探索的排程。  

     您可以設定多個週期性排程和多個非週期性排程。  

    > [!NOTE]  
    >  如果同時在 [排程] 索引標籤處顯示多個排程，所有排程會按照排程上指示的設定時間執行網路探索。 對於週期性排程也是如此。  

12. 選擇 [確定] 儲存設定。  

###  <a name="BKMK_HowToVerifyNetDisc"></a> 如何確認網路探索是否已完成  
 完成網路探索所需的時間，會因各種不同因素而有所不同。 這些可能包括以下一種或多種因素：  

-   網路的大小  

-   網路的拓撲  

-   設定為尋找網路中路由器的躍點數目上限  

-   執行的探索類型  

由於網路探索不會在探索完成時產生建立警示訊息，您可以利用下列程序確認探索在何時完成。  

##### <a name="to-verify-that-network-discovery-has-finished"></a>確認網路探索已完成  

1.  在 Configuration Manager 主控台中，選擇 [監視]。  

2.  在 [監視] 工作區中，展開 [系統狀態]，然後選擇 [狀態訊息查詢]。  

3.  選擇 [所有狀態訊息]。  

4.  在 [首頁] 索引標籤的 [狀態訊息查詢] 群組中，選擇 [顯示訊息]。  

5.  在 [選取日期和時間] 下拉式清單中，選取包含探索何時開始的數值，然後選擇 [確定] 以開啟 [Configuration Manager 狀態訊息檢視器]。  

    > [!TIP]  
    >  您也可以使用 [指定日期和時間]  選項以選取您執行探索的特定日期和時間。 如果您在特定日期執行網路探索，並且只想要擷取該日期的訊息時，此選項就很有用。  

6.  若要驗證網路探索是否完成，請搜尋包含下列詳細資料的狀態訊息：  

    -   訊息識別碼: **502**  

    -   元件: **SMS_NETWORK_DISCOVERY**  

    -   描述： **此元件已停止**  

    如果未出現此狀態訊息，表示網路探索尚未完成。  

7.  若要在網路探索開始時進行驗證，請搜尋包含下列詳細資料的狀態訊息：  

    -   訊息識別碼: **500**  

    -   元件: **SMS_NETWORK_DISCOVERY**  

    -   描述： **此元件已啟動**  

    這項資訊會確認網路探索已啟動。 如果沒有此資訊，請重新排程網路探索。  
