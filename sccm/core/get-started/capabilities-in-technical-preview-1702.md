---
title: "Technical Preview 1702 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1702 版中可用的功能。"
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bdbcd1a3c64a1d50f2f6219b2a5e17d60979864
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1702 中的功能

*適用於︰System Center Configuration Manager (Technical Preview)*

本文介紹 System Center Configuration Manager Technical Preview 1702 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>從 Configuration Manager 主控台傳送意見反應

此預覽版引進 Configuration Manager 主控台中的新意見反應選項。 [意見反應] 選項可讓您透過 Configuration Manager UserVoice 意見反應網站直接將意見反應傳送給開發小組。  

>您可以找到 [意見反應] 選項：
-  在功能區中，於每個節點的 [常用] 索引標籤的最左邊。  
   ![功能區](./media/feedback-home.png)

-  以滑鼠右鍵按一下主控台中的任何物件時。   
    ![按一下滑鼠右鍵選項](./media/feedback-option.png)   

選擇 [意見反應] 會將瀏覽器開啟到 Configuration Manager UserVoice 意見反應網站，網址為 https://configurationmanager.uservoice.com/forums/300492-ideas。
##  <a name="changes-for-updates-and-servicing"></a>更新與服務的變更
下列是這個預覽版引進的項目。

**更為簡單的更新選項**  
下次您的基礎結構可以進行兩個以上的更新時，只會下載最新的更新。 例如，如果您的目前站台版本是比可用的最新版本還要舊兩個以上版本的版本，則只會自動下載該最新更新版本。  

您可以選擇下載並安裝其他可用的更新，即使它們不是最新版本也是一樣。 不過，您會收到已將更新取代為較新更新的警告。 若要下載 [可供下載] 的更新，請選取主控台中的更新，然後按一下 [下載]。

**改善較舊更新的清理**   
我們已新增自動清理函式，可刪除站台伺服器的 'EasySetupPayload' 資料夾中不需要的下載。  


## <a name="peer-cache-improvements"></a>對等快取改善
從這個版本開始，對等快取來源電腦將會拒絕對等快取來源電腦符合下列任一條件時的內容要求︰  
 -  處於電力偏低模式。
 -  CPU 負載會在要求內容時超過 80%。
 -  磁碟 I/O 的 *AvgDiskQueueLength* 超過 10。
 -  無法再連線至電腦。   

當您使用 System Center Configuration Manager SDK 時，可以使用對等來源功能的用戶端代理程式設定類別來進行這些設定 (*SMS_WinPEPeerCacheConfig*)。

電腦拒絕內容要求時，提出要求的電腦會繼續於其在可用內容來源位置的集區中搜尋內容表單替代來源。   

## <a name="azurediscovery"></a> 使用 Azure Active Directory 網域服務管理裝置、使用者和群組

使用這個 Technical Preview 版本，您可以管理加入 Azure Active Directory (AD) 網域服務受管理網域裝置。 您也可以使用各種 Configuration Manager 探索方法來探索該網域中的裝置、使用者和群組。

Technical Preview 站台基礎結構、用戶端和 Azure AD 網域服務網域必須全部在 Azure 中執行。


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>設定 Configuration Manager 使用 Azure AD
若要搭配使用 Azure AD 與 Configuration Manager，您需要下列項目︰
-   Azure 訂用帳戶。
-   含網域服務 (DS) 的 Azure AD。
-   在加入 Azure AD 的 Azure VM 上執行的 Configuration Manager 站台。
-   在相同 Azure AD 環境中執行的 Configuration Manager 用戶端。

若要設定 Azure AD 網域服務，請參閱[開始使用 Azure AD 網域服務](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started)。

### <a name="discover-resources"></a>探索資源
設定 Configuration Manager 在 Azure AD 中執行之後，可以使用下列 Active Directory 探索方法在 Azure AD 中搜尋資源：  
- Active Directory 系統探索
- Active Directory 使用者探索
- Active Directory 群組探索  

針對您使用的每種方法，編輯 LDAP 查詢以搜尋 Azure AD OU 結構，而不是內部部署 Active Directory 的一般容器。 這需要您指示查詢來搜尋 Azure 訂用帳戶中的 Active Directory。  

