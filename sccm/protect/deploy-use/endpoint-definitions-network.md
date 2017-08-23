---
title: "來自網路共用的 Endpoint Protection 惡意程式碼定義 | Microsoft Docs"
description: "了解如何手動從 Microsoft 下載最新的定義更新，然後將用戶端設定為下載這些定義。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 110bd9a9d04b27ef6794145fae66dbd910308bdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>啟用 Endpoint Protection 惡意程式碼定義，從網路共用針對 Configuration Manager 下載

*適用於：System Center Configuration Manager (最新分支)*

 您可以手動從 Microsoft 下載最新的定義更新，然後將用戶端設定為從網路上的共用資料夾下載這些定義。 當您使用此更新來源時，使用者也可以初始定義更新。

> [!NOTE]
>  用戶端必須具有共用資料夾的讀取權，才能夠下載定義更新。

 如需如何下載定義及引擎更新以將其儲存在檔案共用上的詳細資訊，請參閱 [Install the latest Microsoft antimalware and antispyware software](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx) (安裝最新的 Microsoft 反惡意程式碼和反間諜功能軟體)。

## <a name="to-configure-definition-downloads-from-a-file-share"></a>設定檔案共用中的定義下載

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。

2.  在 [資產與相容性]  工作區中，展開 [Endpoint Protection] ，然後按一下 [反惡意程式碼原則] 。

3.  開啟 [預設反惡意程式碼原則]  的 [內容] 頁面，或建立新的反惡意程式碼原則。 如需如何建立反惡意程式碼原則的詳細資訊，請參閱[如何在 Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。

4.  在 [反惡意程式碼內容] 對話方塊的 [定義更新]  區段中，按一下 [設定來源] 。

5.  在 [設定定義更新來源]  對話方塊中，選取 [來自 UNC 檔案共用的更新] 。

6.  按一下 [確定]  關閉 [設定定義更新來源]  對話方塊。

7.  按一下 [設定路徑] 。 然後，在 [設定定義更新 UNC 路徑]  對話方塊中，將一或多個 UNC 路徑新增至網路共用上定義更新檔的位置。

8.  按一下 [確定]  關閉 [設定定義更新 UNC 路徑]  對話方塊。


> [!div class="button"]
[下一步 >](endpoint-antimalware-policies.md)

> [!div class="button"]
[上一步 >](endpoint-configure-alerts.md)
