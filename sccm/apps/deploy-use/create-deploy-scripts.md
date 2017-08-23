---
title: "使用 Configuration Manager 建立並執行指令碼 | Microsoft Docs"
description: "使用 Configuration Manager 在用戶端裝置上建立並執行指令碼。"
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: ed84f7900eee5c04728d0e4d1b46027c36327bec
ms.sourcegitcommit: b41d3e5c7f0c87f9af29e02de3e6cc9301eeafc4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台建立及執行 PowerShell 指令碼

適用於：System Center Configuration Manager (最新分支)

在 Configuration Manager 中，除了使用套件和程式部署指令碼以外，您還可使用下列功能採取下列動作：

- 將 PowerShell 指令碼匯入到 Configuration Manager
- 從 Configuration Manager 主控台編輯指令碼 (僅適用於未簽署的指令碼)
- 將指令碼標示為 [已核准] 或 [已拒絕] 以提升安全性
- 在 Windows 用戶端電腦及內部部署受管理 Windows 電腦的集合上執行指令碼。 您不須部署指令碼，它們會以近乎即時的方式在用戶端裝置上執行。
- 在 Configuration Manager 主控台中檢查指令碼所傳回的結果。

>[!TIP]
>在這個版本的 Configuration Manager 中，指令碼是發行前版本功能。 若要啟用指令碼，請參閱 [System Center Configuration Manager 的發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="prerequisites"></a>先決條件

若要執行 PowerShell 指令碼，用戶端必須執行 PowerShell 3.0 版或更新版本。 不過，如果您執行的指令碼包含較新版 PowerShell 中的功能，執行指令碼所在的用戶端上必須執行該版本。

Configuration Manager 用戶端必須執行至少 1706 版或更新版的用戶端，才能執行指令碼。

若要使用指令碼，您必須是適當 Configuration Manager 安全性角色的成員。

- 若要匯入及撰寫指令碼 - 您的帳戶必須具備**合規性設定管理員**安全性角色中 **SMS 指令碼**的**建立**權限。
- 若要核准或拒絕指令碼 - 您的帳戶必須具備**合規性設定管理員**安全性角色中 **SMS 指令碼**的**核准**權限。
- 若要執行指令碼 - 您的帳戶必須具備**合規性設定管理員**安全性角色中**集合**的**執行指令碼**權限。

如需有關 Configuration Manager 安全性角色的詳細資訊，請參閱[以角色為基礎之系統管理的基礎](/sccm/core/understand/fundamentals-of-role-based-administration)。

使用者預設無法核准自己所撰寫的指令碼。 由於指令碼相當強大、用途廣泛且可部署至許多裝置，您可以將指令碼撰寫者與指令碼核准者之角色分開。 這些角色可針對執行指令碼而未受監督的情況提供一層額外的安全性。 為簡化測試，您可以不實施次要核准。

## <a name="allow-users-to-approve-their-own-scripts"></a>允許使用者核准自己的指令碼

1. 在 Configuration Manager 主控台中，按一下 [系統管理] 。
2. 在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。
3. 在站台清單中，選擇您的站台，然後在 [首頁] 索引標籤上的 [站台] 群組中，按一下 [階層設定]。
4. 在 [階層設定內容] 對話方塊的 [一般] 索引標籤上，取消選取 [不允許指令碼作者核准自己的指令碼]。

## <a name="import-and-edit-a-script"></a>匯入及編輯指令碼

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。
2. 在 [軟體程式庫] 工作區中，按一下 [指令碼]。
3. 在 [首頁] 索引標籤上的 [建立] 群組中，按一下 [建立指令碼]。
4. 在 [建立指令碼] 精靈的 [指令碼] 頁面上，設定下列設定：
    - **指令碼名稱** - 輸入指令碼的名稱。 雖然可以使用相同名稱來建立多個指令碼，但使用重複名稱會讓您更難在 Configuration Manager 主控台中找出所需的指令碼。
    - **指令碼語言** - 目前僅支援 PowerShell 指令碼。
    - **匯入** - 將 PowerShell 指令碼匯入到主控台。 指令碼會顯示在 [指令碼] 欄位中。
    - **清除** - 將目前的指令碼從 [指令碼] 欄位中移除。
    - **指令碼** - 顯示目前已匯入的指令碼。 您可以視需要編輯此欄位中的指令碼。
5. 完成精靈。 新指令碼會顯示在 [指令碼] 清單中，其狀態為 [等候核准]。 您必須先核准此指令碼，才能在用戶端裝置上執行它。

### <a name="script-examples"></a>指令碼範例

以下是您可能想搭配這項功能使用的一些指令碼範例。

#### <a name="create-a-folder"></a>建立資料夾

*New-Item "c:\scripts" -type folder name* 
 
 
#### <a name="create-a-file"></a>建立檔案

*New-Item c:\scripts\new_file.txt -type file name*


## <a name="approve-or-deny-a-script"></a>核准或拒絕指令碼

您必須先核准指令碼，才能執行它。 核准指令碼：

1. 在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。
2. 在 [軟體程式庫] 工作區中，按一下 [指令碼]。
3. 在 [指令碼] 清單中，選擇您想要核准或拒絕的指令碼，然後在 [首頁] 索引標籤上的 [指令碼] 群組中，按一下 [核准/拒絕]。
4. 在 [核准或拒絕指令碼] 對話方塊中，**核准**或**拒絕**指令碼，並視需要輸入與您決策相關的註解。 如果您拒絕某個指令碼，它就無法在用戶端裝置上執行。
5. 完成精靈。 在 [指令碼] 清單中，[核准狀態] 資料行會隨著您採取的動作而發生變更。

## <a name="run-a-script"></a>執行指令碼
指令碼經核准後，就能在您選擇的集合上執行。

1. 在 Configuration Manager 主控台中，按一下 [資產與合規性]。
2. 在 [資產與相容性] 工作區中，按一下 [裝置集合]。
3. 在 [裝置集合] 清單中，按一下要用來作為指令碼執行位置的裝置集合。
4. 在 [首頁] 索引標籤的 [所有系統] 群組中，按一下 [執行指令碼]。
5. 在 [執行指令碼] 精靈的 [指令碼] 頁面上，從清單中選擇一個指令碼。 此清單只會顯示已核准的指令碼。
6. 按一下 [下一步] 完成精靈。

>[!IMPORTANT]
>指令碼會有一小時的執行時間。 如果指令碼未在這段期間執行 (如電腦已關閉)，您必須再次執行。

## <a name="next-steps"></a>後續步驟

對用戶端裝置執行指令碼之後，請使用此程序來監視作業是否成功。

1. 在 Configuration Manager 主控台中，按一下 [監視] 。
2. 在 [監視] 工作區中，按一下 [指令碼狀態]。
3. 在 [指令碼狀態] 清單中，您可以檢視在用戶端裝置上執行之每個指令碼的結果。 指令碼結束代碼 **0** 通常表示指令碼已成功執行。
