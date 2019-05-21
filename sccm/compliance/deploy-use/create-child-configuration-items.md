---
title: 创建子配置项目
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中创建子配置项目。
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b88ee7eaac8df8ffce93937f3a3f2616b9e085b
ms.sourcegitcommit: 417e3834a42b415a8e129327dd3c15cc0c7ec5a2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65443155"
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建子配置项目

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的子配置项目是与原始配置项目保持关系的配置项目的副本，因为它们从父配置项目继承原始配置。  

在 Configuration Manager 控制台中查看子配置项目的属性时，无法通过所继承的对象和设置的验证条件对其进行编辑。 但是，您可以将其他验证条件添加到子配置项目并进行编辑，也可以向子配置项目添加新的对象和设置。
例如，创建和编辑子配置项目可以完善原始配置项目以满足业务要求。  

> [!NOTE]  
>  只能从类型为“Windows 台式机和服务器(自定义)” 的配置项目创建子配置项目。  

## <a name="to-create-a-child-configuration-item"></a>创建子配置项目  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置项目”。  

3.  在“配置项目”  列表中，选择要为其创建子配置项目的配置项目，然后在“主页”  选项卡上的“配置项目”  组中，单击“创建子配置项目” 。  

4.  在“创建子配置项目向导”  的“常规” 页上，可以选择要用于创建子级的父配置项目的特定修订版本。 此向导中的其他步骤与用于创建标准配置项目的步骤相同。 有关详细信息，请参阅 [How to create custom configuration items for Windows desktop and server computers](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)（如何为 Windows 台式机和服务器计算机创建自定义配置项目）。  

5.  完成向导。 新的子配置项目会显示在“配置项目”  列表中。  
