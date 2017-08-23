---
title: "透過網路使用多點傳送來部署 Windows | Microsoft Docs"
description: "在 System Center Configuration Manager 環境中使用多點傳送，讓多部電腦可以同時下載作業系統映像。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
caps.latest.revision: "13"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 55266696aa7340fddda3a57ff90e20222ff665a5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>利用 System Center Configuration Manager 使用多點傳送透過網路來部署 Windows

*適用於：System Center Configuration Manager (最新分支)*

多點傳送是一種網路最佳化方法，若您的 System Center Configuration Manager 環境中可能會有多個用戶端同時下載同一個作業系統映像，則可以使用這個方法。 使用多點傳送時，多部電腦可以同時下載由發佈點多點傳送的作業系統映像，不需由發佈點一一透過個別連線傳送資料複本至每個用戶端。  

 在下列作業系統部署案例中使用多點傳送，可以透過網路部署作業系統：  

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

 完成任一作業系統部署案例中的步驟，然後使用下列章節支援多點傳送。  

##  <a name="BKMK_Configure"></a> 設定發佈點以支援多點傳送  
 若要在部署作業系統時使用多點傳送，您必須將發佈點設定為支援多點傳送。 如需詳細資訊，請參閱[設定發佈點以支援多點傳送](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)。  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>準備多點傳送部署的作業系統映像  
 若要設定作業系統映像套件來支援多點傳送，請參閱[準備多點傳送部署的作業系統映像](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)。  

##  <a name="BKMK_Deploy"></a> 部署工作順序  
 將作業系統部署至目標集合。 如需詳細資訊，請參閱 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。  
