---
title: "自动将设备分类到集合 | Microsoft Docs"
description: "使用 System Center Configuration Manager 自动将设备分类到集合。"
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d1b79fb091a6ae4b967d63843ae7b45a0cbeb555
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自动将设备分类到集合

*适用范围：System Center Configuration Manager (Current Branch)*

可创建设备类别，可将其用于配合使用 Microsoft Intune 和 Configuration Manager 时自动在设备集合中放置设备。 然后用户在 Intune 中注册设备时需要选择某个设备类别。 可从 Configuration Manager 控制台中更改设备类别。

> [!IMPORTANT]  
    >  此功能适用于 **2016 年 6 月**及以后版本的 Microsoft Intune。 试用这些过程前，请确保已更新到此版本。

## <a name="create-device-categories"></a>创建设备类别

1.  转到“资产和符合性” > “概述” > “设备集合”。
2.  在“主页”选项卡上的“设备集合”组中，选择“管理设备类别”。
3.  创建、编辑或删除类别。

## <a name="associate-a-collection-with-a-device-category"></a>将集合与设备类别相关联

将集合与设备类别关联后，该类别中的所有设备都会添加到该集合。 无法将设备类别规则添加到内置集合（如“所有系统”）。

1.  在设备集合“属性”对话框的“成员身份规则”选项卡上，选择“添加规则” > “设备类别规则”。
2.  在“选择设备类别”对话框中，选择一个或多个设备类别，所选类别将应用到集合中的所有设备。

## <a name="change-the-category-of-a-device"></a>更改设备的类别

1.  在“资产和符合性” > “概述” > “设备”中，从“设备”列表中选择一个设备。
2.  在“主页”选项卡的“设备”组中，选择“更改类别”。
3.  选择一个类别，然后选择“确定”。

## <a name="view-which-category-a-device-belongs-to"></a>查看设备所属的类别

在“资产和符合性” > “概述” > “设备”中的“设备”列表中，此类别在“设备类别”列中显示。

如果“设备类别” 列未显示，请在“设备”列（如“名称”）中右键单击其中一个列标题，然后选择“设备类别”。

如果将某个设备分配到某个类别，随后又删除该类别，则“按用户在 Microsoft Intune 中注册的设备的列表”报表将在“设备类别”列显示 GUID，而不显示类别名称。
