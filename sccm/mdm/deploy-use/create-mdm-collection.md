---
title: "使用 System Center Configuration Manager 创建 MDM 集合 | Microsoft Docs"
description: "使用 System Center Configuration Manager 创建 MDM 集合。"
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
ms.openlocfilehash: 43316e4915b27aaeca563eaf52b51f053a839222
ms.sourcegitcommit: 974fbc4408028c8be28911e5cd646efcf47c7f15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2017
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 创建 MDM 集合

*适用范围：System Center Configuration Manager (Current Branch)*

需要 Configuration Manager 用户集合以指定可以向管理中注册设备的用户。 由于 Intune 许可证由用户进行分配，所以只能使用用户集合（而非设备集合）。

> [!NOTE]
> 若要向 Intune 注册设备，无需在 Office 365 门户或 Azure Active Directory 门户中向用户分配许可证。 只需在与 Intune 订阅（在一个[后续步骤](configure-intune-subscription.md)中）关联的集合中包括用户即可。

为进行测试，可以设置**直接规则**并添加可以注册设备的特定用户。 在 Configuration Manager 控制台中，选择“资产和符合性” > “用户集合”，单击“主页”选项卡 >“创建”组，然后单击“创建用户集合”。 若要实现更广泛的分发，应使用**查询规则**定义用户。 有关集合的详细信息，请参阅[如何创建集合](https://technet.microsoft.com/library/mt629371.aspx)。

![为 MDM 创建用户集合](../media/mdm-create-user-collection.png)

> [!div class="button"]
[下一步 >](confirm-dns.md)
