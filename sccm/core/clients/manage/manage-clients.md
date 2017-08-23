---
title: "管理用戶端 | Microsoft Docs"
description: "了解如何管理 System Center Configuration Manager 中的用戶端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3a86924b2e5db3ac16eeda78b95ae6747ffd656f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>如何管理 System Center Configuration Manager 中的用戶端

適用於：System Center Configuration Manager (最新分支)

已安裝 System Center Configuration Manager 用戶端且將其順利指派給 Configuration Manager 站台後，您就可以在 [資產與相容性] 工作區的 [裝置] 節點中，以及在 [裝置集合] 節點中的一或多個集合中查看裝置。 當您選取裝置或集合時，可以執行管理操作。 不過，還有其他方法可以管理用戶端，這些方法可能與主控台的其他工作區有關，或與未使用 Configuration Manager 主控台的工作有關。  

> [!NOTE]  
>  Configuration Manager 用戶端可能已安裝，但尚未顯示在 Configuration Manager 主控台中。 如果用戶端尚未順利指派給站台，或是必須重新整理主控台或更新集合成員資格，就會發生此情況。  
>   
>  此外，若尚未安裝 Configuration Manager 用戶端，主控台中可能也會顯示裝置。 如果探索到裝置，但尚未安裝及指派 Configuration Manager 用戶端，就會發生此情況。 利用 Exchange Server 連接器管理的行動裝置，以及由 Microsoft Intune 註冊的裝置，都不會安裝 Configuration Manager 用戶端。  
>   
>  使用 Configuration Manager 主控台的 [用戶端] 欄判斷是否已安裝 Configuration Manager 用戶端，以便從 Configuration Manager 主控台管理該用戶端。  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> 從裝置節點管理用戶端  

請注意，根據不同的裝置類型，某些選項可能無法使用。  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] >  [裝置]。  

