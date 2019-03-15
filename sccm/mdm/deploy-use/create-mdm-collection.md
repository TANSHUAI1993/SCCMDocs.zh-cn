---
title: 创建 MDM 集合
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager 创建 MDM 集合。
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ec7c4cd58fbb717ab586d355ba4f0bf5f91fd06
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881650"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 创建 MDM 集合

适用范围：System Center Configuration Manager (Current Branch)

需要 Configuration Manager 用户集合以指定可以向管理中注册设备的用户。 由于 Intune 许可证由用户进行分配，所以只能使用用户集合（而非设备集合）。

> [!NOTE]
> 若要注册使用 Intune 的设备，你不必将许可证分配给 Microsoft 365 管理中心或 Azure Active Directory 门户中的用户。 只需在与 Intune 订阅（在一个[后续步骤](configure-intune-subscription.md)中）关联的集合中包括用户即可。

为进行测试，可以设置**直接规则**并添加可以注册设备的特定用户。 在 Configuration Manager 控制台中，选择“资产和符合性” > “用户集合”，单击“主页”选项卡 >“创建”组，然后单击“创建用户集合”。 若要实现更广泛的分发，应使用**查询规则**定义用户。 有关集合的详细信息，请参阅[如何创建集合](https://technet.microsoft.com/library/mt629371.aspx)。

![为 MDM 创建用户集合](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [下一步 >](confirm-dns.md)
