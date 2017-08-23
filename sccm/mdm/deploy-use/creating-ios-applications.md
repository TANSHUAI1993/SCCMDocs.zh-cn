---
title: "建立 iOS 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 iOS 裝置的應用程式時，必須考慮的事項。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 iOS 應用程式

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 應用程式有一或多個部署類型，其中包含將軟體部署至裝置所需的安裝檔案與資訊。 部署類型也包含指定部署軟體之時間和方法的規則。  

 您可以使用下列兩種方式建立應用程式：  

-   透過讀取應用程式安裝檔案的方式自動建立應用程式和部署類型。  

-   手動建立應用程式並在之後新增部署類型。  

-   從檔案匯入應用程式。  

如需建立 Configuration Manager 應用程式與部署類型的必要步驟，請參閱[啟動建立應用程式精靈](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)。 此外，當您建立並部署 iOS 裝置的應用程式時，請記住下列考量。  

## <a name="general-considerations"></a>一般考量  
 Configuration Manager 支援部署下列應用程式類型：  

|裝置類型|支援的檔案|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> 在 System Center Configuration Manager 中，匯入 iOS 應用程式時，不需要指定內容清單 (.plist) 檔案。|  

 支援下列部署動作：  

|裝置類型|支援的動作|  
|-----------------|-----------------------|  
|iOS|**可用**、**必要**。 使用者必須同意安裝和解除安裝。

> [!IMPORTANT]  
>  使用者目前無法從適用於 iOS 的 Microsoft Intune 公司入口網站應用程式安裝公司應用程式。 這是因為 iOS App Store 中發行之應用程式的限制所致 (請參閱 App Store 審核指南的第 2 節)。 使用者可以在其裝置上瀏覽至 Intune Web 入口網站 (portal.manage.microsoft.com) 來安裝公司應用程式 (包括受管理的 App Store 應用程式與企業營運應用程式套件)。 如需 Intune 公司入口網站應用程式所啟用的行動管理功能詳細資訊，請參閱 [Microsoft Intune 的已註冊裝置管理功能](https://technet.microsoft.com/library/dn600287.aspx)。  
