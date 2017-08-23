---
title: "將 Windows 升級至最新版本 | Microsoft Docs"
description: "了解如何使用 Configuration Manager，將作業系統從 Windows 7 或更新版本升級到 Windows 10。"
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 026d61113a918e43ac4395ef092b1931f33f16d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 將 Windows 升級至最新版本

適用於：System Center Configuration Manager (最新分支)

本主題提供 System Center Configuration Manager 的步驟，可將電腦上的作業系統從 Windows 7 或更新版本升級至 Windows 10 的步驟，或是將目的地電腦上的 Windows Server 2012 升級至 Windows Server 2016。 有不同的部署方法可供您選擇，例如獨立媒體或軟體中心。 就地升級案例：  

-   升級目前執行下列作業系統的電腦：
    - Windows 7、Windows 8 或 Windows 8.1。 您也可以執行 Windows 10 的組建至組建升級。 例如，您可以將 Windows 10 RTM 升級到 Windows 10 1511 版。  
    - Windows Server 2012。 您也可以執行 Windows Server 2016 的組建至組建升級。 如需支援的升級路徑詳細資訊，請參閱[支援的升級路徑](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)。    

-   保留電腦上的應用程式、設定和使用者資料。  

-   沒有外部相依性，例如 Windows ADK。  

-   比傳統作業系統部署更快且更有彈性。  

 使用下列章節，使用工作順序透過網路來部署作業系統。  

##  <a name="BKMK_Plan"></a> 方案  

-   **檢閱升級作業系統之工作順序的限制**  

     檢閱升級作業系統之工作順序的下列需求和限制，以確定它符合您的需要：  

    -   您只應新增在安裝映像之後，與部署作業系統及設定電腦的核心工作相關的工作順序步驟。 這包括安裝套件、應用程式或更新的步驟，以及執行命令列、PowerShell 或設定動態變數的步驟。  

    -   檢閱電腦上安裝的驅動程式和應用程式，確保其與 Windows 10 相容，然後再部署升級工作順序。  

    -   下列工作與就地升級不相容，因此需要您使用傳統作業系統部署：  

        -   變更電腦網域成員資格或更新本機系統管理員。  

        -   在電腦上實作基本變更，包括磁碟分割、將架構從 x86 變更為 x64、實作 UEFI，或修改基礎作業系統語言。  

        -   您有自訂需求，包括使用自訂基底映像、使用協力廠商<sup></sup> 磁碟加密，或需要 WinPE 離線作業。  

-   **規劃並實作基礎結構需求**  

     升級案例的唯一先決條件，便是您必須有發佈點，以供作業系統升級套件和工作順序中包含的任何其他套件之用。 如需詳細資訊，請參閱[安裝或修改發佈點](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)。

##  <a name="BKMK_Configure"></a> 設定  

1.  **準備作業系統升級套件**  

     Windows 10 升級套件包含在目的地電腦升級作業系統時的必要檔案。 升級套件的版本、架構和語言必須與要升級的用戶端相同。  如需詳細資訊，請參閱[管理作業系統升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

2.  **建立工作順序以升級作業系統**  

     使用[建立工作順序以升級作業系統](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步驟，自動化升級作業系統。  

    > [!IMPORTANT]
    > 當您使用獨立媒體時，工作順序必須內含開機映像，在 [工作順序媒體精靈] 中才可使用該媒體。

    > [!NOTE]  
    > 一般都是使用[建立工作順序以升級作業系統](create-a-task-sequence-to-upgrade-an-operating-system.md)中的步驟來建立工作順序，以便將作業系統升級為 Windows 10。 該工作順序包含 [升級作業系統] 步驟，以及其他建議的步驟和群組，以處理端對端升級程序。 不過，您可以建立自訂工作順序，並新增[升級作業系統](../understand/task-sequence-steps.md#BKMK_UpgradeOS)工作順序步驟，將作業系統升級。 這是將作業系統升級為 Windows 10 的唯一必要步驟。 如果您選擇這個方法，請在 [升級作業系統] 步驟之後也同時新增[重新啟動電腦](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)步驟，完成升級。 請務必使用 [目前安裝的預設作業系統] 設定，將電腦重新啟動為已安裝的作業系統，而不是 Windows PE。  

##  <a name="BKMK_Deploy"></a> 部署  

-   使用下列部署方法之一來部署作業系統：  

    -   [透過網路使用軟體中心部署 Windows](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [使用獨立媒體，而不使用網路來部署 Windows](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>監視  

-   **監視工作順序部署**  

     若要監視工作順序部署以升級作業系統，請參閱[監視作業系統部署](monitor-operating-system-deployments.md)。  
