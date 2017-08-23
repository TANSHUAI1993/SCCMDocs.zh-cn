---
title: "管理 Dynamics CRM Online 存取 | Microsoft Docs"
description: "了解如何從 iOS 和 Android 裝置使用 Microsoft Intune 條件存取，來控制對 Microsoft Dynamics CRM Online 的存取。"
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理 Dynamics CRM Online 存取

適用於：System Center Configuration Manager (最新分支)

您可以從 iOS 和 Android 裝置使用 Microsoft Intune 條件存取，來控制對 Microsoft Dynamics CRM Online 的存取。  Intune 條件存取有兩個元件：
* [裝置相容性原則](../../protect/deploy-use/device-compliance-policies.md)，裝置必須符合此原則才算相容。
* [條件存取原則](../../protect/deploy-use/manage-access-to-services.md)，其中指定裝置必須符合才能存取服務的條件。

若要深入了解條件存取如何運作，請參閱[管理服務的存取權](../../protect/deploy-use/manage-access-to-services.md)一文。


當目標使用者嘗試在其裝置上使用 Dynamics CRM 應用程式時，就會進行下列評估：

![此圖顯示用來決定允許或禁止裝置存取服務的決策點](media/mdm-ca-dynamics-crm-flow-diagram.png)

需要存取 Dynamics CRM Online 的裝置必須：
* 是 **Android** 或 **iOS** 裝置。
* 向 Microsoft Intune **註冊**。
* 必須**符合**所部署的任何 Microsoft Intune 相容性原則。

裝置狀態儲存在 Azure Active Directory，它會根據您指定的條件，授與或封鎖存取權。

如不符合條件，使用者會在登入時看見下列訊息之一：
* 如果裝置未向 Microsoft Intune 註冊，或未在 Azure Active Directory 中登錄，就會顯示訊息，指示如何安裝及註冊公司入口網站應用程式。
* 如果裝置不相容，即會顯示一則訊息，將使用者引導至 Microsoft Intune 公司入口網站或公司入口網站應用程式，讓他們能夠在該處找到問題的相關資訊，以及如何修復問題的方法。

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>設定 Dynamics CRM Online 的條件存取  
### <a name="step-1-configure-active-directory-security-groups"></a>步驟 1：設定 Active Directory 安全性群組

在開始之前，請先為條件式存取原則設定 Azure Active Directory 安全性群組。 您可以在 **Office 365 系統管理中心**設定這些群組。 這些群組將用於設定原則的目標使用者，或將使用者豁免於原則。 當使用者成為原則的目標時，他們使用的每個裝置都必須相容，才能存取資源。

您可以指定兩種群組類型來用於 Dynamics CRM 原則：
* **目標群組** - 包含套用原則的使用者群組。
* **免套用的群組** - 包含免套用原則的使用者群組。

如果使用者隸屬於這兩個群組，他們將免套用原則。

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步驟 2：建立及部署相容性原則
[建立及部署](../../protect/deploy-use/device-compliance-policies.md)相容性原則到將受此原則影響的所有裝置。 這些是目標群組中的使用者所使用的所有裝置。

> [!NOTE]
> 相容性原則會部署至 Microsoft Intune 群組，而條件存取原則會以 Azure Active Directory 安全性群組為目標。

> [!IMPORTANT]
> 如果您尚未部署相容性原則，則會將裝置視為相容。

當您就緒時，請繼續執行步驟 3。
### <a name="step-3-configure-the-dynamics-crm-policy"></a>步驟 3︰設定 Dynamics CRM 原則
接著，設定原則要求只有受管理和相容的裝置才可以存取 Dynamics CRM。 這項原則會儲存在 Azure Active Directory。

1.  在 Microsoft Intune 管理主控台中，選擇 [原則] > [條件存取] > [Dynamics CRM Online 原則]。

     ![Dynamics CRM Online 條件存取原則頁面的螢幕擷取畫面](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  選取 [啟用條件存取原則]。
3.  在 **[應用程式存取]**下，您可以選擇將條件式存取原則套用至：
  * **iOS**
  * **Android**
4.  選擇 [目標群組] 下方的 [修改]，選取要套用原則的 Azure Active Directory 安全性群組。 您可以選擇針對所有使用者，或僅針對選取的使用者群組。
5.  選擇性地選擇 [免套用的群組] 下方的 [修改]，選取免套用此原則的 Azure Active Directory 安全性群組。
6.  完成之後，請選擇 [儲存]。

您現在已設定 Dynamics CRM 的條件存取。 您不需部署條件式存取原則，它會立即生效。
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>監視相容性及條件式存取原則

在 [群組] 工作區中，您可以檢視裝置的條件存取狀態。

選取任何行動裝置群組，然後在 **[裝置]** 索引標籤上，選取下列其中一個 **[篩選]**：
* [沒有登錄 AAD 的裝置] - 從 Dynamics CRM 封鎖這些裝置。
* [不相容的裝置] - 從 Dynamics CRM 封鎖這些裝置。
* [已登錄了 AAD 並相容的裝置] - 這些裝置可以存取 Dynamics CRM。

###  <a name="see-also"></a>請參閱
[管理對電子郵件的存取](../../protect/deploy-use/manage-email-access.md)

[管理對 SharePoint Online 的存取](../../protect/deploy-use/manage-sharepoint-online-access.md)

[管理對商務用 Skype Online 的存取](../../protect/deploy-use/manage-skype-for-business-online-access.md)
