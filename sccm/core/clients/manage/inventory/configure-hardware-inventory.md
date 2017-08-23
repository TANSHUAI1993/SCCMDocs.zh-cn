---
title: "設定硬體清查 | Microsoft Docs"
description: "在 System Center Configuration Manager 中設定所有用戶端或集合的硬體清查。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0baadb95ec8dbb945f1a611ebb95a03cec3199bd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

適用於：System Center Configuration Manager (最新分支)

此程序可設定硬體清查的預設用戶端設定，並套用到階層中的所有用戶端。 如果您只想要將這些設定套用至部分用戶端，請建立自訂裝置用戶端設定，並將它指派給包含您要設定硬體清查之裝置的集合。 請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)。  

> [!NOTE]  
>  如果用戶端裝置收到來自多組用戶端設定的硬體清查設定，則當用戶端報告硬體清查時，會將每組設定的硬體清查類別合併。  

### <a name="to-configure-hardware-inventory"></a>若要設定硬體清查  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定] > [預設用戶端設定]。  

4.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

5.  在 [預設設定] 對話方塊中，選擇 [硬體清查]。  

6.  在 [裝置設定]  清單中，設定下列項目：  

    -   **在用戶端上啟用硬體清查** - 選取 [True]。  

    -   **硬體清查排程** - 按一下 [排程] 指定用戶端收集硬體清查的時間間隔。  

7.  設定您需要的其他[硬體清查用戶端設定](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)。  

在下次下載用戶端原則時，用戶端裝置會使用這些設定來進行設定。 若要起始單一用戶端的原則擷取，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  
