---
title: "為用戶端管理的 Mac 建立設定項目 - Configuration Manager | Microsoft Docs"
description: "使用 System Center Configuration Manager Mac OS X 設定項目，管理 Mac OS X 裝置的設定。"
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 541e5ad629a9e2ed9c353dff150f9b86b9d12b7d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>如何為 System Center Configuration Manager 用戶端所管理的 Mac OS X 裝置建立組態項目
使用 System Center Configuration Manager **Mac OS X (自訂)** 設定項目管理 Configuration Manager 用戶端所管理之 Mac OS X 裝置的設定。  
  
 Mac OS X 作業系統使用內容清單 (或 plist) 檔案來儲存應用程式設定。 相容性設定可用來評估及補救內容清單檔案中的設定。 您也可以撰寫殼層指令碼，傳回可評估及補救相容性的值，來管理 Mac OS X 設定。  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>建立自訂 Mac OS X 組態項目  
  
1.  在 Configuration Manager 主控台中，按一下 [資產與合規性]。  
  
2.  在 [資產與相容性]  工作區中，展開 [相容性設定] ，然後按一下 [設定項目] 。  
  
3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立設定項目] 。  
  
4.  在 [建立設定項目精靈]  的 [一般] 頁面上，指定設定項目的名稱和選擇性描述。  
  
5.  在 [指定您要建立的組態項目類型] 下，選取 [Mac OS X (自訂)] 。  
  
6.  如果您要建立並指派類別，以協助您在 Configuration Manager 主控台中搜尋和篩選設定項目，請按一下 [類別]。  
  
7.  在精靈的 [支援的平台]  頁面上，選取將評估組態項目的特定 Mac OS X 版本。  
  
8.  在精靈的 [設定]  頁面上，您將會新增要在 Mac 電腦上評估相容性的設定。 按一下 [新增]  以開啟 [建立設定]  對話方塊。  
  
9. 在 [建立設定]  對話方塊中，輸入設定的唯一名稱和描述。  
  
10. 選擇您要的 [設定類型]  ，然後提供必要資訊，如下表所示：  
  
    -   **Mac OS X 喜好設定** -  
  
        -   **應用程式識別碼** - 指定您要從中評估索引鍵相容性之內容清單檔案的應用程式識別碼。  
  
             例如，如果您想要編輯的 Safari 網頁瀏覽器設定，您可能會使用 **com.apple.Safari.plist**。  
  
        -   **金鑰** – 指定您想要評估 Mac 電腦上的符合性的索引鍵的名稱。 請使用下列語法：/<字典\>/<索引鍵名稱\>。  
  
            > [!IMPORTANT]  
            >  索引鍵名稱區分大小寫，且當其名稱與 Mac 電腦上的索引鍵名稱不同時將不會進行評估。 此外，索引鍵名稱在指定之後就無法再進行編輯。 如果您需要編輯索引鍵的名稱，刪除並重新建立此設定。  
  
    -   **指令碼** -  
  
        -   **探索指令碼** - 按一下 [新增指令碼] ，然後輸入殼層指令碼，以評估 Mac 電腦上的設定相容性。 在殼層指令碼中使用 **echo** 命令，以將值傳回至 Configuration Manager 評估其相容性。 Configuration Manager 使用 **STDOUT** 中傳回的結果來評估相容性。  
  
            > [!IMPORTANT]  
            >  請勿在探索指令碼中包含 **reboot** 命令。 由於每次重新啟動用戶端就會執行探索指令碼，因此這樣做會導致 Mac 電腦持續重新啟動。  
  
        -   **補救指令碼 (選擇性)** - 選擇性地按一下 [新增指令碼]  ，然後輸入殼層指令碼，以用來補救 Mac 用戶端電腦上所找到的任何不相容設定。  
  
            > [!IMPORTANT]  
            >  為了確保您不會引入 Mac 電腦無法解譯的格式字元，請勿使用複製並貼上，而改為在指令碼中輸入。  
  
11. 選擇 [資料類型]  ，這是條件傳回資料所使用的格式，之後會使用條件來評估設定。  
  
    > [!NOTE]  
    >  **浮點數** 資料類型支援只有 3 個數字的小數點後。  
    >   
    >  Configuration Manager 不支援使用**布林** Mac 設定項目指令碼設定的資料類型。 相反地，請將資料類型設定為 [整數]  ，並確定指令碼會傳回整數值。  
  
