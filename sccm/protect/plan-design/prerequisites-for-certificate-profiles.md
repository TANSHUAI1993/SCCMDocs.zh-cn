---
title: "憑證設定檔必要條件 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的憑證設定檔以及其外部相依性和產品中的相依性。"
ms.custom: na
ms.date: 03/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
caps.latest.revision: "9"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: fba52ee305fe67418f2fe544bfe94d10467236d0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中憑證設定檔的先決條件

*適用於：System Center Configuration Manager (最新分支)*


System Center Configuration Manager 中的憑證設定檔具有外部相依性和產品中的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|執行 Active Directory 憑證服務 (AD CS) 的企業發行憑證授權單位 (CA)。<br /><br /> 若要撤銷頂層階層的站台伺服器之電腦帳戶的憑證，需要 Configuration Manager 中憑證設定檔所使用之每個憑證範本的 *發行及管理憑證* 權限。 或者，授與憑證管理員權限以授與所有由該 CA 所使用的憑證範本權限。<br /><br /> 支援由管理員核准憑證要求。 不過，用來發行憑證的憑證範本必須針對憑證主體設定為 [在要求中提供]，System Center Configuration Manager 才能自動提供這個值。|如需有關 Active Directory 憑證服務的詳細資訊，請參閱您的 Windows Server 文件。<br /><br /> Windows Server 2012： [Active Directory 憑證服務概觀](http://go.microsoft.com/fwlink/p/?LinkId=286744)<br /><br /> Windows Server 2008： [Windows Server 2008 中的 Active Directory 憑證服務](http://go.microsoft.com/fwlink/p/?LinkId=115018)|  
|Active Directory 憑證服務的網路裝置註冊服務角色服務 (在 Windows Server 2012 R2 上執行)。<br /><br /> 其他情況：<br /><br /> 用戶端與網路裝置註冊服務之間的通訊不支援 TCP 443 (供 HTTPS 使用) 或 TCP 80 (供 HTTP 使用) 以外的連接埠號碼。<br /><br /> 執行網路裝置註冊服務的伺服器必須位於與發行 CA 不同的伺服器上。|System Center Configuration Manager 會在 Windows Server 2012 R2 中與網路裝置註冊服務通訊，以產生並驗證簡單憑證註冊通訊協定 (SCEP) 要求。<br /><br /> 如果您將憑證發行給從網際網路連線的使用者或裝置 (如 Microsoft Intune 所管理的行動裝置)，則這些裝置必須能夠從網際網路存取執行網路裝置註冊服務的伺服器。 例如，在周邊網路 (也稱為遮蔽式子網路) 中安裝伺服器。<br /><br /> 如果您在執行網路裝置註冊服務的伺服器和發行 CA 的伺服器之間有防火牆，就必須將防火牆設定為允許兩個伺服器之間的通訊 (DCOM)。 這項防火牆需求也適用於執行 System Center Configuration Manager 站台伺服器和發行 CA 的伺服器，如此 System Center Configuration Manager 才能撤銷憑證。<br /><br /> 如果網路裝置註冊服務設定為需要 SSL，則安全性最佳作法是確保連線的裝置可以存取憑證撤銷清單 (CRL) 以驗證伺服器憑證。<br /><br /> 如需 Windows Server 2012 R2 中網路裝置註冊服務的詳細資訊，請參閱 [Using a Policy Module with the Network Device Enrollment Service (使用原則模組搭配網路裝置註冊服務)](http://go.microsoft.com/fwlink/p/?LinkId=328657)。|  
|如果發行 CA 執行 Windows Server 2008 R2，則伺服器需要適用於 SCEP 更新要求的 Hotfix。|如果 Hotfix 尚未安裝在發行 CA 電腦上，請安裝 Hotfix。 如需詳細資訊，請參閱 Microsoft 知識庫中的文章 [2483564：如果使用 NDES 管理憑證，Windows Server 2008 R2 中 SCEP 憑證的更新要求會失敗](http://go.microsoft.com/fwlink/?LinkId=311945) 。|  
|PKI 用戶端驗證憑證和匯出的根 CA 憑證。|此憑證會對 System Center Configuration Manager 驗證執行網路裝置註冊服務的伺服器。<br /><br /> 如需詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)。|  
|支援的裝置作業系統。|您可以將憑證設定檔部署至執行 iOS、Windows 8.1、Windows RT 8.1、Windows 10 和 Android 作業系統的裝置上。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 相依性  

|相依性|詳細資訊|  
|----------------|----------------------|  
|憑證登錄點網站系統角色|您必須先安裝憑證登錄點網站系統角色，才能使用憑證設定檔。 此角色會與 System Center Configuration Manager 資料庫、System Center Configuration Manager 站台伺服器和 System Center Configuration Manager 原則模組進行通訊。<br /><br /> 如需此站台系統角色的系統需求，以及此角色在階層中之安裝位置的詳細資訊，請參閱 [System Center Configuration Manager 的支援設定](../../core/plan-design/configs/supported-configurations.md)主題中的＜站台系統需求＞一節。<br /><br /> 請注意，憑證登錄點不能安裝在執行網路裝置註冊服務的同一部伺服器上。|  
|安裝在執行 Active Directory 憑證服務之網路裝置註冊服務角色服務的伺服器上的 System Center Configuration Manager 原則模組|若要部署憑證設定檔，您必須安裝 System Center Configuration Manager 原則模組。 您可以在 System Center Configuration Manager 安裝媒體上找到此原則模組。|  
|探索資料|憑證主體以及主體別名的值都是由 System Center Configuration Manager 提供，並且是從探索收集的資訊擷取而來：<br /><br /> 使用者憑證：Active Directory 使用者探索。<br /><br /> 電腦憑證：Active Directory 系統探索和網路探索。|  
|管理憑證設定檔的特定安全性權限|您必須具有下列安全性權限才能管理公司資源存取設定，例如憑證設定檔、Wi-Fi 設定檔和 VPN 設定檔：<br /><br /> 檢視與管理憑證設定檔的警示和報告：[警示] 物件的 [建立] 、[刪除] 、[修改] 、[修改報告] 、[讀取]  及 [執行報告]  。<br /><br /> 建立和管理憑證設定檔：[憑證設定檔] 物件的 [撰寫原則] 、[修改報告]  、[讀取]  及 [執行報告]  。<br /><br /> 管理 Wi-Fi、憑證和 VPN 設定檔部署：[集合] 物件的 [部署組態原則] 、[修改用戶端狀態警示] 、[讀取]  及 [讀取資源]  。<br /><br /> 管理所有組態原則：[組態原則] 物件的 [建立] 、[刪除] 、[修改]  、[讀取]  及 [設定安全性範圍]  。<br /><br /> 執行憑證設定檔相關的查詢：[查詢]  物件的 [讀取]  權限。<br /><br /> 在 System Center Configuration Manager 主控台中檢視憑證設定檔資訊：[站台] 物件的 [讀取] 權限。<br /><br /> 檢視憑證設定檔的狀態訊息：[狀態訊息]  物件的 [讀取]  權限。<br /><br /> 建立和修改信任的 CA 憑證設定檔：[信任的 CA 憑證設定檔] 物件的 [撰寫原則] 、[修改報告]  、[讀取]  及 [執行報告]  。<br /><br /> 建立和管理 VPN 設定檔：[VPN 設定檔] 物件的 [撰寫原則] 、[修改報告]  、[讀取]  及 [執行報告]  。<br /><br /> 建立和管理 Wi-Fi 設定檔：[Wi-Fi 設定檔] 物件的 [撰寫原則] 、[修改報告]  、[讀取]  及 [執行報告]  。<br /><br /> [公司資源存取管理員] 安全性角色包括在 System Center Configuration Manager 中管理憑證設定檔所需的上列權限。 如需詳細資訊，請參閱 **Configure role-based administration** 主題中的 [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md) 一節。|  
