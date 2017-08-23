---
title: "建立遠端連線設定檔 | Microsoft Docs"
description: "使用 System Center Configuration Manager 遠端連線設定檔，讓使用者遠端連線至工作電腦。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72fc94c6449649656a7e8b81659c2b5cc2551107
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的遠端連線設定檔

*適用於︰System Center Configuration Manager (最新分支)*

使用 System Center Configuration Manager 遠端連線設定檔可允許您的使用者在未連線到網域或透過網際網路連線到其個人電腦時，從遠端連線到工作電腦。  

 使用者可以從下列裝置類型，連線到其工作電腦：  

-   執行 Microsoft Windows 的電腦  

-   執行 iOS 的裝置  

-   執行 Android 的裝置  

您可以使用遠端連線設定檔，為 Configuration Manager 階層中的使用者部署遠端桌面連線設定。 之後，使用者就可以藉由公司入口網站，使用該入口網站所提供的遠端桌面連線設定，透過遠端桌面存取其主要工作電腦。  

如果您要讓使用者透過公司入口網站連線到其工作電腦，就必須使用 Microsoft Intune。 如果您不使用 Intune，使用者仍可使用遠端連線設定檔中的資訊，透過 VPN 連線以遠端桌面連線到其工作電腦。  

> [!IMPORTANT]  
>  當您使用 Configuration Manager 主控台指定遠端連線設定檔的設定時，這些設定會儲存在用戶端電腦的本機原則中。 這些設定可能會覆寫其他應用程式所設定的遠端桌面設定。 此外，如果您使用 Windows 群組原則設定遠端桌面設定，群組原則中所指定的設定值就會覆寫那些使用 Configuration Manager 所設定的設定。  

 當您安裝 Configuration Manager 時，會建立一個新安全性群組 **Remote PC Connect**。 部署遠端連線設定檔時，您要部署設定檔之電腦的主要使用者即會填入此群組。 雖然本機系統管理員會將使用者名稱加入到此群組，當下一次評估已部署之遠端連線設定檔的相容性時，便會從群組中移除這些使用者。  

 如果以手動方式將使用者加入到此群組，使用者就會起始遠端連線，但連線資訊不會發佈在公司入口網站。  

 如果您手動將 Configuration Manager 新增的使用者從群組中移除，Configuration Manager 會在下一次評估遠端連線設定檔的相容性時，自動新增回使用者，以補救這項變更。  

> [!IMPORTANT]  
>  如果使用者和裝置之間的使用者裝置親和性關聯有變化 (例如，使用者連線的電腦不再是使用者的主要裝置時)，Configuration Manager 會停用遠端連線設定檔及 Windows 防火牆設定，避免與電腦連線。  

## <a name="prerequisites"></a>先決條件  

