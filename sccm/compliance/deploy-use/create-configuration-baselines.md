---
title: "建立設定基準 | Microsoft Docs"
description: "在可部署至集合的 System Center Configuration Manager 中建立設定基準。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 649942d3d468ec35c7246e08f741cdebd22fb3ac
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立設定基準

*適用於︰System Center Configuration Manager (最新分支)*


System Center Configuration Manager 中的設定基準包含預先定義的設定項目和 (選擇性) 其他設定基準。 建立組態基準之後，您可以將它部署至集合，讓該集合中的裝置下載組態基準，並以此評估相容性。  

 Configuration Manager 中的設定基準可以包含特定的設定項目修訂，或者可以設定為一律使用最新版的設定項目。 如需設定項目修訂的詳細資訊，請參閱[設定資料的管理工作](../../compliance/deploy-use/management-tasks-for-configuration-data.md)。  

 有兩種方法可以用來建立設定基準：  

-   從檔案匯入組態資料。 若要啟動 [匯入組態資料精靈] ，請在 [資產與相容性]  工作區的 [設定項目]  或 [組態基準]  節點中，按一下 [匯入組態資料] 。  

-   使用 [建立組態基準]  對話方塊建立新的組態基準。  

 使用 [建立組態基準]  對話方塊，以下列程序建立組態基準。  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定基準]。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立組態基準] 。  

4.  在 [建立組態基準]  對話方塊中，輸入組態基準的唯一名稱和描述。 名稱最多可以使用 255 個字元，描述最多可以使用 512 個字元。  

5.  [組態資料]  清單會顯示隨附於這個組態基準的所有組態項目或組態基準。 按一下 [新增]  將新的組態項目或組態基準加入清單中。 您可以從下列項目中選擇：  

    -   **Configuration Items**  

    -   **軟體更新**  

    -   **Configuration Baselines**  
      > [!IMPORTANT]
      > 您必須將每個設定基準限制成不超過 1000 個軟體更新。
6.  使用 [變更目的]  清單指定您在 [組態資料]  清單中選取的組態項目行為。 您可以從下列項目中選取：  

    -   **必要** ：如果用戶端裝置上偵測不到組態項目，組態基準會評估為不相容。 如果偵測到，就會評估相容性  

    -   **選擇性** ：如果用戶端電腦上找到它所參考的應用程式，組態項目只會評估相容性。 如果找不到應用程式，組態基準不會標示為不相容 (僅適用於應用程式組態項目)。  

    -   **禁止** ：如果用戶端電腦上偵測到組態項目，組態基準會評估為不相容 (僅適用於應用程式組態項目)。  

    > [!NOTE]
    >  只有當您在 [建立設定項目精靈]  的 [一般]  頁面上按一下 [此設定項目包含應用程式設定]  選項時，才能使用 [變更目的] 清單。  

7.  使用 [變更修訂]  清單來選取特定或最新的組態項目修訂，評估用戶端裝置的相容性，或選取 [永遠使用最新版本]  一律使用最新的修訂。 如需設定項目修訂的詳細資訊，請參閱[設定資料的管理工作](../../compliance/deploy-use/management-tasks-for-configuration-data.md)。  

8.  若要從設定基準移除設定項目，請選取設定項目，然後按一下 [移除]。  

9. 按一下 [確定]  關閉 [建立組態基準]  對話方塊並建立組態基準。  
