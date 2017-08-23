---
title: "設定用戶端狀態 | Microsoft Docs"
description: "選取 System Center Configuration Manager 中的用戶端狀態設定。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 060d63ab8bce9c3bb39d2db404580b9f59416d33
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中設定用戶端狀態

*適用對象：System Center Configuration Manager (最新分支)*

您必須設定站台指定用於將用戶端標記為非作用中的參數，以及設定一旦用戶端活動低於指定閾值時的警示選項，才能監視 System Center Configuration Manager 用戶端狀態，以及補救所找到的問題。 您也可以停止讓電腦自動補救用戶端狀態找到的所有問題。  

##  <a name="BKMK_1"></a> 設定用戶端狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中按一下 [用戶端狀態] ，然後在 [首頁]  索引標籤的 [用戶端狀態]  群組中按一下 [用戶端狀態設定] 。  

3.  在 [用戶端狀態設定內容]  對話方塊中，指定下列用於判斷用戶端活動的值：  

    > [!NOTE]  
    >  如果不符合其中任何設定，用戶端將標示為非作用中。  

    -   **以下指定天數內的用戶端原則要求：** 指定用戶端提出原則要求之後的天數。 預設值是 **7** 天。  

    -   **以下指定天數內的活動訊號探索：** 指定用戶端電腦傳送活動訊號探索記錄至站台資料庫後的天數。 預設值是 **7** 天。  

    -   **以下指定天數內的硬體清查：** 指定用戶端電腦傳送硬體清查記錄至站台資料庫後的天數。 預設值是 **7** 天。  

    -   **以下指定天數內的軟體清查：** 指定用戶端電腦傳送軟體清查記錄至站台資料庫後的天數。 預設值是 **7** 天。  

    -   **以下指定天數內的狀態訊息：** 指定用戶端電腦傳送狀態訊息至站台資料庫後的天數。 預設值是 **7** 天。  

4.  在 [用戶端狀態設定內容]  對話方塊中，指定下列用於判斷保留用戶端狀態歷程記錄資料的天數：  

    -   **保留以下指定天數內的用戶端狀態歷程：** 指定您要將用戶端狀態歷程記錄保留在站台資料庫中的天數。 預設值是 **31** 天。  

5.  按一下 [確定]  儲存內容，並且關閉 [用戶端狀態設定內容]  對話方塊。  

##  <a name="BKMK_Schedule"></a> 設定用戶端狀態排程  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視]  工作區中按一下 [用戶端狀態] ，然後在 [首頁]  索引標籤的 [用戶端狀態]  群組中按一下 [排程用戶端狀態更新] 。  

3.  在 [排程用戶端狀態更新]  對話方塊中，設定用戶端狀態進行更新的間隔，然後按一下 [確定]。  

    > [!NOTE]  
    >  變更用戶端狀態更新的排程時，更新會在下次排程的用戶端狀態更新 (之前設定的排程) 時生效。  

##  <a name="BKMK_2"></a> 設定用戶端狀態警示  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置集合] 。  

3.  在 [裝置集合]  清單中，選取您要用於設定警示的集合，然後在 [首頁]  索引標籤的 [內容]  群組中按一下 [內容] 。  

    > [!NOTE]  
    >  您無法設定使用者集合的警示。  

4.  在 [&lt;集合名稱\> 內容] 對話方塊的 [警示] 索引標籤上，按一下 [新增]。  

    > [!NOTE]  
    >  您所指派到的安全性角色具有警示權限時，才會顯示 [警示]  索引標籤。  

5.  在 [新增集合警示]  對話方塊中，選擇您要在用戶端狀態閾值低於特定值時產生的警示，然後按一下 [確定] 。  

6.  在 [警示]  索引標籤的 [條件]  清單中選取每個用戶端狀態警示，然後指定下列資訊。  

    -   **警示名稱** - 接受預設名稱或輸入新的警示名稱。  

    -   **警示嚴重性** - 從下拉式清單中，選擇將顯示在 Configuration Manager 主控台中的警示等級。  

    -   **產生警示** - 指定警示的閾值百分比。  

7.  按一下 [確定] 關閉 [&lt;集合名稱\> 內容] 對話方塊。  

##  <a name="BKMK_3"></a> 排除電腦的自動補救功能  

1.  在要停用自動補救功能的用戶端電腦上開啟登錄編輯程式。  

    > [!WARNING]  
    >  如果使用登錄編輯程式的方式不正確，可能會導致嚴重問題而必須重新安裝作業系統。 Microsoft 無法保證您可以解決因不正確使用登錄編輯程式所造成的問題。 您必須自行承擔使用登錄編輯器的風險。  

2.  瀏覽至 **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**。  

3.  針對此登錄編輯程式輸入下列任一值：  

    -   **True** - 用戶端電腦不會自動補救找到的任何問題。 不過，一旦此用戶端出現任何問題，您仍然會在 [監視]  工作區中收到警示。  

    -   **False** - 用戶端電腦會自動補救找到的問題，您會在 [監視] 工作區中收到警示。 這是預設設定。  

4.  關閉登錄編輯程式。  

 您也可以使用 CCMSetup **NotifyOnly** 安裝內容安裝用戶端，停止用戶端執行自動補救。 如需用戶端安裝內容的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。  
