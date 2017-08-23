---
title: "Technical Preview 1610 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1610 版中可用的功能。"
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 59633ce68e2bb2d722900215751f345d6d098721
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1610 中的功能

適用於︰System Center Configuration Manager (Technical Preview)



本文介紹 System Center Configuration Manager Technical Preview 1610 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。      安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>在自動部署規則中依內容大小進行篩選
您現在可以在自動部署規則中依軟體更新的內容大小進行篩選。 例如，您可以將 [內容大小 (KB)] 篩選設定為 [< 2048]，僅下載小於 2MB 的軟體更新。 使用此篩選可防止自動下載大型軟體更新，以在網路頻寬有限時，提供簡化 Windows 下層服務的更佳支援。 如需詳細資訊，請參閱 [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)(Configuration Manager 及下層作業系統上的簡化 Windows 服務)。

#### <a name="to-configure-the-content-size-field"></a>設定內容大小欄位
若要設定 [內容大小 (KB)] 欄位，請在建立 ADR 時移至 [建立自動部署規則精靈] 中的 [軟體更新] 頁面，或移至現有 ADR 內容中的 [軟體更新] 索引標籤。

![內容大小欄位](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>所需軟體對話方塊的功能改善
當使用者收到所需軟體時，可從 [延遲並於此之後再提醒我一次:] 設定的值下拉式清單中進行選取：
- 稍後︰指定通知根據用戶端代理程式設定中所設定的通知設定進行排程。
- 固定時間︰指定通知將排程在選取的時間後再次顯示。 例如，如果使用者選取 30 分鐘，就會在 30 分鐘後再次顯示通知。

![用戶端代理程式設定中的 [電腦代理程式] 頁面](media/computeragentsettings.png)

最大延遲時間一律會以用戶端代理程式設定中每次設定部署時間表時一起設定的通知值會依據。 例如，如果將 [電腦代理程式] 頁面上的設定 [部署期限超過 24 小時，每隔下列時間通知使用者 (小時)] 設定為 10 小時，而且啟動對話方塊時還有 24 小時以上才會超過期限，則最多會有 10 小時 (但永不超過) 對使用者顯示一組延遲選項。 隨著期限將近，對話方塊會顯示愈來愈少的選項，並與部署時間表之每個元件的相關用戶端代理程式設定一致。

此外，針對高風險部署 (例如部署作業系統的工作順序)，現在會採用更入侵式的使用者通知體驗。 每次通知使用者需要重要的軟體維護時，都會在使用者的電腦上顯示類似如下的對話方塊，而不是顯示暫時性工作列通知：

![所需軟體對話方塊](media/requiredsoftwaredialog.png)


詳細資訊：
- [管理高風險部署的設定](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [如何設定用戶端設定](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>拒絕先前核准的應用程式要求

身為系統管理員，您現在可以拒絕先前核准的應用程式要求。 拒絕後，稍後若要安裝此應用程式，使用者必須重新提交要求。 拒絕並不會解除安裝應用程式；而是會強制重新核准來自該使用者對該應用程式的任何新要求。 之前，只能針對尚未核准的應用程式要求執行應用程式要求拒絕動作。

#### <a name="try-it-out"></a>試試看
若要拒絕應用程式核准要求：

1.  在 Configuration Manager 主控台中，[建立和部署需要核准的應用程式](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications)。
2.  在用戶端電腦上，開啟 [軟體中心] 並提交應用程式要求。
3.  在 Configuration Manager 主控台中，核准應用程式要求。
4.  拒絕核准的應用程式要求︰ 在 Configuration Manager 主控台中，巡覽 [軟體程式庫] > [概觀] > [應用程式管理] > [核准要求]，然後選取您要拒絕的應用程式要求。  在功能區中，按一下 [拒絕]。

## <a name="exclude-clients-from-automatic-upgrade"></a>排除自動升級用戶端
Technical Preview 1610 引進新的設定，可讓您用來防止用戶端集合自動安裝更新版用戶端版本。  這適用於自動升級及其他方法，例如以軟體更新為基礎的升級、登入指令碼和群組原則。 這可用於需要在升級用戶端時更小心的電腦集合。 排除集合中的用戶端會略過安裝更新版用戶端軟體的要求。

### <a name="configure-exclusion-from-automatic-upgrade"></a>設定自動升級的排除範圍
若要設定自動升級的排除範圍：
1.  在 Configuration Manager 主控台中，開啟 [系統管理] > [站台設定] > [站台] 下的 [階層設定]，然後選取 [用戶端升級] 索引標籤。
2.  選取 [Exclude specified clients from upgrade]\(排除升級指定的用戶端) 核取方塊，然後針對 [Exclusion collection]\(排除集合)，選取您要排除的集合。 您只能選取單一集合進行排除。
3.  按一下 [確定] 以關閉並儲存設定。 然後，在用戶端更新原則之後，排除集合中的用戶端就不會再自動安裝用戶端軟體的更新。

  ![自動升級的排除範圍設定](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> 雖然使用者介面指出用戶端不會透過任何方法升級，但您可以使用兩種方法來覆寫這些設定。 用戶端推入安裝和手動用戶端安裝可用來覆寫此設定。 如需詳細資訊，請參閱下一節。

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>如何升級排除集合中的用戶端
只要集合設定為要排除，該集合的成員只能透過兩種方法之一覆寫此排除範圍，以升級其用戶端軟體：
 - **用戶端推入安裝** - 您可以使用用戶端推入安裝來升級排除集合中的用戶端。 因為這視為系統管理員的意圖，所以允許這樣做。此方法可讓您升級用戶端，而不需要從排除範圍中移除整個集合。       
 - **手動用戶端安裝** - 您可以使用下列命令列參數搭配 ccmsetup，手動升級排除集合中的用戶端：***/ignoreskipupgrade***

  如果您嘗試手動升級屬於排除集合成員的用戶端，但未使用此參數，則用戶端不會安裝新的用戶端軟體。 如需詳細資訊，請參閱[如何手動安裝 Configuration Manager 用戶端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually)。

如需用戶端安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。

## <a name="windows-defender-configuration-settings"></a>Windows Defender 組態設定

您現在可以使用 Configuration Manager 主控台中的設定項目，在 Intune 註冊的 Windows 10 電腦上設定 Windows Defender 用戶端設定。

具體來說，您可以設定下列 Windows Defender 設定：
- 允許即時監視
- 允許行為監視
- 啟用網路檢查系統
- 掃描所有下載
- 允許指令碼掃描
- 監視檔案和程式活動
  - 監視的檔案
- 追蹤已解決的惡意程式碼天數
- 允許用戶端 UI 存取
- 排程系統掃描
  - 排定的日期
  - 排定的時間
- 排程每日快速掃描
  - 排定的時間
- 掃描期間限制 CPU 使用量 掃描封存檔
- 掃描電子郵件訊息
- 掃描卸除式磁碟機
- 掃描對應的磁碟機
- 掃描從網路共用開啟的檔案
- 簽章更新間隔
- 允許雲端保護
- 提示使用者提交樣本
- 潛在的垃圾應用程式偵測
- 排除的檔案/資料夾
- 排除的檔案副檔名
- 排除的處理程序

> [!NOTE]
> 只有在執行 Windows 10 11 月更新 (1511) 及更新版本的用戶端電腦上，才能設定這些設定。

### <a name="try-it-out"></a>試試看！

1.  在 Configuration Manager 主控台中，移至 [資產與合規性] > [概觀] > [合規性設定] > [設定項目]，然後建立新的**設定項目**。
2.  輸入名稱，然後在 [未以 Configuration Manager 用戶端管理之裝置的設定] 下選取 [Windows 8.1 與 Windows 10]，然後按一下 [下一步]。
3.  確定在 [支援的平台] 頁面上已選取 [所有 Windows 10 (64 位元)] 和 [所有 Windows 10 (32 位元)]，然後按一下 [下一步]。
4.  選取 [Windows Defender] 設定群組，然後按一下 [下一步]。
5.  在此頁面上設定所需的設定，然後按一下 [下一步]。
6.  完成精靈。
7.  將此設定項目新增至設定基準，然後將此基準部署到執行 Windows 10 11 月更新 (1511) 或更新版本的電腦。

> [!NOTE]
> 部署設定基準時，請記得核取 [補救不符合規範的設定] 核取方塊。

## <a name="request-policy-sync-from-administrator-console"></a>從系統管理員主控台要求原則同步

您現在可以從 Configuration Manager 主控台要求行動裝置的原則同步，而不必要求從裝置本身進行同步。 同步要求狀態資訊會以裝置檢視中的新欄位來提供，稱為 [Remote Sync State]\(遠端同步處理狀態)。 每部行動裝置的狀態也會出現在 [內容] 對話方塊的 [探索資料] 區段中。

### <a name="try-it-out"></a>試試看！

1.  在 Configuration Manager 主控台中，移至 [資產與合規性] > [概觀] > [裝置]。
2.  在 [遠端裝置動作] 功能表中，選取 [Send Sync Request]\(傳送同步處理要求)。

同步處理可能需要五到十分鐘。 原則中的任何變更都會同步處理到裝置。 您可以在 [裝置] 檢視的 [Remote Sync State]\(遠端同步處理狀態) 欄中，或在裝置的 [內容] 對話方塊中，追蹤同步處理要求的狀態。

## <a name="additional-security-role-support"></a>其他安全性角色支援

除了系統高權限管理員，下列內建的安全性角色現在也具備 [公司擁有的所有裝置] 節點中項目的完整存取權，包括**預先宣告的裝置**、**iOS 註冊設定檔**，以及 **Windows 註冊設定檔**：•   **資產管理員** •   **公司資源存取管理員**

系統仍會為**唯讀分析師**角色授與 Configuration Manager 主控台中這些區域的唯讀存取權。

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Windows 10 VPN 設定檔的條件存取

您現在可以要求在 Azure Active Directory 中註冊的 Windows 10 裝置必須符合標準，才能透過在 Configuration Manager 主控台中建立的 Windows 10 VPN 設定檔來存取 VPN。 這能夠透過 VPN 設定檔精靈中 [驗證方法] 頁面上新的 [為此 VPN 連線啟用條件存取] 核取方塊以及 Windows 10 VPN 設定檔的 VPN 設定檔內容來進行。 如果您啟用設定檔的條件式存取，您也可以指定不同的憑證來進行單一登入驗證。

## <a name="see-also"></a>另請參閱
[System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)
