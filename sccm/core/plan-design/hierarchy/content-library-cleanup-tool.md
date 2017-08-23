---
title: "內容庫清理工具 | Microsoft Docs"
description: "使用內容庫清理工具，將不再和 System Center Configuration Manager 部署相關聯的孤立內容移除。"
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>System Center Configuration Manager 的內容庫清理工具

*適用對象：System Center Configuration Manager (最新分支)*

 從 1702 版開始，您可以使用命令列工具 (**ContentLibraryCleanup.exe**) 從發佈點移除不再與任何套件或應用程式相關聯的內容 (孤立的內容)。 此工具稱為內容庫清理工具，並會取代針對過去 Configuration Manager 產品所發行的類似舊版工具。  

此工具只會影響您在執行此工具時所指定發佈點上的內容。 此工具無法移除站台伺服器上的內容庫內容。

您在管理中心站台或主要站台可以在站台伺服器上的 *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* 資料夾中找到 **ContentLibraryCleanup.exe**。

## <a name="requirements"></a>需求  
 一次只能針對單一發佈點執行此工具。  
 - 其可以在裝載您想清除的發佈點所在的電腦上直接執行，或從另一部伺服器遠端執行此工具。
 - 執行此工具的使用者帳戶必須要有直接以角色為基礎的系統管理權限，其相當於 Configuration Manager 階層上的系統高權限管理員。 如果收到這些權限的帳戶身為具有系統高權限管理員權限的 Windows 安全性群組成員，此工具將無法運作。

## <a name="modes-of-operation"></a>作業模式
您可以在下列兩種模式中執行此工具。 建議您在「假設狀況」模式中執行工具，以便您先檢閱結果，再於「刪除模式」中執行此工具：
  1.    **假設狀況模式**：   
      如果您未指定 **/delete** 參數，此工具會在假設狀況模式中執行，並識別要從發佈點刪除的內容。
   - 在此模式中執行時，此工具不會刪除任何資料。
   - 和要刪除的內容相關的資訊會寫入至工具記錄檔，而且系統不會提示您確認每個可能的刪除動作。  
      </br>   

  2. **刪除模式**：   
    當您搭配 **/delete** 參數執行此工具時，此工具會在刪除模式中執行。

     - 當在此模式中執行時，您可以從發佈點的內容庫刪除指定發佈點上所發現的孤立內容。
     -  在刪除每個檔案之前，您都必須確認應刪除檔案。  您可以選取 **Y** 表示是、選取 **N** 表示否，或選取 [全部皆是] 略過接下來的提示並刪除所有孤立的內容。  
     </br>

當此工具在任一種模式中執行時，它會自動建立記錄，其名稱包含此工具的執行模式、發佈點名稱以及操作的日期和時間。 當工具完成時，會自動開啟記錄檔。

預設會在此工具執行所在的電腦上，將記錄檔寫入到執行此工具之使用者帳戶的暫存資料夾。 您可以使用 **/log** 參數，將記錄檔重新導向至另一個位置，包括網路共用。


## <a name="run-the-tool"></a>執行工具
執行工具：
1. 請在包含 **ContentLibraryCleanup.exe** 的資料夾開啟系統管理命令提示字元。  
2. 接著輸入命令列，其中包含必要的命令列參數及您要使用的選擇性參數。

**已知問題** 執行此工具時，如果有任何套件或部署失敗或正在進行中，可能會傳回類似下列錯誤︰
-  *System.InvalidOperationException：因為套件 <packageID> 未完全安裝，所以目前無法清除此內容庫。*

**因應措施：** 無。 正在進行部署或無法部署內容時，此工具無法可靠識別孤立的檔案。 因此，在解決該問題之前，此工具不允許您清除內容。

### <a name="command-line-switches"></a>命令列參數  
您可以依任何順序使用下列命令列參數。   

|參數|詳細資料|
|---------|-------|
|**/delete**  |**選擇性** </br> 當您要從發佈點刪除內容時，請使用此參數。 刪除內容之前，您會收到提示。 </br></br> 未使用此參數時，工具會記錄要刪除之內容的相關結果，但不會從發佈點刪除內容。 </br></br> 範例︰***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**選擇性** </br> 此參數以會隱藏所有提示 (例如要刪除內容的提示) 的無訊息模式來執行此工具，而且不會自動開啟記錄檔。 </br></br> 範例︰***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;發佈點 FQDN>**  | **必要** </br> 指定您要清除之發佈點的完整網域名稱 (FQDN)。 </br></br> 範例︰***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;主要站台 FQDN>**       | 從主要站台的發佈點清除內容時為**選擇性**。</br>從次要站台的發佈點清除內容時為**必要**。 </br></br>連線到父主要站台，以對 SMS_Provider 執行的工具。 這些查詢可讓工具判斷發佈點上應該要有什麼內容，以便識別孤立且可移除的內容。 因為無法直接從次要站台取得必要的詳細資料，所以必須為位於次要站台的發佈點建立父主要站台的連線。</br></br> 指定發佈點所屬之主要站台的 FQDN，或發佈點在次要站台時之父主要站台的 FQDN。 </br></br> 範例︰***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;主要站台碼>**  | 從主要站台的發佈點清除內容時為**選擇性**。</br>從次要站台的發佈點清除內容時為**必要**。 </br></br> 指定發佈點所屬之主要站台的站台碼，或發佈點在次要站台時之父主要站台的站台碼。</br></br> 範例︰***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**選擇性** </br> 指定工具要寫入記錄檔的位置。 這可以是本機磁碟機或在網路共用上。</br></br> 在執行此工具的電腦上，不使用這個參數時，記錄檔會位在使用者的暫存資料夾中。</br></br> 本機磁碟機的範例︰***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>網路共用的範例︰***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;共用>\&lt;資料夾>***|
