---
title: "使用 System Center Configuration Manager 建立 MDM 集合 | Microsoft Docs"
description: "使用 System Center Configuration Manager 建立 MDM 集合。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: fabbcfd2d5656d4fa8cb87feffe87e17998df145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 建立 MDM 集合

*適用於：System Center Configuration Manager (最新分支)*

需要有 Configuration Manager 使用者集合，才能指定可將裝置註冊至管理的使用者。 因為 Intune 授權是由使用者所指派，所以您只能使用使用者集合 (而不是裝置集合)。

> [!NOTE]
> 若要使用 Intune 來註冊裝置，您不需要將授權指派給 Office 365 入口網站或 Azure Active Directory 入口網站中的使用者。 只需要包括集合中與 Intune 訂閱相關聯的使用者 (在[稍後步驟](configure-intune-subscription.md)中)。

基於測試，您可以設定**直接規則**，並新增可註冊裝置的特定使用者。 在 Configuration Manager 主控台中，選擇 [資產與合規性] > [使用者集合]，並按一下 [常用] 索引標籤 > [建立] 群組，然後按一下 [建立使用者集合]。 針對更廣泛的發佈，您應該使用 [查詢規則] 來定義使用者。 如需集合的詳細資訊，請參閱[如何建立集合](https://technet.microsoft.com/library/mt629371.aspx)。

![建立 MDM 的使用者集合](../media/mdm-create-user-collection.png)

> [!div class="button"]
[下一個步驟 >](confirm-dns.md)
