---
title: "部署 Mac 用戶端 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中將用戶端部署至 Mac 電腦。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6ce212c6745b70a47553891e5dbc124b4c4e50fa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

適用於：System Center Configuration Manager (最新分支)

本主題描述如何在 Mac 電腦上部署和維護 Configuration Manager 用戶端。 若要了解您必須先進行何種設定，再將用戶端部署到 Mac 電腦，請參閱[準備將用戶端軟體部署到 Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)。

為 Mac 電腦安裝新的用戶端時，您可能必須同時安裝 Configuration Manager 更新，以反映 Configuration Manager 主控台中的新用戶端資訊。

在這些程序中，您有兩個選項可以安裝用戶端憑證。 在[準備將用戶端軟體部署到 Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements) 中，深入了解 Mac 的用戶端憑證。  

-   利用 [CMEnroll 工具](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac)使用 Configuration Manager 註冊。 註冊程序不支援自動憑證更新，所以您必須在安裝的憑證到期前，先重新註冊 Mac 電腦。    

-   [使用與 Configuration Manager 無關的憑證要求和安裝方法](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager)。 

>[!IMPORTANT]
>  若要將用戶端部署到執行 macOS Sierra 的裝置上，必須正確設定管理點憑證的「主體名稱」，例如，使用管理點伺服器的 FQDN。


## <a name="configure-client-settings-for-enrollment"></a>設定註冊時使用的用戶端設定  
 您必須使用[預設用戶端設定](../../../core/clients/deploy/about-client-settings.md)來設定 Mac 電腦的註冊；您無法使用自訂用戶端設定。  

 Configuration Manager 需要它才能在 Mac 上要求及安裝憑證。  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>為 Configuration Manager 設定預設用戶端設定，以註冊 Mac 的憑證  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] >  [用戶端設定] > [預設用戶端設定]。  

4.  在 [首頁] 索引標籤的 [內容] 群組中，選擇 [內容]。  

5.  選取 [註冊] 區段，然後設定這些設定：  

    1.  **允許使用者註冊行動裝置和 Mac 電腦：是**  

    2.  **註冊設定檔：**選擇 [設定設定檔]。  

6.  在 [行動裝置註冊設定檔] 對話方塊中，選擇 [建立]。  

7.  在 [建立註冊設定檔]  對話方塊中，輸入此註冊設定檔的名稱，然後設定 [管理網站碼] 。 選取包含要管理 Mac 電腦之管理點的 Configuration Manager 主要站台。  

    > [!NOTE]  
    >  如果您無法選取網站，請確認網站內至少有一個管理點已設定為支援行動裝置。  

8.  選擇 [新增]。  

9. 在 [新增行動裝置的憑證授權單位] 對話方塊中，選取負責發行憑證給 Mac 電腦的憑證授權單位 (CA) 伺服器。  

10. 於 [建立註冊設定檔] 對話方塊中，選取您於步驟 3 所建立的 Mac 電腦憑證範本。  

