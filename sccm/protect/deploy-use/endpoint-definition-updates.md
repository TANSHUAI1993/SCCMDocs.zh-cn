---
title: "設定 Endpoint Protection | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 選取及設定 Endpoint Protection 方法，讓用戶端電腦上的反惡意程式碼定義保持最新狀態。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b5da7900a4f8e2f330c4dcb2cac00b45099bd909
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-definition-updates-for-endpoint-protection"></a>設定 Endpoint Protection 的定義更新  

*適用於：System Center Configuration Manager (最新分支)*

 使用 System Center Configuration Manager 中的 Endpoint Protection，您可以使用數種方法中的任何一項方法，將階層中用戶端電腦上反惡意程式碼的定義維持在最新狀態。 本主題中的資訊可以協助您選取及設定這些方法。

 若要更新反惡意程式碼定義，您可以使用一或多個下列方法：

-   [從 Configuration Manager 發佈的更新](endpoint-definitions-configmgr.md) – 此方法會使用 Configuration Manager 軟體更新，將定義及引擎更新傳遞到階層中的電腦。

-   [從 Windows Server Update Services (WSUS) 發佈的更新](endpoint-definitions-wsus.md) - 此方法使用 WSUS 基礎結構，將定義和引擎更新傳遞給電腦。

-   [從 Microsoft Update 發佈的更新](endpoint-definitions-microsoft-updates.md) - 此方法可讓電腦直接連線到 Microsoft Update，以下載定義及引擎更新。 這個方法對未經常連線到商業網路的電腦很有用。

-   [從 Microsoft 惡意程式碼防護中心發佈的更新](endpoint-definitions-protection-center.md) - 此方法會從 Microsoft 惡意程式碼防護中心下載定義更新。

-   [來自 UNC 檔案共用的更新](endpoint-definitions-network.md) - 使用此方法，您可以將最新的定義和引擎更新儲存到網路上的共用。 之後，用戶端便可以存取網路來安裝更新。

 您可以設定多個定義更新來源，並控制其受到評估及套用的順序。 此程序是在您建立反惡意程式碼原則時，於 [設定定義更新來源]  對話方塊中所完成。

> [!IMPORTANT]
>  對於 Windows 10 電腦，您必須設定 Endpoint Protection，以更新 Windows Defender 的惡意程式碼定義。

## <a name="how-to-configure-definition-update-sources"></a>如何設定定義更新來源
 使用下列程序，設定要用於每個反惡意程式碼原則的定義更新來源。

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。

2.  在 [資產與相容性]  工作區中，展開 [Endpoint Protection] ，然後按一下 [反惡意程式碼原則] 。

3.  開啟 [預設反惡意程式碼原則]  的 [內容] 頁面，或建立新的反惡意程式碼原則。 如需如何建立反惡意程式碼原則的詳細資訊，請參閱[如何在 Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。

4.  在 [反惡意程式碼內容] 對話方塊的 [定義更新]  區段中，按一下 [設定來源] 。

5.  在 [設定定義更新來源]  對話方塊中，選取用要於定義更新的來源。 您可以按一下 [上]  或 [下]  來修改使用這些來源的順序。

6.  按一下 [確定]  關閉 [設定定義更新來源]  對話方塊。

## <a name="configure-endpoint-protection-definitions"></a>設定 Endpoint Protection 定義

-   [從 Configuration Manager 發佈的更新](endpoint-definitions-configmgr.md) – 此方法會使用 Configuration Manager 軟體更新，將定義及引擎更新傳遞到階層中的電腦。

-   [從 Windows Server Update Services (WSUS) 發佈的更新](endpoint-definitions-wsus.md) - 此方法使用 WSUS 基礎結構，將定義和引擎更新傳遞給電腦。

-   [從 Microsoft Update 發佈的更新](endpoint-definitions-microsoft-updates.md) - 此方法可讓電腦直接連線到 Microsoft Update，以下載定義及引擎更新。 這個方法對未經常連線到商業網路的電腦很有用。

-   從 Microsoft 惡意程式碼防護中心發佈的更新 - 此方法會從 Microsoft 惡意程式碼防護中心下載定義更新。

-   [來自 UNC 檔案共用的更新](endpoint-definitions-network.md) - 使用此方法，您可以將最新的定義和引擎更新儲存到網路上的共用。 之後，用戶端便可以存取網路來安裝更新。
