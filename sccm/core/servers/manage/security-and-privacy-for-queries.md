---
title: "查詢的安全性和隱私權 | Microsoft Docs"
description: "當您查詢站台資料庫中的資訊時，請了解安全性和隱私權的最佳做法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager 的查詢安全性和隱私權

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 的查詢可讓您從以指定準則為基礎的站台資料庫中擷取資訊。 Configuration Manager 會在標準作業期間收集站台資料庫資訊。 例如，透過使用從探索或清查收集到的資訊，您可以設定查詢識別符合指定準則的裝置。  

 如需查詢的詳細資訊，請參閱 [System Center Configuration Manager 的查詢簡介](../../../core/servers/manage/introduction-to-queries.md)。 如需使用查詢擷取收集資訊之 Configuration Manager 作業的安全性最佳做法和隱私權資訊的詳細資訊，請參閱 [System Center Configuration Manager 的安全性和隱私權](../../../core/plan-design/security/security-and-privacy.md)。  

## <a name="security-best-practices-for-queries"></a>查詢的安全性最佳做法  
 請使用下列查詢安全性最佳做法。  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|當您要匯出或匯入儲存在網路位置的查詢時，請保護位置和網路通道。|限制誰可以存取網路資料夾。<br /><br /> 使用在網路位置和站台伺服器之間的伺服器訊息區 (SMB) 簽署或網際網路通訊協定安全性 (IPsec)，在匯入前防止攻擊者竄改查詢資料。|  

## <a name="see-also"></a>請參閱  
 [System Center Configuration Manager 的查詢技術參考](../../../core/servers/manage/queries-technical-reference.md)
