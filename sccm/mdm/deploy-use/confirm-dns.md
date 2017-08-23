---
title: "使用 System Center Configuration Manager 確認網域名稱需求 | Microsoft Docs"
description: "使用 System Center Configuration Manager 確認網域名稱需求。"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: "18"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 35b24294073956a6bdb14cae07705f56d31e00a9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 確認網域名稱需求

*適用對象：System Center Configuration Manager (最新分支)*

如有必要，請採取下列步驟來滿足 Configuration Manager 外部的任何相依性：

1. 每位使用者都必須要有指派來註冊裝置的 Intune 授權。 若要建立 Intune 授權與使用者的關聯，每個使用者都必須要有可公開解析的使用者主要名稱 (UPN) (例如 johndoe@contoso.com) 或於 Azure Active Directory 中設定的替代登入識別碼。 例如，設定替代登入識別碼可讓使用者使用電子郵件地址登入，即使其 UPN 的格式為 NetBIOS 也是一樣 (例如，CONTOSO\johndoe)。

  - 如果貴公司使用可公開解析的 UPN (即 johndoe@contoso.com)，就不需要進行後續設定。
  - 如果公司使用無法解析的 UPN (即 CONTOSO\johndoe)，則您必須[在 Azure Active Directory 中設定替代識別碼](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)。

2.  部署和設定 Active Directory Federation Services (AD FS)。 (選用)

     當您設定單一登入時，您的使用者可使用其公司認證登入，以存取 Intune 中的服務。

     如需詳細資訊，請參閱下列主題：
    -   [準備進行單一登入](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [規劃及部署 AD FS 2.0 以搭配使用單一登入](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  部署及設定目錄同步處理。

     目錄同步處理可讓您在 Intune 中填入同步處理的使用者帳戶。 同步處理的使用者帳戶和安全性群組會新增至 Intune。 無法註冊目錄同步作業是使用 Microsoft Intune 設定 Configuration Manager MDM 時，無法註冊裝置的一個常見原因。

     如需詳細資訊，請參閱 Active Directory 文件庫中的 [目錄整合](http://go.microsoft.com/fwlink/?LinkID=271120) 。

4.  選擇性但不建議：如果您未使用 Active Directory Federation Services，可重新設定使用者的 Microsoft Online 密碼。

     如果您未使用 AD FS，您必須為每個使用者設定 Microsoft Online 密碼。

> [!div class="button"]
[< 上一個步驟](create-mdm-collection.md)  [下一個步驟 >](configure-intune-subscription.md)
