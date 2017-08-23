---
title: "維護 Mac 用戶端 | Microsoft Docs"
description: "Configuration Manager Mac 用戶端的維護工作。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3bf6651f58dc0c2aa4773f77115c3fbcd4a33221
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="maintain-mac-clients"></a>維護 Mac 用戶端
*適用於：System Center Configuration Manager (最新分支)*

以下是解除安裝 Mac 用戶端以及更新其憑證的程序。

##  <a name="uninstalling-the-mac-client"></a>解除安裝 Mac 用戶端  

1.  在 Mac 電腦上，開啟終端機視窗，並瀏覽至包含 **macclient.dmg** 的資料夾。  

2.  導覽至 Tools 資料夾並輸入下列命令列︰  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  **-c** 屬性指示用戶端在解除安裝作業的同時移除用戶端當機記錄和記錄檔。 此項建議是為了避免您將來重新安裝用戶端時發生混淆。  

3.  如有必要，您可以手動移除 Configuration Manager 所使用的用戶端驗證憑證，或者予以撤銷。 CMUnistall 不會移除或撤銷此憑證。  

##  <a name="renewing-the-mac-client-certificate"></a>更新 Mac 用戶端憑證  
 請使用下列其中一種方法更新 Mac 用戶端憑證：  

-   [更新憑證精靈](#renew-certificate-wizard)  

-   [手動更新憑證](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>更新憑證精靈  

1.  在 ccmclient.plist 檔案中將下列值設定為「字串」，控制 [更新憑證精靈] 開啟的時機：  

 -   **RenewalPeriod1** - 指定使用者可以更新憑證的第一個更新間隔 (以秒為單位)。 預設值為 3,888,000 秒 (45 天)。 不要設定小於 300 的值，因為期間會還原成預設值。 

 -   **RenewalPeriod2** - 指定使用者可以更新憑證的第二個更新間隔 (以秒為單位)。 預設值為 259,200 秒 (3 天)。 如果此值設定成大於或等於 300 秒且小於或等於 **RenewalPeriod1**，即會使用此值。 如果 **RenewalPeriod1** 大於 3 天， **RenewalPeriod2**就會使用 3 天的值。  如果 **RenewalPeriod1** 小於 3 天，則 **RenewalPeriod2** 會設為和 **RenewalPeriod1**相同的值。  

 -   **RenewalReminderInterval1** - 指定在第一個更新間隔期間向使用者顯示更新憑證精靈的頻率 (以秒為單位)。 預設值為 86,400 秒 (1 天)。 如果 **RenewalReminderInterval1** 大於 300 秒且小於 **RenewalPeriod1**設定的值，則會使用設定的值。 否則，將會使用預設值 1 天。  

 -   **RenewalReminderInterval2** - 指定在第二個更新間隔期間向使用者顯示更新憑證精靈的頻率 (以秒為單位)。 預設值為 28,800 秒 (8 小時)。 如果 **RenewalReminderInterval2** 大於 300 秒、小於或等於 **RenewalReminderInterval1** ，且小於或等於 **RenewalPeriod2**，則會使用設定的值。 否則會使用 8 小時的值。  

     **範例：** 如果值保留為其預設值，在憑證到期前的 45 天，精靈會每隔 24 小時開啟。  在憑證到期 3 天內，精靈會每隔 8 小時開啟。  

     **範例：** 使用下列命令列，或使用指令碼，將第一個更新間隔設定為 20 天。  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  當 [更新憑證精靈] 開啟時，[使用者名稱] 和 [伺服器名稱] 欄位通常已預先填入，因此使用者只要輸入密碼即可更新憑證。  

    > [!NOTE]  
    >  如果精靈沒有開啟，或是如果您意外關閉精靈，請從 [Configuration Manager]  喜好設定頁面按一下 [更新]  ，開啟精靈。  

###  <a name="renew-certificate-manually"></a>手動更新憑證  
 Mac 用戶端憑證的一般有效期為 1 年。 Configuration Manager 不會自動更新在註冊期間所要求的使用者憑證，因此您必須使用下列程序來手動更新憑證。  

> [!IMPORTANT]  
>  如果憑證到期，您必須解除安裝 Mac 用戶端，然後再重新安裝以及重新註冊。  

 此程序會移除在為同一台 Mac 電腦要求新憑證時需用到的 SMSID。 移除和取代用戶端 SMSID 時，在從 Configuration Manager 主控台刪除用戶端之後，任何已儲存的用戶端記錄 (例如清查) 都將刪除。  

1.  針對必須更新使用者憑證的 Mac 電腦建立並填入一個裝置集合。  

    > [!WARNING]  
    >  Configuration Manager 不會監視為 Mac 電腦所註冊的憑證有效期間。 您必須在 Configuration Manager 以外個別進行監視，找出要新增到此集合的 Mac 電腦。  

2.  在 [資產與相容性]  工作區內，開啟 [建立設定項目精靈] 。  

3.  在 [一般]  頁面上，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **類型：Mac OS X**  

4.  在 [支援的平台] 頁面上，確定已選取所有 Mac OS X 版本。  

5.  在 [設定] 頁面上，選擇 [新增]，然後在 [建立設定] 對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **設定類型︰指令碼**  

    -   **資料類型︰字串**  

6.  在 [建立設定] 對話方塊中，針對 [探索指令碼] 選擇 [新增指令碼] 以指定指令碼探索已設定 SMSID 的 Mac 電腦。  

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

12. 在精靈的 [相容性規則]  頁面上，按一下 [新增] ，然後在 [建立規則]  對話方塊中，指定下列資訊：  

    -   **名稱：移除 Mac 的 SMSID**  

    -   **選取的設定︰**選擇 [瀏覽]，然後選取您先前指定的探索指令碼。  

    -   在 **下列值** 的欄位中，輸入 **(com.microsoft.ccmclient SMSID) 的網域/預設值組不存在**。  

    -   啟用 [當此設定不相容時，執行指定的補救指令碼] 選項。  

13. 完成建立設定項目精靈。  

14. 建立包含您剛才建立之設定項目的設定基準，並且將此基準部署到您在步驟 1 建立的裝置集合。  

     如需如何建立並部署設定基準的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立設定基準](../../../compliance/deploy-use/create-configuration-baselines.md)與[如何在 System Center Configuration Manager 中部署設定基準](../../../compliance/deploy-use/deploy-configuration-baselines.md)。  

15. 對於已移除 SMSID 的 Mac 電腦，請執行下列命令來安裝新的憑證︰  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     收到提示時，請提供進階使用者帳戶的密碼以執行命令，然後再提供 Active Directory 使用者帳戶的密碼。  

16. 若要將註冊的憑證限制到 Configuration Manager，請在 Mac 電腦上開啟終端機視窗，並進行下列變更︰  

    a.  輸入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  在 [金鑰鏈存取] 對話方塊中的 [金鑰鏈] 區段，選擇 [系統] 後，再於 [類別] 區段選擇 [金鑰]。  

    c.  展開金鑰以檢視用戶端憑證。 若找到您剛安裝的憑證及其私密金鑰，請按兩下該金鑰。  

    d.  在 [存取控制] 索引標籤上，選擇 「Confirm before allowing access」 (允許存取前先確認)。  

    e.  瀏覽至 **/Library/Application Support/Microsoft/CCM**，選取 [CCMClient]，然後選擇 [新增]。  

    f.  選擇 [儲存變更] 並關閉 [金鑰鏈存取] 對話方塊。  

17. 重新啟動 Mac 電腦。  

