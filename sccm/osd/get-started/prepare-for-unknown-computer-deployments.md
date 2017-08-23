---
title: "準備未知電腦部署 | Microsoft Docs"
description: "了解如何將作業系統部署至 System Center Configuration Manager 環境中不是由 Configuration Manager 管理的電腦。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 445e76950f0605da917f3d0e7e71557d969e3c2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-for-unknown-computer-deployments-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的未知電腦部署準備

*適用於：System Center Configuration Manager (最新分支)*

使用本主題中的資訊將作業系統部署至 System Center Configuration Manager 環境中的未知電腦。 未知電腦是指不是由 Configuration Manager 管理的電腦。 這表示 Configuration Manager 資料庫中沒有這些電腦的記錄。 未知電腦包括：  

-   未安裝 Configuration Manager 用戶端的電腦  

-   未匯入至 Configuration Manager 的電腦  

-   Configuration Manager 尚未探索到的電腦  

 您可以使用下列的部署方法，以將作業系統部署至未知的電腦：  

-   [使用 PXE 透過網路部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

-   [使用可開機媒體部署作業系統](../deploy-use/create-bootable-media.md)  

-   [使用預先設置的媒體部署作業系統](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>未知電腦部署工作流程  
 以下是將作業系統部署至未知電腦時的基本工作流程：  

-   選取部署中要使用的未知電腦物件。 您可以將作業系統部署到 [所有未知電腦]  集合中的未知電腦物件之一，也可以將 [所有未知電腦]  集合的物件加入另一個集合。 Configuration Manager 提供在 [所有未知電腦] 集合中的兩個未知電腦物件。 其中一個物件用於 x86 電腦，另一個物件用於 x64 電腦。  

    > [!NOTE]  
    >  [x86 未知電腦]  物件用於僅具備 x86 能力的電腦。 **[x64 未知電腦]** 物件用於具備 x86 和 x64 能力的電腦。 換句話說，這些物件會描述目的地電腦的架構。 而不是您要部署到目的地電腦上的作業系統。  

-   設定支援 PXE 的發佈點或建立媒體，以支援未知電腦部署。  

-   部署工作順序以安裝作業系統  

## <a name="unknown-computer-installation-process"></a>未知電腦安裝程序  
 電腦初次從 PXE 或媒體啟動時，Configuration Manager 會查看 Configuration Manager 資料庫中是否有該電腦的記錄存在。 如果有記錄，Configuration Manager 會接著查看是否有任何部署至該記錄的工作順序。 如果沒有記錄，Configuration Manager 會查看是否有任何部署至未知電腦物件的工作順序。 任一情況下，Configuration Manager 都會接著執行下列其中一個動作：  

-   如果有可用的工作順序，Configuration Manager 會提示使用者執行工作順序。  

-   如果有必要的工作順序，Configuration Manager 會自動執行該工作順序。  

-   如果該記錄沒有部署的工作順序，Configuration Manager 會產生錯誤，表示目的地電腦沒有部署的工作順序。  

 未知電腦啟動時，Configuration Manager 會將該電腦識別為未佈建的電腦，而不是未知電腦。 這表示該電腦現在可以接收之前部署至未知電腦物件的工作順序。 部署的工作順序接著就會安裝必須包含 Configuration Manager 用戶端的作業系統映像。  

 安裝 Configuration Manager 用戶端之後，就會建立該電腦的記錄，且該電腦會在適當的 Configuration Manager 集合中列出。 如果電腦無法安裝作業系統映像或 Configuration Manager 用戶端，則會建立此電腦的「未知」記錄，且此電腦會出現在 [所有系統] 集合中。  

> [!NOTE]  
>  在安裝作業系統映像期間，工作順序可以從這部電腦擷取集合變數，但是不能擷取電腦變數。  

##  <a name="BKMK_EnablingUnknown"></a> 啟用未知電腦支援  
 使用下列項目以在使用 PXE、可開機媒體和預先設置媒體來部署作業系統時啟用未知電腦的支援。  

-   **PXE**  

     在針對 PXE 啟用之發佈點的 [PXE]  索引標籤上，選取 [啟用未知電腦支援]  核取方塊。 如需詳細資訊，請參閱[設定發佈點接受 PXE 要求](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)。  

-   **可開機媒體**  

     在 [建立工作順序媒體精靈] 的 [安全性]  頁面上選取 [啟用未知電腦支援]  核取方塊。 如需詳細資訊，請參閱[設定發佈點接受 PXE 要求](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)以及[利用 System Center Configuration Manager 使用 PXE 透過網路來部署 Windows](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

-   **預先設置的媒體**  

     在 [建立工作順序媒體精靈] 的 [安全性]  頁面上選取 [啟用未知電腦支援]  核取方塊。 如需詳細資訊，請參閱 [Create prestaged media with System Center Configuration Manager](../deploy-use/create-prestaged-media.md)。  
