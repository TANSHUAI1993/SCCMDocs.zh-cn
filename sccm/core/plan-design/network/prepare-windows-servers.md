---
title: "準備 Windows Server | Microsoft Docs"
description: "請確定電腦符合當成 System Center Configuration Manager 站台伺服器或站台系統伺服器使用的必要條件。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9b97dedb5d2be0bd2e47260033e6e4361467dc4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>準備 Windows 伺服器以支援 System Center Configuration Manager

*適用對象：System Center Configuration Manager (最新分支)*

在您將 Windows 電腦當成 System Center Configuration Manager 站台系統伺服器使用之前，必須確定電腦符合其預期用途 (站台伺服器或站台系統伺服器) 的必要條件。  

-   這些必要條件通常包含一個或多個 Windows 功能或角色，使用電腦伺服器管理員可加以啟用。  

-   由於啟用 Windows 功能和角色的方法因不同作業系統而有所差異，所以請參考您的作業系統文件，以取得設定所用作業系統的詳細資訊。  

這篇文章中的資訊提供支援 Configuration Manager 站台系統所需的 Windows 設定類型概觀。 如需特定站台系統角色的設定詳細資料，請參閱[站台和站台系統必要條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)。

##  <a name="BKMK_WinFeatures"></a> Windows 功能和角色  
 當您在電腦上設定 Windows 功能和角色時，可能需要將電腦重新開機，才能完成設定。 因此，在安裝 Configuration Manager 站台或站台系統伺服器之前，找出即將裝載特定站台系統角色是個不錯的主意。
### <a name="features"></a>功能  
 下列 Windows 功能為特定站台系統伺服器所需，並且應該先加以設定，再將站台系統角色安裝於該電腦。  

-   **.NET Framework**：包括  

    -   ASP.NET  
    -   HTTP 啟動  
    -   非 HTTP 啟動  
    -   Windows Communication Foundation (WCF) 服務  

    不同站台系統角色需要不同版本的 .NET Framework。  

    由於 .NET Framework 4.0 及更新版本無法與舊版相容以取代 3.5 及較舊版本，因此當不同版本列為必要版本時，請規劃在同一部電腦上啟用每個版本。  

-   **背景智慧型傳送服務 (BITS)**：管理點需要 BITS (和自動選取的選項) 才可支援與受管理裝置間的通訊。  

-   **BranchCache**：可在發佈點設定 BranchCache，以支援使用 BranchCache 的用戶端。  

-   **重複資料刪除**：可在發佈點設定重複資料刪除，而從中獲得好處。  

-   **遠端差異壓縮 (RDC)**：每部裝載站台伺服器或發佈點的電腦都需要 RDC。   
    RDC 可用於產生封裝簽章及執行簽章比較。  

### <a name="roles"></a>角色  
 下列 Windows 角色為支援軟體更新及作業系統部署等特定功能所需，而 IIS 為大多數常用站台系統角色所需。  

 -   **網路裝置註冊服務** (在 Active Directory 憑證服務下)：此 Windows 角色是使用 Configuration Manager 中「憑證設定檔」的必要條件。  

 -   **網頁伺服器 (IIS)**：包括：  
    -   一般 HTTP 功能 >  
        -   HTTP 重新導向  
    -   應用程式開發 >  
        -   .NET 擴充性  
        -   ASP.NET  
        -   ISAPI 擴充程式  
        -   ISAPI 篩選器  
    -   管理工具 >  
        -   IIS 6 管理相容性  
        -   IIS 6 Metabase 相容性  
        -   IIS 6 Windows Management Instrumentation (WMI) 相容性  
    -   安全性 >  
        -   要求篩選  
        -   Windows 驗證  

 下列站台系統角色使用其中一或多項所列 IIS 設定：  
    -   應用程式類別目錄 Web 服務點  
    -   應用程式類別目錄網站點  
    -   發佈點  
    -   註冊點  
    -   註冊 Proxy 點  
    -   後援狀態點  
    -   管理點  
    -   軟體更新點  
    -   狀態移轉點     

    所需 IIS 最低版本為站台伺服器作業系統所提供的版本。  

    除了這些 IIS 設定外，您可能還需要設定[用於發佈點的 IIS 要求篩選](#BKMK_IISFiltering)。  

-   **Windows 部署服務**：此角色是與「作業系統部署」搭配使用。  
-   **Windows Server Update Services**：此角色為您部署軟體更新時所需。  

##  <a name="BKMK_IISFiltering"></a> 用於發佈點的 IIS 要求篩選  
 IIS 預設會使用要求篩選來封鎖 HTTP 或 HTTPS 通訊存取伺服器數個副檔名和資料夾位置。 在發佈點上，如此可預防用戶端下載包含遭封鎖副檔名或資料夾位置的套件。  

 如果您的套件來源檔案包含在 IIS 遭要求篩選設定封鎖的副檔名，您就必須將要求篩選設為允許這些副檔名。 在您的發佈點電腦上 IIS Manager 中 [編輯要求篩選功能](https://technet.microsoft.com/library/hh831621.aspx) 即可完成此作業。  

 此外，Configuration Manager 的套件和應用程式使用下列副檔名。 請確認您的要求篩選設定未封鎖這些副檔名：  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

例如，軟體部署的來源檔案中可能包含名為 **bin**的資料夾，或是副檔名為 **.mdb** 的檔案。  

-   IIS 要求篩選預設會封鎖對這些項目的存取權 (**bin** 會封鎖為 [隱藏區段]，**.mdb** 則封鎖為 [副檔名])。  

-   在發佈點上使用預設的 IIS 組態時，使用 BITS 的用戶端將無法從發佈點下載此軟體部署，並且會表示他們正在等候內容。  

-   若要讓用戶端下載此內容，請在每個適用的發佈點上編輯 IIS Manager 中的 [要求篩選]，以允許存取您所部署套件及應用程式中的副檔名和資料夾。  

> [!IMPORTANT]  
>  編輯要求篩選可能增加電腦的受攻擊面。  
>   
>  -   您在伺服器層級進行的編輯適用於伺服器上所有網站。  
> -   您對個別網站所做的編輯僅使用於該網站。  
>   
>  最佳安全作法是在專用 Web 伺服器上執行 Configuration Manager。 如果必須在該 Web 伺服器上執行其他應用程式，請使用 Configuration Manager 的自訂網站。 如需相關資訊，請參閱 [Websites for site system servers in System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md) (System Center Configuration Manager 中的站台系統伺服器網站)。  

## <a name="http-verbs"></a>HTTP 動詞
**管理點︰**為了確保用戶端可以成功與管理點進行通訊，請在管理點伺服器上確認允許下列 HTTP 動詞︰  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**發佈點︰**發佈點需要允許下列 HTTP 動詞：
 - GET
 - HEAD
 - PROPFIND

如需設定要求篩選的相關資訊，請參閱 TechNet 上的[在 IIS 中設定要求篩選](https://technet.microsoft.com/library/hh831621.aspx#Verbs)，或適用於裝載管理點的 Windows Server 版本的類似文件。
