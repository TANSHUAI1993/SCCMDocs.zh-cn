---
title: "管理裝置的基本概念 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 來管理裝置。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 45d84122a86da880268c93ecd994250df6b76c8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 來管理裝置的基本概念

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 可以管理兩大類裝置：

-   「用戶端」係指您安裝 Configuration Manager 用戶端軟體的裝置，例如工作站、膝上型電腦、伺服器及行動裝置。 有些管理功能 (例如硬體清查) 需要此用戶端軟體。  

-   「受管理的裝置」可以包含「用戶端」，但它通常是未安裝 Configuration Manager 用戶端軟體的行動裝置。 您使用 Intune 或 Configuration Manager 的內建內部部署行動裝置管理，在這類裝置上執行管理工作。

您也可以根據使用者，而不只是用戶端類型來分組和識別裝置。

## <a name="managing-devices-with-the-configuration-manager-client"></a>使用 Configuration Manager 用戶端管理裝置

有兩種方式可以使用 Configuration Manager 用戶端軟體來管理裝置。 第一種方式是探索網路上的裝置，然後將用戶端軟體部署到該裝置。 另一種方式是在新的電腦上手動安裝用戶端軟體，然後在電腦加入網路時，讓它加入您的站台。 若要探索尚未安裝用戶端軟體的裝置，請執行一或多個內建的探索方法。 探索到裝置之後，使用數種方法之一來安裝用戶端軟體。 如需使用探索的資訊，請參閱[為 System Center Configuration Manager 執行探索](../../core/servers/deploy/configure/run-discovery.md)。  

 探索受支援而可執行 Configuration Manager 用戶端軟體的裝置之後，您可以使用數種方法中的其中一種方式來安裝軟體。 安裝軟體並將用戶端指派給主要站台之後，您便可以開始管理裝置。  常見的安裝方法包括︰

 - 用戶端推入安裝。

 - 以軟體更新為基礎的安裝。

 - 群組原則。

 - 在電腦上手動安裝。
 - 將用戶端納入您部署的作業系統映像。  


 安裝用戶端之後，您可以使用集合來簡化管理裝置的工作。 集合是您建立的裝置或使用者群組，因此您可以將它們當成群組來管理。 例如，您可能想要在 Configuration Manager 註冊的所有行動裝置上安裝行動裝置應用程式。 如果是這種情況，您可以使用 [所有行動裝置] 集合。  

 如需詳細資訊，請參閱下列主題：  

-   [選擇 System Center Configuration Manager 的裝置管理解決方案](../../core/plan-design/choose-a-device-management-solution.md)  

-   [System Center Configuration Manager 中的用戶端安裝方法](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [System Center Configuration Manager 的集合簡介](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>用戶端設計  
 當您初次安裝 Configuration Manager 時，階層中的所有用戶端都會採用您可變更的預設用戶端設定。 用戶端設定包括這些設定選項：

 -  裝置與站台通訊的頻率。

 -  用戶端是否已設定軟體更新和其他管理作業。

 -  使用者是否可以註冊其行動裝置，以便由 Configuration Manager 管理。  

您可以建立自訂用戶端設定，然後將它們指派給集合。  集合的成員是設定為採用自訂設定，而您可以建立多個依您指定順序 (依數字順序) 套用的自訂用戶端設定。  如果有設定發生衝突，則順序編號最小的設定會覆寫其他設定。  

下圖為如何建立及套用自訂用戶端設定的說明範例。  

 ![用戶端設計](media/ClientSettings.gif)  

 若要深入了解用戶端設定，請參閱  
                [如何在 System Center Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)[關於 System Center Configuration Manager 中的用戶端設定](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>在不使用 Configuration Manager 用戶端的情況下管理裝置  
 Configuration Manager 支援管理某些尚未安裝用戶端軟體，且非 Intune 管理的裝置。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)和[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

## <a name="user-based-management"></a>以使用者為基礎的管理  
 Configuration Manager 支援 Active Directory Domain Services 使用者集合。 當您使用使用者集合時，您可以在集合成員使用的所有電腦上安裝軟體。 為確保您部署的軟體僅安裝在指定為使用者主要裝置的裝置上，請設定使用者裝置親和性。 使用者可以擁有一個或多個主要裝置。  

 使用者控制其軟體部署體驗的方式之一，就是使用**軟體中心**用戶端介面。 **軟體中心**會自動安裝到用戶端電腦上，從 [開始] 功能表執行。 **軟體中心**讓使用者管理自己的軟體並執行下列工作：  

-   安裝軟體。  

-   將軟體排程在非工作時間自動安裝。  

-   設定 Configuration Manager 可以在何時將軟體安裝在裝置上。  

-   如果在 Configuration Manager 中已設定遠端控制，可以設定遠端控制的存取設定。  

-   如果系統管理設定了電源管理選項，就可以設定相關選項。  


 **軟體中心**中的連結可讓使用者連線至**應用程式類別目錄**，並且在此瀏覽、安裝和要求軟體。 **應用程式類別目錄**也用來設定喜好設定、抹除行動裝置，以及 (已設定時) 指定使用者裝置親和性的主要裝置。   

 使用者也可以透過瀏覽器內部網路或網際網路工作階段存取**應用程式類別目錄**。  
