---
title: "配置 Endpoint Protection | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 Endpoint protection 选择和配置方法以便使反恶意软件定义在客户端计算机上保持最新状态。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b5da7900a4f8e2f330c4dcb2cac00b45099bd909
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-definition-updates-for-endpoint-protection"></a>为 Endpoint Protection 配置定义更新  

*适用范围：System Center Configuration Manager (Current Branch)*

 通过 System Center Configuration Manager 中的 Endpoint Protection，你可以使用若干可用方法中的任何方法使反恶意软件定义在层次结构中的客户端计算机上保持最新。 本主题中的信息可以帮助你选择和配置这些方法。

 若要更新反恶意软件定义，可以使用以下方法中的一种或多种：

-   [从 Configuration Manager 中分发的更新](endpoint-definitions-configmgr.md) - 此方法使用 Configuration Manager 软件更新将定义和引擎更新传送到层次结构中的计算机。

-   [从 Windows Server Update Services (WSUS) 分发的更新](endpoint-definitions-wsus.md) - 此方法使用 WSUS 基础结构将定义和引擎更新传送到计算机。

-   [从 Microsoft 更新分发的更新](endpoint-definitions-microsoft-updates.md) - 此方法允许计算机直接连接到 Microsoft 更新以下载定义和引擎更新。 对于不经常连接到企业网络的计算机，此方法会很有用。

-   [从 Microsoft 恶意软件防护中心分发的更新](endpoint-definitions-protection-center.md) - 此方法将从 Microsoft 恶意软件防护中心下载定义更新。

-   [来自 UNC 文件共享的更新](endpoint-definitions-network.md) - 使用此方法，你可以将最新的定义和引擎更新保存到网络共享上。 然后客户端便可访问网络以安装更新。

 你可以配置多个定义更新源，并控制对其进行评估和应用的顺序。 将在创建反恶意软件策略时，在“配置定义更新源”  对话框中完成此操作。

> [!IMPORTANT]
>  对于 Windows 10 电脑，必须配置 Endpoint Protection 以更新 Windows Defender 的恶意软件定义。

## <a name="how-to-configure-definition-update-sources"></a>如何配置定义更新源
 使用以下过程配置要用于每个反恶意软件策略的定义更新源。

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。

2.  在“资产和符合性”  工作区中，展开“Endpoint Protection” ，然后单击“反恶意软件策略” 。

3.  打开“默认反恶意软件策略”  的属性页，或创建新的反恶意软件策略。 有关如何创建反恶意软件策略的详细信息，请参阅[如何在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。

4.  在反恶意软件属性对话框的“定义更新”  部分中，单击“设置源” 。

5.  在“配置定义更新源”  对话框中，选择要用于定义更新的源。 可以单击“向上”  或“向下”  来修改使用这些源的顺序。

6.  单击“确定”  以关闭“配置定义更新源”  对话框。

## <a name="configure-endpoint-protection-definitions"></a>配置 Endpoint Protection 定义

-   [从 Configuration Manager 中分发的更新](endpoint-definitions-configmgr.md) - 此方法使用 Configuration Manager 软件更新将定义和引擎更新传送到层次结构中的计算机。

-   [从 Windows Server Update Services (WSUS) 分发的更新](endpoint-definitions-wsus.md) - 此方法使用 WSUS 基础结构将定义和引擎更新传送到计算机。

-   [从 Microsoft 更新分发的更新](endpoint-definitions-microsoft-updates.md) - 此方法允许计算机直接连接到 Microsoft 更新以下载定义和引擎更新。 对于不经常连接到企业网络的计算机，此方法会很有用。

-   从 Microsoft 恶意软件防护中心分发的更新 - 此方法将从 Microsoft 恶意软件防护中心下载定义更新。

-   [来自 UNC 文件共享的更新](endpoint-definitions-network.md) - 使用此方法，你可以将最新的定义和引擎更新保存到网络共享上。 然后客户端便可访问网络以安装更新。
