---
title: "创建 Android 应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 Android 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Android 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 应用程序具有一个或多个部署类型，这些是将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。  

 可以使用下列方法创建应用程序：  

-   通过读取应用程序安装文件来自动创建应用程序和部署类型。  

-   手动创建应用程序并稍后添加部署类型。  

-   从文件导入应用程序。  

请参阅[启动创建应用程序向导](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)，了解创建 Configuration Manager 应用程序和部署类型所需的步骤。 此外，创建和部署适用于 Android 设备的应用程序时，请记住以下注意事项。  

## <a name="general-considerations"></a>一般注意事项

Configuration Manager 支持以下适用于 Android 的应用类型的部署：

|设备类型|受支持的文件|
|-|-|
|Android|.apk|

支持以下部署操作：

|设备类型|支持的操作|
|-|-|
|Android|**可用**、**必需**。 用户必须同意安装和卸载。

