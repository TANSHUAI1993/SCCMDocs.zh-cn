---
title: "管理作業系統升級套件 | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 管理作業系統升級套件。"
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5fef04f26b12bced073332fd1f7b4e7c7bd7d398
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理作業系統升級套件

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的升級套件包含用來升級電腦上之現有作業系統的 Windows 安裝程式來源檔案。 使用下列區段管理 Configuration Manager 中的作業系統升級套件。

##  <a name="BKMK_AddOSUpgradePkgs"></a> 新增作業系統升級封裝至 Configuration Manager  
 在您可以使用作業系統升級套件之前，必須先將此套件加入 Configuration Manager 站台。 請使用下列程序將作業系統升級封裝加入站台。  

#### <a name="to-add-an-operating-system-upgrade-package"></a>加入作業系統升級封裝  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [作業系統升級封裝] 。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [新增作業系統升級封裝]  啟動 [新增作業系統升級封裝精靈]。  

4.  在 [資料來源]  頁面上，指定作業系統升級封裝之安裝來源檔的網路路徑。 例如，將 UNC **\\\server\path** 指定為安裝來源檔所在位置。  

    > [!NOTE]  
    >  安裝來源檔案包含 Setup.exe 和其他檔案和資料夾，以便安裝作業系統。  

    > [!IMPORTANT]  
    >  限制存取安裝來源檔案，以避免不必要的竄改。  

5.  在 [一般]  頁面上指定下列資訊，然後按 [下一步] 。 這項資訊可在您有多個作業系統安裝程式時做為識別用途。  

    -   **名稱**：指定作業系統安裝程式的名稱。  

    -   **版本**：指定作業系統安裝程式的版本。  

    -   **註解**：指定作業系統安裝程式的簡短描述。  

6.  完成精靈。  

 現在您可以將作業系統安裝程式發佈至部署工作順序所存取的發佈點。  

##  <a name="BKMK_DistributeBootImages"></a> 將作業系統映像發佈至發佈點  
 作業系統映像發佈至發佈點的方式，與您發佈其他內容的方式相同。 在大部分情況下，您必須在部署作業系統之前，將作業系統映像發佈至至少一個發佈點。 如需發佈作業系統映像的步驟，請參閱 [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> 套用軟體更新至作業系統升級套件  
 自 Configuration Manager 1602 版開始，您可以將新的軟體更新套用至作業系統升級套件中的作業系統映像。 在您可將軟體更新套用至升級套件之前，必須先使軟體更新基礎結構就緒、已成功同步處理軟體更新，並已將軟體更新下載至站台伺服器上的內容庫。 如需詳細資訊，請參閱 [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (部署軟體更新)。  

 您可以依指定的排程將適用的軟體更新套用至升級套件。 Configuration Manager 會依照您指定的排程，將選取的軟體更新套用至作業系統升級套件，然後選擇性地將更新的升級套件發佈至發佈點。 有關作業系統升級套件的資訊會儲存在站台資料庫中，包括匯入時已套用的軟體更新。 最初新增時已套用至升級套件的軟體更新也會儲存在站台資料庫中。 當您啟動精靈將軟體更新套用至作業系統升級套件時，精靈會擷取尚未套用至升級套件的可用軟體更新清單供您選取。 Configuration Manager 會從站台伺服器上的內容庫複製軟體更新，並將此軟體更新套用至作業系統升級套件。  

 利用下列程序將軟體更新套用至作業系統升級套件。  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>套用軟體更新至作業系統升級套件  

1.  在 Configuration Manager 主控台中，按一下 [軟體程式庫] 。  

2.  在 [軟體程式庫]  工作區中，展開 [作業系統] ，然後按一下 [作業系統升級封裝] 。  

3.  選取要套用軟體更新的作業系統升級套件。  

4.  在 **[首頁]** 索引標籤的 **[作業系統升級套件]** 群組中，按一下 **[排程更新]** 以啟動精靈。  

5.  在 [選擇更新]  頁面上，選取要套用至作業系統映像的軟體更新，然後按 [下一步] 。  

6.  在 [設定排程]  頁面上指定下列設定，然後按 [下一步] 。  

    1.  **排程**：指定將軟體更新套用至作業系統映像的排程。  

    2.  **發生錯誤時繼續**：選取此選項，即使發生錯誤仍會將軟體更新套用至映像。  

    3.  **將映像發佈至發佈點**：選取此選項，在套用軟體更新之後更新發佈點上的作業系統映像。  

7.  確認 [摘要]  頁面中的資訊，然後按 [下一步] 。  

8.  在 [完成]  頁面上，確認軟體更新已成功套用至作業系統映像。  
