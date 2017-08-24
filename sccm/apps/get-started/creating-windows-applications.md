---
title: "创建 Windows 应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 Windows 设备的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c80cc42f9ce6775067a89a9f5a63c1bf4a0c7ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Windows 应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

除了创建应用程序的其他 System Center Configuration Manager 要求和过程，在创建和部署适用于 Windows 设备的应用程序时还必须考虑以下注意事项。  

## <a name="general-considerations"></a>一般注意事项  
 Configuration Manager 支持部署以下应用文件类型：  

|设备类型|支持的文件类型|  
|-----------------|---------------------|  
|Windows RT 和 Windows RT 8.1|*.appx, \*.appxbundle|  
|注册为移动设备的 Windows 8.1 和更高版本|*.appx, \*.appxbundle|  

 支持以下部署操作：  

|设备类型|支持的操作|  
|-----------------|-----------------------|  
|Windows 8.1 及更高版本|可用、必需、卸载|  
|Windows RT|可用、必需、卸载|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>对通用 Windows 平台 (UWP) 应用的支持  
 Windows 10 设备无需旁加载密钥即可安装业务线应用。 但是，若要启用旁加载，注册表项 **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** 必须将值设置为“1”。  

 如果未配置此注册表项，Configuration Manager 在第一次向设备部署应用时会自动将此值设置为 **1**。 如果将此值设置为 **0**，则 Configuration Manager 无法自动更改此值，业务线应用部署将失败。  

 通用 Windows 平台业务线应用必须使用代码签名证书签名，并且该证书应在应用部署到的每个设备上受信任。 你可以使用内部 PKI 基础结构中的证书，也可以使用设备上安装的第三方公共根证书中的证书。  

 在 Windows 10 移动版设备上，可以使用非 Symantec 代码签名证书对通用 **.appx** 应用签名。 对于 **.xap** 应用以及要在 Windows 10 移动版设备上安装且针对 Windows Phone 8.1 生成的 **.appx** 包，必须使用 Symantec 代码签名证书。  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>将 Windows Installer 应用部署到已注册的 Windows 10 PC  
 **通过 MDM 的 Windows Installer (\*.msi)** 安装程序类型让你可以创建基于 Windows Installer 的应用并将其部署到运行 Windows 10 且已注册的电脑上。  

 使用此安装程序类型时，需要考虑下列注意事项：  

-   只能上载扩展名为 .msi 的单个文件。  

-   该文件的产品代码和产品版本将用于应用检测。  

-   使用该应用的默认重启行为。 Configuration Manager 不对此进行控制。  

-   为单个用户安装每用户 MSI 包。  

-   为设备上的所有用户安装每计算机 MSI 包。  

-   当每个版本的 MSI 产品代码相同时，支持应用更新。  
