---
title: "使用 Lookout 設定訂閱 | System Center Configuration Manager"
description: "本主題提供如何設定 Lookout 裝置威脅保護的詳細資訊。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: b777140c753e709f4048a30e63d8ae730d3e8723
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>設定訂閱進行 Lookout 裝置威脅保護

*適用對象：System Center Configuration Manager (最新分支)*

若要準備好您的訂閱進行 Lookout 裝置威脅保護服務，Lookout 支援 (enterprisesupport@lookout.com) 需要 Azure Active Directory (Azure AD) 訂閱的下列資訊。 Lookout 行動端點安全性租用戶將會與 Azure AD 訂閱相關聯，以整合 Lookout 與 Intune。 

* **Azure AD 租用戶識別碼**
* 用於**完整** Lookout 主控台存取的 **Azure AD 群組物件識別碼**
* 用於**受限制** Lookout 主控台存取的 **Azure AD 群組物件識別碼** (選擇性)

> [!IMPORTANT]
> 尚未與 Azure AD 租用戶相關聯的現有 Lookout 行動端點安全性租用戶無法用於與 Azure AD 和 Intune 的整合。 請連絡 Lookout 支援，以建立新的 Lookout 行動端點安全性租用戶。 使用新的租用戶，將 Azure AD 使用者上架。

使用下節，收集您需要提供給 Lookout 支援小組的資訊。  

