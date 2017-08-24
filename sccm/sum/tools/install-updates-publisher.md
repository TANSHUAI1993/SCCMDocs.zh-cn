---
title: "安装 Updates Publisher | Microsoft Docs"
description: "在环境中安装 System Center Updates Publisher"
ms.custom: na
ms.date: 07/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 5c95a8b99b91531773392a77d25377465079b070
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-updates-publisher"></a>安装 Updates Publisher

*适用范围：System Center Updates Publisher*

本主题介绍了如何获取、安装和设置 Updates Publisher，以便在环境中使用。


## <a name="prerequisites-and-limitations"></a>先决条件和限制
下面各部分详细介绍了 Updates Publisher 的安装和使用要求，以及使用限制或已知问题。

### <a name="operating-systems"></a>操作系统
在以下版本的 64 位操作系统上安装和运行 Updates Publisher。 没有最低累积更新或 Service Pack 要求。

-   Windows Server 2016（Standard、Datacenter）
-   Windows Server 2012 R2（Standard、Datacenter）
-   Windows 10（专业版、教育版、专业教育版、企业版）
-   Windows 8.1（专业版、企业版）

### <a name="prerequisites"></a>先决条件
运行 Updates Publisher 的计算机必须满足以下要求：

-   **64 位操作系统**：安装 Updates Publisher 的计算机必须运行 64 位操作系统。
-   **WSUS 4.0 或更高版本**：
    -   为了满足此要求，在 Windows Server 上，安装默认的管理控制台。
    -   对于 Windows 10 和 Windows 8.1，安装[适用于 Windows 操作系统的远程服务器管理工具 (RSAT)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)。 这会安装使用 Updates Publisher 所必需的支持（*API 和 PowerShell cmdlet* 以及*用户界面管理控制台*）。
-   **权限**：
    -   安装：本地管理员
    -   大多数操作：本地用户
    -   发布或涉及 WSUS 的操作：WSUS 服务器上 WSUS 管理员组的成员。

### <a name="supported-languages"></a>支持的语言
虽然 Updates Publisher 目前只有英文版，但也可以管理其他语言的更新。 语言支持因任务（如发布、创建或编辑更新）而异。

导出或发布更新时，Updates Publisher 会根据安装 Updates Publisher 的计算机的区域设置显示软件更新的标题和说明。

例如，假设创建的软件更新具有英语和西班牙语标题。

-   如果在默认区域设置为英语的计算机上创建此更新，那么标题和说明会以英语显示。
-   然后，如果将此更新导出或发布到区域设置为西班牙语的计算机上，那么相应计算机会以西班牙语显示标题和说明。

### <a name="publishing"></a>发布
发布软件更新时，可以指定软件更新二进制文件的语言。 还可以为二进制文件指定中性语言。 支持以下语言：

-   阿拉伯语
-   中文（香港特别行政区）
-   和 SharePoint 2010 显示的“中文(繁体)”
-   中文（简体）
-   捷克语
-   丹麦语
-   荷兰语
-   英语
-   芬兰语
-   法语
-   德语
-   希腊语
-   希伯来语
-   匈牙利语
-   意大利语
-   日语
-   朝鲜语
-   挪威语
-   波兰语
-   葡萄牙语
-   葡萄牙语（巴西）
-   俄语
-   西班牙语
-   瑞典语
-   土耳其语

### <a name="software-update-titles-and-descriptions"></a>软件更新标题和说明
软件更新的标题和说明支持以下语言。

-   和 SharePoint 2010 显示的“中文(繁体)”
-   中文（简体）
-   英语
-   法语
-   德语
-   意大利语
-   日语
-   朝鲜语
-   葡萄牙语（巴西）
-   俄语
-   西班牙语



## <a name="install-updates-publisher"></a>安装 Updates Publisher
从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=847967)获取用于安装 System Center Updates Publisher 的 **UpdatesPubliser.msi**。

若要安装 Updates Publisher，在满足*先决条件*的计算机上运行 **UpdatesPublisher.msi**。 安装程序会创建以下文件夹，以包含运行 Updates Publisher 所必需的文件：*&lt;path&gt;\Program Files\Microsoft\UpdatesPublisher*。

因为此文件夹包含使用 Updates Publisher 所必需的全部文件，所以可以将此文件夹及其内容复制到新的位置或计算机中，然后从相应位置使用 Updates Publisher。 不过，新的位置或计算机必须满足运行 Updates Publisher 的先决条件。

安装完成后，运行“UpdatesPublisher”文件夹中的 **UpdatesPublisher.exe**，启动 Updates Publisher。

## <a name="next-steps"></a>后续步骤
 安装 Updates Publisher 后，我们建议为 Updates Publisher [配置选项](updates-publisher-options.md)。 必须先配置一些选项，然后才能使用 Updates Publisher 的一些功能。

 不过，如果要使用默认功能，并且不打算将更新部署到更新服务器或受管理设备，可以直接跳到[管理软件更新目录](updates-publisher-catalogs.md)或[创建软件更新](create-updates-with-updates-publisher.md)，创建你自己的更新目录。

