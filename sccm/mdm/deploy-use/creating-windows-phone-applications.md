---
title: 创建 Windows Phone 应用程序
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 中为 Windows Phone 设备创建和部署应用程序。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77eb0b750934641ceb66b2c8aa611544c654f54f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385433"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>在 Configuration Manager 中创建 Windows Phone 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 应用程序具有一个或多个部署类型。 部署类型包括将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。  

请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications#bkmk_create)，了解创建 Configuration Manager 应用程序和部署类型的步骤。 

创建和部署适用于 Windows Phone 设备的应用程序时，请记住以下注意事项：  


Configuration Manager 支持部署以下应用文件类型：  

|设备类型|支持的文件类型|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 移动版|xap, appx, appxbundle|

将 Windows Phone 应用部署为“可用”或“必需”。 还可使用部署来卸载应用。  
