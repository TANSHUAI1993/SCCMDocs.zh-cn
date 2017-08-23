---
title: "管理透過 Intune 進行管理之裝置的合規性 | Microsoft Docs"
description: "透過處理一些常見的案例，了解 System Center Configuration Manager 合規性設定需要。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3a63f6c55c317c9c84d4394dfdcb9f1cbbbc90b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="managing-compliance-on-devices-managed-with-intune"></a>管理透過 Intune 進行管理之裝置的合規性

*適用於：System Center Configuration Manager (最新分支)*

這些案例透過您可能遇到的一些常見案例，為您簡介使用 System Center Configuration Manager 的合規性設定。  

 如果您已經熟悉合規性設定，有關您所使用之所有功能的詳細文件可在[透過 Intune 進行管理之裝置的設定項目](#configuration-items-for-devices-managed-with-intune)一節中找到。  

 [開始使用合規性設定](../../compliance/get-started/get-started-with-compliance-settings.md)提供有關合規性設定的基本概念，而[規劃和設定合規性設定](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)可協助您實作任何所需的先決條件。  

## <a name="general-information-for-each-scenario"></a>每個案例的通用資訊  
 在每個案例中，您會建立執行特定工作的設定項目。 請使用下列步驟開啟 [建立設定項目精靈]：  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定項目]。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立設定項目] 。  

4.  在 [建立設定項目精靈] 的 [一般]  索引標籤上 (如下所示)，指定設定項目的名稱和描述，然後為本主題的每個案例選擇適當的設定項目類型。  

     ![顯示 [建立設定項目精靈] 的 [一般] 頁面。](media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-with-intune"></a>使用 Intune 進行管理之 Windows 8.1 和 Windows 10 裝置的案例  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>案例：限制存取所有 Windows 電腦上的應用程式市集  
 在這個案例中，您是公司處理高機密資訊的 IT 管理員。 因此，您限制了使用者可以安裝的應用程式。 您希望所有 Windows 10 電腦的使用者都不要下載 Windows 市集的應用程式，所以您採取了下列動作。  

1.  在 [建立設定項目精靈] 的 [一般] 頁面上，選取 [Windows 8.1 和 Windows 10] 設定項目類型，然後按一下 [下一步]。  

2.  在 [支援的平台] 頁面上，選取所有的 Windows 10 平台。  

3.  在 [裝置設定] 頁面上，選取 [市集]，然後按一下 [下一步]。  

4.  在 [市集] 頁面上，選取 [禁止] 作為 [應用程式市集] 的值。  

5.  選取 [補救不符合規範的設定] 確保變更套用至所有電腦。  

6.  完成精靈以建立設定項目。  

 您現在可以使用[建立及部署設定基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主題中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="scenarios-for-windows-phone-devices-managed-with-intune"></a>使用 Intune 進行管理之 Windows Phone 裝置的案例  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>案例：停用 Windows phone 的螢幕擷取  
 在這個案例中，您會在公司使用 Windows Phone 8.1 裝置。 這些裝置會執行包含機密資訊的銷售應用程式。 為了保護公司，您要停用裝置的螢幕擷取功能，因為這個功能可能會對外傳送公司的機密資訊。  

1.  在 [建立設定項目精靈] 的 [一般] 頁面上，選取 [Windows Phone] 設定項目類型，然後按一下 [下一步]。  

2.  在 [支援的平台] 頁面上，選取 [所有 Windows Phone 8.1] 平台。  

3.  在 [裝置設定] 頁面上，選取 [裝置]，然後按一下 [下一步]。  

4.  在 [裝置] 頁面上，選取 [停用] 作為 [螢幕擷取] 的值。  

5.  選取 [補救不符合規範的設定] 確保變更套用至所有 Windows Phone 8.1 裝置。  

6.  完成精靈以建立設定項目。  

 您現在可以使用[以 System Center Configuration Manager 建立及部署組態基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主題中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-with-intune"></a>使用 Intune 進行管理之 iOS 和 Mac OS X 裝置的案例  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>案例：停用 iOS 裝置的相機  
 在這個案例中，貴公司要製造新的產品設計藍圖。 這裡面有絕對不能外洩的機密資訊。 貴公司為所有員工配備 iPhone 或 iPad，您希望停用這些裝置上的相機，以免它們被用於拍攝藍圖。  

1.  在 [建立設定項目精靈] 的 [一般] 頁面上，選取 [iOS 和 Mac OS X] 設定項目類型，然後按一下 [下一步]。  

2.  在 [支援的平台] 頁面上，選取所有 iPhone 和所有 iPad 裝置平台。  

3.  在 [裝置設定] 頁面上，選取 [安全性]，然後按一下 [下一步]。  

4.  在 [安全性] 頁面上，選取 [禁止] 作為 [相機] 的值。  

5.  選取 [補救不符合規範的設定] 確保變更套用至所有 iOS 裝置。  

6.  完成精靈以建立設定項目。  

 您現在可以使用[以 System Center Configuration Manager 建立及部署組態基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主題中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>使用 Intune 進行管理之 Android 與 Samsung KNOX Standard 裝置的案例  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>案例：所有的 Android 5 裝置都需要密碼  
 在這個案例中，您要建立 Android 5 裝置的設定項目，但是要求使用者裝置要設定至少 6 個字元的密碼。 而且，如果使用者輸入 5 次不正確的密碼，就會抹除裝置。  

1.  在 [建立設定項目精靈] 的 [一般] 頁面上，選取 [Android 和 Samsung KNOX] 設定項目類型，然後按一下 [下一步]。  

2.  在 [支援的平台] 頁面上，只選取 [Android 5]\(以確保設定只套用到該平台)。  

3.  在 [裝置設定] 頁面上，選取 [密碼]，然後按一下 [下一步]。  

4.  在 [密碼] 頁面設定以下設定：  

    -   **裝置需要密碼設定** > **必要**  

    -   **[最小密碼長度 (字元數)]** > **[6]**  

    -   **[抹除裝置前允許的失敗登入嘗試次數]** > **[5]**  

5.  完成精靈以建立設定項目。  

 您現在可以使用[建立及部署設定基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主題中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="configuration-items-for-devices-managed-with-intune"></a>使用 Intune 進行管理之裝置的設定項目

下列為不受 Configuration Manager 用戶端管理之裝置 (例如向 Microsoft Intune 註冊的裝置) 的可用 System Center Configuration Manager 設定項目類型。  

 -   [如何建立使用 Intune 進行管理之 Windows 8.1 與 Windows 10 裝置的設定項目](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [如何建立使用 Intune 進行管理之 Windows Phone 裝置的設定項目](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [如何建立使用 Intune 進行管理之 iOS 與 Mac OS X 裝置的設定項目](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [如何建立使用 Intune 進行管理之 Android 與 Samsung KNOX Standard 裝置的設定項目](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
