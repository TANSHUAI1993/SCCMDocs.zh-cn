---
title: "啟用合規性原則中的裝置保護規則 | Microsoft Docs"
description: "啟用裝置合規性原則中的行動裝置威脅保護規則。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: faa92e150686e615164ce3f5435b77a65305aab3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>啟用合規性原則中的裝置威脅保護規則

*適用於：System Center Configuration Manager (最新分支)*

具有 Lookout 行動裝置威脅保護的 Intune 可讓您偵測行動裝置威脅，並在裝置上進行風險評定。 您可以在 Configuration Manager 中建立合規性原則規則以納入風險評定來判斷裝置是否符合規範。 接著，您可以使用條件式存取原則，根據裝置合規性來允許或封鎖存取 Exchange、SharePoint 和其他服務。

若要讓 Lookout 裝置威脅偵測影響裝置的合規性原則：

* 必須啟用合規性原則中的 [裝置威脅保護] 規則。

* [Intune 系統管理員主控台] 中的 [Lookout 狀態] 必須顯示為 [作用中]。 如需如何啟用 Lookout 整合的詳細資訊和指示，請參閱[在 Intune 中啟用 Lookout MTP 連線](enable-lookout-connection-in-intune.md)主題。


在合規性原則中建立裝置威脅保護規則之前，建議您先[設定訂用帳戶使用 Lookout 裝置威脅防護](set-up-your-subscription-with-lookout.md)、[在 Intune 中啟用 Lookout 連線](enable-lookout-connection-in-intune.md)並[設定 Lookout for Work 應用程式](configure-and-deploy-lookout-for-work-apps.md)。 只有在設定完成之後，才會強制執行合規性原則。

若要啟用裝置威脅保護規則，您可以使用現有的合規性原則或建立新的合規性原則。

在 Lookout 裝置威脅保護的設定過程中，您已在 [Lookout 主控台](https://aad.lookout.com)中建立原則，將各種威脅分類為高、中與低等級。 在 Intune 合規性原則中，您將使用威脅等級來設定允許的最高威脅等級。

在合規性原則精靈的 [規則] 頁面，以下列資訊定義新的規則：
  * 條件：裝置威脅保護的最高風險等級。
  * 值：值必須為下列其中一項：
    * **無 (受保護)**：這是最安全的選項。 這表示裝置不能受到任何威脅。 如果發現任何威脅，會將裝置評估為不符合規範。
    * **低**：如果僅存在低等級的威脅，會將裝置評估為符合規範。 任何較高等級的威脅會使裝置變成不符合規範的狀態。
    * **中**：如果在裝置上發現的威脅為低等級或中等級，會將裝置評估為符合規範。 如果偵測到高等級的威脅，會將裝置判斷為不符合規範。
    * **高**：這是最不安全的選項。 基本上這會允許所有的威脅等級，而且可能只有在您只針對報告用途而使用此解決方案時才有用。

如果您針對 Office 365 和其他服務建立條件式存取原則，則上述的合規性評估會納入考量，並且會封鎖不符合規範的裝置存取公司資源，直到威脅解決為止。

裝置威脅保護狀態顯示於 [監視] 工作區的 [安全性] 節點上。
各種威脅等級狀態的摘要會以視覺化圖表顯示。 您可以按一下圖表的個別區段來查看詳細資訊，例如平台報告為不符合規範之裝置的數量，以及已報告的任何錯誤。
您也可以在 [資產與合規性] 工作區的 [裝置] 底下查看個別裝置狀態。  您可以新增 [裝置威脅合規性] 和 [裝置威脅等級] 欄位來查看狀態。  預設不會顯示這些欄位。