3.  選取一或多個裝置，然後從功能區中選取一個用戶端管理工作，或以滑鼠右鍵按一下裝置：  

    -   **管理使用者裝置親和性資訊**  

         設定使用者和裝置間的關聯，讓您有效地部署軟體給使用者。  

         請參閱 [System Center Configuration Manager 的連結使用者和裝置與使用者裝置親和性](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **將裝置新增至新的或現有的集合**  

         透過直接規則將裝置新增至集合。  
         
    -   **使用用戶端推入精靈安裝及重新安裝用戶端**  

         安裝及重新安裝 Configuration Manager 用戶端，以便在執行 Windows 的電腦上修復或重新設定該用戶端。 包括站台設定選項，以及您為用戶端推入安裝所設定的 client.msi 內容。  

        > [!TIP]  
        >  安裝 (及重新安裝) Configuration Manager 用戶端的方式有很多種。 雖然 [用戶端推入精靈] 提供可讓您從主控台方便執行的用戶端安裝方法，但此方法有許多相依性，不適用於所有環境。 如需相依性的詳細資訊，請參閱 [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (在 System Center Configuration Manager 中進行 Windows 用戶端部署的先決條件)。 如需其他用戶端安裝方法的詳細資訊，請參閱 [System Center Configuration Manager 中的用戶端安裝方法](../../../core/clients/deploy/plan/client-installation-methods.md)。  

         請參閱 [如何使用用戶端推入安裝 Configuration Manager 用戶端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。  

    -   **重新指派網站**  

         重新指派一個或多個用戶端 (包括受管理的行動裝置) 到階層中的另一個主要網站。 用戶端可以個別重新指派，也可多選並大量重新指派至新網站。  

    -   **遠端管理用戶端**  

         您可以執行 [資源總管] 查看 Windows 用戶端的硬體和軟體清查資訊，以及使用 [遠端控制]、[遠端協助] 或 [遠端桌面]，從遠端管理該用戶端。  

         請參閱[如何使用資源總管檢視 System Center Configuration Manager 中的硬體清查](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)和[如何使用資源總管檢視 System Center Configuration Manager 的軟體清查](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

         請參閱[如何使用 System Center Configuration Manager 從遠端管理 Windows 用戶端電腦](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)。  

    -   **核准用戶端**  

         當用戶端使用 HTTP 和自我簽署憑證與站台系統通訊時，您必須核准這些用戶端，以便將它們識別為受信任的電腦。 根據預設，網站設定會自動核准相同 Active Directory 樹系和受信任樹系的用戶端，如此就不需要手動核准每個用戶端。 不過，您必須手動核准信任的工作群組電腦，以及信任但未核准的其他電腦。  

        > [!WARNING]  
        >  雖然某些管理功能可用於未核准的用戶端，但 Configuration Manager 不支援此狀況。  

         您不需要核准一律使用 HTTPS 與站台系統通訊的用戶端，用戶端也可以在使用 HTTP 與站台系統通訊時使用 PKI 憑證。 這些用戶端會使用 PKI 憑證建立信任關係。  

    -   **封鎖或解除封鎖用戶端**  

         請封鎖您不再信任的用戶端，以防止該用戶端接收用戶端原則，以及防止 Configuration Manager 站台系統與其通訊。  

        > [!WARNING]  
        >  封鎖用戶端只會防止用戶端與 Configuration Manager 站台系統通訊，不會防止用戶端與其他裝置通訊。 另外，當用戶端使用 HTTP 而非 HTTPS 與網站系統通訊時，則有一些安全性限制。  

         您可以解除封鎖已遭到封鎖的用戶端。 不過，如果您解除封鎖在其遭到封鎖時針對 AMT 佈建的 Intel AMT 型電腦，則您必須先採取額外的步驟，才可以再次管理超出訊號範圍的電腦。  

         請參閱[判斷是否要在 System Center Configuration Manager 中封鎖用戶端](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)。  

    -   **清除必要的 PXE 部署**  

         為電腦重新部署必要的 PXE 部署。  

         請參閱[利用 System Center Configuration Manager 使用 PXE 透過網路來部署 Windows](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)。  

    -   **管理用戶端內容**  

         檢視以用戶端為目標的探索資料和部署。 您也可以設定讓工作順序用於將作業系統部署至裝置的變數。  

    -   **刪除用戶端**  

        > [!WARNING]  
        >  如果您想要解除安裝 Configuration Manager 用戶端，或將該用戶端從集合中移除，請勿刪除該用戶端。  

         藉由 [刪除] 動作可手動將用戶端記錄從 Configuration Manager 資料庫刪除，除非是用於疑難排解，否則您通常不應使用此動作。 如果您刪除用戶端記錄，且仍然安裝用戶端並與 Configuration Manager 通訊，雖然會遺失用戶端歷程記錄和先前的任何關聯，但 [活動訊號探索] 將會重新建立用戶端記錄，且該用戶端記錄將會重新顯示在 Configuration Manager 主控台中。  

        > [!NOTE]  
        >  當您刪除已由 Configuration Manager 註冊的行動裝置用戶端，此動作也會撤銷已發行給行動裝置的 PKI 憑證，此憑證隨後便會遭到管理點的拒絕，即使 IIS 並未檢查 CRL。 當您刪除這些用戶端時，不會撤銷行動裝置舊版用戶端上的憑證。  

         若要解除安裝用戶端，請參閱 [解除安裝 Configuration Manager 用戶端](#BKMK_UninstalClient)。  

         若要將用戶端指派給新的主要站台，請參閱[如何將用戶端指派給 System Center Configuration Manager 中的站台](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

         若要將用戶端從集合中移除，請重新設定集合內容。 請參閱[如何在 System Center Configuration Manager 中管理集合](../../../core/clients/manage/collections/manage-collections.md)。  

    -   **抹除行動裝置**  

         您可以抹除支援抹除命令的行動裝置。  

         此動作會永久移除行動裝置上的所有資料，這些資料包括個人設定和個人資料。 此動作通常會將行動裝置重設回原廠預設值。 當行動裝置已不再受信任時，請抹除該行動裝置，例如裝置遺失或遭到偷竊。  

        > [!TIP]  
        >  如需行動裝置如何處理遠端抹除命令的詳細資訊，請參閱製造商的文件。  

         在行動裝置接收到抹除命令前，通常會有一段延遲時間：  

        -   如果行動裝置是由 Configuration Manager 或 Microsoft Intune 所註冊，用戶端會在下載其用戶端原則時收到此命令。  

        -   如果行動裝置是由 Exchange Server 連接器所管理，則會在與 Exchange 進行同步處理時收到此命令。  

         您可以利用 [抹除狀態] 欄，監視裝置接收抹除命令的時間。 在裝置傳送抹除認可給 Configuration Manager 後，您才可以取消抹除命令。  

    -   **淘汰行動裝置**  

         只有由 Intune 或內部部署行動裝置管理註冊的行動裝置才會支援 [淘汰] 選項。  

         如需詳細資訊，請參閱 [Help protect your data with remote wipe, remote lock, or passcode reset using System Center Configuration Manager (使用 System Center Configuration Manager 透過遠端抹除、遠端鎖定或密碼重設來協助保護您的資料)](../../../mdm/deploy-use/wipe-lock-reset-devices.md)。  

    -   **變更裝置的擁有權**  

         如果裝置未加入網域，且未安裝 Configuration Manager 用戶端，您可以將裝置的擁有權變更為 [公司] 或 [個人]。  

         您可以在應用程式需求中使用這個值來控制部署，以及控制要從使用者裝置收集多少清查。  

        您可能需要以滑鼠右鍵按一下任意欄標題，然後選擇 [裝置擁有者] 欄以將該欄新增至檢視。

         如需詳細資訊，請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)。  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> 從裝置集合節點管理用戶端  
  您可以在 [裝置] 節點中的單一裝置或多部裝置上執行的許多工作，也可以在集合上執行。 這會自動將操作套用到集合中所有合格的裝置。 請注意，這會產生大量的網路封包，以及增加站台伺服器的 CPU 使用量。  

  在您執行集合等級的用戶端管理工作之前，請考慮集合中有多少裝置、這些裝置是否連線到低頻寬的網路連線，以及所有裝置需要多長時間才能完成工作。 一旦啟動，就無法從主控台停止工作。  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>從裝置集合節點管理用戶端  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置集合]。  

3.  選取集合，然後從功能區中選取下列一個用戶端管理工作，或以滑鼠右鍵按一下集合。 這些用戶端管理工作「只能」在集合層級執行。  

    -   **掃描電腦上是否有惡意程式碼，並下載反惡意程式碼定義檔。**  

         請參閱 [System Center Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。  

    -   **部署軟體、設定基準和工作順序。**  

         請參閱：  

        -   [在 System Center Configuration Manager 中部署軟體更新](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [在 System Center Configuration Manager 中規劃和設定相容性設定](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **設定電源管理設定。**  

         請參閱[如何在 System Center Configuration Manager 中建立及套用電源計劃](../../../core/clients/manage/power/create-and-apply-power-plans.md)。 電源計劃只能和執行 Windows 的電腦搭配使用。  

    -   **通知電腦盡快下載原則。**  

         使用用戶端通知來通知選取的 Windows 用戶端盡快在用戶端原則輪詢間隔外下載電腦原則。  

         用戶端通知工作會顯示在 [監視]  工作區的 [用戶端操作]  節點中。  

##  <a name="BKMK_ClientCache"></a> 設定 Configuration Manager 用戶端的用戶端快取  
用戶端快取會儲存用戶端安裝應用程式和程式時所使用的暫存檔案。 軟體更新也可以使用用戶端快取，但是軟體更新不受所設定快取大小的限制，而且將一律嘗試下載至快取。 您可以在手動安裝 Configuration Manager 用戶端時、使用用戶端推入安裝時，或用戶端安裝後，設定用戶端快取設定，例如大小和位置。

從 Configuration Manager 1606 版開始，您可以使用 Configuration Manager 主控台中的用戶端設定來指定快取資料夾的大小。   

 Configuration Manager 用戶端快取的預設位置為 %*windir*%\ccmcache 且預設磁碟空間為 5120 MB。  

> [!IMPORTANT]  
>  請不要加密用戶端快取所使用的資料夾。 Configuration Manager 無法下載內容至加密的資料夾。  

### <a name="about-client-cache"></a>關於用戶端快取  

Configuration Manager 用戶端會在收到部署後隨即下載所需軟體的內容，但是會等到部署排程的時間才執行。 Configuration Manager 用戶端會在排程的時間查看快取中是否有內容。 如果內容是在快取中而且是正確的版本，則用戶端會使用此快取內容。 當所需的內容版本變更，或內容遭到刪除以讓出空間給另一個套件時，內容就會再次下載至快取。  

如果用戶端嘗試下載的程式或應用程式內容超過快取的大小，部署就會因為快取大小不足而失敗，且 Configuration Manager 會產生狀態訊息識別碼 10050。 如果之後快取大小增加，則結果為：  

-   對於必要程式：用戶端不會自動重試下載內容。 您必須重新部署套件及程式至用戶端。  
-   對於必要應用程式：用戶端會在下載其用戶端原則時自動重試下載內容。  

如果用戶端嘗試下載的套件小於快取大小，但快取已滿，則所有必要部署會繼續重試，直到有快取空間可用、下載逾時或達到快取空間失敗的重試限制為止。 如果之後快取大小增加，Configuration Manager 用戶端會在下一個重試間隔期間再次嘗試下載套件。 用戶端每四個小時就會嘗試下載內容，直到嘗試達 18 次。  

用戶端使用快取的內容後，該內容不會自動刪除，而會保留在快取中至少一天。 如果您設定套件內容時，選擇將內容保存在用戶端快取中，用戶端就不會自動從快取中刪除套件內容。 如果用戶端快取空間為過去 24 小時內下載的套件所使用，而用戶端必須下載新套件，您可以增加用戶端快取大小，或選擇刪除選項以刪除保存的快取內容。  

 利用下列程序在手動安裝用戶端期間或用戶端安裝後，設定用戶端快取。  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>若要在使用手動用戶端安裝進行用戶端安裝時，設定用戶端快取  

從安裝來源位置執行 CCMSetup.exe 命令，然後指定下列需要的內容，並以空格分隔：  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > 如果是 1606 版，使用 Configuration Manager 主控台中 [用戶端設定] 的快取大小設定而不是 SMSCACHESIZE。 如需詳細資訊，請參閱 [Client Cache Settings](../../../core/clients/deploy/about-client-settings.md#client-cache-settings) (用戶端快取設定)。

如需如何使用適用於 CCMSetup.exe 之命令列屬性的詳細資訊，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>若要在使用用戶端推入安裝進行用戶端安裝時，設定用戶端快取資料夾  

1.  在 Configuration Manager 主控台中，選擇 [管理] > [站台設定] > [站台]。  

3.  選取適當的站台，然後在 [首頁] 索引標籤的 [設定] 群組中，選擇 [用戶端安裝設定] > [安裝內容] 索引標籤。  

5.  指定下列內容並以空格分隔：  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > 如果是 1606 版，使用 Configuration Manager 主控台中 [用戶端設定] 的快取大小設定而不是 SMSCACHESIZE。 如需詳細資訊，請參閱 [Client Cache Settings](../../../core/clients/deploy/about-client-settings.md#client-cache-settings) (用戶端快取設定)。

       如需如何使用適用於 CCMSetup.exe 之命令列屬性的詳細資訊，請參閱 [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md) (關於 System Center Configuration Manager 中的用戶端安裝內容)。  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>設定用戶端電腦上的用戶端快取資料夾  

1.  在用戶端電腦上瀏覽至 [控制台] 中的 [Configuration Manager]，然後按兩下開啟內容。  

2.  在 [快取] 索引標籤上，設定空間和位置內容。 預設位置為 *%windir%*\ccmcache。  

5.  若要刪除快取資料夾中的檔案，請選擇 [刪除檔案]。  

    > [!NOTE]
    > 
    > 快取資料夾是標準 Windows 資料夾，因此您可以使用指令碼、公用程式或 PowerShell Cmdlet `Remove-Item`，將資料夾內容的刪除作業自動化。 


### <a name="to-configure-client-cache-size-in-client-settings"></a>在用戶端設定中設定用戶端快取大小

從 1606 版開始，您可以調整用戶端快取資料夾的大小而不需要重新安裝用戶端。 若要完成這項動作，您可以在 Configuration Manager 主控台中使用用戶端設定，以設定用戶端快取大小。  

1. 在 Configuration Manager 主控台中，移至 **[系統管理]** > **[用戶端設定]**。

2. 按兩下 **[預設用戶端設定]**。
  您也可以建立自訂用戶端設定，以更有選擇性地套用快取大小。 如需預設和自訂用戶端設定的詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md)。

 3. 選擇 [用戶端快取設定]，針對 [設定用戶端快取大小] 選擇 [是]，然後使用 [MB] 或 [磁碟百分比] 設定。 快取可以調整為任何較小的大小。

     在下載下一個用戶端原則時，Configuration Manager 用戶端會使用這些設定以設定快取大小。

##  <a name="BKMK_UninstalClient"></a> 解除安裝 Configuration Manager 用戶端  
 您可以使用 **CCMSetup.exe** 搭配 **/Uninstall** 內容，從電腦中解除安裝 Windows Configuration Manager 用戶端軟體。 在個別電腦上的命令提示字元中執行 CCMSetup.exe，或部署套件和程式來解除安裝一組電腦集合的用戶端。  

> [!WARNING]  
>  您無法從行動裝置解除安裝 Configuration Manager 用戶端。 如果您必須從行動裝置移除 Configuration Manager 用戶端，則必須抹除裝置，這樣會刪除行動裝置上的所有資料。  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>若要從命令提示字元解除安裝 Configuration Manager 用戶端  

1.  開啟 Windows 命令提示字元，並將資料夾變更至 CCMSetup.exe 所在的位置。  

2.  輸入 **Ccmsetup.exe /uninstall**，然後按 **Enter**。  

> [!NOTE]  
>  解除安裝程序不會在畫面上顯示任何結果。 若要確認用戶端解除安裝成功，請查看用戶端電腦上 *%windir%\ ccmsetup* 資料夾中的記錄檔 **CCMSetup.log**。  

##  <a name="BKMK_ConflictingRecords"></a> 管理 Configuration Manager 用戶端的衝突記錄  
 Configuration Manager 會使用硬體識別碼嘗試識別可能重複的用戶端，並發出衝突記錄的警示。 例如，如果您重新安裝電腦，硬體識別碼會相同，但 Configuration Manager 使用的 GUID 可能會變更。  

 當 Configuration Manager 可以使用電腦帳戶的 Windows 驗證或來自受信任來源的 PKI 憑證解決衝突時，即會自動解決衝突。 不過，若 Configuration Manager 無法解決衝突，則會使用階層設定，在偵測到重複的硬體識別碼時自動合併記錄 (預設設定)，或是讓您決定何時合併、封鎖或建立新的用戶端記錄。 如果您決定手動管理重複的記錄，則必須在 Configuration Manager 主控台中手動解決衝突的記錄。  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>若要變更管理衝突記錄的階層設定  

1.  在 Configuration Manager 主控台中，選擇 [管理] > [站台設定] > [站台] > [階層設定]
2.  在 [用戶端核准和衝突的記錄] 索引標籤上，選擇 [自動解決衝突的記錄] 或 [手動解決衝突的記錄]。  

#### <a name="to-manually-resolve-conflicting-records"></a>若要手動解決衝突的記錄  

1.  在 Configuration Manager 主控台中，選擇 [監視] > [系統狀態] > [衝突的記錄]。  

3.  選取一或多個衝突的記錄，然後選擇 [衝突的記錄]。  

4.  選取下列其中一項：  

    -   [合併] 會將新偵測到的記錄與現有用戶端記錄結合。  

    -   [新增] 會為衝突的用戶端記錄建立新記錄。  

    -   [封鎖] 會為衝突的用戶端記錄建立新記錄，但會將它標示為已封鎖。  

## <a name="manage-duplicate-hardware-identifiers"></a>管理重複的硬體識別碼
從 Configuration Manager 1610 版開始，您可以提供一份硬體識別碼清單，讓 Configuration Manager 在 PXE 開機及用戶端註冊時略過這些識別碼。 這麼做有助於解決下列兩個常見的問題。

1. 許多新的裝置 (如 Surface Pro 3) 不包括內建的乙太網路連接埠。 USB 至乙太網路介面卡通常用來建立作業系統部署的有線連線。 不過，基於成本和一般使用性的考量，這通常是共用介面卡。 而該介面卡的 MAC 位址是用來識別裝置，因此每個部署之間，如果沒有額外的系統管理員動作，重複使用介面卡就會產生問題。 從 1610 版開始，您可以排除這張介面卡的 MAC 位址，以在這種情況下重複使用介面卡。
2. SMBIOS 識別碼應該是唯一的硬體識別碼，但有些專用硬體裝置會建置重複的識別碼。 雖然這種情況不像上述 USB 至乙太網路介面卡的案例那麼常見，但硬體識別碼清單亦可用來解決此問題。

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>若要新增 Configuration Manager 要略過的硬體識別碼  
1. 在 Configuration Manager 主控台中，移至 [管理] > [概觀] > [站台設定] > [站台]。
2. 在 [首頁] 索引標籤的 [站台] 群組中，選擇 [階層設定]。
3. 在 [用戶端核准和衝突的記錄] 索引標籤的 [Duplicate hardware identifiers]\(重複的硬體識別碼) 區段中，選擇 [新增] 新增硬體識別碼。

##  <a name="BKMK_PolicyRetrieval"></a> 起始 Configuration Manager 用戶端的原則抓取  
 Windows Configuration Manager 用戶端會依照您設定的排程 (用戶端設定) 下載其用戶端原則。 不過，有時候您可能想要從用戶端起始臨機操作原則抓取，例如用於疑難排解或測試。  

您可以使用下列方法來起始原則抓取：


- [用戶端通知](#initiate-client-policy-retrieval-using-client-notification) 
- [用戶端上的 [動作] 索引標籤](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [指令碼](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  如需執行 Linux 和 UNIX 之用戶端原則抓取的資訊，請參閱 [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU)。  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>使用用戶端通知起始用戶端原則抓取  

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [裝置集合]。  

3.  選取包含您要下載原則之電腦的裝置集合。 在 [首頁] 索引標籤的 [集合] 群組中，選擇 [用戶端通知] > [下載電腦原則]。  

    > [!NOTE]  
    >  您也可以使用用戶端通知，針對 [裝置]  節點下暫時集合節點中顯示的一個或多個所選取裝置起始原則抓取。  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>在 Configuration Manager 用戶端的 [動作] 索引標籤上手動起始用戶端原則抓取  

1.  在電腦的 [控制台] 中選取 [Configuration Manager]  。  

2.  在 [動作] 索引標籤上，選擇 [電腦原則抓取和評估週期] 起始電腦原則，然後選擇 [立即執行]。  

4.  選擇 [確定] 確認提示。  

5.  針對您需要的任何其他動作重複步驟 3 和 4，例如，使用者用戶端設定的 **[使用者原則抓取和評估週期]**。  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>使用指令碼手動起始用戶端原則抓取  

1.  開啟文字編輯器，例如 [記事本]。  

2.  複製下列內容並插入檔案中：  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  以副檔名 .vbs 儲存檔案。  

4.  在用戶端電腦上，使用下列其中一種方法執行檔案：  

    -   使用 Windows 檔案總管瀏覽至檔案，然後按兩下指令碼檔案。  

    -   開啟命令提示字元，然後輸入：**cscript &lt;路徑\檔案名稱.vbs>**。  

5.  在 [Windows Script Host] 對話方塊中，選擇 [確定]。  
