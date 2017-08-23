---
title: "建立 Windows 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Windows 裝置的應用程式時，必須考慮的事項。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Windows 應用程式

*適用於：System Center Configuration Manager (最新分支)*

建立和部署 Windows 裝置的應用程式時，除了建立應用程式的其他 System Center Configuration Manager 需求和程序之外，還必須考慮下列項目。  

## <a name="general-considerations"></a>一般考量  
 Configuration Manager 支援部署下列應用程式檔案類型：  

|裝置類型|支援的檔案類型|  
|-----------------|---------------------|  
|Windows RT 和 Windows RT 8.1|*.appx、\*.appxbundle|  
|註冊為行動裝置的 Windows 8.1 及更新版本|*.appx、\*.appxbundle|  

 支援下列部署動作：  

|裝置類型|支援的動作|  
|-----------------|-----------------------|  
|Windows 8.1 及更新版本|可用、必要、解除安裝|  
|Windows RT|可用、必要、解除安裝|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>支援通用 Windows 平台 (UWP) 應用程式  
 Windows 10 裝置不需要側載金鑰，即可安裝企業營運應用程式。 不過，登錄機碼 **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** 的值必須為 1，才能啟用側載。  

 如果未設定此登錄機碼，Configuration Manager 就會在您初次將應用程式部署到裝置時，自動將此值設為 **1**。 如果您已將此值設為 **0**，Configuration Manager 即無法自動變更此值，而部署企業營運應用程式就會失敗。  

 通用 Windows 平台的企業營運應用程式必須使用程式碼簽署的憑證來簽署，而此憑證會受到部署該應用程式的每部目標裝置所信任。 您可以使用來自內部 PKI 基礎結構的憑證，也可以使用安裝於裝置上的協力廠商公用根憑證。  

 在 Windows 10 行動裝置版的裝置上，您可以使用非 Symantec 的程式碼簽署憑證來簽署通用 **.appx** 應用程式。 要安裝於 Windows 10 行動裝置版裝置的 **.xap** 應用程式以及針對 Windows Phone 8.1 所建置的 **.appx** 套件，則必須使用 Symantec 程式碼簽署憑證。  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>將 Windows Installer 應用程式部署到已註冊的 Windows 10 電腦  
 [透過 MDM 的 Windows Installer (\*.msi)] 的安裝類型可讓您建立以 Windows Installer 為基礎的應用程式，並將其部署到執行 Windows 10 的已註冊電腦上。  

 當您使用這種安裝程式類型時，必須考量下列幾點：  

-   您只能上傳副檔名為 .msi 的單一檔案。  

-   使用檔案的產品代碼和產品版本來偵測應用程式。  

-   使用應用程式的預設重新啟動行為。 Configuration Manager 不會控制這個項目。  

-   針對單一使用者安裝每位使用者的 MSI 套件。  

-   針對裝置上的所有使用者安裝每部電腦的 MSI 套件。  

-   當各版的 MSI 產品代碼相同時，支援應用程式更新。  
