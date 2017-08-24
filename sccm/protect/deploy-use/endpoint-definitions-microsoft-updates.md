---
title: "网络共享中的 Endpoint Protection 恶意软件定义 | Microsoft Docs"
description: "了解如何可以实现从 Microsoft 更新为 Configuration Manager 下载 Endpoint Protection 的恶意软件定义。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 58c468fc3d4427cc1f2a8f197ab784a767151203
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>实现从 Microsoft 更新为 Configuration Manager 下载 Endpoint Protection 恶意软件定义

*适用范围：System Center Configuration Manager (Current Branch)*


 当你选择从 Microsoft 更新下载定义更新时，客户端将按照反恶意软件策略对话框的“定义更新”  部分中定义的间隔检查 Microsoft 更新网站。

 当客户端不具有到 Configuration Manager 站点的连接或当你希望用户能够启动定义更新时，此方法会很有用。

> [!IMPORTANT]
>  客户端必须在 Internet 上具有对 Microsoft 更新的访问权限，才能够使用此方法下载定义更新。

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>使用 Microsoft 恶意软件防护中心下载定义
 你可以将客户端配置为从 Microsoft 恶意软件防护中心下载定义更新。 如果 Endpoint Protection 客户端未能够从另一源下载更新，则使用此选项下载定义更新。 如果 Configuration Manager 基础结构存在阻止更新交付的问题，此更新方法会很有用。

> [!IMPORTANT]
>  客户端必须在 Internet 上具有对 Microsoft 更新的访问权限，才能够使用此方法下载定义更新。


> [!div class="button"]
[下一步 >](endpoint-antimalware-policies.md)

> [!div class="button"]
[返回 >](endpoint-configure-alerts.md)
