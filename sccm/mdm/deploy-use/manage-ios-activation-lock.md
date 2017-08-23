---
title: "管理 iOS 啟用鎖定 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理 iOS 啟用鎖定。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 88bef04a52f716ae13afc21c25d33dea06a3fc9c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理 iOS 啟用鎖定

適用於：System Center Configuration Manager (最新分支)


System Center Configuration Manager 可以協助您管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的功能。 啟用「啟用鎖定」時，必須先輸入使用者的 Apple ID 和密碼，才能讓所有人：

- 關閉「尋找我的 iPhone」
- 清除裝置
- 重新啟動裝置

在 **不受監督** 裝置上，使用「尋找我的 iPhone」應用程式時，會自動啟用「啟用鎖定」。

在 **受監督** 裝置上，您必須使用 Configuration Manager 相容性設定來啟用「啟用鎖定」。

> [!TIP]
> iOS 裝置的受監督模式可讓您使用 Apple Configurator 工具來鎖定裝置，將功能限制在特定商務用途。 受監督的模式通常僅適用於屬公司擁有的裝置。

雖然啟用鎖定可以協助保護 iOS 裝置，並提高裝置遺失和遭竊時的復原機會，但是這項功能可能會為身為 IT 系統管理員的您帶來一些挑戰。 例如：

- 其中一位使用者在裝置上設定啟用鎖定。 使用者之後離職並歸還裝置。 如果沒有使用者的 Apple ID 和密碼，就無法重新啟用裝置，即使您抹除它也是一樣。
- 您需要一份啟用鎖定已啟用之所有裝置的報表。
- 在重新整理組織中的裝置期間，您想要將某些裝置重新指派給不同的部門。 您只能重新指派啟用鎖定未啟用的裝置。


為了協助解決這些問題，Apple 在 iOS 7.1 中引進了啟用鎖定略過。 這可讓您從沒有使用者的 Apple ID 和密碼的受監督裝置移除啟用鎖定。 受監督的裝置會產生裝置特定啟用鎖定略過碼，並儲存在 Apple 啟用伺服器上。

您可以在 [這裡](https://support.apple.com/HT201365)深入閱讀「啟用鎖定」。

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Configuration Manager 如何協助您管理啟用鎖定

Configuration Manager 可以透過兩種方式協助您管理啟用鎖定：

1. 在受監督裝置上啟用「啟用鎖定」。
2. 在受監督裝置上略過「啟用鎖定」。

> [!IMPORTANT]
> 您不可以在不受監督裝置上略過「啟用鎖定」。

屬公司擁有裝置之這個項目的商業優勢如下：



- 使用者可以獲得「尋找我的 iPhone」應用程式的安全性優點
- 您可以讓使用者執行工作，並知道在需要重新規劃裝置時，您將裝置淘汰或解除鎖定


## <a name="enable-activation-lock-on-supervised-devices"></a>在受監督裝置上啟用「啟用鎖定」

您可以使用 Configuration Manager 相容性設定來建立和部署 **iOS 和 Mac OS X** 類型的設定項目，以在受監督裝置上啟用「啟用鎖定」：

1. 使用[如何為不是使用 System Center Configuration Manager 用戶端所管理的 iOS 和 Mac OS X 裝置建立設定項目](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)主題中的資訊，建立 **iOS 和 Mac OS X** 類型的設定項目。
2. 在 [建立設定項目精靈] 的 **[系統安全性]** 頁面上，將 **[允許啟用鎖定 (僅限受監督的模式)]** 設定設成 **[允許]**。
3. [將設定項目加入設定基準中](/sccm/compliance/deploy-use/create-configuration-baselines)。
4. [部署此設定基準](/sccm/compliance/deploy-use/deploy-configuration-baselines)到某個集合，而這個集合包含您要啟用「啟用鎖定」的 iOS 裝置。

> [!IMPORTANT]
> 請先確定您實際擁有裝置，再執行這個程序。 否則，將會略過啟用鎖定，而且實際擁有裝置的人都可以完整存取該裝置來關閉「尋找我的 iPhone」、清除裝置，或重新啟用裝置。

您只能略過「啟用鎖定」，或擷取受監督裝置上的「啟用鎖定」略過碼；嘗試略過不受監督裝置上的啟用鎖定或是檢視略過碼，會導致錯誤。



## <a name="view-the-activation-lock-bypass-code"></a>檢視啟用鎖定略過碼

1. 在 Configuration Manager 主控台中，按一下 [資產與相容性] 。
2. 在 [資產與相容性]  工作區中，按一下 [裝置] 。
3. 選取處於受監督模式並已啟用「啟用鎖定」的已註冊裝置。
4. 在 **[首頁]** 索引標籤的 **[裝置]** 群組中，按一下 **[遠端裝置動作]** > **[檢視啟用鎖定略過碼]**。
5. **[啟用鎖定略過碼]** 對話方塊會顯示所選取裝置的略過碼。

## <a name="bypass-activation-lock"></a>略過啟用鎖定

1. 在 Configuration Manager 主控台中，按一下 [資產與相容性] 。
2. 在 [資產與相容性]  工作區中，按一下 [裝置] 。
3. 選取處於受監督模式並已啟用「啟用鎖定」的已註冊裝置。
3. 在 **[首頁]** 索引標籤的 **[裝置]** 群組中，按一下 **[遠端裝置動作]** > **[略過啟用鎖定]**。
5. 閱讀警告對話方塊中的訊息，然後當您準備好繼續進行時按一下 **[是]** 。
6. 您可以從下列位置檢查解除鎖定要求的狀態：

    - 裝置內容對話方塊中裝置的探索資料。
    - **[裝置]** 檢視中的 **[啟用鎖定略過狀態]** 資料行 (預設會隱藏此資料行)。
    - 詳細資料窗格的 **[摘要]** 索引標籤中的 **[遠端裝置動作資訊]** 區段 (選取裝置時)。
