---
title: "應用程式管理簡介 | Microsoft Docs"
description: "探索管理和部署 System Center Configuration Manager 應用程式所需的基本資訊。"
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: "18"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 959a36413d06bb225f260bd44c1d3d59efd44e69
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>System Center Configuration Manager 的應用程式管理簡介

適用於：System Center Configuration Manager (最新分支)

在本主題中，您將了解開始使用 System Center Configuration Manager 應用程式之前所需知道的基本概念。  

> [!TIP]  
>  如果您已熟悉如何在 Configuration Manager 中管理應用程式，則可略過這個主題，並移至如何建立範例應用程式。 請參閱[使用 System Center Configuration Manager 建立和部署應用程式](../../apps/get-started/create-and-deploy-an-application.md)。  

## <a name="what-is-an-application"></a>何謂應用程式？  
 雖然「應用程式」是電腦中廣泛使用的術語，但是在 Configuration Manager 中，其意義有些不同。 請將應用程式視為一個盒子。 這個盒子包含軟體套件的一或多組安裝檔 (稱為 **部署類型**)，以及軟體部署方式的指示。  

 將應用程式部署至裝置時， **需求** 決定在裝置上安裝的部署類型。  

 您可以使用應用程式完成更多工作。 透過閱讀本指南，您將會了解這些事項。 下表介紹您在深入探索之前需要知道的一些概念：  

