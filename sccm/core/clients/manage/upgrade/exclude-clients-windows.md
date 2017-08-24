---
title: "排除客户端升级 | Windows | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中排除 Windows 客户端的升级。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: de5602179f3ac55b51133b8280a0143f1b0ff30e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中排除升级 Windows 计算机的客户端

*适用范围：System Center Configuration Manager (Current Branch)*

从版本 1610 开始，可排除客户端集合，使其不会自动安装更新的客户端版本。 这适用于自动升级以及其他方法，例如基于软件更新的升级、登录脚本和组策略。 可将其用于在升级客户端时需特别注意的计算机集合。 排除集合中的客户端会忽略安装更新客户端软件的请求。

## <a name="configure-exclusion-for-automatic-upgrades"></a>配置自动升级排除

1. 在 Configuration Manager 控制台中，转到“管理” > “站点配置” > “站点”，然后单击“层次结构设置”。

2. 单击“客户端升级”选项卡。

3. 单击“从升级中排除指定的客户端”复选框，然后选中“排除集合”，然后选择要排除的集合。 只能选择排除单个集合。

4.  单击“确定”以关闭并保存配置。 然后，客户端更新策略后，排除集合中的客户端将不再自动安装客户端软件更新。 有关详细信息，请参阅[如何升级 Windows 计算机的客户端](upgrade-clients-for-windows-computers.md)。

![用于自动升级排除的设置](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>尽管用户界面声明无法通过任何方法升级客户端，但仍有两种方法可用于替代这些设置。 可使用客户端请求安装和手动客户端安装替代此配置。 有关更多详细信息，请参阅以下部分。

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>如何升级排除集合中的客户端

只要某个集合被配置为排除，则只能通过上述两种方法中的一种来升级集合成员的客户端软件，它会替代排除设置：
 - **客户端请求安装** – 可以使用“客户端请求安装”来升级排除集合中的客户端。 由于该操作被视为管理员的意图，因此可以此升级客户端，而无需将整个集合从排除设置中删除。       

 - **手动客户端安装** – 可以手动升级排除集合中的客户端，方法是结合使用后列命令行开关和 ccmsetup：***/ignoreskipupgrade***

  如果尝试在不使用此开关的情况下手动升级排除集合中的客户端，客户端将不会安装新的客户端软件。 有关详细信息，请参阅[如何手动安装 Configuration Manager 客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)。

有关客户端安装方法的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。
