---
title: "電子郵件設定檔的必要條件 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的電子郵件設定檔和其產品內外部的相依性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 451317db1d7aab888c03d1a099b9ce25311e06d0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="email-profile-prerequisites"></a>電子郵件設定檔必要條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的電子郵件設定檔在產品內外部都有相依性。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|必須授與特定安全性權限，才能管理電子郵件設定檔|您必須具備下列安全性權限，才能管理公司資源存取設定，例如電子郵件設定檔：<br /><br /> - 檢視與管理電子郵件設定檔的警示和報告：[警示] 物件的 [建立]、[刪除]、[修改]、[修改報告]、[讀取] 和 [執行報告] 權限。<br /><br /> - 建立和管理憑證設定檔：[憑證設定檔] 物件的 [撰寫原則]、[修改報告]、[讀取] 和 [執行報告] 權限。<br /><br /> - 管理電子郵件設定檔部署：[集合] 物件的 [部署設定原則]、[修改用戶端狀態警示]、[讀取] 和 [讀取資源] 權限。<br /><br /> - 管理所有設定原則：[設定原則] 物件的 [建立]、[刪除]、[修改]、[讀取]和 [設定安全性範圍] 權限。<br /><br /> - 執行與電子郵件設定檔相關的查詢：[查詢] 物件的 [讀取] 權限。<br /><br /> 在 System Center Configuration Manager 主控台中檢視電子郵件設定檔資訊：[站台] 物件的 [讀取] 權限。<br /><br /> - 檢視電子郵件設定檔的狀態訊息：[狀態訊息] 物件的 [讀取] 權限。<br /><br /> - 建立和管理電子郵件設定檔：[通訊佈建設定檔] 物件的 [撰寫原則]、[修改報告]、[讀取] 和 [執行報告] 權限。<br /><br /> [公司資源存取管理員] 安全性角色包括在 System Center Configuration Manager 中管理電子郵件設定檔所需的上列權限。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中設定安全性](../../core/plan-design/security/configure-security.md)。|  
|Active Directory 中的郵件屬性|如果您要利用使用者的主要 SMTP 位址，在電子郵件設定檔中產生使用者電子郵件地址，則必須設定 System Center Configuration Manager 使用者探索，以從 Active Directory 探索 [郵件] 屬性 (這是預設設定)。|  

## <a name="external-dependencies"></a>外部相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|Active Directory 中的郵件屬性|如果您要利用使用者的主要 SMTP 位址，在電子郵件設定檔中產生使用者的電子郵件地址，此位址必須存在於 Active Directory 的 [郵件] 屬性中。<br /><br /> 如需詳細資訊，請參閱 Windows Server 文件。|
