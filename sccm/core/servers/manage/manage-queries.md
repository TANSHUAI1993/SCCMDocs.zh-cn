---
title: "管理查詢 | Microsoft Docs"
description: "了解如何管理查詢。 包含詳細參考資料表。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 738dcf0b52f18b38b732bf8ca5d7a87369b1c468
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理查詢

*適用對象：System Center Configuration Manager (最新分支)*

請使用本主題中的資訊協助您管理 System Center Configuration Manager 的查詢。  

 如需如何建立查詢的資訊，請參閱[如何在 System Center Configuration Manager 中建立查詢](../../../core/servers/manage/create-queries.md)。  

## <a name="how-to-manage-queries"></a>如何管理查詢  
 在 [監視]  工作區中，選取 [查詢] ，並選取要管理的查詢，然後選取管理工作。  

 請參閱下表，了解選取管理工作前需要知道的資訊。  

|管理工作|詳細資料|詳細資訊|  
|---------------------|-------------|----------------------|  
|**執行**|執行選取的查詢，並在 Configuration Manager 主控台中顯示結果。|沒有其他資訊。|  
|**安裝用戶端**|開啟 [安裝用戶端精靈]，可讓您在所選取查詢傳回的電腦上安裝 Configuration Manager 用戶端。<br /><br /> 這個選項不適用於傳回行動裝置、使用者或使用者群組的查詢。|如需如何使用用戶端推入安裝 Configuration Manager 用戶端的詳細資訊，請參閱[將用戶端部署到 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。|  
|**匯出**|開啟 [匯出物件精靈]  ，可讓您將這個查詢匯出至管理物件格式 (MOF) 檔案，之後再於另一個站台匯入這個檔案。|沒有其他資訊。|  
|**移動**|開啟 [移動選取的項目]  對話方塊，您可以在其中將選取的查詢移至先前在 [查詢]  節點下建立的資料夾。|沒有其他資訊。|  

## <a name="see-also"></a>另請參閱  
 [System Center Configuration Manager 中查詢的作業和維護](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
