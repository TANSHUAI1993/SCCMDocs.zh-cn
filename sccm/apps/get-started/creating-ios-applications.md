---
title: "创建 iOS 应用程序 | System Center Configuration Manager"
description: "请参阅创建和部署适用于 iOS 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c3845635846cae183e81d0ddb9c8222dabd8929


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 iOS 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

除了创建应用程序的其他 System Center Configuration Manager 要求和过程，在创建和部署适用于 iOS 设备的应用程序时还必须考虑以下注意事项。  

## <a name="general-considerations"></a>一般注意事项  
 Configuration Manager 支持部署以下应用类型：  

|设备类型|受支持的文件|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> 在 System Center Configuration Manager 中，不需要在导入 iOS 应用时指定属性列表 (.plist) 文件。|  

 支持以下部署操作：  

|设备类型|支持的操作|  
|-----------------|-----------------------|  
|iOS|可用、必需的（但用户必须同意安装）、卸载|  

> [!IMPORTANT]  
>  目前，最终用户无法从 iOS 的 Microsoft Intune 公司门户应用程序中安装公司应用程序。 这是由于 iOS 应用商店中发布的应用受到限制（请参阅应用商店查看准则，第 2 部分）。 用户可通过浏览到 Intune Web 门户 (portal.manage.microsoft.com) 在其设备上安装企业应用（包括托管的应用商店应用和业务线应用包）。 有关由 Intune 公司门户应用启用的移动管理功能的详细信息，请参阅 [Microsoft Intune 中的注册设备管理功能](https://technet.microsoft.com/library/dn600287.aspx)。  



<!--HONumber=Nov16_HO1-->


