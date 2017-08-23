---
title: "自訂作業系統映像 - Configuration Manager | Microsoft Docs"
description: "使用擷取組建工作順序、手動設定或兩者的組合，來自訂作業系統映像。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 485cb3ca4988f983c1ec71b6c8daf136571bf0ea
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="customize-operating-system-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自訂作業系統映像

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的作業系統映像為 WIM 檔案，且代表參照檔和資料夾的已壓縮集合，而若要在電腦上順利安裝及設定作業系統，便需要使用該檔案。 自訂作業系統映像的建立及擷取會在參照電腦上完成，同時您必須使用所有必要的作業系統檔案、支援檔案、軟體更新、工具，以及其他軟體應用程式來設定此參照電腦。 手動設定參照電腦到何程度，完全由您決定。 您可以利用組建並擷取工作順序來完全自動設定參照電腦，可以手動設定參照電腦的某些設定，然後再使用工作順序自動執行其他設定，也可以手動設定參照電腦但不使用工作順序。 參閱下列章節來自訂作業系統。

##  <a name="BKMK_PrepareReferenceComputer"></a> 為參照電腦做準備  
 從參照電腦擷取作業系統映像之前，需要考量一些事項。  

###  <a name="BKMK_RefComputerDecide"></a> 決定要進行自動或手動設定  
 以下內容概述自動和手動設定參照電腦的優缺點。  

#### <a name="automated-configuration"></a>自動設定  
 **優點**  

-   讓設定自動完成可免除系統管理員或使用者必須在電腦前操作的需求。  

-   您可以重複使用工作順序，以重複執行其他高信賴等級參照電腦的設定。  

-   您可以修改工作順序以符合不同的參照電腦，而不需重新建立整個工作順序。  

 **缺點**  

-   建立工作順序的初始化動作在建立及測試時可能需要較長的時間。  

-   如果參照電腦需求有大幅度的變更，則需要較長時間重新建立及重新測試工作順序。  

#### <a name="manual-configuration"></a>手動設定  
 **優點**  

-   您不需要建立工作順序或花時間進行測試，以及疑難排解工作順序。  

-   您可以直接從 CD 安裝，不需將所有軟體套件 (包含 Windows 本身) 放入 Configuration Manager 套件中。  

 **缺點**  

-   參照電腦組態的準確性，取決於設定電腦的系統管理員或使用者。  

-   您仍然需要確認及測試參照電腦的設定是否正確。  

-   您不可重複使用設定方法。  

-   整個過程中，需要有人積極參與。  

###  <a name="BKMK_RefComputerConsiderations"></a> 關於參照電腦的考量  
 以下列出當您設定參照電腦時要考量的基本項目。  

-   **要部署的作業系統**  

     參照電腦必須安裝您想要部署到目的地電腦的作業系統。 如需可供部署之作業系統的詳細資訊，請參閱[作業系統部署的基礎結構需求](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

-   **適當的 Service Pack**  

     參照電腦必須安裝您想要部署到目的地電腦的作業系統。  

-   **適當的軟體更新**  

     安裝您想要從參照電腦擷取時包含在作業系統映像中的所有軟體應用程式。 您也可以在將擷取之作業系統映像部署至目的地電腦時，安裝軟體應用程式。  

-   **工作群組成員資格**  

     參照電腦必須設定為工作群組的成員。  

-   **Sysprep**  

     系統準備 (Sysprep) 工具是一種可讓您和其他部署工具搭配使用，以在新硬體上安裝 Windows 作業系統的技術。 Sysprep 會藉由將電腦設定為電腦重新啟動時建立新的電腦安全性識別碼 (SID)，備妥電腦以用於磁碟映像的製作，或傳遞給客戶。 另外，Sysprep 會清除使用者和電腦特定的設定和資料，千萬不可將這些資料複製到目的地電腦。  

     您可以執行下列命令，手動對參照電腦進行 Sysprep：  

     `Sysprep /quiet /generalize /reboot`  

     /generalize 選項會指示 Sysprep 移除 Windows 安裝中的系統特定資料。 系統特定資訊包含事件記錄檔、唯一安全性識別碼 (SID) 和其他唯一資訊。 移除唯一系統資訊之後，會重新啟動電腦。  

     您可以使用 [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) 工作順序步驟或擷取媒體，自動執行 Sysprep。  

    > [!IMPORTANT]  
    >  [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) 工作順序步驟在執行 Sysprep 之前，會試圖將參照電腦上的本機系統管理員密碼重設為空白值。 如果已啟用本機安全性原則 [密碼必須符合複雜性需求]  ，則此工作順序無法重設系統管理員密碼。 在此案例中，請先停用此原則，再執行工作順序。  

     如需 Sysprep 的詳細資訊，請參閱 [系統準備 (Sysprep) 技術參考](http://go.microsoft.com/fwlink/?LinkId=280286)。  

-   **需要適當的工具和指令碼以減少安裝案例**  

     需要適當的工具和指令碼以減少安裝案例  

-   **適當的桌面自訂，例如桌布、商標和預設的使用者設定檔**  

     您可以利用當您從參照電腦擷取作業系統映像時想要納入的桌面自訂內容，設定參照電腦。 桌面內容包含桌布、組織商標和標準的預設使用者設定檔。  

##  <a name="BKMK_ManuallyBuildReference"></a> 手動建立參照電腦  
 請使用下列程序，手動建立參照電腦。  

> [!NOTE]  
>  手動建立參照電腦時，可以使用擷取媒體來擷取作業系統映像。 如需詳細資訊，請參閱[建立擷取媒體](../deploy-use/create-capture-media.md)。  

#### <a name="to-manually-build-the-reference-computer"></a>手動建立參照電腦  

1.  識別要當作參照電腦使用的電腦。  

2.  使用適當的作業系統和建立您要部署之作業系統映像所需的其他軟體，設定參照電腦。  

    > [!WARNING]  
    >  至少要安裝適當的作業系統和 Service Pack、支援驅動程式和必要的軟體更新。  

3.  將參照電腦設定為工作群組的成員。  

4.  重設參照電腦上的本機系統管理員密碼，使密碼值為空白。  

5.  使用下列命令執行 Sysprep：  **sysprep /quiet /generalize /reboot**。 /generalize 選項會指示 Sysprep 移除 Windows 安裝中的系統特定資料。 系統特定資訊包含事件記錄檔、唯一安全性識別碼 (SID) 和其他唯一資訊。 移除唯一系統資訊之後，會重新啟動電腦。  

 參照電腦就緒後，請使用工作順序從參照電腦擷取作業系統映像。  如需詳細步驟，請參閱 [從現有的參照電腦擷取作業系統映像](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer)。  

##  <a name="BKMK_UseTSToBuildReference"></a> 使用工作順序來建立參照電腦  
 您可以使用工作順序將建立參照電腦的程序自動化，以部署作業系統、驅動程式、應用程式等等。  使用下列步驟來建置參照電腦，然後從參照電腦擷取作業系統映像。  

-   使用工作順序從參照電腦建置和擷取作業系統映像。  如需詳細步驟，請參閱 [使用工作順序來建立和擷取參照電腦](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS)。  
