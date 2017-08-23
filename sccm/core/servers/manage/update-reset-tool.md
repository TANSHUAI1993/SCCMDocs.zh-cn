---
title: "更新重設工具 | Microsoft Docs"
description: "針對 System Center Configuration Manager 的主控台內更新使用更新重設工具。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1960f86e98a957559f379b9eeb6d293f7e4182e5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="update-reset-tool"></a>更新重設工具

適用於：System Center Configuration Manager (最新分支)  


從 1706 版開始，Configuration Manager 主要站台和管理中心網站包含 Configuration Manager 更新重設工具 **CMUpdateReset.exe**。 當主控台內更新無法下載或複寫時，請使用此工具來修正問題。 此工具位於站台伺服器的 ***\cd.latest\SMSSETUP\TOOLS*** 資料夾中。

您可以使用此工具，搭配所有仍受支援的最新分支版本。

您可以在[主控台內更新](/sccm/core/servers/manage/install-in-console-updates)尚未安裝且處於失敗狀態時使用此工具。 失敗狀態表示更新下載正在進行中，但已停滯或花費過長的時間。 如果花費的時間已超過以往針對類似大小之更新套件的預期時間長達數小時，即視為過長的時間。 它也可能是指將更新複寫到子主要站台失敗。  

當您執行此工具時，它會針對您指定的更新執行。 此工具預設不會刪除已成功安裝或下載的更新。  

### <a name="prerequisites"></a>先決條件
您用來執行此工具的帳戶需要有下列權限：
-   對管理中心網站之站台資料庫及您階層中每個主要站台的「讀取」和「寫入」權限。 若要設定這些權限，您可以新增使用者帳戶作為每個站台之 Configuration Manager 資料庫上 **db_datawriter** 和 **db_datareader** [固定資料庫角色](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles)的成員。 此工具不會與次要站台進行互動。
-   您階層之最上層站台上的「本機系統管理員」。
-   裝載服務連接點之電腦上的「本機系統管理員」。

您需要有所要重設之更新套件的 GUID。 取得 GUID：
  1.   在主控台中，移至 [系統管理] > [更新與服務]。
  2.   在顯示窗格中，以滑鼠右鍵按一下其中一個資料行 (例如 [狀態]) 的標題，然後選取 [套件 GUID] 以將該資料行加入顯示。
  3.   資料行現在會顯示更新套件 GUID。

> [!TIP]  
> 若要複製 GUID，請選取您想要重設之更新套件的資料列，然後使用 CTRL+C 來複製該資料列。 如果您將所複製的選取項目貼到文字編輯器中，則可以接著僅複製 GUID，以在執行工具時作為命令列參數使用。

### <a name="run-the-tool"></a>執行工具    
此工具必須在階層的最上層站台上執行。

當您執行工具時，請使用命令列參數來指定：
  -   位於階層頂層站台的 SQL Server。
  -   頂層站台的站台資料庫名稱。
  -   您要重設之更新套件的 GUID。

根據更新的狀態，工具會識別所需存取的其他伺服器。   

如果更新套件處於 [下載後] 狀態，此工具就不會清除套件。 您可以選擇使用強制刪除參數 (請參閱本主題稍後的＜命令列參數＞)，來強制移除已成功下載的更新。

在執行此工具之後：
-   如果已刪除套件，請重新啟動頂層站台的 SMS_Executive 服務。 接著請檢查更新以重新下載套件。
-   如果套件並未刪除，您無須採取任何動作。 更新會重新初始化，然後重新啟動複寫或安裝。

**命令列參數：**  

| 參數        |說明                 |  
|------------------|----------------------------|  
|**-S &lt;您最上層站台之 SQL Server 的 FQDN>** | *必要* <br> 指定裝載階層頂層站台之站台資料庫的 SQL Server FQDN。    |  
| **-D &lt;資料庫名稱>**                        | *必要* <br> 指定頂層站台之資料庫的名稱。  |  
| **-P &lt;套件 GUID>**                         | *必要* <br> 指定要重設之更新套件的 GUID。   |  
| **-I &lt;SQL Server 執行個體名稱>**             | *選擇性* <br> 識別裝載站台資料庫之 SQL Server 的執行個體。 |
| **-FDELETE**                              | *選擇性* <br> 強制刪除已成功下載的更新套件。 |  
 **範例：**  
 在典型的案例中，您想要重設有下載問題的更新。 您的 SQL Server FQDN 為*server1.fabrikam.com*，站台資料庫位於*CM_XYZ*，而套件 GUID 是*61F16B3C-F1F6-4F9F-8647-2A524B0C802C*。  您需執行：***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 在較極端的案例中，您想要強制刪除有問題的更新套件。 您的 SQL Server FQDN 為*server1.fabrikam.com*，站台資料庫位於*CM_XYZ*，而套件 GUID 是*61F16B3C-F1F6-4F9F-8647-2A524B0C802C*。  您需執行：***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
