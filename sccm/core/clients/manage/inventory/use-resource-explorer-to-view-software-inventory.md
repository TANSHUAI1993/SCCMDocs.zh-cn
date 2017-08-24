---
title: "查看软件清单 | Microsoft Docs | 资源浏览器"
description: "使用资源浏览器查看 System Center Configuration Manager 中的软件清单。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b76bcf65c61b0a2690a468d375ac95b1334d5298
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>如何使用资源浏览器来查看 System Center Configuration Manager 中的软件清单

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的资源浏览器查看从层次结构中的计算机收集的软件清单的相关信息。  

> [!NOTE]  
>  在客户端上运行软件清单周期后，资源浏览器才会显示清单数据。  

 资源浏览器提供下列软件清单信息：  

-   **软件**：  

    -   **收集的文件** - 在软件清单期间所收集的文件。  

    -   **文件详细信息** - 在软件清单期间清点的与特定产品或制造商无关的文件。  

    -   **上次软件扫描** - 客户端计算机上最后一次软件清单和文件收集的日期和时间。  

    -   **产品详细信息** - 由软件清单清点的按制造商分组的软件产品。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>若要从 Configuration Manager 控制台运行资源浏览器  

1.  在 Configuration Manager 控制台中，选择“资产和符合性”

2.  在“资产和符合性”工作区中，选择“设备”或打开显示设备的任何集合。  

3.  选择包含想要查看的清单的计算机，然后在“主页”选项卡 >“设备”组中，选择“启动” > “资源浏览器”。

4.  可以右键单击“资源浏览器”窗口右窗格中的任意项，然后选择“属性”，以可读性更强的格式查看收集的清单信息。  
 
