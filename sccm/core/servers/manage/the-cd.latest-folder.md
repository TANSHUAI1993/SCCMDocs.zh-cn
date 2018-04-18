---
title: CD.Latest 文件夹
titleSuffix: Configuration Manager
description: 了解有关新的更新过程的详细信息，该过程会从 Configuration Manager 控制台内部将更新传递到产品。
ms.custom: na
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 86b6393a6719895357d34fe8e562f3d0c967ad06
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 CD.Latest 文件夹

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 引入一种新的更新过程，该过程会从 Configuration Manager 控制台内部将更新传递到产品。 为了支持这种更新 Configuration Manager 的新方法，创建了一个名为 **CD.Latest** 的新文件夹，其中包含用于站点的更新版本的 Configuration Manager 安装文件副本。  

CD.Latest 文件夹包含一个名为 Redist 的文件夹，该文件夹包含安装程序下载和使用的可再发行文件。 这些文件与在该 CD.Latest 文件夹中找到的 Configuration Manager 文件的版本相匹配。 当从 CD.Latest 文件夹运行安装程序时，必须使用与该安装程序的版本相匹配的文件。 为此，可以指示安装程序从 Microsoft 下载新文件和当前文件，或指示安装程序使用包含在 CD.Latest 文件夹中的 Redist 文件夹中的文件。

但基线媒体（例如 2018 年 3 月发布的 1802 基线版本）不包含 Redist 文件夹。 只有在安装控制台中更新后才会创建 Redist 文件夹。 同时，从基线媒体安装站点时，请使用所用 Redist 文件夹。  

> [!TIP]
> 请确保使用最新的可再发行文件。 如果最近没有下载可再发行文件，请计划允许安装程序从 Microsoft 执行该操作。   

 下面是在管理中心站点或主站点服务器上创建或更新 CD.Latest 文件夹的方案：  

-   从 Configuration Manager 控制台中安装更新或修补程序：在 Configuration Manager 安装文件夹中创建或更新该文件夹。  

-   运行内置 Configuration Manager 备份任务：在指定备份文件夹位置下创建或更新该文件夹。  

-  使用基线媒体（如 1802 版）安装新站点时，将会创建 CD.Latest 文件夹。

对于以下各项支出 CD.Latest 文件夹中的源文件：  

1.  **备份和恢复：**若要恢复站点，必须使用 CD.Latest 文件夹中与站点匹配的源文件。 使用内置站点备份任务运行站点备份时，CD.Latest 文件夹作为备份的一部分包括在内。

    -   **当你在站点恢复中重新安装站点时，** 会从包含在你的备份中的 CD.Latest 文件夹安装站点。 此操作会使用与你的站点备份和站点数据库匹配的文件版本安装站点。  如果你无权访问正确的 CD.Latest 文件夹版本，你可以通过在实验室环境中安装站点，然后更新该站点以匹配你要恢复的版本，获取一个带有正确文件版本的 CD.Latest 文件夹。

        > [!IMPORTANT]  
        >  如果你没有正确的可用 CD.Latest 文件夹及其内容，则无法恢复站点，必须重新安装它。  

    -   当你没有 CD.Latest 文件夹，但是具有正常运行的子主站点或管理中心站点时，可以将该站点用作站点恢复的引用站点。  

2.  **安装子主站点：** 要在安装了一个或多个控制台内部更新的管理中心站点下安装新的子主站点，必须使用来自管理中心站点的 CD.Latest 文件夹中的安装程序和源文件。 安装程序从来自管理中心站点的 CD.Latest 文件夹副本运行时，它使用与管理中心站点版本匹配的安装源文件。 有关详细信息，请参阅[使用安装向导来安装站点](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)。  

3.  **扩展独立主站点：** 要通过安装新的管理中心站点来扩展独立主站点时，必须使用来自主站点的 CD.Latest 文件夹中的安装程序和源文件来安装新的管理中心站点。 从来自主站点的 CD.Latest 文件夹副本运行时，它使用与主站点版本匹配的安装源文件。 有关详细信息，请参阅[使用安装向导来安装站点](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)中的[扩展独立主站点](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand))

> [!IMPORTANT]  
>  对于以下各项不支持更新后的 CD.Latest 源文件：  
>   
>  -   为新层次结构安装新站点  
>  -   将 Microsoft System Center 2012 Configuration Manager 站点升级到 System Center Configuration Manager
>  -   安装 Configuration Manager 客户端
>  -   安装 Configuration Manager 管理控制台

