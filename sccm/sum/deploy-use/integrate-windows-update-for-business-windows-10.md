---
title: "與 Windows 10 中的 Windows Update for Business 整合 | Microsoft Docs"
description: "針對連線到 Windows Update 服務的裝置，您可以使用 Windows Update for Business 讓組織中的 Windows 10 裝置保持最新狀態。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 26e73a69d5e6ca69e766fcf3cedd992353c92cd6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>與 Windows 10 中的 Windows Update for Business 整合

*適用於：System Center Configuration Manager (最新分支)*

商務用 Windows Update (WUfB) 可讓您組織中的 Windows 10 裝置直接連接到 Windows Update (WU) 服務，永遠掌握最新的安全性防禦措施及 Windows 功能。 Configuration Manager 能夠區分使用 WUfB 及 WSUS 取得軟體更新的 Windows 10 電腦。  

 將 Configuration Manager 用戶端設定為從 WU (包括 WUfB 或 Windows 測試人員) 接收更新時，某些 Configuration Manager 功能便無法再使用：  

-   Windows Update 相容性報告：  

    -   Configuration Manager 不會察覺發佈到 WU 的更新。 設定為從 WU 接收更新的 Configuration Manager 用戶端會將 Configuration Manager 主控台中的更新顯示為 [不明]。  

    -   整體相容性狀態的疑難排解很困難，原因是 [不明]  狀態以往僅供尚未從 WSUS 回報掃描狀態的用戶端使用。  現在則也包含從 WU 接收更新的 Configuration Manager 用戶端。  

    -   從 WU 接收更新的用戶端將無法正常使用建基於更新相容性狀態的條件式存取 (用於公司資源)，原因是其永遠無法符合 Configuration Manager 的相容性。  

    -   定義更新相容性是整體更新相容性報告的一部分，而且也無法正常運作。  定義更新相容性也是條件存取評估的一部分。  

-   建基於更新相容性狀態之 Defender 的整體 Endpoint Protection 報告由於缺少掃描資料，而不會傳回精確的結果。  

-   如果用戶端是連接 WUfB 以接收更新，Configuration Manager 就無法將 Office、IE 以及 Visual Studio 這類 Microsoft 更新部署到該用戶端。  

-   如果用戶端是連接 WUfB 以接收更新，Configuration Manager 就無法將協力廠商更新 (發行至 WSUS 且透過 Configuration Manager 管理) 部署到該用戶端。  

-   使用軟體更新基礎結構的 Configuration Manager 完整用戶端部署，將不適用於連接 WUfB 以接收更新的用戶端。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>識別使用 WUfB 進行 Windows 10 更新的用戶端  
 使用下列程序來識別使用 WUfB 取得 Windows 10 更新和升級的用戶端、將這些用戶端設定為停止使用 WSUS 取得更新，並部署用戶端代理程式設定以停用這些用戶端的軟體更新工作流程。  

 **先決條件**  

-   執行 Windows 10 Desktop Pro 或 Windows 10 Enterprise Edition 1511 版或更新版本的用戶端  

-   [商務用 Windows Update](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) 已部署，且用戶端使用 WUfB 取得 Windows 10 更新及升級。  

#### <a name="to-identify-clients-that-use-wufb"></a>識別使用 WUfB 的用戶端  

1.  如果之前已啟用 Windows Update 代理程式，請予停用以免對 WSUS 進行掃描。   
    您可以設定登錄機碼 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**，指出電腦要執行 WSUS 或 Windows Update 掃描。  當值為 2 時，它不會執行 WSUS 掃描。  

2.  在 Configuration Manager 資源總管的 [Windows Update] 節點下，有個新屬性 **UseWUServer**。  

3.  根據透過 WUfB 連線之所有電腦的 **UseWUServer** 屬性，建立要更新和升級的集合。  

4.  建立用戶端代理程式設定，以停用軟體更新工作流程，並將設定部署至直接連線到 WUfB 的電腦集合。  

5.  透過 WUfB 管理的電腦會在相容性狀態中顯示 [不明]，而且不會計入整體相容性百分比的一部分。  

## <a name="configure-windows-update-for-business-deferral-policies"></a>設定 Windows Update for Business 延遲原則
<!-- 1290890 -->
從 Configuration Manager 1706 版開始，您可以為由 Windows Update for Business 直接管理的 Windows 10 裝置，設定 Windows 10「功能更新」或「品質更新」的延遲原則。 您可以在 [軟體程式庫] > [Windows 10 服務] 底下的新 [Windows Update for Business 原則] 節點中管理延遲原則。