## <a name="get-your-azure-ad-information"></a>取得 Azure AD 資訊
### <a name="azure-ad-tenant-id"></a>Azure AD 租用戶識別碼
登入 [Azure AD 管理入口網站](https://manage.windowsazure.com)，然後選取您的訂閱。 

![顯示租用戶名稱之 Azure AD 頁面的螢幕擷取畫面](media/aad_tenant_name.png) 當您選擇訂閱名稱時，產生的 URL 會包括訂閱識別碼。  如果您有尋找訂閱識別碼的任何問題，請參閱這篇 [Microsoft 支援文章](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US)以取得尋找訂閱識別碼的秘訣。   
### <a name="azure-ad-group-id"></a>Azure AD 群組識別碼
Lookout 主控台支援 2 種存取層級︰  
* **完整存取：**Azure AD 系統管理員可以建立具有「完整存取」的使用者群組，以及選擇性地建立具有「限制存取」的使用者群組。  只有這些群組中的使用者才能登入 **Lookout 主控台**。
* **限制存取：**這個群組中的使用者無法存取 Lookout 主控台的數個設定和註冊相關模組，並且只能唯讀存取 Lookout 主控台的「安全性原則」模組。  

如需權限的詳細資訊，請閱讀 Lookout 網站上的[這篇文章](https://personal.support.lookout.com/hc/en-us/articles/114094105653)。

[群組物件識別碼] 位於 [Azure AD 管理主控台] 中群組的 [內容] 頁面上。

![反白顯示 GroupID 欄位之 [內容] 頁面的螢幕擷取畫面](media/aad_group_object_id.png)

收集這項資訊之後，請連絡 Lookout 支援 (電子郵件︰enterprisesupport@lookout.com)。

Lookout 支援會與您的主要連絡人合作以將您的訂閱上架，並使用您所收集的資訊建立 Lookout 企業帳戶。


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>使用 Lookout 裝置威脅保護設定訂閱
### <a name="step-1-set-up-your-device-threat-protection"></a>步驟 1：設定裝置威脅保護
在 Lookout 支援建立 Lookout 企業帳戶之後，您就可以登入 Lookout 主控台。   來自 Lookout 的電子郵件會傳送給您公司的主要連絡人，並且內含登入 URL 連結：https://aad.lookout.com/les?action=consent

當您第一次登入 Lookout 主控台時，必須使用具有 Azure AD 全域管理員角色的使用者帳戶，因為 Lookout 需要這項資訊才能註冊 Azure AD 租用戶。   後續登入不需要使用者具有這個層級的 Azure AD 特殊權限。  在這個首次登入時，會顯示同意頁面。 選擇 [接受] 完成註冊。

![Lookout 主控台之第一次登入頁面的螢幕擷取畫面](media/lookout-initial-login.png)

接受並同意之後，會將您重新導向至 Lookout 主控台。 使用下列 URL 即可完成初始註冊後的後續登入：https://aad.lookout.com

如果您發生登入問題，請參閱[疑難排解文章]()。

後續步驟概述您必須執行才能在 [Lookout 主控台](https://aad.lookout.com)內完成 Lookout 設定的工作。

### <a name="step-2-configure-the-intune-connector"></a>步驟 2：設定 Intune 連接器

1.  在 Lookout 主控台中，從 [系統] 模組中選擇 [連接器] 索引標籤，然後選取 [Intune]。

  ![開啟 [連接器] 索引標籤並反白顯示 Intune 選項之 Lookout 主控台的螢幕擷取畫面](media/lookout-setup-intune-connector.png)

2.  在 [連線設定] 選項中，設定活動訊號頻率 (分鐘)。  Intune 連接器現在已就緒。  

  ![顯示已設定活動訊號頻率之 [連線設定] 索引標籤的螢幕擷取畫面](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>步驟 3︰設定註冊群組
在 [註冊管理] 選項上，定義應該向 Lookout 註冊其裝置的一組使用者。 最佳做法是從小組使用者測試開始，並熟悉整合運作方式。  滿意測試結果之後，就可以將註冊擴充至其他使用者群組。

若要開始使用註冊群組，請先定義 Azure AD 安全性群組，其將是要在 Lookout 裝置威脅保護中註冊的第一組良好使用者。 在 Azure AD 中建立群組之後，請在 Lookout 主控台中移至 [註冊管理] 選項，並新增 Azure AD 安全性群組**顯示名稱**以進行註冊。

使用者位於註冊群組時，表示他們在 Azure AD 中所識別和支援的任何裝置都已註冊，且可以在 Lookout 裝置威脅保護中啟用。  第一次在其支援的裝置上開啟 Lookout for Work 應用程式時，會在 Lookout 中啟動裝置。

![Intune 連接器註冊頁面的螢幕擷取畫面](media/lookout-enrollment.png)

最佳做法是使用預設值 (5 分鐘) 作為時間增量，以檢查是否有新裝置。

>[!IMPORTANT]
> 顯示名稱區分大小寫。  使用 Azure 入口網站之安全性群組的 [內容] 頁面中所顯示的 [顯示名稱]。 請注意，在下圖中，於安全性群組的 [內容] 中，[顯示名稱] 是駝峰式大小寫。  不過，標題會以全部小寫顯示，而且不應該用來進入 Lookout 主控台。
>![Azure 入口網站、Azure Active Directory 服務、[內容] 頁面的螢幕擷取畫面](media/aad-group-display-name.png)

目前版本的限制如下：  
* 不會對群組顯示名稱進行任何驗證。  請務必使用 Azure AD 安全性群組之 Azure 入口網站中所顯示 [顯示名稱] 欄位中的值。
* 目前不支援在群組內建立群組。  指定的 Azure AD 安全性群組可能只包含使用者，而未包含巢狀群組。


### <a name="step-4-configure-state-sync"></a>步驟 4：設定狀態同步處理
在 [State Sync]\(狀態同步處理) 選項中，指定應該傳送至 Intune 的資料類型。  目前，您必須啟用裝置狀態和威脅狀態，Lookout Intune 整合才能正確運作。  根據預設會啟用這些項目。
### <a name="step-5-configure-error-report-email-recipient-information"></a>步驟 5︰設定錯誤報告電子郵件收件者資訊
在 [Error Management]\(錯誤管理) 選項中，輸入應接收錯誤報告的電子郵件地址。

![Intune 連接器錯誤管理頁面的螢幕擷取畫面](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>步驟 6： 進行註冊設定
在 [系統] 模組的 [連接器] 頁面上，指定將裝置視為中斷連線之前的天數。  中斷連線的裝置會被視為不相容，並且會根據 SCCM 條件式存取原則來封鎖存取您公司應用程式。 您可以指定介於 1 與 90 天之間的值。

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>步驟 7：設定電子郵件通知
如果您想要接收威脅的電子郵件警示，請使用應接收通知的使用者帳戶來登入 [Lookout 主控台](https://aad.lookout.com)。 在 [系統] 模組的 [喜好設定] 索引標籤上，選擇所需的通知，並將它們設定為 **ON**。 儲存變更。

![顯示使用者帳戶之 [喜好設定] 頁面的螢幕擷取畫面](media/lookout-email-notifications.png) 如果您不想再收到電子郵件通知，請將通知設定為 **OFF**，然後儲存變更。
### <a name="step-8-configure-threat-classification"></a>步驟 8：設定威脅分類
Lookout 裝置威脅保護會分類各種類型的行動威脅。 [Lookout 威脅分類](http://personal.support.lookout.com/hc/en-us/articles/114094130693)具有相關聯的預設風險層級。 隨時可以變更這些項目，以符合您公司的需求。

![顯示威脅和分類之 [原則] 頁面的螢幕擷取畫面](media/lookout-threat-classification.png)

>[!IMPORTANT]
> 因為 Intune 整合會在執行階段根據這些風險層級來計算裝置合規性，所以這裡指定的風險層級是裝置威脅保護的重要層面。 換句話說，如果裝置具有最少層級為高、中或低的使用中威脅，則 Intune 系統管理員會在原則中設定將裝置識別為不相容的規則。 Lookout 裝置威脅保護中的威脅分類原則直接驅使 Intune 中的裝置合規性計算。

## <a name="watching-enrollment"></a>監看註冊
安裝完成之後，Lookout 裝置威脅保護會開始輪詢 Azure AD 是否有對應至所指定註冊群組的裝置。  您可以找到 [裝置] 模組上所註冊之裝置的相關資訊。  裝置的初始狀態會顯示為擱置。  在裝置上安裝、開啟和啟動 Lookout for Work 應用程式之後，裝置狀態會變更。  如需如何將 Lookout for Work 應用程式發送到裝置的詳細資訊，請參閱[設定和部署 Lookout for Work 應用程式](configure-and-deploy-lookout-for-work-apps.md)主題。
## <a name="next-steps"></a>後續步驟
[在 Intune 中啟用 Lookout MTP 連線](enable-lookout-connection-in-intune.md)
