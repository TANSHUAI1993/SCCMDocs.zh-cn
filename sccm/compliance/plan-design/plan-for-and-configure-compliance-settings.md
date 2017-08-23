---
title: "規劃與設定合規性設定 | Microsoft Docs"
description: "了解使用 System Center Configuration Manager 相容性設定的必要條件和設定工作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d26ac3de58d2f0ef447725e63fc2d8adda6ea06c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中規劃和設定相容性設定

*適用對象：System Center Configuration Manager (最新分支)*

開始使用 System Center Configuration Manager 相容性設定之前，您需要了解幾個必要條件，並且需要執行一些設定工作。  

## <a name="prerequisites-for-compliance-settings"></a>相容性設定的必要條件  

|必要條件|詳細資訊|  
|------------------|----------------------|  
|必須啟用並設定 Windows Configuration Manager 用戶端以進行相容性評估。|請參閱下面的|  
|如果您想要執行報告，則必須設定站台的報告功能。|[System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)|  
|必要的安全性權限。|[相容性設定管理員] 安全性角色包含管理相容性設定、使用者資料和設定檔套件項目以及遠端連線設定檔所需的權限。<br /><br /> [設定以角色為基礎的系統管理](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>啟用和設定相容性設定 (僅限 Windows 電腦)  

這個程序設定相容性設定的預設用戶端設定，並套用至階層中的所有電腦。 如果您只想某些電腦套用這些設定，請建立自訂裝置用戶端設定，並將它指派給包含要使用相容性設定之電腦的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱 [How to Configure Client Settings](../../core/clients/deploy/configure-client-settings.md) (如何設定用戶端設定)。  

> [!TIP]  
>  其他裝置類型不需要進行任何特定組態，即可評估相容性設定。  

1.  在 Configuration Manager 主控台中按一下 [管理] > [用戶端設定] > **[預設設定]**。  
2.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  
3.  在 [預設設定]  對話方塊中，按一下 [相容性設定] 。  
4.  設定相容性設定的下列用戶端設定：
    - **在用戶端上啟用相容性評估**：如果想要評估用戶端裝置的相容性請設為 [True]。
    - **排程相容性評估**：如果您想要修改用戶端裝置上的預設相容性評估排程，請按一下 [排程]。
    - **啟用使用者資料和設定檔**：如果您想要建立使用者資料和設定檔設定項目，並將其部署至 Windows 電腦，請啟用這個選項。 如需詳細資訊，請參閱 [Create user data and profiles configuration items](/sccm/compliance/deploy-use/create-remote-connection-profiles) (建立使用者資料和設定檔設定項目)。
5. 按一下 [確定]  ，關閉 [預設設定]  對話方塊。  

用戶端電腦會在下一次下載用戶端原則時，使用這些設定進行設定。  
