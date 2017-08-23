---
title: "應該使用哪個分支 | Microsoft Docs"
description: "了解 System Center Configuration Manager 可用分支之間的差異。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 26356a80bd8c78d4517253bae73e53d8d8f3a73a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>我應該使用哪個 Configuration Manager 分支？

*適用於：System Center Configuration Manager (最新分支、長期維護分支和 Technical Preview)*


從 2016 年 10 月開始，System Center Configuration Manager 有三個分支可使用。 請使用本主題協助選擇正確的分支。

> [!TIP]  
> 同一個階層中的所有站台必須執行相同的分支。 不支援在不同站台具有不同分支的階層。

## <a name="current-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 的最新分支
這是您希望選項能取得最新特性和功能的生產環境所使用的授權分支。 這是您有下列其中一種產品時使用的分支：System Center Datacenter、System Center Standard、System Center Configuration Manager 或對等訂閱權限。 如需軟體保證和授權選項的詳細資訊，請參閱 [System Center Configuration Manager 的授權和分支](learn-more-editions.md)。


>  [!TIP]
> 最新分支可以安裝成不需要授權的評估版。 評估版可使用 180 天，並支援升級至最新分支的授權版本。

最新分支一年會更新數次新功能。 每個更新版本在發行後都有一年支援。 您必須在一年到期日當天或之前，更新至最新分支的較新版本。 較新版本的更新會提供為主控台內更新。

若要將最新分支安裝為新站台或從 System Center 2012 Configuration Manager Service Pack 2 或 System Center 2012 R2 Configuration Manager Service Pack 1 升級，請使用 System Cener 2016 所附 DVD 或屬於 System Center Configuration Manager 獨立版的 System Center Configuration Manager [基準媒體](/sccm/core/servers/manage/updates#baseline-and-update-versions)。 System Center Configuration Manager 的授權方式會決定您對此媒體的存取權。 較新的基準版本 (如 1702) 不支援安裝 LTSB。

您也可以使用基準媒體來安裝新站台，它會是最新分支評估版。 如果只想安裝評估版，您可以從 [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) 網站取得軟體。

>  [!NOTE]
> 使用基準媒體安裝新 Configuration Manager 階層的站台。 如果先前已安裝 1511 版這類基準版本，請使用主控台內更新將站台更新為新的版本 (例如 1606 版)。
>
> 使用主控台內更新所更新的站台，會產生和使用基準媒體安裝的新站台一樣的站台。
>
> 如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](/sccm/core/servers/manage/updates)。

**最新分支的功能**
- 收到啟用新功能的[主控台內更新](/sccm/core/servers/manage/install-in-console-updates)。
- 收到提供現有功能安全性及品質修正程式的主控台內更新。
- 必要時支援頻外更新。 請參閱[使用更新註冊工具](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)或[使用 Hotfix 安裝程式](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)。
- 可與 Microsoft Intune 和其他雲端服務及基礎結構交互操作。
- 支援與其他 Configuration Manager 安裝彼此間互相[移轉資料](/sccm/core/migration/migrate-data-between-hierarchies)。
- 支援從舊版 Configuration Manager 升級。
- 支援安裝為評估版，未來可從此版升級為完整授權版安裝。

最新分支的初始版本是 1511 版。 後續更新的版本包括 1602、1606 等等。 每個版本都會保留一年的支援，Microsoft 建議您最新版一發行即予以更新。 您有一年的時間可以更新為較新版本，也可以略過更新逕行安裝最新的可用版本。 因為每個版本都會累積，如果您略過更新而安裝最新版本，仍然可以從舊版存取所有功能和增強功能。

如需詳細資訊，請參閱[最新分支版本的支援](/sccm/core/servers/manage/current-branch-versions-supported)。

**更新選項**
- 利用使用中的軟體保證，您可以安裝最新分支版本的主控台內更新。  
- 沒有任何選項可將最新分支轉換成 Technical Preview。 Technical Preview 是不需要授權的個別安裝。
- 沒有任何選項可將最新分支轉換成長期維護分支 (LTSB)。 您必須解除安裝最新分支，再將 LTSB 安裝為新安裝。

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>System Center Configuration 的長期維護分支
這是 Configuration Manager 客戶實際執行時使用的授權分支，這些客戶使用最新分支，且其 Configuration Manager 軟體保證 (SA) 或對等訂閱權限在 2016 年 10 月 1 日後才到期。 如需軟體保證和授權選項的詳細資訊，請參閱 [System Center Configuration Manager 的授權和分支](learn-more-editions.md)。

