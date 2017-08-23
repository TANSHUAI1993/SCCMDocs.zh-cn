---
title: "憑證和安全性 | Microsoft Docs"
description: "管理 System Center Updates Publisher 的憑證和安全性"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: c43af95a539a9284e4e49822b284783e02f9fa21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>管理 Updates Publisher 的憑證和安全性

適用於：System Center Configuration Manager (最新分支)

以下程序可協助您設定更新伺服器上的憑證存放區、在用戶端電腦上設定自我簽署憑證，以及設定群組原則以允許電腦上的 Windows Update 代理程式掃描已發行的更新。

## <a name="configure-the-certificate-store-on-the-update-server"></a>設定更新伺服器上的憑證存放區
 Updates Publisher 使用數位憑證來簽署它所發行之目錄中的更新。 在目錄可以發行到更新伺服器之前，該憑證必須位於更新伺服器上的憑證存放區，以及 Updates Publisher 電腦的憑證存放區中 (若該電腦位於更新伺服器的遠端)。

下列程序是將憑證新增到更新伺服器上憑證存放區的其中一種方法。

### <a name="to-configure-the-certificate-store"></a>設定憑證存放區
1.  在可以存取 Updates Publisher 電腦及更新伺服器的電腦上，按一下 [開始]，按一下 [執行]，在文字方塊中輸入 **MMC**，然後按一下 [確定] 以開啟 Microsoft Management Console (MMC)。

2.  依序按一下 [檔案]、[新增/移除嵌入式管理單元]、[新增]、[憑證]、[新增]，選取 [電腦帳戶]，然後按一下 [下一步]。

3.  選取 [另一部電腦]，輸入更新伺服器的名稱，或按一下 [瀏覽] 來尋找更新伺服器電腦，依序按一下 [完成]、[關閉]、[確定]。

4.  依序展開 [憑證 (更新伺服器名稱)]**、[WSUS]，然後按一下 [憑證]。

5.  在結果面板中，以滑鼠右鍵按一下目標憑證，按一下 [所有工作]，然後按一下 [匯出]。

6.  在 [憑證匯出精靈] 中，使用預設設定來以精靈中所指定的名稱和位置建立匯出檔。 繼續下一步之前，更新伺服器必須能存取此檔案。

7.  以滑鼠右鍵按一下 [受信任的發行者]，按一下 [所有工作]，然後按一下 [匯入]。 使用在步驟 6 匯出的檔案來完成 [憑證匯入精靈]。

8.  若使用自我簽署憑證 (例如「WSUS 發行者自我簽署」)，請以滑鼠右鍵按一下 [信任的根憑證授權]，按一下 [所有工作]，然後按一下 [匯入]。 使用在步驟 6 匯出的檔案來完成 [憑證匯入精靈]。

9.  以滑鼠右鍵按一下 [憑證 (更新伺服器名稱)]**，按一下 [連線至另一部電腦]，輸入 Updates Publisher 電腦的電腦名稱，然後按一下 [確定]。

10. 如果 Updates Publisher 位於更新伺服器的遠端，請重複步驟 7 至步驟 9 的動作，以將憑證匯入 Updates Publisher 電腦上的憑證存放區。



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>在用戶端電腦上設定自我簽署憑證
在用戶端電腦上，Windows Update 代理程式 (WUA) 會掃描目錄中的更新。 當代理程式無法在本機電腦上的「受信任的發行者」存放區中找到數位憑證時，此程序將無法安裝更新。 若使用自我簽署憑證 (例如「WSUS 發行者自我簽署」) 來發行更新目錄，則該憑證也必須位於本機電腦的「信任的根憑證授權」憑證存放區中，讓代理程式能驗證該憑證是否有效。

您可以使用數種方法來在用戶端電腦上設定憑證，例如使用群組原則和「憑證匯入精靈」，或使用 Certutil 工具和軟體發佈。

以下提供在用戶端電腦上設定簽署憑證的其中一個範例。

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>在用戶端電腦上設定自我簽署憑證
1.  在可以存取更新伺服器的電腦上，按一下 [開始]，按一下 [執行]，在文字方塊中輸入 **MMC**，然後按一下 [確定] 以開啟 Microsoft Management Console (MMC)。

2.  依序按一下 [檔案]、[新增/移除嵌入式管理單元]、[新增]、[憑證]、[新增]，選取 [電腦帳戶]，然後按一下 [下一步]。

3.  選取 [另一部電腦]，輸入更新伺服器的名稱，或按一下 [瀏覽] 來尋找更新伺服器電腦，依序按一下 [完成]、[關閉]、[確定]。

4.  依序展開 [憑證 (更新伺服器名稱)]**、[WSUS]，然後按一下 [憑證]。

5.  在結果面板中，以滑鼠右鍵按一下憑證，按一下 [所有工作]，然後按一下 [匯出]。 使用預設設定來完成 [憑證匯出精靈]，來以精靈中所指定的名稱和位置建立匯出憑證檔。

6.  使用下列其中一種方法來將簽署更新目錄的憑證，新增到每部會使用 WUA 在目錄中掃描更新的用戶端電腦。 以下列方式在用戶端電腦上新增憑證：

    -   針對自我簽署憑證：將憑證新增到 [信任的根憑證授權] 和 [受信任的發行者] 憑證存放區。

    -   針對憑證授權單位 (CA) 所發行的憑證：將憑證新增到 [受信任的發行者] 憑證存放區。

    > [!NOTE]
    > WUA 也會檢查本機電腦上是否啟用 [允許來自內部網路 Microsoft 更新服務位置的已簽署內容] 群組原則設定。 必須為 WUA 啟用此原則設定，以掃描使用更新發行者建立與發行的更新。 如需啟用此群組原則設定的詳細資訊，請參閱[如何在用戶端電腦上設定群組原則](https://technet.microsoft.com/library/bb530967.aspx(d=robot)。



## <a name="configuring-group-policy-to-allow-wua-on-computers-to-scan-for-published-updates"></a>設定群組原則以允許電腦上的 WUA 掃描已發行的更新。
在電腦上的 Windows Update 代理程式 (WUA) 可以掃描由 Updates Publisher 所建立及發行的更新之前，必須先啟用原則設定，以允許來自內部網路 Microsoft 更新服務位置的已簽署內容。 啟用原則設定之後，若更新是在本機電腦上的 [受信任的發行者] 憑證存放區中簽署，WUA 將接受透過內部網路位置接收的更新。 有數種方法可以在環境中設定電腦上的群組原則。

針對沒有位於網域上的電腦，可以設定登錄機碼設定，以允許來自內部網路 Microsoft 更新服務位置位置的已簽署內容。

以下程序提供基礎步驟，可針對網域上的電腦設定群組原則，以及針對沒有位於網域上的電腦設定登錄機碼。

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>設定群組原則以允許 WUA 掃描已發行的更新
1.  使用具有適當安全性權限以設定群組原則的角色，開啟群組原則物件編輯器 Microsoft Management Console (MMC) 嵌入式管理單元。

2.  按一下 [瀏覽]，並選取連結到已設定群組原則會傳播至目標用戶端電腦之站台的網域、OU 或 GPO。 依序按一下 [確定]、[完成]、[關閉]，然後按一下 [確定]。

3.  在主控台樹狀目錄中展開選取的原則設定，依序展開 [電腦設定]、[系統管理範本] 和 [Windows 元件]，然後按一下 [Windows Update]。

4.  在結果窗格中，以滑鼠右鍵按一下 [允許來自內部網路 Microsoft 更新服務位置的已簽署內容]，再依序按一下 [內容]、[啟用]、[確定]。
