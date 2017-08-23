---
title: "移轉安全性和隱私權 | Microsoft Docs"
description: "取得移轉至 System Center Configuration Manager 環境的安全性最佳做法和隱私權資訊。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8aa6971d75924ab5bcacd70c330913097ecf8717
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>移轉至 System Center Configuration Manager 的安全性和隱私權

*適用於：System Center Configuration Manager (最新分支)*

本主題包含移轉至 System Center Configuration Manager 環境的安全性最佳做法和隱私權資訊。  

## <a name="security-best-practices-for-migration"></a>適用於移轉的安全性最佳作法  
 使用下列適用於移轉的安全性最佳作法。  

|安全性最佳作法|詳細資訊|  
|----------------------------|----------------------|  
|針對來源站台 SMS Provider 帳戶和來源站台 SQL Server 帳戶使用電腦帳戶，而不是使用者帳戶。|如果您必須使用適用於移轉的使用者帳戶，當完成移轉時，請移除帳戶詳細資料。|  
|當您將內容從來源站台之發佈點移轉至目的地站台之發佈點時，便可使用 IPsec。|雖然已雜湊移轉之內容來偵測竄改 (如果資料在傳送時遭到修改)，移轉作業將會失敗。|  
|限制並監視可建立移轉作業的系統管理使用者。|目的地階層之資料庫整體性，取決於系統管理使用者選擇從來源階層匯入的資料整體性。 此外，此系統管理使用者可讀取來源階層的所有資料。|  

### <a name="security-issues-for-migration"></a>移轉的安全性問題  
移轉有下列安全性問題：  

-   也許可在移轉其用戶端記錄之前，將從來源站台封鎖的用戶端成功指派到目的地階層。  

     雖然 Configuration Manager 保留您移轉之用戶端的封鎖狀態，但如果指派作業是在完成用戶端記錄之移轉作業之前發生，用戶端便可成功指派到目的地階層。  

-   不會移轉稽核訊息。  

當您將資料從來源站台移轉到目的地站台時，會遺失來源階層的稽核資訊。  

## <a name="privacy-information-for-migration"></a>適用於移轉的隱私權資訊  
 移轉時會發現您在來源基礎結構中識別出的站台資料庫的資訊，並會將此資料儲存到目的地階層中的資料庫。 System Center Configuration Manager 可從來源站台或階層探索到哪些資訊，取決於來源環境啟用哪些功能，以及該來源環境執行的管理作業。  

 如需有關安全性和隱私權資的詳細資訊，請參閱下列其中一個主題：  

-   如需 Configuration Manager 2007 隱私權資訊的詳細資訊，請參閱 Configuration Manager 2007 文件庫中的 [Configuration Manager 2007 的安全性與隱私權](http://go.microsoft.com/fwlink/p/?LinkId=216450)。  

-   如需 System Center 2012 Configuration Manager 隱私權資訊的詳細資訊，請參閱 System Center 2012 Configuration Manager 文件庫中的 [System Center 2012 Configuration Manager 的安全性和隱私權](https://technet.microsoft.com/library/gg682033.aspx)。  

-   如需 System Center Configuration Manager 隱私權資訊的詳細資訊，請參閱 [System Center Configuration Manager 的安全性和隱私權](../../core/plan-design/security/security-and-privacy.md)。  

您可以將部分或全部的受支援資料從來源站台移轉到目的地階層。  

預設不啟用移轉功能，而且需要數個設定步驟。 不會將移轉資訊傳送給 Microsoft。  

從來源階層移轉資料時，需先考慮您的隱私權需求。  
