---
title: "設定憑證基礎結構 | Microsoft Docs"
description: "了解如何在 Configuration Manager 中設定憑證註冊。"
ms.custom: na
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
caps.latest.revision: "7"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 640eb1df9d53fc83d93c39a7ecbaf2668e176805
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-certificate-infrastructure"></a>設定憑證基礎結構

適用於：System Center Configuration Manager (最新分支)

了解在 System Center Configuration Manager 中設定憑證基礎結構。 在開始之前，請先檢查 [System Center Configuration Manager 中憑證設定檔的先決條件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)中列出的任何先決條件。  

使用下列步驟來設定 SCEP 或 PFX 憑證的基礎結構。

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>步驟 1 - 安裝及設定網路裝置註冊服務和相依性 (僅適用於 SCEP 憑證)

 您必須安裝及設定 Active Directory 憑證服務 (AD CS) 的網路裝置註冊服務角色服務、變更憑證範本的安全性權限、部署公開金鑰基礎結構 (PKI) 用戶端驗證憑證，並編輯登錄以增加 Internet Information Services (IIS) 預設 URL 大小限制。 若有需要，您還必須設定發行憑證授權單位 (CA) 以允許自訂有效期間。  

> [!IMPORTANT]  
>  在設定 System Center Configuration Manager 以使用網路裝置註冊服務之前，請先驗證網路裝置註冊服務的安裝和設定。 如果這些相依性無法正常運作，您在使用 System Center Configuration Manager 進行憑證註冊疑難排解時將會遇到困難。  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>安裝及設定網路裝置註冊服務和相依性  

