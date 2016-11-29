---
title: "创建 Windows Phone 应用程序 | System Center Configuration Manager"
description: "请参阅创建和部署适用于 Windows Phone 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0963c86e51c78e8ba46dec29ecf6ccc669f6cc3b


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Windows Phone 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

除了创建应用程序的其他 System Center Configuration Manager 要求和过程，在创建和部署适用于 Windows Phone 设备的应用程序时还必须考虑以下注意事项。  

## <a name="general-considerations"></a>一般注意事项  
 Configuration Manager 支持部署以下应用类型：  

|设备类型|受支持的文件|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap、.appx、.appxbundle|  

 支持以下部署操作：  

|设备类型|支持的操作|  
|-----------------|-----------------------|  
|Windows Phone 8 和 Windows Phone 8.1|可用、要求、卸载|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>使用取代来部署最新 Windows Phone 公司门户应用的步骤  
 下表提供了创建和部署最新 Windows Phone 8 公司门户应用的步骤、详细信息和更多信息。  

|步骤|更多信息|  
|----------|----------------------|  
|**步骤 1：** 获取最新的公司门户应用。|下载 [Windows Phone 8 公司门户应用](http://go.microsoft.com/fwlink/?LinkId=268440)。|  
|**步骤 2：** 使用 Symantec 证书对公司门户应用进行签名。|有关如何对公司门户应用进行签名的信息，请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows Phone 和 Windows 10 移动版混合设备管理](../../mdm/deploy-use/set-up-windows-phone-hybrid-enrollment.md)。|  
|**步骤 3：** 使用公司门户应用的最新版本创建新的应用程序，并指定取代关系。|有关详细信息，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md)和[修订和取代应用程序](../../apps/deploy-use/revise-and-supersede-applications.md)。|  
|**步骤 4：**将应用程序添加到 Microsoft Intune 订阅向导。|添加 Microsoft Intune 订阅向导的应用程序 Windows Phone 8 页面。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 设置 Windows Phone 和 Windows 10 版移动混合设备管理](../../mdm/deploy-use/set-up-windows-phone-hybrid-enrollment.md)。|  
|**步骤 5：**删除向 Microsoft Intune 订阅向导添加公司门户应用时自动创建的部署。|Microsoft Intune 订阅已创建了此应用的自动部署，因为此部署将不支持取代。|  
|**步骤 6：** 在“部署软件向导”  的“部署设置”  页面创建新应用程序部署，并检查“自动升级此应用程序的任何取代版本” 。|使用取代功能以及用取代关系创建的应用程序来创建新部署。|  
|**步骤 7（可选）：** 默认情况下，7 天后将在设备上安装取代应用。 为了更快地将公司门户应用部署到以前注册的设备，你可以将“计划部署的重新评估”  设置更改为较低的值。<br /><br /> 如果将此值设置为低于默认值的值，则可能会对网络和客户端计算机性能有负面影响。|无更多信息。|  



<!--HONumber=Nov16_HO1-->


