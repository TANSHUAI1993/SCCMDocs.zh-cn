---
title: "更新 | Microsoft Docs"
description: "了解稱為「更新和服務」的主控台內服務方式，可讓您輕鬆尋找並安裝建議的更新。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: "51"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d46aca88111d4ee0e96b75ca5a3ec57aa4274d6d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="updates-for-system-center-configuration-manager"></a>System Center Configuration Manager 的更新

適用於：System Center Configuration Manager (最新分支)

System Center Configuration Manager 使用稱為「更新與服務」的主控台內服務方法。 此主控台內方法可針對您的 Configuration Manager 基礎結構，輕鬆地尋找並安裝建議的更新。 主控台內的服務會以頻外更新的方式進行增補，例如適用於需要解決客戶環境特定問題的 Hotfix。  

> [!TIP]  
> 管理 System Center Configuration Manager 站台及階層基礎結構時，「升級」、「更新」及「安裝」等詞彙是用來描述三種不同的概念。 若要了解如何使用每個詞彙，請參閱[關於升級、更新和安裝](/sccm/core/understand/upgrade-update-install)。


 **下列主題可協助您了解如何尋找並安裝 System Center Configuration Manager 的不同更新類型：**  

-   [安裝適用於 System Center Configuration Manager 的主控台內更新](../../../core/servers/manage/install-in-console-updates.md)  

