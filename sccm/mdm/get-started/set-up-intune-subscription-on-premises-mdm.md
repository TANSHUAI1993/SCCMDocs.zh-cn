---
title: "設定 Intune 訂閱 | Microsoft Docs"
description: "在 System Center Configuration Manager 中為內部部署行動裝置管理設定 Intune 訂閱來追蹤授權。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 5a81ec06e16992ae1c41b0fc98ebcd07386c5381
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>為 System Center Configuration Manager 中的內部部署行動裝置管理設定 Microsoft Intune 訂閱

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 內部部署行動裝置管理需要 Microsoft Intune 訂閱來追蹤授權。 不會使用 Intune 服務來管理裝置或儲存管理資訊。 針對內部部署行動裝置管理，所有裝置管理都是透過 Configuration Manager 基礎結構來處理。  

> [!NOTE]  
> 從 1610 版開始，Configuration Manager 支援同時使用 Microsoft Intune 和內部部署 Configuration Manager 基礎結構來管理行動裝置。   

> [!TIP]  
>  建議您在安裝必要站台系統角色，讓新安裝的站台系統角色能以最快時間開始運作前，先設定進行內部部署行動裝置管理的 Intune 訂閱。  

##  <a name="sign-up-for-microsoft-intune"></a>註冊 Microsoft Intune  
 需要有 Intune，才能進行內部部署行動裝置管理功能。 只要[註冊](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/)試用版或付費訂閱，並前往下一個步驟，就能將訂閱新增至 Configuration Manager。  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>將訂用帳戶新增至 Configuration Manager  
 若要將訂閱新增至 Configuration Manager，請遵循與使用 Intune 新增行動裝置管理的訂閱時相同的基本步驟。 請閱讀下列針對特定差異的附註，然後使用[設定 Intune 訂閱](../deploy-use/configure-intune-subscription.md)中的指示。  

> [!NOTE]  
>  當新增 Intune 訂閱時，請記住：  
>   
>  -   [新增 Microsoft Intune 訂閱精靈] 中指定的集合不會用於內部部署行動裝置管理使用者權限委派， 而僅用於透過 Intune 進行的行動裝置管理。 不過，您必須指定集合，精靈才能繼續。  
> -   內部部署行動裝置管理會忽略精靈中所指定的站台碼設定。 而使用您在註冊設定檔中指定的站台碼，此設定檔可授與使用者註冊裝置的權限。  
> -   請勿啟用多重要素驗證。 不支援內部部署行動裝置管理。  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>為內部部署行動裝置管理設定 Intune 訂閱  

1.  在 Configuration Manager 主控台中，以滑鼠右鍵按一下 [Microsoft Intune 訂閱]，然後按一下 [內容]。  

2.  在 [內部部署行動裝置管理] 方塊中，選擇下列其中一項︰

  - 如果您只想要透過內部部署方式管理裝置，請按一下 [Only manage devices on-premises (僅管理內部部署裝置)] 旁的核取方塊，然後按一下 [確定]。  

      > [!NOTE]  
      >  按一下此核取方塊後，即表示您將 Intune 訂閱設為讓所有管理資訊皆維持在內部部署，且不會將資料複寫至雲端。  

    - 如果您想要同時透過 Intune 和 Configuration Manager 內部部署管理裝置，請不要核取這個方塊。

3.  如果您打算管理 Windows 10 行動裝置版的裝置，請以滑鼠右鍵依序按一下 [Microsoft Intune 訂閱] 、[設定平台] 及 [Windows Phone]  。  

4.  按一下 [Windows Phone 8.1 與 Windows 10 行動裝置版] 旁的核取方塊，然後按一下 [確定] 。  

5.  如果您打算管理 Windows 10 桌上型電腦，請以滑鼠右鍵依序按一下 [Microsoft Intune 訂閱] 、[設定平台] 及 [啟用 Windows 註冊] 。  

6.  按一下 [啟用 Windows 註冊] 旁的核取方塊，然後按一下 [確定] 。  
