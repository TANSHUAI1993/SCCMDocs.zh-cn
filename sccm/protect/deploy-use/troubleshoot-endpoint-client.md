---
title: "Windows Defender 或 Endpoint Protection 用戶端疑難排解 | Microsoft Docs"
description: "了解如何為 Windows Defender 和 Endpoint Protection 問題進行疑難排解。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1b096e71f5131214fb4e235e84d0b7f63e566831
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Windows Defender 或 Endpoint Protection 用戶端疑難排解

*適用於：System Center Configuration Manager (最新分支)*


如果您發生 Windows Defender 或 Endpoint Protection 問題，請連絡安全性系統管理員以取得支援。 您也可以嘗試疑難排解下列問題：  

-   [更新 Windows Defender 或 Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [啟動 Windows Defender 或 Endpoint Protection 服務](#starting-windows-defender-or-endpoint-protection-service)  
-   [網際網路連線問題](#internet-connection-issues)  
-   [偵測到無法修復的威脅](#detected-threat-cant-be-remediated)  
-   [安裝 Endpoint Protection 用戶端](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>更新 Windows Defender 或 Endpoint Protection  
 Windows Defender 或 Endpoint Protection 會自動與 Microsoft Update 一起運作，確保病毒和間諜軟體定義處於最新狀態。  

 **徵兆**  

 本文解決自動更新的常見問題，包括下列情況：  

-   您看到錯誤訊息，指出更新已失敗。  

-   當您檢查更新時，會收到錯誤訊息，指出無法檢查、下載或安裝病毒和間諜軟體定義更新。  

-   即使您已連線到網際網路，更新還是失敗。  

-   未依排程自動安裝更新。  

 **原因**  

 更新問題的最常見原因是網際網路連線問題。 不過，如果您因可瀏覽至其他網站而知道已連線到網際網路，則問題可能是與 Windows Internet Explorer 的設定衝突所造成。  

> [!IMPORTANT]  
>  您必須結束 Internet Explorer，才能完成這些步驟。 因此，請列印它們、寫下它們，或將它們複製到另一個檔案，然後將這個主題加入書籤以供未來存取。  

### <a name="step-1-reset-your-internet-explorer-settings"></a>步驟 1：重設 Internet Explorer 設定  

1.  結束所有開啟的程式 (包括 Internet Explorer)。  

    > [!NOTE]  
    >  重設 Internet Explorer 中的這些設定會刪除暫存檔、Cookie、瀏覽歷程記錄和線上密碼。 但是，不會刪除我的最愛。  

2.  按一下 [開始]  ，並搜尋 **inetcpl.cpl**，然後按 **Enter**。  

3.  在 [網際網路選項]  對話方塊中，按一下 [進階]  索引標籤。  

4.  在 [重設 Internet Explorer 設定] 下，按一下 [重設] ，然後按一下 [重設]  。  

5.  等到 Internet Explorer 完成重設設定，然後按一下 [確定] 。  

6.  開啟 Internet Explorer。  

7.  開啟 Microsoft Security Essentials，並按一下 [更新]  索引標籤，然後按一下 [更新] 。  

8.  如果問題持續發生，請繼續進行下一個步驟。  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>步驟 2：設定 Internet Explorer 作為預設瀏覽器  

1.  結束所有開啟的程式 (包括 Internet Explorer)。  

2.  按一下 [開始]  ，並搜尋 **inetcpl.cpl**，然後按 **Enter**。  

3.  在 [網際網路選項]  對話方塊中，按一下 [程式]  索引標籤。  

4.  在 [預設網頁瀏覽器] 下，按一下 [設成預設值] 。  

5.  按一下 [ **確定**]。  

6.  開啟 Windows Defender 或 Endpoint Protection。 按一下 [更新]  索引標籤，然後按一下 [更新] 。  

7.  如果問題持續發生，請繼續進行下一個步驟。  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>步驟 3：確定電腦上已正確設定日期和時間  

1.  開啟 Windows Defender 或 Endpoint Protection。  

2.  如果您收到的錯誤訊息包含 0x80072f8f 代碼，此問題最可能是電腦上的日期或時間設定不正確所造成。  

3.  若要重設您電腦的日期或時間設定，請遵循 [修正損毀的桌面捷徑和一般系統維護工作](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579) 中的步驟進行。  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>步驟 4：重新命名您電腦上的 [軟體發佈] 資料夾  

1. 停止自動更新服務  

    1.  按一下 [開始]  ，並搜尋 **services.msc**，然後按一下 [確定] 。  

    2.  在 [自動更新服務] 上按一下滑鼠右鍵，然後按一下 [停止] 。  

    3.  最小化 [服務] 嵌入式管理單元。  

2.  重新命名 **SoftwareDistribution** 目錄，如下所示：  

    1.  按一下 [開始]  ，並搜尋  **cmd**，然後按一下 [確定] 。  

    2.  輸入 **cd %windir%**，然後按 **Enter**。  

    3.  輸入 **ren SoftwareDistribution SDTemp**，然後按 **Enter**。  

    4.  輸入 **exit**，然後按 **Enter**。  

3.  啟動自動更新服務，如下所示：  

    1.  最大化 [服務] 嵌入式管理單元。  

    2.  在 [自動更新服務] 上按一下滑鼠右鍵，然後按一下 [啟動] 。  

    3.  關閉 [服務] 嵌入式管理單元視窗。  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>步驟 5：重設電腦上的 Microsoft 防毒更新引擎  

1.  按一下 [開始]  ，並搜尋  **cmd**，然後按一下 [確定] ，再於 [命令提示字元] 上按一下滑鼠右鍵，然後選取 [以系統管理員身分執行] 。  

2.  在 [命令提示字元]  視窗中，輸入下列命令，並在每個命令之後按 **Enter** ：  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Exit**  

3.  重新啟動電腦。  

4.  開啟 Windows Defender 或  
          Endpoint Protection，並按一下 [更新] 索引標籤，然後按一下 [更新]。  

5.  如果問題持續發生，請繼續進行下一個步驟。  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>步驟 6：手動安裝病毒和間諜軟體定義更新  

-   如果您是執行 32 位元 Windows 作業系統，請在 [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342) 手動下載最新更新。  

-   如果您是執行 64 位元 Windows 作業系統，請在 [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341) 手動下載最新更新。  

-   按一下 [執行] 。 在您的電腦上手動安裝最新更新。  


### <a name="step-7-contact-support"></a>步驟 7：連絡支援服務  

-   如果這些步驟無法解決問題，請連絡支援服務。 如需詳細資訊，請參閱 [客戶支援](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174)。  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>啟動 Windows Defender 或 Endpoint Protection 服務  
 **徵兆**  

 您收到訊息通知，表示「Windows Defender 或 Endpoint Protection 並未監控電腦，因為程式的服務已停止。**您應該立即重新啟動該服務。」** 

 **解決方案**  

### <a name="step-1-restart-your-computer"></a>步驟 1：重新啟動電腦。  

-   關閉所有應用程式，然後重新啟動電腦。  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>步驟 2：確定「Windows Defender」或「Endpoint Protection 服務」已設定為 [自動] 並已啟動  

1.  按一下 [開始]  ，並搜尋 **services.msc**，然後按 **Enter**。  

2.  搜尋「 **Microsoft 反惡意程式碼服務**」。 用滑鼠右鍵按一下該服務，然後選取 [內容]  ，或是按兩下以開啟該服務。  

3.  檢查確定「**啟動類型**」已設定為「**自動**」。  

4.  按一下 [啟動]  按鈕以啟動服務。 如果 [啟動]  按鈕無法使用，請按一下 [停止]  按鈕，然後按一下 [開始]  按鈕重新啟動服務。  

5.  確定您記下任何可能在此程序中出現的錯誤，線上提交案例，並包含錯誤資訊。  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>步驟 3：移除所有現有的網際網路安全性程式  

1.  按一下 [開始]  ，並搜尋 **appwiz.cpl**，然後按 **Enter**。  

2.  在已安裝程式的清單中，解除安裝所有協力廠商的網際網路安全性程式。*  

3.  重新啟動電腦，然後試著再次安裝 Windows Defender 或  
          Endpoint Protection。  

> [!NOTE]  
>  某些網際網路安全性應用程式不會完全解除安裝。 您可能需要下載並執行先前的安全性應用程式的清理公用程式，才能完全移除該應用程式。  

> [!CAUTION]  
>  當您移除網際網路安全性程式時，您的電腦是未受保護的。 如果您在移除現有網際網路安全性程式之後安裝   
>       Endpoint Protection 時發生問題，請線上提交案例來連絡 Windows Defender 或  
>       Endpoint Protection 支援 (如需詳細資訊，請參閱[如何線上提交案例](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx))。  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>步驟 4：解除安裝/重新安裝 Endpoint Protection  

1.  按一下 [開始]  ，並搜尋 **appwiz.cpl**，然後按 **Enter**。  

2.  在已安裝程式的清單中，按一下 [Endpoint Protection] ，然後將它解除安裝。  

3.  系統提示時，請重新啟動電腦，然後試著再次安裝 Endpoint Protection。  

##  <a name="internet-connection-issues"></a>網際網路連線問題  
 為了確保您的電腦從 Windows Update 收到最新的更新，您必須連線到網際網路。  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>步驟 1：驗證電腦連線到網際網路  

1.  按一下 [開始] ，並搜尋 **ncpa.cpl**，然後按 **Enter**。  

2.  在連線名稱上按一下滑鼠右鍵，然後按一下 [狀態] 。  

3.  如果您的電腦已連線，在 Windows XP 中，連線狀態會顯示為 [已連線] 、[已啟用] 或 [驗證成功]  。 在 Windows Vista 和 Windows 7 中，[IPv4]  狀態會顯示為 [網際網路] 。  

4.  如果您的電腦似乎未連線，請在連線名稱上按一下滑鼠右鍵，然後按一下 [連線] 、[啟用] 、[驗證] 或 [修復] 。  

### <a name="step-3-restart-your-computer"></a>步驟 3：重新啟動電腦  

-   關閉所有開啟的程式，然後重新啟動電腦。  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>步驟 4：如果您仍然無法連線到網際網路，請檢查您的連線  

1.  如果您使用撥號連線，請確定電話線連接到牆上插座，並已穩固地連接數據機。  

2.  如果您使用纜線數據機，請確定纜線連接到數據機，並已穩固地連接數據機與您電腦的連線。  

3.  如果您使用纜線數據機或 DSL 路由器，請確定已穩固地連接路由器和電腦的連線。 請嘗試拔除並關閉路由器和數據機。 請等候數分鐘，並先插上數據機，再等待一分鐘，然後插上路由器，並重新啟動電腦。  

##  <a name="detected-threat-cant-be-remediated"></a>偵測到無法修復的威脅  
 Windows Defender 或  
      Endpoint Protection 偵測到隱藏在副檔名為 .zip 的壓縮檔或網路共用中的潛在威脅時，會嘗試以隔離或移除威脅的方式來處理威脅。  

### <a name="remove-or-scan-the-file"></a>移除或掃描檔案  

-   如果偵測到的威脅是在 .zip 檔案中，請瀏覽到 .zip 檔案，然後移除該檔案，或是用滑鼠右鍵按一下該檔案並選取 [以 Windows Defender 掃描]  或 [以 Endpoint Protection 掃描] 來掃描該檔案。 如果 Windows Defender 或 Endpoint Protection 偵測到檔案中有其他威脅，則會發出有關這些威脅的通知，讓您可以選擇適當的動作。  

-   如果偵測到的威脅是在網路共用中，請瀏覽到網路共用，然後用滑鼠右鍵按一下該檔案並選取 [以 Windows Defender 掃描]  或 [以 Endpoint Protection 掃描] 來掃描該檔案。 如果 Windows Defender 或 Endpoint Protection 偵測到網路共用中有其他威脅，則會發出有關這些威脅的通知，讓您可以選擇適當的動作。  

-   如果您不確定檔案的來源，最好的解決方案之一就是在電腦上執行完整掃描。 完整掃描可能要花一些時間才能完成，不過它讓 Windows Defender 或 Endpoint Protection 有可能找出感染的來源並加以清理。  

##  <a name="install-the-endpoint-protection-client"></a>安裝 Endpoint Protection 用戶端  

> [!NOTE]  
>  在 Windows 10 電腦上，Windows Defender 是與作業系統一起安裝。  

 **徵兆**  

 不明原因造成安裝失敗，或您收到有錯誤碼的錯誤訊息，例如 0x80070643、0X8007064A、0x8004FF2E、0x8004FF01、0x8004FF07、0x80070002、0x8007064C、0x8004FF00、0x80070001、0x80070656、0x8004FF40、0xC0000156、0x8004FF41、0x8004FF0B、0x8004FF11、0x80240022、0x8004FF04、0x80070660、0x800106B5、0x80070715、0x80070005、0x8004EE00、0x8007003、0x800B0100、0x8007064E 或 0x8007007E。  

 如果電腦是執行 Windows XP Service Pack 2 (SP2)，您可能會看到下列一個或多個錯誤訊息：  

-   安裝精靈遺失完成安裝所需的篩選器管理員彙總套件。  

-   KB914882 安裝錯誤，安裝程式無法更新您的 Windows XP 檔案，因為您系統上安裝的語言和更新語言不同。  

 **原因**  

 Endpoint Protection 無法安裝在正執行其他安全性程式的電腦上。 有時即使您移除其他的安全性程式，也無法完全解除安裝。 您必須執行正版的 Windows 作業系統，才能安裝 Endpoint Protection。  

 **解決方案**  

> [!IMPORTANT]  
>  在解決這個問題時，您會需要重新啟動電腦。 將此頁設為書籤 (標示為「我的最愛」)，讓您較容易再次找到本主題，或列印下來以便參考。  

### <a name="step-1-remove-any-existing-security-programs"></a>步驟 1：移除所有現有的安全性程式  
**僅限 Endpoint Protection**

1.  完整解除安裝所有現有的網際網路安全性程式。  

2.  重新啟動電腦。  

3.  重新安裝 Endpoint Protection。 如果仍然無法解決問題，請繼續下一步。  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>步驟 2：確定 Windows Installer 服務正在執行  

1.  按一下 [開始]  ，並搜尋 **services.msc**，然後按 **Enter**。  

2.  用滑鼠右鍵按一下 [ **Windows Installer**]，然後按一下 [ **開始**]。 如果 [啟動]  無法使用，但 [停止]  和 [重新啟動]  選項可以使用，表示服務已經啟動。  

3.  在「 **服務** 」頁面上的 [ **檔案** ] 功能表中，按一下 [ **結束**]。  

4.  按一下 [開始]，然後搜尋**命令提示字元**。 用滑鼠右鍵按一下 [命令提示字元] ，然後按一下 [以系統管理員身分執行] 。  

5.  輸入 **MSIEXEC /REGSERVER**，然後按 **Enter**。  

    > [!NOTE]  
    >  沒有此命令是否完成或失敗的指示。  

6.  重新安裝 Endpoint Protection。 如果仍然無法解決問題，請繼續下一步。  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>步驟 3：在「選擇式啟動」模式中啟動  

1.  按一下 [開始]  ，並搜尋 **msconfig**，然後按 **Enter**。  

2.  在 [ **一般** ] 索引標籤上按一下 [ **選擇啟動項目**]，然後取消選取 [ **載入啟動項目** ] 核取方塊。  

3.  在 [服務]  索引標籤上，選取 [隱藏所有 Microsoft 服務]  核取方塊，然後取消選取所有還在清單中的服務的核取方塊。  

4.  按一下 [ **確定**]，然後按一下 [ **重新啟動** ] 以重新啟動電腦。  

5.  嘗試重新安裝 Endpoint Protection。  



### <a name="see-also"></a>請參閱  
 [Endpoint Protection 用戶端常見問題集](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Endpoint Protection 用戶端說明](../../protect/deploy-use/endpoint-protection-client-help.md)
