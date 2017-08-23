---
title: "建立集合 | Microsoft Docs"
description: "在 System Center Configuration Manager 中建立集合，更輕鬆地管理使用者和裝置群組。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44b4707b1a40624c51decf548d23ddd2164c5833
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立集合

*適用於：System Center Configuration Manager (最新分支)*

集合是使用者或裝置的群組。 請使用集合來執行例如應用程式管理、部署合規性設定，或安裝軟體更新等工作。 您也可以使用集合來管理用戶端設定群組，或搭配角色型系統管理來指定系統管理使用者可以存取的資源。 Configuration Manager 包含數個內建集合。 如需詳細資訊，請參閱 [System Center Configuration Manager 的集合簡介](../../../../core/clients/manage/collections/introduction-to-collections.md)。  

> [!NOTE]  
>  集合可包含使用者或裝置，但不能同時包含兩者。  

 下表列出可用來設定 Configuration Manager 集合成員的規則。  

|成員資格規則類型|詳細資訊|  
|--------------------------|----------------------|  
|直接規則|用來選擇要新增到集合的使用者或電腦。 除非從 Configuration Manager 中移除資源，否則這個成員資格不會變更。 Configuration Manager 必須已探索到資源或您必須匯入資源，才可以將它們新增至直接規則集合。 直接規則集合比查詢規則集合具有更高的系統管理負荷，因為需要手動變更。|  
|查詢規則|依據 Configuration Manager 排程執行的查詢，來動態更新集合的成員資格。 例如，您可以在 Active Directory 網域服務中，建立屬於人力資源組織單位成員的使用者集合。 當人力資源組織單位加入或移除新使用者時，此集合會自動更新。<br /><br /> 如需可用來建置集合的範例查詢，請參閱[如何在 System Center Configuration Manager 中建立查詢](../../../../core/servers/manage/create-queries.md)。|  
|包含集合規則|將其他集合的成員包含在 Configuration Manager 集合中。如果包含集合有所變更，則目前集合的成員資格會依排程更新。<br /><br /> 您可將多個包含集合規則新增至某個集合。<br /> |  
|排除集合規則|排除集合規則可讓您從 Configuration Manager 集合中排除另一個集合的成員。 如果排除集合有所變更，則目前集合的成員資格會依排程更新。<br /><br /> 您可將多個排除集合規則新增至某個集合。 如果一個集合同時具有包含集合規則和排除集合規則，就會發生衝突，此時排除集合規則的優先順序會較高。<br />              **範例：** 您可以建立一個集合，其中具有一個包含集合規則和一個排除集合規則。 包含集合規則是針對 Dell 桌上型電腦的集合。 排除集合規則是針對擁有少於 4 GB RAM 的電腦集合。 新的集合將包含至少 4 GB RAM 的 Dell 桌上型電腦。|  

 使用下列程序可協助您在 Configuration Manager 中建立集合。 您也可以匯入集合；不論集合是在這個 Configuration Manager 站台或其他站台建立皆可。 如需如何匯出和匯入集合的資訊，請參閱[如何在 System Center Configuration Manager 中管理集合](../../../../core/clients/manage/collections/manage-collections.md)。  

 如需為執行 Linux 和 UNIX 的電腦建立集合的相關資訊，請參閱[如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器的用戶端](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)。  

##  <a name="BKMK_1"></a> 若要建立裝置集合  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置集合]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立裝置集合]。  

4.  在 [一般] 頁面上提供 [名稱] 和 [註解]。 然後，在 [限制集合] 中選擇 [瀏覽]，以選取限制集合。 集合將只會包含來自限制集合的成員。  

5.  在 [建立裝置集合精靈] 的 [成員資格規則] 頁面上，於 [新增規則] 清單中，選取您要用於此集合的成員資格規則類型。 您可以為每個集合設定多個規則。  

        
##### <a name="to-configure-a-direct-rule"></a>若要設定直接規則  

1.  在 [建立直接成員資格規則精靈]  的 [搜尋資源] 頁面上，指定下列資訊：  

-   **資源類別**：選取您要搜尋並新增至集合的資源類型。 從 [系統資源]  的值進行選取以搜尋用戶端電腦傳回的清查資料，或選擇 [未知電腦]  以從未知電腦所傳回的值進行選取。  

