---
title: "連結使用者和裝置與使用者裝置親和性 | Microsoft Docs"
description: "使用使用者裝置親和性連結使用者和裝置，並自動將應用程式部署到與使用者相關聯的所有裝置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4e8e677851ad9ae7d027ab685e842a8ff5e35573
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>System Center Configuration Manager 的連結使用者和裝置與使用者裝置親和性

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager (Configuration Manager) 中的使用者裝置親和性可建立使用者與一或多部裝置的關聯。 這樣不需要知道使用者裝置的名稱，也可為使用者部署應用程式。 不需要將應用程式部署至該使用者的每部裝置，而是部署給該使用者。 接著，使用者裝置親和性會自動確定該應用程式是否已安裝在與該使用者相關聯的所有裝置上。  

 您可以定義主要裝置，它們通常是使用者每天用於執行工作的裝置。 在使用者和裝置之間建立親和性時，可以獲得更多應用程式部署選項。 例如，如果使用者需要 Microsoft Visio，您可以使用 Windows Installer 部署將其安裝在該使用者的主要裝置上。 不過，在非主要裝置上，您可以將 Visio 部署為虛擬應用程式。 您也可以在使用者未登入時，利用使用者裝置親和性在使用者的裝置上預先部署軟體，讓使用者在登入時，應用程式已安裝好且可執行。  

 您必須管理電腦的使用者裝置親和性資訊。 Configuration Manager 會自動管理使用者裝置與其所註冊之行動裝置的親和性。  

## <a name="manually-set-up-user-device-affinity"></a>手動設定使用者裝置親和性  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置]。  

3.  在清單中，選取裝置。 然後，在 [首頁] 索引標籤的 [裝置] 群組中，選擇 [編輯主要使用者]。  

4.  在 [編輯主要使用者] 對話方塊中，搜尋並選取要新增為所選裝置之主要使用者的使用者。 選擇 [新增]。  

    > [!NOTE]  
    > [主要使用者] 清單會顯示哪些使用者已經是此裝置的主要使用者，以及用於指派每個使用者-裝置關聯性的方法。  

## <a name="set-up-primary-devices-for-a-user"></a>設定使用者的主要裝置  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [使用者]。  

3.  在清單中，選取使用者。 然後，在 [裝置] 索引標籤上，選擇 [編輯主要裝置]。  

4.  在 [編輯主要裝置] 對話方塊中，搜尋並選取裝置以將其新增為所選使用者的主要裝置。 選擇 [新增]。  

    > [!NOTE]  
    > [主要裝置] 清單會顯示哪些裝置已設為此使用者的主要裝置，以及用於指派每個使用者-裝置關聯性的方法。  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>自動建立使用者裝置親和性 (僅限 Windows 電腦)  
 Configuration Manager 會從 Windows 事件記錄檔讀取使用者登入相關資料。 若要自動建立使用者裝置親和性，您必須在用戶端電腦的本機安全性原則中開啟這兩個選項，將登入事件儲存在 Windows 事件記錄檔中：  

-   **稽核帳戶登入事件**  
-   **稽核登入事件**  

 若要進行這些設定，請使用 Windows 群組原則。  

> [!IMPORTANT]  
> 如果錯誤導致 Windows 事件記錄檔產生大量項目，可能會建立新的事件記錄檔。 若發生此情況，Configuration Manager 就無法使用現有的登入事件。  
>   
> 開啟 Windows XP 中的 [稽核帳戶登入事件] 及 [稽核登入事件] 設定時請小心。 根據預設，保留原則是 7 天，而這些事件很有可能會填滿安全性事件記錄檔。 如果事件記錄檔已滿，標準使用者將無法登入。 為預防此問題，請將安全性事件記錄檔的原則 [保持方法] 值設定為 [視需要覆寫事件]。 若要讓使用者裝置親和性有足夠資料，也請將原則安全性事件記錄檔大小上限設定為合理的值，例如 5-20 MB。  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>設定站台自動建立使用者裝置親和性  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定]。  

2.  若要修改預設用戶端設定，請選取 [預設用戶端設定]，然後在 [首頁] 索引標籤的 [內容] 群組中選擇 [內容]。 若要建立自訂用戶端代理程式設定，請選取 [用戶端設定] 節點，然後在 [首頁] 索引標籤的 [建立] 群組中選擇 [建立自訂用戶端裝置設定]。  

    > [!NOTE]  
    > 如果修改預設用戶端設定，會將這些設定部署至階層中的所有電腦。 如需設定用戶端設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

