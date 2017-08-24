---
title: "网络共享中的 Endpoint Protection 恶意软件定义 | Microsoft Docs"
description: "了解如何从 Microsoft 手动下载最新定义更新，然后将客户端配置为下载这些定义。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 110bd9a9d04b27ef6794145fae66dbd910308bdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>启用 Endpoint Protection 恶意软件定义，以便从网络共享为 Configuration Manager 下载定义

*适用范围：System Center Configuration Manager (Current Branch)*

 你可以手动从 Microsoft 下载最新定义更新，然后将客户端配置为从网络上的共享文件夹下载这些定义。 用户还可以在你使用此更新源时启动定义更新。

> [!NOTE]
>  客户端必须具有对共享文件夹的读取访问权限，才能够下载定义更新。

 有关如何下载要存储在文件共享上的定义和引擎更新的详细信息，请参阅[安装最新的 Microsoft 反恶意软件和反间谍软件](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx)。

## <a name="to-configure-definition-downloads-from-a-file-share"></a>若要从文件共享配置定义下载

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。

2.  在“资产和符合性”  工作区中，展开“Endpoint Protection” ，然后单击“反恶意软件策略” 。

3.  打开“默认反恶意软件策略”  的属性页，或创建新的反恶意软件策略。 有关如何创建反恶意软件策略的详细信息，请参阅[如何在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。

4.  在反恶意软件属性对话框的“定义更新”  部分中，单击“设置源” 。

5.  在“配置定义更新源”  对话框中，选择“来自 UNC 文件共享的更新” 。

6.  单击“确定”  以关闭“配置定义更新源”  对话框。

7.  单击“设置路径” 。 然后，在“配置定义更新 UNC 路径”  对话框中，添加一个或多个指向网络共享上定义更新文件位置的 UNC 路径。

8.  单击“确定”  以关闭“配置定义更新 UNC 路径”  对话框。


> [!div class="button"]
[下一步 >](endpoint-antimalware-policies.md)

> [!div class="button"]
[返回 >](endpoint-configure-alerts.md)
