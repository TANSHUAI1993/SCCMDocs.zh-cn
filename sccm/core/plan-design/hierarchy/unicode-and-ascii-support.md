---
title: "Unicode 和 ASCII 支援 | Microsoft Docs"
description: "了解 System Center Configuration Manager 物件中的 Unicode 和 ASCII 字元支援。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 18f1c64c1f27001a0fdfbab4236d09a5bc279272
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Unicode 和 ASCII 支援

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 會使用 Unicode 字元建立大部分的物件。 不過，有幾個物件僅支援 ASCII 字元，或者有其他限制。  

 下節所列的物件只能使用 ASCII 字元集的字元，或者會有其他限制。  

-   [使用 ASCII 字元的物件](#BKMK_ASCIIchar)  

-   [其他限制](#BKMK_OtherCharLimitations)  

-   [未當地語系化的 Configuration Manager 物件](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> 使用 ASCII 字元的物件  
 只有在建立下列物件時，Configuration Manager 才支援 ASCII 字元集：  

-   站台碼  

-   所有站台系統伺服器電腦的名稱  

-   下列 Configuration Manager 帳戶：  

    > [!NOTE]  
    >  這些帳戶支援 ACSII 字元，並在以俄文執行的站台上支援 RUS 字元。  

    -   用戶端推入安裝帳戶  

    -   健全狀況狀態參照發佈帳戶  

    -   健全狀況狀態參照查詢帳戶  

    -   管理點資料庫連線帳戶  

    -   網路存取帳戶  

    -   套件存取帳戶  

    -   標準傳送者帳戶  

    -   站台系統安裝帳戶  

    -   軟體更新點連線帳戶  

    -   軟體更新點 Proxy 伺服器帳戶  

    > [!NOTE]  
    >  您所指定之以角色為基礎的系統管理帳戶支援 Unicode。  
    >   
    >  Reporting Services 點帳戶支援 Unicode，但不支援 RUS 字元。  

-   站台伺服器及站台系統的完整網域名稱 (FQDN)  

-   Configuration Manager 的安裝路徑  

-   SQL Server 執行個體名稱  

-   下列站台系統角色的路徑：  

    -   應用程式類別目錄 Web 服務點  

    -   應用程式類別目錄網站點  

    -   註冊點  

    -   註冊 Proxy 點  

    -   Reporting Services 點  

    -   狀態移轉點  

-   下列資料夾的路徑：  

    -   用於儲存用戶端狀態移轉資料的資料夾  

    -   包含 Configuration Manager 報告的資料夾  

    -   用於儲存 Configuration Manager 備份的資料夾  

    -   用於儲存站台安裝程式安裝來源檔案的資料夾  

    -   用於儲存安裝程式必須使用之下載內容的資料夾  

-   下列物件的路徑：  

    -   IIS 網站  

    -   虛擬應用程式的安裝路徑  

    -   虛擬應用程式名稱  

-   AMT 及頻外管理的下列物件：  

    -   AMT-based 型電腦的 FQDN  

    -   AMT 型電腦的電腦名稱  

    -   網域 NetBIOS 名稱  

    -   無線設定檔名稱和 SSID  

    -   受信任的根憑證授權單位名稱  

    -   憑證授權單位 (CA) 的名稱和範本名稱  

    -   IDE 重新導向映像檔的檔案名稱和路徑  

    -   AMT 資料儲存區的內容  

-   開機媒體 ISO 檔案名稱  

##  <a name="BKMK_OtherCharLimitations"></a> 其他限制  
 以下是可支援字元集和語言版本的其他限制：  

-   Configuration Manager 不支援變更站台伺服器電腦的地區設定。  

-   企業憑證授權單位 (CA) 不支援使用雙位元組字元集 (DBCS) 的用戶端電腦名稱。 可使用的用戶端電腦名稱受限於 IA5 字元集的 PKI 限制。 此外，Configuration Manager 不支援使用 DBCS 的 CA 名稱或主體名稱值。  

##  <a name="BKMK_LangNonLocalize"></a> 未當地語系化的 Configuration Manager 物件  
 Configuration Manager 資料庫支援多數已儲存物件使用的 Unicode，如果可以，會以符合電腦地區設定的作業系統語言顯示此項資訊。 電腦的地區設定必須與安裝在站台之用戶端或伺服器語言一致，用戶端介面或 Configuration Manager 主控台才能以該電腦的作業系統語言顯示資訊。  

 不過，有幾個 Configuration Manager 物件並不支援 Unicode，而是使用 ASCII 儲存在資料庫中，或者有其他語言限制。 這項資訊一律會使用 ASCII 字元集或建立該物件時所使用的語言顯示。  
