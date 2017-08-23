---
title: "使用憑證授權單位建立 PFX 憑證設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 PFX 檔案，產生支援加密資料交換的使用者特定憑證。"
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 43d8b2217763681be69711fce93c020a65da1cd8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>如何使用憑證授權單位建立 PFX 憑證設定檔

適用於：System Center Configuration Manager (最新分支)

在本文中，您將了解如何使用憑證授權單位建立認證的憑證設定檔。

[憑證設定檔](../../protect/deploy-use/introduction-to-certificate-profiles.md)提供有關建立及設定憑證設定檔的一般資訊。 本主題會強調說明一些與 PFX 憑證相關之憑證設定檔的特定資訊。

## <a name="pfx-certificate-profiles"></a>PFX 憑證設定檔
System Center Configuration Manager 可讓您使用憑證授權單位所核發的認證來建立 PFX 憑證設定檔。  從 1706 版開始，您可以選擇 Microsoft 或 Entrust 作為您的憑證授權單位。  部署到使用者裝置時，個人資訊交換 (.pfx) 檔案會產生使用者特定憑證，以支援加密的資料交換。

若要從現有的憑證檔案匯入憑證認證，請參閱[如何透過匯入憑證詳細資料建立 PFX 憑證設定檔](../../mdm/deploy-use/import-pfx-certificate-profiles.md)。

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>建立及部署個人資訊交換 (PFX) 憑證設定檔  

### <a name="get-started"></a>開始使用

1.  在 System Center Configuration Manager 主控台中，選擇 [資產與相容性]。  
2.  在 [資產與合規性] 工作區中，依序選擇 [合規性設定]&gt;[公司資源存取]&gt;[憑證設定檔]。  

3.  在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立憑證設定檔]。

