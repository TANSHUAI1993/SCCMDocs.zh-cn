---
title: "站台系統角色選項 | Microsoft Docs"
description: "如需不一定一目了然的 Configuration Manager 站台系統角色的詳細資訊，請參閱這篇文章。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>為 System Center Configuration Manager 設定站台系統角色的選項

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 站台系統角色的大部分設定選項都是一目了然，或是您在設定它們時已在精靈或對話方塊中說明。 下列各節說明其設定可能需要其他資訊的站台系統角色。  

##  <a name="BKMK_ApplicationCatalog_Website"></a> 應用程式類別目錄網站點  
 如需如何為應用程式類別目錄設定應用程式類別目錄網站點的資訊，請參閱 [Plan for and configure application management in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md) (在 System Center Configuration Manager 中規劃和設定應用程式管理)。  

 **用戶端連線**  

 選取 [HTTPS]，可使用更安全的連線設定以及可判定用戶端是否從網際網路連線。 此選項需要在伺服器上提供 PKI 憑證，才能用於對用戶端進行伺服器驗證，並可透過安全通訊端層 (SSL) 進行資料加密。 如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 如需伺服器憑證的範例部署，以及如何在 Internet Information Services (IIS) 中進行設定的詳細資訊，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)的＜為執行 IIS 的站台系統部署 Web 伺服器憑證＞一節。  

 **將應用程式類別目錄網站新增到信任的站台區域**  

 此訊息會顯示預設用戶端設定中的值，[將應用程式類別目錄網站新增到 Internet Explorer 信任的網站區域] 用戶端設定目前是否設為 [True] 或 [False]。 如果已使用自訂用戶端設定來設定此設定值，則必須自行確認此值。  

 如果是為了完整網域名稱 (FQDN) 設定了此站台系統，且網站不位於 Internet Explorer 中信任的網站區域中時，會提示使用者在連線到應用程式類別目錄時提供認證。  

 **組織名稱**  

 輸入使用者在應用程式類別目錄中看到的名稱。 此商標資訊可協助使用者將此網站識別為信任的來源。  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> 應用程式類別目錄 Web 服務點  
 如需如何為應用程式類別目錄設定應用程式類別目錄 Web 服務點的資訊，請參閱 [Plan for and configure application management in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md) (在 System Center Configuration Manager 中規劃和設定應用程式管理)。  

 **HTTPS**  

 選取 [HTTPS]  將應用程式類別目錄網站點驗證到此應用程式類別目錄 Web 服務點。  此選項需要在執行應用程式類別目錄網站點的伺服器上提供 PKI 憑證，以用於伺服器驗證，並可透過 SSL 進行資料加密。 如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 如需伺服器憑證的部署範例，以及如何在 IIS 中進行設定的資訊，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)的＜為執行 IIS 的站台系統部署 Web 伺服器憑證＞一節。  

##  <a name="BKMK_CertificateRegistrationPoint"></a> 憑證登錄點  
 如需如何設定憑證登錄點的詳細資訊，請參閱[憑證設定檔簡介](/sccm/protect/deploy-use/introduction-to-certificate-profiles)。  

