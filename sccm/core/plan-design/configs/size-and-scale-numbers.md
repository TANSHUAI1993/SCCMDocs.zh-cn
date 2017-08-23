---
title: "大小和縮放比例 | Microsoft Docs"
description: "識別 System Center Configuration Manager 環境中支援裝置所需的站台系統角色和站台數目。"
ms.custom: na
ms.date: 07/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f539e2d282b56e56a9c58c773788325b27ea6b37
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>System Center Configuration Manager 的大小和縮放比例

*適用於：System Center Configuration Manager (最新分支)*



每個 System Center Configuration Manager 部署都會有可支援的站台、站台系統角色和裝置數目上限。 這些數字會視階層結構 (您使用的站台類型和數目) 以及您部署的站台系統角色而不同。  下列區域中的資訊可協助您識別支援要用來管理環境之裝置所需的站台系統角色和站台數目。

使用本主題中的資訊以及下列各文章中的資訊︰
-   [建議的硬體](../../../core/plan-design/configs/recommended-hardware.md)
-   [支援的站台系統伺服器作業系統](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [用戶端和裝置的支援作業系統](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [站台和站台系統必要條件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


下列支援數目是根據使用建議的 Configuration Manager 硬體以及所有可用 Configuration Manager 功能的預設設定。 如果您未使用建議的硬體，或使用更積極的自訂設定 (例如執行硬體或軟體清查的頻率高於每七天一次的預設值)，站台系統的效能可能會降低，也可能不符合指定層級的支援。

##  <a name="bkmk_SiteSystemScale"></a> 站台類型  
 **管理中心網站：**  

-   管理中心網站可支援最多 25 個子主要站台。  

**主要站台：**  

-   每一個主要站台可支援最多 250 個次要站台。  

-   每個主要站台的次要站台數目是根據持續連線且可靠的廣域網路 (WAN) 連線。 若為具有少於 500 個用戶端的位置，請考慮發佈點，而不是次要站台。  

 如需主要站台可支援之用戶端和裝置數目的相關資訊，請參閱本主題中的[站台和階層的用戶端數目](#bkmk_clientnumbers)。  

**次要站台：**  

-   次要站台不支援子站台。  

-   管理中心網站可支援最多 25 個子主要站台。  

**應用程式類別目錄網站點：**  

-   您可以在主要站台安裝應用程式類別目錄網站點的多個執行個體。  

    > [!TIP]  
    >  最佳作法是，當應用程式類別目錄網站點和應用程式類別目錄 Web 服務點提供服務給內部網路上的用戶端時，將它們安裝在相同的站台系統上。  

    -   若要改善效能，請規劃每個執行個體支援最多 50,000 個用戶端。  

    -   此站台系統角色的每個執行個體都支援由階層所支援的用戶端數目上限。  

## <a name="bkmk_roles"></a> Site system roles    

**應用程式類別目錄 Web 服務點：**  

-   您可以在主要站台安裝應用程式類別目錄 Web 服務點的多個執行個體。  

    > [!TIP]  
    >  最佳作法是，當應用程式類別目錄網站點和應用程式類別目錄 Web 服務點提供服務給內部網路上的用戶端時，將它們安裝在相同的站台系統上。  

    -   若要改善效能，請規劃每個執行個體支援最多 50,000 個用戶端。  

    -   此站台系統角色的每個執行個體都支援由階層所支援的用戶端數目上限。  

**發佈點：**  

-   每個站台的發佈點：  

    -   每個主要和次要站台支援最多 250 個發佈點。  

    -   每個主要和次要站台支援最多 2000 個其他設定為提取發佈點的發佈點。 **例如**，當 2000 個發佈點設定為提取發佈點時，單一主要站台可支援 2250 個發佈點。  

    -   每個發佈點支援最多 4,000 個用戶端連線。  

    -   提取發佈點在存取來自來源發佈點的內容時，行為類似用戶端。  

-   每個主要站台支援最多合併總計 5,000 個發佈點。 這個總數包含在主要站台的所有發佈點，和屬於主要站台之子次要站台的所有發佈點。  

-   每個發佈點支援最多合併總計 10,000 個封裝和應用程式。  

> [!WARNING]  
>  一個發佈點可支援的用戶端實際數目，取決於網路的速度以及發佈點電腦的硬體設定。  
>   
>  一個來源發佈點可支援的提取發佈點數目，也同樣地取決於來源發佈點電腦的網路速度和硬體設定。 但此數目也受到您已部署的內容量影響。 原因是不同於用戶端通常會在部署期間的不同時間存取內容，所有提取發佈點會同時要求內容，且可能要求所有可用的內容，而不是像用戶端那樣只要求它們適用的內容。 太多處理負載放在來源發佈點時，將內容發佈到您環境中的預期發佈點時可能會有無法預期的延遲。  


**後援狀態點：**  

-   每個後援狀態點最多可以支援 100,000 個用戶端。  

**管理點：**  

-   每個主要站台可支援最多 15 個管理點。  

    > [!TIP]  
    >  請不要在透過主要站台伺服器或站台資料庫伺服器之緩慢連結的伺服器上安裝管理點。  

-   每個次要站台支援單一管理點，它必須安裝在次要站台伺服器上。  

 如需管理點可支援之用戶端與裝置數目的資訊，請參閱本主題中的[管理點](#bkmk_mp)一節。  

**軟體更新點：**  

-   站台伺服器上安裝的軟體更新點可以支援最多 25,000 個用戶端。  

-   位於站台伺服器遠端的電腦上所安裝的軟體更新點可以支援最多 150,000 個用戶端，前提是遠端電腦符合 Windows Server Update Services (WSUS) 需求可支援這個數目的用戶端。  

-   根據預設，Configuration Manager 不支援將軟體更新點設定為網路負載平衡 (NLB) 叢集。 不過，您可以使用 Configuration Manager SDK，在 NLB 叢集上設定最多四個軟體更新點。  

##  <a name="bkmk_clientnumbers"></a> 站台和階層的用戶端數目  
 使用下列資訊，判斷您可以於站台上或階層中支援的用戶端數目和用戶端類型。  

###  <a name="bkmk_cas"></a> 使用管理中心網站的階層  
管理中心網站支援的裝置總數，包含針對下列三個群組所列出之最多裝置數目：  

-   700,000 部電腦 (執行 Windows、Linux 和 UNIX 的電腦)。 另請參閱[內嵌裝置](#embedded)的支援。

-   25,000 部執行 Mac 和 Windows CE 7.0 的裝置  

-   下列其中一項，根據您的部署如何支援行動裝置管理 (MDM)：  

    -   使用內部部署 MDM 管理的 100,000 部裝置  

    -   300,000 部雲端型裝置  

 例如，當您整合 Microsoft Intune 時，可以在某個階層中支援 700,000 部桌上型電腦、最多 25,000 個 Mac 與 Windows CE 7.0，以及最多 300,000 部雲端型裝置，總共 1,025,000 部裝置。 如果您支援由內部部署 MDM 管理的裝置，階層的總計會是 825,000 部裝置。  

> [!IMPORTANT]  
>  在管理中心網站使用 SQL Server 標準版的階層中，階層支援最多 50,000 部桌上型電腦與裝置。 在獨立主要站台使用中的 SQL Server 版本不會限制該站台容量，以支援最多指定數目的用戶端。  


###  <a name="bkmk_chipri"></a> 子主要站台  
使用管理中心網站之階層中的每個子主要站台支援下列：  

-   總計 150,000 部用戶端與裝置，不限於特定群組或類型，只要支援不超過階層所支援的數目即可。 另請參閱[內嵌裝置](#embedded)的支援。

例如，支援執行 Mac 和 Windows CE 7.0 的 25,000 部電腦的主要站台 (因為這是階層的限制)，之後可以支援額外的 125,000 部桌上型電腦。 其所支援裝置的總數最高為子主要站台支援的最大限制：150,000。

###  <a name="bkmk_pri"></a> 獨立主要站台  
獨立主要站台支援下列的裝置數目：  

-   總計 175,000 部用戶端與裝置，不得超過：  

    -   150,000 部電腦 (執行 Windows、Linux 和 UNIX 的電腦)。 另請參閱[內嵌裝置](#embedded)的支援。

    -   25,000 部執行 Mac 和 Windows CE 7.0 的裝置

    -   下列其中一項，根據您的部署如何支援行動裝置管理：  

        -   使用內部部署 MDM 管理的 50,000 部裝置  

        -   150,000 部雲端型裝置  


例如，支援 150,000 部桌上型電腦和 10,000 部 Mac 或 Windows CE 7.0 的獨立主要站台僅可以支援額外的 15,000 部裝置。 這些可以是雲端型或使用內部部署 MDM 管理的裝置。  

### <a name="embedded"></a> 主要站台和 Windows Embedded 裝置
主要站台支援已啟用檔案型寫入篩選器 (FBWF) 的 Windows Embedded 裝置。 當內嵌的裝置未啟用寫入篩選器時，主要站台支援的內嵌裝置數目上限即為該站台允許的裝置數目。 主要站台支援的裝置總數中，如果這些裝置已針對[規劃將用戶端部署至 Windows Embedded 裝置](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices)中重要事項所列例外狀況而設定的話，最多有 10,000 部可以作為 Windows Embedded 裝置。 主要站台只支援 3,000 部已啟用 EWF 且未針對例外狀況而設定的 Windows Embedded 裝置。

###  <a name="bkmk_sec"></a> 次要站台  
次要站台支援下列：  

-   15,000 部桌上型電腦 (執行 Windows、Linux 和 UNIX 的電腦)  

###  <a name="bkmk_mp"></a> 管理點  
每個管理點都可以支援下列數目的裝置：  

-   總計 25,000 部用戶端和裝置，不得超過：  

    -   25,000 部桌上型電腦 (執行 Windows、Linux 和 UNIX 的電腦)  

    -   下列其中之一 (非兩者皆是)：  

        -   使用內部部署 MDM 管理的 10,000 部裝置  

        -   10,000 部執行 Mac 和 Windows CE 7.0 用戶端的裝置
