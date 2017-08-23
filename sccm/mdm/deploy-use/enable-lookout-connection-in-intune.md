---
title: "在 Intune 中啟用 Lookout MTP | Microsoft Docs"
description: "在 Intune 管理主控台中啟用 Lookout Mobile Threat Protection。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f9ddbcc981fa1274a41ae16a6a939c0cdf739c3e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>在 Intune 管理主控台中啟用 Lookout MTP 連線

*適用於：System Center Configuration Manager (最新分支)*

本主題說明如何在 Intune 中啟用 Lookout MTP 連線。 您應該先在 Lookout 主控台中設定 Intune 連接器再執行此步驟。  如果尚未設定，請執行[設定 Lookout Mobile Threat Protection 訂閱](set-up-your-subscription-with-lookout.md)中所述的步驟。

若要在 Intune 中啟用 Lookout MTP 連線，請在 [Microsoft Intune 系統管理員主控台](https://manage.microsoft.com) 的 [管理] 頁面中，選擇 [Third Party Service Integration]\(協力廠商服務整合)。 選擇 [Lookout 狀態] 並使用切換按鈕啟用 [與 MTP 同步處理]。

![反白顯示啟用切換按鈕的 Lookout 同步處理頁面的螢幕擷取畫面](media/lookout-intune-synchronization.png)

如此即在 Intune 系統管理員主控台中完成 Lookout 與 Intune 整合設定。  接下來實作此解決方案的步驟，涉及部署 [Lookout 工作應用程式](configure-and-deploy-lookout-for-work-apps.md)以及設定[合規性](enable-device-threat-protection-rule-compliance-policy.md)原則。

>[!IMPORTANT]
> 您**必須**先設定 Lookout 工作應用程式，再建立合規性政策規則及設定條件式存取。 這可確保在使用者能存取電子郵件或其他公司資源之前，應用程式即已就緒供使用者安裝。

## <a name="next-steps"></a>後續步驟
[設定 Lookout 工作應用程式](configure-and-deploy-lookout-for-work-apps.md)
