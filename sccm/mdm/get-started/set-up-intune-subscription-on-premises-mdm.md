---
title: "设置 Intune 订阅 | Microsoft Docs"
description: "在 System Center Configuration Manager 中为本地移动设备管理设置 Intune 订阅。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 5a81ec06e16992ae1c41b0fc98ebcd07386c5381
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中为本地移动设备管理设置 Microsoft Intune 订阅

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 本地移动设备管理需要 Microsoft Intune 订阅来跟踪许可证。 Intune 服务不能用于管理设备或存储管理信息。 对于本地移动设备管理，所有设备管理均由 Configuration Manager 基础结构处理。  

> [!NOTE]  
> 从版本 1610 开始，Configuration Manager 支持同时使用 Microsoft Intune 和本地 Configuration Manager 基础结构来管理移动设备。   

> [!TIP]  
>  建议先设置本地移动设备管理的 Intune 订阅，然后再安装所需的站点系统角色，以最小化新安装站点系统角色开始正常运行所需的时间。  

##  <a name="sign-up-for-microsoft-intune"></a>注册 Microsoft Intune  
 需要 Intune 才能使本地移动设备管理正常运行。 只需针对试用或付费订阅进行[注册](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)，然后转到下一步，将订阅添加到 Configuration Manager。  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>将 Intune 订阅添加到 Configuration Manager  
 若要将订阅添加到 Configuration Manager，请按照使用 Intune 为移动设备管理添加订阅的相同基本步骤进行添加。 阅读以下有关特定差异的说明，然后使用[配置 Microsoft Intune 订阅](../deploy-use/configure-intune-subscription.md)中的指示。  

> [!NOTE]  
>  添加 Intune 订阅时，请记住以下内容：  
>   
>  -   添加 Microsoft Intune 订阅向导中指定的集合不用于本地移动设备管理用户权限委派。 仅用于通过 Intune 实现的移动设备管理。 但是，需要指定一个继续执行向导所需的集合。  
> -   对于本地移动设备管理，会忽略向导中指定的站点代码设置。 使用的站点代码是你在某个注册配置文件中指定的代码，该文件授予用户注册设备的权限。  
> -   请勿启用多重身份验证。 在本地移动设备管理中不受支持。  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>为本地移动设备管理配置 Intune 订阅  

1.  在 Configuration Manager 控制台中，右键单击“Microsoft Intune 订阅”，然后单击“属性”。  

2.  在“本地移动设备管理”框中，选择以下选项之一：

  - 如果计划只在本地管理设备，请单击“仅本地管理设备”旁边的复选框，然后单击“确定”。  

      > [!NOTE]  
      >  通过单击此复选框，将会配置 Intune 订阅以保留所有本地管理信息且不将数据复制到云中。  

    - 如果计划通过 Intune 和本地 Configuration Manager 管理设备，请保留此框处于未选中状态。

3.  如果打算管理 Windows 10 移动设备，请右键单击“Microsoft Intune 订阅” ，单击“配置平台” ，然后单击“Windows Phone”  。  

4.  单击“Windows Phone 8.1 和 Windows 10 移动版” 旁边的复选框，然后单击“确定” 。  

5.  如果打算管理 Windows 10 桌面计算机，请右键单击“Microsoft Intune 订阅” ，单击“配置平台” ，然后单击“启用Windows 注册” 。  

6.  单击“启用 Windows 注册” 旁边的复选框，然后单击“确定” 。  
