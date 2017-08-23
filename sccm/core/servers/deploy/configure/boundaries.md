---
title: "定義界限 | Microsoft Docs"
description: "了解如何在您的內部網路上定義網路位置，其中可包含您要管理的裝置。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bed70809008fde5e2b0215f4dce049402edf83ba
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>針對 System Center Configuration Manager 將網路位置定義為界限

*適用於：System Center Configuration Manager (最新分支)*

Configuration Manager 界限是您網路上的位置，該位置包含您要管理的裝置。 裝置所在的界限相當於 Active Directory 站台，或是安裝於裝置上的 Configuratoin Manager 用戶端所識別的網路 IP 位址。
 - 您可以手動建立個別界限。 不過，Configuration Manager 不支援使用 Supernet 的直接入口作為界限。 不過，您可以使用 IP 位址範圍界限類型。
 - 您可以設定 [Active Directory 樹系探索](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)方法以自動探索，並針對它探索到的各個 IP 子網路和 Active Directory 站台建立界限。 當 Active Directory 樹系探索識別指派給 Active Directory 網站的 Supernet 時，Configuration Manager 會將 Supernet 轉換為 IP 位址範圍界限。  

裝置使用 Configuration Manager 系統管理員未注意到的 IP 位置並不是罕見狀況。 對裝置的網路位置存疑時，請對該裝置使用 **IPCONFIG** 命令，確認裝置回報為位置的內容。  

當您建立界限時，界限會自動收到根據界限類型和範圍所定的名稱。 您無法修改這個名稱。 相反地，您可以指定描述以協助在 Configuration Manager 主控台中識別界限。  

每個界限都可供您階層中的每個站台使用。 建立界限後，您可以修改其內容以執行下列動作：  
-   將界限新增至一個或多個界限群組。  
-   變更界限的類型或範圍。  
-   檢視界限 [站台系統]  索引標籤，查看與界限相關聯的站台系統伺服器 (發佈點、狀態移轉點和管理點)。  

## <a name="to-create-a-boundary"></a>建立界限  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] > [界限]。  

2.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立界限]  **Boundary.**。  

3.  在 [建立界限] 對話方塊的 [一般]  索引標籤上，您可以指定 [描述]  ，以易記名稱或參照來識別界限。  

4.  選取此界限的 [類型]  ：  

    -   如果您選取 [IP 子網路] ，則必須指定此界限的 [子網路識別碼]  。  
        > [!TIP]  
        >  您可以指定 [網路]  和 [子網路遮罩]  ，以自動指定 [子網路識別碼]  。 儲存界限時，只會儲存 [子網路識別碼] 值。  

    -   如果您選取 [Active Directory 站台] ，則必須指定或 [瀏覽]  至本機站台伺服器樹系中的 Active Directory 站台。  

        > [!IMPORTANT]  
        >  您為界限指定 Active Directory 站台時，界限會包含每一個身為該 Active Directory 站台成員的 IP 子網路。 如果 Active Directory 中 Active Directory 站台的設定變更，此界限中的網路位置也會變更。  

    -   如果您選取 [IPv6 首碼] ，則必須指定 IPv6 首碼格式的 [首碼]  。  

    -   如果您選取 [IP 位址範圍] ，則必須指定包含部分 IP 子網路或包含多個 IP 子網路的 [起始 IP 位址]  和 [結束 IP 位址]  。    

5.  按一下 [確定]  儲存新界限。  

## <a name="to-configure-a-boundary"></a>設定界限  

1.  在 Configuration Manager 主控台中按一下 [系統管理] > [階層設定] > [界限]。  

2.  選取您要修改的界限。  

3.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

4.  在界限的 [內容]  對話方塊中，選取 [一般]  索引標籤以編輯界限的 [描述]  或 [類型]  。 您也可以編輯界限的網路位置來變更界限的範圍。 例如，您可以為 Active Directory 站台界限指定新的 Active Directory 站台名稱。  

5.  選取 [站台系統]  索引標籤即可檢視與此界限相關聯的站台系統。 您無法從界限的內容變更此設定。  

    > [!TIP]  
    >  若要使站台系統伺服器成為界限的站台系統，站台系統伺服器必須是包含此界限的至少一個界限群組的相關聯站台系統伺服器。 這設定在界限群組的 [參照]  索引標籤上。  

6.  選取 [界限群組]  索引標籤可修改此界限的界限群組成員資格：  

    -   若要將此界限新增至一個或多個界限群組，請按一下 [新增] ，選取一個或多個界限群組的核取方塊，然後按一下 [確定] 。  

    -   若要從界限群組中移除此界限，請選取界限群組，然後按一下 [移除] 。  

7.  按一下 [確定]  關閉界限內容，並儲存設定。  
