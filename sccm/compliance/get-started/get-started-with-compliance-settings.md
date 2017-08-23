---
title: "開始使用合規性設定 | Microsoft Docs"
description: "了解如合規性設定在 System Center Configuration Manager 中的運作方式。 也深入了解您需要知道的核心概念。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f16c87dfd0c4f80d96aedf7f5f7497f2bbd4752a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中開始使用相容性設定

*適用於：System Center Configuration Manager (最新分支)*

開始建立 System Center Configuration Manager 設定項目之前，您應該先檢閱本主題來了解合規性設定的運作方式，並深入了解您需要知道的核心概念。  

## <a name="how-compliance-settings-works"></a>相容性設定的運作方式  
 合規性設定讓您管理貴組織中伺服器、膝上型電腦、桌上型電腦和行動裝置的設定與合規性。  

 組態項目可分為兩種主要類別：  

-   **使用 Configuration Manager 用戶端管理的裝置設定** - 通常是您已安裝 Configuration Manager 用戶端軟體的裝置，以便您管理裝置。  

-   **不使用 Configuration Manager 用戶端管理的裝置設定** - 通常是使用 Microsoft Intune 或 Configuration Manager 內部部署裝置管理來管理的裝置。  

## <a name="what-devices-are-supported"></a>支援哪些裝置？  


|裝置類型|詳細資訊|  
|------------|----------------------|  
|Windows 電腦 (含 Configuration Manager 用戶端)|可讓您建立自訂的組態項目，藉此評估項目，例如登錄機碼、檔案和 Active Directory 屬性。<br /><br /> 當您使用 Windows 10 的組態項目類型時，請從預先定義的清單中選取您要的設定。|  
|Windows 電腦 (使用 Microsoft Intune 註冊)|請從預先定義的清單中選取您要的設定。|  
|iOS 裝置 (使用 Microsoft Intune 註冊)|請從預先定義的清單中選取您要的設定。|  
|Android 裝置 (使用 Microsoft Intune 註冊)|請從預先定義的清單中選取您要的設定。|  
|Windows Phone 裝置 (使用 Microsoft Intune 註冊)|請從預先定義的清單中選取您要的設定。|  
|Mac 電腦 (含 Configuration Manager 用戶端)|可讓您建立自訂的組態項目，藉此評估項目，例如 Mac OS X 喜好設定 (屬性清單) 的值，以及由指令碼傳回的結果。|  
|Mac 電腦 (使用 Microsoft Intune 註冊)|請從預先定義的清單中選取您要的設定。|  

## <a name="what-is-a-configuration-item"></a>什麼是設定項目？  
 組態項目可以視為儲存下列資訊的容器 (您所設定的資訊將取決於組態項目類型：  

-   **偵測方法資訊** (適用於僅包含應用程式設定值的 Windows 組態項目) - 可讓您偵測應用程式的 Windows Installer 檔案，或使用自訂指令碼，偵測是否已安裝該應用程式。  

-   **設定** - 這些設定代表用來在用戶端裝置上評估相容性的商業或技術條件。 您可以進行新的設定，或瀏覽至參照電腦上現有的設定。  

-   **相容性規則** - 相容性規則可指定用於定義組態項目設定相容性的條件。 設定至少必須有一項相容性規則，才能評估其相容性。 某些設定可讓您補救所找到不相容的值。 您可以建立新的規則，或瀏覽至任何組態項目中現有的設定來選取其中的規則。  

-   **支援的平台** - 這些是您定義的裝置平台，在這些平台上將針對相容性評估組態項目。 如果您將組態項目部署至不在支援平台清單中的裝置時，將不會針對相容性評估該組態項目。  

## <a name="what-is-a-configuration-baseline"></a>什麼是組態基準？  
 評估相容性的方法是定義組態基準，其中包含您想要評估的組態項目，以及包含描述您必須具有之相容性層級的設定和規則。 作為最佳作法，您可以從 Microsoft System Center Configuration Manager Configuration Packs 網頁匯入這項設定資料，這些資料由 Microsoft 和其他廠商在 Configuration Manager 所定義，然後您可以將其匯入至 Configuration Manager。 或者您可以建立新的組態項目和組態基準。  

 定義組態基準之後，您可以透過集合將其部署至使用者和裝置，並評估其排程上的相容性設定。 可以將多個組態基準部署到裝置。 如此可提供您高階的控制。  

 用戶端裝置會針對每個已部署的組態基準評估其相容性，並立即使用狀況訊息和狀態訊息，將結果報告至站台。 如果用戶端裝置目前未連接到網路，但已下載部署的組態基準中所參考的組態項目，便會針對相容性評估此組態基準。 重新連線時，會傳送相容性資訊。  

 您可以從 Configuration Manager 主控台 [監視] 工作區中的 [部署] 節點，監視設定基準評估合規性的結果，以檢視不符合規範的最常見原因、錯誤，以及受影響的使用者和裝置數目。 您也可以執行相容性設定報告，以尋找詳細資訊，例如哪些裝置相容或不相容，以及組態基準的哪個項目會導致電腦不相容。 您也可以從執行 Configuration Manager 用戶端軟體的 Windows 電腦檢視相容性評估結果，方法是在 [控制台] 的 Configuration Manager 中使用 [設定] 索引標籤。  

## <a name="user-data-and-profiles-configuration-items"></a>使用者資料和設定檔組態項目  
 使用者資料和設定檔組態項目所包含的設定，可控制階層中使用者如何在執行 Windows 8 及更新版本的電腦上管理資料夾重新導向、離線檔案和漫遊設定檔。 您可以將這些設定部署到使用者集合，然後從 Configuration Manager 主控台的 [監視] 節點監控其合規性。 不同於其他組態項目，在部署之前，您不需要將這些設定加入組態基準。 您可以藉由 [部署使用者資料和設定檔組態項目]  對話方塊直接部署這些設定。  

 如需詳細資訊，請參閱[建立使用者資料和設定檔設定項目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)。  

## <a name="remote-connection-profiles"></a>遠端連線設定檔  
 遠端連線設定檔提供一組工具和資源，可協助您建立、部署和監視您組織中各裝置的遠端連線設定。 藉由部署這些設定，可將使用者連線到其在公司網路中的電腦所需的時間，縮到最短。  

如需詳細資訊，請參閱[建立遠端連線設定檔](/sccm/compliance/deploy-use/create-remote-connection-profiles)。  

## <a name="windows-edition-upgrade"></a>Windows 版本升級
版本升級原則可讓您藉由提供新的產品金鑰或授權檔案，將執行特定版本 Windows 10 的裝置自動升級至較新版本。

如需詳細資訊，請參閱[使用版本升級原則升級 Windows 裝置](/sccm/compliance/deploy-use/upgrade-windows-version)