### <a name="external-dependencies"></a>外部相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|遠端桌面閘道伺服器。|如果您想要讓使用者透過網際網路從公司網域外部連線，您必須安裝並設定遠端桌面閘道伺服器。<br /><br /> 如果遠端桌面或終端機服務設定是由另一個應用程式或群組原則設定進行管理，則遠端連線設定檔可能無法正常作用。 當您從 Configuration Manager 主控台部署遠端連線設定檔時，其設定會儲存在用戶端電腦的本機原則中。 這些設定可能會覆寫其他應用程式所設定的遠端桌面設定。 此外，如果您使用群組原則設定來指定遠端桌面設定，群組原則設定中指定的設定便會覆寫 Configuration Manager 所設定的設定。<br /><br /> 如需如何安裝及設定遠端桌面閘道伺服器的詳細資訊，請參閱 Windows Server 文件。|  
|如果用戶端電腦執行主機型防火牆，則必須啟用 Mstsc.exe 程式。|當您設定遠端連線設定檔時，您必須啟用 [允許 Windows 網域和私人網路上連線的 Windows 防火牆例外]  設定。 當啟用此設定時，Configuration Manager 會自動將 Windows 防火牆設定為啟用 Mstsc.exe 程式。 不過，如果用戶端電腦執行不同的主機型防火牆，您就必須手動設定此防火牆的相依性。<br /><br /> 用於設定 Windows 防火牆的群組原則設定可以覆寫您在 Configuration Manager 中指定的設定。 如果您使用群組原則來設定 Windows 防火牆，請確認群組原則設定不會封鎖 Mstsc.exe 程式。|  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|Configuration Manager 必須連線至 Microsoft Intune (稱作混合式設定)。|如需將 Configuration Manager 連線至 Microsoft Intune 的詳細資訊，請參閱＜使用 Configuration Manager 和 Microsoft Intune 管理行動裝置＞。|  
|若要讓使用者連線至公司網路上的工作電腦，該電腦必須是該使用者的主要裝置。|如需使用者裝置親和性的詳細資訊，請參閱[使用使用者裝置親和性連結使用者和裝置](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。|  
|若要管理遠端連線設定檔，必須授與特定的安全性權限。|**相容性設定管理員** 安全性角色包括管理遠端連線設定檔所需的權限。 如需詳細資訊，請參閱 <br />[設定以角色為基礎的系統管理](/sccm/core/servers/deploy/configure/configure-role-based-administration)。|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>遠端連線設定檔的安全性和隱私權考量  

### <a name="security-considerations"></a>安全性考量  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|手動指定使用者裝置親和性，而不是讓使用者識別自己的主要裝置。 此外，請勿啟用基於使用方式的設定。|由於您必須先啟用 [允許工作電腦的所有主要使用者從遠端連線]  ，才能部署遠端連線設定檔，所以請一律手動指定使用者裝置親和性。 請勿將由使用者或裝置收集到的資訊視為已授權。 如果您部署遠端連線設定檔，而且信任的系統管理使用者未指定使用者裝置親和性，未授權的使用者可能會獲得較高的權限，因而能夠從遠端連線到電腦。<br /><br /> 如果您啟用基於使用方式的設定，則此資訊會透過 Configuration Manager 未提供安全保護的狀態訊息進行收集。 若要降低此威脅，請在用戶端電腦和管理點之間使用伺服器訊息區 (SMB) 簽署或網際網路通訊協定安全性 (IPsec)。|  
|限制網站伺服器電腦上的本機系統管理權限。|站台伺服器上具有本機系統管理權限的使用者可以手動新增成員至 Configuration Manager 自動建立及維護的 Remote PC Connect 安全性群組。 這可能會導致權限的提升，因為新增至此群組的成員會獲得遠端桌面權限。|  

### <a name="privacy-considerations"></a>隱私權考量  

-   如果使用者從公司入口網站起始與工作電腦的連線，便會下載副檔名為 .rdp 或 .wsrdp 的檔案，其中含有裝置名稱以及起始遠端桌面工作階段所需的遠端桌面閘道伺服器名稱。 檔案副檔名視裝置的作業系統而定。 例如，Windows 7 及 Windows 8 作業系統使用 .rdp 檔案，而 Windows 8.1 則使用 .wsrdp 檔案。  

-   使用者可以選擇開啟或儲存 .rdp 檔案。 如果使用者選擇開啟 .rdp 檔案，視瀏覽器所設定的保留設定而定，檔案可能會儲存在網頁瀏覽器的快取中。 如果使用者選擇儲存檔案，則檔案不會儲存在瀏覽器快取中。 檔案將會儲存到使用者手動將它刪除為止。  

-   .wsrdp 檔案會從本機下載並且自動儲存於本機。 此檔案會在使用者下次執行遠端桌面工作階段時覆寫。  

-   設定遠端連線設定檔之前，請考慮您的隱私權需求。  


## <a name="create-a-remote-connection-profile"></a>建立遠端連線設定檔

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [遠端連線設定檔]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立遠端連線設定檔] 。  

4.  在 [建立遠端連線設定檔精靈]  的 [一般] 頁面上，指定各使用 256 個字元數上限之設定檔的名稱和選擇性描述。  

5.  在 [設定檔設定] 頁面上，指定遠端連線設定檔的下列設定：  

    -   **遠端桌面閘道伺服器的完整名稱和連接埠 (選用)** - 指定用於連線的遠端桌面閘道伺服器的名稱。  

        > [!NOTE]  
        >  Configuration Manager 不支援使用國際化網域名稱在此方塊中指定伺服器。  
        >   
        >  伺服器名稱長度不可超過 256 個字元，且可包含大寫字元、小寫字元、數字字元，以及 **–** 和 **_** 字元，並以句號分隔。  

    -   **僅允許來自透過網路層級驗證執行遠端桌面的電腦進行連線**  

6.  針對下列每一種連線設定選取 [已啟用]  或 [已停用]  ：  

    -   **允許遠端連線到工作電腦**  

    -   **允許工作電腦的所有主要使用者從遠端連線**  

    -   **允許 Windows 網域及私人網路連線的 Windows 防火牆例外**  

    > [!IMPORTANT]  
    >  在您繼續通過此精靈頁面之前，所有三項設定都必須相同。  

7.  在 [摘要] 頁面上，檢閱要採取的動作，然後完成精靈。  

 新的遠端連線設定檔會顯示在 [資產與相容性]  工作區的 [遠端連線設定檔]  節點中。  

部署遠端連線設定檔  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [遠端連線設定檔]。  

3.  在 [遠端連線設定檔]  清單中，選取您想要部署的遠端連線設定檔，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。  