1.  在執行 Windows Server 2012 R2 的伺服器上，為 Active Directory 憑證服務伺服器角色安裝及設定網路裝置註冊服務角色服務。 如需詳細資訊，請參閱 TechNet 上 Active Directory 憑證服務文件庫中的 [網路裝置註冊服務指南](http://go.microsoft.com/fwlink/p/?LinkId=309016) 。  

2.  檢查並在必要時修改網路裝置註冊服務使用的憑證範本安全性權限：  

    -   執行 System Center Configuration Manager 主控台的帳戶：[讀取] 權限。  

         這是執行建立憑證設定檔精靈的必要權限，您可以進行瀏覽以選取在建立 SCEP 設定檔時使用的憑證範本。 選取憑證範本就表示系統會自動填入精靈中的某些設定，因此您不需要進行太多設定，同時也可降低所選設定與網路裝置註冊服務使用之憑證範本不相容的風險。  

    -   網路裝置註冊服務應用程式集區使用的 SCEP 服務帳戶：[讀取]  和 [註冊]  權限。  

         此需求並非專門針對 System Center Configuration Manager，但它是設定網路裝置註冊服務的一部分。 如需詳細資訊，請參閱 TechNet 上 Active Directory 憑證服務文件庫中的 [網路裝置註冊服務指南](http://go.microsoft.com/fwlink/p/?LinkId=309016) 。  

    > [!TIP]  
    >  若要識別網路裝置註冊服務使用的憑證範本，請在執行網路裝置註冊服務的伺服器上檢視下列登錄機碼：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP。  

    > [!NOTE]  
    >  這些是適用於大部分環境的預設安全性權限。 不過，您也可以使用替代的安全性設定。 如需詳細資訊，請參閱[規劃憑證設定檔在 System Center Configuration Manager 中的憑證範本權限](../../protect/plan-design/planning-for-certificate-template-permissions.md)。  

3.  將可支援用戶端驗證 的 PKI 憑證部署至此伺服器。 您可能已在可使用的電腦上安裝適用的憑證，或者您可能需要 (或想要) 特別部署適合此用途的憑證。 如需此憑證需求的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../core/plan-design/network/pki-certificate-requirements.md)主題中＜伺服器的 PKI 憑證＞一節之「使用網路裝置註冊服務角色服務執行 Configuration Manager 原則模組的伺服器」中的詳細資訊。  

    > [!TIP]  
    >  如果您需要部署此憑證的協助，您可以使用[部署發佈點的用戶端憑證](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012)的指示，因為其憑證需求完全相同，但有一點例外：  
    >   
    >  -   請勿在憑證範本內容的 [要求處理]  索引標籤上選取 [允許匯出私密金鑰]  核取方塊。  
    >   
    >  您不需要使用私密金鑰匯出此憑證，因為您可以瀏覽至本機電腦存放區，並在設定 System Center Configuration Manager 原則模組時選取。  

4.  找出用戶端驗證憑證所鏈結的根憑證。 然後將這個根 CA 憑證匯出至憑證 (.cer) 檔案。 請將這個檔案儲存到安全的位置，讓您稍後在安裝及設定憑證登錄點的網站系統伺服器時可安全地存取。  

5.  在相同伺服器上，使用登錄編輯程式並在 HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters 中設定下列登錄機碼 DWORD 值以增加 IIS 預設 URL 大小限制：  

    -   將 [MaxFieldLength]  設為 [65534] 。  

    -   將 [MaxRequestBytes]  設為 [16777216] 。  

     如需詳細資訊，請參閱Microsoft 知識庫中的文章 [820129：Windows 的 Http.sys 登錄設定](http://go.microsoft.com/fwlink/?LinkId=309013) 。  

6.  在相同伺服器的 Internet Information Services (IIS) 管理員中，修改 /certsrv/mscep 應用程式的要求篩選設定，然後重新啟動伺服器。 在 [編輯要求篩選設定]  對話方塊中，[要求限制]  設定應如下所示：  

    -   **允許的內容長度上限 (位元組)**： **30000000**  

    -   **URL 長度上限 (位元組)**： **65534**  

    -   **查詢字串上限 (位元組)**： **65534**  

     如需關於這些設定以及如何設定的詳細資訊，請參閱 IIS 參考庫中的 [Requests Limits (要求限制)](http://go.microsoft.com/fwlink/?LinkId=309014) 。  

7.  如果您希望您所要求的憑證有效期間低於目前使用的憑證範本：根據預設，企業 CA 的這項設定會停用。 若要在企業 CA 上啟用此選項，請使用 Certutil 命令列工具，然後使用下列命令停止後再重新啟動憑證服務：  

    1.  **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

    2.  **net stop certsvc**  

    3.  **net start certsvc**  

     如需詳細資訊，請參閱 TechNet 上 PKI 技術文件庫中的 [Certificate Services Tools and Settings (憑證服務工具和設定)](http://go.microsoft.com/fwlink/p/?LinkId=309015) 。  

8.  使用下列連結做為範例，確認網路裝置註冊服務正常運作： **https://server.contoso.com/certsrv/mscep/mscep.dll**。 您應該查看內建的網路裝置註冊服務網頁。 這個網頁提供服務的說明，並說明網路裝置會使用 URL 來提交憑證要求。  

 現在網路裝置註冊服務和相依性已設定完成，您可以準備安裝及設定憑證登錄點。


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>步驟 2 - 安裝及設定憑證登錄點。

您必須在 System Center Configuration Manager 階層安裝及設定至少一個憑證登錄點，而且您可以將這個站台系統角色安裝在管理中心網站或主要站台中。  

> [!IMPORTANT]  
>  在安裝憑證登錄點之前，請參閱 **站台系統需求** 主題中的 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) 一節，取得憑證登錄點的作業系統需求和相依性。  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>安裝及設定憑證登錄點  

1.  在 System Center Configuration Manager 主控台中，按一下 [系統管理]。  

2.  在 [系統管理]  工作區中，展開 [網站設定] ，按一下 [伺服器和網站系統角色] ，然後選取要用於憑證登錄點的伺服器。  

3.  在 [首頁]  索引標籤的 [伺服器]  群組中，按一下 [新增網站系統角色] 。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。  

5.  在 [Proxy]  頁面上，按 [下一步] 。 憑證登錄點不會使用網際網路 Proxy 設定。  

6.  在 [系統角色選取]  頁面上，在可用角色的清單中選取 [憑證登錄點]  ，然後按 [下一步] 。 

7. 在 [憑證登錄模式] 頁面上，選取您想要此憑證登錄點來 [處理 SCEP 憑證要求] 或 [處理 PFX 憑證要求]。 憑證登錄點無法同時處理這兩種要求，但如果您正在使用這兩種憑證類型，您可以建立多個憑證登錄點。

   如果是處理 PFX 憑證，您必須選擇憑證授權單位，即 Microsoft 或 Entrust。

8.  [憑證登錄點設定] 頁面會根據憑證類型而有所不同：
    -   如果您選取 [處理 SCEP 憑證要求]，請設定下列各項︰
        -   憑證登錄點的 [網站名稱]、[HTTPS 連接埠號碼] 和 [虛擬應用程式名稱]。 這些欄位會自動填入預設值。 
        -   **網路裝置註冊服務和根 CA 憑證的 URL** - 按一下 [新增]，接著在 [新增 URL 和根 CA 憑證] 對話方塊方塊中，指定下列各項︰
            - **網路裝置註冊服務的 URL**：指定的 URL 格式如下：https://<伺服器 FQDN>/certsrv/mscep/mscep.dll。 例如，如果執行網路裝置註冊服務的伺服器 FQDN 是 server1.contoso.com，請輸入 **https://server1.contoso.com/certsrv/mscep/mscep.dll**。
            - **根 CA 憑證**：瀏覽並選取您建立及儲存於 **步驟 1：安裝及設定網路裝置註冊服務和相依性**。 此根 CA 憑證允許憑證登錄點驗證 System Center Configuration Manager 原則模組所要使用的用戶端驗證憑證。  

    - 如果您選取 [處理 PFX 憑證要求]，則需設定所選憑證授權單位的連線詳細資訊和認證。

        - 若要使用 Microsoft 作為憑證授權單位，請按一下[新增]，然後在 [新增憑證授權單位與帳戶] 對話方塊中指定下列各項：
            - **憑證授權單位伺服器名稱** - 輸入您的憑證授權單位伺服器名稱。
            - **憑證授權單位帳戶** - 按一下 [設定]，以選取或建立有權限在憑證授權單位上範本中註冊的帳戶。
            - **憑證登錄點連線帳戶** - 選取或建立可將憑證登錄點連線至 Configuration Manager 資料庫的帳戶。 此外，您可以使用裝載憑證登錄點的電腦本機電腦帳戶。
            - **Active Directory 憑證發佈帳戶** - 選取帳戶或建立新的帳戶，用來將憑證發行至 Active Directory 中的使用者物件。

            - 在 [網路裝置註冊的 URL 和根 CA 憑證] 對話方塊中指定下列項目，然後按一下 [確定]：  

        - 若要使用 Entrust 作為憑證授權單位，請指定：

           - **MDM Web 服務 URL**
           - URL 的使用者名稱和密碼認證。

           使用 MDM API 定義 Entrust Web 服務 URL 時，務必使用至少版本 9 的 API，如下列範例所示：

           `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

           更早之前的 API 版本不支援 Entrust。

9. 按 [下一步]  ，並且完成精靈。  

10. 請等待數分鐘讓安裝完成，然後使用下列任何方式確認憑證登錄點已安裝成功：  

    -   在 [監視]  工作區中展開 [系統狀態] ，按一下 [元件狀態] ，然後在 [SMS_CERTIFICATE_REGISTRATION_POINT]  元件中尋找狀態訊息。  

    -   在站台系統伺服器上，使用 <Configuration Manager 安裝路徑\>\Logs\crpsetup.log 檔案和 Configuration Manager 安裝路徑\>*<*\Logs\crpmsi.log 檔案。 在安裝成功之後會傳回 0 的結束代碼。  

    -   使用瀏覽器，確認可連線至憑證登錄點的 URL，例如 https://server1.contoso.com/CMCertificateRegistration。 您應會看到 [伺服器錯誤]  頁面上的應用程式名稱，以及 HTTP 404 描述。  

11. 找出憑證登錄點在主要站台伺服器電腦之下列資料夾中自動建立的根 CA 匯出憑證檔案：<ConfigMgr 安裝路徑\>\inboxes\certmgr.box。 請將這個檔案儲存到安全的位置，讓您稍後在執行網路裝置註冊服務的伺服器上安裝 System Center Configuration Manager 原則模組時可安全地存取。  

    > [!TIP]  
    >  這個憑證不會立即出現在此資料夾中。 您可能需稍候片刻 (如半小時)，System Center Configuration Manager 才會將檔案複製到這個位置。  


## <a name="step-3----install-the-system-center-configuration-manager-policy-module-for-scep-certificates-only"></a>步驟 3 - 安裝 System Center Configuration Manager 原則模組 (僅適用於 SCEP 憑證)。

您必須在執行**步驟 2：安裝及設定憑證登錄點**時，在憑證登錄點的內容中指定為 [網路裝置註冊服務的 URL] 的每部伺服器上，安裝及設定 System Center Configuration Manager 原則模組。  

##### <a name="to-install-the-policy-module"></a>安裝原則模組  

1.  在執行網路裝置註冊服務的伺服器上，以網域系統管理員的身分登入，並將下列檔案從 System Center Configuration Manager 安裝媒體上的 <Configuration Manager 安裝媒體\>\SMSSETUP\POLICYMODULE\X64 資料夾複製到暫存資料夾：  

    -   PolicyModule.msi  

    -   PolicyModuleSetup.exe  

    此外，如果您的安裝媒體上含有 LanguagePack 資料夾，就可複製此資料夾與其中的內容。  

2.  從暫存資料夾執行 PolicyModuleSetup.exe 以啟動 [System Center Configuration Manager 原則模組安裝精靈]。  

3.  在精靈的初始頁面上，按 [下一步] 接受授權條款，然後按 [下一步] 。  

4.  在 [安裝資料夾]  頁面上，接受原則模組的預設安裝資料夾，或指定替代資料夾，然後按 [下一步] 。  

5.  在 [憑證登錄點]  頁面上，使用網站系統伺服器的 FQDN 以及在憑證登錄點的內容中指定的虛擬應用程式名稱，指定憑證登錄點的 URL。 預設的虛擬應用程式名稱是 CMCertificateRegistration。 例如，如果網站系統伺服器的 FQDN 是 server1.contoso.com，且您已使用預設虛擬應用程式名稱，請指定 **https://server1.contoso.com/CMCertificateRegistration**。  

6.  接受預設的連接埠 [443]  ，或指定憑證登錄點使用的替代連接埠號碼，然後按 [下一步] 。  

7.  在 [原則模組的用戶端憑證] 頁面，瀏覽至並指定您在下列步驟部署的用戶端驗證憑證： **步驟 1：安裝及設定網路裝置註冊服務和相依性**，然後按 [下一步] 。  

8.  在 [憑證註冊點憑證]  頁面上，按一下 [瀏覽]  ，以選取為根 CA 匯出的憑證檔，該憑證檔為您在 **步驟 2：安裝及設定憑證登錄點**結尾所找到且儲存的憑證檔。  

    > [!NOTE]  
    >  如果您尚未儲存此憑證檔案，該檔案會位於站台伺服器電腦上的 <Configuration Manager 安裝路徑\>\inboxes\certmgr.box 中。  

9. 按 [下一步]  ，並且完成精靈。  

 如果您要解除安裝 System Center Configuration Manager 原則模組，請使用控制台中的 [程式和功能]。 

 
設定步驟現已完成，您準備好可以建立和部署憑證設定檔，來將憑證部署至使用者和裝置。 如需如何建立憑證設定檔的詳細資訊，請參閱 [How to create certificate profiles in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md) (如何在 System Center Configuration Manager 中建立憑證設定檔)。  
