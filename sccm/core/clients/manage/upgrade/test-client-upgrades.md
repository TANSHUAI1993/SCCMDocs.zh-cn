---
title: "測試進入生產階段前集合的用戶端升級 | Microsoft Docs"
description: "在 System Center Configuration Manager 中測試進入生產階段前集合的用戶端升級。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: "10"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 572ef13883f7930e69ec1f1f53c9bfe029898c81
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>如何測試 System Center Configuration Manager 的進入生產階段前集合用戶端升級

*適用於︰System Center Configuration Manager (最新分支)*

您可以先在進入生產階段前集合中測試新的 Configuration Manager 用戶端版本，然後用它來升級站台的其餘部分。  當您這樣做時，只會將屬於測試集合的裝置升級。 一旦測試過用戶端之後，您就可以升級該用戶端，讓站台的其餘部分都能使用新版本的用戶端軟體。

> [!NOTE]
> 若要將測試用戶端升階至生產環境，您必須以具備**系統高權限管理員**的安全性角色和**全部**的安全性範圍的使用者身分來登入。 如需詳細資訊，請參閱[以角色為基礎的系統管理基本概念](/sccm/core/understand/fundamentals-of-role-based-administration)。 您也必須登入至已連線到管理中心網站或最上層獨立主要站台的伺服器。

 測試進入生產階段前集合中的用戶端有 3 個基本步驟。  

1.  設定自動升級用戶端使用進入生產階段前集合。  

2.  安裝包含新版用戶端的 Configuration Manager 更新。  

3.  將新用戶端升階到生產環境。  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>設定自動升級用戶端使用進入生產階段前集合  

1. [設定集合](..\collections\create-collections.md)，內含您要在其中部署進入生產階段前用戶端的電腦。 請不要在進入生產階段前集合中包含工作群組電腦。 它們無法使用發佈點所需的驗證來存取進入生產階段前用戶端套件。   

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [站台設定] > [站台]，然後選擇 [階層設定]。  

     在 [階層設定屬性]  的 [用戶端升級] 索引標籤中：  

    -   選取 [使用進入生產階段前用戶端自動升級進入生產階段前集合的所有用戶端]   

    -   輸入要做為進入生產階段前集合的集合名稱  

![測試用戶端升級](media/test-client-upgrades.png)

>[!NOTE]
>若要變更這些設定，您的帳戶必須是「系統高權限管理員」安全性角色，以及「全部」安全性範圍的成員。


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>安裝包含新版用戶端的 Configuration Manager 更新  

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [更新與服務]，選取 [可用] 更新，然後選擇 [安裝更新套件]。 (1702 版之前，[更新與服務] 位於 [系統管理] > [雲端服務] 底下)。

     如需安裝更新的詳細資訊，請參閱 [System Center Configuration Manager 的更新](../../../../core/servers/manage/updates.md)  

2.  在安裝更新期間，在精靈的 [用戶端選項] 頁面上選取 [在進入生產階段前集合中測試]。  

3.  完成精靈的其餘部分，並安裝更新套件。  

     完成精靈之後，進入生產階段前集合中的用戶端會開始部署更新的用戶端。 您可以監視升級用戶端的部署，請前往 **[監視]** > **[用戶端狀態]** > **[進入生產階段前用戶端部署]**。 如需詳細資訊，請參閱[如何在 Configuration Manager 中設定用戶端狀態](../../../../core/clients/deploy/monitor-client-deployment-status.md)。

    > [!NOTE]
    > 在進入生產階段前集合中，裝載站台系統角色之電腦上的部署狀態可能會報告為 [不符合標準]，即使用戶端已成功部署也一樣。 當您將用戶端升階為生產階段時，就會正確報告部署狀態。

##  <a name="to-promote-the-new-client-to-production"></a>將新用戶端升級到生產環境  

1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [更新與服務]，然後選擇 [將生產階段前用戶端升階]。 (1702 版之前，[更新與服務] 位於 [系統管理] > [雲端服務] 底下)。

    > [!TIP]
    > 當您監視 **[監視]** [用戶端狀態] **[進入生產階段前用戶端部署]** > **中主控台的用戶端部署時，也可以使用** > **[Promote Pre-production Client (將生產階段前用戶端升階)]**按鈕。

2.  檢閱在生產階段和生產階段前的用戶端版本，請確定指定了正確的生產階段前集合，然後依序按一下 [升階] 及 [是]。  

3.  對話方塊關閉後，更新的用戶端版本將會取代階層中使用的用戶端版本。 接著可以升級整個站台的用戶端。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

>[!NOTE]
>若要啟用生產階段前用戶端，或是將生產階段前用戶端升級為生產階段用戶端，您的帳戶必須是針對 [更新套件] 物件具有「讀取」和「修改」權限的安全性角色成員。
>用戶端升級會遵循您所設定的任何 Configuration Manager 維護時段。