### <a name="prerequisites"></a>先決條件
Windows Update for Business 所管理的 Windows 10 裝置必須能夠連線到網際網路。

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>建立 Windows Update for Business 延遲原則
1. 在 [軟體程式庫] > [Windows 10 服務] > [Windows Update for Business 原則] 中
2. 在 [首頁] 索引標籤的 [建立] 群組中，選取 [建立 Windows Update for Business 原則] 以開啟「建立 Windows Update for Business 原則精靈」。
3. 在 [一般] 頁面上，提供原則的名稱和描述。
4. 在 [延遲原則] 頁面上，設定是要延遲還是暫停「功能更新」。    
    「功能更新」通常是 Windows 的新功能。 在設定 [分支整備層級] 設定之後，您可以接著定義在 Microsoft 提供「功能更新」之後，是否要延遲接收「功能更新」，以及要延遲多久。
    - **分支整備層級**：設定裝置將接收其 Windows 更新的分支 (「最新分支」或「最新商務分支」)。
    - **延遲期 (天)**：指定「功能更新」的延遲天數。 您可以將這些「功能更新」的接收延遲 180 天 (自其發行日算起)。
    - **暫停功能更新開始**：選取是否要讓裝置在自暫停更新日算起最長可達 60 天的期間內，暫停接收「功能更新」。 在過了天數上限之後，暫停功能將自動失效，裝置將會掃描 Windows Update 是否有適用的更新。 進行此掃描之後，您可以再次暫停更新。 您可以取消選取此核取方塊來取消暫停「功能更新」。   
5. 選擇是要延遲還是暫停「功能更新」。     
    「品質更新」通常是對現有 Windows 功能的修正和改進，並且通常是在每個月的第一個星期二發佈，但是可由 Microsoft 隨時發行。 您可以定義在「品質更新」可供使用之後，是否要延遲接收「品質更新」，以及要延遲多久。
    - **延遲期 (天)**：指定「功能更新」的延遲天數。 您可以將這些「功能更新」的接收延遲 180 天 (自其發行日算起)。
    - **暫停品質更新開始**：選取是否要讓裝置在自暫停更新日算起最長可達 35 天的期間內，暫停接收「品質更新」。 在過了天數上限之後，暫停功能將自動失效，裝置將會掃描 Windows Update 是否有適用的更新。 進行此掃描之後，您可以再次暫停更新。 您可以取消選取此核取方塊來取消暫停「品質更新」。
6. 選取 [安裝來自其他 Microsoft 產品的更新]，以啟用讓延遲設定適用於 Microsoft Update 及 Windows Update 的群組原則設定。
7. 選取 [包含 Windows Update 的驅動程式] 以自動從 Windows Update 更新驅動程式。 如果您取消選取此設定，就不會從 Windows Update 下載驅動程式更新。
8. 完成精靈步驟以建立新的延遲原則。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>部署 Windows Update for Business 延遲原則
1. 在 [軟體程式庫] > [Windows 10 服務] > [Windows Update for Business 原則] 中
2. 在 [首頁] 索引標籤的 [部署] 群組中，選取 [部署 Windows Update for Business 原則]。
3. 進行以下設定：
    - **要部署的設定原則**：選取您要部署的 Windows Update for Business 原則。
    - **集合**：按一下 [瀏覽] 以選取您要部署原則的集合。
    - **支援時補救不符合規範的規則**：選取此選項即可針對 Windows Management Instrumentation (WMI)、登錄、指令碼以及 Configuration Manager 所註冊行動裝置的所有設定，自動補救所有不符合規範的原則。
    - **允許在維護期間以外補救**：如果已針對您部署原則的集合設定維護期間，啟用此選項即可讓合規性設定在維護期間之外補救值。 如需維護期間的詳細資訊，請參閱[如何在 Configuration Manager 中使用維護期間](/sccm/core/clients/manage/collections/use-maintenance-windows)。
    - **產生警示**：設定一個警示，以在設定基準合規性於指定的日期和時間低於指定百分比時產生警示。 您也可以指定是否要將警示傳送至 System Center Operations Manager。
    - **隨機延遲 (小時)**：指定一個延遲時間範圍，以避免「網路裝置註冊服務」的處理時間過長。 預設值是 64 小時。
    - **排程**：指定在用戶端電腦上評估已部署之設定檔時所依據的合規性評估排程。 此排程可以是簡易或自訂排程。 當使用者登入時，用戶端電腦會評估此設定檔。
4.  完成精靈步驟以部署設定檔。
