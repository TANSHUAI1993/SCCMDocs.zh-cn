---
title: "管理商務用 Skype Online 存取 | Microsoft Docs"
description: "了解如何使用條件式存取原則來管理商務用 Skype Online 的存取權。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: cacb22a85e74a7d9cae75ad907d0206487cd4dc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-skype-for-business-online-access"></a>管理商務用 Skype Online 存取

*適用對象：System Center Configuration Manager (最新分支)*


使用  **商務用 Skype Online** 的條件式存取原則，根據您所指定的條件管理商務用 Skype Online 存取。  


 當目標使用者嘗試在他們的裝置上使用商務用 Skype Online，則會發生下列評估︰![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>先決條件  

-   啟用商務用 Skype Online 的新式驗證。 請填寫這份 [Connect 表單](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) ，以註冊加入新式驗證計畫。  

-   您所有的一般使用者都必須使用商務用 Skype Online。 如果您有同時部署商務用 Skype Online 與商務用 Skype 內部部署，則一般使用者不會套用條件式存取原則。  

-   需要存取商務用 Skype Online 的裝置必須：  

    -   為 Android 或 iOS 裝置。  

    -   註冊 Intune。  

    -   與任何已部署的 Intune 相容性原則相容。  

 裝置狀態儲存在 Azure Active Directory，它會根據您指定的條件，授與或封鎖存取權。  
如不符合條件，使用者會在登入時看見下列訊息之一：  

-   如果裝置未註冊 Intune，或未在 Azure Active Directory 中登錄，就會顯示訊息，指示如何安裝及註冊公司入口網站應用程式。  

-   如果裝置不相容，即會顯示一則訊息，將使用者引導至 Intune 公司入口網站或公司入口網站 app，讓他們能夠在該處找到問題的相關資訊，以及如何修復問題的方法。  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>設定商務用 Skype Online 的條件式存取  

### <a name="step-1-configure-active-directory-security-groups"></a>步驟 1：設定 Active Directory 安全性群組  
 在開始之前，請先為條件式存取原則設定 Azure Active Directory 安全性群組。 您可以在 Office 365 系統管理中心中設定這些群組。 這些群組包含將成為原則目標的使用者，或是免套用此原則的使用者。 當使用者成為原則的目標時，他們使用的每個裝置都必須相容，才能存取資源。  

 您可以指定要用於商務用 Skype 原則的兩種群組類型 ︰  

-   目標群組 â€“ 包含套用原則的使用者群組  

-   豁免群組 â€“ 包含豁免原則的使用者群組 (選擇性)  
    如果使用者隸屬於這兩個群組，他們將免套用原則。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>步驟 2：建立及部署相容性原則  
 請確定您針對商務用 Skype Online 原則設為目標之所有裝置建立與部署相容性原則。  

 如需如何設定相容性原則的詳細資訊，請參閱[在 System Center Configuration Manager 中管理裝置相容性原則](../../protect/deploy-use/device-compliance-policies.md)。  

> [!NOTE]  
>  如果您尚未部署相容性原則而啟用商務用 Skype Online 原則，則系統將允許所有已在 Intune 中註冊的目標裝置進行存取。  

 當您就緒時，請繼續執行步驟 3。  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>步驟 3：設定商務用 Skype Online 原則  
 接著，設定原則以要求只有受管理和相容的裝置才可以存取商務用 Skype Online。 這項原則會儲存在 Azure Active Directory。  

1.  在 [Microsoft Intune 管理主控台](https://manage.microsoft.com)中，按一下 **[原則]** > **[條件式存取]** > **Skype for Business Online [原則]**。  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  選取 **[啟用條件存取原則]**。  

3.  在 **[應用程式存取]**下，您可以選擇將條件式存取原則套用至：  

    -   iOS  

    -   Android  

4.  按一下 [目標群組] 下方的 [修改]  ，選取要套用原則的 Azure Active Directory 安全性群組。 您可以選擇針對所有使用者，或僅針對選取的使用者群組。  

5.  按一下 [豁免群組] 下方的 [修改]  ，選取豁免此原則的 Azure Active Directory 安全性群組。  

6.  完成之後，請按一下 [儲存] 。  

 您現在已設定商務用 Skype Online 的條件式存取。 您不需部署條件式存取原則，它會立即生效。  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>監視相容性及條件式存取原則  
 在 [群組] 工作區中，您可以檢視裝置的條件式存取狀態。  

 選取任何行動裝置群組，然後在 **[裝置]** 索引標籤上，選取下列其中一個 **[篩選]**：  

-   **沒有註冊 AAD 的裝置** â€“ 商務用 Skype Online 已封鎖這些裝置。  

-   **不相容的裝置** â€“ 商務用 Skype Online 已封鎖這些裝置。  

-   **已註冊 AAD 且相容的裝置** â€“ 這些裝置可以存取商務用 Skype Online。  

### <a name="see-also"></a>請參閱  

 [在 System Center Configuration Manager 中管理裝置相容性原則](../../protect/deploy-use/device-compliance-policies.md)
