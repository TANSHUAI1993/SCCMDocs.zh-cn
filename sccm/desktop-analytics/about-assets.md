---
title: 在桌面 Analytics 中的资产
titleSuffix: Configuration Manager
description: 了解有关设备、 应用、 Office 应用、 Office 加载项和桌面 Analytics 中的 Office 宏。
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 149c5f2a4469a353c6dce6fde86527ca95518484
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62254636"
---
# <a name="assets-in-desktop-analytics"></a>在桌面 Analytics 中的资产 

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

设备到桌面 Analytics 报告数据后，它提供了以下资产的清单：
- 设备  
- 硬件驱动程序  
- 已安装的应用  
- Office 应用程序  
- Office 加载项  
- Office 宏  

在服务门户中，选择**资产**Desktop 分析菜单中。


## <a name="devices"></a>设备

**设备**选项卡显示注册到 Desktop 分析在组织中的所有设备有关的关键信息。 您可以对任何列或筛选器的特定值进行排序。

> [!NOTE]  
> 如果仪表板并不报告的设备数预期为您的环境，请参阅[Desktop 分析故障排除](/sccm/desktop-analytics/troubleshooting)。  



## <a name="apps"></a>应用

**应用**选项卡上显示所有安装应用程序在 Windows 设备上检测到该服务。

**值得注意**超过 2%的已注册的设备上安装应用。 <!--You can change the threshold of "noteworthy" by {doing something}.--> 

配置**重要性**的应用程序通过设置以下类别之一：

- 严重
- 重要
- 忽略
- 未检查

从列表中，选择应用，并选择**编辑**。 此操作将显示应用详细信息。 选择**重要性**下拉列表菜单，然后设置的值。 你还可以分配**所有者**。 如果您进行任何更改，则选择**保存**。 


## <a name="office-apps"></a>Office 应用程序

**Office 应用**选项卡是类似于应用选项卡。它只显示应用程序，例如 Microsoft Word 或 Excel，并没有分类或值得注意的内容计数。 为与其他应用相同的方式设置的重要性和 Office 应用程序的所有者。


## <a name="office-add-ins"></a>Office 加载项

**Office 加载项**选项卡显示支持工具，例如，Microsoft Azure 信息保护或分析工具库。 此选项卡是类似于应用选项卡，并包括值得一提的计数。 与应用程序设置的重要性和所有者。 


## <a name="office-macros"></a>Office 宏

**Office 宏**选项卡显示的任何设备是否具有最近访问可以包含宏的任何文件。 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> 如果还使用[使用的 Readiness Toolkit](https://aka.ms/readinesstoolkit)对于 Office 加载项和 Visual Basic for Applications (VBA) 宏，此选项卡还显示从这些设备的其他数据。 
> 
> 不需要使用的 Readiness Toolkit 使用 Desktop 分析。  



## <a name="next-steps"></a>后续步骤

- [了解桌面分析部署计划](/sccm/desktop-analytics/about-deployment-plans)  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

