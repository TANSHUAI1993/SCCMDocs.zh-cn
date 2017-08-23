---
title: "作業系統部署簡介 | Microsoft Docs"
description: "在 Configuration Manager 環境中部署作業系統之前，請先了解相關概念。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2baa6b7dbd66ab41bc9b67e8f43c313be233153c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-operating-system-deployment-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的作業系統部署簡介

適用於：System Center Configuration Manager (最新分支)

您可以透過許多不同的方式來使用 Configuration Manager 部署作業系統。 請參閱本節的資訊，以了解如何部署作業系統，並將工作自動化。 

##  <a name="BKMK_OSDeploymentProcess"></a> 作業系統部署程序  
 Configuration Manager 提供數種可用於部署作業系統的方法。 無論採用哪一種部署方法，都有幾個必須執行的動作：  

-   識別啟動開機映像或安裝您必須部署之作業系統映像所需的 Windows 裝置驅動程式。  

-   識別您想要用來啟動目的地電腦的開機映像。  

-   使用工作順序擷取要部署的作業系統映像。 或者，您可以使用預設的作業系統映像。  

-   將開機映像、作業系統映像及任何相關內容發佈至發佈點。  

-   建立含有部署開機映像和作業系統映像之步驟的工作順序。  

-   將工作順序部署到電腦集合。  

-   監視部署。  

##  <a name="BKMK_OSDScenarios"></a> 作業系統部署案例  
 在 Configuration Manager 中有許多作業系統部署案例，可讓您依據自己的環境和作業系統安裝目的來選擇。  例如，您可以使用新版本的 Windows 磁碟分割和格式化現有的電腦，或將 Windows 升級至最新版本。 為了協助您決定符合需求的部署方法，請檢閱[部署企業作業系統的案例](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)。  您可以從下列作業系統部署案例選擇：  