|概念|說明|    
|-|-|  
|**Requirements**|在舊版的 Configuration Manager 中，您通常會建立集合，以包含您想要在其中部署應用程式的目標裝置。 雖然您仍然可以建立集合，但是可以透過需求為應用程式部署指定更詳細的準則。<br /><br /> 例如，您可以指定應用程式只能安裝在執行 Windows 10 的裝置上。 之後，您可以將應用程式部署至裝置，但該應用程式只會安裝於執行 Windows 10 的裝置上。<br /><br /> Configuration Manager 會評估需求，以判斷是否要安裝應用程式和其任何部署類型。 然後會判斷可套用來安裝應用程式的正確部署類型。 根據預設，系統會每 7 天根據用戶端設定 [排程部署的重新評估] 重新評估需求規則，確保其相容性。<br /><br /> 如需詳細資訊，請參閱[建立和部署應用程式](../../apps/get-started/create-and-deploy-an-application.md)。|  
|**全域條件**|雖然需求要搭配單一應用程式中的特定部署類型來使用，但您也可以建立全域條件。 這些是預先定義需求的程式庫，您可以與任何應用程式和部署類型搭配使用。<br /><br /> Configuration Manager 包含一組內建全域條件，而您也可以建立專屬的全域條件。<br /><br /> 如需詳細資訊，請參閱[建立全域條件](../../apps/deploy-use/create-global-conditions.md)。|  
|**模擬部署**|評估應用程式的需求、偵測方法及相依性。 它會報告結果，而不會實際安裝應用程式。<br /><br /> 如需詳細資訊，請參閱[模擬應用程式部署](../../apps/deploy-use/simulate-application-deployments.md)。|  
|**部署動作**|指定是要安裝或解除安裝 (支援時) 正在部署的應用程式。<br /><br /> 如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。|  
|**部署目的**|指定部署應用程式是 [必要] 還是 [可用] 。<br /><br /> [必要] 表示會根據已設定的排程自動部署應用程式。 不過，如果應用程式未隱藏，使用者便可追蹤應用程式部署狀態，也可使用 [軟體中心] 在期限前安裝應用程式。<br /><br /> [可用] 表示如果應用程式部署給使用者，則使用者會在軟體中心看見已發行的應用程式，並可依需求要求該應用程式。<br /><br /> 如需詳細資訊，請參閱[部署應用程式](../../apps/deploy-use/deploy-applications.md)。|  
|**修訂**|當您針對應用程式或包含在應用程式內的部署類型進行修訂時，Configuration Manager 會建立新的應用程式版本。 您可以顯示每個應用程式版本的歷程記錄、檢視其內容、還原先前的應用程式版本，或刪除舊版本。<br /><br /> 如需詳細資訊，請參閱[更新和淘汰應用程式](../../apps/deploy-use/update-and-retire-applications.md)。|  
|**偵測方法**|偵測方法用來探索是否已安裝已部署的應用程式。 如果偵測方法表示已安裝應用程式，則 Configuration Manager 不會嘗試再次安裝。<br /><br /> 如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|**相依性**|相依性會從安裝部署類型之前必須先行安裝的其他應用程式中，定義一或多個部署類型。 您可以將相依的部署類型設定為在安裝部署類型之前自動安裝。<br /><br /> 如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|**取代**|Configuration Manager 可讓您使用取代關聯性來升級或取代現有應用程式。 當您取代應用程式時，您可以指定新的部署類型來取代被取代應用程式的部署類型。 您也可以決定是否要先升級或解除安裝被取代的應用程式，然後再安裝取代的應用程式。<br /><br /> 如需詳細資訊，請參閱[建立應用程式](../../apps/deploy-use/create-applications.md)。|  
|**使用者為中心的管理**|Configuration Manager 應用程式支援以使用者為中心的管理，讓您可以將特定使用者與特定裝置產生關聯。 您不需要記住使用者裝置的名稱，就可以將應用程式部署給使用者和裝置。 這個功能可協助您確保特定使用者存取的每個裝置上都搭載了最重要的應用程式。 若使用者獲得一部新電腦，您也可以在使用者登入前，自動將其應用程式安裝到裝置上。<br /><br /> 如需詳細資訊，請參閱[連結使用者和裝置與使用者裝置親和性](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。|  

## <a name="what-application-types-can-you-deploy"></a>您可以部署的應用程式類型為何？  
 Configuration Manager 可讓您部署下列應用程式類型：  

- Windows Installer (*.msi 檔案)
- Windows 應用程式封裝 (*.appx、*.appxbundle)
- Windows 應用程式套件 (在 Windows 市集中)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization  5
- Windows Mobile 封包
- macOS  


此外，當您透過 Microsoft Intune 或 Configuration Manager 內部部署裝置管理功能來管理裝置時，可以進一步管理下列應用程式類型：

- Windows Phone 應用程式套件 (*.xap 檔案)
- iOS 應用程式套件 (*.ipa 檔案)
- Android 應用程式套件 (*.apk 檔案)
- Google Play 上的 Android 應用程式套件
- Windows Phone 應用程式套件 (在 Windows Phone 市集中)
- 透過 MDM 的 Windows Installer
- Web 應用程式



## <a name="state-based-applications"></a>狀態型應用程式  
 Configuration Manager 應用程式會使用狀態式監控功能，您可藉此追蹤使用者和裝置最近的應用程式部署狀態。 狀態訊息會顯示有關個別裝置的資訊。 例如，如果應用程式是部署至使用者集合，您可以在 Configuration Manager 主控台中檢視部署與部署目的的相容性狀態。 您可以使用 Configuration Manager 主控台中的 [監視] 工作區，來監視所有軟體的部署。 軟體部署包括軟體更新、相容性設定、應用程式、工作順序以及封裝和程式。 如需詳細資訊，請參閱[監視應用程式](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

 Configuration Manager 會定期重新評估應用程式部署。 例如：  

-   部署的應用程式會由使用者解除安裝。 因此，在下一個評估週期中，Configuration Manager 會偵測到應用程式不存在並進行重新安裝。  

-   應用程式未安裝在裝置上的原因是其不符合需求。 稍後，裝置會進行變更，因此現在已符合需求。 Configuration Manager 會偵測到這個變更並安裝應用程式。  


 您可以使用 [排程部署的重新評估] 用戶端設定，來設定應用程式部署的重新評估間隔。 如需詳細資訊，請參閱[關於用戶端設定](../../core/clients/deploy/about-client-settings.md)。  

## <a name="get-started-creating-an-application"></a>開始建立應用程式  
 如果您想要直接開始建立應用程式，可以在[建立和部署應用程式](../../apps/get-started/create-and-deploy-an-application.md)主題中找到建立簡單應用程式的逐步解說。  

 如果您已熟悉基本概念，但需要所有可用選項的更詳細參考資訊，請從[建立應用程式](/sccm/apps/deploy-use/create-applications)開始了解。  

## <a name="software-center-and-the-application-catalog"></a>軟體中心和應用程式類別目錄  
 在舊版的 Configuration Manager 中，軟體中心是用來安裝和排程軟體安裝、進行遠端控制設定，以及設定電源管理。 使用者可以連線到應用程式類別目錄來瀏覽和要求軟體、設定某些喜好設定，以及遠端抹除其行動裝置。  

 雖然 System Center Configuration Manager 仍提供這些設定，但現在已有新版的軟體中心，讓您能夠瀏覽應用程式。 您不必使用應用程式類別目錄，不過這需要 Silverlight 功能的網頁瀏覽器。 不過，仍然需要應用程式類別目錄網站點和應用程式類別目錄 Web 服務點站台系統角色，才能讓使用者可用的應用程式出現在軟體中心內。  

 如需詳細資訊，請參閱[規劃和設定應用程式管理](../../apps/plan-design/plan-for-and-configure-application-management.md)。  

## <a name="configuration-manager-packages-and-programs"></a>Configuration Manager 套件和程式  
 Configuration Manager 會持續支援產品舊版本中所使用的套件和程式。 在您部署以下項目時，使用封裝和程式的部署可能會比使用應用程式的部署適合：  

-   並未在電腦上安裝應用程式的程式碼，如重組電腦磁碟機的程式碼。  

-   不需要持續監控的「單次用」指令碼。  

-   按週期性排程執行且無法使用全域評估的指令碼。

 如需詳細資訊，請參閱[套件和程式](../../apps/deploy-use/packages-and-programs.md)。  
