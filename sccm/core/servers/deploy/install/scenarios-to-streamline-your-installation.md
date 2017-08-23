---
title: "安裝案例 | Microsoft Docs"
description: "了解在更新或升級站台時，安裝新 Configuration Manager 階層的技術。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 938b2970e4d8534fdd5f3daf0c9a5ddb1f576e60
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>System Center Configuration Manager 安裝簡化案例

*適用於︰System Center Configuration Manager (最新分支)*

隨著 System Center Configuration Manager 最新分支更新版本的發行，不論要將新階層安裝到更新版本 (例如更新 1610)，或從 Microsoft System Center 2012 Configuration Manager 進行升級，都提供可簡化程序的新案例。

支援的案例包括：  

**安裝新的 System Center Configuration Manager 最新分支階層**以執行更新版本。  

-   只安裝頂層站台，緊接著安裝更新，讓該站台成為具有您將使用的更新版本的最新版本。 接著，您可以將其他站台直接安裝到該更新版本。  
-   在此案例中，您可以略過下列程序：將其他站台安裝到基準層級，然後將它們更新到您要使用的更新版本。  
-   在此案例中，您可以略過下列程序：將用戶端安裝到基準版本，然後在您更新到較新版本時重新安裝用戶端。  

**升級 Microsoft System Center 2012 Configuration Manager** 基礎結構至 System Center Configuration Manager 的更新版本。  

-   先將管理中心網站和每個主要站台手動升級到基準版本 (例如 1606 版)，再安裝更新版本 (例如 1610 版)。  
-   在主要站台執行您要使用的更新版本之前，請不要從 Microsoft System Center 2012 Configuration Manager 升級次要站台。  
-   在主要站台執行您要使用的更新版本之前，請不要從 Microsoft System Center 2012 Configuration Manager 升級站台。  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>案例：將新階層安裝到更新版本  
在此範例案例中，請使用 System Center Configuration Manager 的基準版本 (例如 1610 版) 來安裝階層的第一個站台。 接著，請在部署其他站台或用戶端之前安裝 1610 更新。  

-   由於您打算使用更新版本 (例如 1610 版) 而不是停留在基準版本 (例如 1606 版)，因此您不需要先安裝其他站台，再將它們升級。 這也適用於用戶端。  
-   請不要安裝版本為 1606 的次要站台，然後將它們升級到 1610 版。 相反地，請在主要站台執行 1610 版之後安裝次要站台。  

請遵循下列順序︰  

1.  使用基準媒體來**安裝新階層的頂層站台**。  

    -   您只能使用基準媒體來安裝新階層的第一個站台。  
    -   例如，使用基準版本 1606 來安裝頂層站台。 如需詳細資訊，請參閱[使用安裝精靈安裝站台](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)。  

    在此步驟之後，您的頂層站台就會執行 1606 版。  

2.  **使用主控台內更新，將您的頂層站台更新到較新的版本**。  

    -   在安裝任何子站台或用戶端之前，先將您的頂層站台更新到您打算使用的更新版本。  
    -   例如，您可以將執行 1606 版的頂層站台更新到 1610 版。 如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)。  

    在此步驟之後，您的頂層站台就會執行 1610 版。  

3.  **在管理中心網站底下安裝新的子主要站台。**  

    -   使用管理中心網站伺服器上 [CD.Latest] 資料夾中的安裝媒體來安裝子主要站台。 如需詳細資訊，請參閱 [System Center Configuration Manager 的 CD.Latest 資料夾](../../../../core/servers/manage/the-cd.latest-folder.md)。  

      必須使用此來源媒體，才能確保新的子主要站台與管理中心網站的版本相符。  

    在此步驟之後，新的子主要站台就會執行 1610 版。  

4.  **在每個主要站台，使用主控台內選項來安裝新的次要站台**。  

    -   如果您未在主要站台版本為 1606 時安裝次要站台，就不需要升級次要站台。  
    -   相反地，請安裝執行 1610 版的新次要站台。 如需詳細資訊，請參閱 [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites) (使用安裝精靈安裝站台) 主題中的[Install a secondary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary) (安裝次要站台)。  

    在此步驟之後，新次要站台就會安裝並執行 1610 版。  

