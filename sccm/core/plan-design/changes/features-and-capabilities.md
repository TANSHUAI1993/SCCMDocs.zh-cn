---
title: "特色與功能 | Microsoft Docs"
description: "深入了解 System Center Configuration Manager 的主要管理功能。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4691f43dccdf73936107f4635321897b9779bead
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>System Center Configuration Manager 的功能

*適用於：System Center Configuration Manager (最新分支)*

以下是 System Center Configuration Manager 的主要管理功能。 每一項功能都有自己的必要條件，而且您要使用的功能可能影響 Configuration Manager 階層的設計和實作。 例如，如果您要將軟體部署至階層中的裝置，則必須安裝發佈點網站系統角色。  

 如需如何規劃和安裝 Configuration Manager 以便在您的環境中支援這些管理功能的詳細資訊，請參閱[準備開始使用 System Center Configuration Manager](../../../core/plan-design/get-ready.md)。  

 **應用程式管理**  

 提供一組工具和資源，可幫助您建立、管理、部署及監視您所管理一系列不同裝置中的應用程式。 此外，Configuration Manager 提供您工具來協助保護您在使用者應用程式中的公司資料。 請參閱[應用程式管理簡介](/sccm/apps/understand/introduction-to-application-management)。

 **公司資源存取**  

 提供一組工具和資源，方便組織中的使用者從遠端位置存取資料和應用程式。 這些工具包括 Wi-Fi 設定檔、VPN 設定檔、憑證設定檔，以及對 Exchange 和 SharePoint Online 的條件存取。 請參閱[使用 System Center Configuration Manager 保護資料和站台基礎結構](../../../protect/understand/protect-data-and-site-infrastructure.md)和[管理 System Center Configuration Manager 中的服務存取權](../../../protect/deploy-use/manage-access-to-services.md)。  

 **相容性設定**  

 提供一組工具和資源，可幫助您評估、追蹤及補救企業中用戶端裝置的設定相容性。 此外，您可以使用相容性設定來設定一系列您所管理裝置上的功能和安全性設定。 請參閱[使用 System Center Configuration Manager 確裝置合規性](../../../compliance/understand/ensure-device-compliance.md)。  

 **Endpoint Protection**  

 為企業中的電腦提供安全性、反惡意程式碼及 Windows 防火牆管理。 請參閱 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

 **清查**  

 提供一組工具幫助您識別及監視資產：  

-   **硬體清查**：收集有關企業中裝置硬體的詳細資訊。 請參閱 [System Center Configuration Manager 中的硬體清查簡介](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md)。  

-   **軟體清查**：收集和報告組織中用戶端電腦上所儲存檔案的資訊。 請參閱 [System Center Configuration Manager 中的軟體清查簡介](../../../core/clients/manage/inventory/introduction-to-software-inventory.md)。  

-   **Asset Intelligence**：提供收集企業中清查資料及監視軟體授權使用情形的工具。 請參閱 [System Center Configuration Manager 中的 Asset Intelligence 簡介](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)。  

**使用 Microsoft Intune 的行動裝置管理**  

 您可以透過網際網路使用 Microsoft Intune 服務，進而使用 Configuration Manager 來管理 iOS、Android (包含 Samsung KNOX Standard)、Windows Phone 以及 Windows 裝置。

 雖然您是使用 Intune 服務，但是管理工作是利用服務站台系統角色 (可透過 Configuration Manager 主控台取得) 來完成。 請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)。  

 **內部部署行動裝置管理**  

 使用內部部署 Configuration Manager 基礎結構和裝置平台內建的管理功能，來註冊及管理電腦與行動裝置 (而不是依賴個別安裝的 Configuration Manager 用戶端)。 目前支援管理 Windows 10 企業版和 Windows 10 行動裝置版裝置。 請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

 **作業系統部署**  

 提供建立作業系統映像的工具。 接著您可以使用 PXE 開機或可開機媒體 (像是 CD 組、DVD 或 USB 快閃磁碟機)，利用這些映像將作業系統部署至電腦。 請注意，這適用於 Configuration Manager 所管理的電腦，以及未受管理的電腦。 請參閱 [System Center Configuration Manager 的作業系統部署簡介](../../../osd/understand/introduction-to-operating-system-deployment.md)。  

 **電源管理**  

 提供一組工具和資源，可讓您用來管理和監視企業中用戶端電腦的功率耗用量。 請參閱 [System Center Configuration Manager 的電源管理簡介](../../../core/clients/manage/power/introduction-to-power-management.md)。  

 **查詢**  

 提供一項工具，可擷取階層中資源的相關資訊，以及有關清查資料和狀態訊息的資訊。 您接著可以使用這項資訊來報告或定義裝置或使用者集合，以進行軟體部署和組態設定。 請參閱 [System Center Configuration Manager 的查詢簡介](../../../core/servers/manage/introduction-to-queries.md)。  

 **遠端連線設定檔**  

 提供一組工具和資源，協助您建立、部署和監視組織中各裝置的遠端連線設定。 藉由部署這些設定，可將使用者連線到其公司網路中電腦所需的時間縮到最短。 請參閱[在 System Center Configuration Manager 中使用遠端連線設定檔](/sccm/compliance/deploy-use/create-remote-connection-profiles)。  

 **使用者資料和設定檔組態項目**  

 Configuration Manager 中的使用者資料和設定檔設定項目包含一些設定，這些設定可為階層中的使用者管理執行 Windows 8 及更新版本電腦上的資料夾重新導向、離線檔案和漫遊設定檔。 請參閱[在 System Center Configuration Manager 中使用使用者資料和設定檔設定項目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)。  

 **遠端控制**  

 提供從 Configuration Manager 主控台遠端管理用戶端電腦的工具。 請參閱 [System Center Configuration Manager 的遠端控制簡介](../../../core/clients/manage/remote-control/introduction-to-remote-control.md)。  

 **報告**  

 提供一組工具和資源，可幫助您從 Configuration Manager 主控台使用 SQL Server Reporting Services 的進階報告功能。 請參閱 [System Center Configuration Manager 的報告簡介](../../../core/servers/manage/introduction-to-reporting.md)。  

 **軟體計量**  

 提供從 Configuration Manager 用戶端監視及收集軟體使用資料的工具。 請參閱[在 System Center Configuration Manager 中使用軟體計量監視應用程式使用量](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。  

 **軟體更新**  

 提供一組工具和資源，可幫助您管理、部署及監視企業中的軟體更新。 請參閱 [System Center Configuration Manager 的軟體更新簡介](/sccm/sum/understand/software-updates-introduction)。  
