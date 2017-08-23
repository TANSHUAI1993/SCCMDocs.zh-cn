---
title: "監視 Endpoint Protection 狀態 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 階層中監視 Endpoint Protection。"
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b5771f4faebc06076bdbf84727848c881fc1dfb4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-endpoint-protection-status"></a>如何監視 Endpoint Protection 狀態

*適用於：System Center Configuration Manager (最新分支)*

您可以在 Microsoft System Center Configuration Manager 階層中監視 Endpoint Protection，方法是使用 [監視] 工作區中 [安全性] 下的 [Endpoint Protection 狀態] 節點、[資產與合規性] 工作區中的 [Endpoint Protection] 節點，以及使用報告。  

##  <a name="BKMK_1"></a> 如何使用 Endpoint Protection 狀態節點監視 Endpoint Protection  

1.  在 Configuration Manager 主控台中，按一下 [監視] 。  

2.  在 [監視] 工作區中，展開 [安全性] 然後按一下 [Endpoint Protection 狀態]。  

3.  在 **集合** 清單中選取您要檢視狀態資訊的集合。  

    > [!IMPORTANT]  
    >  集合是可讓您選取在下列情況：  
    >   
    >  -   當您在 [*<集合名稱\>* 內容] 對話方塊的 [警示] 索引標籤上選取 [在 Endpoint Protection 儀表板中檢視此集合] 時。  
    > -   當您將 Endpoint Protection 反惡意程式碼原則部署至集合時。  
    > -   當您啟用 Endpoint Protection 用戶端設定並將其部署至集合時。  

4.  檢視中顯示的資訊 **安全性狀態** 和 **操作狀態** 區段。 您可以按一下來建立暫時的集合中的任何狀態連結 **裝置** 中的節點 **資產與相容性** 工作區。 暫時的集合包含具有選定狀態的電腦。  

    > [!IMPORTANT]  
    >  [Endpoint Protection 狀態] 節點中顯示的資訊取決於從 Configuration Manager 資料庫摘要的最後一筆資料，因此可能不是最新資訊。 如果您想要擷取最新的資料，請在 **[首頁]** 索引標籤上按一下 **[執行摘要]**，或按一下 **[排程摘要]** ，以調整摘要間隔。  

##  <a name="BKMK_2"></a> 如何在資產與相容性工作區中監視 Endpoint Protection  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 **資產與相容性** 工作區中，執行下列動作:  

    -   按一下 **裝置**。 在 **裝置** 清單，選取 電腦，然後按一下 **惡意程式碼的詳細資料**  索引標籤。  

    -   按一下 **裝置集合**。 在 **[裝置集合]** 清單中，選取包含您想要監視之電腦的集合，然後在 **[首頁]** 索引標籤的 **[集合]** 群組中，按一下 **[顯示成員]**。  

3.  在 [*<集合名稱\>*] 清單中選取電腦，然後按一下 [惡意程式碼詳細資料] 索引標籤。  

##  <a name="BKMK_3"></a> 如何使用報告監視 Endpoint Protection  
 使用下列報告，協助您檢視有關的資訊 Endpoint Protection 階層中。 您也可以使用這些報告來協助疑難排解任何 Endpoint Protection 問題。 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)和 [System Center Configuration Manager 中的記錄檔](../../core/plan-design/hierarchy/log-files.md)。 Endpoint Protection 報告位於 Endpoint Protection 資料夾中。  

|報表名稱|說明|  
|-----------------|-----------------|  
|**反惡意程式碼活動報表**|顯示指定之集合的反惡意程式碼活動的概觀。|  
|**受感染的電腦**|顯示的電腦偵測到指定的威脅清單。|  
|**最上層使用者的威脅**|顯示具有最多的偵測到威脅的使用者清單。|  
|**使用者的威脅清單**|顯示找不到指定的使用者帳戶的威脅的清單。|  

## <a name="malware-alert-levels"></a>惡意程式碼警示等級  
 使用下表來識別不同 Endpoint Protection 警示層級可能會顯示在報告中，或是在 Configuration Manager 主控台。  

|警示等級|說明|  
|-----------------|-----------------|  
|**失敗**|Endpoint Protection 無法補救惡意程式碼。 檢查您日誌中的錯誤詳細資料。<br /><br /> **注意：**如需 Configuration Manager 和 Endpoint Protection 記錄檔的清單，請參閱 [System Center Configuration Manager 中的記錄檔](../../core/plan-design/hierarchy/log-files.md)主題中的＜Endpoint Protection＞一節。|  
|**移除**|Endpoint Protection 已順利移除惡意程式碼。|  
|**已隔離**|Endpoint Protection 已將惡意程式碼移至安全的位置，使其無法執行，直到您將它移除，或允許它執行。|  
|**已清除**|惡意程式碼已清除受感染的檔案中。|  
|**允許**|選取要包含惡意程式碼執行的軟體可讓系統管理使用者。|  
|**沒有動作**|Endpoint Protection 對惡意程式碼不採取任何動作。 這可能發生在偵測到惡意程式碼並不會再偵測到惡意程式碼; 之後重新啟動電腦比方說，如果對應的網路磁碟機上偵測到的惡意程式碼是不重新連線時重新啟動電腦。|  
|**封鎖**|Endpoint Protection 封鎖惡意程式碼，使其無法執行。 這可能會發生在處理序已在電腦上的找到包含惡意程式碼。|
