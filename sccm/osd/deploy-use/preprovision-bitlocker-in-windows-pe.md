---
title: "在 Windows PE 中預先佈建 BitLocker | Microsoft Docs"
description: "Configuration Manager 中的 [預先佈建 BitLocker] 工作可先從 Windows 預先安裝環境啟用 BitLocker，再進行作業系統部署。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: baca498dbc5b8e168852aa3c18ee23a9c483e69c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="preprovision-bitlocker-in-windows-pe-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 在 Windows PE 中預先佈建 BitLocker

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的 [預先佈建 BitLocker] 工作順序步驟可讓您在部署作業系統之前，先從 Windows 預先安裝環境 (Windows PE) 啟用 BitLocker。 由於只加密已使用的磁碟空間，因此加密速度較快。 這是藉由在執行 Windows 安裝程序之前，將隨機產生的透明保護裝置套用至格式化的磁碟區並加密磁碟區的方式進行。 預先佈建 BitLocker 是 Windows 8 和 Windows Server 2012 引進的功能。 不過，只要執行特定步驟，您仍可以在硬碟上預先佈建 BitLocker 並安裝 Windows 7。 Windows 7 安裝程式完成後，您必須設定 BitLocker 金鑰保護裝置，因為 Windows 7 BitLocker 控制台不支援使用透明保護裝置的 BitLocker。 您必須依照 [啟用 BitLocker]  步驟或使用 manage-bde.exe 命令列工具新增金鑰保護裝置。  

 一般而言，您必須執行下列步驟才能順利在即將安裝 Windows 7 的電腦上預先佈建 BitLocker：  

-   在 Windows PE 中重新啟動電腦  

    > [!IMPORTANT]  
    >  您必須使用包含 Windows PE 4 或更新版本的開機映像才能預先佈建 BitLocker。 如需 Configuration Manager 中所支援 Windows PE 版本的詳細資訊，請參閱 [Configuration Manager 外部的相依性](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies)。  

-   分割和格式化硬碟  

-   中的 [預先佈建 BitLocker]  

-   使用特定作業系統和網路設定安裝 Windows 7  

-   將金鑰保護裝置新增至 BitLocker  

 在 Configuration Manager 中，於硬碟上預先佈建 BitLocker 並安裝 Windows 7 的建議做法是建立新的工作順序，然後從 [建立工作順序精靈] 的 [建立新工作順序] 頁面選取 [安裝現有的映像套件]。 此精靈將會建立下表所列的工作順序步驟。  

> [!NOTE]  
>  根據您在精靈中進行設定的方式，工作順序可能會有額外的步驟。 例如，如果您在精靈的 [狀態移轉]  頁面上選取了 [擷取的 Microsoft Windows 設定]  ，就可能會有 [擷取 Windows 設定]  這個步驟。  

|工作順序步驟|詳細資料|  
|------------------------|-------------|  
|停用 BitLocker|此步驟會停用 BitLocker 加密 (若目前啟用的話)。 如需詳細資訊，請參閱[停用 BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker)。|  
|在 Windows PE 中重新啟動電腦|此步驟會執行指派給工作順序的開機映像，在 Windows PE 中重新啟動電腦。 您必須使用包含 Windows PE 4 或更新版本的開機映像才能預先佈建 BitLocker。 如需詳細資訊，請參閱[重新啟動電腦](../understand/task-sequence-steps.md#BKMK_RestartComputer)。|  
|分割磁碟 0 – BIOS<br /><br /> 分割磁碟 0 – UEFI|這些步驟使用 BIOS 或 UEFI 針對目的地電腦的指定磁碟執行格式化和分割的動作。 當工作順序偵測到目的地電腦處於 UEFI 模式時，即會使用 UEFI。 如需詳細資訊，請參閱[格式化和分割磁碟](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk)。|  
|中的 [預先佈建 BitLocker]|這個步驟會在 Windows PE 中啟用磁碟上的 BitLocker。 只有已使用的磁碟空間會加密。 由於您已在上一個步驟分割和格式化硬碟，在無資料的情況下，加密很快就可以完成。 如需詳細資訊，請參閱[預先佈建 BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker)。|  
|套用作業系統|此步驟會準備用來在目的地電腦上安裝作業系統的回應檔，並將 OSDTargetSystemDrive 工作順序變數設定為包含作業系統檔案之分割區的磁碟機代號。 設定 Windows 和 ConfigMgr 步驟將使用此回應檔和變數來安裝作業系統。 如需詳細資訊，請參閱 [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)。|  
|套用 Windows 設定|此步驟會將 Windows 設定新增至回應檔。 設定 Windows 和 ConfigMgr 步驟將使用回應檔安裝作業系統。 如需詳細資訊，請參閱[套用 Windows 設定](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)。|  
|套用網路設定|此步驟會將網路設定新增至回應檔。 設定 Windows 和 ConfigMgr 步驟將使用回應檔安裝作業系統。 如需詳細資訊，請參閱[套用網路設定步驟](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings)。|  
|套用裝置驅動程式|此步驟將比對並安裝驅動程式，作為作業系統部署的一部分。 如需詳細資訊，請參閱[自動套用驅動程式](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers)。|  
|設定 Windows 和 ConfigMgr|此步驟會從 Windows PE 轉換為新的作業系統。 此工作順序步驟是部署任何作業系統的必要部分。 它會將 Configuration Manager 用戶端安裝到新的作業系統中，並準備好讓工作順序繼續在新的作業系統中執行。 如需詳細資訊，請參閱[設定 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)。|  
|啟用 BitLocker|此步驟將在硬碟上啟用 BitLocker 加密，並且設定金鑰保護裝置。 由於硬碟已預先佈建 BitLocker，此步驟可以很迅速地完成。 Windows 7 會要求您新增金鑰保護裝置。 若您不使用此步驟，可以執行 manage-bde.exe 命令列工具設定金鑰保護裝置。 如需詳細資訊，請參閱[啟用 BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker)。|  
