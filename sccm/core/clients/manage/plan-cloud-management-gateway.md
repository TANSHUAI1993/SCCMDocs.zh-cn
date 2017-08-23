---
title: "雲端管理閘道規劃 | Microsoft Docs"
description: 
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a7380ae781447880ffcba0778694ea62e10c4889
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>在 Configuration Manager 中進行雲端管理閘道規劃

適用於：System Center Configuration Manager (最新分支)

從 1610 版開始，雲端管理閘道提供簡單的方法，管理網際網路上的 Configuration Manager 用戶端。 雲端管理閘道服務已部署至 Microsoft Azure，並需要 Azure 訂用帳戶。 它會使用稱為雲端管理閘道連接器端點的新角色，連線至您內部部署的 Configuration Manager 基礎結構。 在部署及設定後，用戶端就能夠存取內部部署的 Configuration Manager 站台系統角色，不論它們位在內部的私人網路還是網際網路。

> [!TIP]  
> 隨 1610 版引進的雲端管理閘道為發行前版本的功能。 若要啟用它，請參閱[使用更新的發行前版本功能](/sccm/core/servers/manage/pre-release-features)。

請使用 Configuration Manager 主控台將服務部署至 Azure、新增雲端管理閘道連接器端點角色，並設定站台系統角色以允許雲端管理閘道流量。 雲端管理閘道目前只支援管理點和軟體更新點角色。

需要用戶端憑證和安全通訊端層 (SSL) 憑證，才能進行電腦驗證，以及加密不同服務層級之間的通訊。 用戶端電腦通常會透過強制執行群組原則來接收用戶端憑證。 若要加密用戶端與裝載角色的站台系統伺服器之間的流量，您必須從 CA 建立自訂 SSL 憑證。 您也需要在 Azure 上設定管理憑證，以允許 Configuration Manager 部署雲端管理閘道服務。

## <a name="requirements-for-cloud-management-gateway"></a>雲端管理閘道的需求

-   用戶端電腦和執行雲端管理閘道連接器端點的站台系統伺服器。

-   來自內部 CA 的自訂 SSL 憑證 - 用來加密與用戶端電腦的通訊，並驗證雲端管理閘道服務的身分識別。

-   雲端服務的 Azure 訂用帳戶。

-   Azure 管理憑證 - 用來向 Azure 驗證 Configuration Manager。

## <a name="specifications-for-cloud-management-gateway"></a>雲端管理閘道的規格

- 每個雲端管理閘道執行個體支援 4000 個用戶端。
- 建議您至少建立兩個雲端管理閘道執行個體，以改善可用性。
- 雲端管理閘道只支援管理點和軟體更新點角色。
-   雲端管理閘道目前不支援下列 Configuration Manager 功能︰

    -   用戶端部署
    -   自動站台指派
    -   使用者原則
    -   應用程式類別目錄 (包括軟體核准要求)
    -   完整的作業系統部署 (OSD)
    -   Configuration Manager 主控台
    -   遠端工具
    -   報告網站
    -   網路喚醒
    -   Mac、Linux 及 UNIX 用戶端
    -   Azure Resource Manager
    -   對等快取
    -   內部部署行動裝置管理

## <a name="cost-of-cloud-management-gateway"></a>雲端管理閘道的成本

>[!IMPORTANT]
>下面提供的成本資訊僅供評估之用。 您的環境可能有其他變數會影響使用雲端管理閘道的總成本。

雲端管理閘道使用下列 Microsoft Azure 功能，會產生 Azure 訂閱帳戶費用︰

