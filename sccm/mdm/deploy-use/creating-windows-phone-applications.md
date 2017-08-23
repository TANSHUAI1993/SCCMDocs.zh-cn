---
title: "建立 Windows Phone 應用程式 | Microsoft Docs"
description: "查看在您建立和部署 Windows Phone 裝置的應用程式時，必須考慮的事項。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6cbf2389a72c0c384ef8e84a1755ac77b64bfc6d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 建立 Windows Phone 應用程式

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 應用程式有一或多個部署類型，其中包含將軟體部署至裝置所需的安裝檔案與資訊。 部署類型也包含指定部署軟體之時間和方法的規則。  

 您可以使用下列兩種方式建立應用程式：  

-   透過讀取應用程式安裝檔案的方式自動建立應用程式和部署類型。  

-   手動建立應用程式並在之後新增部署類型。  

-   從檔案匯入應用程式。  

如需建立 Configuration Manager 應用程式與部署類型的必要步驟，請參閱[啟動建立應用程式精靈](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)。 此外，當您建立並部署 Windows Phone 裝置的應用程式時，請記住下列考量。  

## <a name="general-considerations"></a>一般考量  
 Configuration Manager 支援部署下列應用程式檔案類型：  

|裝置類型|支援的檔案類型|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap、.appx、.appxbundle|
|Windows 10 Mobile|.xap、.appx、.appxbundle|

 支援下列部署動作：  

|裝置類型|支援的動作|  
|-----------------|-----------------------|  
|Windows Phone 8、Windows Phone 8.1 及 Windows 10 Mobile|可用、必要、解除安裝|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>使用取代方式部署最新 Windows Phone 公司入口網站應用程式的步驟  
 下表提供用於建立及部署最新 Windows Phone 8 公司入口網站應用程式的步驟、詳細資料和更多資訊。  

|步驟|詳細資訊|  
|----------|----------------------|  
|**步驟 1：**取得最新的公司入口網站應用程式。|下載 [Windows Phone 8 公司入口網站應用程式](http://go.microsoft.com/fwlink/?LinkId=268440)。|  
|**步驟 2：**使用您的 Symantec 憑證簽署公司入口網站應用程式。|如需如何簽署公司入口網站應用程式的相關資訊，請參閱[以 System Center Configuration Manager 和 Microsoft Intune 來設定 Windows Phone 及 Windows 10 行動裝置版混合式裝置管理](../../mdm/deploy-use/enroll-hybrid-windows.md)。|  
|**步驟 3：**使用最新版公司入口網站應用程式建立新的應用程式，並指定取代關聯性。|如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)和[修改和取代應用程式](../../apps/deploy-use/revise-and-supersede-applications.md)。|  
|**步驟 4：**將應用程式新增至 [Microsoft Intune 訂閱精靈]。|如需詳細資訊，請參閱[以 System Center Configuration Manager 和 Microsoft Intune 來設定 Windows Phone 及 Windows 10 行動裝置版混合式裝置管理](../../mdm/deploy-use/enroll-hybrid-windows.md)。|  
|**步驟 5：**刪除在您將公司入口網站應用程式新增到 [Microsoft Intune 訂閱精靈] 時自動建立的部署。|Microsoft Intune 訂閱已建立此應用程式的自動部署，因為此部署不會支援取代。|  
|**步驟 6：**建立應用程式的新部署。 在 [部署軟體精靈] 的 [部署設定] 頁面上，選取 [自動升級任何會取代此應用程式的版本]。|使用您以取代關聯性建立的應用程式，建立含取代的新部署。|  
|**步驟 7 (選用)：**依預設，取代應用程式會在 7 天後安裝於裝置上。 若要更快將公司入口網站應用程式部署到先前註冊的裝置，可以將 [排程部署的重新評估] 設定變更為較低的值。<br /><br /> 如果將這個值設定成比預設值低的值，可能會對您的網路及用戶端電腦效能造成負面影響。|沒有其他資訊。|  