4.  在 [建立憑證設定檔精靈] 的 [一般] 頁面上，指定下列資訊：  

    -   **名稱**：輸入憑證設定檔的唯一名稱。 您最多可以使用 256 個字元。  

    -   **描述**：提供一段描述以說明憑證設定檔的概觀，以及可協助您在 System Center Configuration Manager 主控台中進行識別的其他相關資訊。 您最多可以使用 256 個字元。  

    -   在 [指定您要建立的憑證設定檔類型] 中，選擇 [個人資訊交換 -- PKCS #12 (PFX) 設定 - 建立]，然後從下拉式清單中選擇您的憑證授權單位。  從 1706 版開始，您可以選擇 **Microsoft** 或 **Entrust**。

### <a name="select-supported-platforms"></a>選取支援的平台

[支援的平台] 頁面可識別憑證設定檔支援的作業系統和裝置。  

憑證設定檔可支援多個作業系統及裝置，不過，某些作業系統或裝置組合可能需要不同的設定。  在這些情況下，最好為個別的設定組合建立獨立的設定檔。  

從 1706 版開始，有下列選項可供使用：

- Windows 10
    - 所有 Windows 10 (64 位元)
    - 所有 Windows 10 (32 位元)
    - 所有 Windows 10 全像攝影版企業版和更新版本
    - 所有 Windows 10 全像攝影版和更新版本
    - 所有 Windows 10 團隊版和更新版本
    - 所有 Windows 10 行動裝置版和更新版本
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> 目前不支援 MacOS/OSX 裝置。  

未選取其他任何選項時，[全選] 核取方塊會選取所有可用的選項。  選取一或多個選項時，[全選] 會清除現有的選取項目。 

1.  選取一或多個憑證設定檔支援的平台。

1.  選擇 [下一步] 以繼續。  


### <a name="configure-certification-authorities"></a>設定憑證授權單位

在這裡，您可以選擇處理 PFX 憑證的憑證登錄點 (CRP)。  

1.  從 [主要站台] 清單中，選擇包含 CA 之 CRP 角色的伺服器。
1.  從 [憑證授權單位] 清單中，在左側資料行放置核取記號來選擇相關的 CA。
1.  準備好繼續進行時，請選擇 [下一步]。

若要深入了解，請參閱[憑證基礎結構](../../protect/deploy-use/certificate-infrastructure.md)。


### <a name="configure-certificate-settings-for-microsoft-ca"></a>設定 Microsoft CA 的憑證設定

若要設定 Microsoft 作為 CA 時的憑證設定：

1.  從 [憑證範本名稱] 下拉式清單中選擇憑證範本。

1.  啟用 [憑證使用方式] 核取方塊，以將憑證設定檔使用於 S/MIME 簽署或加密。

    使用 Microsoft 作為 CA 時若核取此選項，與目標使用者相關聯的所有 PFX 憑證都會傳遞至使用者註冊的所有裝置。  未選取此核取方塊時，每個裝置會收到唯一的憑證。  

1.  將 [主體名稱格式] 設為 [一般名稱] 或 [完整的辨別名稱]。  如果不確定要使用何者，請連絡您的憑證授權單位系統管理員。

1.  針對 [主體別名]，視需要為您的 CA 啟用 [電子郵件地址] 和 [使用者主體名稱 (UPN)]。

1.  [更新閾值] 會根據到期前剩餘的時間百分比來決定何時自動更新憑證。

1.  將 [憑證有效期間] 設為憑證的存留期。  設定一個 1-100 之間的數字和一段期間 (年、月或日) 以指定期間。

1.  當憑證登錄點指定 Active Directory 認證時，會啟用 [Active Directory 發佈]。  啟用此選項會將憑證設定檔發佈至 Active Directory。

1.  如果您在指定支援的平台時選取一或多個 Windows 10 平台：

    1.  將 [Windows 憑證存放區] 設為 [使用者]。  ([本機電腦] 選項不會部署憑證，不應選擇此選項。)
    1.  從下列其中一個選項選取 [金鑰儲存提供者 (KSP)]：

        - **安裝至信賴平台模組 (TPM) (若存在)**  
        - **安裝至信賴平台模組 (TPM)，否則便失敗** 
        - **安裝至 Windows Hello 企業版否則便失敗** 
        - **安裝至軟體金鑰儲存提供者** 

1.  完成後，選擇 [下一步] 或 [摘要]。

### <a name="configure-certificate-settings-for-entrust-ca"></a>設定 Entrust CA 的憑證設定

若要設定 Entrust 作為 CA 時的憑證設定：

1.  從 [數位識別碼設定] 下拉式清單中，選擇組態設定檔。  數位識別碼設定選項是由 Entrust 系統管理員建立。

1.  核取 [憑證使用方式] 時，會將憑證設定檔使用於 S/MIME 簽署或加密。

    使用 Entrust 作為 CA 時，與目標使用者相關聯的所有 PFX 憑證都會傳遞至使用者註冊的所有裝置。    *未*核取此核取方塊時，每個裝置會收到唯一的憑證。  (不同的 CA 會有不同的行為；若要深入了解，請參閱對應的章節)。

1.  使用 [格式] 按鈕將 Entrust **主體名稱格式**權杖對應至 ConfigMgr 欄位。  

    [憑證名稱格式] 對話方塊會列出 Entrust 數位識別碼設定變數。  針對每個 Entrust 變數，從相關聯的下拉式清單中選擇適當的 LDAP 變數。

1.  使用 [格式] 按鈕將 Entrust **主體替代名稱**權杖對應至支援的 LDAP 變數。  

    [憑證名稱格式] 對話方塊會列出 Entrust 數位識別碼設定變數。  針對每個 Entrust 變數，從相關聯的下拉式清單中選擇適當的 LDAP 變數。

1.  [更新閾值] 會根據到期前剩餘的時間百分比來決定何時自動更新憑證。

1.  將 [憑證有效期間] 設為憑證的存留期。  設定一個 1-100 之間的數字和一段期間 (年、月或日) 以指定期間。

1.  當憑證登錄點指定 Active Directory 認證時，會啟用 [Active Directory 發佈]。  啟用此選項會將憑證設定檔發佈至 Active Directory。

1.  如果您在指定支援的平台時選取一或多個 Windows 10 平台：

    1.  將 [Windows 憑證存放區] 設為 [使用者]。  ([本機電腦] 選項不會部署憑證，不應選擇此選項。)
    1.  從下列其中一個選項選取 [金鑰儲存提供者 (KSP)]：

        - **安裝至信賴平台模組 (TPM) (若存在)**  
        - **安裝至信賴平台模組 (TPM)，否則便失敗** 
        - **安裝至 Windows Hello 企業版否則便失敗** 
        - **安裝至軟體金鑰儲存提供者** 

1.  完成後，選擇 [下一步] 或 [摘要]。


### <a name="finish-up"></a>完成

1.  在 [摘要] 頁面上，檢視您的選取項目，並確認您的選擇。

1.  準備就緒時，選擇 [下一步] 以建立設定檔。  

1.  包含 PFX 檔案的憑證設定檔現在可從 [憑證設定檔]  工作區取得。 

1.  若要部署設定檔：

    1. 開啟 [資產與相容性] 工作區。
    1. 選擇 [相容性設定] > [公司資源存取] > [憑證設定檔]
    1. 以滑鼠右鍵按一下所需的憑證設定檔，然後選擇 [部署]。 


## <a name="see-also"></a>請參閱
[建立新的憑證設定檔](../../protect/deploy-use/create-certificate-profiles.md)會逐步引導您完成 [建立憑證設定檔精靈]。

[如何透過匯入憑證詳細資料建立 PFX 憑證設定檔](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[部署 Wi-Fi、VPN、電子郵件和憑證設定檔](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)描述如何部署憑證設定檔。