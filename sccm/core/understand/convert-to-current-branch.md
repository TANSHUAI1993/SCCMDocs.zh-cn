---
title: "将 Long-Term Servicing Branch 升级到 Current Branch | Microsoft Docs"
description: "了解如何将 Long-Term Servicing Branch 站点转换为 Current Branch 站点。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6e7edc85630d22c5bbba1ff66bd1199903db76db
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>将 Long-Term Servicing Branch 升级到 Current Branch

*适用范围：System Center Configuration Manager (Long-Term Servicing Branch)*

请参阅本主题以了解如何将运行 Configuration Manager 的 Long-Term Servicing Branch (LTSB) 的站点和层次结构升级（转换）为 Current Branch。

如果具有授予 Current Branch 使用权的当前软件保障协议（或类似的许可权），则可以将安装从 LTSB 转换到 Current Branch。  这是一种单向转换，因为不支持将 Current Branch 站点转换为 LTSB。

如果拥有多个站点，则只需转换层次结构的顶层站点。 在转换顶层站点后：
- 子主站点也会自动进行转换。
-   必须从 Configuration Manager 控制台中手动更新辅助站点。

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>运行安装程序转换 Long-Term Servicing Branch
在层次结构的顶层站点上，可以从合格的基线媒体运行 Configuration Manager 安装程序并选择“站点维护”。  然后当授权页出现时，为 Current Branch 选择选项并完成向导。

站点转换为 Current Branch 后，可以使用以前不可用的功能。

> [!NOTE]  
> 合格的基线媒体是具有等于或高于 LTSB 安装版本的媒体。

例如：因为 LTSB 基于版本 1606，因此不能使用基线 1511 媒体将其转换为 Current Branch。 而是需要从用于安装 LTSB 站点的相同的基线媒体 1606 版本中运行安装程序，然后为 Current Branch 选择授权选项。  或者，如果已发布了 Current Branch 更高的基线版本，则可以从该基线媒体运行安装程序。

关于基线版本的列表，请参阅 **Configuration Manager 的更新**中的[基线和更新版本](/sccm/core/servers/manage/updates)。

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>使用 Configuration Manager 控制台转换 Long-Term Servicing Branch
如果站点运行 LTSB，则可以使用 Configuration Manager 控制台中的以下选项将站点转换为 Current Branch：

 1. 在控制台中，转到“管理” > “站点配置” > “站点”，然后打开“层次结构设置”。  

 2. 选择选项将站点转换为 Current Branch，然后选择“应用”。  

站点转换为 Current Branch 后，可以使用以前不可用的功能。