##  <a name="BKMK_Distribution_Point"></a> 發佈點  
 如需如何設定內容部署發佈點的詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

 如需如何設定 PXE 部署發佈點的詳細資訊，請參閱[利用 System Center Configuration Manager 使用 PXE 透過網路來部署 Windows](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

 如需如何設定多點傳送部署發佈點的資訊，請參閱 [利用 System Center Configuration Manager 使用多點傳送透過網路來部署 Windows](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

 **在 Configuration Manager 需要時安裝並設定 IIS**  
 選取此選項，讓 Configuration Manager 在站台系統上安裝及設定 IIS (如果尚未安裝)。 IIS 必須安裝在所有發佈點上，而且您必須選取此設定以在精靈中繼續操作。  

 **站台系統安裝帳戶**  
 對於安裝在站台伺服器的發佈點，只有站台伺服器的電腦帳戶可以當成站台系統安裝帳戶來使用。  

 **建立自我簽署憑證或匯入 PKI 用戶端憑證**  
 此憑證有兩種用途：  

1.  在發佈點傳送狀態訊息前，向管理點驗證發佈點。  

2.  當選取 [為用戶端啟用 PXE 支援] 時，會將憑證傳送到執行 PXE 開機的電腦，如此電腦就可在部署作業系統期間連線到管理點。  

站台中的所有管理點都設定為使用 HTTP 時，會建立自我簽署憑證。 管理點設定為使用 HTTPS 時，則匯入 PKI 用戶端憑證。  

若要匯入憑證，請瀏覽至具有 PKI 憑證的公開金鑰加密標準 #12 (PKCS #12) 檔案，其應符合下列 Configuration Manager 需求：  

-   預期用途必須包含用戶端驗證。  

-   必須設定私密金鑰才可匯出。  

對於憑證主體名稱或主體別名 (SAN) 並無特定需求，您可以針對多個發佈點使用同一個憑證。  

如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。 如需此憑證的部署範例，請參閱[為 System Center Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)中的*部署發佈點的用戶端憑證*一節。  

**啟用此發佈點供預先設置的內容使用**  
選取此核取方塊以啟用預先設置內容的發佈點。 選取此核取方塊時，可在發佈內容時設定發佈行為。 您可以選擇是否永遠在發佈點上預先設置內容、預先設置套件的初始內容 (但在內容更新時使用一般內容發佈程序)，或是永遠對套件中的內容使用一般內容發佈程序。  

**界限群組**  
 您可以將界限群組關聯到發佈點。 部署內容期間，用戶端必須存在於與發佈點關聯的界限群組之中，才能將界限群組當成內容的來源位置使用。
 - **在 1610 版之前**，您可以選取 [允許內容的後援來源位置] 核取方塊，讓位於這些界限群組以外的用戶端回復，並在沒有其他發佈點可用時，將發佈點當成內容的來源位置使用。
 - **從 1610 版開始**，您無法再設定 [允許內容的後援來源位置]。  相反地，您可以設定界限群組之間的關聯性，以查看用戶端何時可以開始搜尋其他界限群組中的有效內容來源位置。

##  <a name="BKMK_Enrollment_Point"></a> 註冊點  
註冊點可用於安裝 Mac 電腦，且註冊利用內部部署行動裝置管理所管理的裝置。 如需詳細資訊，請參閱下列各項：  

-   [How to deploy clients to Macs in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md) (如何在 System Center Configuration Manager 中將用戶端部署至 Mac 電腦)  

-   [使用者如何在 System Center Configuration Manager 中使用內部部署行動裝置管理註冊裝置](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**允許的連線**  
 會自動選取 HTTPS 設定，且需要在伺服器上提供 PKI 憑證，以對註冊 Proxy 點進行伺服器驗證、對頻外服務點進行伺服器驗證，以及透過 SSL 加密資料。 如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 如需伺服器憑證的部署範例，以及如何在 IIS 中進行設定的資訊，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)的＜為執行 IIS 的站台系統部署 Web 伺服器憑證＞一節。  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> 註冊 Proxy 點  
如需如何設定行動裝置註冊 Proxy 點的資訊，請參閱 [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md) (使用者如何在 System Center Configuration Manager 中使用內部部署行動裝置管理註冊裝置)。  

**用戶端連線**  
 會自動選取 HTTPS 設定，且在伺服器上需要提供 PKI 憑證，才可對行動裝置及由 Configuration Manager 所註冊的 Mac 電腦進行伺服器驗證，並可透過安全通訊端層 (SSL) 進行資料加密。 如需憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

 如需伺服器憑證的部署範例，以及如何在 IIS 中進行設定的資訊，請參閱[為 Configuration Manager 部署 PKI 憑證的逐步範例：Windows Server 2008 憑證授權單位](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)的＜為執行 IIS 的站台系統部署 Web 伺服器憑證＞一節。  

##  <a name="BKMK_Fallback_Status_Point"></a> 後援狀態點  
[狀況訊息數目] 和 [節流間隔 (秒)]  
雖然這些選項的預設設定 (10,000 個狀況訊息和 3,600 秒的節流間隔) 足夠應付大部分情況，但您可能需要在以下兩種狀況為 True 時，變更設定：  

-   後援狀態點僅接受來自內部網路的連線。  

-   在為多部電腦進行用戶端部署首展期間，您會使用後援狀態點。  

在此案例中，持續的狀態訊息資料流可能會建立狀態訊息的積存，該積存會造成持續一段時間內之站台伺服器上的中央處理器 (CPU) 使用量過高。 此外，您可能會看不到 Configuration Manager 主控台以及在用戶端部署報告中用戶端部署的最新資訊。  

這些後援狀態點的設計，主要是針對用戶端部署期間所產生狀態訊息進行設定。 這些設定值並不是針對用戶端部署問題而設定，例如當網際網路上的用戶端無法連線到以網際網路為基礎的管理點時。 由於後援狀態點不能只是將這些設定值套用到用戶端部署期間所產生狀況訊息，所以請勿在後援狀態點接受網際網路的連線時設定這些設定值。  

成功安裝 System Center 2012 Configuration Manager 用戶端的每一部電腦，會將下列四種狀況訊息傳送到後援狀態點：  

-   已啟動用戶端部署  

-   成功完成用戶端部署  

-   已啟動用戶端指派  

-   成功完成用戶端指派  

無法安裝或指派 Configuration Manager 用戶端的電腦，會傳送其他的狀態訊息。  

例如，假設您將 Configuration Manager 用戶端部署到 20,000 部電腦，部署可能會傳送 80,000 個狀態訊息到後援狀態點。 因為預設的節流設定可每 3600 秒 (1 小時) 傳送 10,000 個狀態訊息到後援狀態點，所以狀態訊息可能會積存在後援狀態點上。 您也必須考慮到後援狀態點和站台伺服器之間的可用網路頻寬，以及可處理許多狀態訊息的狀態訊息處理能力。  

為避免發生這些問題，請考慮增加狀態訊息數目，並縮短節流間隔時間。  

如果下列其中一項條件為 True，請重設後援狀態點的節流值：  

-   您估計目前的節流值，比處理來自後援狀態點之狀況訊息所需的節流值還要高。  

-   您發現目前的節流設定值會在站台伺服器上造成高 CPU 使用量。  

除非您清楚會產生何種結果，否則請勿變更後援狀態點節流設定的設定值。 例如，當您新增過高的節流設定，站台伺服器上的 CPU 使用量便會增高，進而造成所有的站台作業變得緩慢。  