-   [使用 System Center Configuration Manager 的服務連接工具](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [使用更新註冊工具將 Hotfix 匯入 System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [使用 Hotfix 安裝程式來安裝 System Center Configuration Manager 更新](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


如果您使用 Technical Preview 分支，請參閱 [System Center Configuration Manager 的 Technical Preview](/sccm/core/get-started/technical-preview) 以了解該分支特有的其他資訊。


##  <a name="bkmk_Baselines"></a> 基準和更新版本  
 System Center Configuration Manager 最新分支的初次發行為版本 1511，該版本為基準版本。 較近期的基準版本包括 1606 版和 1702 版：

-   在新階層中安裝新的站台時，請使用最新的基準版本。  

-   您使用基準版本從 System Center 2012 Configuration Manager 進行升級。 升級至 System Center Configuration Manager 之後，您就可以不再使用基準版本來保持最新狀態，而是改為只使用[主控台內更新](/sccm/core/servers/manage/install-in-console-updates)來更新至最新版本。  

-   會定期發行額外的基準版本。 當您使用最新的基準版本安裝新的階層時，請避免在額外的升級基礎結構以更新到最新狀態之後，安裝 Configuration Manager 的過期版本。  

安裝基準版本之後，其他的 Configuration Manager 版本會在主控台內的更新中提供。 主控台內更新會將您的基礎結構更新為最新版本的 Configuration Manager。  

-   您安裝主控台內更新以更新頂層站台的版本。  

-   除非遭到您在主要站台中設定的維護期間封鎖，否則在管理中心網站安裝的更新會自動在子主要站台中安裝。  

-   您在主控台中手動將次要站台更新為新版本。  

當您安裝更新時，更新會在站台伺服器中名為 CD.Latest 的資料夾中儲存該版本的安裝檔案。 如需這些檔案的詳細資訊，請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../../core/servers/manage/the-cd.latest-folder.md)。  

-   您會在站台復原期間使用 CD.Latest 資料夾中的檔案，並在不執行基準版本的階層中安裝其他站台。  

-   您無法使用 CD.Latest 中的安裝檔案來安裝新階層的第一個站台，或從 System Center 2012 Configuration Manager 升級站台。  

部分 Configuration Manager 的更新會在針對現有基礎結構的主控台內更新版本，及新的基準版本中提供。  

下列版本的 Configuration Manager 可在基準版本、更新版本或兩者中提供：  

|版本 |可用時間|[支援結束日期](/sccm/core/servers/manage/current-branch-versions-supported) |基準|主控台內更新|  
|-------------|-----------|------------|--------------|------------------------|  
|[1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)<br /><br /> 5.00.8540.1000|2017 年 7 月 31 日|2018 年 7 月 31 日|否|是|
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|2017 年 3 月 27 日| 2018 年 3 月 27 日|是|是|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|2016 年 11 月 18 日| 2017 年 11 月 18 日|否|是|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|2016 年 7 月 22 日| 2017 年 7 月 22 日|否|是|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) 與 1606 Hotfix 彙總套件 (KB3186654) </br></br>5.00.8412.1307 *(注意 1)* |2016 年 10 月 12 日| 2017 年 10 月 12 日|是|否|
| 1602<br /><br /> 5.00.8355.1000|2016 年 3 月 11 日| 2017 年 3 月 11 日|否|是| 
| 1511 <br /><br /> 5.00.8325.1000|2015 年 12 月 8 日| 2016 年 12 月 8 日|是|否|  


*(附註 1)* 1606 和 1702 基準媒體是屬於[大量授權服務中心](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC) 上 Microsoft System Center 2016 或 System Center Configuration Manager (最新分支和長期維護分支) 版本的一部分。 例如，您可以在 VLSC 上搜尋「System Center Config Mgr (最新分支和 LTSB)」，系統將會傳回可供下載的 1606 和 1702 版基準媒體。

要檢查您 Configuration Manager 站台的版本，請移至主控台左上角的 **關於 System Center Configuration Manager** (會顯示新站台和主控台版本)。  

##  <a name="bkmk_inconsole"></a> 主控台內更新及服務  
 當您使用 System Center Configuration Manager 的生產環境就緒安裝 (也稱為最新分支) 時，您安裝的大部分更新在更新及服務通道中均有提供。 這個方法會識別、下載和提供適用於您目前基礎結構版本和組態的更新，且僅會包括 Microsoft 建議所有客戶進行的更新。   
 它們包括：  

-   新版本，例如版本 1610、1702 或 1706。  

-   更新，包括您目前版本的新功能。

-   適用於您 Configuration Manager 版本的 Hotfix，所有客戶均應安裝。

主控台內更新可提供更高的穩定性，並可解決常見的問題。 這些更新會取代舊版產品 Service Pack、累積更新、適用於所有客戶的 Hotfix 以及Microsoft Intune 的延伸模組。 這些更新也適用於以下一或多個情況：  

-   主要和管理中心網站伺服器  

-   站台系統角色和站台系統伺服器  

-   SMS 提供者執行個體  

-   Configuration Manager 主控台  

-   Configuration Manager 用戶端  

Configuration Manager 會在您同步服務連接點站台系統角色與 Microsoft 雲端服務和下載中心時，為您探索新的更新：  

-   當您的服務連線端點處於線上模式時，您的站台會每天自動與 Microsoft 同步，以自動識別適用於您基礎結構的新更新。  若要下載更新和更新的可轉散發檔案，裝載服務連接點站台系統角色的電腦會使用**系統**內容來存取下列網際網路位置︰go.microsoft.com 和 download.microsoft.com。 如需服務連接點所連線之其他位置的相關資訊，請參閱[關於 System Center Configuration Manager 中的服務連接點](../../../core/servers/deploy/configure/about-the-service-connection-point.md)中的[網際網路存取需求](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls)。  

-   當您的服務連線端點處於離線模式時，請使用服務連線工具來手動與 Microsoft 雲端進行同步。 如需詳細資訊，請參閱 [使用 System Center Configuration Manager 的服務連接工具](../../../core/servers/manage/use-the-service-connection-tool.md)。  

-   主控台內更新會取代需要個別尋找和安裝個別更新、Service Packs 及新功能的需求。  

-   您只會安裝所選擇的主控台內更新，且在安裝部分更新時，可以選擇想要啟月及使用的個別功能。 如需詳細資訊，請參閱[從更新啟用選擇性功能](../../../core/servers/manage/install-in-console-updates.md#bkmk_options)。  

安裝主控台內更新時：  

-   會自動執行必要條件檢查。 您也可以在開始安裝前先執行這項檢查。  

-   它會在管理中心網站 (如果有的話) 及主要站台中自動安裝。 您可以使用[站台伺服器的服務保留時間](../../../core/servers/manage/service-windows.md)控制每個主要站台伺服器都可以更新其基礎結構的時間。  

-   站台伺服器更新後，所有受影響的站台系統角色 (包括 SMS 提供者執行個體) 都會自動更新。 Configuration Manager 主控台也會提示主控台使用者在站台安裝更新之後更新主控台。  

-   如果更新包括 Configuration Manager 用戶端，您可以選擇在進入生產階段前環境中測試更新，或立即將更新套用到所有用戶端。  

-   更新主要站台之後，次要站台不會自動更新。 相反地，您必須起始次要站台的更新。  

> [!NOTE]  
>  System Center Configuration Manager (最新分支) 的生產版本、長期維護分支以及 System Center Configuration Manager 的 Technical Preview 是不同的版本。 因此，適用於一個分支的更新無法做為其他分支的主控台內更新。 如需可用分支的詳細資訊，請參閱[我應該使用哪個 Configuration Manager 分支？](/sccm/core/understand/which-branch-should-i-use)

##  <a name="bkmk_outofband"></a> 頻外 Hotfix  
某些 Hotfix 是針對解決特定問題而發行，或是適用於所有客戶，但無法使用主控台內的方法來安裝，因此可用性十分有限。 這些修正程式是以頻外方式傳送，並不會在 Microsoft 雲端服務中出現。  

一般而言，當您在尋找修正程式或對 Configuration Manager 部署有問題時，可在 Microsoft 客戶支援服務、知識庫文章或 [System Center Configuration Manager 團隊部落格](https://blogs.technet.microsoft.com/configmgrteam)中了解頻外 Hotfix。  

您可使用下列方式之一，手動安裝這些修正程式：  

-   **更新註冊工具：** 此工具可手動將 Hotfix 匯入您的 Configuration Manager 主控台並在此處安裝，如同自動探索的主控台內更新。 使用下列檔案名稱結構的更新會使用此方式： **.update.exe**。  此類型的 Hotfix 完整名稱為：**&lt;產品\>-&lt;產品版本\>-&lt;知識庫文章識別碼\>-ConfigMgr.Update.exe**。  

     如需詳細資訊，請參閱[使用更新註冊工具將 Hotfix 匯入 System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)。  

-   **Hotfix 安裝程式：** 此工具用來手動安裝無法使用主控台內方式安裝的 Hotfix。 使用下列檔案名稱結構的修正程式可使用此方式： **&lt;產品\>-&lt;產品版本\>-&lt;知識庫文章識別碼\>-&lt;平台\>-&lt;語言\>.exe**。

     如需詳細資訊，請參閱[使用 Hotfix 安裝程式來安裝 System Center Configuration Manager 更新](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)。
