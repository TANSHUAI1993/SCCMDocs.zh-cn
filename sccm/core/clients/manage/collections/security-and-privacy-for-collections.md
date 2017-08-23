---
title: "集合安全性和隱私權 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中集合的安全性與隱私權最佳作法。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0cade975e96220e193db1de92816f97cd253532d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager 中集合的安全性和隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 集合的安全性最佳作法和隱私權資訊。  

 沒有專門針對 Configuration Manager 集合的隱私權資訊。 集合是資源的容器，例如使用者和裝置。 集合成員資格通常依賴 Configuration Manager 在標準作業期間所收集的資訊。 例如，透過使用從探索或清查收集到的資源資訊，集合可以設定成包含符合指定準則的裝置。 集合也可以用戶端管理作業目前的狀態資訊為基礎，例如部署軟體和檢查相容性。 除了這些查詢式的集合，系統管理使用者也可以在資源中加入集合。  

 如需有關集合的詳細資訊，請參閱 [System Center Configuration Manager 的集合簡介](../../../../core/clients/manage/collections/introduction-to-collections.md)。 如需可用於設定集合成員資格之 Configuration Manager 作業的安全性最佳作法詳細資訊和隱私權資訊，請參閱 [System Center Configuration Manager 的安全性最佳作法和隱私權資訊](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md)。  

## <a name="security-best-practices-for-collections"></a>集合的安全性最佳做法  
 請使用下列集合安全性最佳做法。  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|當您使用儲存在網路位置的受管理物件格式 (MOF) 檔案匯出或匯入集合時，請保護位置和網路通道。|限制存取網路資料夾的人員。<br /><br /> 使用在網路位置和站台伺服器之間的伺服器訊息區 (SMB) 簽署或網際網路通訊協定安全性 (IPsec)，防止攻擊者竄改匯出的集合資料。 在網路上使用 IPsec 為資料加密，以防止洩露資訊。|  

### <a name="security-issues-for-collections"></a>集合的安全性問題  
 集合有下列安全性問題：  

-   如果您使用集合變數，本機系統管理員可以讀取潛在的敏感資訊。  

     當您部署作業系統時，可以使用集合變數。  
