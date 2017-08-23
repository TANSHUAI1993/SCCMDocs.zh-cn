---
title: "透過網路使用可開機媒體部署 Windows | Microsoft Docs"
description: "使用 System Center Configuration Manager 中的可開機媒體部署，以在啟動目的地電腦時部署作業系統。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: "5"
author: mattbriggs
ms.author: mattbriggs
manager: angrobe
ms.openlocfilehash: 9b20e5e2a66d92038033e816e6fc701581c48a7f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>透過網路利用 System Center Configuration Manager 使用可開機媒體部署 Windows

適用於：System Center Configuration Manager (最新分支)

您可以在啟動目的地電腦時使用可開機媒體來部署作業系統。 該媒體包含指向工作順序 (作業系統映像) 的指標，以及其他來自網路的必要內容。 啟動目的地電腦時，電腦會擷取指標中參考的項目。 因為可開機媒體不含內容，所以不需要在媒體上取代目標即可更新它。

在下列作業系統部署案例中使用多點傳送，可以透過網路部署作業系統：

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [在新電腦 (裸機) 上安裝新的 Windows 版本](install-new-windows-version-new-computer-bare-metal.md)  

-   [取代現有的電腦和傳輸設定](replace-an-existing-computer-and-transfer-settings.md)  

完成任一作業系統部署案例中的步驟，然後使用以下各節利用可開機媒體部署作業系統。  

## <a name="configure-deployment-settings"></a>設定部署設定  
當您使用可開機媒體啟動作業系統部署程序時，請將部署設定成作業系統可供媒體使用。 您可以在 [部署軟體精靈] 的 [部署設定] 頁面上，或是在部署內容的 [部署設定] 索引標籤上設定此選項。 如果是 [供下列項目使用]  設定，請設定下列其中之一：

-   Configuration Manager 用戶端、媒體與 PXE

-   僅媒體與 PXE

-   僅媒體與 PXE (隱藏)

## <a name="create-the-bootable-media"></a>建立可開機媒體
您可以指定可開機媒體為 USB 快閃磁碟機或 CD/DVD 組。 啟動媒體的電腦必須支援您選擇作為可開機磁碟機的選項。 如需詳細資訊，請參閱[建立可開機媒體](create-bootable-media.md)。  

##  <a name="BKMK_Deploy"></a> 從可開機媒體安裝作業系統  
在電腦的可開機磁碟機中插入可開機媒體，然後打開電源來安裝作業系統。
