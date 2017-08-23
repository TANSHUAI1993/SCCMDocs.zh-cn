---
title: "Endpoint Protection 用戶端說明 | Microsoft Docs"
description: "深入了解 Endpoint protection 功能和增強功能，協助您保護電腦免受威脅。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
caps.latest.revision: "6"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 212c73fcb947c3b56da6055bf47fe078301ad90d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection-client-help"></a>Endpoint Protection 用戶端說明

*適用於：System Center Configuration Manager (最新分支)*


此版本的 Windows Defender 或 Endpoint Protection 包含下列功能，可協助保護電腦免受威脅：  

-   **Windows 防火牆整合。** Endpoint Protection 設定可讓您開啟或關閉 Windows 防火牆。  
-   **網路檢查系統：** 這項功能透過檢查網路流量，協助您主動封鎖已知網路弱點的惡意探索，藉此增強即時防護。  
-   **防護引擎。** 即時保護會尋找並停止在您的電腦上安裝或執行惡意程式碼。 更新的引擎提供增強的偵測和清理功能，效能更佳。  

Windows Defender 是 Windows 10 作業系統的一部分。  在舊版 Windows 中，您的系統管理員可以使用管理軟體來提供 Windows Defender 或 Endpoint Protection。

您也可以找到 [Windows Defender 和 Endpoint Protection 常見問題集](endpoint-protection-client-faq.md)的清單。 如需協助進行疑難排解，請參閱[針對 Windows Defender 或 Endpoint Protection 用戶端進行疑難排解](troubleshoot-endpoint-client.md)。 如需新功能的清單，請參閱 [Windows Defender 用戶端的新功能](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender)。

## <a name="windows-firewall-integration"></a>Windows 防火牆整合  
 Windows 防火牆有助於防止攻擊者或惡意軟體透過網際網路或網路存取電腦。 現在當您安裝 Endpoint Protection 時，安裝精靈會驗證 Windows 防火牆是否已開啟。 如果您刻意關閉 Windows 防火牆，可以取消選取核取方塊，避免將它開啟。 可以透過 [控制台] 的 [系統及安全性] 設定，隨時變更 Windows 防火牆設定。  

## <a name="network-inspection-system"></a>網路檢查系統  
 在軟體廠商開發及散佈安全性更新之前，攻擊者會對公開的弱點發動一波波的網路攻擊。 弱點研究顯示，從最初攻擊報告到開發、測試及發行合適的安全性更新，可能需要一個月以上的時間。 這段防護空窗期讓許多電腦遭受長期的攻擊和入侵。 網路檢查系統與即時防護搭配運作，將弱點揭露與更新部署之間的時間間隔從數星期大幅減少為數小時，更有助於防止網路型攻擊。  

## <a name="award-winning-protection-engine"></a>獲獎的防護引擎  
 Windows Defender 或 Endpoint Protection 內含獲獎的保護引擎，這個引擎會定期更新。 由 Microsoft 惡意程式碼防護中心中的反惡意程式碼研究者團隊所支援，提供最新惡意程式碼威脅的回應，全年無休。  

## <a name="windows-defender-settings"></a>Windows Defender 設定
Windows Defender 設定可啟用設定來協助保護電腦免受惡意軟體攻擊。 您的系統管理員可能會管理部分 Windows Defender 設定。 您可以使用 Windows Defender 設定來管理其他人。 建議您啟用 Windows Defender 設定來協助保護您的電腦和資料。

若要檢視 Windows Defender 設定，請在您的電腦上搜尋 `Windows Defender`。 開啟 **Windows Defender**，然後選取 [設定]。 Windows Defender 設定包含：
- **即時保護** - 尋找並停止在您的電腦上安裝或執行惡意程式碼。
- **雲端型保護** - Windows Defender 會將有關潛在安全性威脅的資訊傳送給 Microsoft。
- **自動提交範例** - 允許 Windows Defender 將可疑檔案範例傳送給 Microsoft，以協助改善惡意程式碼偵測。
- **排除項目** - 您可以排除特定檔案、資料夾、副檔名或處理程序，不進行 Windows Defender 掃描。
- **增強型通知** - 啟用通知有關電腦健全狀況的通知。 即使 [關閉]，您還是會收到重大通知。
- **Windows Defender Offline** - 您可以執行 Windows Defender Offline，來協助尋找並移除惡意軟體。 此掃描將會重新啟動您的電腦，而且需要大約 15 分鐘。

### <a name="see-also"></a>請參閱  
 [Endpoint Protection 用戶端常見問題集](endpoint-protection-client-faq.md)   
 [Windows Defender 或 Endpoint Protection 用戶端疑難排解](troubleshoot-endpoint-client.md)
