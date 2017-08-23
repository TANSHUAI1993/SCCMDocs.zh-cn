---
title: "使用 1606 基準媒體來安裝站台 | Microsoft Docs"
description: "安裝或升級到適用於 System Center Configuration Manager 的 LTSB。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 39653604ba5fd8e1fe9dd4d42889221d983f9bec
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>使用 1606 版基準媒體為 System Center Configuration Manager 進行安裝或升級

*適用於：System Center Configuration Manager (最新分支)、(長期維護分支)*

當您執行 Configuration Manager 1606 版基準媒體的安裝程式時，可以安裝 System Center Configuration Manager 的長期維護分支或最新分支站台。

基準媒體會以 Microsoft System Center 2016 之一部分的形式於 DVD 上提供使用，也可從 System Center Configuration Manager (最新分支和長期維護分支 1606) 發行中取得。 若要了解基準媒體，請參閱[基準和更新版本](/sccm/core/servers/manage/updates#baseline-and-udpate-versions)。


使用 1606 版基準媒體時，下列是您要安裝或升級的站台︰
- 最新分支站台：此站台相當於一開始使用 1511 基準媒體安裝，之後再更新為 1606 版以及 1606 Hotfix 彙總套件 - KB3186654 的站台。
-   LTSB 站台：它就相當於執行 1606 版以及 1606 Hotfix 彙總套件 - KB3186654 的最新分支站台。 基準媒體已經包括 Hotfix 彙總套件。  但是，LTSB 並不支援最新分支提供的所有功能，如 [System Center Configuration Manager 的長期維護分支簡介](introduction-to-the-ltsb.md)所述。

如果您不熟悉 System Center Configuration Manager 的不同分支，請參閱[我應該使用哪個 Configuration Manager 分支](which-branch-should-i-use.md)。




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>1606 基準媒體引進的安裝程式變更
1606 基準媒體針對 Configuration Manager 安裝程式引進下列變更。

### <a name="branch-and-edition"></a>分支和版本
在執行安裝程式時，即會顯示 [授權] 頁面，其中提供可讓您選取要安裝的 Configuration Manager 分支。 您可以選擇最新分支或 LTSB 作為授權的安裝，亦可選擇將最新分支的評估版作為未經授權的安裝。

如需詳細資訊，請參閱 [System Center Configuration Manager 的授權與分支](learn-more-editions.md)。

### <a name="software-assurance-expiration"></a>軟體保證到期
在安裝期間，您可以選擇輸入 [軟體保證到期日] 值。 這是選擇性的值，您可以視提醒需要加以指定。

> [!NOTE]
> Microsoft 不會驗證您輸入的到期日，亦不會將這個日期用於授權驗證。  因此，您可以將它作為到期日的提醒。 這個功能很實用，因為 Configuration Manager 會定期檢查線上提供的新軟體更新，因此您應該維持最新的軟體保證授權狀態，才能保有使用其他更新的資格。    

- 當您從 System Center Configuration Manager 1606 版基準媒體執行安裝程式時，可以在 [安裝精靈] 的 [產品金鑰] 頁面上指定日期值。
- 您也可以在 Configuration Manager 主控台中選取 [階層設定內容] > [授權]，以指定這個日期。

如需詳細資訊，請參閱 [System Center Configuration Manager 的授權和分支](learn-more-editions.md)中的＜軟體保證合約＞。


### <a name="additional-pre-upgrade-configurations"></a>其他升級前的設定
開始將 System Center 2012 Configuration Manager 升級至 LTSB 之前，您必須在升級前檢查清單中一併採取下列額外步驟。  
解除安裝 LTSB 不支援的站台系統角色：
- Asset Intelligence 同步處理點
- Microsoft Intune 連接器
- 雲端式發佈點

如需詳細資訊，請參閱[升級至 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)。


### <a name="new-scripted-installation-options"></a>新的指令碼執行的安裝選項
1606 版基準媒體支援新的自動安裝指令碼檔案機碼，可進行新頂層站台的指令碼執行的安裝。 若要在站台擴充同時，安裝新的獨立主要站台，或新增管理中心網站，就適用這種方式。

使用自動安裝指令碼安裝授權的分支時，您必須將下列區段、機碼名稱和值新增至指令碼的 [Options] 區段。 您不需要使用這些值，就可以編寫最新分支評估版安裝的指令碼：  

 **SABranchOptions**
-   **機碼名稱：SAActive**
  - 值︰0 或 1。  
  - 詳細資料︰0 會安裝未經授權的最新分支評估版，而 1 會安裝授權的版本。   

- **CurrentBranch**
  - 值︰0 或 1。  
  - 詳細資料：0 會安裝長期維護分支，而 1 會安裝最新分支。  

例如，若要安裝授權的最新分支版本，您會使用︰

  **機碼名稱：SABranchOptions**
   -    **SAActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** 只能搭配基準媒體的安裝程式使用。 如果您是從先前使用 1606 基準媒體安裝之站台的 CD.Latest 資料夾執行安裝程式，即不適用此方法。
>
> **SABranchOptions** 不適用於從 System Center 2012 Configuration Manager 進行指令碼式升級，而一律會產生最新分支。

如需詳細資訊，請參閱[使用命令列來安裝 System Center Configuration Manager 站台](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites)。


## <a name="install-a-new-site"></a>安裝新的站台
當您使用 1606 基準媒體安裝其中一個分支的新站台時，請參閱[安裝 System Center Configuration Manager 站台](/sccm/core/servers/deploy/install/installing-sites)主題中記載的站台規劃、準備和安裝程序，以及下列安裝程式的相關考量︰

- 在安裝期間，您必須選擇要安裝的 Configuration Manager 分支，並可指定軟體保證合約的詳細資料。
- 同一個階層中的所有站台都必須執行相同的分支。 同一個階層中的不同站台不支援混合使用 LTSB 和最新分支架構。
-   新的指令碼執行的安裝。 如需詳細資訊，請參閱本文稍早的＜新的指令碼執行的安裝選項＞。

## <a name="expand-a-stand-alone-primary-site"></a>擴充獨立主要站台
您可以擴充執行 LTSB 的獨立主要站台。  此程序與最新分支站台所用的相同，除了以下一點應特別注意：

- 安裝新管理中心網站時，您必須使用之前用來安裝 LTSB 站台之原始來源媒體中的安裝程式。 在這種情況下，不支援從 CD.Latest 資料夾執行安裝程式。

如需擴充站台的詳細資訊，請參閱[使用安裝精靈安裝站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)中的＜擴充獨立主要站台＞。

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>從 System Center 2012 Configuration Manager 進行升級
當您從 System Center 2012 Configuration Manager 進行升級時，請參閱[升級至 System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) 主題中所述的站台規劃、準備和程序，但需進行下列變更：

**升級至最新分支：**
- 在安裝期間，您必須選擇最新分支，並可指定軟體保證合約的詳細資料。
-   新的指令碼執行的安裝。 如需詳細資訊，請參閱本文稍早的＜新的指令碼執行的安裝選項＞。

**升級至 LTSB：**  
- 升級前檢查清單完成後要遵循的額外步驟。
- 在安裝期間，您必須選擇 LTSB，並可指定軟體保證合約的詳細資料。
- 您可以只升級執行 System Center 2012 Configuration Manager Service Pack 2 或 System Center 2012 R2 Configuration Manager Service Pack 1 的站台。

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>1606 基準媒體的就地升級路徑
您可以使用 1606 基準媒體，將下列版本升級至 System Center Configuration Manager 的授權版本：
- System Center 2012 Configuration Manager Service Pack 2。
- System Center 2012 R2 Configuration Manager Service Pack 1。

您也可以使用此媒體，將未經授權的最新分支評估版升級至最新分支的完整授權版本。

此媒體不支援升級下列項目：
- 其他版本的 System Center 2012 Configuration Manager。
- Configuration Manager 2007 或更早版本。
- System Center Configuration Manager 的候選版安裝。

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>關於 CD.Latest 資料夾和 LTSB
使用 Configuration Manager 在站台伺服器的 CD.Latest 資料夾中所建立的媒體時，具有下列限制。 這些限制適用於執行 LTSB 的站台︰

CD.Latest 資料夾中的媒體支援下列作業︰
- 站台復原。
- 站台維護。
- 安裝其他子主要站台。

CD.Latest 資料夾中的媒體不支援下列作業︰  
- 在站台擴充同時安裝管理中心網站。

如需詳細資訊，請參閱 [CD.Latest 資料夾](/sccm/core/servers/manage/the-cd.latest-folder)。

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>LTSB 的備份、復原及站台維護
若要針對執行 LTSB 的站台進行備份、復原或維護作業，請使用 [System Center Configuration Manager 備份和復原](/sccm/protect/understand/backup-and-recovery)中的指導方針與程序。  

從 LTSB 站台備份的 CD.Latest 資料夾，使用 Configuration Manager 安裝程式。
