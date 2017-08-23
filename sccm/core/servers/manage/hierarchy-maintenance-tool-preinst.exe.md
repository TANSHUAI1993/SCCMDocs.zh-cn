---
title: "階層維護工具 | Microsoft Docs"
description: "了解階層維護工具的作用，以及您可能會使用它的原因。 包含命令列選項參考。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f3ddeaadfb1418aeeaacdca47768600c86b59083
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-system-center-configuration-manager"></a>System Center Configuration Manager 的階層維護工具 (Preinst.exe)

*適用於：System Center Configuration Manager (最新分支)*

階層管理員服務在執行時，階層維護工具 (Preinst.exe) 會將命令傳送至 System Center Configuration Manager 階層管理員。 階層維護工具會在安裝 Configuration Manager 站台時自動安裝。 您可以在站台伺服器上的 \\&lt;站台伺服器名稱>\SMS_&lt;站台碼>\bin\X64\00000409 共用資料夾中找到 Preinst.exe。  

 下列案例中皆可使用階層維護工具：  

-   需要交換安全金鑰時，有時候，您必須手動起始站台之間交換公開金鑰的程序。 如需詳細資訊，請參閱本主題的 [在站台之間手動交換公開金鑰](#BKMK_ManuallyExchangeKeys) 。  

-   移除不再使用之目的地站台的非作用中作業。  

-   無法使用安裝程式解除安裝站台時，從 Configuration Manager 主控台刪除站台伺服器。 例如，若未先執行安裝程式來解除安裝站台，而實際移除 Configuration Manager 站台，其站台資訊仍會存在於父站台的資料庫中，且父站台會繼續嘗試與該子站台通訊。 若要解決此問題，就必須執行階層維護工具並從父站台的資料庫手動刪除子站台。  

-   停止站台中的所有 Configuration Manager 服務，而不必個別停止服務。  

-   復原站台時，可以使用 CHILDKEYS 選項從多個子站台發佈公開金鑰到復原站台。  

目前的使用者必須具有本機電腦的系統管理權限，才能執行階層維護工具。 此外，該使用者必須明確擁有站台 - 系統管理員安全性權限；使用者透過成為擁有該權限之群組的成員而繼承此權限是不夠的。  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>階層維護工具命令列選項  
使用階層維護工具時，必須在管理中心網站、主要站台或次要站台伺服器上本機執行。  

當您執行階層維護工具時，必須使用下列語法：preinst.exe /&lt;選項\>。 以下為命令列選項。  

 **/DELJOB &lt;站台碼**>** - 在站台上使用此選項，可刪除所有作業，或從目前的站台對指定目的地站台執行命令。  

 **/DELSITE &lt;要移除之子站台的站台碼**>** - 在父站台上使用此選項，可從公站台的站台資料庫刪除子站台的資料。 通常，如果站台伺服器電腦在您解除安裝該電腦中的站台之前即已解除委任，即可使用此選項。  

> [!NOTE]  
>  /DELSITE 選項不會解除安裝電腦中由 ChildSiteCodeToRemove 參數指定的站台。 此選項只會將站台資訊從 Configuration Manager 站台資料庫中移除。  

**/DUMP &lt;站台碼**>** - 在本機站台伺服器上使用此選項，可將站台控制映像寫入站台安裝磁碟機的根資料夾。 您可以將特定站台控制映像寫入該資料夾，也可以寫入階層中所有的站台控制檔案。  

-   /DUMP &lt;站台碼> - 只寫入指定站台的站台控制映像。  

-   /DUMP 會寫入所有站台的站台控制檔案。  

映像是以二進位形式儲存在 Configuration Manager 站台資料庫中的站台控制檔案。 傾印站台控制檔案映像是基礎映像加上擱置中差異映像的總和。  

使用階層維護工具傾印站台控制檔案映像後，檔案名稱的格式為 sitectrl_&lt;站台碼>.ct0。  

**/STOPSITE** - 在本機站台伺服器上使用此選項，可初始 Configuration Manager 站台元件管理員服務的關閉週期，而此週期將會局部重設該站台。 執行此關閉週期時，站台伺服器及其遠端站台系統上的部分 Configuration Manager 服務會停止。 這些服務會標幟為重新安裝。 由於此關機週期的緣故，重新安裝服務時，會自動變更某些密碼。  

> [!NOTE]  
>  如果要查看站台元件管理員的關閉、重新安裝及密碼變更記錄，請在使用此命令列選項之前啟用此元件的記錄功能。  

關閉週期一旦啟動後就會自動進行，並略過所有無回應的元件或電腦。 不過，如果站台元件管理員服務在關閉週期期間無法存取遠端系統，則站台元件管理員服務會在重新啟動時重新安裝原先安裝在該遠端站台系統上的元件。 站台元件管理服務重新啟動時，會重複嘗試重新安裝已標幟重新安裝的所有服務，直到成功為止。  

您可以使用 Service Manager 重新啟動站台元件管理員服務。 該服務重新啟動後，會解除安裝、重新安裝並重新啟動所有受影響的服務。 使用 /STOPSITE 選項起始關閉週期後，一旦站台元件管理員服務重新啟動之後就必須執行重新安裝週期。  

**/KEYFORPARENT** - 在站台上使用此選項，可將該站台的公開金鑰發佈至父站台。  

/KEYFORPARENT 選項會將站台的公開金鑰置於 &lt;站台碼>.CT4 檔案中，該檔案位於程式檔案磁碟機的根目錄中。 使用此選項執行 preinst.exe 後，請將 &lt;站台碼>.CT4 檔案手動複製到父站台的 ...\Inboxes\hman.box 資料夾 (非 hman.box\pubkey)。  

**/KEYFORCHILD** - 在站台上使用此選項，可將該站台的公開金鑰發佈至子站台。  

/KEYFORCHILD 選項會將站台的公開金鑰置於 &lt;站台碼>.CT5 檔案中，該檔案位於程式檔案磁碟機的根目錄中。 使用此選項執行 preinst.exe 後，請將 &lt;站台碼>.CT5 檔案手動複製到子站台的 ...\Inboxes\hman.box 資料夾 (非 hman.box\pubkey)。  

**/CHILDKEYS** - 您可以在復原站台的子站台上使用此選項。 使用此選項，可將多個子站台的公開金鑰發佈至復原站台。  

/CHILDKEYS 選項會將您執行該選項時所在站台的金鑰，以及該站台之子站台的所有公開金鑰置於 &lt;站台碼>.CT6 檔案中。  

使用此選項執行 preinst.exe 後，請將 &lt;站台碼>.CT6 檔案手動複製到復原站台的 ...\Inboxes\hman.box 資料夾 (非 hman.box\pubkey)。  

**/PARENTKEYS** - 您可以在復原站台的父站台上使用此選項。 使用此選項，可將所有父站台的公開金鑰發佈至復原站台。  

/PARENTKEYS 選項會將您執行該選項時所在站台的金鑰，以及該站台之每個上層父站台的金鑰置於 &lt;站台碼\>.CT7 檔案中。  

使用此選項執行 preinst.exe 後，請將 &lt;站台碼>.CT7 檔案手動複製到復原站台的 ...\Inboxes\hman.box 資料夾 (非 hman.box\pubkey)。  

##  <a name="BKMK_ManuallyExchangeKeys"></a> 在站台之間手動交換公開金鑰  
Configuration Manager 站台預設會啟用 [要求安全金鑰交換] 選項。 需要交換安全金鑰時，在兩種情況下，您必須手動起始站台之間交換公開金鑰的程序：  

-   如果 Active Directory 架構未針對 Configuration Manager 擴充  

-   Configuration Manager 站台未將站台資料發佈至 Active Directory  

您可以使用階層維護工具匯出每個站台的公開金鑰。 匯出金鑰後，必須手動在站台之間交換金鑰。  

> [!NOTE]  
>  手動交換公開金鑰後，您可以檢閱 **hman.log** 記錄檔，記錄檔會將發佈至 Active Directory 網域服務的站台設定變更和站台資訊記錄在父站台伺服器，以確保主要站台確實已處理新的公開金鑰。  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>將子站台公開金鑰手動傳送至父站台  

1.  登入子站台後，請開啟命令提示字元並瀏覽至 **Preinst.exe**所在位置。  

2.  輸入下列命令，匯出子站台的公開金鑰：**Preinst /keyforparent**  

3.  /keyforparent 選項會將子站台的公開金鑰置於 **&lt;站台碼\>.CT4** 檔案中，該檔案位於系統磁碟機的根目錄中。  

4.  將 **&lt;站台碼\>.CT4** 檔案移至父站台的 **&lt;安裝目錄\>\inboxes\hman.box** 資料夾。  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>將父站台公開金鑰手動傳送至子站台  

1.  登入父站台後，請開啟命令提示字元並瀏覽至 **Preinst.exe**所在位置。  

2.  輸入下列命令，匯出父站台的公開金鑰：**Preinst /keyforchild**。  

3.  /keyforchild 選項會將父站台的公開金鑰置於 **&lt;站台碼\>.CT5** 檔案中，該檔案位於系統磁碟機的根目錄中。  

4.  將 **&lt;站台碼\>.CT5** 檔案移至子站台的 **&lt;安裝目錄\>\inboxes\hman.box** 目錄。  
