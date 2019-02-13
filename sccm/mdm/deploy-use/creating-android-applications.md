---
title: 创建 Android 应用程序
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 中针对 Android 设备创建和部署应用程序。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef070186112642d204aade24039da87c0e3a22f0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139664"
---
# <a name="create-android-applications-in-configuration-manager"></a>在 Configuration Manager 中创建 Android 应用程序

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 应用程序具有一个或多个部署类型。 部署类型包括将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。  

请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications#bkmk_create)，了解创建 Configuration Manager 应用程序和部署类型的步骤。 

创建和部署适用于 Android 设备的应用程序时，请记住以下注意事项：  



## <a name="general-considerations-for-android-apps"></a>Android 应用的一般注意事项

Configuration Manager 支持部署 Android .apk 包。 

它支持以下部署操作：

|设备类型|支持的操作|
|-|-|
|Android|**可用**，**所需**:用户必须同意安装和卸载。|
|Android for Work |可用、必需 |



## <a name="approve-and-deploy-android-for-work-apps"></a>批准和部署 Android for Work 应用

作为 Configuration Manager 管理员，还可以在 [Play for Work 网站](https://play.google.com/work)中批准应用。 然后将这些应用部署到托管的 Android for Work 设备。

使用以下步骤在 Play for Work 应用商店中批准应用，将其同步到 Configuration Manager 控制台，然后将其部署到托管的 Android for Work 设备中。 若要将应用部署到用户的工作配置文件，需要在 Play for Work 中批准应用。 然后将应用与 Configuration Manager 控制台同步。

1. 打开浏览器并转到： https://play.google.com/work。  

2. 使用绑定到 Microsoft Intune 租户的 Google 管理员帐户登录。  

3. 浏览要在环境中部署的应用。 为每个应用选择“批准”，使应用可用于 Android for Work。  

4. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Android for Work”节点。  

5. 在功能区中单击“同步”。  

6. 等待 10 分钟以使应用同步。然后转到“软件库”工作区，展开“应用程序管理”，然后选择“应用商店应用的许可证信息”节点。  

7. 选择从 Play for Work 同步的应用，然后单击“创建应用程序”。  

8. 完成向导。  

9. 转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点。 选择 Android for Work 应用，然后照常部署。  

若要将 Play for Work 应用与 Configuration Manager 同步，请首先在 Play for Work 网站上批准至少一个应用。

部署为“可用”的应用会显示在带有工作徽章的 Google Play 应用中，而不是公司门户。 这允许部署来自受信任的源的应用。 带有工作徽章的 Google Play 应用是受信任的源。 不必允许来自不受信任的源的应用。