下列範例會使用 *contoso.onmicrosoft.com* 的 Azure AD：
 - **系統探索**   
Azure AD 會將裝置儲存在 **AADDC Computers** OU 下方。  設定下列各項：  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **使用者探索** AAD 會將使用者儲存在 **AADDC Users** OU 下方。  設定下列各項：
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **群組探索**  
Azure AD 沒有可儲存群組的 OU。 相反地，使用與 [系統] 或 [使用者] 查詢相同的一般結構，並設定 LDAP 查詢以指向包含您要探索之群組的 OU。

如需 Azure AD 的詳細資訊，請參閱下列內容：  
 - azure.microsoft.com 上的 [Azure Active Directory 網域服務](https://azure.microsoft.com/en-us/services/active-directory-ds)。
 - docs.microsoft.com 上的 [Active Directory Domain Services 文件](https://docs.microsoft.com/azure/active-directory-domain-services)。

## <a name="conditional-access-device-compliance-policy-improvements"></a>條件式存取裝置合規性政策改善

使用者所使用的應用程式為不符合規範的應用程式清單一部分時，新的裝置合規性政策規則是可用來協助您封鎖存取可支援條件式存取的公司資源。 新增符合規範規則 [無法安裝的應用程式] 時，系統管理員可以定義不符合規範的應用程式清單。 將應用程式新增至不符合規範的清單時，此規則需要系統管理員輸入 [應用程式名稱]、[應用程式識別碼] 和 [應用程式發行者]\ (選擇性)。 這項設定僅適用於 iOS 和 Android 裝置。

此外，這可協助組織透過不安全的應用程式來降低資料外洩，並透過特定應用程式來避免過多的資料使用。

- 深入了解[裝置合規性政策運作方式](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies)。
- 深入了解[建立和部署裝置合規性政策](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy)。

### <a name="try-it-out"></a>試試看

**案例︰**識別在公司外部傳送公司資料可能會造成資料外洩的應用程式，或造成資料使用過多的應用程式，然後[建立和部署裝置合規性政策](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy)，以將這些應用程式新增至不符合規範的應用程式清單。 在使用者可以移除封鎖的應用程式之前，這會封鎖存取支援條件式存取的公司資源。

## <a name="antimalware-client-version-alert"></a>反惡意程式碼用戶端版本警示
從這個預覽版開始，如果超過 20% (預設) 的受管理用戶端使用反惡意程式碼用戶端過期版本 (即 Windows Defender 或 Endpoint Protection 用戶端)，則 Configuration Manager Endpoint Protection 會發出警示。

### <a name="try-it-out"></a>試試看
請使用用戶端設定原則確定已在所有桌上型電腦和伺服器用戶端上啟用 Endpoint Protection。 您現在可以檢視 [反惡意程式碼用戶端版本] 和 [Endpoint Protection 部署狀態]，方法是移至 [資產與合規性] > [概觀] > [裝置] > [所有桌面及伺服器用戶端]。 若要檢查警示，請檢視 [監視] 工作區中的 [警示]。 如果超過 20% 的受管理用戶端執行反惡意程式碼軟體過期版本，則會顯示「反惡意程式碼用戶端版本已過期」警示。 此警示不會出現在 [監視] > [概觀] 索引標籤上。 若要更新過期的反惡意程式碼用戶端，請啟用反惡意程式碼用戶端的軟體更新。

若要設定產生警示的百分比，請展開 [監視] > [警示] > [所有警示]，然後按兩下 [反惡意程式碼用戶端已過期]，並修改 [如果具有反惡意程式碼用戶端過期版本的受管理用戶端百分比超過下列數值，則產生警示] 選項。

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Windows Update for Business 更新的合規性評估
您現在可以設定合規性政策更新規則，在條件式存取評估時加入 Windows Update for Business 評估結果。
> [!IMPORTANT]
> 您必須具有 Windows 10 Insider Preview Build 15019 或更新版本，才能使用 Windows Update for Business 更新的合規性評估。

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>允許 Windows Update for Business 管理 Windows 10 更新
若要收集 Windows Update for Business 更新的合規性評估資訊，請使用下列程序設定用戶端代理程式設定以明確允許 Windows Update for Business 管理 Windows 10 更新。
1. 在 Configuration Manager 主控台中，移至 **[系統管理]** > **[用戶端設定]**。
2. 在用戶端設定的內容中，移至 [軟體更新]，然後將 [使用 Windows Update for Business 管理 Windows 10 更新] 設定選取為 [是]。

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>建立 Windows Update for Business 評估的合規性政策
1. 在 Configuration Manager 主控台中，移至 [資產與合規性] > [合規性設定] > [合規性原則]。
2. 按一下 [建立合規性政策]，或選取要修改的現有合規性政策。
3. 在 [一般] 頁面上，提供名稱和描述，並選取 [使用 Configuration Manager 用戶端管理之裝置的合規性規則]，然後設定報告的非合規性嚴重性並按一下 [下一步]。
4. 在 [支援的平台] 頁面上，選取 [Windows 10]，然後按一下 [下一步]。
5. 在 [規則] 頁面上，按一下 [新增...]，然後針對 [條件] 選擇 [Require Windows Update for Business compliance]\(需要 Windows Update for Business 合規性)。 [值] 設定會自動設為 [True]。

新的原則會顯示在 [資產與相容性]  工作區的 [相容性原則]  節點中。

### <a name="deploy-a-compliance-policy"></a>部署相容性原則
1. 在 Configuration Manager 主控台中，移至 [資產與合規性] > [合規性設定]，然後按一下 [合規性政策]。
2. 在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。
3. 在 [部署相容性原則]  對話方塊中，按一下 [瀏覽]  選取要部署原則的使用者集合。
   此外，您可以選取選項以在原則不相容時產生警示，同時設定評估這項原則是否相符所依據的排程。
4. 完成之後，請按一下 [確定] 。

### <a name="monitor-the-compliance-policy"></a>監視相容性原則
建立合規性政策之後，可以在 Configuration Manager 主控台中監視合規性結果。 如需詳細資訊，請參閱[監視合規性政策](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)。


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>具有強烈影響之工作順序的軟體中心設定和通知訊息的改善
這個版本包括具有強烈影響之部署工作順序的軟體中心設定和通知訊息的下列改善：

- 在工作順序的內容中，您現在可以將任何工作順序 (包括非作業系統工作順序) 設定為高風險部署。 任何符合特定條件的工作順序都會自動定義為具有強烈影響。 如需詳細資料，請參閱[管理高風險部署](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments)。
- 在工作順序的內容中，您可以選擇使用預設通知訊息，或建立您自己的自訂通知訊息來進行具有強烈影響的部署。
- 在工作順序的內容中，您可以設定軟體中心內容，包括進行必要的重新啟動、工作順序的下載大小，以及估計的執行階段。
- 就地升級之預設具有強烈影響的部署訊息現在指出會自動移轉您的應用程式、資料和設定。 先前，任何作業系統安裝的預設訊息指出將會遺失所有應用程式、資料和設定，但這不適用於就地升級。

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>將工作順序設定為具有強烈影響的工作順序
使用下列程序將工作順序設定為具有強烈影響。
> [!NOTE]
> 任何符合特定條件的工作順序都會自動定義為具有強烈影響。 如需詳細資料，請參閱[管理高風險部署](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments)。

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫] > [作業系統] > [工作順序]。
2. 選取要編輯的工作順序，然後按一下 [內容]。
3. 在 [使用者通知] 索引標籤上，選取 [這是具有強烈影響的工作順序]。

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>建立高風險部署的自訂通知
1. 在 Configuration Manager 主控台中，移至 [軟體程式庫] > [作業系統] > [工作順序]。
2. 選取要編輯的工作順序，然後按一下 [內容]。
3. 在 [使用者通知] 索引標籤上，選取 [使用自訂文字]。
>  [!NOTE]
>  選取 [這是具有強烈影響的工作順序] 時，您只能設定使用者通知文字。

4. 設定下列設定 (每個文字方塊最多 255 個字元)：

   **使用者通知標題文字**：指定在軟體中心使用者通知上顯示的藍色文字。 例如，在預設使用者通知中，本節包含與下列類似的訊息：「請確認是否要升級這部電腦的作業系統」。

   **使用者通知訊息文字**：有三個文字方塊提供自訂通知的內文。
   - 第 1 個文字方塊︰指定本文，通常包含使用者指示。 例如，在預設使用者通知中，本節包含與下列類似的訊息：「升級作業系統需要一些時間，而且您的電腦可能會重新啟動數次。」
   - 第 2 個文字方塊︰指定本文下的粗體文字。 例如，在預設使用者通知中，本節包含與下列類似的訊息：「這項就地升級會安裝新的作業系統，並自動移轉您的應用程式、資料和設定。」
   - 第 3 個文字方塊︰指定粗體文字下的最後一行文字。 例如，在預設使用者通知中，本節包含與下列類似的訊息：「按一下 [安裝] 開始安裝。 否則，請按一下 [取消]。」   

   假設您在內容中設定下列自訂通知。

   ![工作順序的自訂通知](.\media\user-notification.png)

   使用者從軟體中心開啟安裝時，將會顯示下列通知訊息。

   ![工作順序的自訂通知](.\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>設定軟體中心內容
使用下列程序設定軟體中心中所顯示工作順序的詳細資料。 這些詳細資料僅供參考。  
1. 在 Configuration Manager 主控台中，移至 [軟體程式庫] > [作業系統] > [工作順序]。
2. 選取要編輯的工作順序，然後按一下 [內容]。
3. 在 [一般] 索引標籤上，可以使用下列軟體中心設定︰
  - **需要重新啟動**：讓使用者知道在安裝期間是否需要重新啟動。
  - **下載大小 (MB)**︰指定軟體中心中針對工作順序顯示的 MB 數。  
  - **估計執行時間 (分鐘)**：指定軟體中心中針對工作順序顯示的估計執行時間 (分鐘)。


## <a name="check-for-running-executable-files-before-installing-an-application"></a>在安裝應用程式之前檢查執行中可執行檔

在部署類型的 *<deployment type name>* [內容] 對話方塊中，於 [安裝行為] 索引標籤上，您現在可以指定多個可執行檔中的其中一個，而其執行時，將會封鎖部署類型的安裝。 使用者必須先關閉執行中可執行檔 (或者會針對必要部署而自動予以關閉)，才能安裝部署類型。

### <a name="try-it-out"></a>請試試看。

1.  在 Configuration Manager 部署類型的內容中，選擇 [安裝行為] 索引標籤。
2.  選擇 [新增] 以新增您想要檢查的一或多個可執行檔名稱。 您也可以新增顯示名稱，讓使用者可以輕鬆地找出清單中的應用程式。
3.  如果部署是必要的，則可以在部署軟體精靈中選擇性選擇 [自動關閉您在部署類型屬性對話方塊之 [安裝行為] 索引標籤上所指定且正在執行的可執行檔]。

如果應用程式已部署為 [可用]，而且使用者嘗試安裝應用程式，則會提示他們在繼續安裝之前關閉任何您指定的執行中可執行檔。

如果應用程式已部署為 [必要]，並且選取 [自動關閉您在部署類型屬性對話方塊之 [安裝行為] 索引標籤上所指定且正在執行的可執行檔] 選項，則他們會看到一個對話方塊，通知他們在到達應用程式安裝期限時會自動關閉您指定的可執行檔。 您可以在 [用戶端設定] > [電腦代理程式] 中排定這些對話方塊。 如果您不想讓使用者看到這些訊息，請在部署內容的 [使用者體驗] 索引標籤上選取 [在軟體中心和所有通知中隱藏]。

如果應用程式已部署為 [必要]，但未選取 [自動關閉您在部署類型屬性對話方塊之 [安裝行為] 索引標籤上所指定且正在執行的可執行檔] 選項，則在一或多個指定的應用程式正在執行時，應用程式的安裝會失敗。

## <a name="create-pfx-certificates-with-s-mime-support"></a>使用 S MIME 支援來建立 PFX 憑證

您現在可以建立支援 S/MIME 的 PFX 憑證設定檔，並將它部署至使用者。  此憑證接著可供使用者已註冊的裝置用於 S/MIME 加密和解密。

此外，您現在可以在多個憑證登錄點站台系統角色上指定多個憑證授權單位 (CA)，然後指派哪些 CA 處理要求以作為憑證設定檔的一部分。

針對 iOS 裝置，您可以建立 PFX 憑證設定檔與電子郵件設定檔的關聯，並啟用 S/MIME 加密。  這接著會在 iOS 的原生電子郵件用戶端中啟用 S/MIME，並建立正確 S/MIME 加密憑證與它的關聯。

如需 Configuration Manager 中憑證的詳細資訊，請參閱[簡介 System Center Configuration Manager 中的憑證設定檔]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles)。


## <a name="new-compliance-settings-for-ios-devices"></a>iOS 裝置的新合規性設定

我們已新增設定，可供您針對 iOS 裝置在設定項目中使用。 這些是先前存在於 Microsoft Intune 獨立設定中的設定，現在當您搭配使用 Intune 和 Configuration Manager 時可以使用這些設定。 如果您需要上述任何設定的協助，請參閱 [Microsoft Intune 的 iOS 原則設定](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune)。

- **將資料從受管理應用程式同步到 iCloud**
- **遞交以繼續在其他裝置執行活動**
- **iCloud 照片共享**
- **iCloud 相片圖庫**
- **信任新的企業應用程式作者**
- **允許使用者從 iBook Store 下載標示為 [成人作品] 的內容** (僅限受監督模式)
- **強制已配對的 Apple Watch 使用手腕偵測**
- **AirPlay 連出要求的密碼**
- **修改帳戶設定** (僅限受監督模式)
- **變更應用程式行動數據使用量設定** (僅限受監督模式)
- **清除所有內容及設定** (僅限受監督模式)
- **設定裝置的限制** (僅限受監督模式)
- **使用主機配對來控制 iOS 裝置可配對的裝置** (僅限受監督模式)
- **安裝組態設定檔和憑證** (僅限受監督模式)
- **修改裝置名稱** (僅限受監督模式)
- **修改密碼** (僅限受監督模式)
- **Apple Watch 配對** (僅限受監督模式)
- **修改通知設定** (僅限受監督模式)
- **修改背景圖片** (僅限受監督模式)
- **修改診斷提交設定** (僅限受監督模式)
- **修改藍牙** (僅限受監督模式)
- **AirDrop** (僅限受監督模式)
- **使用 Siri 從網際網路查詢使用者產生的內容** (僅限受監督模式)
- **Siri 不雅內容篩選** (僅限受監督模式)
- **在 Spotlight 搜尋中從網際網路傳回結果** (僅限受監督模式)
- **字組定義查閱** (僅限受監督模式)
- **預測鍵盤** (僅限受監督模式)
- **自動校正** (僅限受監督模式)
- **鍵盤拼字檢查** (僅限受監督模式)
- **鍵盤快速鍵** (僅限受監督模式)
<!--- - **Enterprise app trust settings modification** --->
- **只用 Apple Configurator 及 iTunes 安裝應用程式** (僅限受監督模式)
- **自動應用程式下載** (僅限受監督模式)
- **變更 [尋找我的朋友] 應用程式設定** (僅限受監督模式)
- **存取 iBooks Store** (僅限受監督模式)
- **「訊息」應用程式** (僅限受監督模式)
- **Podcasts** (僅限受監督模式)
- **Apple Music** (僅限受監督模式)
- **iTunes Radio** (僅限受監督模式)
- **Apple News** (僅限受監督模式)
- **Game Center** (僅限受監督模式)
- **將 AirDrop 視為未受管理的目的地**

## <a name="android-for-work-support"></a>Android for Work 支援

從 Technical Preview 1702 版開始，您可以將 Google 帳戶繫結至混合式 MDM 租用戶。 這可讓您執行下列動作：

- 將[支援的 Android 裝置](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)註冊為 Android for Work，方法是在這些已註冊的裝置上建立工作設定檔
- 核准 Play for Work 市集中的應用程式，並將它們與 Configuration Manager 主控台同步，然後將它們部署至裝置的工作設定檔
- 建立和部署設定項目來設定這些裝置的工作設定檔和密碼設定
- 針對 Android for Work 裝置建立和部署合規性政策項目和資源存取設定檔，就像已對 Android 裝置執行的一樣
- 在 Android for Work 裝置上執行選擇性抹除

當您將裝置註冊為 Android for Work 時，會在 Intune 可管理的裝置上建立工作設定檔。 在 Android 裝置上，此工作設定檔與個人設定檔並存。 使用者可以輕鬆地切換工作設定檔應用程式與個人設定檔應用程式。 您無法管理個人設定檔中的項目。 個人應用程式和資料會保持不變。 Configuration Manager 可以完整控制工作設定檔和其內容，而且可以從裝置中予以移除。

Android for Work 是與 Android 不同的平台，而且您需要決定哪種形式的管理用於支援工作設定檔的 Android 裝置。

### <a name="try-it-out"></a>試試看！
下列各節描述 Android for Work 管理。

#### <a name="enable-android-for-work-management"></a>啟用 Android for Work 管理
1. 在 https://accounts.google.com/SignUp 建立 Google 帳戶，以用作將與這個 Intune 租用戶的所有 Android for Work 管理工作建立關聯的 Android for Work 系統管理員帳戶。 這可能是管理 Android 裝置的系統管理員所共用的 Google 帳戶。 這是您的組織在 Play for Work 主控台中管理及發行應用程式所使用的 Google 帳戶。 您將使用此帳戶來核准 Play for Work 市集中的應用程式，因此請記下帳戶名稱和密碼。
2. 將 Google 帳戶繫結至 Configuration Manager 中所管理的 Intune 租用戶，以啟用 Android 註冊：
  1. 移至 [系統管理] > [概觀] > [雲端服務] > [Microsoft Intune 訂閱]，然後選取 Intune 訂閱。
  2. 在功能區中，按一下 [設定平台] > [Android]，並確定已核取 [啟用 Android 註冊]。
  3. 在功能區中，按一下 [設定平台] > [Android for Work]。
  4. 在對話方塊中，按一下 [在 Intune 主控台中設定 Android for Work]。 Intune 主控台會在網頁瀏覽器中開啟。
  5. 使用 Intune 系統管理員認證來登入 Intune 入口網站。
  6. 按一下 [設定] 以開啟 Google Play 的 Android for Work 網站。
  7. 在 Google 的登入頁面上，輸入步驟 1 中的 Google 帳戶認證，然後提供您的公司資訊。
3. 當您返回 Intune 入口網站時，Android for Work 已啟用，並且會有三個 Android for Work 裝置註冊選項︰
  - **將所有裝置作為 Android 管理** - (已停用) 所有 Android 裝置 (包括支援 Android for Work 的裝置) 將會註冊為傳統 Android 裝置。
  - **將受支援的裝置作為 Android for Work 管理** - (已啟用) 所有支援 Android for Work 的裝置都會註冊為 Android for Work 裝置。 不支援 Android for Work 的任何 Android 裝置都會註冊為傳統 Android 裝置。
  - **將這些群組中僅限使用者的受支援裝置作為 Android for Work 管理** - (測試中) 可讓您將 Android for Work 管理的目標設為有限的一組使用者。 只有註冊支援 Android for Work 之裝置的所選群組成員，才能註冊為 Android for Work 裝置。 所有其他成員則會註冊為 Android 裝置。
  
> [!NOTE]
> 一項已知的問題會造成 [將這些群組中僅限使用者的受支援裝置作為 Android for Work 管理] **Android** 選項無法正常運作。 指定的 Azure AD 群組中的使用者裝置將註冊為 Android，而不是 Android for Work。 若要測試 Android for Work，您必須使用 [Manage all supported devices as Android for Work]\(將所有支援的裝置作為 Android for Work 管理)。


  若要啟用 Android for Work 註冊，您必須選擇下面兩個選項中的其中一個。 [將這些群組中僅限使用者的受支援裝置作為 Android for Work 管理] 選項需要您先設定 Azure Active Directory 安全性群組。

繫結完成時，您會在 Intune 入口網站中看到帳戶名稱和組織名稱；此時，您可以關閉這兩個瀏覽器。

#### <a name="approve-and-deploy-android-for-work-apps"></a>核准和部署 Android for Work 應用程式
遵循下列步驟來核准 Play for Work 市集中的應用程式，並將它們與 Configuration Manager 主控台同步，然後將它們部署至受管理 Android for Work 裝置。 若要將應用程式部署至使用者的工作設定檔，您需要核准 Play for Work 市集中的應用程式，然後將應用程式與 Configuration Manager 主控台同步。

1. 開啟瀏覽器並前往︰https://play.google.com/work。
2. 使用您已繫結至 Intune 租用戶的 Google 系統管理員帳戶登入。
3. 瀏覽您要在環境中部署的應用程式，然後針對它們都按一下 [核准]。
4. 在 Configuration Manager 主控台中，移至 [系統管理員] > [概觀] > [雲端服務] > [Android for Work]，然後按一下 [同步]。
5. 等待 10 分鐘來同步處理應用程式，然後移至 [軟體程式庫] > [概觀] > [應用程式管理] > [市集應用程式的授權資訊]。
6. 按一下從 Play for Work 同步處理的應用程式，然後按一下 [建立應用程式]。
7. 完成精靈，然後按一下 [關閉]。
8. 移至 [軟體程式庫] > [概觀] > [應用程式管理] > [應用程式]，並選取 Android for Work 應用程式，然後如常進行部署。

若要將 Play for Work 應用程式與 Configuration Manager 同步，您必須至少核准 Play for Work 網站上的一個應用程式。

#### <a name="enroll-an-android-for-work-device"></a>註冊 Android for Work 裝置
Android for Work 裝置的註冊方式與 Android 類似。 在行動裝置上下載並執行 Android 的公司入口網站應用程式。 系統會提示您在註冊程序期間建立工作設定檔。  建立工作設定檔之後，您必須切換至受管理公司入口網站版本。 受管理公司入口網站會在右下角標上小型橘色公事包。

#### <a name="create-and-deploy-a-configuration-item"></a>建立和部署設定項目
Android for Work 有兩個設定項目設定群組︰
- 密碼
- 工作設定檔

您可以設定工作設定檔之間的內容共用，以及在執行 Android 6 或更高版本的裝置上設定下列設定項目︰
- 要求特定權限的應用程式的行為
- 在鎖定畫面上是否可以看到工作設定檔內應用程式的通知

若要嘗試這麼做，請透過標準工作流程建立設定項目，並選擇 [一般] 頁面上的 [Android for Work]，然後設定每個設定群組的設定，方法是將設定項目新增至基準，並如常部署。 這些設定只適用於註冊為 Android for Work 的裝置，而不適用於註冊為 Android 的裝置。

#### <a name="perform-selective-wipe"></a>執行選擇性抹除
因為您只可管理工作設定檔，所以只能選擇性地抹除註冊為 Android for Work 的裝置。 這可防止抹除個人設定檔。 在 Android for Work 裝置上執行選擇性抹除會移除工作設定檔 (包括所有應用程式和資料)，並解除註冊裝置。

若要選擇性地抹除 Android for Work 裝置，請使用 Configuration Manager 主控台中的一般[選擇性抹除](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)程序。

#### <a name="known-issues-for-android-for-work"></a>Android for Work 的已知問題
[Configuring sync schedule in Android for Work email profiles causes them to fail to deploy]\(在 Android for Work 電子郵件設定檔中設定同步處理排程，會導致它們無法部署) Android for Work 電子郵件設定檔之 ConfigMgr UI 中的其中一個選項為「排程」。 在其他平台上，這可讓系統管理員設定排程，以將電子郵件和其他電子郵件帳戶資料同步處理到部署的目標行動裝置上。 不過，它不適用於 Android for Work 電子郵件設定檔，而且選擇「未設定」以外的任何選項，則會導致該設定檔無法部署至任何裝置。