5.  **在主要站台安裝新的用戶端。**  

    -   如果您未在主要站台版本為 1606 時安裝用戶端，就不需要將用戶端從 1606 版升級到 1610 版。  
    -   相反地，請安裝執行 1610 版的新用戶端。 如需詳細資訊，請參閱[在 System Center Configuration Manager 中部署用戶端](../../../clients/deploy/deploy-clients-to-windows-computers.md)。  

    在此步驟之後，就會安裝執行 1610 版的新用戶端。  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>案例：將 System Center 2012 Configuration Manager 升級到 System Center Configuration Manager 最新分支的更新版本  
在此範例案例中，將 Microsoft System Center 2012 Configuration Manager 基礎結構升級到 System Center Configuration Manager 的更新版本，例如 1610 版。  

-   在您安裝 1610 版的更新之前，必須先將管理中心網站和每個主要站台升級到基準版本 1606。  
-   次要站台和用戶端則不會升級或安裝 1606 版。 反之，它們會直接從 Microsoft System Center 2012 Configuration Manager 移轉為 System Center Configuration Manager 1610 版。  

請遵循下列順序︰  

1.  **升級頂層 Microsoft System Center 2012 Configuration Manager 站台**至最新分支的基準版本 (例如 1606 版)，方法是使用 System Center Configuration Manager 來源媒體。 如需詳細資訊，請參閱[升級至 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)。  

    -   就像傳統升級案例一樣，您一律是先升級階層的頂層站台，然後再升級子站台。  

    在此步驟之後，您的頂層站台就會執行 1606 版。  

2.  將**您階層中的每個子主要站台升級** 到該相同基準版本。  

    -   當您從 Microsoft System Center 2012 Configuration Manager 升級時，必須將每個主要站台手動升級到最新分支的基準版本。  
    -   您目前不需要升級次要站台。  

    在此步驟之後，每個主要站台都會執行 1606 版。  

3.  **設定子主要站台的維護時段**。 將所有主要站台升級到基準版本之後，請規劃設定維護期間以控制這些站台安裝基礎結構更新的時間。 如需詳細資訊，請參閱[如何使用 System Center Configuration Manager 中的維護期間](../../../../core/clients/manage/collections/use-maintenance-windows.md)。  (維護期間在 1606 版中稱為「服務保留時間」。)  

    -   子主要站台會自動安裝您在管理中心網站所安裝的相同更新。  
    -   次要站台不會自動安裝新版本。 您必須從主控台內手動升級。  

  在此步驟之後，當您在管理中心網站上安裝更新時，子主要站台將只有在其維護期間允許的情況下，才會安裝該更新。  

4.  **在您的頂層站台安裝更新版本**。 這會更新您的頂層站台。 在管理中心網站安裝更新版本之後，除非維護期間封鎖安裝，否則每個子主要站台都會自動安裝更新。  

    -   例如，您可以將頂層站台從 1606 版更新到 1610 版。 如需詳細資訊，請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)。  

    在此步驟之後，您的管理中心網站和每個主要站台都會執行 1610 版。  

5.  **升級次要站台。** 在主要站台安裝更新並執行 1610 版之後，請使用主控台內選項來升級次要站台。  

    -   這會將次要站台從 Microsoft System Center 2012 Configuration Manager 直接升級到您在主要站台上安裝的更新版本。  
    -   如需升級次要站台的資訊，請參閱[升級至 System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) 中的[升級站台](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade)。  

6.  **升級用戶端。** 若要升級用戶端，請使用[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)中的資訊。  

    -   這會將用戶端從 Microsoft System Center 2012 Configuration Manager 直接升級到您在主要站台上安裝的更新版本。  

    在此步驟之後，用戶端就會升級到 1610 版，而不需先升級到 1606 版。
