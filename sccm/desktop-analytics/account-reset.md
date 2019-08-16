---
title: 如何重置帐户
titleSuffix: Configuration Manager
description: 了解如何重置桌面分析帐户。
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3eb3f08c7c1358343b4bf06aef80ba84a5fb8d8c
ms.sourcegitcommit: 2b07fb7e2a17b5624429e81f9b6b9b3223b6f16d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69536776"
---
# <a name="how-to-reset-your-account"></a>如何重置帐户

<!-- 3733897 -->

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

如果你在环境中设置了桌面分析, 但想要重新开始使用载入和注册, 请使用此过程来重置你的帐户。

## <a name="prerequisites"></a>先决条件

只有**全局管理员**才能重置 Azure 门户中的帐户。

## <a name="behaviors"></a>Behaviors

- 此过程不会更改任何现有 Azure AD 用户、应用或权限

- 如果选择添加新的工作区, 则不会保留资产上的以下任何用户输入:
    - 重要性
    - Owner
    - 升级决策
    - 修正说明

## <a name="process"></a>过程

1. 以具有**全局管理员**角色的用户身份在 Microsoft 365 设备管理 "中打开[桌面分析门户](https://aka.ms/desktopanalytics)。

1. 在**全局设置**菜单中, 选择 "**连接的服务**"。 在 "注册设备" 部分, 选择要**重置**的选项。

1. 如果你决定继续, 你的帐户将被重置。 需要重新设置桌面分析。

## <a name="next-steps"></a>后续步骤

重置后, 刷新页面, 然后重新运行载入过程。 有关详细信息, 请参阅[如何设置桌面分析](/sccm/desktop-analytics/set-up)。

如果在此过程中遇到任何问题, 请与 Microsoft 支持部门联系以获得进一步的帮助。