LTSB 是以 1606 版為基礎。 這個分支不會收到提供新功能或更新現有功能的主控台內更新。 但會提供重要的安全性修正程式。 若要安裝 LTSB，您必須使用 1606 版[基準媒體](/sccm/core/servers/manage/updates#baseline-and-update-versions)，亦即 System Center 2016 或 System Center Configuration Manager 隨附的 DVD。

若要將 LTSB 安裝為新的站台或從支援的 Configuration Manager 2012 站台升級，請使用 1606 版的[基準媒體](/sccm/core/servers/manage/updates#baseline-and-update-versions) DVD，隨附於 System Center 2016 或 System Center Configuration Manager (最新分支和長期維護分支 1606) 版本。 您可以使用基準媒體來安裝執行 1606 版最新分支的新站台，或執行長期維護分支的新站台。

> [!TIP]  
> 若要了解 System Center 2016，請參閱 [System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) 文件。 這份文件也會告訴您如何取得 System Center 2016，但需要 microsoft 軟體授權合約或類似的權限。

> 若要在大量授權服務中心 (VLSC) 中尋找 System Center Configuration Manager 1606 版，請前往 [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) 的 [下載和金鑰] 索引標籤，並搜尋 "system center config"，然後選取 [System Center Config Mgr (最新分支與 LTSB)]。

> 您也可以從 [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview) 下載 System Center 2016 評估版。

**LTSB 的功能**
-   收到提供重要安全性修正程式的主控台內更新
- 在 Configuration Manager 的 SA 合約或對等權限過期時提供安裝選項
- 當您有 Configuration Manager 的目前 SA 合約或對等權限時，支援升級 (轉換) 至最新分支

**限制**  
LTSB 是以最新分支 1606 版為基礎，並具有下列限制：
- LTSB 在正式運作後 (2016 年 10 月) 會提供 10 年的重大安全性更新支援，過後此分支的支援即到期。 如需技術支援週期的詳細資訊，請參閱 [Microsoft 週期原則](https://support.microsoft.com/en-us/lifecycle)。
- 支援一組有限的伺服器和用戶端作業系統及相關技術 (如 SQL Server 版本) 清單。 如需此分支支援項目的詳細資訊，請參閱[支援的長期維護分支設定](supported-configurations-for-ltsb.md)。
- 不會收到新功能的更新。
- 不支援新增 Microsoft Intune 訂閱，因此無法使用下列項目：
  - 混合式 MDM 設定的 Intune
 - 內部部署 MDM
-   不支援使用 Windows 10 服務儀表板、服務計畫、Windows 10 最新分支 (CB) 或最新商務分支 (CBB)。
- 不支援 Windows 10 LTSB 和 Windows Server 的未來版本。
-   不支援 Asset Intelligence。
-   不支援雲端式發佈點。
-   不支援將 Exchange Online 的支援作為 Exchange Connector。
-   不支援任何發行前版本功能。



**更新選項**
- 您可以將 LTSB 安裝轉換成最新分支安裝。 支援在 LTSB 支援到期前後轉換為最新分支。

  若要轉換，您必須擁有使用中的 Microsoft 軟體保證協議。 如需詳細資訊，請參閱下列連結：
  - [將長期維護分支升級至最新分支](convert-to-current-branch.md)
  - [System Center Configuration Manager 的授權和分支](learn-more-editions.md)
  - [Configuration Manager 的更新](/sccm/core/servers/manage/updates)中的[基準和更新版本](/sccm/core/servers/manage/updates#baseline-and-update-versions)
- 沒有任何選項可將 LTSB 轉換成 Technical Preview。 Technical Preview 是不需要授權的個別安裝。
-   您無法將最新分支的評估版升級為 LTSB 安裝。


## <a name="technical-preview-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 Technical Preview
Technical Preview 是用於實驗室環境，讓您了解並試用開發中的 Configuration Manager 最新功能。 Technical Preview 在生產環境中不受支援，也不需要有軟體保證的授權協議。

若要安裝執行 Technical Preview 的新站台，請使用最新版 [System Center Configuration Manager Technical Preview 的基準媒體](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview)。 安裝 Technical Preview 之後，每個月都有新版的主控台內更新。

**Technical Preview 的功能**
-  以最新分支的最新基準版本為基礎
-  收到將安裝更新為最新版 Technical Preview 的主控台內更新
-  我們的開發人員希望您能對隨附的開發中新功能提供意見反應
-  收到僅適用於 Technical Preview 分支的更新

**限制**
-  [支援是有限的](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview)，包括只有一部主要站台及最多 10 個用戶端。  
-  無法升級至最新分支或 LTSB。
-  不支援使用移轉將資料匯入或匯出至另一個 Configuration Manager 安裝。
-  不支援從舊版 Configuration Manager 升級。
-  不支援安裝為評估版。

Technical Preview 首度推出的功能，通常會加入最新分支的新更新中。 每個新的 Technical Preview 版本都包含舊版 Technical Preview 的功能，即使這些功能已加入至最新分支。

如需詳細資訊，請參閱 [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) 。

**更新選項**
-   您可以安裝新版 Technical Preview 的任何主控台內更新。
-   沒有任何選項可將 Technical Preview 轉換成最新分支或 LTSB。


## <a name="identify-your-branch-and-version"></a>識別您的分支和版本
當您檢視 Configuration Manager 站台的版本資訊時，也可確認分支。

**版本**   
若要檢查站台的版本，請在主控台中，移至主控台左上角的 [關於 System Center Configuration Manager]，[站台版本] 會在該處顯示。 如需站台版本的清單，請參閱 []()。

**分支**  
若要確認站台的分支 (為 LTSB 或最新分支)，請移至主控台的 [系統管理] > [站台設定] > [站台]，並開啟 [階層設定]。 如果其中具有可以轉換為最新分支的作用中選項，即表示站台執行 LTSB 版本。 當站台執行最新分支時，此選項即會呈現灰色。
如需 Configuration Manager 不同版本的資訊，請參閱 [Configuration Manager 的更新](/sccm/core/servers/manage/updates)中的＜基準和更新版本＞。
