---
title: "System Center Configuration Manager 的基礎 | Microsoft Docs"
description: "深入了解 System Center Configuration Manager 的基本概念。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 662ac092746f37c354e5accf288e3375c16b9c72
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-system-center-configuration-manager"></a>System Center Configuration Manager 的基礎

適用於：System Center Configuration Manager (最新分支)

如果您不熟悉 System Center Configuration Manager，請在執行安裝程式安裝您的第一個站台之前，先閱讀基本主題了解 Configuration Manager 的基本概念。 如果您熟悉 Configuration Manager，則可深入了解。 建議您從 [System Center Configuration Manager 的新功能](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)開始。  

 如需有關支援的作業系統以及支援的環境、硬體需求和容量資訊的詳細資訊，請參閱 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)。  

 當您部署 Configuration Manager 時，會部署一個或多個站台：  

-   **當您部署多個站台時**，站台會形成父子關聯性，統稱為階層。 使用階層集中管理大量站台和裝置。  資料和資訊在階層往下流動，送達您所管理的裝置。 裝置的資訊，以及設定工作和要求的結果，會在階層中往上流動。  

-   **當您部署單一站台時**，它也稱為「階層」。  

 某些組態工作和設定將套用至階層中的所有站台，而其他則套用至個別站台。  

## <a name="fundamental-concepts-for-system-center-configuration-manager"></a>System Center Configuration Manager 的基本概念
檢視下列各主題來了解 System Center Configuration Manager 的基本概念：  

-   [System Center Configuration Manager 的站台和階層基本概念](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [使用 System Center Configuration Manager 來管理裝置的基本概念](../../core/understand/fundamentals-of-managing-devices.md)  

-   [System Center Configuration Manager 的用戶端管理基本概念](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [System Center Configuration Manager 的安全性基本概念](../../core/understand/fundamentals-of-security.md)  