-   虛擬機器

    -   雲端管理閘道目前需要 Standard\_A2 虛擬機器。 建立服務時，您可以選取支援服務的 VM 數量 (預設值為一部)。

    -   僅供評估之用，預期單一 Azure Standard\_A2 虛擬機器可同時支援約 2000 個以網際網路為基礎的用戶端。

    -   請參閱 [Azure 價格計算機](https://azure.microsoft.com/en-us/pricing/calculator/)以利判斷潛在成本。

      >[!NOTE]
      >虛擬機器的成本隨地區而異。

-   輸出資料傳輸

    -   資料從服務傳出即產生費用。 請參閱 [Azure 頻寬定價詳細資料](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)以利判斷潛在成本。

    -   僅供評估之用，以網際網路為基礎的用戶端每小時執行原則重新整理計算，預期每個用戶端每月大約為 100 MB。

    >[!NOTE]
    > 執行透過雲端管理閘道支援的其他動作 (例如部署軟體更新或應用程式)，會增加從 Azure 輸出的資料傳輸量。

-   內容儲存體

    -   使用雲端管理閘道管理的以網際網路為基礎的用戶端，會從 Windows Update 免費取得軟體更新內容。

    -   任何其他必要內容 (例如，應用程式) 必須發佈至雲端架構發佈點。 目前，雲端管理閘道只支援使用雲端發佈點將內容傳送至用戶端。

    - 如需詳細資訊，請參閱使用[雲端式發佈](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution)的成本。

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>雲端管理閘道 (CMG) 的相關常見問題集

### <a name="why-use-the-cloud-management-gateway"></a>為何使用雲端管理閘道？

針對網際網路用戶端管理，此角色可將管理簡化為 Configuration Manager 主控台的三個步驟。

1. 使用[建立雲端管理閘道](/sccm/core/clients/manage/setup-cloud-management-gateway)精靈將 CMG 部署至 Azure。
2. 設定[雲端管理閘道連接點](/sccm/core/servers/deploy/configure/install-site-system-roles)站台系統角色。
3. [設定雲端管理閘道流量的角色](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic)，例如管理點和軟體更新點。

### <a name="how-does-the-cloud-management-gateway-work"></a>雲端管理閘道如何運作？

- 雲端管理閘道連接點能在網際網路和雲端管理閘道之間提供一致且高效能的連線。
- Configuration Manager 會將設定發行至 CMG，包括連線資訊和安全性設定。
- CMG 會驗證 Configuration Manager 用戶端要求，並將要求轉送至雲端管理閘道連接點。 這些要求會根據 URL 對應轉送至企業網路中的角色。

### <a name="how-is-the-cloud-management-gateway-deployed"></a>雲端管理閘道如何部署？

服務連接點上的雲端服務管理員元件會處理所有 CMG 部署工作。 此外，它也會從 Azure AD 監視並報告服務健康情況和記錄資訊。

#### <a name="certificate-requirements"></a>憑證需求

您需要下列憑證以保護 CMG：

- **管理憑證**：這可以是任何憑證，包括自我簽署憑證。 您可以使用已上傳至 Azure AD 的公開憑證，或是已匯入 Configuration Manager 之[具有私密金鑰的 PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)，以向 Azure AD 進行驗證。
- **Web 服務憑證**：建議使用公開 CA 憑證以取得用戶端的原生信任。 CNAME 必須在公開 DNS 登錄中建立。 不支援萬用字元憑證。
- **上傳至 CMG 的根/次級 CA 憑證**：CMG 必須在用戶端 PKI 憑證上執行完整鏈結驗證。 如果您使用企業 CA 發行用戶端 PKI 憑證，且其根或次級 CA 無法自網際網路取得，您必須將它上傳至 CMG。

#### <a name="deployment-process"></a>部署程序

部署包含兩個階段：

- 部署雲端服務
    - 上傳您的 [Azure 服務定義結構描述 (英文)](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef) 檔案
    - 上傳您的 [Azure 服務設定結構描述 (英文)](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg) 檔案。
- 在您的 Azure AD 伺服器上設定 CMG 元件，並設定 Internet Information Services (IIS) 中的端點、HTTP 處理常式及服務

如果您變更 CMG 的設定，將會針對 CMG 起始設定部署。

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>雲端管理閘道如何協助確保安全性？

CMG 可透過下列方式協助確保安全性：

- 接受並管理來自 CMG 連接點的連線，包括使用內部憑證和連線識別碼的相互 SSL 驗證。
- 接受並轉送用戶端要求
    - 在用戶端 PKI 憑證上使用相互 SSL 預先驗證連線。
    - 憑證信任清單會檢查用戶端 PKI 憑證的根。 您可以在站台屬性的用戶端通訊設定中指定此設定。 同時也針對用戶端執行和管理點相同的驗證。
    - 驗證接收的 URL
    - 篩選接收的 URL，以檢查是否有正在連線的 CMG 連接點可以處理 URL 要求。  
    - 針對每個發行端點進行內容長度檢查。
    - 使用「循環配置資源」，以在來自相同站台的 CMG 連接點之間進行負載平衡。

- 保護 CMG 連接點
    - 針對正在連線之 CMG 的所有虛擬執行個體，建置一致的 HTTP/TCP 連線。 於每分鐘檢查並維護連線。
    - 使用內部憑證來與 CMG 進行相互 SSL 驗證。
    - 根據 URL 對應轉送 HTTP 要求。
    - 報告連線狀態以顯示管理服務健康情況狀態。
    - 於每 5 分鐘針對每個端點報告端點流量報告。

- 保護發行端點 Configuration Manager 用戶端對向角色，像是管理點和 IIS 中軟體更新點主機端點，以處理用戶端要求。 每個發行至 CMG 的端點都具有 URL 對應。
用戶端使用外部 URL 來與 CMG 通訊。
內部 URL 為用來將要求轉送至內部伺服器的 CMG 連接點。

#### <a name="example"></a>範例：
當您在管理點上啟用 CMG 流量時，Configuration Manager 會在內部針對每個管理點伺服器 (例如，ccm_system、ccm_incoming 及 sms_mp) 建立一組 URL 對應。
管理點 ccm_system 端點的外部 URL 看起來應該會類似：**https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**。
每個管理點的 URL 皆會是唯一的。 接著，Configuration Manager 用戶端會將已啟用 CMG 的 MP 名稱 (例如 **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>**) 置於其網際網路管理點清單中。
所有已發行的外部 URL 都會在 CMG 能夠進行 URL 篩選時自動上傳至 CMG。 所有 URL 對應都會複寫至 CMG 連接點，使它可以根據用戶端要求外部 URL 轉送至內部伺服器。

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>雲端管理閘道所使用的連接埠為何？

- 內部部署網路不需要任何輸入連接埠。 CMG 的部署將會自動在 CMG 上大量建立。
- 除了 443 之外，CMG 連接點也會需要部份輸出連接埠。

|||||
|-|-|-|-|
|資料流成|伺服器|伺服器連接埠|用戶端|
|CMG 部署|Azure|443|Configuration Manager 服務連接點|
|建置 CMG 通道|CMG|VM 執行個體：1 連接埠：443<br>VM 執行個體：N (N>=2 且 N<= 16) 連接埠：10124~N 10140~N|CMG 連接點|
|用戶端至 CMG|CMG|443|用戶端|
|CMG 連接器至站台角色 (目前為管理點和軟體更新點)|站台角色|於站台角色上設定的通訊協定/連接埠|CMG 連接點|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>如何改進雲端管理閘道的效能？

- 如果可以的話，請在相同的網路區域中設定 CMG、CMG 連接點及 Configuration Manager 站台伺服器，以降低延遲。
- 目前 Configuration Manager 用戶端和 CMG 之間的連線並無法感知區域。
- 若要獲得高可用性，建議每個站台至少有 2 個 CMG 虛擬執行個體及 2 個 CMG 連接點
- 您可以透過新增更多 VM 執行個體來調整 CMG，以支援更多用戶端。 它們會由 Azure AD 負載平衡器進行負載平衡。
- 建立更多 CMG 連接點以將負載分散於它們之間。 CMG 會透過「循環配置資源」的方式，將流量引導至其正在連線的 CMG 連接點。
- 在 1702 版中，每個 CMG VM 執行個體所支援的用戶端數目為 6 千個。 當 CMG 通道處於高負載時，系統仍然會處理要求，但可能會花費比平常更久的時間。

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>如何監視雲端管理閘道？

如需針對部署進行疑難排解，請使用 **CloudMgr.log** 和 **CMGSetup.log**。
如需針對服務健康情況進行疑難排解，請使用 **CMGService.log** 和 **SMS_CLOUD_PROXYCONNECTOR.log**。
如需針對用戶端流量進行疑難排解，請使用 **CMGHttpHandler.log**、**CMGService.Log** 和 **SMS_CLOUD_PROXYCONNECTOR.log**。

如需所有 CMG 相關的記錄檔清單，請參閱 [Configuration Manager 中的記錄檔](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>後續步驟

[設定雲端管理閘道](setup-cloud-management-gateway.md)
