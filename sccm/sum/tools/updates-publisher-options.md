---
title: "設定選項 | Microsoft Docs"
description: "設定使用 System Center Updates Publisher 的選項"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: b66ed0a5e1c87d8c82853da86e3d55b0e2c043bb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-options-for-updates-publisher"></a>設定 Updates Publisher 的選項

*適用於：System Center Updates Publisher*

檢閱與設定會影響 Updates Publisher 作業的選項和相關設定。

若要存取 Updates Publisher 選項，請在主控台左上角按一下 [Updates Publisher 屬性] 索引標籤，然後選擇 [選項]。

![選項](media/properties1.png)   


選項可分為下列類型：

-   更新伺服器
-   ConfigMgr 伺服器
-   Proxy 設定
-   受信任的發行者
-   進階
-   更新
-   記錄

## <a name="update-server"></a>更新伺服器
您必須設定 Updates Publisher 搭配更新伺服器 (例如 Windows Server Update Services (WSUS)) 運作，才能[發行更新](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles)。 這包含指定伺服器、在伺服器位於主控台遠端的情況下連線至該伺服器的方法，以及用來數位簽署您所發行之更新的憑證。

-   **設定更新伺服器**。 當您設定更新伺服器時，請選取 Configuration Manager 階層中最上層的 WSUS 伺服器 (更新伺服器)，來讓所有子站台都能存取您所發行的更新。

  如果您的更新伺服器位於 Updates Publisher 伺服器的遠端，請指定伺服器的完整網域名稱 (FQDN)，以及您是否會透過 SSL 連線。 當您透過 SSL 連線時，預設連接埠會從 8530 變成 8531。 請確定您所設定的連接埠符合您更新伺服器所使用的連接埠。

    > [!TIP]  
    > 如果您沒有設定更新伺服器，則仍然可以使用 Updates Publisher 來撰寫軟體更新。

-   **設定簽署憑證**。 您必須設定並成功連線至更新伺服器，才能設定簽署憑證。

    Updates Publisher 會使用簽署憑證來簽署發行至更新伺服器的軟體更新。 如果更新伺服器的憑證存放區，或執行 Updates Publisher 的電腦中沒有數位憑證，則發行會失敗。

    如需將憑證新增至憑證存放區的詳細資訊，請參閱 [Updates Publisher 的憑證與安全性](/sccm/sum/tools/updates-publisher-security)。

    如果沒有自動偵測到更新伺服器的數位憑證，請選擇下列其中一項：

    -   **瀏覽**：只有在更新伺服器是安裝在執行主控台的伺服器上時，「瀏覽」才可供使用。 選取憑證之後，您必須選擇 [建立] 來將該憑證新增到更新伺服器上的 WSUS 憑證存放區。 針對透過此方法所選取的憑證，您必須輸入 **.pfx** 檔案密碼。

    -   **建立**：使用此選項建立新的憑證。 這也會將憑證新增至更新伺服器上的 WSUS 憑證存放區。

    「如果您建立自己的簽署憑證」，請設定下列各項︰

    -   啟用 [允許匯出私密金鑰] 選項。

    -   設定數位簽章的 [金鑰使用方法]。

    -   將 [最小金鑰大小] 設定為等於或大於 2048 位元的值。

    使用 [移除] 選項從 WSUS 憑證存放區移除憑證。 當更新伺服器位於您所使用之 Updates Publisher 主控台的本機網路上，或當您使用 **SSL** 來連線至遠端更新伺服器時，便可以使用此選項。

## <a name="configmgr-server"></a>ConfigMgr 伺服器
當您搭配 Updates Publisher 使用 Configuration Manager 時，便使用這些選項。

-   **指定 Configuration Manager 伺服器**：在您啟用 Configuration Manager 的支援之後，請指定 Configuration Manager 階層中最上層站台伺服器的位置。 如果該伺服器位於 Updates Publisher 安裝的遠端，請指定站台伺服器的 FQDN。 選擇 [測試連線] 以確定您可以連線到站台伺服器。

