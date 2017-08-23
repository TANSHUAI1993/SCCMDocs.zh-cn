---
title: "如何建立使用 Intune 進行管理之 Android for Work 裝置的設定項目"
ms.custom: na
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
caps.latest.revision: "17"
caps.handback.revision: "0"
author: robstackmsft
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 87b34f0a3cce87f6e2ba813957a69b743648c1ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>如何建立使用 Intune 進行管理之 Android for Work 裝置的設定項目

 使用 System Center Configuration Manager **Android for Work** 設定項目，管理 Microsoft Intune 中所註冊或 Configuration Manager 透過內部部署方式管理之 Android for Work 裝置的設定。  

### <a name="to-create-an-android-for-work-configuration-item"></a>建立 Android for Work 設定項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與合規性]。  

2.  在 [資產與相容性]  工作區中，展開 [相容性設定] ，然後按一下 [設定項目] 。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立設定項目] 。  

4.  在 [建立設定項目精靈]  的 [一般] 頁面上，指定設定項目的名稱和選擇性描述。  

5.  在 [指定您要建立的設定項目類型] 下，選取 [Android for Work]。  

6.  如果您要建立並指派類別，以協助您在 Configuration Manager 主控台中搜尋和篩選設定項目，請選擇 [類別]。  

  按一下 [下一步] 。

7.  在精靈的 [裝置設定] 頁面上，選取您想要設定的設定群組。 如需詳細資訊，請參閱 [Android for Work 設定項目設定](#android-for-work-configuration-item-settings-reference)，再按一下 [下一步]。  

  > [!TIP]  
  >  如果未列出您想要的設定，請選取 [設定不在預設設定群組中的其他設定] 核取方塊。  

9. 在每一個設定頁面上，進行您需要的設定，並指定這些設定與裝置不相容時是否要進行補救 (如果支援的話)。  

10. 針對每個設定群組，您也可以設定下列嚴重性，以在找到不相容的組態項目時加以回報：  

    -   **無** - 不符合這項合規性規則的裝置不會回報 Configuration Manager 報告的失敗嚴重性。  

    -   **資訊** - 不符合這項合規性規則的裝置會回報 Configuration Manager 報告的 [資訊] 失敗嚴重性。  

    -   **警告** - 不符合這項合規性規則的裝置會回報 Configuration Manager 報告的 [警告] 失敗嚴重性。  

    -   **重大** - 不符合這項合規性規則的裝置會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。  

    -   **重大事件** - 不符合這項合規性規則的裝置會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。 這個嚴重性等級也會在應用程式事件記錄檔中記錄為 Windows 事件。  

11. 在精靈的 [平台適用性]  頁面上，檢閱是否有與您先前選取的支援平台不相容的任何設定。 您可以返回並移除這些設定，也可以繼續。  

    > [!TIP]  
    >  系統不會針對不支援的設定進行相容性評估。  

12. 完成精靈。  

 您可以在 [資產與合規性] 工作區的 [設定項目] 節點中檢視新的設定項目。  

##  <a name="android-for-work-configuration-item-settings-reference"></a>Android for Work 設定項目設定參考  

### <a name="password"></a>密碼  

|設定|詳細資料|  
|-------------|-------------|  
|**需要裝置上的密碼設定**|支援的裝置上需要的密碼。|  
|**最小密碼長度 (字元數)**|密碼長度下限。|  
|**密碼到期天數**|密碼必須變更之前的天數。|  
|**記住的密碼數目**|防止重複使用最近使用過的密碼。|  
|**抹除裝置前允許的失敗登入次數**|如果登入嘗試失敗是這個數目即抹除裝置。|  
|**鎖定裝置前的閒置時間**|選取裝置鎖定前未使用的時間長度。|
|**密碼品質**|選取所需的密碼複雜性等級以及是否可以使用生物特徵辨識裝置。|  
|**允許 Smart Lock 和其他信任代理程式**|可讓您控制相容 Android 裝置上的 Smart Lock 功能。 此電話功能 (有時也稱為信任代理程式) 可讓您在裝置位於受信任的位置 (例如連線到特定的藍牙裝置或靠近 NFC 標記) 時，停用或略過裝置鎖定畫面密碼。 您可以使用此設定來防止使用者設定 Smart Lock。|
|**解除鎖定的指紋**|&nbsp;|

###  <a name="work-profile"></a>工作設定檔  
 這些設定僅適用於 Samsung KNOX 裝置。  

|設定名稱|詳細資料|  
|------------------|-------------|  
|**允許工作與個人設定檔之間的資料共用**|從下列選項進行選擇：<br>- **尚未設定**<br>- 預設共用限制<br>- **工作設定檔中的應用程式可以處理來自個人設定檔的要求**<br>- **個人設定檔中的應用程式可以處理來自工作設定檔的要求**<br><br>(另請參閱使用自訂 URI 的[複製-貼上設定](#copy-paste-configuration-item-settings))|  
|**裝置鎖定時隱藏工作設定檔通知 (Android 6.0 +)**||
|**設定預設的應用程式權限原則 (Android 6.0+)**|從下列選項進行選擇：<br>- **尚未設定**<br>- **一律要求確認**<br>- **自動授與**<br>- **自動拒絕**|

### <a name="copy-paste-configuration-item-settings"></a>複製-貼上設定項目設定
[允許工作與個人設定檔之間的資料共用] 的選項均未防止複製-貼上的行為。 請使用可設定為防止複製-貼上的自訂設定。 您可以透過自訂 URI 來進行此設定。

- OMA-URI：./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- 值類型：布林值

將 DisallowCrossProfileCopyPaste 設定為 true 可防止 Android for Work 個人與工作設定檔之間的複製貼上行為。

## <a name="see-also"></a>另請參閱  
 [不使用 System Center Configuration Manager 用戶端所管理之裝置的設定項目](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
