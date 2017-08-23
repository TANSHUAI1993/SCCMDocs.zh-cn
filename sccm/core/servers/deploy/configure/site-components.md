---
title: "Configuration Manager 的站台元件 | Microsoft Docs"
description: "了解如何設定站台元件，以修改站台系統角色和站台狀態報告的行為。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="site-components-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站台元件

*適用對象：System Center Configuration Manager (最新分支)*

在每個 System Center Configuration Manager 站台，您都可以設定站台元件，以修改站台系統角色和站台狀態報告的行為。 站台元件設定適用於站台，以及該站台上適用站台系統角色的每個執行個體。  

## <a name="about-site-components"></a>關於站台元件  
 在 Configuration Manager 主控台檢視不同站台元件的選項時，大部分選項的意義都可透過其名稱得知。 不過，下列詳細資料可協助解說某些較複雜的設定，或將您導向到其他加以解釋的內容。  

### <a name="software-distribution"></a>軟體發佈  

-   **內容發佈設定：**您可以指定設定以修改站台伺服器將內容傳輸到其發佈點的方式。 如果您將用於並行發佈設定的值提高，內容發佈就可以使用更多的網路頻寬。  

-   **網路存取帳戶：**如需設定及使用網路存取帳戶的資訊，請參閱[網路存取帳戶](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)。  

### <a name="software-update-point"></a>軟體更新點  

-   如需軟體更新點元件設定選項的資訊，請參閱[安裝軟體更新點](../../../../sum/get-started/install-a-software-update-point.md)。  

### <a name="management-point"></a>管理點  

-   **管理點：**您可以將站台設定為將其管理點的相關資訊發行到 Active Directory 網域服務。  

     Configuration Manager 用戶端使用管理點來尋找服務，以及尋找界限群組成員資格和 PKI 憑證選擇選項這類站台資訊。 用戶端也會使用管理點，在下載軟體的站台和發佈點中尋找其他管理點。 管理點也可協助用戶端完成站台指派，以及下載用戶端原則與上傳用戶端資訊。  

     由於用戶端用來尋找管理點的大部分安全方法都是在 Active Directory 網域服務中進行發佈，因此您通常一律選取所有可運作的管理點來發佈至 Active Directory 網域服務。 不過，此服務位置方法需要符合下列條件：

     - 已延伸 Configuration Manager 的架構。
     - 具有**系統管理**容器，內含可讓站台伺服器發行到此容器的適當安全性權限。
     - Configuration Manager 站台設定成發行到 Active Directory 網域服務。
     - 用戶端屬於與站台伺服器樹系相同的 Active Directory 樹系。  

     內部網路上的用戶端無法使用 Active Directory 網域服務以尋找管理點時，請改用 [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) 發行。  

 如需服務位置的一般資訊，請參閱[了解用戶端如何找到 System Center Configuration Manager 的站台資源和服務](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

-   **在 DNS 中發佈選取的內部網路管理點：**內部網路上的用戶端無法從 Active Directory 網域服務找到管理點時，請指定此選項。 相反地，用戶端可以使用 DNS 服務位置資源記錄 (SRV RR) 在其指派的站台找到管理點。  

    如果 Configuration Manager 要將內部網路管理點發行至 DNS，則必須符合下列所有條件：  

    -   您的 DNS 服務包含 8.1.2 (含) 以上版本的 BIND。  

    -   您的 DNS 伺服器已設定為自動更新，並支援服務位置資源記錄。  

    -   Configuration Manager 中管理點的指定完整網域名稱 (FQDN) 在 DNS 中包含主機項目 (A 或 AAA 記錄)。  

    > [!WARNING]  
    >  對於要尋找 DNS 中所發行之管理點的用戶端，您必須將用戶端指派給特定站台，而不是使用自動站台指派。 設定這些用戶端，透過其管理點的網域尾碼來使用站台碼。 如需詳細資訊，請參閱[如何將用戶端指派給 System Center Configuration Manager 中的站台](/sccm/core/clients/deploy/assign-clients-to-a-site)中的[尋找管理點](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)。  

     如果 Configuration Manager 用戶端無法使用 Active Directory 網域服務或 DNS 在內部網路上尋找管理點，則會使用 [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins)。 為此站台安裝的第一個管理點設定為接受內部網路的 HTTP 用戶端連線時，即會自動發行到 WINS。  

### <a name="status-reporting"></a>狀態報告  

-   這些設定直接設定站台及用戶端狀態報表內含的詳細資料層級。  

### <a name="email-notification"></a>電子郵件通知  

-   指定帳戶和電子郵件伺服器詳細資料，讓 Configuration Manager 傳送警示的電子郵件通知。  

### <a name="collection-membership-evaluation"></a>集合成員資格評估  

-   使用此工作以設定累加式評估集合成員資格的頻率。 累加式評估只會更新已新增或變更資源的集合成員資格。  

### <a name="edit-the-site-components-at-a-site"></a>在站台上編輯站台元件  

使用下列步驟來編輯站台元件：

1.  在 Configuration Manager 主控台中，按一下 [系統管理] > [站台設定] > [站台]，然後選取包含您要設定之站台元件的站台。  

2.  在 [首頁] 索引標籤的 [設定] 群組中，按一下 [設定站台元件]。 然後選取您要設定的站台元件。  

##  <a name="BKMK_ServiceMgr"></a> 使用 Configuration Manager Service Manager 管理站台元件  
您可以使用 Configuration Manager Service Manager 來控制 Configuration Manager 服務，以及檢視任一 Configuration Manager 服務或工作執行緒 (皆指 Configuration Manager 元件) 的狀態。 了解 Configuration Manager 元件的下列事項：  

-   元件可以在任何站台系統上執行。  

-   管理元件的方式與您管理 Windows 中的服務一樣。 您可以啟動、停止、暫停、繼續或查詢 Configuration Manager 元件。  

Configuration Manager 服務會在具有任務時執行 (通常是將設定檔寫入元件收件匣時)。 如果您必須識別出作業中的元件，則可以使用 Configuration Manager Service Manager 來操作各種服務和執行緒。 您接著可以檢視 Configuration Manager 行為中所產生的變更。 例如，您可以一次停止一個 Configuration Manager 服務，直到消除某個特定回應為止。 如此可讓您判斷哪一種服務導致此行為。  

> [!TIP]  
>  以下程序可用來操作 Configuration Manager 元件作業。  

### <a name="use-the-configuration-manager-service-manager"></a>使用 Configuration Manager Service Manager  

1.  在 Configuration Manager 主控台中，按一下 [監視] >  [系統狀態]，然後按一下 [元件狀態]。  

2.  在 [首頁] 索引標籤上，於 [元件] 群組中按一下 [開始]。 然後選取 [Configuration Manager Service Manager]。  

3.  Configuration Manager Service Manager 開啟時，連線至您要管理的網站。  

     若您看不到要管理的站台，請依序按一下 [站台] 與 [連線] ，然後輸入正確站台的站台伺服器名稱。  

4.  展開網站，並根據您要管理的元件所在位置瀏覽至 [元件]  或 [伺服器] 。  

5.  在右側窗格中，選取一個或多個元件。 然後，在 [元件] 功能表上，按一下 [查詢] 以更新選擇狀態。  

6.  更新元件狀態後，使用 [元件] 功能表上四種以動作為基礎的選項之一，以修改元件作業。 要求動作後，您必須查詢元件，以顯示元件的新狀態。  

7.  完成修改元件操作狀態後，請關閉 Configuration Manager Service Manager。  
