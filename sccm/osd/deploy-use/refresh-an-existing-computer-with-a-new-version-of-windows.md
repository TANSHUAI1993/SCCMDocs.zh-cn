---
title: "使用新的 Windows 版本重新整理現有的電腦 | Microsoft Docs"
description: "您可以在 Configuration Manager 中使用多種方法來磁碟分割和格式化 (抹除) 現有電腦，並在電腦上安裝新作業系統。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b247cbb68ed63a8eb99715a248686d68a28c53e2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>使用 System Center Configuration Manager 以新的 Windows 版本重新整理現有的電腦

適用於：System Center Configuration Manager (最新分支)

本主題提供在 System Center Configuration Manager 中磁碟分割和格式化 (抹除) 現有電腦，並在電腦上安裝新作業系統的一般步驟。 這個案例中有多種不同的部署方法可供選擇，例如 PXE、可開機媒體或軟體中心。 您也可以選擇安裝狀態移轉點來儲存設定，然後在新的作業系統安裝之後將它們還原至新的作業系統。 如果您不確定此作業系統部署案例是否適合您，請參閱[部署企業作業系統的案例](scenarios-to-deploy-enterprise-operating-systems.md)。  

 請使用下列章節的內容，以新版的 Windows 重新整理現有的電腦。  

##  <a name="BKMK_Plan"></a> 方案  

-   **規劃並實作基礎結構需求**  

     必須要備妥數個基礎結構需求，才能部署作業系統 (例如 Windows ADK、使用者狀態移轉工具 (USMT)、Windows 部署服務 (WDS)、支援的硬碟設定等)。如需詳細資訊，請參閱[作業系統部署的基礎結構需求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

-   **安裝狀態移轉點 (轉移設定時才需要)**  

     當您要從現有的電腦擷取設定，然後將設定還原到新的作業系統時，您必須安裝狀態移轉點。 如需詳細資訊，請參閱[狀態移轉點](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)。  

##  <a name="BKMK_Configure"></a> 設定  

1.  **準備開機映像**  

     開機映像會啟動 Windows PE 環境中的電腦 (內含有限元件和服務的最低作業系統)，接著在電腦上安裝完整的 Windows 作業系統。   部署作業系統時，您必須選取要使用的開機映像，將此映像發佈到發佈點。 請使用下列資訊準備開機映像：  

    -   如需深入了解開機映像，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

    -   如需如何自訂開機映像的詳細資訊，請參閱[自訂開機映像](../get-started/customize-boot-images.md)。  

    -   將開機映像發佈到發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

2.  **準備作業系統映像**  

     作業系統映像包含在目的地電腦安裝作業系統的必要檔案。 請使用下列資訊準備作業系統映像：  

    -   若要深入了解如何建立作業系統映像，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  

    -   將作業系統映像發佈至發佈點。 如需詳細資訊，請參閱[發佈內容](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

3.  **建立工作順序以透過網路部署作業系統**  

     使用網路上自動化作業系統安裝的工作順序。 請使用[建立工作順序以安裝作業系統](create-a-task-sequence-to-install-an-operating-system.md)中的步驟，建立工作順序以部署作業系統。 根據所選部署方法之不同，工作順序可能有其他考量。  

    > [!NOTE]  
    >  在此案例中，工作順序會格式化電腦上的硬碟，並進行磁碟分割。 若要擷取使用者設定，您必須使用狀態移轉點，然後在 [建立工作順序精靈] 的 [狀態移轉]  頁面上選取 [將使用者設定和檔案儲存在狀態移轉點上]  。 如果您在本機儲存使用者設定和檔案，它們將在格式化硬碟時遺失，且 Configuration Manager 將無法還原設定。 如需詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

##  <a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一來部署作業系統：  

    -   [使用 PXE 透過網路部署 Windows](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [使用多點傳送透過網路來部署 Windows](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [建立 OEM 原廠或本機 Depot 的映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [使用獨立媒體，而不使用網路來部署 Windows](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [透過網路使用可開機媒體部署 Windows](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [使用軟體中心透過網路部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>監視  

-   **監視工作順序部署**  

     若要監視工作順序部署以安裝作業系統，請參閱[監視作業系統部署](monitor-operating-system-deployments.md)。  
