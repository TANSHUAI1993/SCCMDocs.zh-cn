---
title: "使用 System Center Configuration Manager 設定 Intune 訂閱 | Microsoft Docs"
description: "使用 System Center Configuration Manager 設定 Intune 訂閱。"
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 22d890c972d3166f9c7b583d8d3fa917c1897880
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 設定 Intune 訂閱

*適用對象：System Center Configuration Manager (最新分支)*

Intune 訂閱可讓您透過網際網路管理裝置。 這包含指定哪些使用者集合可以註冊裝置，以及定義要向使用者呈現的資訊。 在建立 Intune 訂閱時，您也可以使用貴公司的標誌和自訂色彩配置，將公司商標新增到 Intune 公司入口網站。

Intune 訂閱會執行下列動作：

-   擷取服務連線點所需的憑證，以連線至 Intune 服務
-   定義可讓使用者註冊行動裝置的使用者集合
-   定義及設定您要支援的行動平台

> [!IMPORTANT]
>  在 Configuration Manager 中建立 Microsoft Intune 訂閱會讓您的站台服務連接點進入「線上模式」。 請參閱[關於 System Center Configuration Manager 中的服務連線點](../../core/servers/deploy/configure/about-the-service-connection-point.md)。

## <a name="to-create-the-microsoft-intune-subscription"></a>建立 Windows Intune 訂閱

1.  如果您還沒有這麼做，可在 [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216) 上註冊 Microsoft Intune 帳戶。  建立 Intune 帳戶之後，就不需要將任何使用者新增至 Intune 帳戶，或執行其他設定。

2.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

3.  在 **[系統管理]** 工作區中，展開 **[雲端服務]**，然後按一下 **[Microsoft Intune 訂閱]**(搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理新功能)。 在 [首頁]  索引標籤上按一下 [新增 Microsoft Intune 訂閱] 。

![建立 Intune 訂閱](../media/mdm-set-intune.png)

4.  在 [建立 Microsoft Intune 訂閱精靈] 的 [簡介]  頁面檢閱文字，然後按 [下一步] 。

5.  在 [訂閱]  頁面上按一下 [登入]  ，並使用您的工作或學校帳戶登入。 在 [設定行動裝置管理授權單位] 對話方塊中，選取只透過 Configuration Manager 主控台使用 Configuration Manager 管理行動裝置的核取方塊。 若要繼續訂閱，您必須選取此選項。

    > [!IMPORTANT]
    >  一旦您選取 Configuration Manager 作為管理授權單位，便只能在 Configuration Manager 1610 版或更新版本以及 Microsoft Intune 1705 版中，才能將管理授權單位變更為 Microsoft Intune，而不需要連絡 Microsoft 支援服務，也不需要取消現有受管理裝置的註冊並重新註冊。 如需詳細資訊，請參閱[變更您的 MDM 授權單位](/sccm/mdm/deploy-use/change-mdm-authority)。

6.  按一下隱私權連結以檢閱其內容，然後按 [下一步] 。

7.  在 [一般]  頁面指定下列選項，然後按 [下一步] 。

  -   **集合**：指定包含將註冊其行動裝置之使用者的使用者集合。

      > [!NOTE]
      >  如果從集合中移除使用者，則從使用者資料庫中移除使用者記錄時，使用者的裝置將會繼續受到管理達 24 小時。

  -   **公司名稱**：指定您的公司名稱。

  -   **公司隱私權文件的 URL**：如果您將公司隱私權資訊發佈至可從網際網路存取的連結，請提供使用者可以從公司入口網站存取的連結，例如 http://www.contoso.com/CP_privacy.html。 隱私權資訊可釐清使用者與您的公司共用哪些資訊。

  -   **公司入口網站的色彩配置**：您可以選擇變更公司入口網站預設的藍色色彩。

  -   **Configuration Manager 網站碼**：指定主要網站的網站碼，以管理行動裝置。

    > [!NOTE]
    >  變更網站碼只會影響新的註冊項目，不會影響現有已註冊的裝置。

8.  在 [公司連絡資訊] 頁面上，於公司入口網站應用程式的 [連絡 IT]\(Contact IT) 下指定向使用者顯示的公司連絡資訊。 提供您公司的連絡資訊，然後按一下 [下一步]。

9. 在 [公司標誌] 頁面上，您可以選擇是否要在公司入口網站中顯示標誌，然後按一下 [下一步]。

10. 完成精靈。

> [!div class="button"]
[< 上一個步驟](confirm-dns.md)  [下一個步驟 >](terms-and-conditions.md)
