---
title: "根據風險限制存取權 | Microsoft Docs"
description: "根據裝置、網路和應用程式的風險，來限制公司資源的存取權。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>根據裝置、網路和應用程式的風險，來管理公司資源的存取權

*適用於：System Center Configuration Manager (最新分支)*

您可以依據由 Lookout 執行的風險評估 (Lookout 為整合 Microsoft Intune 的裝置威脅防護解決方案)，控制行動裝置的公司資源存取權。 Lookout 服務會收集裝置的作業系統 (OS) 漏洞、已安裝的惡意應用程式和惡意網路設定檔的遙測，作為風險依據。 

根據 Lookout 報告的風險評估 (透過 System Center Configuration Manager (SCCM) 合規性政策加以啟用)，您可以設定條件式存取原則，以允許或封鎖判定為不符合規範的裝置，因為這些裝置上偵測到潛在威脅。

[混合式 MDM 部署 (整合 SCCM 與 Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) 可讓您依據由 Lookout 這類裝置威脅防護解決方案執行的風險評定，來控制公司資源與資料的存取權。

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>混合式 MDM 部署和 Lookout 裝置威脅防護如何協助保護公司資源？
在行動裝置上執行 Lookout 行動裝置應用程式 (Lookout for Work) 時，其可擷取檔案系統、 網路堆疊、裝置和應用程式的遙測 (如果適用的話)，並傳送至 Lookout 裝置威脅防護雲端服務，以計算行動威脅的彙總裝置風險。 您也可以在 Lookout 主控台中視需求變更潛在威脅的風險層級分類。  

現在，SCCM 中的合規性政策包含適用於 Lookout Mobile Threat Protection 的新規則，該規則是以 Lookout 裝置威脅風險評估為依據。 啟用此規則時，系統會評估裝置的合規性。

如果裝置的判定結果為不符合合規性政策，即會使用條件式存取原則封鎖 Exchange Online 和 SharePoint Online 這類資源的存取權。 當存取遭到封鎖時，系統會提供使用者有助解決問題的逐步解說，以獲得公司資源的存取權。 本逐步解說會透過 Lookout for Work 應用程式加以啟動。

## <a name="supported-platforms"></a>支援的平台：
* **Android 4.1 和更新版本**，並在 Microsoft Intune 中註冊。
* **iOS 8 和更新版本**，並在 Microsoft Intune 中註冊。
如需 Lookout 支援的平台和語言資訊，請參閱[這篇文章](https://personal.support.lookout.com/hc/en-us/articles/114094140253)。

## <a name="prerequisites"></a>必要條件：
* [混合式 MDM 部署](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Microsoft Intune 和 Azure Active Directory 的訂閱。
* Lookout Mobile EndPoint Security 的企業訂閱。  如需詳細資訊，請參閱 [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>範例案例
以下是一些常見的案例：
### <a name="control-access-based-on-threat-from-malicious-apps"></a>依據惡意應用程式的威脅來控制存取權：
在裝置上偵測到惡意應用程式 (如惡意程式碼) 時，您可以封鎖這些裝置，使其不得：
* 連線到公司的電子郵件 (需等到威脅解決之後才行)。
* 使用 OneDrive for Work 應用程式同步處理公司的檔案。
* 存取業務關鍵的應用程式。

**當偵測到惡意應用程式時，封鎖存取：**

![此圖表顯示，當裝置因為其中的惡意應用程式導致判定為不符合規範時，條件式存取原則會封鎖存取](media/config-mgr-maliciousapps_blocked.png)

**威脅修復之後，裝置即解除封鎖並可存取公司資源：**

![此圖表顯示，當裝置在修復之後判定為符合規範時，條件式存取原則會允許存取](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>依據網路威脅來控制存取權：
偵測您的網路威脅 (例如攔截式攻擊)，並依據裝置風險來限制存取 WiFi 網路。

**透過 WiFi 封鎖網路存取：**

![此圖表顯示，條件式存取依據網路威脅來封鎖 WiFi 的存取](media/config-mgr-network-wifi-blocked.png)

**修復後允許存取：**

![此圖表顯示，條件式存取在威脅修復之後允許存取](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>依據網路威脅來控制存取 SharePoint Online：

偵測您的網路威脅 (例如攔截式攻擊)，並依據裝置風險來防止同步處理公司的檔案。

**根據裝置上偵測到的網路威脅，封鎖存取 SharePoint Online：**

![此圖表顯示，條件式存取會根據威脅偵測，封鎖裝置存取 SharePoint Online](media/config-mgr-network-spo-blocked.png)


**修復後允許存取：**

![此圖表顯示，條件式存取在網路威脅修復之後允許存取](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>後續步驟
您必須執行下列主要步驟來實作這個解決方案：
1.  [設定您的訂閱與 Lookout Mobile Threat Protection](set-up-your-subscription-with-lookout.md)
2.  [在 Intune 中啟用 Lookout MTP 的連線](enable-lookout-connection-in-intune.md)
3.  [設定和部署 Lookout for Work 應用程式](configure-and-deploy-lookout-for-work-apps.md)
4.  [設定合規性政策](enable-device-threat-protection-rule-compliance-policy.md)
5.  [對 Lookout 整合進行疑難排解](troubleshoot-lookout-integration.md)
