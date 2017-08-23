---
title: "透過網路使用軟體中心部署 Windows | Microsoft Docs"
description: "您可以將作業系統部署至 Software Center，以使用新版本的 Windows 重新整理現有電腦，或將 Windows 升級至最新版本。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: "5"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 8988409c68b7f69439ed03872c316b2139d25616
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>使用軟體中心透過網路利用 System Center Configuration Manager 部署 Windows

適用於：System Center Configuration Manager (最新分支)

針對會在 System Center Configuration Manager 中安裝作業系統的工作順序，您可以讓軟體中心提供此工作順序。 您可以透過下列作業系統部署案例將作業系統部署到軟體中心：

-   [使用新的 Windows 版本重新整理現有的電腦](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [將 Windows 升級至最新版本](upgrade-windows-to-the-latest-version.md)

完成其中一個作業系統部署案例的步驟。 然後使用以下各節的內容來針對於軟體中心提供的部署進行準備。

## <a name="configure-deployment-settings"></a>設定部署設定  
請設定部署來使作業系統部署可在軟體中心取得。 您可以在 [部署軟體精靈] 的 [部署設定] 頁面上，或是在部署內容的 [部署設定] 索引標籤上設定部署。 如果是 [供下列項目使用]  設定，請設定 [只有 Configuration Manager 用戶端]  或是 [Configuration Manager 用戶端、媒體與 PXE] 。 當系統部署作業系統之後，目標集合的成員就可以在軟體中心中看到該作業系統。

##  <a name="BKMK_Deploy"></a> 將工作順序部署到電腦  
將作業系統部署至目標集合。 如需詳細資訊，請參閱 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)。 當您針對軟體中心部署作業系統時，可以將該部署設定為必要或可用的部署。

-   **需要部署**：需要部署會在軟體中心內提供作業系統，而且會在設定的指派排程時自動啟動。

-   **提供進行部署**：軟體中心內會提供作業系統，使用者可於需求時安裝該作業系統。
