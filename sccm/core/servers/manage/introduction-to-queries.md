---
title: "查詢簡介 | Microsoft Docs"
description: "建立並執行查詢，以找出 System Center Configuration Manager 階層中符合查詢準則的物件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f84d518670c0ece3c08c890d2293335518f7f8e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager 的查詢簡介

適用於：System Center Configuration Manager (最新分支)

您可以建立並執行查詢，以找出 System Center Configuration Manager 階層中符合查詢準則的物件。 這些物件包含電腦或使用者群組等特定類型的項目。 查詢可以傳回大部分類型的 Configuration Manager 物件，其中包括網站、集合、應用程式以及清查資料。  

 建立查詢時，您必須指定至少兩個參數：要搜尋的位置與您想要搜尋的項目。 例如，若要尋找 Configuration Manager 站台中所有電腦的可用硬碟空間量，您可以建立查詢以搜尋 [邏輯磁碟] 屬性類別和 [可用空間 (MB)] 屬性，以取得可用硬碟空間。  

 建立初始查詢之後，您可以指定其他的查詢準則。 例如，您可以指定查詢結果僅包含指派給指定站台的電腦。 您也可以修改結果的顯示方式，依您所需的順序來檢視結果。 例如，您可以指定依可用硬碟空間量的遞增或遞減順序來排序結果。  

 當您建立查詢時，Configuration Manager 會將其儲存並顯示在 [監視] 工作區的 [查詢] 節點中。 您可以從這個位置建立新的查詢，然後執行、更新或管理現有的查詢。  

 您也可以將查詢匯入 Configuration Manager 集合中的查詢規則。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../core/clients/manage/collections/create-collections.md)。  

## <a name="see-also"></a>另請參閱  
 [System Center Configuration Manager 的查詢技術參考](../../../core/servers/manage/queries-technical-reference.md)
