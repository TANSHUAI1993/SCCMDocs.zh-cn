---
title: "選擇 Intune 獨立部署或混合式 MDM | Microsoft Docs"
description: "選擇要部署使用 Intune 和 Configuration Manager 的混合式行動裝置管理，還是要執行 Intune 獨立部署。"
ms.custom: na
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: "10"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 26c36df77c21254c7ad2b8a45906bd3706f9ec65
ms.sourcegitcommit: 06aef618f72c700f8a716a43fb8eedf97c62a72b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2017
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>在 Microsoft Intune 獨立部署與使用 System Center Configuration Manager 的混合式行動裝置管理之間進行選擇

*適用於：System Center Configuration Manager (最新分支)*

使用 Microsoft Intune 進行行動裝置管理 (MDM) 時，最常詢問的其中一個問題就是：「我應該整合 Intune 和 Configuration Manager (混合式 MDM)，還是在僅限雲端的設定中執行 Intune 獨立部署？」 若要回答此問題，您應該仔細比較這兩個選項。

## <a name="intune-standalone"></a>Intune 獨立部署
Intune 獨立部署是 Microsoft 建議的部署拓撲。 Intune 獨立部署是僅限雲端的 MDM 解決方案，可透過可從世界各地存取的 Web 主控台來進行管理。 北美洲、歐洲和亞洲都有託管的 Intune Datacenter。 因為 Intune 是雲端服務，所以您可以在相對較短的時間範圍內將 Intune 管理部署到您的裝置。

客戶通常會發現部署獨立拓撲更為快速且輕鬆，因為沒有內部部署元件的相依性。 Intune 獨立部署現在已在 Microsoft Azure 雲端平台上，且提供如下的多種進階功能：
- 整合的企業行動管理平台：Azure 入口網站中的整合雲端平台與系統管理體驗，可用於 Intune、Azure AD Premium 與 Azure 資訊保護。
- 行動裝置管理：眾多的行動裝置管理與資訊保護功能。
- 彈性規模：部署與管理行動裝置，而不需要擔心規模的問題。
- 角色型存取控制：根據指派的角色與範圍來限制系統管理功能的存取。
- 以程式設計方式存取 (API)：支援 Microsoft Graph API，以及 SDK 和 PowerShell 管理選項。
- Web 主控台：依 Web 標準打造的 HTML 5 主控台，可支援大多數的新式網頁瀏覽器。
- 進階報告：可建立自訂報告的功能。
- 靈活性：安裝簡單，且能快速傳遞新功能。


## <a name="hybrid-mdm-with-configuration-manager"></a>搭配 Configuration Manager 的混合式 MDM
混合式 MDM 是將 Intune 行動裝置管理功能整合至 Configuration Manager 的解決方案。 它使用 Intune 作為將原則、設定檔和應用程式傳遞至裝置的傳遞通道，但使用 Configuration Manager 內部部署基礎結構來管理內容與裝置。 混合式實作提供了「單一整合窗口」控制功能。  這表示您可以使用相同的內部部署基礎結構和系統管理主控台透過 Intune 來管理行動裝置，以及透過傳統 Configuration Manager 用戶端來管理電腦和伺服器。 基於如下原因，可選擇混合式 MDM：  
- 您想要藉由相同的系統管理主控台，以管理在 Intune 中註冊的行動裝置，以及使用 Configuration Manager 用戶端管理的裝置
- 您的基礎結構需要有多部 NDES 伺服器，以便將憑證傳遞到行動裝置
- 您的基礎結構需要有多個 Exchange 連接器
- 您需要 S/MIME 加密支援


## <a name="changing-the-mdm-authority-setting"></a>變更 MDM 授權單位設定
若需要變更 MDM 授權單位設定，不需要連絡 Microsoft 支援服務，也不需要將現有受管理裝置解除註冊並重新註冊，便可以自行變更。 如需詳細資訊，請參閱[變更您的 MDM 授權單位](../deploy-use/change-mdm-authority.md)。

> [!NOTE]    
> 您必須要有 Configuration Manager 1610 版或更新的版本，才能將 MDM 授權單位變更為 Intune 獨立部署。 若是使用先前版本的 Configuration Manager，仍然可以變更 MDM 授權單位，但是需要 Microsoft 支援服務與作業的協助。 同時您也需要在變更 MDM 授權單位之後，解除註冊並重新註冊所有的裝置。  
