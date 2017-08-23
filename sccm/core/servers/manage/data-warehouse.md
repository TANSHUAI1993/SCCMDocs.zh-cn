---
title: "資料倉儲 | Microsoft Docs"
description: "資料倉儲服務點與 System Center Configuration Manager 資料庫"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: eedbf12d3bf628666efc90c85a8dfab37e4dc9ab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>System Center Configuration Manager 的資料倉儲服務點
*適用於︰System Center Configuration Manager (最新分支)*

從版本 1702 開始，您可以使用資料倉儲服務點來儲存並報告您的 Configuration Manager 部署的長期歷程記錄資料。

> [!TIP]
> 「資料倉儲」服務點是隨版本 1702 引進的發行前版本功能。 若要啟用它，請參閱[使用發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

> 從 1706 版開始，這項功能不再是發行前版本功能。

資料倉儲支援高達 2 TB 的資料，其含有變更追蹤的時間戳記。 資料儲存可透過從 Configuration Manager 站台資料庫自動同步處理至資料倉儲資料庫來完成。 然後即可從您的 Reporting Services 點存取此資訊。 同步處理到資料倉儲資料庫的資料會保留三年。 內建工作會定期移除超過三年的資料。

同步處理的資料包括來自全域資料和站台資料群組的下列資料：
- 基礎結構健全狀況
- 安全性
- 合規性
- 惡意程式碼   
- 軟體部署
- 清查詳細資料 (但不會同步處理清查歷程記錄)

當站台系統角色安裝時，它會安裝並設定資料倉儲資料庫。 它也會安裝數個報告，以便您可以輕鬆地搜尋資料並報告。



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>資料倉儲服務點的必要條件
- 僅階層中的頂層站台才支援資料倉儲站台系統角色。 (管理中心網站或獨立主要站台)。
- 您安裝站台系統角色的電腦需要 .NET Framework 4.5.2 或更新版本。
- 安裝站台系統角色之電腦的電腦帳戶是用來與資料倉儲資料庫同步處理資料。 此帳戶需要下列權限：  
  - 將裝載資料倉儲資料庫之電腦上的**系統管理員**。
  - 資料倉儲資料庫上的 **DB_owner** 權限。
  - 頂層站台站台資料庫的 **DB_reader** 和「執行」權限。
- 資料倉儲資料庫需要使用 SQL Server 2012 或更新版本。 可以是 Standard、Enterprise 或 Datacenter 版本。
- 下列的 SQL Server 組態可以用來裝載倉儲資料庫：  
  - 預設執行個體
  - 具名執行個體
  - SQL Server AlwaysOn 可用性群組
  - SQL Server 容錯移轉叢集
-   當資料倉儲資料庫位於遠端站台伺服器資料庫時，您必須具備裝載資料庫之每部 SQL Server 的個別授權。
- 如果您使用[分散式檢視](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews)，必須在裝載管理中心網站站台資料庫的同一部伺服器上安裝資料倉儲服務點站台系統角色。



> [!IMPORTANT]  
> 當執行「資料倉儲」服務點或裝載資料倉儲資料庫的電腦下列其中一種語言時，便不支援「資料倉儲」：
> - JPN – 日文
> - KOR – 韓文
> - CHS – 簡體中文
> - CHT – 繁體中文。在未來的版本中將會解決這個問題。


## <a name="install-the-data-warehouse"></a>安裝資料倉儲
每個階層都支援此角色的單一執行個體，位於該頂層站台的任何站台系統上。 裝載倉儲資料庫的 SQL Server 可以是本機站台系統角色，或者遠端站台系統角色。 雖然資料倉儲可搭配安裝於相同站台的 Reporting Services 點運作，這兩個站台系統角色不必安裝在同一部伺服器上。   

若要安裝角色，使用「新增站台系統角色精靈」 或「建立站台系統伺服器精靈」。 如需詳細資訊，請參閱[安裝站台系統角色](/sccm/core/servers/deploy/configure/install-site-system-roles)。  

當您安裝此角色時，Configuration Manager 會在您指定的 SQL Server 執行個體上為您建立資料倉儲資料庫。 如果您指定現有資料庫的名稱 (就像是在[將資料倉儲資料庫移至新的 SQL Server](#move-the-data-warehouse-database) 時所執行的動作)，Configuration Manager 不會建立新的資料庫，而是會使用您指定的資料庫。

### <a name="configurations-used-during-installation"></a>安裝期間所使用的設定
[系統角色選取] 頁面：  

[一般] 頁面：
-   **Configuration Manager 資料倉儲資料庫連線設定**：
 - **SQL Server 完整網域名稱**：  
 指定裝載資料倉儲服務點資料庫之伺服器的完整網域名稱 (FQDN)。
 - **SQL Server 執行個體名稱 (如適用)**：   
 如果您沒有使用 SQL Server 的預設執行個體，您必須指定執行個體。
 - **資料庫名稱**：   
 指定資料倉儲資料庫的名稱。 資料庫名稱不能超過 10 個字元。 (未來的版本將增加支援的名稱長度)。
 Configuration Manager 會以此名稱建立資料倉儲資料庫。 如果您指定的資料庫名稱已存在於 SQL Server 執行個體上，Configuration Manager 會使用該資料庫。
 - **連線時要使用的 SQL Server 連接埠**：   
 指定針對裝載資料倉儲資料庫之 SQL Server 設定的 TCP/IP 連接埠號碼。 資料倉儲同步處理服務會使用此連接埠來連線到資料倉儲資料庫。  

[同步處理排程] 頁面：   
- **同步處理排程**：
 - **開始時間**：  
 指定您想要啟動資料倉儲同步處理的時間。
 - **循環模式**：
    - **每日**：指定每日執行同步處理。
    - **每週**：指定每週一天，及每週循環同步處理。

## <a name="reporting"></a>報告
安裝資料倉儲服務點後，安裝於相同站台上之 Reporting Services 點上會有數個可用報告。 如果您在安裝 Reporting Services 點之前安裝資料倉儲服務點，在您稍後安裝 Reporting Services 點時會自動加入這些報告。

資料倉儲站台系統角色包含下列報告，其中包含 [資料倉儲] 類別：
 - **應用程式部署 - 歷程記錄**：   
 檢視特定應用程式和電腦之應用程式部署的詳細資料。
 - **Endpoint Protection 和軟體更新合規性 - 歷程記錄**：檢視缺少軟體更新的電腦。  
 - **一般硬體清查 - 歷程記錄**：   
 檢視特定電腦的所有硬體清查。
 - **一般軟體清查 - 歷程記錄**：   
 檢視特定電腦的所有軟體清查。
 - **基礎結構健康情況概觀 - 歷程記錄**：  
 顯示您 Configuration Manager 基礎結構健全狀況的概觀
 - **偵測到的惡意程式碼清單 - 歷程記錄**：    
 檢視組織中已偵測到的惡意程式碼。
 - **軟體發佈摘要 - 歷程記錄**:   
 特定公告和電腦的軟體發佈摘要。


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>將現有的獨立主要站台擴充到階層中
在您可以安裝管理中心網站以擴充現有的獨立主要站台之前，您必須先解除安裝資料倉儲服務點角色。 安裝管理中心網站之後，您可以在管理中心網站安裝站台系統角色。  

不同於移動資料倉儲資料庫，此變更會導致您先前在主要站台上同步處理的歷程資料遺失。 不支援從主要站台備份資料庫，並在管理中心網站還原資料庫。




## <a name="move-the-data-warehouse-database"></a>移動資料倉儲資料庫
您可以使用下列步驟將資料倉儲資料庫移至新的 SQL Server：

1.  使用 SQL Server Management Studio 備份資料倉儲資料庫。 然後，將該資料庫還原到裝載資料倉儲的新電腦上的 SQL Server。   
> [!NOTE]     
> 當您將資料庫還原到新的伺服器之後，請確定新資料倉儲資料庫的資料庫存取權限與原始資料倉儲資料庫的權限相同。  

2.  使用 Configuration Manager 主控台從目前的伺服器移除資料倉儲服務點站台系統角色。
3.  重新安裝資料倉儲服務點，並指定裝載您還原之資料倉儲資料庫的新 SQL Server 和執行個體名稱。
4.  安裝站台系統角色之後，即完成移動。

## <a name="troubleshooting-data-warehouse-issues"></a>針對資料倉儲問題進行疑難排解
**記錄檔**：  
您可以使用下列記錄來調查安裝資料倉儲服務點或同步處理資料的問題：
 - *DWSSMSI.log* 和 *DWSSSetup.log* - 使用這些記錄可調查安裝資料倉儲服務點時所發生的錯誤。
 - *Microsoft.ConfigMgrDataWarehouse.log* - 使用此記錄可調查站台資料庫與資料倉儲資料庫之間的資料同步處理。

**設定失敗**  
 當資料倉儲是遠端站台系統伺服器上安裝的第一個站台系統角色時，在該電腦上的資料倉儲服務點安裝會失敗。  
  - **解決方式**：   
    請確定您要安裝資料倉儲服務點的電腦已經裝載至少一個其他站台系統角色。  


**已知的同步處理問題**：   
同步處理會因為 *Microsoft.ConfigMgrDataWarehouse.log* 中的下列原因失敗：**“failed to populate schema objects” (無法填入結構描述物件)**  
 - **解決方式**：  
    請確定裝載站台系統角色之電腦的電腦帳戶是資料倉儲資料庫上的 **db_owner**。

當資料倉儲資料庫和 Reporting Service 點位在不同的站台系統上時，無法開啟資料倉儲報告。  

 - **解決方式**：  
    將資料倉儲資料庫的 **db_datareader** 權限授與 **Reporting Services 點帳戶**。

當您開啟資料倉儲報告時傳回下列錯誤︰

*報表處理期間發生錯誤。(rsProcessingAborted) 無法與資料來源 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_' 建立連接。(rsErrorOpeningConnection) 與伺服器的連接已成功建立，但在登入前的信號交換時發生錯誤。(提供者: SSL 提供者，錯誤: 0 - 憑證鏈結由不受信任的授權單位所發行。)*

- **解決方式**：使用下列步驟設定憑證：

  1. 在裝載資料倉儲資料庫的電腦上︰

    1. 開啟 IIS，按一下 [伺服器憑證]，以滑鼠右鍵按一下 [建立自我簽署憑證]，然後將憑證名稱的「易記名稱」指定為**資料倉儲 SQL Server 識別憑證**。 選取憑證存放區為 [個人]。
    2. 開啟 [SQL Server Configuration Manager]，在 [SQL Server 網路組態] 底下以滑鼠右鍵按一下 [MSSQLSERVER 的通訊協定] 並選取 [內容]。 然後，在 [憑證] 索引標籤上，選取 [資料倉儲 SQL Server 識別憑證] 作為憑證，然後儲存變更。  
    3. 開啟 [SQL Server Configuration Manager]，在 [SQL Server 服務] 底下，重新啟動 **SQL Server 服務**與 **Reporting Service**。
    4.  開啟 Microsoft Management Console (MMC) 並加入 [憑證] 嵌入式管理單元，選取以管理本機電腦 [電腦帳戶] 的憑證。 然後，在 MMC 中，展開 [個人] 資料夾 > [憑證]，並將**資料倉儲 SQL Server 識別憑證**匯出為 **DER 編碼二進位 X.509 (.CER)** 檔案。    
  2.    在裝載 SQL Server Reporting Services 的電腦上，開啟 MMC 並加入 [憑證] 嵌入式管理單元。 然後選取管理 [電腦帳戶] 的憑證。 在 [信任的根憑證授權單位] 資料夾底下，匯入**資料倉儲 SQL Server 識別憑證**。


## <a name="data-warehouse-dataflow"></a>資料倉儲資料流程   
![資料倉儲流程](./media/datawarehouse.png)

**資料儲存和同步處理**

| 步驟   | 詳細資料  |
|:------:|-----------|  
| **1**  |  站台伺服器將資料傳送並儲存在站台資料庫。  |  
| **2**  |      資料倉儲服務點根據其排程和設定，從站台資料庫取得資料。  |  
| **3**  |  資料倉儲服務點將同步處理的資料複本傳送並儲存在資料倉儲資料庫。 |  
**報告**

| 步驟   | 詳細資料  |
|:------:|-----------|  
| **A**  |  使用者使用內建報表要求資料。 此要求會使用 SQL Server Reporting Services 傳遞到 Reporting Services 點。 |  
| **B**  |      大部分報告是針對目前的資訊，並會對站台資料庫執行這些要求。 |  
| **C**  | 當報告要求歷程記錄資料時，會透過使用其中一個 [類別] 為 [資料倉儲] 的報告，對資料倉儲資料庫執行要求。   |  