-   **設定閾值**：當您使用 [自動] 發行集類型發行更新時，將會使用閾值。 閾值可協助您判斷發行的是更新的完整內容還是中繼資料。 若要深入了解發行集類型，請參閱[將更新指派至發行集](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    您可以使用下列其中一個閾值，或是兩個都啟用：

    -   **要求的用戶端計數閾值**：這會定義在 Updates Publisher 可以自動發行更新的完整內容之前，必須要求更新的用戶端數量。 在有指定數目的用戶端要求更新之前，只會發行更新的中繼資料。

    -   **套件來源大小閾值 (MB)**：這會避免自動發行超出您所指定之大小的更新。 如果更新的大小超過此值，將只會發行中繼資料。 小於指定大小的更新可以發行其完整內容。

## <a name="proxy-settings"></a>Proxy 設定
當您從網際網路匯入軟體目錄，或是將更新發行至網際網路時，Updates Publisher 會使用 Proxy 設定。

-   指定 Proxy 伺服器的 FQDN 或 IP 位址。 支援 IPv4 和 IPv6。

-   如果 Proxy 伺服器會針對網際網路存取驗證使用者，您必須指定 Windows 名稱。 不支援的通用主體名稱 (UPN)。

## <a name="trusted-publishers"></a>受信任的發行者
當您匯入更新目錄時，該目錄的來源 (根據其憑證) 會新增為信任的發行者。 同樣地，當您發行更新時，更新憑證的來源會新增為信任的發行者。

您可以檢視每個發行者的憑證詳細資料，並從信任的發行者清單中移除發行者。

當用戶端搜尋更新時，來自不受信任之發行者的內容可能會危害用戶端電腦。 您應該僅接受來自您所信任之發行者的內容。

## <a name="advanced"></a>進階
進階選項包含下列項目：

-   **存放庫位置**：檢視與修改資料庫檔案 **scupdb.sdf** 的位置。 此檔案是 Updates Publisher 的存放庫。

-   **時間戳記︰**啟用時，會針對您所簽署的更新新增一個可識別其簽署時間的時間戳記。 於憑證有效時簽署的更新，可以在該簽署憑證過期後使用。 根據預設，軟體更新在其簽署憑證過期之後將無法進行部署。

-   **檢查已訂閱目錄的更新**：Updates Publisher 每次啟動時，可以自動檢查您已訂閱的目錄是否有更新。 找到目錄更新時，詳細資料會在 [更新工作區] 的 [概觀] 視窗中，以 [最近的警示] 提供。

-   **憑證撤銷**：選擇此選項以啟用憑證撤銷檢查。

-   **本機來源發行**：Updates Publisher 可以使用您正在發行之更新的本機複本，而不用從網際網路下載該更新。 位置必須是執行 Updates Publisher 之電腦上的資料夾。 根據預設，此位置是 **My Documents\LocalSourcePublishing**。 當您先前已下載一個或多個更新，或已對您想要部署的更新做出變更時，請使用此選項。

-   **軟體更新清理精靈**：啟動更新清理精靈。 精靈會使位於更新伺服器上，但沒有位於 Updates Publisher 存放庫中的更新到期。 如需詳細資料，請參閱[使未參考的更新到期](#expire-unreferenced-software-updates)。

## <a name="updates"></a>更新
 Updates Publisher 可以在每次開啟時自動檢查是否有新的更新。 您也可以選擇加入接收 Updates Publisher 的預覽組建。

若要手動檢查更新，請在 Updates Publisher 主控台中，按一下![屬性](media/properties2.png)  
以開啟 [Updates Publisher 屬性]，然後選擇 [檢查更新]。

在 Updates Publisher 找到新的更新之後，它會顯示 [可用的更新] 視窗，您便可以選擇安裝它。 如果您選擇不安裝該更新，它會在下一次開啟主控台時向您提供。

## <a name="logging"></a>記錄
Updates Publisher 會將有關 Updates Publisher 的基本資訊記錄到 **&lt;*path*&gt;\Windows\Temp\UpdatesPublisher.log**。

使用記事本或 **CMTrace** 來檢視記錄檔。 CMTrace 是 Configuration Manager 記錄檔工具，可在 Configuration Manager 來源媒體的 **\SMSSetup\Tools** 資料夾中找到。

您可以變更記錄檔的大小及其詳細資料層級。

當您啟用資料庫記錄時，會包含針對 Updates Publisher 資料庫所執行之查詢的相關資訊。 使用資料庫記錄可能導致 Updates Publisher 電腦的效能降低。

若要檢視記錄檔，請在主控台中按一下![屬性](media/properties2.png)以開啟 [Updates Publisher 屬性]，然後選擇 [檢視記錄檔]。

## <a name="expire-unreferenced-software-updates"></a>使未參考的軟體更新到期
您可以執行 [軟體更新清理精靈] 來使位於更新伺服器上，但沒有位於 Updates Publisher 存放庫中的更新到期。 這會通知 Configuration Manager，然後 Configuration Manager 會從所有未來的部署中移除那些更新。

使更新到期的動作將無法回復。 請只有在您確定貴組織已不再需要所選取的軟體更新時，才執行此工作。

### <a name="to-remove-expired-software-updates"></a>移除已到期的軟體更新
1.  在 Updates Publisher 主控台中，按一下![屬性](media/properties2.png)以開啟 [Updates Publisher 屬性]，然後選擇 [選項]。

2.  選擇 [進階]，然後在 [軟體更新清除精靈] 下，選擇 [啟動]。

3.  選取您要設為到期的軟體更新，然後選擇 [下一步]。

4.  檢閱您的選取項目之後，選擇 [下一步] 以接受選取項目並將那些更新設為到期。

5.  在精靈完成後，選擇 [關閉] 以完成精靈。
