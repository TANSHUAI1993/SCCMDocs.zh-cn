---
title: "設定用戶端設定 | Microsoft Docs"
description: "選取 System Center Configuration Manager 的用戶端設定。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 478d562bfb7fdb3921a4278741ff096e81e6092a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中設定用戶端設定

*適用於：System Center Configuration Manager (最新分支)*

您可以從 [系統管理] > [用戶端設定] 管理 System Center Configuration Manager 中的所有用戶端設定。 若您想要設定在階層中未套用任何自訂設定之所有使用者和裝置的設定，可修改預設設定。 如果您只想要將不同的設定套用至部分使用者或裝置，可建立自訂設定並將這些設定部署至集合。  

如需各項用戶端設定的資訊，請參閱[關於 Configuration Manager 中的用戶端設定](../../../core/clients/deploy/about-client-settings.md)。

> [!NOTE]  
>  您也可以使用組態項目管理用戶端，以評估、追蹤和補救裝置的組態相容性。 如需詳細資訊，請參閱 [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md) (使用 System Center Configuration Manager 確保裝置相容性)。  

##  <a name="configure-the-default-client-settings"></a>設定預設的用戶端設定    

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定] > [預設用戶端設定]。  

3.  在 [常用] 索引標籤上，選擇 [內容]。  

4.  在瀏覽窗格中，檢視及設定每一組設定的用戶端設定。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則抓取，請參閱[如何管理 System Center Configuration Manager 中的用戶端](../../../core/clients/manage/manage-clients.md)中的[起始 Configuration Manager 用戶端的原則抓取](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="create-and-deploy-custom-client-settings"></a>建立及部署自訂用戶端設定  
當您部署這些自訂設定時，這些設定會覆寫預設用戶端設定。 在開始此程序之前，請先確定您擁有包含這些需要自訂用戶端設定之使用者或裝置的集合。  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [用戶端設定]。  

3.  在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立自訂用戶端設定]，然後選擇其中一項：  

    -   **建立自訂用戶端裝置設定**  

    -   **建立自訂用戶端使用者設定**  

4.  指定唯一的名稱和選項描述。  

5.  選取一個或多個顯示設定群組的核取方塊。  

6.  選擇瀏覽窗格中的每個設定群組，設定可用的設定，然後按一下 [確定]。   

8.  選取您建立的自訂用戶端設定。 在 [常用] 索引標籤的 [用戶端設定] 群組中，選擇 [部署]。  

9. 在 [選取集合] 對話方塊中，選取適當的集合，然後選擇 [確定]。 按一下詳細資料窗格中的 [部署]  索引標籤，即可驗證所選取的集合。  

10. 檢視您剛才建立的自訂用戶端設定的順序。 如果您有多個自訂用戶端設定，則這些設定會依照其順序編號套用。 如果發生任何衝突，順序編號最小的設定會覆寫其他設定。 若要變更順序編號，請在 [常用] 索引標籤的 [用戶端設定] 群組中，選擇 [將項目往上移] 或 [將項目往下移] 。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則抓取，請參閱[如何管理 System Center Configuration Manager 中的用戶端](../../../core/clients/manage/manage-clients.md)中的[起始 Configuration Manager 用戶端的原則抓取](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="view-client-settings"></a>檢視用戶端設定  
 當有多個用戶端設定部署至相同裝置、使用者或使用者群組時，設定的優先順序和組合可能會很複雜。 若要檢視用戶端設定：  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置] > [使用者] 或 [使用者集合]。  

3.  選取裝置、使用者或使用者群組，然後在 [用戶端設定]  群組中，選取 [結果用戶端設定] 。  

4.  從左窗格選取用戶端設定，隨即顯示設定。 在此檢視中，設定是唯讀的。 

    > [!NOTE]  
    >  若要檢視用戶端設定，您必須具有用戶端設定的讀取存取權限。  

    