3.  在 [使用者和裝置親和性] 中，設定下列項目：  

    -   **使用者裝置親和性閾值 (分鐘)**。 設定建立使用者裝置親和性之前的裝置使用分鐘數。  

    -   **使用者裝置親和性閾值 (天)**。 設定衡量使用親和性閾值的天數。  

    -   **從使用資料自動設定使用者裝置親和性**。 若要讓站台自動建立使用者裝置親和性，請從下拉式清單中選取 [True]。 如果您選取 [False]，則必須核准所有使用者裝置親和性指派。  

    > [!TIP]  
    > **範例：**如果您將 [使用者裝置親和性閾值 (分鐘)] 設定為 **60** 分鐘，並將 [使用者裝置親和性閾值 (天)] 設定為 **5** 天，則使用者在 5 天內至少必須使用該裝置 60 分鐘，才會自動建立使用者裝置親和性。  

自動建立使用者裝置親和性之後，Configuration Manager 會繼續監視使用者裝置親和性閾值。 如果使用者的裝置活動低於您設定的閾值，就會移除使用者裝置親和性。 將 [使用者裝置親和性閾值 (天)] 的值設定為 **7** 天以上，可避免因使用者未登入 (例如在週末期間) 而失去自動設定的使用者裝置親和性。  

## <a name="import-user-device-affinities-from-a-file"></a>從檔案匯入使用者裝置親和性  
 若要同時建立許多關聯性，您可以匯入包含多個使用者裝置親和性詳細資料的檔案。 在此程序中，必須先探索到主體裝置，且主體裝置必須是 Configuration Manager 資料庫中的資源，否則程序將失敗。  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [使用者] 或 [裝置]。  

2.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [匯入使用者裝置親和性]。  

3.  在 [匯入使用者裝置親和性精靈] 的 [選擇對應] 頁面上，設定這項資訊：  

    -   **檔案名稱**。 指定逗號分隔值 (CSV) 檔案，其中會列出要相互建立親和性的使用者及裝置。 在此檔案中，每一對使用者和裝置都必須各有其專屬資料列，並以逗號分隔值。 使用下列格式：<網域>&#92;<使用者名稱>,<裝置 NetBIOS 名稱>。  

    -   **此檔案具有可供參照的欄位標題**。 如果 .csv 檔案具有頂端資料列標頭，請選取這個選項，並在匯入期間忽略標頭資料列。  

4.  如果要匯入的檔案中每個資料列都有兩個以上的項目，您可以使用 [資料行] 和 [指派] 來指定代表使用者和裝置的資料行，以及匯入時要忽略的資料行。  

5.  選擇 [下一步]，然後完成 [匯入使用者裝置親和性精靈]。  

## <a name="let-users-create-their-own-device-affinities"></a>讓使用者建立其專屬裝置親和性  
 使用下列程序，您可以設定使用者在軟體中心應用程式中建立其專屬使用者裝置親和性。  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>設定站台允許使用者建立的使用者裝置親和性要求  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定]。  

2.  若要修改預設用戶端設定，請選取 [預設用戶端設定]，然後在 [首頁] 索引標籤的 [內容] 群組中選擇 [內容]。 若要建立自訂用戶端代理程式設定，請選取 [用戶端設定] 節點，然後在 [首頁] 索引標籤的 [建立] 群組中選擇 [建立自訂用戶端使用者設定]。  

    > [!NOTE]  
    > 如果修改預設用戶端設定，會將這些設定部署至階層中的所有電腦。 如需設定用戶端設定的詳細資訊，請參閱[設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

3.  選取用戶端設定 [使用者和裝置親和性]  ，然後在 [允許使用者定義其主要裝置]  下拉式清單中，選取 [True] 。  

### <a name="set-up-a-user-device-affinity"></a>設定使用者裝置親和性  

1.  在 [應用程式類別目錄] 中，選擇 [我的系統]。  

2.  選取 [我經常使用這部電腦工作] 選項。  

## <a name="manage-user-device-affinity-requests-from-users"></a>管理使用者的使用者裝置親和性要求  
 用戶端設定 [從使用資料自動設定使用者裝置親和性]  設為 [False] 時，必須由您核准所有使用者裝置親和性指派。  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>核准或拒絕使用者裝置親和性要求  

1.  在 Configuration Manager 主控台中，選擇 [資產與相容性]。  

2.  在 [資產與相容性]  工作區中，選取您要管理哪一個使用者或裝置集合的親和性要求。  

3.  在 [首頁] 索引標籤的 [集合] 群組中，選擇 [管理親和性要求]。  

4.  在 [管理使用者裝置親和性要求] 對話方塊中，選取親和性要求，然後選擇 [核准] 或 [拒絕]。  
