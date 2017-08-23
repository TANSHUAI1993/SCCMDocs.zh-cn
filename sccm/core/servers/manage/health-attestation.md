---
title: "健全狀況證明 | Microsoft Docs"
description: "深入了解可在 Configuration Manager 主控台中檢視的裝置健全狀況證明功能。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: "17"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 54b3433a002b8ef29059bab04458138348f95d66
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>System Center Configuration Manager 的健康情況證明

*適用於：System Center Configuration Manager (最新分支)*

系統管理員可以在 Configuration Manager 主控台內檢視 [Windows 10 裝置健康情況證明](https://technet.microsoft.com/library/mt592023.aspx)的狀態。  系統管理員可透過裝置健康情況證明，確認用戶端電腦已啟用下列可信任的 BIOS、TPM 及開機軟體設定：  

-   開機初期啟動的反惡意程式碼 - 開機初期啟動的反惡意程式碼 (ELAM) 可在您電腦啟動時且在其他廠商驅動程式初始化之前，為它提供保護。 [如何開啟 ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker -「Windows BitLocker 磁碟機加密」是一種軟體，可讓您將存放在 Windows 作業系統磁碟區上的所有資料都加密。  [如何開啟 BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   安全開機 -「安全開機」是由電腦產業成員所開發的一種安全標準，可協助確保您的電腦只使用電腦製造商信任的軟體來開機。 [深入了解安全開機](https://technet.microsoft.com/library/hh824987.aspx)  
-   程式碼完整性 -「程式碼完整性」是一項功能，可藉由在每次將驅動程式或系統檔案載入記憶體時驗證其完整性，改進作業系統的安全性。 [深入了解程式碼完整性](https://technet.microsoft.com/library/dd348642.aspx)  

由 Configuration Manager 管理的電腦和內部部署資源，以及透過 Microsoft Intune 管理的行動裝置，皆可使用這項功能。 系統管理員可以指定要透過雲端還是內部部署基礎結構來執行報告。 內部部署裝置健康情況證明監視可讓系統管理員監視無法存取網際網路的用戶端電腦。

## <a name="enable-health-attestation"></a>啟用健康情況證明

 **需求：**  

-   執行 Windows 10 版本 1607 或 Windows Server 2016 版本 1607 並[已啟用裝置健康情況證明](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)的用戶端裝置
-    支援 TPM 1.2 或 TPM 2 的裝置
-   Configuration Manager 用戶端代理程式與 has.spserv.microsoft.com (連接埠 443)「健康情況證明」服務 (雲端管理) 之間或與支援裝置健康情況證明的管理點 (內部部署) 之間的通訊

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 用戶端電腦上啟用健康情況證明服務通訊

請使用此程序，為連接到網際網路的裝置，啟用裝置健康情況證明監視。

1.  在 Configuration Manager 主控台中，選擇 **[系統管理]** > **[概觀]** > **[用戶端設定]**。  選取 **[電腦代理程式]** 設定索引標籤。  
2.  在 **[預設設定]** 對話方塊中，選取 **[電腦代理程式]** ，然後向下捲動到 **[啟用與健康情況證明服務之間的通訊]**。  
3.  將 **[啟用與健康情況證明服務之間的通訊]** 設定為 **[是]**，然後按一下 **[確定]**。  
4. 將應該回報裝置健康情況的裝置集合設為目標。

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>如何在 Configuration Manager 用戶端電腦上啟用內部部署健康情況證明服務通訊
請使用此程序，為沒有連接到網際網路的內部部署裝置，啟用裝置健康情況證明監視。

從 Configuration Manager 1702 版開始，您可以在管理端點上設定內部部署裝置健康情況證明服務 URL，以支援無法存取網際網路的用戶端裝置。

1. 在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [概觀] > [站台設定] > [站台]。
2. 在具有支援內部部署裝置健康情況證明用戶端之管理點的主要站台或次要站台上按一下滑鼠右鍵，然後選取 [設定站台元件] > [管理點]。 [管理點元件內容] 頁面隨即開啟。
3. 在 [進階選項] 索引標籤上，選取 [新增]，然後指定一個有效的內部部署裝置健康情況證明服務 URL。 您可以新增多個 URL。 如果指定多個內部部署 URL，用戶端就會收到整組 URL，然後隨機選擇要使用的 URL。
4.  在 Configuration Manager 主控台中，選擇 **[系統管理]** > **[概觀]** > **[用戶端設定]**。  選取 **[電腦代理程式]** 設定索引標籤。  
5.  在 [預設設定] 對話方塊中，選取 [電腦代理程式] ，然後向下捲動到 [使用內部部署健康情況證明服務] 並設定為 [是]。
6. 使用用戶端代理程式設定，將應該回報裝置健康情況的裝置集合設為目標，以啟用裝置健康情況證明報告功能。

您也可以「編輯」或「移除」裝置健康情況證明服務 URL。

> [!NOTE]
> 如果您在升級至 Configuration Manager 1702 版之前即已使用裝置健康情況證明，則在升級時，管理點內容中會預先填入用戶端代理程式設定中指定的內部部署 URL。 內部部署用戶端在升級前會繼續使用用戶端代理程式設定中指定的 URL。 之後，它們就會切換到管理端點上指定的其中一個 URL。

## <a name="monitor-device-health-attestation"></a>監視裝置健康情況證明

1.  若要檢視裝置健康情況證明檢視，請在 Configuration Manager 主控台中，移至 **[監視]** 工作區，按一下 **[安全性]** 節點，然後按一下 **[健康情況證明]**。  
2.  隨即會顯示「裝置健康情況證明」。  

Configuration Manager 的裝置健康情況證明會顯示下列各項資訊：  

-   **健康情況證明狀態** - 顯示處於相容、不相容、錯誤及不明狀態的裝置比例  
-   **回報健康情況證明的裝置** - 顯示回報「健康情況證明」狀態的裝置百分比  
-   **不相容的裝置 (依用戶端類型)** - 顯示不相容之行動裝置和電腦的比例  
-   **遺失的前幾項健康情況證明設定** - 顯示遺漏健康情況證明設定的裝置數目 (依每個設定列出)

「用戶端裝置健康情況證明」狀態可用來針對使用 Configuration Manager 搭配 Microsoft Intune 來管理的裝置，定義合規性政策中的條件式存取規則。 如需詳細資訊，請參閱[管理 System Center Configuration Manager 中的裝置相容性原則](/sccm/protect/deploy-use/device-compliance-policies)。  
