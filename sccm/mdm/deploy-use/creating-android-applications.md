---
title: "创建 Android 应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 Android 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3a89abc81cd70f4e499bf4e3087fd53915377c44
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Android 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 应用程序具有一个或多个部署类型。 部署类型包括将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。  

 可以使用下列方法创建应用程序：  

-   通过读取应用程序安装文件来自动创建应用程序和部署类型。  
-   手动创建应用程序并稍后添加部署类型。  
-   从文件导入应用程序。  

请参阅[启动创建应用程序向导](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)，了解创建 Configuration Manager 应用程序和部署类型所需的步骤。 此外，创建和部署适用于 Android 设备的应用程序时，请记住以下注意事项。  

## <a name="general-considerations-for-android-apps"></a>Android 应用的一般注意事项

Configuration Manager 支持以下适用于 Android 的应用类型的部署：

|设备类型|受支持的文件|
|-|-|
|Android|.apk|

支持以下部署操作：

|设备类型|支持的操作|
|-|-|
|Android|可用、必需 用户必须同意安装和卸载。|
|Android for Work | **必需** |

## <a name="approve-and-deploy-android-for-work-apps"></a>批准和部署 Android for Work 应用
作为 Configuration Manager 管理员，你还可以在 [Play for Work 网站](https://play.google.com/work)中批准应用，并将这些应用部署到托管的 Android for Work 设备。

使用以下步骤在 Play for Work 应用商店中批准应用，将其同步到 Configuration Manager 控制台，然后将其部署到托管的 Android for Work 设备中。 若要将应用部署到用户的工作配置文件中，需要在 Play for Work 中批准该应用，然后将应用与 Configuration Manager 控制台同步。

1. 打开浏览器并转到：https://play.google.com/work。
2. 使用绑定到你的 Intune 租户的 Google 管理员帐户登录。
3. 浏览要在你的环境中部署的应用，然后为每个应用选择“批准”，使应用可用于Android for Work。
4. 在 Configuration Manager 控制台中，转到“管理员” > “概述” > “云服务” > “Android for Work”，然后选择“同步”。
5. 等待应用同步（最多 10 分钟），然后转到“软件库” > “概述” > “应用程序管理” > “应用商店应用的许可证信息”。
6. 选择从 Play for Work 同步的应用，然后选择“创建应用程序”。
7. 完成该向导，然后选择“关闭”。
8. 转到“软件库” > “概述” > “应用程序管理” > “应用程序”，选择 Android for Work 应用，然后照常部署。

若要将 Play for Work 应用与 Configuration Manager 同步，首先必须在 Play for Work 网站上至少批准一个应用。