11. 按一下 [確定] 關閉 [註冊設定檔] 對話方塊，接著按一下 [預設用戶端設定] 對話方塊。  

    > [!TIP]  
    >  若要變更用戶端原則間隔，請使用 [用戶端原則] 用戶端設定群組中的 [用戶端原則輪詢間隔]。  

 下一次使用者下載用戶端原則時，所有使用者都會以這些設定進行設定。 若要起始單一用戶端的原則擷取，請參閱[起始 Configuration Manager 用戶端的原則抓取](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

 除了註冊用戶端設定之外，也請確保您已設定下列用戶端裝置設定︰  

-   **硬體清查**：啟用並設定此內容，以從 Mac 和 Windows 用戶端電腦收集硬體清查。 如需詳細資訊，請參閱[如何擴充 System Center Configuration Manager 中的硬體清查](../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

-   **合規性設定**：啟用並設定此內容，以於 Mac 和 Windows 用戶端電腦上評估和補救設定。 如需詳細資訊，請參閱[規劃和設定相容性設定](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

> [!NOTE]  
>  如需 Configuration Manager 用戶端設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md)。  

## <a name="download-the-client-source-files-for-macs"></a>下載 Mac 的用戶端來源檔案  

1.  下載 Mac OS X 用戶端檔案套件 **ConfigmgrMacClient.msi**，並將它儲存到執行 Windows 的電腦中。  

     Configuration Manager 安裝媒體並未提供這個檔案。 您可以從 [Microsoft Download Center (Microsoft 下載中心)](http://go.microsoft.com/fwlink/?LinkID=525184)下載此檔案。  

2.  在 Windows 電腦上，執行 **ConfigmgrMacClient.msi**，將 Mac 用戶端套件 Macclient.dmg 解壓縮至本機磁碟的資料夾中 (預設為 **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**)。  

3.  將 Macclient.dmg 檔案複製到 Mac 電腦上的資料夾。  

4.  在 Mac 電腦上執行 Macclient.dmg 檔案，將檔案解壓縮至本機磁碟機的資料夾。  

5.  於該資料夾中，確保檔案 Ccmsetup 和 CMClient.pkg 已解壓縮，並且已建立命名為 Tools 的資料夾，其中包含 CMDiagnostics、CMUninstall、CMAppUtil 和 CMEnroll 工具。

    -  **Ccmsetup**：在您的 Mac 電腦上安裝 Configuration Manager 用戶端。  

    -   **CMDiagnostics**：在您的 Mac 電腦上收集與 Configuration Manager 用戶端相關的診斷資訊。  

    -   **CMUninstall**：從 Mac 電腦解除安裝用戶端。  

    -   **CMAppUtil**：將 Apple 應用程式套件轉換為可部署為 Configuration Manager 應用程式的格式。  

    -   **CMEnroll**：要求並安裝 Mac 電腦的用戶端憑證，才能安裝 Configuration Manager 用戶端。   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>在 Mac 上安裝用戶端，然後註冊用戶端憑證  

您可以使用 [Mac 電腦註冊精靈](#enroll-the-client-with-the-mac-computer-enrollment-wizard)註冊個別用戶端。

如需啟用多個用戶端註冊的自動化，請使用 [CMEnroll 工具](#client-and-certificate-automation-with-cmenroll)。   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>使用 [Mac 電腦註冊精靈] 註冊用戶端  

1.  在完成安裝用戶端後，[電腦註冊精靈] 便會開啟。 如果未開啟精靈，或是您意外關閉精靈，請按一下 [Configuration Manager] 喜好設定頁面中的 [註冊]，來開啟精靈。  

2.  在精靈的第二個頁面上，提供︰  

    -   **使用者名稱** - 可用的使用者名稱格式如下︰  

        -   '網域\名稱'。 例如：'contoso\mnorth'  

        -   'user@domain'。 例如：'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  當您使用電子郵件地址填入 [使用者名稱] 欄位時， Configuration Manager 會自動使用電子郵件地址的網域名稱和註冊 Proxy 點伺服器的預設名稱來填入 [伺服器名稱] 欄位。 如果此網域名稱和伺服器名稱不符合註冊 Proxy 點伺服器名稱，請將正確名稱告知使用者，使用者才能在註冊其 Mac 電腦時使用此名稱。  

         使用者名稱和對應密碼必須符合 Active Directory 使用者帳戶，並具有 Mac 用戶端憑證範本的讀取和註冊權限。  

    -   **密碼** - 輸入與指定的使用者名稱相對應的密碼。  

    -   **伺服器名稱** - 輸入註冊 Proxy 點伺服器的名稱。  


### <a name="client-and-certificate-automation-with-cmenroll"></a>使用 CMEnroll 的用戶端和憑證自動化  

使用此程序來自動化用戶端安裝，以及使用 CMEnroll 工具來要求和註冊用戶端憑證。 若要執行此工具，您必須擁有 Active Directory 使用者帳戶。

1.  在 Mac 電腦上，瀏覽至 Macclient.dmg 檔案內容解壓縮所在的資料夾。  

2.  請輸入下列命令列︰ **sudo ./ccmsetup**  

3.  請等候直至您看見 [已完成安裝]  訊息。 雖然安裝程式會顯示必須立即重新啟動的訊息，但請不要重新啟動並繼續下一個步驟。  

4.  從 Mac 電腦上的 [工具] 資料夾中輸入下列命令：**sudo ./CMEnroll -s &lt;註冊 Proxy 伺服器名稱> -ignorecertchainvalidation -u &lt;使用者名稱'>**  

    用戶端安裝之後，Mac [電腦註冊精靈] 便會開啟以協助您註冊 Mac 電腦。 若要使用此方法註冊用戶端，請參閱本主題的 [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) 。  

5. 輸入 Active Directory 使用者帳戶的密碼。  當您輸入此命令時，會要求您出示兩個密碼：第一個提示是針對執行命令的進階使用者帳戶。 第二個提示是針對 Active Directory 使用者帳戶。 提示外觀看似相同，所以請確認是否以正確順序輸入密碼。  

    使用者名稱的格式可以如下︰  

    -   '網域\名稱'。 例如：'contoso\mnorth'  

    -   'user@domain'。 例如：'mnorth@contoso.com'  

     使用者名稱和對應密碼必須符合 Active Directory 使用者帳戶，並具有 Mac 用戶端憑證範本的讀取和註冊權限。  

     範例：若註冊 Proxy 點伺服器命名為 **server02.contoso.com**，且 **contoso\mnorth** 的使用者名稱已獲授與 Mac 用戶端憑證範本的權限，請輸入如下︰**sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  如果使用者名稱包含任何 **&lt;>"+=** 字元，註冊將會失敗。 請使用不包含這些字元的使用者名稱來取得頻外憑證。  
    >  
    >  若要讓使用者能體驗更順暢的使用經驗，您可以編寫安裝步驟和命令列，讓使用者只需要輸入使用者名稱和密碼。  

5.  請等候直至您看見 [已順利註冊]  訊息。  

6.  若要將註冊的憑證限制到 Configuration Manager，請在 Mac 電腦上開啟終端機視窗，並進行下列變更︰  

    a.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  在 [金鑰鏈存取] 對話方塊中的 [金鑰鏈] 區段，選擇 [系統] 後，再於 [類別] 區段選擇 [金鑰]。  

    c.  展開金鑰以檢視用戶端憑證。 若找到您剛安裝的憑證及其私密金鑰，請按兩下該金鑰。  

    d.  在 [存取控制] 索引標籤上，選擇 「Confirm before allowing access」 (允許存取前先確認)。  

    e.  瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient]，然後選擇 [新增]。  

    f.  選擇 [儲存變更] 並關閉 [金鑰鏈存取] 對話方塊。  

7.  重新啟動 Mac 電腦。  

 於 Mac 電腦 [系統偏好設定]  開啟 Configuration Manager  項目，驗證用戶端安裝是否已順利完成。 您也可更新和檢視 [所有系統]  集合，確認此集合中已顯示該 Mac 電腦為受管理用戶端。  

> [!TIP]  
>  若要協助針對 Mac 用戶端進行疑難排解，您可以使用 Mac OS X 用戶端套件隨附的 CMDiagnostics 程式來收集下列診斷資訊︰  
>   
>  -   執行中處理程序清單  
> -   Mac OS X 作業系統版本  
> -   與 Configuration Manager 用戶端相關的 Mac OS X 當機報告 (其中包含 **CCM\*.crash** 和 **System Preference.crash**)。  
> -   由 Configuration Manager 用戶端安裝所建立的用料表 (BOM) 檔案和內容清單 (.plist) 檔案。  
> -   資料夾 /Library/Application Support/Microsoft/CCM/Logs 的內容。  
>   
>  CmDiagnostics 收集的資訊會新增至 ZIP 檔案，該檔案儲存於電腦桌面上，名稱為 cmdiag-*<主機名稱\>***-***&gt;日期與時間\>*.zip。***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>使用與 Configuration Manager 獨立的憑證要求和安裝方法  

首先，從[準備將用戶端軟體部署到 Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients) 執行這些特定工作：

1. [將 Web 伺服器憑證部署至站台系統伺服器](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [將用戶端驗證憑證部署至站台系統伺服器](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [設定管理點和發佈點](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [選用：安裝 Reporting Services 點](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

然後，執行下列工作︰

5. [下載 Mac 的用戶端來源檔案](#download-the-client-source-files-for-macs)。  
6. 請使用您所選憑證部署方法隨附的指示，來要求並安裝 Mac 電腦上的用戶端憑證。  
7.  導覽至您由 Microsoft Download Center 下載後並解壓縮的 macclient.dmg 檔案內容資料夾位置。  

3.  輸入下列命令列：**sudo ./ccmsetup -MP <管理點網際網路 FQDN\> -SubjectName <憑證主體值\>**。  憑證主體值區分大小寫，請依憑證詳細資料中所顯示正確輸入。  

     範例：若站台系統內容中的網際網路 FQDN 為 **server03.contoso.com**，而 Mac 用戶端憑證使用 FQDN **mac12.contoso.com** 作為憑證主體的一般名稱，請輸入︰**sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  請等候直至您看見 [已完成安裝]  訊息，再重新啟動 Mac 電腦。  

5.  若要確保此憑證可供 Configuration Manager 存取，請在 Mac 電腦上開啟終端機視窗，並進行這些變更︰  

    a.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  在 [金鑰鏈存取] 對話方塊中的 [金鑰鏈] 區段，選擇 [系統] 後，再於 [類別] 區段選擇 [金鑰]。  

    c.  展開金鑰以檢視用戶端憑證。 若找到您剛安裝的憑證及其私密金鑰，請按兩下該金鑰。  

    d.  在 [存取控制] 索引標籤上，選擇 「Confirm before allowing access」 (允許存取前先確認)。  

    e.  瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient]，然後選擇 [新增]。  

    f.  選擇 [儲存變更] 並關閉 [金鑰鏈存取] 對話方塊。  

6.  如果您有多個憑證含有相同的主體值，您必須指定憑證序號以識別您要用於 Configuration Manager 用戶端的憑證。 若要這樣做，請使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序號\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 於 Mac 的 [系統偏好設定] 開啟 [Configuration Manager] 項目，驗證用戶端安裝是否已順利完成。 您也可更新和檢視 [所有系統] 集合，確認此集合中已顯示該 Mac 為受管理用戶端。  

## <a name="renewing-the-mac-client-certificate"></a>更新 Mac 用戶端憑證  
 更新 Mac 電腦上的電腦憑證之前，請使用下列程序︰  

 此程序會移除用戶端在 Mac 電腦上使用新憑證或更新的憑證時需用到的 SMSID。  

> [!IMPORTANT]  
>  移除和取代用戶端 SMSID 時，在從 Configuration Manager 主控台刪除用戶端之後，任何已儲存的用戶端記錄 (例如清查) 都將刪除。  

### <a name="to-renew-the-mac-client-certificate"></a>更新 Mac 用戶端憑證  

1.  針對必須更新電腦憑證的 Mac 電腦建立並填入一個裝置集合。  

2.  在 [資產與相容性]  工作區內，開啟 [建立設定項目精靈] 。  

3.  在精靈的 [一般]  頁面上，指定下列資訊︰  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **類型：Mac OS X**  

4.  在精靈的 [支援的平台]  頁面上，確定已選取所有 Mac OS X 版本。  

5.  在精靈的 [設定]  頁面上，按一下 [新增]  ，然後在 [建立設定]  對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **設定類型︰指令碼**  

    -   **資料類型︰字串**  

6.  在 [建立設定]  對話方塊的 [探索指令碼] 中，按一下 [新增指令碼]  以指定指令碼探索已設定 SMSID 的 Mac 電腦。  

7.  在 [編輯探索指令碼]  對話方塊中，輸入下列殼層指令碼：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  選擇 [確定] 以關閉 [編輯探索指令碼] 對話方塊。  

9. 在 [建立設定] 對話方塊中，針對 [補救指令碼 (選用)] 選擇 [新增指令碼] 以指定指令碼在 Mac 電腦上找到 SMSID 時將其移除。  

10. 在 [建立補救指令碼]  對話方塊中，輸入下列殼層指令碼：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 選擇 [確定] 以關閉 [建立補救指令碼] 對話方塊。  

12. 在精靈的 [合規性規則] 頁面上，選擇 [新增]，然後在 [建立規則] 對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **選取的設定︰**選擇 [瀏覽]，然後選取您先前指定的探索指令碼。  

    -   在 **下列值** 的欄位中，輸入 **(com.microsoft.ccmclient SMSID) 的網域/預設值組不存在**。  

    -   啟用 [當此設定不相容時，執行指定的補救指令碼] 選項。  

13. 完成建立設定項目精靈。  

14. 建立包含您剛才建立之設定項目的設定基準，並且將此基準部署到您在步驟 1 建立的裝置集合。  

     如需如何建立和部署設定基準的詳細資訊，請參閱[如何在 System Center Configuration Manager 建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)。  

15. 在已移除 SMSID 的 Mac 電腦上安裝新憑證後，執行下列指令以設定用戶端使用新憑證：  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. 如果您有多個憑證含有相同的主體值，則必須指定憑證序號以識別您要用於 Configuration Manager 用戶端的憑證。 若要這樣做，請使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序號\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. 重新啟動。  


## <a name="see-also"></a>請參閱

[維護 Mac 用戶端](/sccm/core/clients/manage/maintain-mac-clients)
