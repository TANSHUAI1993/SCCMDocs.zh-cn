---
title: "设置 Intune 订阅 | 本地 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中为本地移动设备管理设置 Intune 订阅。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4daf5d6ea30aa1fb4aa189ef6da9b364fe197805


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中为本地移动设备管理设置 Microsoft Intune 订阅

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 本地移动设备管理需要 Microsoft Intune 订阅来跟踪许可证。 Intune 服务不能用于管理设备或存储管理信息。 对于本地移动设备管理，所有设备管理均由 Configuration Manager 基础结构处理。  

> [!IMPORTANT]  
>  Configuration Manager 不支持同时将 Microsoft Intune 和本地 Configuration Manager 基础结构作为管理机构使用。 因此，设置 Intune 订阅以用于本地管理时，实际上禁用了 Intune 管理。  

 将 Intune 服务设置为使用本地移动设备涉及以下高级步骤：  

-   [注册 Microsoft Intune](#bkmk_signup)  

-   [将 Intune 订阅添加到 Configuration Manager](#bkmk_addSub)  

-   [为本地移动设备管理配置 Intune 订阅](#bkmk_configure)  

> [!TIP]  
>  建议先设置本地移动设备管理的 Intune 订阅，然后再安装所需的站点系统角色，以最小化新安装站点系统角色开始正常运行所需的时间。  

##  <a name="a-namebkmksignupa-sign-up-for-microsoft-intune"></a><a name="bkmk_signup"></a> 注册 Microsoft Intune  
 需要 Intune 才能使本地移动设备管理正常运行。 只需针对试用或付费订阅进行[注册](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)，然后转到下一步，将订阅添加到 Configuration Manager。  

##  <a name="a-namebkmkaddsuba-add-the-intune-subscription-to-configuration-manager"></a><a name="bkmk_addSub"></a> 将 Intune 订阅添加到 Configuration Manager  
 若要将订阅添加到 Configuration Manager，请按照使用 Intune 为移动设备管理添加订阅的相同基本步骤进行添加。 阅读以下说明以了解具体差异，然后使用[使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)](../../mdm/plan-design/hybrid-mobile-device-management.md) 中[创建 Microsoft Intune 订阅](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_subscription)中的说明。  

> [!NOTE]  
>  添加 Intune 订阅时，请记住以下内容：  
>   
>  -   添加 Microsoft Intune 订阅向导中指定的集合不用于本地移动设备管理用户权限委派。 仅用于通过 Intune 实现的移动设备管理。 但是，需要指定一个继续执行向导所需的集合。  
> -   对于本地移动设备管理，会忽略向导中指定的站点代码设置。 使用的站点代码是你在某个注册配置文件中指定的代码，该文件授予用户注册设备的权限。  
> -   请勿启用多重身份验证。 在本地移动设备管理中不受支持。  

##  <a name="a-namebkmkconfigurea-configure-the-intune-subscription-for-on-premises-mobile-device-management"></a><a name="bkmk_configure"></a> 为本地移动设备管理配置 Intune 订阅  

1.  在 Configuration Manager 控制台中，右键单击“Microsoft Intune 订阅”，然后单击“属性”。  

2.  在“本地移动设备管理”框中，单击“仅管理本地设备” 旁边的复选框，然后单击“确定” 。  

    > [!NOTE]  
    >  通过单击此复选框，将会配置 Intune 订阅以保留所有本地管理信息且不将数据复制到云中。  

3.  如果打算管理 Windows 10 移动设备，请右键单击“Microsoft Intune 订阅” ，单击“配置平台” ，然后单击“Windows Phone”  。  

4.  单击“Windows Phone 8.1 和 Windows 10 移动版” 旁边的复选框，然后单击“确定” 。  

5.  如果打算管理 Windows 10 桌面计算机，请右键单击“Microsoft Intune 订阅” ，单击“配置平台” ，然后单击“启用Windows 注册” 。  

6.  单击“启用 Windows 注册” 旁边的复选框，然后单击“确定” 。  



<!--HONumber=Nov16_HO1-->


