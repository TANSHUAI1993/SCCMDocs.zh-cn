---
title: "升級評估安裝 | Microsoft Docs"
description: "了解如何將 System Center Configuration Manager 的評估安裝升級至完整安裝。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8f951805c2fc25059965c15c94934c0f8546735c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>將 System Center Configuration Manager 的評估安裝升級完整安裝

*適用對象：System Center Configuration Manager (最新分支)*

如果安裝的是 System Center Configuration Manager 評估版，則在 180 天之後，Configuration Manager 主控台會變成唯讀，直到您在安裝程式的 [站台維護] 頁面中啟用產品為止。 在 180 天時限之前或之後的任何時間，都可以選擇將評估安裝升級為完整安裝。  

> [!NOTE]  
>  將 Configuration Manager 主控台連線至 Configuration Manager 的評估安裝時，主控台標題列會顯示評估安裝到期前的剩餘天數。 天數不會自動重新整理，而且只有在您重新連線到站台時才會更新。  

 您可以升級下列執行評估安裝的站台：  

-   管理中心網站  
-   主要網站  

由於次要網站不被視為評估安裝，在主要網站升級為完整安裝之後，您不需要修改次要網站。  

評估版升級為授權版本的必要條件：  

-   升級期間必須要有有效的產品。  
-   您的帳戶對於站台安裝所在的電腦，必須具有**系統管理員**權限。  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>將 Configuration Manager 評估版升級為授權版  

1.  在站台伺服器上，從 Configuration Manager 安裝資料夾 (**%path%\BIN\X64**) 執行 **Setup.exe** (Configuration Manager 安裝程式)。 因為當您從安裝媒體執行安裝程式時無法使用站台維護選項，所以您必須執行位於站台伺服器之 Configuration Manager 資料夾中的安裝程式複本。  
2.  在 [開始之前] 頁面上，選取 [下一步]。  
3.  在 [開始使用] 頁面上，選取 [執行站台維護或重設此站台]，然後選取 [下一步]。  
4.  在 [站台維護] 頁面上，選取 [將評估版升級為授權版]，輸入有效的產品金鑰，然後選取 [下一步]。  
5.  在 [Microsoft 軟體授權條款] 頁面上，閱讀並接受授權條款，然後選取 [下一步]。  
6.  在 [設定] 頁面上，選取 [關閉] 以完成精靈。  

    > [!NOTE]  
    >  仍然連線至升級站台之 Configuration Manager 主控台的標題列，在將主控台重新連線至站台之前，可能會指出該站台仍為評估版。  
