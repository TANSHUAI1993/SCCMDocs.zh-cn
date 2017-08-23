---
title: "測試資料庫更新 | Microsoft Docs"
description: "於安裝 Configuration Manager 更新時，測試升級網站資料庫。"
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6b76c97cd205bb02683a7bfa1eb378471a75551d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>於安裝更新時測試資料庫升級

適用於：System Center Configuration Manager (最新分支)

本主題中的資訊可以協助您在針對 Configuration Manager 的目前分支安裝主控台內更新之前，執行測試資料庫升級。 不過，測試升級已不再是必要或建議的步驟，除非 Configuration Manager 未明確支援的自訂影響或修改了您的資料庫。

## <a name="do-i-need-to-run-a-test-upgrade"></a>我是否需要執行測試升級？
由於 System Center Configuration Manager 所導入的變更，使得我們得以取代此升級測試。 這些變更簡化了將生產環境更新至較新版本的程序和速度。 此重新設計的目的是為協助客戶以較低風險的方式維持在最新的狀態，並在安裝每個新更新時降低作業的額外負荷。

這些變更是針對安裝更新的方式，其中包括能自動回復失敗的更新，而不需要執行站台復原的邏輯。 這些變更可讓使用者透過主控台來管理更新安裝，且包含[重試失敗更新的安裝](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry)的選項。

> [!TIP]
> 從較舊的產品 (例如 System Center 2012 Configuration Manager) 升級到 System Center Configuration Manager 時，[測試資料庫升級會保留為建議的步驟](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade)。

如果您仍然計畫在安裝主控台內更新時測試站台資料庫的升級，下列資訊將能補充[安裝主控台內更新的相關指導](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)。

## <a name="prepare-to-run-a-test-database-upgrade"></a>準備執行測試資料庫升級  
在階層中安裝新的更新之前 (例如更新 1702)，您可以測試站台資料庫的升級。

若要執行升級測試，請使用來自目標更新版本之 Configuration Manager 的站台上 [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) 資料夾中之來源檔案的 Configuration Manager 安裝程式。 此需求表示，若要測試更新到 1702 的資料庫更新：
-   您必須至少有一個執行 1702 版的站台，以從中取得 CD.Latest 資料夾。
-   如果您沒有執行所需版本的站台，請考慮在實驗室環境中安裝站台，然後將該站台更新到新的版本。 這會建立具有正確版本來源檔案的 CD.Latest 資料夾。

升級測試會針對您還原至個別 SQL Server 執行個體之站台資料庫的備份執行。  您會以 **testdbupgrade** 命令列參數執行來自 **CD.Latest** 資料夾的安裝程式，以針對資料庫的已還原複本進行測試升級。 測試升級完成後，系統便會捨棄升級的資料庫。 它不可由 Configuration Manager 站台使用。

如果更新安裝失敗，您應該不會需要復原站台。 您可以改為從主控台內重試更新安裝。

##  <a name="run-the-test-upgrade"></a>執行測試升級    
1.  使用來自執行目標更新版本之站台上 **CD.Latest** 資料夾中的 Configuration Manager 安裝程式及來源檔案。  

2.  將 **CD.Latest** 資料夾複製到 SQL Server 執行個體上您將用來執行測試資料庫升級的位置。

3.  建立您想要進行測試升級之站台資料庫的備份。 接下來，將資料庫的複本還原至未裝載 Configuration Manager 站台的 SQL Server 執行個體。 SQL Server 執行個體必須使用與您站台資料庫相同的 SQL Server 版本。  

4.  還原資料庫複本後，從包含目標更新版本之來源檔案的 CD.Latest 資料夾中，執行安裝程式。 當您執行安裝程式時，請使用 **/TESTDBUPGRADE** 命令列選項。 如果裝載資料庫複本的 SQL Server 執行個體不是預設的執行個體，請提供命令列引數，以識別裝載站台資料庫複本的執行個體。   

  例如，您有一個資料庫名稱為 *SMS_ABC* 的站台資料庫。 您會將此站台資料庫的複本，還原到執行個體名稱為 *DBTest* 的受支援 SQL Server 執行個體。 若要測試此站台資料庫複本的升級，請使用下列命令列：**Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**。  

  您可在 System Center Configuration Manager 來源媒體的下列位置找到 Setup.exe：**SMSSETUP\BIN\X64**。  

5.  在您執行升級測試的 SQL Server 執行個體上，監視位於系統磁碟機根目錄中的 *ConfigMgrSetup.log* 以了解進度及成功與否。  

     如果測試升級失敗，請修正與站台資料庫升級失敗相關的任何問題。 然後，建立新的站台資料庫備份，並測試新資料庫複本的升級。  



## <a name="next-steps"></a>後續步驟
順利完成測試資料庫更新後，請捨棄更新的資料庫。 它不可由 Configuration Manager 站台使用。 您接著可以返回作用中的站台，並[開始更新安裝](/sccm/core/servers/manage/install-in-console-updates)。
