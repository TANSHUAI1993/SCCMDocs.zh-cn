---
title: "建立子設定項目 | Microsoft Docs"
description: "在 System Center Configuration Manager 中建立子設定項目。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 33d4a2d5a09af74e1d76ac9b34a42b749f5bf7ef
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>如何建立 System Center Configuration Manager 中的子組態項目

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的子設定項目是設定項目的複本，其保留原始設定項目的關聯性，因此會繼承父設定項目的原始設定。  

當您在 Configuration Manager 主控台中檢視子設定項目的內容時，無法編輯含有其驗證準則的繼承物件和設定。 不過，您可以將額外驗證準則新增至子組態項目並加以編輯，您也可以將新的物件和設定新增至子組態項目。
建立和編輯子設定項目的一般用途是重新調整原始設定項目，以符合商務需求。  

> [!NOTE]  
>  您只能透過 [Windows 桌上型電腦和伺服器 (自訂)] 類型的組態項目來建立子組態項目。  

## <a name="to-create-a-child-configuration-item"></a>若要建立子組態項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定項目]。  

3.  在 [設定項目]  清單中，選取您要為其建立子設定項目的設定項目，然後在 [首頁]  索引標籤的 [設定項目]  群組中，按一下 [建立子設定項目] 。  

4.  在 [建立子設定項目精靈]  的 [一般] 頁面中，您可以選擇父設定項目的特定修訂版以用來建立子項。 此精靈的其他步驟與建立標準組態項目的步驟一致。 如需詳細資訊，請參閱[如何為 Windows 桌上型電腦和伺服器電腦建立自訂設定項目](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)。  

5.  完成精靈。 新的子設定項目即會顯示在 [設定項目]  清單中。  