4.  在 [部署遠端連線設定檔]  對話方塊中，指定下列資訊：  

    -   **集合** - 按一下 [瀏覽]  以選取您要部署遠端連線設定檔的裝置集合。  

    -   **支援時補救不相容的規則** - 啟用此選項可在發現裝置上的遠端連線設定檔不相容 (例如不存在) 時自動補救。  

    -   **允許在維護期間以外補救** - 如果已針對您部署遠端連線設定檔的集合設定維護期間，請啟用此選項讓 Configuration Manager 補救維護期間以外的遠端連線設定檔。 如需維護期間的詳細資訊，請參閱[如何使用維護期間](/sccm/core/clients/manage/collections/use-maintenance-windows)。  

    -   **產生警示** - 啟用此選項，可設定當遠端連線設定檔相容性低於指定之日期和時間所指定的百分比時，產生警示。 您也可以指定是否要將警示傳送至 System Center Operations Manager。  

    -   **指定此組態基準的相容性評估排程** - 指定在裝置上評估部署之遠端連線設定檔的排程。 您可以指定簡易或自訂排程。  

    > [!TIP]  
    >  如果裝置離開部署有遠端連線設定檔的集合，裝置上的遠端連線設定檔設定便會停用。 不過，若要正確執行此程序，您必須至少已部署一個設定項目或含有站台設定項目的設定基準。  
    >   
    >  當使用者登入時，裝置會評估設定檔。  
    >   
    >  如果兩個遠端連線設定檔已部署至相同的裝置集合，其中一個設定檔中已核取 [支援時補救不相容的規則]  ，而另一個設定檔中未核取相同的選項，而且兩個遠端連線設定檔包含不同的連線設定，則未核取這個選項的設定檔可能會覆寫另一個設定檔中的設定。 Configuration Manager 不支援此類型的遠端連線設定檔部署。  

5.  按一下 [確定]  以關閉 [部署遠端連線設定檔]  對話方塊並建立部署。  

## <a name="monitor-a-remote-connection-profile"></a>監視遠端連線設定檔  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 主控台中檢視相容性結果  

1.  在 Configuration Manager 主控台中，按一下 [監視] > [部署]。  

3.  在 [部署]  清單中，選取您要檢閱相容性資訊的遠端連線設定檔部署。  

4.  您可以在主頁面檢閱有關遠端連線設定檔部署相容性的摘要資訊。 若要檢視更詳細的資訊，請選取遠端連線設定檔部署，然後在 [首頁]  索引標籤的 [部署]  群組中，按一下 [檢視狀態]  以開啟 [部署狀態]  頁面。  

     [部署狀態]  頁面包含下列索引標籤：  

    -   **相容** ：根據受影響的資產數目，顯示遠端連線設定檔的相容性。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含與遠端連線設定檔相容的所有裝置。 [資產詳細資料]  窗格也顯示與這個設定檔相容的裝置。 按兩下清單中的裝置以顯示其他資訊。  

        > [!IMPORTANT]  
        >  如果遠端連線設定檔在用戶端裝置上不適用，就不會進行評估； 不過，仍會傳回為相容。  

    -   **錯誤** ：根據受影響的資產數目，顯示一份所選遠端連線設定檔部署的所有錯誤清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含因為這個設定檔而產生錯誤的所有裝置。 當您選取裝置時，[資產詳細資料]  窗格會顯示受到所選問題影響的裝置。 按兩下清單中的裝置以顯示與此問題有關的其他資訊。  

    -   **不相容** ：根據受影響的資產數目，顯示一份遠端連線設定檔中所有不相容規則的清單。 您可以按兩下規則，在 [資產與相容性]  工作區的 [使用者]  節點下方建立臨時節點。 這個節點包含與這個設定檔不相容的所有裝置。 當您選取裝置時，[資產詳細資料]  窗格會顯示受到所選問題影響的裝置。 按兩下清單中的裝置以顯示與此問題有關的其他資訊。  

    -   **不明** ：顯示未針對所選遠端連線設定檔部署報告相容性的所有裝置清單，以及裝置目前的用戶端狀態。  

5.  在 [部署狀態]  頁面中，您可以檢閱與部署之遠端連線設定檔相容性有關的詳細資訊。 [部署]  節點下方會建立一個臨時節點以協助您更快再找到此資訊。  

### <a name="view-compliance-results-with-reports"></a>使用報告檢視相容性結果  
 Configuration Manager 包含內建報告，您可利用這些報告來監視遠端連線設定檔的相關資訊。 這些報告具有 [相容性和設定管理] 的報告類別。  

> [!IMPORTANT]  
>  當您在相容性設定的報告中使用 [裝置篩選器]  和 [使用者篩選器]  參數時，必須使用萬用字元 (%)。  

 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](/sccm/core/servers/manage/reporting)。  
