---
title: "自动将设备分类到集合 | Microsoft Docs"
description: "使用 System Center Configuration Manager 自动将设备分类到集合。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: d5ef7260bcc2ab9cc56d8fed530a406aa1045c5a

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自动将设备分类到集合

*适用范围：System Center Configuration Manager (Current Branch)*

可创建设备类别，可将其用于配合使用 Microsoft Intune 和 Configuration Manager 时自动在设备集合中放置设备。 然后要求用户在 Intune 中注册设备时选择某个设备类别。 此外，还可以从 Configuration Manager 控制台中更改设备的类别。

> [!IMPORTANT]  
    >  此功能适用于 **2016 年 6 月**版本的 Microsoft Intune。 试用这些过程前，请确保已更新到此版本。

## <a name="create-device-categories"></a>创建设备类别

1.  在 Configuration Manager 控制台的“资产和符合性”工作区中，展开“概述”，然后单击“设备集合”。
2.  在“主页”选项卡上的“设备集合”组中，单击“管理设备类别”。
3.  在“管理设备类别”对话框中，可以创建、编辑或删除类别。

## <a name="associate-a-collection-with-a-device-category"></a>将集合与设备类别相关联

将集合与设备类别关联后，指定的分类中的所有设备都会添加到该集合。

> [!IMPORTANT]  
    >  无法将设备类别规则添加到内置集合（如“所有系统”）。

1.  在设备集合“属性” 对话框的“成员身份规则”选项卡上，单击“添加规则” > “设备类别规则”。
2.  在“选择设备类别”对话框中，选择一个或多个设备类别，所选类别将应用到集合中的所有设备。
3.  关闭“选择设备类别”对话框和集合属性对话框。


## <a name="change-the-category-of-a-device"></a>更改设备的类别

1.  在 Configuration Manager 控制台的“资产和符合性”工作区中，展开“概述”，然后单击“设备”。
2.  从“设备”列表选择一个设备，然后在“主页”选项卡上的“设备”组中，单击“更改类别”。
3.  在“编辑设备类别”对话框框中，选择将应用于此设备的类别，然后单击“确定”。

## <a name="view-which-category-a-device-belongs-to"></a>查看设备所属的类别

1.  在 Configuration Manager 控制台的“资产和符合性”工作区中，扩展“概述”，然后单击“设备”。
2.  在“设备”列表中，此类别显示在“设备类别”列。
> [!TIP]  
    >  如果“设备类别” 列未显示，请在“设备”列（如“名称”）中右键单击其中一个列标题，然后选择“设备类别”。

如果将某个设备分配到某个类别，随后又删除该类别，则“按用户在 Microsoft Intune 中注册的设备的列表”报表将在“设备类别”列显示 GUID，而不显示类别名称。



<!--HONumber=Dec16_HO3-->


