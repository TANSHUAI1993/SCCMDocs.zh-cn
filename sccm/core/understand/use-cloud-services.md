---
title: "使用雲端服務搭配 Configuration Manager | Microsoft Docs"
description: "佈建 System Center Configuration Manager 的雲端資源，以補充內部部署基礎結構。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 52f7c63d155d5c34f0f12e13020767dec1867dab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>使用雲端服務搭配 System Center Configuration Manager

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 支援數個雲端式選項。 這些選項能補充您的內部部署基礎結構，並可協助解決像是下列的商務問題：  

-   如何管理 BYOD (透過使用行動裝置管理的 Intune)。  

-   在公司防火牆外，如何提供隔離用戶端或內部網路的資源 (透過使用雲端式發佈點)。  

-   在實體硬體無法使用或無法以邏輯方式放置時，如何擴充基礎結構以支援您的需求 (透過使用 Microsoft Azure 虛擬機器)。  

雖然在部署 Configuration Manager 前不一定要佈建雲端資源，但在階層設計計劃發展太深入之前，先了解這些選項會有所助益。 使用雲端資源或許能協助您省下金錢與時間，並解決內部部署基礎結構無法解決的商務問題。  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>可以搭配 Configuration Manager 使用的雲端資源  
 由於每個選項都有不同的需求，因此請逐一深入調查，以了解獨特的必要條件、限制，以及依使用量而產生的潛在額外成本。  

-   如需雲端發佈點的相關資訊，請參閱[安裝雲端發佈點](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)。

-   如需 Azure 的詳細資訊，請參閱 MSDN Library 中的 [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965)。  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Azure 虛擬機器 (適用於雲端式基礎結構)  
 Configuration Manager 支援使用在 Azure 虛擬機器中執行的電腦，就像在實體公司網路中內部部署執行一樣。 您可以在下列案例使用 Azure 虛擬機器：  

-   **案例 1：**您可以在虛擬機器中執行 Configuration Manager，並用其來管理安裝在其他虛擬機器中的用戶端。  

-   **案例 2：**您可以在虛擬機器中執行 Configuration Manager，並用其來管理未在 Azure 中執行的用戶端。  

-   **案例 3：**您可以一方面在虛擬機器中執行不同的 Configuration Manager 站台系統角色，一方面在您的實體公司網路 (具備用於通訊的適當網路連線) 中執行其他角色。  

適用於在您實體公司網路上安裝 Configuration Manager 的相同網路、作業系統和硬體需求，也適用於在 Azure 中安裝 Configuration Manager。  

需要有 Azure 訂用帳戶，才能使用 Azure 虛擬機器。 會根據所使用的虛擬機器數目、其設定，以及雲端式資源使用量來產生費用。  

此外，在 Azure 虛擬機器上執行的 Configuration Manager 站台和用戶端受限於與內部部署安裝相同的授權需求。  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Azure 服務 (適用於雲端式發佈點)  
 您可以使用 Azure 服務來裝載 Configuration Manager 發佈點，其稱為雲端發佈點。 您可以[使用雲端式發佈點搭配 System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)、內部部署發佈點，以及部署在 Azure 虛擬機器的發佈點。  

 這不同於使用 Azure 虛擬機器，在 Azure 虛擬機器上需部署站台系統角色。 雲端發佈點：  

-   在 Azure 中執行為服務，而不是在虛擬機器上執行。  

-   自動調整以滿足用戶端增加的內容要求。  

-   支援網際網路和內部網路上的用戶端。  

需要有 Azure 訂用帳戶，才能使用 Azure 來裝載發佈點。 會根據傳輸到服務以及從服務傳輸的資料量來產生費用。  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (適用於行動裝置管理)  
 您可以整合 Microsoft Intune 訂閱與 Configuration Manager，以便能夠使用 Intune 服務來管理裝置。 此項整合：  

-   稱為混合式設定，並會擴充 Configuration Manager (或 Intune，視您的檢視方塊而定) 以支援各種裝置。  

-   需要 Microsoft Intune 連接器站台系統角色。  

-   您需要有個別的 Intune 訂閱，而針對您將使用 Intune 來管理的裝置，該訂閱需具有足夠的裝置授權。  

雖然 Intune 使用 Azure，但您不需要個別設定 Azure，同時也不會有超過 Intune 訂閱費用的額外成本。  

### <a name="additional-configuration-manager-capabilities"></a>其他 Configuration Manager 功能  
 某些 Configuration Manager 功能可以連線至雲端服務，例如：  

-   Windows Server Update Services (WSUS)。  

-   下載 Configuration Manager 更新的 Configuration Manager 服務雲端。  

這些其他功能不需要您擁有 Azure 訂用帳戶。 您不需要在雲端中設定特定連線、憑證或服務。 相反地，Configuration Manager 會替您自動加以管理。 您只需要確保適用的站台系統與裝置能夠存取以網際網路為基礎的 URL。  

##  <a name="BKMK_CloudSec"></a> 雲端服務的安全性  
 Configuration Manager 使用憑證來佈建與存取您在 Azure 中的內容，以及管理您使用的服務。 Configuration Manager 會將您儲存在 Azure 中的資料加密，但在 Azure 提供的安全性或資料控制項之外，不會提供額外防護。  

 如需詳細資訊，請參閱不同雲端式資源案例的詳細資料。 您也可以檢視下列 Azure 安全性主題：  

-   [Azure：了解 Azure 中的安全性帳戶管理](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Azure Security Overview](http://go.microsoft.com/fwlink/p/?LinkId=262970) (Azure 安全性概觀)  

-   [Get Past the Security Crossroads in Your Cloud Migration (解決與雲端移轉有關的安全性問題) (解決與雲端移轉有關的安全性問題)](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Azure 資料安全性的第 1 部分 (共 2 個部分)](http://go.microsoft.com/fwlink/p/?LinkId=262974)  
