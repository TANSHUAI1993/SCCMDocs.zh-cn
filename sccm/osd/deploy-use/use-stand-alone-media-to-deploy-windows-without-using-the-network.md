---
title: "使用獨立媒體，而不使用網路來部署 Windows | Microsoft Docs"
description: "在 Configuration Manager 中使用獨立媒體來部署頻寬有限或作為重新整理、安裝或升級電腦之選項的作業系統。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
caps.latest.revision: "16"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 30ae794381c6894e11b21a8167d0af60463c5279
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中使用獨立媒體，而不使用網路來部署 Windows

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的獨立媒體包含在電腦上部署作業系統所需的完整內容。 這包含開機映像、作業系統映像，以及安裝作業系統的工作順序，包括應用程式、驅動程式等。 獨立媒體部署可讓您在下列條件下部署作業系統：  

-   在不適合透過網路複製作業系統映像或其他大型套件的環境中。  

-   在沒有網路連線或網路連線頻寬不足的環境中。  

您可以在下列作業系統部署案例中使用獨立媒體：  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)  

 完成任何一項作業系統部署案例中的步驟，然後使用以下各節準備和建立獨立媒體。  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>使用獨立媒體時，不支援的工作順序動作  
 如果您已完成任何一項受支援作業系統部署案例中的步驟，則已建立部署或升級作業系統的工作順序，且已將所有相關聯的內容發佈至發佈點。 當您使用獨立媒體時，工作順序中不支援下列動作：  

-   工作順序中的自動套用驅動程式步驟。 不支援自動從驅動程式類別目錄套用裝置驅動程式，但您可以選擇 [套用驅動程式封裝] 步驟，讓 Windows 安裝程式可以使用一組指定的驅動程式。  

-   安裝軟體更新。  

-   在部署系統之前安裝軟體。  

-   為使用者與目的地電腦建立關聯，以支援使用者裝置親和性。  

-   動態套件會透過 [安裝套件] 工作來進行安裝。  

-   動態應用程式會透過 [安裝應用程式] 工作來進行安裝。  

> [!NOTE]  
>  如果您部署作業系統的工作順序包含[安裝套件](../understand/task-sequence-steps.md#BKMK_InstallPackage)步驟，而且您在管理中心網站建立獨立媒體，就有可能會發生錯誤。 管理中心網站並未包含執行工作順序期間啟用軟體發佈代理程式所需的所有用戶端設定原則。 CreateTsMedia.log 檔案中，可能會出現下列錯誤：  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  若獨立媒體包含 **安裝套件** 步驟，您必須在啟用軟體發佈代理程式的主要站台建立獨立媒體，或是在工作順序的 [設定 Windows 和 ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) 步驟之後以及第一個 **安裝套件** 步驟之前新增 [執行命令列](../understand/task-sequence-steps.md#BKMK_RunCommandLine) 步驟。 [執行命令列]  步驟會執行 WMIC 命令，在第一個安裝套件步驟執行之前啟用軟體發佈代理程式。 您可以在 [執行命令列]  工作順序中使用下列內容：  
>   
>  **命令列**：**WMIC /命名空間:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>設定部署設定  
 當您使用獨立媒體啟動作業系統部署程序時，必須將部署設定為要讓媒體可以使用作業系統。 您可以在 [部署軟體精靈] 的 [部署設定]  頁面上設定此項目，或是在部署的內容之 [部署設定]  索引標籤上設定此項目。  如果是 [供下列項目使用]  設定，請設定下列其中之一：  

-   **Configuration Manager 用戶端、媒體與 PXE**  

-   **僅媒體與 PXE**  

-   **僅媒體與 PXE (隱藏)**  

## <a name="create-the-stand-alone-media"></a>建立獨立媒體  
 您可以指定獨立媒體為 USB 快閃磁碟機或 CD/DVD 組。 將啟動媒體的電腦，必須能提供選項供您選擇作為可開機磁碟機。 如需詳細資訊，請參閱[建立獨立媒體](create-stand-alone-media.md)。  

## <a name="install-the-operating-system-from-stand-alone-media"></a>從獨立媒體安裝作業系統  
 在電腦的可開機磁碟機中插入獨立媒體，然後打開電源來安裝作業系統。  