-   **屬性名稱**：選取您想要搜尋之選定資源類別的相關聯屬性。 例如，如果您想要選取電腦的 NetBIOS 名稱，請依序選取 [資源類別]  清單中的 [系統資源]  和 [屬性名稱]  清單中的 [NetBIOS 名稱]  。  

-   **排除標記為以過時的資源** - 如果用戶端電腦已標記為過時，請不要在搜尋結果中包含此值。  

-   **排除未安裝 Configuration Manager 用戶端的資源** - 這些不會顯示在搜尋結果中。  

-   **值** ：輸入您要搜尋之選定屬性名稱的值。 您可以將 **%** 百分比字元作為萬用字元。 例如，若要搜尋 NetBIOS 名稱開頭是 "M" 的電腦，請在此欄位中輸入 **M%**。  

2.  在 [選取資源] 頁面上，從 [資源] 清單中選取您想要新增至集合中的資源，然後選擇 [下一步]。  


##### <a name="to-configure-a-query-rule"></a>若要設定查詢規則  

1.  在 [查詢規則內容]  對話方塊中，指定下列資訊：  

-   **名稱**：指定唯一名稱。  

-   **匯入查詢陳述式** - 開啟 [瀏覽查詢] 對話方塊，您可以在其中選取 [Configuration Manager 查詢](../../../../core/servers/manage/create-queries.md)以作為集合的查詢規則。   

-   **資源類別**：選取您要搜尋並新增至集合的資源類型。 從 [系統資源]  的值進行選取以搜尋用戶端電腦傳回的清查資料，或選擇 [未知電腦]  以從未知電腦所傳回的值進行選取。  

-   **編輯查詢陳述式** - 開啟 [查詢陳述式內容] 對話方塊，您可以在其中撰寫要作為集合規則的查詢。 如需查詢的詳細資訊，請參閱 [System Center Configuration Manager 的查詢技術參考](../../../../core/servers/manage/queries-technical-reference.md)。  

    
##### <a name="to-configure-an-include-collection-rule"></a>若要設定包含集合規則  

在 [選取集合] 對話方塊中，選取您想要在新集合中包含的集合，然後選擇 [確定]。  

##### <a name="to-configure-an-exclude-collection-rule"></a>若要設定排除集合規則  

在 [選取集合] 對話方塊中，選取您想要從新集合排除的集合，然後選擇 [確定]。  

-   **針對此集合使用累加式更新** - 選取此選項以僅定期掃描上一次集合評估至今新增或變更過的資源，並且不受完整集合評估的影響。 累加式更新的時間間隔為每 10 分鐘發生一次。  

> [!IMPORTANT]  
>  如果您是使用下列類別的查詢規則來設定集合，則不支援累加式更新。  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (僅限使用者的集合)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (僅限使用者的集合)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **排程此集合的完整更新** - 排程集合成員資格的定期完整評估。  

6.  完成精靈以建立新的集合。 新集合會顯示在 [資產與相容性]  工作區的 [裝置集合]  節點中。  

> [!NOTE]  
>  若要查看集合成員，您必須重新整理或重新載入 Configuration Manager 主控台。 不過，在第一次排程更新，或手動為集合選取 [更新成員資格] 之後，集合才會顯示成員。 可能需要幾分鐘的時間才能完成集合更新。  

##  <a name="BKMK_2"></a> 若要建立使用者集合  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [使用者集合]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立使用者集合]。  

4.  在精靈的 [一般] 頁面提供 [名稱] 和 [註解]。 然後，在 [限制集合] 中選擇 [瀏覽]，以選取限制集合。 集合將只會包含來自限制集合的成員。  

5.  在 [成員資格規則] 頁面上，指定下列各項︰  

    -   在 [新增規則]  清單中，選取您要用於此集合的成員資格規則類型。 您可以為每個集合設定多個規則。  

##### <a name="to-configure-a-direct-rule"></a>若要設定直接規則  

1.  在 [建立直接成員資格規則精靈] 的 [搜尋資源] 頁面上，指定：  

