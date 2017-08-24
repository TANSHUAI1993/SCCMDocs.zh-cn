---
title: "创建 iOS 应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 iOS 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 349fcf335e7faddbcbd2ffe0ece7e711465f28df
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 iOS 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 应用程序具有一个或多个部署类型，这些是将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。  

 可以使用下列方法创建应用程序：  

-   通过读取应用程序安装文件来自动创建应用程序和部署类型。  

-   手动创建应用程序并稍后添加部署类型。  

-   从文件导入应用程序。  

请参阅[启动创建应用程序向导](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)，了解创建 Configuration Manager 应用程序和部署类型所需的步骤。 此外，创建和部署适用于 iOS 设备的应用程序时，请记住以下注意事项。  

## <a name="general-considerations"></a>一般注意事项  
 Configuration Manager 支持以下应用类型的部署：  

|设备类型|受支持的文件|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> 在 System Center Configuration Manager 中，不需要在导入 iOS 应用时指定属性列表 (.plist) 文件。|  

 支持以下部署操作：  

|设备类型|支持的操作|  
|-----------------|-----------------------|  
|iOS|**可用**、**必需**。 用户必须同意安装和卸载。

> [!IMPORTANT]  
>  目前，最终用户无法从 iOS 的 Microsoft Intune 公司门户应用程序中安装公司应用程序。 这是由于 iOS 应用商店中发布的应用受到限制（请参阅应用商店查看准则，第 2 部分）。 用户可通过浏览到 Intune Web 门户 (portal.manage.microsoft.com) 在其设备上安装企业应用（包括托管的应用商店应用和业务线应用包）。 若要深入了解由 Intune 公司门户应用启用的移动管理功能，请参阅 [Enrolled device management capabilities in Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx)（Microsoft Intune 中的注册设备管理功能）。  
