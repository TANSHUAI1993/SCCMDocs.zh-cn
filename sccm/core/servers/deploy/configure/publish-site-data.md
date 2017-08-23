---
title: "發佈站台資料 | Microsoft Docs"
description: "了解如何將 Configuration Manager 站台發佈至 Active Directory Domain Services。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bcfb002c503485f03ba27d7346acb61d0d3c6087
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>發佈 System Center Configuration Manager 的站台資料

*適用對象：System Center Configuration Manager (最新分支)*

延伸 System Center Configuration Manager 的 Active Directory 架構之後，即可將 Configuration Manager 站台發佈至 Active Directory Domain Services (AD DS)。 如此可讓 Active Directory 電腦能從受信任的來源安全地擷取站台資訊。 雖然基本 Configuration Manager 功能並不需要將站台資訊發佈至 AD DS，但如此可減少系統管理負荷。  

-   **當站台設定為發佈至 AD DS 時**，Configuration Manager 用戶端會自動透過 Active Directory 發佈功能，尋找管理點。 他們使用 LDAP 查詢通用類別目錄伺服器。  

-   **當站台未發佈到 AD DS 時**，用戶端必須具有找出預設管理點的替代機制。  

如需用戶端如何尋找管理點的資訊，請參閱 [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務)。  

## <a name="configure-sites-to-publish-to-ad-ds"></a>將站台設定為發佈到 AD DS  
 高階步驟如下：  

-   您必須在要發佈站台資料的每個樹系中，[擴充 System Center Configuration Manager 的 Active Directory 架構](../../../../core/plan-design/network/extend-the-active-directory-schema.md)。 也請確認有出現 **System Management** 容器。  

-   您必須為每個會發佈資料的主要站台之電腦帳戶，授與 **System Management** 容器及其所有子物件的**完全控制**。  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>若要啟用 Configuration Manager 站台可將站台資訊發佈至 Active Directory 樹系

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定] ，然後按一下 [站台] 。 選取想要發佈其站台資料的站台。 接著，在 [首頁] 索引標籤的 [內容] 群組中，按一下 [內容]。  

3.  在站台內容的 [發佈] 索引標籤中選取樹系，讓此站台將站台資料發佈至該樹系。  

4.  按一下 [確定]  儲存設定。  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>若要設定 Active Directory 樹系進行發佈  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [Active Directory 樹系] 。 如果 Active Directory 樹系探索之前已執行，您會在結果窗格中看見每個探索到的樹系。 當 Active Directory 樹系探索執行時，會探索本機樹系和任何信任的樹系。 只有不受信任的樹系必須手動新增。  

    -   若要設定先前探索到的樹系，請在結果窗格中選取樹系。 然後在 [首頁] 索引標籤的 [內容] 群組中，按一下 [內容]，開啟該樹系內容。 繼續進行步驟 3。  

    -   若要設定未列出的新樹系，請在 [首頁] 索引標籤的 [建立] 群組中，按一下 [新增樹系] 以開啟 [新增樹系] 對話方塊。 繼續進行步驟 3。  

3.  在 [一般] 索引標籤上，完成您要探索之樹系的設定，然後指定 [Active Directory 樹系帳戶]。  

    > [!NOTE]  
    >  Active Directory 樹系探索需要通用帳戶，才能探索及發佈至不受信任的樹系。 如果您未使用網站伺服器的電腦帳戶，就只能選取通用帳戶。  

4.  如果您打算允許站台將站台資料發佈至此樹系，可在 [發佈]  索引標籤上，完成發佈至此樹系的設定。  

    > [!NOTE]  
    >  若啟用站台能發佈至樹系，則必須為 Configuration Manager 延伸該樹系的 Active Directory 架構。 Active Directory 樹系帳戶必須具有該樹系中系統容器的完全控制權限。  

5.  當您完成此樹系的設定以搭配使用 Active Directory 樹系探索時，請按一下 [ **OK** ] 以儲存設定。  
