---
title: "Asset Intelligence 安全性隱私權 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中 Asset Intelligence 的安全性與隱私權資訊。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b12054cce52e2b83715a083d78a62e06b5127a2f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 中 Asset Intelligence 的安全性與隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 中 Asset Intelligence 的安全性與隱私權資訊。  

##  <a name="BKMK_Security_AI"></a> Asset Intelligence 的安全性最佳作法  
 使用 Asset Intelligence 時，請使用下列安全性最佳作法。  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|當您匯入授權檔案 (Microsoft 大量授權檔案或一般授權聲明檔案) 時，請保護檔案和通訊通道的安全。|使用 NTFS 檔案系統權限，確保只有授權的使用者才能存取授權檔，以及使用伺服器訊息區 (SMB) 簽署，確保匯入程序期間傳送到站台伺服器時的資料完整性。|  
|使用最低權限的原則來匯入授權檔案。|使用以角色為基礎的系統管理，將 [管理 Asset Intelligence] 權限授與匯入授權檔案的系統管理使用者。 內建角色 [資產管理員] 包含這個權限。|  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Asset Intelligence 的隱私權資訊  
 Asset Intelligence 可擴充 Configuration Manager 的清查功能，以提供企業中更高層級的資產可見性。 不會自動啟用 Asset Intelligence 資訊收集。 您可以修改透過啟用硬體清查報告類別所收集的資訊類型。 如需詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

 Asset Intelligence 資訊儲存在 Configuration Manager 資料庫的方式，與清查資訊相同。 用戶端使用 HTTPS 來連線至管理點時，一律會在傳送至管理點期間加密資料。 用戶端使用 HTTP 連線時，您可以設定要簽署和加密的清查資料傳送。 清查資料不會以加密格式儲存在資料庫中。 資訊會保留在資料庫中，直到以每 90 天的間隔由站台維護工作 [刪除過時清查歷程記錄]  將它刪除為止。 您可以設定刪除間隔。  

 Asset Intelligence 不會傳送有關使用者和電腦或授權使用的資訊給 Microsoft。 您可以選擇傳送 System Center Online 要求進行分類，這表示您可以標記未分類的一個或多個軟體項目，並將其傳送給 System Center Online 進行研究和分類。 在上傳軟體項目之後，Microsoft 研究人員會進行識別、分類，然後將該知識提供給所有使用線上服務的客戶。 您應該注意將資訊提交給 System Center Online 的下列隱私權含意：  

-   上傳僅適用於您選擇要傳送至 System Center Online 的一般軟體項目資訊 (名稱、發行者等)。 清查資訊不會使用上傳進行傳送。  

-   上傳絕不會自動發生，系統並沒有設計成自動完成此工作。 您必須手動選取以及核准各個軟體標題的上傳。  

-   上傳程序之前，會有對話方塊確實顯示要上傳的資料。  

-   不會將授權資訊傳送給 Microsoft。 授權資訊會儲存在 Configuration Manager 資料庫的不同區域中，而且不會傳送給 Microsoft。  

-   任何上傳的軟體項目皆會公開，因此提供的應用程式與其分類會成為 System Center Online Asset Intelligence 類別目錄的一部分，然後可供類別目錄的其他客戶下載。  

-   軟體項目的來源不會記錄在 Asset Intelligence 類別目錄中，並且不供其他客戶使用。 不過，您仍然必須確認未載入任何包含任何私人資訊的應用程式標題。  

-   資料一旦上傳就無法取回。  

 在您設定 Asset Intelligence 資料收集並且決定是否將資訊提交給 System Center Online 之前，請考慮貴組織的隱私權需求。  