-   **資源類別**：選取您要搜尋並新增至集合的資源類型。 從 [使用者資源] 的值進行選取以搜尋 Configuration Manager 所收集的使用者資訊，或選擇 [使用者群組資源] 以搜尋 Configuration Manager 所收集的使用者群組資訊。  

-   **屬性名稱**：選取您想要搜尋之資源類別的相關聯屬性。 例如，如果您想要選取使用者的組織單位名稱，請依序選取 [資源類別]  清單中的 [使用者資源]  和 [屬性名稱]  清單中的 [使用者 OU 名稱]  。  

-   **值︰**輸入您想要搜尋的值。 您可以將 **%** 百分比字元作為萬用字元。 例如，若要在 Contoso OU 中搜尋使用者，請在此欄位中輸入 **Contoso** 。  

2.  在 [選取資源] 頁面上，從 [資源] 清單中選取您想要新增至集合中的資源。  

##### <a name="to-configure-a-query-rule"></a>若要設定查詢規則  

1.  在 [查詢規則屬性] 對話方塊中，提供︰  

-   **名稱**︰唯一的名稱。  

-   **匯入查詢陳述式** - 開啟 [瀏覽查詢] 對話方塊，您可以在其中選取 [Configuration Manager 查詢](../../../../core/servers/manage/queries-technical-reference.md)以作為集合查詢規則。  

-   **資源類別**：選取您要搜尋並新增至集合的資源類型。 從 [使用者資源] 的值進行選取以搜尋 Configuration Manager 所收集的使用者資訊，或選擇 [使用者群組資源] 以搜尋 Configuration Manager 所收集的使用者群組資訊。  

-   **編輯查詢陳述式** - 開啟 [查詢陳述式內容] 對話方塊，您可以在其中[撰寫查詢](../../../../core/servers/manage/queries-technical-reference.md)以作為集合的規則。  

##### <a name="to-configure-an-include-collection-rule"></a>若要設定包含集合規則  

在 [選取集合] 對話方塊中，選取您想要在新集合中包含的集合，然後選擇 [確定]。  

##### <a name="to-configure-an-exclude-collection-rule"></a>若要設定排除集合規則  

在 [選取集合] 對話方塊中，選取您想要從新集合排除的集合，然後選擇 [確定]。  


-   **針對此集合使用累加式更新** - 選取此選項以僅定期掃描上一次集合評估至今新增或變更過的資源，並且不受完整集合評估的影響。 累加式更新的時間間隔為每 10 分鐘發生一次。  

> [!IMPORTANT]  
>  如果您是使用下列類別的查詢規則來設定集合，則不支援累加式更新。  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (僅限使用者的集合)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (僅限使用者的集合)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **排程此集合的完整更新** - 排程集合成員資格的定期完整評估。  

6.  完成精靈。 新集合會顯示在 [資產與相容性]  工作區的 [使用者集合]  節點中。  

> [!NOTE]  
>  若要查看集合成員，您必須重新整理或重新載入 Configuration Manager 主控台。 不過，在第一次排程更新，或手動選取集合的 [更新成員資格]  之後，集合才會顯示成員。 可能需要幾分鐘的時間才能完成集合更新。  

##  <a name="BKMK_3"></a> 若要匯入集合  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [使用者集合] 或 [裝置集合]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [匯入集合]。  

4.  在 [匯入集合精靈] 的 [一般] 頁面中，選擇 [下一步]。  

5.  在 [MOF 檔案名稱] 頁面上，選擇 [瀏覽]，然後瀏覽至包含您要匯入之集合資訊的 MOF 檔案。  

    > [!NOTE]  
    >  您要匯入的檔案必須已從站台匯出，且該站台需執行與此項目相同版本的 Configuration Manager。 如需匯出集合的詳細資訊，請參閱[如何在 System Center Configuration Manager 中管理集合](../../../../core/clients/manage/collections/manage-collections.md)。  

6.  完成精靈以匯入集合。 新集合會顯示在 [資產與相容性]  工作區的 [使用者集合]  或 [裝置集合]  節點中。 若要查看新匯入集合的集合成員，請重新整理或重新載入 Configuration Manager 主控台。  
