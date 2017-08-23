---
title: "管理 Office 365 ProPlus 更新 | Microsoft Docs"
description: "Configuration Manager 會將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器，讓更新能夠部署至用戶端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 902d7f7216ca7bb585afae587a6706e2332da9d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus

適用於：System Center Configuration Manager (最新分支)

Configuration Manager 可讓您使用下列方式來管理 Office 365 專業增強版應用程式：

- [Office 365 用戶端管理儀表板](#office-365-client-management-dashboard)：從 Configuration Manager 1610 版開始，便可以在 Office 365 用戶端管理儀表板中檢閱 Office 365 用戶端資訊。    

- [部署 Office 365 應用程式](#deploy-office-365-apps)：從 1702 版開始，便可以從 Office 365 用戶端管理儀表板來啟動 Office 365 安裝程式，讓初始的 Office 365 應用程式安裝體驗更為簡易。 此精靈可讓您設定 Office 365 安裝設定，從 Office 內容傳遞網路 (CDN) 下載檔案，然後利用該內容來建立並部署指令碼應用程式。    

- [部署 Office 365 更新](#deploy-office-365-updates)：從 Configuration Manager 1602 版開始，便能使用軟體更新管理工作流程來管理 Office 365 用戶端更新。 當 Microsoft 將新的 Office 365 用戶端更新發佈至 Office 內容傳遞網路 (CDN) 時，Microsoft 也會將更新套件發佈至 Windows Server Update Services (WSUS)。 當 Configuration Manager 將 Office 365 用戶端更新從 WSUS 類別目錄同步處理至站台伺服器之後，更新就可以部署至用戶端。    

- [新增 Office 365 更新下載的語言](#add-languages-for-office-365-update-downloads)：從 Configuration Manager 1610 版開始，便可為 Configuration Manager 新增支援，以下載 Office 365 所支援任一語言的更新，而不論在 Configuration Manager 中是否支援這些語言。  

- [變更更新頻道](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager)：您可以使用群組原則，將登錄機碼值變更發佈至 Office 365 用戶端，以變更更新頻道。


## <a name="office-365-client-management-dashboard"></a>Office 365 用戶端管理儀表板  
Office 365 用戶端管理儀表板提供下列資訊的圖表：

- Office 365 用戶端數目
- Office 365 用戶端版本
- Office 365 用戶端語言
- Office 365 用戶端通道     
  如需詳細資訊，請參閱 [Office 365 ProPlus 更新通道的概觀](https://technet.microsoft.com/library/mt455210.aspx)。

若要在 Configuration Manager 主控台中檢視 Office 365 用戶端管理儀表板，請移至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。 使用儀表板頂端的 [集合] 下拉式清單設定，依特定集合成員篩選儀表板資料。

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>在 Office 365 用戶端管理儀表板中顯示資料
[Office 365 用戶端管理] 儀表板中所顯示的資料來自硬體清查。 您必須先啟用硬體清查，並選取 [Office 365 專業增強版設定] 硬體清查類別，資料才會顯示在儀表板中。
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>在 Office 365 用戶端管理儀表板中顯示資料
1. 啟用硬體清查 (若尚未啟用)。 如需詳細資料，請參閱[設定硬體清查](\sccm\core\clients\manage\configure-hardware-inventory)。
2. 在 Configuration Manager 主控台中，瀏覽至 [系統管理] > [用戶端設定] > [預設用戶端設定]。  
3. 在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  
4. 在 **預設用戶端設定**  對話方塊中按一下 **硬體清查**。  
5. 在 **裝置設定** 清單中，按一下 **設定類別**。  
6. 在 [硬體清查類別] 對話方塊中，選取 [Office 365 ProPlus Configurations]\(Office 365 ProPlus 設定)。  
7.  按一下 **確定** 以儲存您的變更並關閉 **硬體清查類別** 對話方塊。  
Office 365 用戶端管理儀表板將在報告硬體清查時開始顯示資料。

## <a name="deploy-office-365-apps"></a>部署 Office 365 應用程式  
從 1702 版開始，在 Office 365 用戶端管理儀表板中啟動 Office 365 安裝程式，便可進行初始的 Office 365 應用程式安裝。 此精靈可讓您設定 Office 365 安裝設定，從 Office 內容傳遞網路 (CDN) 下載檔案，然後針對檔案來建立並部署指令碼應用程式。 除非在用戶端上安裝 Office 365，否則無法使用 Office 365 更新。

針對先前的 Configuration Manager 版本，在用戶端上首次安裝 Office 365 應用程式時，必須採取下列步驟：
- 下載 Office 365 部署工具 (ODT)
- 下載 Office 365 安裝來源檔案，包括所有需要的語言套件。
- 產生指定正確 Office 版本與頻道的 Configuration.xml。
- 建立和部署舊版套件或指令碼應用程式，以供用戶端安裝 Office 365 應用程式。

### <a name="requirements"></a>需求
- 執行 Office 365 安裝程式的電腦必須能夠存取網際網路。  
- 執行 Office 365 安裝程式的使用者必須具有精靈中所提供內容位置共用的「讀取」和「寫入」權限。
- 如果您收到 404 下載錯誤，請將下列檔案複製到使用者的 %temp% 資料夾︰
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  


### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>從 Office 365 用戶端管理儀表板將 Office 365 應用程式部署至用戶端
1. 在 Configuration Manager 主控台中，巡覽至 [軟體程式庫] > [概觀] > [Office 365 用戶端管理]。
2. 按一下右上方窗格中的 [Office 365 Installer]。 [Office 365 用戶端安裝精靈] 隨即開啟。
3. 在 [應用程式設定] 頁面上，提供應用程式的名稱和描述，輸入檔案的下載位置，然後按一下 [下一步]。 請使用 &#92;&#92;*server*&#92;*share* 格式來指定位置。
4. 在 [匯入用戶端設定] 頁面上，選擇要從現有的 XML 組態檔匯入 Office 365 用戶端設定，還是要手動指定設定，然後按一下 [下一步]。  

    如果您有現成的組態檔，請輸入檔案的位置，然後跳至步驟 7。 請注意，您必須使用 &#92;&#92;*server*&#92;*share*&#92;*檔案名稱*.XML 格式來指定位置。
    > [!IMPORTANT]    
    > XML 設定檔中只可包含 [Office 365 ProPlus 用戶端所支援的語言](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx)。

5. 在 [Client Products]\(用戶端產品) 頁面上，依序選取您使用的 Office 365 套件、要包含的應用程式、應包含的任何其他 Office 產品，然後按一下 [下一步]。
6. 在 [用戶端設定] 頁面上，選擇要包含的設定，然後按一下 [下一步]。
7. 在 [部署] 頁面上，選擇是否要部署應用程式，然後按一下 [下一步]。  
如果您選擇不要在精靈中部署套件，請跳至步驟 9。
8. 設定精靈頁面的其餘部分，就像是一般應用程式部署一樣。 如需詳細資訊，請參閱[建立和部署應用程式](/sccm/apps/get-started/create-and-deploy-an-application)。
9. 完成精靈。
10. 從 [軟體程式庫] > [概觀] > [應用程式管理] > [應用程式]，可部署或編輯應用程式。    

在您使用 Office 365 安裝程式建立和部署 Office 365 應用程式之後，Configuration Manager 預設並不會管理 Office 更新。 若要讓 Office 365 用戶端收到來自 Configuration Manager 的更新，請參閱[使用 Configuration Manager 部署 Office 365 更新](#deploy-office-365-updates-with-configuration-manager)。

>[!NOTE]
>部署 Office 365 應用程式之後，您可以建立自動部署規則，以維護應用程式。 若要建立適用於 Office 365 應用程式的自動部署規則，請從 Office 365 用戶端管理儀表板按一下 [建立 ADR]，然後在您選擇產品時，選取 [Office 365 用戶端]。 如需詳細資訊，請參閱[自動部署軟體更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。


## <a name="deploy-office-365-updates"></a>部署 Office 365 更新
使用下列步驟以 Configuration Manager 部署 Office 365 更新：

1.  [確認需求](https://technet.microsoft.com/library/mt628083.aspx)：請見主題的＜使用 Configuration Manager 管理 Office 365 用戶端更新的需求＞一節中有關使用 Configuration Manager 管理 Office 365 用戶端更新的需求。  

2.  [設定軟體更新點](../get-started/configure-classifications-and-products.md)，以同步處理 Office 365 用戶端更新。 設定分類的 [更新]，然後針對產品選取 [Office 365 用戶端]。 設定軟體更新點使用 [更新] 分類之後，必須同步處理軟體更新。
3.  啟用 Office 365 用戶端從 Configuration Manager 接收更新。 您可以使用 Configuration Manager 用戶端設定或群組原則來執行這項操作。 使用下列方法之一啟用用戶端：   

    **方法 1**︰從 Configuration Manager 1606 版開始，便可以使用 Configuration Manager 用戶端設定來管理 Office 365 用戶端代理程式。 在設定這項設定並部署 Office 365 更新之後，Configuration Manager 用戶端代理程式會與 Office 365 用戶端代理程式進行通訊，從發佈點下載 Office 365 更新並安裝它們。 Configuration Manager 採用 Office 365 ProPlus 用戶端的清查設定。    

      1.  在 Configuration Manager 主控台中，按一下 [管理] > [概觀] > [用戶端設定]。  

      2.  開啟適當的裝置設定，以啟用用戶端代理程式。 如需預設和自訂用戶端設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

      3.  按一下 [軟體更新]，然後針對 [啟用管理 Office 365 用戶端代理程式] 設定選取 [是]。  

    **方法 2**：使用 Office 部署工具或群組原則，[啟用 Office 365 用戶端以從 Configuration Manager 接收更新](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient)。  

4. [部署 Office 365 更新](deploy-software-updates.md)至用戶端。   

> [!Important]
> 您下載及部署的更新，其語言必須與 Office 365 用戶端的語言相同。 例如，假設您的 Office 365 用戶端設定了 en-us 和 de-de 語言。 在站台伺服器上，您只為適用的 Office 365 更新下載和部署 en-us 內容。 當使用者從軟體中心開始安裝此更新時，更新將會在下載內容時停止回應。   

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Office 365 更新的重新啟動行為與用戶端通知
當您將更新部署到 Office 365 用戶端時，重新啟動行為與用戶端通知會根據您所擁有的 Configuration Manager 版本而有所不同。 下表提供用戶端接收到 Office 365 更新時之使用者體驗的相關資訊：

|Configuration Manager 版本 |使用者經驗|  
|----------------|---------------------|
|1610 之前|系統會設定重新啟動旗標，並在電腦重新啟動之後安裝更新。|
|1610|在安裝更新之前，系統會在不發出警告之下關閉 Office 365 應用程式|
|1610 (含更新) <br/>1702|系統會設定重新啟動旗標，並在電腦重新啟動之後安裝更新。|
|1706|在安裝更新之前，用戶端會接收到快顯和應用程式內通知，以及倒數計時對話方塊。|


## <a name="add-languages-for-office-365-update-downloads"></a>新增 Office 365 更新下載的語言
從 Configuration Manager 1610 版開始，便可為 Configuration Manager 新增支援，以下載 Office 365 所支援任一語言的更新，而不論在 Configuration Manager 中是否支援這些語言。    

> [!IMPORTANT]  
> 設定其他 Office 365 更新語言是全站台設定。 使用下列程序新增語言之後，將會下載這些語言的所有 Office 365 更新，以及您在 [下載軟體更新] 或 [部署軟體更新精靈] 中 [語言選擇] 頁面內所選取的語言。

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>新增支援以下載其他語言的更新
請在管理中心網站或獨立主要站台中的軟體更新點，使用下列程序。
1. 從命令提示字元處，以系統管理使用者身分輸入 *wbemtest*，開啟 Windows Management Instrumentation 測試器。
2. 按一下 [連線]，然後輸入 *root\sms\site_<&lt;siteCode&gt;*。
3. 按一下 [查詢]，然後執行下列查詢︰*select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![WMI 查詢](..\media\1-wmiquery.png)
4. 在 [結果] 窗格中，於具有管理中心網站或獨立主要站台的站台碼之物件上按兩下。
5. 選取 [內容] 屬性，按一下 [編輯內容]，然後按一下 [檢視內嵌項]。
![內容編輯器](..\media\2-propeditor.png)
6. 從第一個查詢結果開始，開啟每個物件，直到找到 **PropertyName**屬性為 **AdditionalUpdateLanguagesForO365** 為止。
7. 選取 [Value2]，然後按一下 [編輯內容]。  
![編輯 Value2 內容](..\media\3-queryresult.png)
8. 新增其他語言至 [Value2] 內容，然後按一下 [儲存內容]。  
例如，-pt-pt (葡萄牙文 - 葡萄牙)、af-za (南非荷蘭文 - 南非)、nn-no (挪威文 (耐諾斯克) - 挪威) 等等。  
![在 [內容編輯器] 中新增語言](..\media\4-props.png)  
9. 依序按一下 [關閉]、[關閉]、[儲存內容]、[儲存物件] \(如果在此按一下 [關閉]，則會捨棄所有值\)，按一下 [關閉]，然後按一下 [結束]，以結束 Windows Management Intstrumentation 測試器。
10. 在 Configuration Manager 主控台中，前往 [軟體程式庫] > [概觀] > [Office 365 用戶端管理] > [Office 365 更新]。
11. 現在，下載 Office 365 更新時，將會下載您在精靈中選取及在此程序中所設定語言的更新。 為確認下載了正確語言的更新，請前往更新的套件來源，並尋找檔案名稱中有該語言代碼的檔案。  
![其他語言的檔名](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>啟用 Office 365 用戶端之後變更更新頻道，可接收來自 Configuration Manager 的更新
啟用 Office 365 用戶端以接收來自 Configuration Manager 的更新之後，若要變更更新頻道，請使用群組原則，將登錄機碼值變更發佈至 Office 365 用戶端。 將 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** 登錄機碼變更為下列值之一︰

- 目前頻道︰  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- 延後的頻道︰  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- 第一次發行目前的頻道︰  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- 第一次發行延後的頻道︰  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf



<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->
