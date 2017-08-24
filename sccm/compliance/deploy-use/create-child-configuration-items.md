---
title: "创建子配置项目 | Microsoft Docs"
description: "在 System Center Configuration Manager 中创建子配置项目。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 33d4a2d5a09af74e1d76ac9b34a42b749f5bf7ef
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建子配置项目

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的子配置项目是与原始配置项目保持关系的配置项目的副本，因为它们从父配置项目继承原始配置。  

在 Configuration Manager 控制台中查看子配置项目的属性时，无法通过所继承的对象和设置的验证条件对其进行编辑。 但是，您可以将其他验证条件添加到子配置项目并进行编辑，也可以向子配置项目添加新的对象和设置。
创建和编辑子配置项目的通常目的在于完善原始配置项目以满足业务要求。  

> [!NOTE]  
>  只能从类型为“Windows 台式机和服务器(自定义)” 的配置项目创建子配置项目。  

## <a name="to-create-a-child-configuration-item"></a>创建子配置项目  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “配置项目”。  

3.  在“配置项目”  列表中，选择要为其创建子配置项目的配置项目，然后在“主页”  选项卡上的“配置项目”  组中，单击“创建子配置项目” 。  

4.  在“创建子配置项目向导”  的“常规” 页上，可以选择要用于创建子级的父配置项目的特定修订版本。 此向导中的其他步骤与用于创建标准配置项目的步骤相同。 有关详细信息，请参阅 [How to create custom configuration items for Windows desktop and server computers](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)（如何为 Windows 台式机和服务器计算机创建自定义配置项目）。  

5.  完成向导。 新的子配置项目会显示在“配置项目”  列表中。  
