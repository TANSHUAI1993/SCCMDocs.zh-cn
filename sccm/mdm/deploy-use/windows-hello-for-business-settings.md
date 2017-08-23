---
title: "Windows Hello 企業版設定 | Microsoft Docs"
description: "了解如何整合 Windows Hello 企業版與 System Center Configuration Manager。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: a97b3d97eb302e4133b0a79a8c7e27004872c8b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager-hybrid"></a>System Center Configuration Manager 的 Windows Hello 企業版設定 (混合式)

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 讓您整合 Windows Hello 企業版 (原 Microsoft Passport for Windows)，這是 Windows 10 裝置的另一種登入方法。 Windows Hello 企業版使用 Active Directory 或 Azure Active Directory 帳戶來取代密碼、智慧卡或虛擬智慧卡。  

Windows Hello 企業版可讓您藉由 **使用者手勢** 登入，而不使用密碼。 使用者手勢可能是簡單的 PIN、生物識別驗證或外部裝置 (例如指紋辨識器)。  

 Configuration Manager 與 Windows Hello 企業版整合的方法有兩種：  

-   您可以使用 Configuration Manager 控制使用者可以/不可用以登入的筆勢。  

-   您可以將驗證憑證儲存在 Windows Hello 企業版金鑰儲存提供者 (KSP) 中。 如需詳細資訊，請參閱[憑證設定檔](create-pfx-certificate-profiles.md)。  

- 您可以將 Windows Hello 企業版原則部署至執行 Configuration Manager 用戶端且已加入網域的 Windows 10 裝置。 [在已加入網域的 Windows 10 裝置上設定 Windows Hello 企業版](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)中有此設定的說明。 當您使用 Configuration Manager 與 Intune (混合) 時，您可以在 Windows 10 和 Windows 10 行動裝置上設定這些設定，但不能在執行 Configuration Manager 用戶端且加入網域的裝置上設定。   

如需設定 Windows Hello 企業版設定的一般資訊，請參閱 [System Center Configuration Manager 的 Windows Hello 企業版設定](../../protect/deploy-use/windows-hello-for-business-settings.md)。

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>設定 Windows Hello 企業版設定 (混合)  

1.  在 Configuration Manager 主控台中，按一下 [管理] > [雲端服務] > [Microsoft Intune 訂閱]。  

3.  從清單中選取您的 Microsoft Intune 訂閱，然後在 **[首頁]** 索引標籤的 **[訂閱]** 群組中，按一下 **[設定平台]** > **[Windows (MDM)]**。  

4.  在 **[Microsoft Intune 訂閱內容]** 對話方塊的 **[Windows Hello 企業版]** 索引標籤上，從下列值中進行選擇，即可對所有已註冊 Windows 10 裝置和 Windows 10 行動裝置版裝置發揮效力：  

    -   **停用註冊之裝置上的 Windows Hello 企業版** 或 **啟用註冊之裝置上的 Windows Hello 企業版** - 在所有已註冊的 Windows 10 和 Windows 10 行動裝置版裝置上，啟用或停用 Windows Hello 企業版。  

    -   **使用信賴平台模組 (TPM)** - 信賴平台模組 (TPM) 晶片提供額外一層資料安全性。 選擇下列其中一個值：  

        -   **必要** (預設) - 只有能存取 TPM 的裝置可以佈建 Windows Hello 企業版。  

        -   **慣用** - 第一次嘗試使用 TPM 的裝置。 如果無法使用此值，則可以使用軟體加密  

    -   **需要 PIN 碼長度下限** - 指定 Windows Hello 企業版的 PIN 所需字元數目下限。 您必須使用至少 4 個字元 (預設值是 6 個字元)。  

    -   **需要 PIN 碼長度上限** - 指定 Windows Hello 企業版的 PIN 允許字元數目上限。 您最多可以使用 127 個字元。  

    -   **PIN 中需要有小寫字母** - 指定 Windows Hello 企業版的 PIN 是否必須使用小寫字母。 從下列選項進行選擇：  

        -   **允許** - 使用者可以在 PIN 中使用小寫字元。  

        -   **必要** - 使用者必須在 PIN 中包含至少一個小寫字元。  

        -   **不允許** (預設) - 使用者不得在 PIN 中使用小寫字元。  

    -   **PIN 中需要有大寫字母** - 指定 Windows Hello 企業版的 PIN 是否必須使用大寫字母。 從下列選項進行選擇：  

        -   **允許** - 使用者可以在 PIN 中使用大寫字元。  

        -   **必要** - 使用者必須在 PIN 中包含至少一個大寫字元。  

        -   **不允許** (預設) - 使用者不得在 PIN 中使用大寫字元。  

    -   **需要特殊字元** - 指定在 PIN 中使用特殊字元的方式。 從下列選項進行選擇：  

        -   **允許** - 使用者可以在 PIN 中使用特殊字元。  

        -   **必要** - 使用者必須在 PIN 中包含至少一個特殊字元。  

        -   **不允許** (預設) - 使用者不得在 PIN 中使用特殊字元 (這也是在未進行設定時會採取的行為)。  

         特殊字元包含：**! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**。  

    -   **需要 PIN 碼期限 (天)** - 指定必須變更裝置 PIN 的天數。 預設為 41 天。  

    -   **禁止重複使用舊 PIN 碼** - 使用此設定來限制重複使用先前用過的 PIN。 預設為不能重複使用最後 5 個使用過的 PIN。  

    -   **啟用生物識別手勢** - 啟用生物識別驗證 (例如臉部辨識或指紋) 以替代 Windows Hello 企業版的 PIN。 使用者仍然必須設定公司 PIN 以免生物識別驗證失敗。  

         若設為 **[已啟用]**，Windows Hello 企業版即允許生物識別驗證。  若設為 **[已停用]**，Windows Hello 企業版會防止生物識別驗證 (針對所有帳戶類型)。  

    -   **使用進階防詐騙 (如可使用)** - 設定是否在支援的裝置上使用進階防詐騙功能。  

         若設為 [已啟用] ，Windows 即要求所有使用者在支援的情況下，使用臉部特徵防詐騙。  

    -   **使用遠端 Passport** - 若此選項設為 **[已啟用]**，使用者即可使用遠端 Windows Hello 企業版作為桌上型電腦驗證的可攜式配套裝置。 桌上型電腦必須已加入 Azure Active Directory，且配套裝置必須設有 Windows Hello 企業版的 PIN。  

5.  完成後，請按一下 [確定] 。  

### <a name="see-also"></a>請參閱  
 [使用 System Center Configuration Manager 保護資料和站台基礎結構](../../protect/understand/protect-data-and-site-infrastructure.md)

 [使用商務用 Windows Hello 管理身分識別驗證](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)。  
