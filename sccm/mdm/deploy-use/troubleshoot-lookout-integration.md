---
title: "針對 Lookout 整合進行疑難排解 | System Center Configuration Manager"
description: "本主題說明 Lookout 整合經常發生的疑難排解問題。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4fd2d3b8aae6a2f42e7c6a87723d16368be30984
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>針對 Lookout 與 Intune 整合進行疑難排解

*適用於：System Center Configuration Manager (最新分支)*

## <a name="troubleshoot-login-errors"></a>針對登入錯誤進行疑難排解
### <a name="403-errors"></a>403 錯誤
當您登入 [Lookout MTP 主控台](https://aad.lookout.com)時，可能會看到 403 錯誤：**您沒有存取服務的授權**。您所指定的使用者名稱不是設定成存取 Lookout MTP 的 Azure Active Directory (Azure AD) 群組成員時，可能會發生這種情況。

Lookout MTP 設定成僅允許所設定 Azure AD 群組的使用者具有存取權。 如果您不確定哪個群組設定成具有 Lookout MTP 存取權，請連絡 Lookout支援。

您可以透過下列方法來連絡 Lookout 支援︰

* 電子郵件：enterprisesupport@lookout.com
* 登入 [MTP 主控台](http://aad.lookout.com)，並瀏覽至 [支援] 模組。
* 前往：https://enterprise.support.lookout.com/hc/en-us/requests，並提出支援要求。

### <a name="unable-to-sign-in"></a>無法登入
Azure AD 全域系統管理員使用者尚未接受初始 Lookout 安裝程式時，您可能會看到下列錯誤。

![顯示登入錯誤之 Lookout 登入畫面的螢幕擷取畫面](media/lookout-consent-not-accepted-error.png)

若要解決這個問題，全域系統管理員使用者必須登入 https://aad.lookout.com/les?action=consent，並接受起始安裝程式的提示。 如需詳細資訊，請參閱[使用 Lookout MTP 設定訂閱](set-up-your-subscription-with-lookout.md)主題。

## <a name="troubleshoot-device-status-issues"></a>針對裝置狀態問題進行疑難排解

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>未顯示在 Lookout MTP 主控台裝置清單中的裝置

在下列任一案例中，可能會發生這個錯誤︰
* 擁有此裝置的使用者不在 [Lookout MTP Console]\(Lookout MTP 主控台) 中所指定的 [註冊群組] 內。  從 [系統] 模組中，移至 [Intune 連接器] 索引標籤，並查看 [Enrollment Management]\(註冊管理) 設定。  您應該會看到設定要進行註冊的一或多個 Azure AD 群組。  確認擁有遺失裝置的使用者是否屬於其中一個指定的 Azure AD 群組。  將新的使用者新增至註冊群組之後，需要設定的輪詢間隔 (5 分鐘是預設值) 才能看到裝置顯示在 Lookout MTP 主控台的 [裝置] 模組中。

* 如果 Lookout MTP 不支援裝置。  不支援的裝置將會出現在 Lookout MTP 主控台上之連接器設定的 [受管理的裝置] 區段中。

### <a name="device-continues-to-be-reported-as-pending"></a>裝置會繼續報告為 [擱置]

顯示 [擱置] 的裝置表示使用者尚未開啟 Lookout for Work 應用程式和點選 [啟用] 按鈕。 如需使用 Lookout for Work 應用程式之裝置啟用的詳細資訊，請閱讀下列主題︰

[系統提示您在 Android 裝置上安裝 Lookout for Work](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>在 Lookout MTP 主控台中，裝置會顯示為使用中，但沒有裝置識別碼。
這表示擁有此裝置的使用者不在 Lookout MTP 主控台中所指定的註冊群組內。   如果已經從註冊群組移除擁有裝置的使用者，或已移除使用者所屬的註冊群組，則裝置可以進入此狀態。

從 Lookout MTP 主控台的 [系統] 模組中，移至 [Intune 連接器] 索引標籤，並檢閱 [註冊] 設定。  您應該會看到設定要進行註冊的一或多個 Azure AD 群組。  確認擁有裝置的使用者是否屬於其中一個指定的 Azure AD 群組。

裝置處於此狀態時，Lookout 會在偵測到任何威脅時繼續通知使用者，但不是將任何威脅資訊傳送至 Intune。

### <a name="device-shows-disconnected-state"></a>裝置顯示已中斷連線狀態

已中斷連線表示 Lookout MTP 在過了預先設定的時間間隔之後仍未接聽到裝置 (預設值為 30 天，最少 7 天)。 這表示公司入口網站應用程式或 Lookout for Work 應用程式未安裝在裝置上或已予以解除安裝。 重新安裝應用程式應該可以解決這個問題。 使用者開啟 Lookout for Work 並啟用應用程式時，裝置會與 Lookout MTP 和 Intune 重新同步。

### <a name="forcing-a-resync-on-the-device"></a>強制在裝置上進行重新同步
從 Lookout MTP 主控台的 [裝置] 模組中，系統管理員可以選取裝置，並選擇將它刪除。   裝置擁有者下一次開啟 Lookout for Work 應用程式，並點選 [啟用] 時，裝置狀態將會執行完整重新同步。

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>裝置的擁有者不再使用此裝置
您必須抹除裝置，並要求新的使用者註冊 (如[本主題](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe)中所述)。


您也可以移至 Lookout MTP 主控台的 [裝置] 模組，然後選擇 [刪除]。

只要新使用者位於 Lookout MTP 主控台中所指定的其中一個註冊群組內，裝置就會在 Azure AD 將裝置關聯到新使用者之後出現。

## <a name="compliance-remediation-workflows"></a>合規性修復工作流程
[系統提示您在 Android 裝置上安裝 Lookout for Work]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[您必須解決 Lookout for Work 在 Android 裝置上找到的威脅](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
