---
title: "System Center Configuration Manager 中的條款和條件 | Microsoft Docs"
description: "在 System Center Configuration Manager 中，將條款和條件部署至使用者群組。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 20be68496099a67ad2d475067f073da2cef16c86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 新增條款及條件

*適用對象：System Center Configuration Manager (最新分支)*

您可以將 System Center Configuration Manager 條款和條件部署至使用者群組，以說明裝置註冊、存取工作資源以及使用公司入口網站，會如何影響裝置與使用者。 使用者必須先接受這些條款和條件，才可使用公司入口網站來註冊及存取其工作。  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>處理 System Center Configuration Manager 中的條款和條件原則  
 您可建立及部署多組條款和條件的集合。 您也可以產生相同條款和條件的不同語言版本，再將這些版本部署到適當的群組。  

## <a name="to-create-a-terms-and-conditions"></a>建立條款和條件  

1.  在 Configuration Manager 主控台中，移至 **[資產與相容性]** > **[概觀]** > **[相容性設定]** > **[條款和條件]**。  

2.  按一下 [建立條款和條件]  可建立新的條款和條件。  

3.  在 [一般]  頁面上，指定下列資訊：  

    -   **名稱** - Configuration Manager 主控台中顯示的唯一名稱  

    -   **描述** - 有助於您在 Configuration Manager 主控台中識別條款和條件的詳細資料  

     然後按 [下一步] 。  

4.  在 [條款]  頁面上，指定下列資訊：  

    -   **標題** - 使用者在公司入口網站中看到的標題  

    -   **條款文字** - 使用者在公司入口網站中看到的條款和條件  

    -   **說明使用者接受之涵義的文字** - 使用者所看到有關接受的標籤。 **範例**：「我同意這些條款和條件。」  

     然後按 [下一步] 。  

5.  完成精靈即可以建立新的條款和條件。 新的條款和條件會顯示在資產與相容性工作區的條款和條件節點內。  

## <a name="to-deploy-a-terms-and-conditions"></a>部署條款和條件  

1.  在 Configuration Manager 主控台中，移至 **[資產與相容性]** > **[概觀]** > **[相容性設定]** > **[條款和條件]**。  

2.  在 **[條款和條件]** 清單中，選取您想要部署的項目，然後按一下 **[部署]**。  

3.  **瀏覽** 至要部署條款和條件的 **集合** ，然後按一下 [確定] 。  

     當目標裝置存取公司入口網站的應用程時，其會顯示您所部署的條款和條件。 使用者必須接受這些條款，才能存取公司資源。  

    > [!NOTE]  
    >  若將一組條款部署至使用者所屬的多個使用者集合，則該使用者在開啟公司入口網站時，會看到相同條款的多個複本。 因為使用者只可接受或拒絕所有條款，所以不可能出現使用者同時接受且拒絕條款的這種模稜兩之接受狀態。 條款和條件接受報表中，每位使用者的每組條款都只有一個資料列，因此報表中沒有任何錯誤。  

## <a name="to-monitor-terms-and-conditions"></a>監視條款和條件  

1.  您可以在 Configuration Manager 主控台中監視條款和條件部署。 在 Configuration Manager 主控台中，移至 **[監視]** > **[概觀]** > **[部署]**。  

2.  選取條款和條件部署。 (從部署清單中選取)  

     摘要區域將會顯示下列統計資料︰  

    -   **相容** - 使用者已接受最新版的條款和條件  

    -   **錯誤**  

    -   **不相容** - 使用者已接受某個版本的條款和條件，但不是最新版  

    -   **不明** - 使用者從未接受條款和條件 (包括沒有已註冊裝置的使用者)  

3.  選取某個條款和條件部署，然後選取 **[執行摘要]** 以查看個別使用者的「部署狀態」。  

     在 [部署狀態] 畫面中，您可以選取狀態索引標籤來檢視具有該狀態的使用者。 您可以按一下 **[執行摘要]** 來更新整個階層的資料。 按一下 **[重新整理]** 即可更新主控台中的資料  

## <a name="to-view--a-terms-and-conditions-report"></a>檢視條款和條件報告  

1.  在 Configuration Manager 主控台中，移至 **[監視]** > **[概觀]** > **[報告]** > **[報表]**。  

2.  選取 **[接受條款和條件]** ，然後按一下 **[執行]**。 隨即會開啟「接受條款和條件」報表。 此報表會顯示已接受條款和條件部署的每位使用者。 欄位包括：  

    -   條款和條件的名稱  

    -   使用者名稱  

    -   接受的版本  

    -   接受日期  

    -   已接受最新  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>更新條款和條件並進行版本控制  
 當您編輯現有條款和條件時，可以選擇部署條款和條件時的行為。 使用下列程序有助您更新現有的條款和條件。  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>如何使用多種版本的條款和條件  

1.  在 Configuration Manager 主控台中，移至 **[資產與相容性]** > **[概觀]** > **[相容性設定]** > **[條款和條件]**。  

2.  選取您要編輯的條款和條件執行個體，然後按兩下加以開啟。  

3.  您可以修改 [一般]  或 [條款]  頁面，進行任何必要的編輯。  

4.  在 [條款]  頁面上，可以接著指定這個新版本是否要求所有使用者都要接受該條款和條件，還是只有新的使用者才會看到新版本。  

     建議您在大幅變更條款和條件時，加大版本號碼並要求接受條款和條件。 如果您想要修正錯字或變更格式，請保留目前的版本號碼。

> [!div class="button"]
[< 上一個步驟](configure-intune-subscription.md)  [下一個步驟 >](create-service-connection-point.md)
