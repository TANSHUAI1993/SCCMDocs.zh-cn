---
title: "規劃憑證範本權限 | Microsoft Docs"
description: "了解規劃設定 System Center Configuration Manager 所使用憑證範本所需的權限。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 832be8c9fda727804f57e83768cd8799db722c67
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-system-center-configuration-manager"></a>規劃憑證設定檔在 System Center Configuration Manager 中的憑證範本權限

*適用於：System Center Configuration Manager (最新分支)*


下列資訊有助於規劃如何設定 System Center Configuration Manager 在您部署憑證設定檔時所使用憑證範本的權限。  

## <a name="default-security-permissions-and-considerations"></a>預設的安全性權限和考量  
 System Center Configuration Manager 用於要求使用者和裝置憑證的憑證範本所需的預設安全性權限如下：  

-   網路裝置註冊服務應用程式集區所使用帳戶的讀取和註冊權限  

-   執行 System Center Configuration Manager 主控台之帳戶的讀取權限  

 如需這些安全性權限的詳細資訊，請參閱[設定憑證基礎結構](../deploy-use/certificate-infrastructure.md)。  

 若使用此預設定，使用者和裝置即無法直接向憑證範本要求憑證，而所有的要求都必須由網路裝置註冊服務起始。 這項限制非常重要，因為這些憑證範本的憑證主體必須設成 [在要求中提供]  ，意即若有惡意使用者或安全受損的裝置要求憑證，便會有身分遭冒用的風險。 若使用預設設定，則必須由網路裝置註冊服務起始這類要求。 不過，如果執行網路裝置註冊服務的服務安全受到危害，仍然會有身分遭冒用的風險。 為避開此風險，請遵循網路裝置註冊服務及執行此角色服務之電腦的所有安全性最佳作法。  

 如果預設的安全性權限無法滿足您的業務需求，您可選擇另一種設定憑證範本安全性權限的方式：您可以新增使用者及電腦的 [讀取] 和 [註冊]權限。  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>新增使用者及電腦的讀取和註冊權限  
 如果您的憑證授權單位 (CA) 基礎結構團隊由不同團隊負責管理，且該團隊希望 System Center Configuration Manager 能先驗證使用者是否擁有有效的 Active Directory 網域服務帳戶，然後才傳送憑證設定檔給使用者以要求使用者憑證，新增使用者及電腦的讀取和註冊權限會是較適當的方式。 對於此設定，您必須先指定一個或多個包含使用者的安全性群組，然後才授與這些群組憑證範本的讀取和註冊權限。 在此種案例中，安全性控制由 CA 系統管理員負責管理。  

 同樣地，您可以指定一個或多個包含電腦帳戶的安全性群組，並授與這些群組憑證範本的讀取和註冊權限。 如果您將電腦憑證設定檔部署到屬於網域成員的電腦，便需為該電腦的電腦帳戶授與讀取和註冊權限。 如果電腦不是網域成員 (例如，如果它是工作群組電腦或個人行動裝置)，便不需要這些權限。  

 雖然這項設定使用額外的安全性控制，但卻不是建議的最佳作法。 原因是指定的裝置使用者或擁有者可能會個別向 System Center Configuration Manager 要求憑證，並且提供可能用來假冒其他使用者或裝置的憑證主體值。  

 此外，如果您指定了無法在要求憑證時通過驗證的帳戶，根據預設，憑證要求將會失敗。 例如，假設執行網路裝置註冊服務的伺服器在 Active Directory 樹系中，而包含憑證登錄點站台系統伺服器的樹系並不信任該 Active Directory 樹系，憑證要求便會失敗。 您可以設定讓憑證登錄點在帳戶因為網路控制器無回應而無法驗證時繼續作業。 不過，這並不是安全性最佳作法。  

 請注意，如果為了確認帳戶權限而設定憑證登錄點，而且網域控制站在可用的情況下拒絕驗證要求 (例如帳戶已鎖定或刪除)，憑證註冊要求將會失敗。  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>檢查使用者及屬於網域成員之電腦的讀取和註冊權限  

1.  在裝載憑證登錄點的站台系統伺服器上，建立下列具有值 0 的 DWORD 登錄機碼：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  如果帳戶因為網域控制站無回應而無法驗證，且您希望略過權限檢查：  

    -   在裝載憑證登錄點的站台系統伺服器上，建立下列具有值 1 的 DWORD 登錄機碼：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  在發行 CA 上，在憑證範本內容的 [安全性]  索引標籤上，新增一個或多個安全性群組，以為使用者或裝置帳戶授與讀取和註冊權限。  
