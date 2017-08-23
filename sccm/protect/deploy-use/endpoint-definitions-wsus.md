---
title: "來自 WSUS 的 Endpoint Protection 惡意程式碼定義 | Microsoft Docs"
definition: Learn how to configure Windows Server Updates Services to auto-approve definition updates.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 0e606b25065fa25c782d1b5f3fbf164e60733353
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>啟用 Endpoint Protection 惡意程式碼定義，從 Windows Server Update Services (WSUS) 針對 Configuration Manager 下載

*適用於：System Center Configuration Manager (最新分支)*

 如果您使用 WSUS 將反惡意程式碼定義維持在最新狀態，則您可以將其設定為自動核准定義更新。 雖然建議您使用 Configuration Manager 軟體更新來將定義維持在最新狀態，但您也可以設定 WSUS，將其作為允許使用者手動起始已更新定義的方法。 使用下列程序將 WSUS 設定為定義更新來源。

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>同步處理 Configuration Manager 軟體更新中的 Endpoint Protection 定義更新

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 [系統管理]  工作區中，展開 [網站設定] ，然後按一下 [網站] 。

3.  選取包含軟體更新點的網站。 在 [設定]  群組中，依序按一下 [設定站台元件] 和 [軟體更新點] 。

4.  在 [軟體更新點元件內容]  對話方塊的 [分類]  索引標籤上，選取 [定義更新]  核取方塊。

5.  指定使用 WSUS 進行更新的 **產品** ：

    -   針對 Windows 8.1 及更早版本，在 [軟體更新點元件內容]  對話方塊的 [產品]  索引標籤上，選取 [Forefront Endpoint Protection 2010]  核取方塊。

    -   針對 Windows 10 及更新版本，在 [軟體更新點元件內容]  對話方塊的 [產品]  索引標籤上，選取 [Windows Defender]  及 [Windows Technical Preview 2]  核取方塊。

6.  按一下 [確定]  關閉 [軟體更新點元件內容]  對話方塊。

 當您的 WSUS 伺服器尚未整合至 Configuration Manager 環境時，使用下列程序設定 Endpoint Protection 更新。

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>同步處理獨立 WSUS 中的 Endpoint Protection 定義更新

1.  在 WSUS 管理主控台中，展開 [電腦] ，按一下 [選項] ，然後按一下 [產品和分類] 。

2.  指定使用 WSUS 進行更新的 **產品** ：

    -   針對 Windows 8.1 及更早版本，在 [軟體更新點元件內容]  對話方塊的 [產品]  索引標籤上，選取 [Forefront Endpoint Protection 2010]  核取方塊。

    -   針對 Windows 10 及更新版本，在 [軟體更新點元件內容]  對話方塊的 [產品]  索引標籤上，選取 [Windows Defender]  及 [Windows Technical Preview 2]  核取方塊。

3.  在 [產品和分類]  對話方塊的 [分類]  索引標籤上，選取 [定義更新]  及 [更新]  核取方塊。

## <a name="approving-definition-updates"></a>核准定義更新
 Endpoint Protection 定義更新必須經核准並下載至 WSUS 伺服器，才能將其提供給要求可用更新清單的用戶端。 用戶端連線至 WSUS 伺服器，以檢查適用的更新，然後要求最新已核准的定義更新。

### <a name="to-approve-definitions-and-updates-in-wsus"></a>核准 WSUS 中的定義和更新

1.  在 WSUS 管理主控台中，按一下 [更新] ，然後按一下 [所有更新]  或想要核准的更新分類。

2.  在更新清單中，以滑鼠右鍵按一下更新或想要核准安裝的更新，然後按一下 [核准] 。

3.  在 [核准更新]  對話方塊中，選取您要核准更新的電腦群組，然後按一下 [已核准安裝] 。

 除了手動核准，您也可以設定定義更新及 Endpoint Protection 更新的自動核准規則。 這會將 WSUS 設定為自動核准由 WSUS 下載 Endpoint Protection 定義更新。

### <a name="to-configure-an-automatic-approval-rule"></a>設定自動核准規則

1.  在 WSUS 管理主控台中，按一下 [選項] ，然後按一下 [自動核准] 。

2.  在 [更新規則]  索引標籤上，按一下 [新增規則] 。

3.  在 [步驟 1：選取屬性]  下的 [新增規則] 對話方塊中，選取 [當更新在某個特定分類中時]  核取方塊。

4.  在 [步驟 2：編輯屬性] 下，按一下 [任何分類] 。

5.  清除 [定義更新] 以外的所有核取方塊，然後按一下 [確定] 。

6.  在 [步驟 1：選取屬性]  下的 [新增規則] 對話方塊中，選取 [當更新在某個特定產品中時]  核取方塊。

7.  在 [步驟 2：編輯屬性] 下，按一下 [任何產品] 。

8.  針對 Windows 8.1 及更早版本清除 [Forefront Endpoint Protection]  以外的所有核取方塊，或針對 Windows 10 及更新版本清除 [Windows Defender]  以外的所有核取方塊，然後按一下 [確定] 。

9. 在 [步驟 3：指定名稱] 下，輸入規則的名稱，然後按一下 [確定] 。

10. 在 [自動核准]  對話方塊中，選取新建立規則的核取方塊，然後按一下 [執行規則] 。

> [!NOTE]
>  若要在 WSUS 伺服器和用戶端電腦上達到最佳效能，請拒絕舊的定義更新。 若要完成這項工作，您可以設定修訂自動核准及自動拒絕已過期的更新。 如需詳細資訊，請參閱 [Microsoft 知識庫文章 938947](http://go.microsoft.com/fwlink/p/?LinkId=204078)。

> [!div class="button"]
[下一步 >](endpoint-antimalware-policies.md)

> [!div class="button"]
[上一步 >](endpoint-configure-alerts.md)
