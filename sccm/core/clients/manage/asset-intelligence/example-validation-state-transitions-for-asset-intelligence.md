---
title: "Asset Intelligence 驗證狀態轉換範例 | Microsoft Docs"
description: "請參閱 System Center Configuration Manager 中 Asset Intelligence 驗證狀態轉換範例。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f280e06f34c0ed355b7c2652c571e36eb6684c59
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 的 Asset Intelligence 驗證狀態轉換範例

*適用於：System Center Configuration Manager (最新分支)*

在 System Center Configuration Manager 中，Asset Intelligence 驗證狀態並非靜態，而是可以從您執行的系統管理動作變更成影響儲存在 Asset Intelligence 類別目錄的資料。 本主題提供可能的驗證狀態轉換範例。

##  <a name="BKMK_UncategorizedIsCategorized"></a> 未分類的類別目錄項目依系統管理使用者分類  

|**狀態轉換**|**狀態轉換描述**|  
|--------------------------|--------------------------------------|  
|**未分類**|之前未被 System Center Online 分類或系統管理使用者已輸入 Asset Intelligence 類別目錄的已清查軟體項目。|  
|**未分類** 至 **使用者定義**|未分類的項目依系統管理使用者分類。|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> 已分類的類別目錄項目重新依系統管理使用者分類  

|**狀態轉換**|**狀態轉換描述**|  
|--------------------------|--------------------------------------|  
|**已驗證**|類別目錄項目已由 System Center Online 研究人員定義，位於 Asset Intelligence 類別目錄中。|  
|**已驗證** 到 **使用者定義**|驗證過的類別目錄項目重新依系統管理使用者分類。|  

> [!NOTE]  
>  因為取自 System Center Online 的分類資訊儲存在資料庫中且無法刪除，所以系統管理使用者之後可以回復為 System Center Online 分類。  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> System Center Online 重新分類使用者定義的類別目錄項目  

|**狀態轉換**|**狀態轉換描述**|  
|--------------------------|--------------------------------------|  
|**未分類**|之前未被 System Center Online 或系統管理使用者分類，但已輸入 Asset Intelligence 類別目錄的已清查軟體項目。|  
|**使用者定義**|未分類的項目依系統管理使用者分類。|  
|**使用者定義** 到 **可更新**|System Center Online 在後續的手動大量更新 Asset Intelligence 類別目錄期間，已使用不同的方式分類使用者定義的類別目錄項目。<br /><br /> 系統管理使用者可以使用 [軟體詳細資料衝突解決]  對話方塊，決定使用新的分類資訊還是使用之前的使用者定義值。|  
|**可更新** 到 **已驗證**|系統管理使用者使用 [軟體詳細資料衝突解決]  對話方塊，在之前的類別目錄更新期間，使用從 System Center Online 收到的新分類資訊。|  
|或||  
|**可更新** 到 **使用者定義**|系統管理使用者使用 [軟體詳細資料衝突解決]  對話方塊，使用先前的使用者定義值。|  

> [!NOTE]  
>  因為取自 System Center Online 的分類資訊儲存在資料庫中且無法刪除，所以系統管理使用者之後可以回復為 System Center Online 分類。  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> 將未分類的類別目錄項目提交至 System Center Online 進行分類  

|**狀態轉換**|**狀態轉換描述**|  
|--------------------------|--------------------------------------|  
|**未分類**|之前未被 System Center Online 或系統管理使用者分類，但已輸入 Asset Intelligence 資料庫的已清查軟體項目。|  
|**未分類** 到 **擱置**|未分類的類別目錄項目已提交至 System Center Online，由系統管理使用者進行分類。|  
|**擱置** 到 **已驗證**|項目由 System Center Online 分類。 系統管理使用者使用大量的類別目錄更新或 Asset Intelligence 類別目錄同步處理，將項目匯入 Asset Intelligence 類別目錄。 使用 Asset Intelligence 同步處理點站台系統角色，兩者都可以使用。|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> 將使用者定義的類別目錄項目提交至 System Center Online 進行分類  

|**狀態轉換**|**狀態轉換描述**|  
|--------------------------|--------------------------------------|  
|**未分類**|之前未被系統管理使用者或 System Center Online 分類，但已輸入 Asset Intelligence 資料庫的已清查軟體項目。|  
|**使用者定義**|您分類了未分類的項目。|  
|**使用者定義** 到 **擱置**|您要將使用者定義項目提交至 System Center Online 進行分類。|  
|**擱置** 到 **可更新**|System Center Online 在後續的類別目錄同步處理期間，已使用不同的方式分類使用者定義的類別目錄項目。 您可以使用 [解決衝突]  動作決定要使用新的分類資訊或使用之前的使用者定義值。 如需有關解決衝突的詳細資訊，請參閱[解決軟體詳細資料衝突](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)。|  
|**可更新** 到 **已驗證**|您在之前的類別目錄更新期間使用了 [解決衝突]  動作，並選取從 System Center Online 收到的新分類資訊。 如需有關解決衝突的詳細資訊，請參閱[解決軟體詳細資料衝突](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)。|  
|或||  
|**可更新** 到 **使用者定義**|您使用了 [解決衝突]  動作，並選取使用先前的使用者定義值。 如需有關解決衝突的詳細資訊，請參閱[解決軟體詳細資料衝突](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)。|  

> [!NOTE]  
>  因為取自 System Center Online 的分類資訊儲存在資料庫中且無法刪除，所以您之後可以回復為 System Center Online 分類。  
