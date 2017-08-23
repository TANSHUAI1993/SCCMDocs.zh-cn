---
title: "在 System Center Configuration Manager 中設定安全性 | Microsoft Docs"
description: "設定 System Center Configuration Manager 的安全性相關選項。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0034381a7a388ddc3eda5e774f3c63d741336301
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-security-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中設定安全性

*適用於：System Center Configuration Manager (最新分支)*

請使用本文的資訊，協助設定 System Center Configuration Manager 的安全性相關選項。  

##  <a name="BKMK_ConfigureClientPKI"></a> 設定用戶端 PKI 憑證的設定  
如果您想要使用公開金鑰基礎結構 (PKI) 憑證，和使用 Internet Information Services (IIS) 的站台系統進行用戶端連線，請使用下列程序設定這些憑證的設定。  

#### <a name="to-configure-client-pki-certificate-settings"></a>設定用戶端 PKI 憑證設定  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [站台設定]，選擇 [站台]，然後選擇要設定的主要站台。  

3.  在 [首頁] 索引標籤的 [內容] 群組中選擇 [內容]，然後選擇 [用戶端電腦通訊] 索引標籤。  

    這個索引標籤只能在主要站台使用。 如果沒有看到 [用戶端電腦通訊]  索引標籤，請確認您未連線到管理中心網站或次要站台。  

4.  當您想要讓指派給站台的用戶端，在連線到使用 IIS 的站台系統時一律使用用戶端 PKI 憑證，請選擇 [僅 HTTPS]。 或者，當您不需要讓用戶端使用 PKI 憑證時，請選擇 [HTTPS 或 HTTP]。  

5.  如果選擇的是 [HTTPS 或 HTTP]，請在您想要使用用戶端 PKI 憑證進行 HTTP 連線時，選擇 [使用可用的 PKI 用戶端憑證 (用戶端驗證功能)]。 用戶端會改用此憑證而非使用自我簽署憑證，以對站台系統做自我驗證。 如果您選擇 [僅 HTTPS]，則會自動選擇此選項。  

    當用戶端被偵測到在網際網路上，或是對僅使用網際網路的用戶端管理進行設定時，這些用戶端永遠都會使用用戶端 PKI 憑證。  

6.  當用戶端有一個以上有效的 PKI 用戶端憑證可用時，可選擇 [修改] 設定所選的用戶端選取方法，然後選擇 [確定]。  

    如需用戶端憑證選取方法的詳細資訊，請參閱[規劃 PKI 用戶端憑證選取](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)。  

7.  選取或清除讓用戶端檢查憑證撤銷清單 (CRL) 的核取方塊。  

    如需用戶端 CRL 檢查的詳細資訊，請參閱[規劃 PKI 憑證撤銷](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。  

8.  如果必須為用戶端指定受信任根憑證授權單位 (CA) 憑證，請選擇 [設定]，匯入根 CA 憑證檔案，然後選擇 [確定]。  

    如需此設定的詳細資訊，請參閱[規劃 PKI 受信任根憑證及憑證簽發者清單](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs)。  

9. 選擇 [確定] 關閉站台的內容對話方塊。  

為階層中的所有主要站台重複此程序。  

##  <a name="BKMK_ConfigureSigningEncryption"></a> 設定簽署及加密  
為站台系統設定站台之所有用戶端皆支援的最安全簽署及加密設定。 這些設定在您讓用戶端使用自我簽署憑證透過 HTTP 與站台系統通訊時，尤其重要。  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>設定站台的簽署及加密  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [系統管理] 工作區中，展開 [站台設定]，選擇 [站台]，然後選擇要設定的主要站台。  

3.  在 [首頁] 索引標籤的 [內容] 群組中選擇 [內容]，然後選擇 [簽署和加密] 索引標籤。  

    這個索引標籤只能在主要站台使用。 如果沒有看到 [簽署和加密]  索引標籤，請確認您未連線到管理中心網站或次要站台。  

4.  設定所需的簽署及加密選項，然後選擇 [確定]。  

    > [!WARNING]  
    >  請先確認可能指派給站台的所有用戶端皆可支援此雜湊演算法，或者擁有有效的 PKI 用戶端驗證憑證，然後選擇 [需要 SHA-256]。 您可能必須在用戶端上安裝更新或 Hotfix，以支援 SHA-256 。 例如，執行 Windows Server 2003 SP2 的電腦必須安裝 [知識庫文章 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)中所參照的 Hotfix。  
    >   
    >  如果您選擇此選項，而用戶端不支援 SHA-256 及使用自我簽署憑證，則 Configuration Manager 會拒絕這些設定。 在此案例中，SMS_MP_CONTROL_MANAGER 元件會記錄訊息識別碼 5443。  

5.  選擇 [確定] 關閉站台的 [內容] 對話方塊。  

為階層中的所有主要站台重複此程序。  

##  <a name="BKMK_ConfigureRBA"></a> 設定以角色為基礎的系統管理  
以角色為基礎的系統管理結合了安全性角色、安全性範圍和指派的集合，為每個系統管理使用者定義系統管理範圍。 系統管理範圍包含系統管理使用者可以在 Configuration Manager 主控台中檢視的物件，以及與這些系統管理使用者擁有執行權限之物件相關的工作。 以角色為基礎的系統管理設定會套用到階層中的每個站台。  

下列為[為 System Center Configuration Manager 設定以角色為基礎的系統管理](../../../core/servers/deploy/configure/configure-role-based-administration.md)一文之相關章節的連結：  

-   [建立自訂安全性角色](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [設定安全性角色](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [設定物件的安全性範圍](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [設定集合以管理安全性](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [建立新的系統管理使用者](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [修改系統管理使用者的系統管理範圍](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  您自己的系統管理範圍，定義您在為其他系統管理使用者設定以角色為基礎的系統管理時，可指派的物件和設定。 如需規劃以角色為基礎之系統管理的詳細資訊，請參閱 [System Center Configuration Manager 以角色為基礎之系統管理的基礎](../../../core/understand/fundamentals-of-role-based-administration.md)。  

##  <a name="BKMK_ManageAccounts"></a> 管理 Configuration Manager 使用的帳戶  
Configuration Manager 支援用於多種不同工作及用途的 Windows 帳戶。  

利用下列程序檢視針對不同工作設定的帳戶，以及管理 Configuration Manager 用於每個帳戶的密碼。  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>管理 Configuration Manager 使用的帳戶  

1.  在 Configuration Manager 主控台中，選擇 [系統管理]。  

2.  在 [管理] 工作區中，展開 [安全性]，然後選擇 [帳戶]，以檢視針對 Configuration Manager 設定的帳戶。  

3.  若要變更針對 Configuration Manager 所設定帳戶的密碼，請選擇帳戶。  

4.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

5.  選擇 [設定] 以開啟 [Windows 使用者帳戶] 對話方塊，並指定 Configuration Manager 的新密碼，以使用該帳戶。  

    > [!NOTE]  
    >  您指定的密碼必須符合在 [Active Directory 使用者和電腦] 中為帳戶指定的密碼。  

6.  選擇 [確定] 完成程序。  
