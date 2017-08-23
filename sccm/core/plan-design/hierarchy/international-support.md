---
title: "多語系支援 | Microsoft Docs"
description: "設定 System Center Configuration Manager 以符合特定的國際需求。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bab51be96445f766e8f5bbf54eee854e5d09cee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="international-support-in-system-center-configuration-manager"></a>System Center Configuration Manager 的多語系支援

*適用對象：System Center Configuration Manager (最新分支)*

下列各節提供的技術詳細資料可協助您設定 System Center Configuration Manager，使其符合特定國際的需求。  

## <a name="gb18030-requirements"></a>GB18030 需求  
 Configuration Manager 符合 GB18030 中定義的標準，因此您可以在中國使用 Configuration Manager。 符合 GB18030 需求的 Configuration Manager 部署必須使用下列設定：  

-   使用 Configuration Manager 時，所用的每一台站台伺服器電腦和 SQL Server 電腦都必須使用中文作業系統。  

-   階層中的每個站台資料庫和每個 SQL Server 執行個體都必須使用相同的集合，而且必須為下列其中之一：  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  這些資料庫定序是 [System Center Configuration Manager 的 SQL Server 版本支援](../../../core/plan-design/configs/support-for-sql-server-versions.md)中所述需求的例外狀況。  

-   您必須將名為 **GB18030.SMS** 的檔案置於階層中每台站台伺服器電腦系統磁碟區的根資料夾中。 此檔案不含任何資料，而且可以是根據此需求命名的空白文字檔。  