-   [升級至最新版本的 Windows](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [使用新的 Windows 版本重新整理現有的電腦](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [取代現有的電腦和傳輸設定](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_OSDMethods"></a> 用於部署作業系統的方法  
 您可以運用數種方法將作業系統部署至 Configuration Manager 用戶端電腦。  

-   **PXE 起始部署**：PXE 起始部署可讓用戶端電腦透過網路要求部署。 在這種部署方法中，會將作業系統映像和 Windows PE 開機映像傳送至設定接受 PXE 開機要求的發佈點。 如需詳細資訊，請參閱[利用 System Center Configuration Manager 使用 PXE 透過網路來部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

-   **在軟體中心內提供作業系統**：您可以部署作業系統，並在軟體中心提供它。 Configuration Manager 用戶端可以從軟體中心起始作業系統安裝。 如需詳細資訊，請參閱[取代現有的電腦和傳輸設定](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)。  

-   **多點傳送部署**：多點傳送部署可以同時將資料傳送至多個用戶端，而不用透過獨立連線將資料複本一一傳送至每個用戶端，因此可以節省網路頻寬。 此一部署方法會將作業系統映像傳送至發佈點。 之後再於用戶端電腦要求部署時部署映像。 如需詳細資訊，請參閱[使用多點傳送透過網路來部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

-   **可開機媒體部署**：可開機媒體部署可讓您在目的地電腦啟動時部署作業系統。 目的地電腦啟動時，會從網路擷取工作順序、作業系統映像，以及任何其他必要的內容。 由於媒體不包含該內容，因此您可以直接更新內容，而不需要重新建立媒體。 如需詳細資訊，請參閱[建立可開機媒體](../deploy-use/create-bootable-media.md)。  

-   **獨立媒體部署**：獨立媒體部署可讓您在下列條件下部署作業系統：  

    -   在不適合透過網路複製作業系統映像或其他大型套件的環境中。  

    -   在沒有網路連線或網路連線頻寬不足的環境中。  

     如需詳細資訊，請參閱[建立獨立媒體](../deploy-use/create-stand-alone-media.md)。  

-   **預先設置媒體部署**：預先設置媒體部署可讓您將作業系統部署至尚未完全佈建的電腦。 預先設置的媒體是一種 Windows Imaging Format (WIM) 檔案，可供廠商或在企業預備中心將其安裝在未連線至 Configuration Manager 環境的裸機電腦上。  

     之後，在 Configuration Manager 環境中，電腦會使用媒體所提供的開機映像啟動，然後連線至站台管理點取得可用的工作順序以完成下載程序。 這種部署方法能夠減少網路流量，因為開機映像和作業系統映像皆已儲存在目的地電腦上。 您可以指定在預先設置媒體中包含應用程式、套件和驅動程式套件。 如需詳細資訊，請參閱[建立預先設置的媒體](../deploy-use/create-prestaged-media.md)。  

##  <a name="BKMK_BootImages"></a> 開機映像  
 Configuration Manager 中的開機映像是 Windows PE (WinPE) 映像，在作業系統部署時使用。 開機映像用來以 WinPE 啟動電腦，WinPE 是最低需求的作業系統，內含有限的元件和服務可讓目的地電腦準備好進行 Windows 安裝。 Configuration Manager 提供兩種開機映像：一種支援 x86 平台，另一種支援 x64 平台。 這些皆視為預設開機映像。 您建立並新增至 Configuration Manager 的開機映像會視為自訂映像。 在您更新 Configuration Manager 時可以自動取代預設開機映像。 如需開機映像的詳細資訊，請參閱[管理開機映像](../get-started/manage-boot-images.md)。  

##  <a name="BKMK_OSImages"></a> 作業系統映像  
 Configuration Manager 中的作業系統映像儲存為 Windows 映像 (WIM) 檔案格式，代表經過壓縮的參照檔案和資料夾集合，其為成功在電腦上安裝及設定作業系統所必需。 在所有作業系統部署案例中，您都必須選取作業系統映像。 您可以使用預設的作業系統映像，或從您設定的參照電腦，建置作業系統映像。 如需詳細資訊，請參閱[管理作業系統映像](../get-started/manage-operating-system-images.md)。  

##  <a name="BKMK_OSUpgradePackages"></a> 作業系統升級套件  
 作業系統升級套件用來升級作業系統，而且是安裝程式初始化的作業系統部署。 您可透過 DVD 或掛接的 ISO 檔案，將作業系統升級套件匯入 Configuration Manager。 如需詳細資訊，請參閱[管理作業系統升級套件](../get-started/manage-operating-system-upgrade-packages.md)。  

##  <a name="BKMK_OSDMedia"></a> 用於部署作業系統的媒體  
 您可以建立數種能用於部署作業系統的媒體， 包括用於擷取作業系統映像的擷取媒體，以及用於部署作業系統的獨立媒體、預先設置媒體及可開機媒體。 如果電腦沒有網路連線或與 Configuration Manager 網站的連線頻寬不足，您可以使用媒體在其上部署作業系統。 如需如何使用媒體的詳細資訊，請參閱[建立工作順序媒體](../deploy-use/create-task-sequence-media.md)。  

##  <a name="BKMK_DeviceDrivers"></a> 裝置驅動程式  
 您可以將裝置驅動程式安裝在目的地電腦上，而不需要將驅動程式包含在要部署的作業系統映像中。 Configuration Manager 提供的驅動程式類別目錄中，包含您匯入 Configuration Manager 之所有裝置驅動程式的參照。 該驅動程式類別目錄位於 [軟體程式庫]  工作區，由兩個節點組成：[驅動程式]  和 [驅動程式封裝] 。 [驅動程式]  節點會列出您已匯入至驅動程式類別目錄中的所有驅動程式。 您可以使用此節點探索有關每個已匯入驅動程式的詳細資料、變更驅動程式所屬的驅動程式套件或開機印象、啟用或停用驅動程式，以及執行其他功能。 如需詳細資訊，請參閱[管理驅動程式](../get-started/manage-drivers.md)。  

##  <a name="BKMK_OSDUserState"></a> 儲存和還原使用者狀態  
 部署作業系統時，可以儲存目的地電腦的使用者狀態、部署作業系統，然後在作業系統部署完畢後還原使用者狀態。 在 Configuration Manager 用戶端電腦上安裝作業系統時通常會運用這個程序。  

 您可以使用工作順序擷取及還原使用者狀態資訊。 擷取到使用者狀態資訊後，可以運用下列任一方法儲存擷取到的資訊：  

-   您可以設定狀態移轉點來遠端存放使用者狀態資料。 擷取工作順序會將資料傳送至狀態移轉點。 等到作業系統部署完畢後，還原工作順序就會擷取資料並還原目的地電腦上的使用者狀態。  

-   您可以將使用者狀態資料存放在本機的特定位置。 在此案例中，擷取工作順序會將使用者資料複製到目的地電腦上的特定位置。 等到作業系統部署完畢後，還原工作順序便會從該位置擷取使用者資料。  

-   您可以指定能用於將使用者資料還原至原始位置的永久連結。 在此案例中，移除舊的作業系統後，使用者資料仍保留在磁碟中。 接著，等到作業系統部署完畢後，還原工作順序會利用永久連結將使用者狀態資料還原至原始位置。  

 如需詳細資訊，請參閱[管理使用者狀態](../get-started/manage-user-state.md)。  

##  <a name="BKMK_UnknownComputer"></a> 部署到未知電腦  
 您可以將作業系統部署至不是由 Configuration Manager 管理的電腦。 這類電腦在 Configuration Manager 資料庫中沒有任何相關記錄。 這些電腦稱為未知電腦。 未知電腦包括：  

-   未安裝 Configuration Manager 用戶端的電腦  

-   未匯入 Configuration Manager 的電腦  

-   Configuration Manager 未探索到的電腦  

 如需詳細資訊，請參閱[準備未知電腦部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

##  <a name="BKMK_UDA"></a> 建立使用者與電腦的關聯  
 部署作業系統時，可以在使用者和目的地電腦之間建立關聯，以支援使用者裝置親和性動作。 當您在使用者和目的地電腦之間建立關聯之後，系統管理使用者可以在與該使用者相關聯的任何電腦上執行動作，例如將應用程式部署到特定使用者的電腦。 不過，當您部署作業系統時，不能將作業系統部署到特定使用者的電腦。 如需詳細資訊，請參閱[為使用者與目的地電腦建立關聯](../get-started/associate-users-with-a-destination-computer.md)。  

##  <a name="BKMK_TaskSequences"></a> 使用工作順序，將步驟自動化  
 您可以在 Configuration Manager 環境中建立工作順序來執行各種工作。 工作順序的動作，會在順序的個別步驟中定義。 當執行工作順序時，會在命令列層級執行各個步驟的動作，而不需要使用者介入。 您可以使用工作順序進行下列作業：  

-   [建立工作順序以安裝作業系統](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [建立非作業系統部署的工作順序](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [建立工作順序以擷取作業系統](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [建立工作順序以擷取和還原使用者狀態](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [建立自訂工作順序](../deploy-use/create-a-custom-task-sequence.md)  
