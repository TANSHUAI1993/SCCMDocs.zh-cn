---
title: "自動將裝置分類為集合 | Microsoft Docs"
description: "使用 System Center Configuration Manager 自動將裝置分類為集合。"
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d1b79fb091a6ae4b967d63843ae7b45a0cbeb555
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自動將裝置分類為集合

適用於：System Center Configuration Manager (最新分支)

您可以建立裝置類別，如此可在您使用 Configuration Manager 與 Microsoft Intune 時自動將裝置放在裝置集合中。 使用者向 Intune 註冊裝置時，必須選擇裝置類別。 您可以從 Configuration Manager 主控台變更裝置類別。

> [!IMPORTANT]  
    >  這項功能適用於 Microsoft Intune 的 **2016 年 6 月**版及更新版本。 請先確定已更新為此版，再嘗試這些程序。

## <a name="create-device-categories"></a>建立裝置類別

1.  移至 [資產與合規性] > [概觀] > [裝置集合]。
2.  在 [常用] 索引標籤的 [裝置集合] 群組中，選擇 [管理裝置類別]。
3.  建立、編輯或移除類別目錄。

## <a name="associate-a-collection-with-a-device-category"></a>建立集合與裝置類別的關聯

當您建立集合與裝置類別的關聯時，該類別中的所有裝置都會新增至該集合。 您無法將裝置類別規則新增至內建集合，例如 [所有系統]。

1.  在裝置集合之 [內容] 對話方塊的 [成員資格規則] 索引標籤上，選擇 [新增規則] > [裝置類別規則]。
2.  在 [選取裝置類別] 對話方塊中，選取將套用至集合中所有裝置的一或多個裝置類別。

## <a name="change-the-category-of-a-device"></a>變更裝置類別

1.  在 [資產與合規性] > [概觀] > [裝置] 下，從 [裝置] 選取裝置。
2.  在 [首頁] 索引標籤的 [裝置] 群組中，選擇 [變更類別]。
3.  選擇一個類別，然後選擇 [確定]。

## <a name="view-which-category-a-device-belongs-to"></a>檢視裝置屬於哪個類別

在 [資產與合規性] > [概觀] > [裝置] 的 [裝置] 清單中，類別會顯示在 [裝置類別] 欄。

如果 [裝置類別] 欄未顯示，請以滑鼠右鍵按一下 [裝置] 清單中的其中一個欄標題 (例如 [名稱])，然後選取 [裝置類別]。

如果您將裝置指派給一個類別，然後刪除該類別，[Microsoft Intune 中每位使用者註冊的裝置清單] 報告會在 [裝置類別] 欄中顯示 GUID，而不是類別名稱。
