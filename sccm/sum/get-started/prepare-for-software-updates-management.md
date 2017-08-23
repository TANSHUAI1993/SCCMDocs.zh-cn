---
title: "準備軟體更新管理 | Microsoft Docs"
description: "若要準備管理更新，請完成這些工作，以顯示 System Center Configuration Manager 主控台中的相容性評估資料。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
ms.openlocfilehash: 5c34bd1ea108dffda10c30281fb9c97ba38ae1ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-for-software-updates-management"></a>準備軟體更新管理

*適用於：System Center Configuration Manager (最新分支)*

您必須先完成下列各節中的步驟，軟體更新的相容性評估資料才會顯示在 System Center Configuration Manager 主控台中，同時您才可以將軟體更新部署到用戶端電腦。

## <a name="step-1-install-a-software-update-point"></a>步驟 1：安裝軟體更新點  
管理中心網站或獨立主要站台和主要站台上需要軟體更新點才能啟用軟體更新相容性評估，以及將軟體更新部署至用戶端。 軟體更新點在次要站台上是選用項目。 如需詳細資訊，請參閱[安裝軟體更新點](install-a-software-update-point.md)。  

## <a name="step-2-synchronize-software-updates"></a>步驟 2：同步處理軟體更新
軟體更新同步處理是擷取符合您設定之準則的軟體更新中繼資料的程序。 除非同步處理軟體更新，否則軟體更新不會顯示在 Configuration Manager 主控台中。 如需詳細資訊，請參閱[同步處理軟體更新](synchronize-software-updates.md)。   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>步驟 3：設定要同步處理的分類和產品
請在管理中心網站或獨立主要站台上執行此設定。 第一次同步處理軟體更新之後，Configuration Manager 會擷取更新的分類和產品清單。 現在，您可以從 [軟體更新點元件內容] 的新選項中進行選取。 設定新的分類和產品之後，請重複步驟 2 啟動軟體更新同步處理，以擷取新準則的軟體更新中繼資料。 如需詳細資訊，請參閱[設定要同步處理的分類和產品](configure-classifications-and-products.md)。

## <a name="step-4-manage-settings-for-software-updates"></a>步驟 4：管理軟體更新的設定
同步處理軟體更新之後，請先確認 Configuration Manager 用戶端設定、群組原則設定和軟體更新設定，再部署軟體更新。 如需詳細資訊，請參閱[管理軟體更新的設定](manage-settings-for-software-updates.md)。
