---
title: "設定 Endpoint Protection | Microsoft Docs"
description: "了解如何設定 Configuration Manager 來更新並發佈 Windows Defender 的惡意程式碼定義。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6917644d6719a1ca636713aa5aebf277927123c8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-endpoint-protection"></a>設定 Endpoint Protection

*適用於：System Center Configuration Manager (最新分支)*

您必須先執行本主題所詳述的設定步驟，才能使用 Endpoint Protection 來管理 Configuration Manager 用戶端電腦上的安全性和惡意程式碼。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>如何設定 Configuration Manager 中的 Endpoint Protection  
 Configuration Manager 中的 Endpoint Protection 具有外部相依性和產品中的相依性。  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中設定 Endpoint Protection 的步驟  
 使用下表以瞭解關於設定 Endpoint Protection 的步驟、細節和詳細資訊。  

> [!IMPORTANT]  
>  如果您管理 Windows 10 電腦的 Endpoint Protection，則您必須設定 Configuration Manager 以更新及發佈 Windows Defender 的惡意程式碼定義。 Windows Defender 包含在 Windows 10，但是仍然必須安裝 SCEPInstall，且仍然需要 Endpoint Protection 的自訂用戶端設定 (下方的**步驟 5**)。  

|步驟|詳細資料|  
|-----------|-------------|  
|**步驟 1：**[建立 Endpoint Protection 點站台系統角色](endpoint-protection-site-role.md)|必須先安裝 Endpoint Protection 點站台系統角色，才能使用 Endpoint Protection。 其只能安裝在一部站台系統伺服器上，而且必須安裝於管理中心網站或獨立主要站台的階層頂端。 |  
|**步驟 2：**[設定 Endpoint Protection 的警示](endpoint-configure-alerts.md)|當特定事件發生時 (例如惡意程式碼感染)，警示會通知系統管理員。 警示顯示於 [監視]  工作區的 [警示]  節點中，或可以選擇性地透過電子郵件傳送給指定的使用者。 |  
|**步驟 3：**[設定 Endpoint Protection 用戶端的定義更新來源](endpoint-definition-updates.md)|可將 Endpoint Protection 設定為使用各種不同的來源來下載定義更新。 |  
|**步驟 4：**[設定預設反惡意程式碼原則，並建立自訂反惡意程式碼原則](endpoint-antimalware-policies.md)|安裝 Endpoint Protection 用戶端時，會套用預設反惡意程式碼原則。 根據預設，部署用戶端後 60 分鐘內即會套用任何已部署的自訂原則。 請確定您在部署 Endpoint Protection 用戶端之前，設定反惡意程式碼原則。 |  
|**步驟 5：**[設定 Endpoint Protection 的自訂用戶端設定](endpoint-protection-configure-client.md)|使用自訂用戶端設定，針對階層中的電腦集合設定 Endpoint Protection 設定。<br /><br /> 注意：請勿設定預設 Endpoint Protection 用戶端設定 (除非您確定要將這些設定套用到階層中的所有電腦)。 |  
