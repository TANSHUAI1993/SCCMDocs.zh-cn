---
title: "監視 Mobile Threat Defense 合規性 | System Center Configuration Manager"
description: "從 Configuration Manager 主控台監視 Mobile Threat Defense 合規性狀態"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**監視 Mobile Threat Defense 合規性**

*適用於：System Center Configuration Manager (最新分支)*

## <a name="to-monitor-the-overall-compliance-status"></a>監視整體的合規性狀態

監視 Mobile Threat Defense 狀態︰

1.  在 Configuration Manager 主控台中，按一下 [監視] 工作區。

2.  在 [監視]  工作區中，按一下 [安全性] 節點。

您會看見不同威脅等級的合規性狀態摘要會以視覺化圖表形式顯示。 您可以按一下圖表的各區段來查看詳細資訊，例如︰ 

- 平台報告為不符合規範之裝置的數量
- 與裝置合規性狀態相關的任何錯誤

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>監視個別的合規性狀態

您也可以查看個別的裝置狀態︰

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性] 工作區。

2.  按一下 [裝置]。

> [!TIP] 
> 您可以新增 [裝置威脅合規性] 和 [裝置威脅等級] 欄位來查看狀態。 預設不會顯示這些欄位。

## <a name="device-threat-protection-tab"></a>[裝置威脅保護] 索引標籤

此外，在 [裝置] 畫面中，您可以選取特定的裝置，然後按一下 [裝置威脅保護] 索引標籤，提供有關裝置合規性狀態的其他詳細資訊。 尋找下面的欄位描述與其預期值，以協助您分析裝置合規性狀態。

> [!IMPORTANT] 
> 只有當選取的裝置是行動裝置時，才會顯示 [裝置威脅保護] 索引標籤。

|欄名|預設為可見|說明| 
|-|-|-|
|**說明**| 是 | Mobile Threat Defense 合作夥伴所提供的威脅詳細資料。 |
|**上次更新時間**| 是 | Mobile Threat Defense 合作夥伴上次在何時傳送有關 Intune 威脅的更新詳細資訊。 |
|**威脅嚴重性**| 是 | 威脅嚴重性是根據 Mobile Threat Defense 合作夥伴主控台中系統管理員的設定來為個別威脅定義。 其為下列三個值之一︰[低]、[中] 或 [高] |
|**威脅狀態**| 是 | 裝置上目前的威脅狀態。 可能的狀態︰[作用中]、[已解決]或[已略過]︰指出使用者已忽略其裝置上的威脅，但該威脅仍然存在。 |
|**威脅類型**| 是 | 威脅的 Mobile Threat Defense 合作夥伴類型。 可能的值︰[應用程式]、[檔案] 或 [作業系統] |
|**AAD 帳戶識別碼**| 否 | Azure Active Directory 的唯一識別碼。 |
|**分類**| 是 | Mobile Threat Defense 合作夥伴提供的威脅分類。 可能的值︰**Root 啟用程式、風險軟體、廣告軟體、收費軟體、資料洩漏、特洛伊木馬病毒、蠕蟲、病毒、入侵程式、後門程式、Bot、應用程式病毒植入程式、點擊詐欺、垃圾郵件、間諜軟體、監視軟體、弱點、不明、Root 越獄、連線、電話詐欺、側載應用程式** |
|**裝置識別碼**| 否 | 代表有威脅資訊的已加入工作場所的裝置 Azure Active Directory 物件識別碼。 |
|**威脅識別碼**| 否 | Mobile Threat Defense 合作夥伴針對威脅產生的唯一識別碼。 威脅識別碼用來追蹤解決方法。 |
|**威脅 URL**| 否 | 存在時，威脅 URL 可連結回到此特定威脅的 Mobile Threat Defense 合作夥伴管理主控台檢視。 |

> [!TIP] 
> 請務必啟用不是「預設為可見」的欄位，以查看您裝置的 Mobile Threat Defense 合規性狀態詳細資訊。
