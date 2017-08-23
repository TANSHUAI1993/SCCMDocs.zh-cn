---
title: "Technical Preview 1512 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1512 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 5cf8d54fbaa98a75ac2a875a23a43b1d3e5be0dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1512-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1512 中的功能

適用於︰System Center Configuration Manager (Technical Preview)

本文介紹 System Center Configuration Manager Technical Preview 1512 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。  

 以下是您可以使用此版本試用的新功能。  

##  <a name="bkmk_devicehealth"></a> 裝置健全狀況證明  
 從 Technical Preview 1512 開始，系統管理員可以在 Configuration Manager 中檢視 Windows 10 裝置健康情況證明的狀態。  這項功能適用於 Configuration Manager 以及搭配 Microsoft Intune 使用的 Configuration Manager。 系統管理員可透過裝置健全狀況證明，確認該用戶端電腦具有可信任的 BIOS、TPM 以及開機軟體設定。 若要支援裝置健全狀況證明，用戶端裝置必須執行 Win10，同時啟用 TPM 2。 裝置健全狀況證明會顯示為下列各項啟用的裝置數目：  

-   早期啟動反惡意程式碼  

-   BitLocker  

-   安全開機  

-   程式碼完整性  

主控台也會顯示排名在前最缺少的健全狀況證明設定，同時顯示裝置數目。  

若要預覽裝置健康情況證明檢視，請在 Configuration Manager 主控台中，移至 [監視] 工作區，按一下 [安全性] 節點，然後按一下 [健康情況證明]。  

##  <a name="bkmk_viewterms"></a> 在主控台中監視條款及條件  
從 Technical  Preview 1512 開始，當您將 Configuration Manager 與 Microsoft Intune 整合時，可以使用 Configuration Manager 主控台檢視哪些使用者已接受 IT 部門所設定的條款及條件，哪些使用者則未接受。  

**若要檢視摘要資訊：**  

-   在 Configuration Manager 主控台中，移至 [監視] > [概觀] > [部署]，然後選取您要檢視的條款及條件部署。  

**若要檢視詳細資訊：**  

1.  在 Configuration Manager 主控台中，移至 [資產與相容性] > [概觀] > [相容性設定] > [條款及條件]，然後選取您要檢視的條款及條件。  

2.  在主控台的底部，依序選取 [部署] 索引標籤和部署，然後按一下 [檢視狀態]。  

##  <a name="bkmk_EPpolicy"></a> Endpoint Protection 原則設定的改善  
在 1512 Technical Preview 中，我們已在 Endpoint Protection 反惡意程式碼原則中新增下列新的設定：  

-   即時保護：**在下載時及安裝前封鎖潛在的垃圾應用程式**  

    -   潛在的垃圾應用程式 (PUA) 是依據評價與研究導向識別碼所區分的威脅分類。 這些最常見的潛在垃圾應用程式為垃圾應用程式搭配程式或其搭配的應用程式。  

    -   預設會啟用保護原則設定 (設定為 [是])。 在啟用的情況下，這個設定於下載和安裝時，會封鎖 PUA。 不過，您可以排除特定檔案或資料夾，以符合您環境的特定需求。  

-   掃描設定：**執行完整掃描時，掃描網路對應的網路磁碟**  

    -   此設定為系統管理員提供能以更細微的方式隨選掃描網路檔案，而能避開在排程進行完整掃描期間，會一律掃描對應網路磁碟機的風險。  

    -   必須對此設定先啟用 [掃描網路檔案] 設定 (設為 [是])，才可進行設定。  

    -   此設定預設會是 [否]，表示完整掃描不會存取對應的網路磁碟機。  

-   提交自動範例檔案設定：  

     反惡意程式碼引擎可能會要求將範例檔案傳送給 Microsoft，進行進一步分析。 根據預設，在傳送這類範例前一律會出現提示。 系統管理員現已可管理下列設定，來設定此行為：  

    -   進階：**啟用自動範例檔提交，可協助 Microsoft 判定某些偵測到的項目是否為惡意**：將此設定變更為 [是] 可啟用自動範例檔提交。 此設定預設為 [否]，表示停用自動提交範例檔案，而且在傳送範例之前將提示使用者。   (此項設定最初由 System Center 2012 R2 Configuration Manager SP1 時採用)  

    -   進階：**允許使用者修改自動範例檔案提交設定**：此設定會決定對裝置具有本機系統管理權限的使用者，是否可以在用戶端介面中變更自動範例檔提交設定。 此設定預設為 [否]，表示設定只能從 Configuration Manager 主控台變更，且裝置的本機系統管理員無法變更此設定。  

         例如，下圖顯示系統管理員已啟用 Windows 10 中的 Windows Defender 設定，而且不允許使用者進行修改：  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    此外，Endpoint Protection 反惡意程式碼原則的 [排除設定] 區段中現有的 [排除檔案及資料夾] 設定，已改良為可以排除裝置。 例如：您現已可以指定排除下列項目： **\device\mvfs** (適用於多版本檔案系統)。 此原則不會驗證裝置路徑。要在用戶端上為反惡意程式碼引擎提供 Endpoint Protection 原則，使其必須能夠解譯裝置字串。  

**使用 Endpoint Protection 原則的必要條件：**  

必須先使用 Endpoint Protection 用戶端設定，安裝及管理 Endpoint Protection 用戶端，才可使用 Endpoint Protection 原則。 若是使用 Windows 7、Windows 8、Windows 8.1 之 System Center Endpoint Protection 用戶端，或是 Windows 10 受管理的 Windows Defender，則此作業已完成。 請參閱 [System Center Configuration Manager 中的 Endpoint Protection](../../protect/deploy-use/endpoint-protection.md)。  