12. 按一下 [確定]  儲存設定並關閉 [建立設定]  對話方塊，然後繼續依照您的需要新增許多設定。  
  
13. 在精靈的 [相容性規則]  頁面上，您將會指定用於定義組態項目相容性的條件。 設定至少必須有一項相容性規則，才能評估其相容性。 按一下 [新增]  以新增規則。  
  
14. 在 [建立規則]  對話方塊中，提供下列資訊：  
  
    -   **名稱：** 輸入符合性規則的名稱。  
  
    -   **描述:** 輸入符合性規則的描述。  
  
    -   **選取的設定︰** 按一下 **瀏覽** 開啟 **選取設定** 對話方塊。 選取您想要定義的規則或按一下 設定 **新設定**。 當您完成時，請按一下 **選取**。  
  
        > [!TIP]  
        >  您也可以按一下 **屬性** 若要檢視目前所選設定的相關資訊。  
  
    -   **規則類型** ：選取您要使用的相容性規則類型：  
  
        -   **值** ：建立規則來比較組態項目所傳回的值與您所指定的值。  
  
        -   **存在** ：建立規則根據裝置上是否有設定，來評估設定。  
  
    -   針對 [值] 規則類型，指定下列資訊：  
  
        -   設定必須符合下列規則 - 選取用來評估所選設定相容性的運算子和值。 您可以使用下列運算子：  
  
            -   **等於**  
  
            -   **不等於**  
  
            -   **大於**  
  
            -   **小於**  
  
            -   **介於**  
  
            -   **大於或等於**  
  
            -   **小於或等於**  
  
            -   **其中一個** - 在文字方塊中，一行指定一個項目。  
  
            -   **無** - 在文字方塊中，一行指定一個項目。  
  
        -   **支援時補救不相容的規則** - 如果您要讓 Configuration Manager 自動補救不相容的規則，請選取這個選項。  
  
            > [!IMPORTANT]  
            >  只有在規則運算子設定為 [等於] 時，才能補救不相容的規則。  
  
        -   **如果找不到此設定執行個體，即回報不相容** - 如果在 Mac 電腦上找不到這項設定，則會回報組態項目不相容。  
  
    -   **報告的不相容嚴重性** - 指定在不符合這項相容性規則時所報告的嚴重性等級。 可用的嚴重性等級如下：  
  
        -   **無** - 不符合這項合規性規則的電腦不會回報 Configuration Manager 報告的失敗嚴重性。  
  
        -   **資訊**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [資訊] 失敗嚴重性。  
  
        -   **警告**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [警告] 失敗嚴重性。  
  
        -   **重大**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。  
  
        -   **重大事件**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。 Mac 用戶端電腦也會記錄這個嚴重性等級。  
  
    -   針對 [存在] 規則類型，指定下列資訊：  
  
        -   選擇其中一個：  
  
            -   **設定必須存在於用戶端裝置上**  
  
            -   **此設定必須存在於用戶端裝置**  
  
        -   **報表的檢驗嚴重性:** 指定如果此符合性規則失敗則會報告嚴重性層級。 可用的嚴重性等級如下：  
  
            -   **無** - 不符合這項合規性規則的電腦不會回報 Configuration Manager 報告的失敗嚴重性。  
  
            -   **資訊**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [資訊] 失敗嚴重性。  
  
            -   **警告**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [警告] 失敗嚴重性。  
  
            -   **重大**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。  
  
            -   **重大事件**不符合這項合規性規則的電腦會回報 Configuration Manager 報告的 [重大] 失敗嚴重性。 Mac 用戶端電腦也會記錄這個嚴重性等級。  
  
        > [!NOTE]  
        >  所顯示的選項可能會依您設定規則的設定類型而有所不同。  
  
    -   按一下 [確定]  關閉 [建立規則]  對話方塊。  
  
15. 在 [摘要]  頁面上，確認新組態項目的設定，然後完成精靈。  
  
 新的設定項目會顯示在 [資產與相容性]  工作區的 [設定項目]  節點中。  
  
 如果您現在要將這個設定項目新增至設定基準，請參閱[如何在 System Center Configuration Manager 中建立組態基準](../../compliance/deploy-use/create-configuration-baselines.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 System Center Configuration Manager 用戶端所管理之裝置的設定項目](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
