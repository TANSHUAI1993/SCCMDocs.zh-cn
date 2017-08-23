---
title: "將用戶端指派至站台 | Microsoft Docs"
description: "將用戶端指派給 System Center Configuration Manager 中的站台。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a0ccd453fbe346c239eb6e37bc3ed557487b1e27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-assign-clients-to-a-site-in-system-center-configuration-manager"></a>如何將用戶端指派給 System Center Configuration Manager 中的站台

*適用於：System Center Configuration Manager (最新分支)*

在安裝 System Center Configuration Manager 用戶端之後，必須將用戶端加入 Configuration Manager 主要站台，您才能加以管理。 用戶端所加入的站台即稱為其「指派的站台」。 不可將用戶端指派至管理中心網站或次要站台。  

成功安裝用戶端後便會發生指派程序，並且決定由哪個站台管理用戶端電腦。 您可以直接將用戶端指派至站台或者使用自動站台指派，使用自動站台指派時用戶端會自動根據目前其已針對階層設定的網路位置或後援站台尋找適當的站台。

當您在 Configuration Manager 註冊期間安裝行動裝置用戶端時，一律會自動將裝置指派至站台。 當您在電腦上安裝用戶端時，您可以選擇是否要將用戶端指派至站台。 不過，若安裝用戶端而不指派，則到成功指派站台為止，用戶端都不受管理。  
 

> [!NOTE]  
>  一律將用戶端指派至執行相同 Configuration Manager 版本的站台。 避免將較新版本的 Configuration Manager 用戶端指派至較舊版本的站台。   必要時，將主要站台更新為您在用戶端所使用的相同 Configuration Manager 版本。  

在將用戶端指派至站台後，即使用戶端變更其 IP 位址以及漫遊至其他站台，仍然維持指派至該站台。 只有系統管理員可以手動將用戶端指派至其他站台或者移除用戶端的指派。  

> [!WARNING]  
>  用戶端維持指派至站台的例外狀況，是您在啟用寫入篩選器下在 Windows Embedded 裝置上指派用戶端。 如果您沒有在指派用戶端之前先停用寫入篩選器，用戶端的站台指派狀態會在裝置下一次重新啟動時還原為其原本的狀態。  
>   
>  例如，如果用戶端設定為自動站台指派，則在啟動時用戶端會重新指派並且可能會指派到不同的站台。 如果用戶端未設定為自動站台指派，但是需要手動站台指派，您就必須在啟動後以手動方式重新指派用戶端，才能再次使用 Configuration Manager 管理此用戶端。  
>   
>  若要避免發生此類行為，請先停用寫入篩選器再在 Embedded 裝置上指派用戶端，然後在您確認站台指派成功之後再啟用寫入篩選器。  

如果用戶端指派失敗，用戶端軟體仍維持安裝在上面，但是將不受管理。 當用戶端已安裝但沒有指派至站台，或是指派至站台但無法與管理點通訊時，會被視為不受管理。  

##  <a name="using-manual-site-assignment-for-computers"></a>針對電腦使用手動站台指派  
 您可以使用以下兩種方式將用戶端電腦手動指派至站台：  

-   使用指定站台碼的用戶端安裝內容。  

-   在控制台的 [Configuration Manager] 中指定站台碼。  

> [!NOTE]  
>  如果您手動將用戶端電腦指派至不存在的 Configuration Manager 站台碼，則站台指派將失敗。   

##  <a name="BKMK_AutomaticAssignment"></a> 針對電腦使用自動站台指派  
 自動站台指派可以在用戶端部署期間進行，或者在您按一下控制台中 [Configuration Manager 內容]  的 [進階]  索引標籤上的 [尋找站台]  時進行。 Configuration Manager 用戶端會比對其自身的網路位置與 Configuration Manager 階層中所設定的界限。 當用戶端的網路位置落在已針對站台指派啟用的界限群組內，或者當階層已針對後援站台設定時，用戶端便會自動指派至該站台，您不需要指定站台代碼。  

 您可以使用以下一種或多種方式設定界限：  

-   IP 子網路  

-   Active Directory 站台  

-   IP v6 首碼  

-   IP 位址範圍  

> [!NOTE]  
>  如果 Configuration Manager 用戶端具有多個網路介面卡，便會因此擁有多個 IP 位址，而用來評估用戶端站台指派的 IP 位址是隨機指派的。  

 如需如何針對站台指派設定界限群組以及如何針對自動站台指派設定後援站台的資訊，請參閱 [Define site boundaries and boundary groups for System Center Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。  

 使用自動站台指派的 Configuration Manager 用戶端會嘗試尋找發行至 Active Directory 網域服務的站台界限群組。 如果此方法失敗 (例如 Active Directory 架構沒有針對 Configuration Manager 擴充，或者用戶端是工作群組電腦)，則用戶端可以從管理點取得界限群組資訊。  

 您可以在安裝用戶端時指定用戶端電腦所使用的管理點，或者用戶端可以使用 DNS 發行或 WINS 找出管理點。  

 如果用戶端找不到包含其網路位置的相關界限群組，而階層並沒有後援站台，則用戶端會每 10 分鐘重試一次，直到可以指派至站台為止。  

 如果以下任何情形適用，則 Configuration Manager 用戶端電腦無法自動指派至站台，必須手動指派：  

-   目前已指派至站台。  

-   位在網際網路上，或者設定為僅限網際網路的用戶端。  

-   其網路位置不是落在 Configuration Manager 階層中其中一個已設定的界限群組內，並且階層沒有後援站台。  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>檢查站台相容性以完成站台指派  
 在用戶端找到其指派的站台後，會檢查用戶端的版本和作業系統以確保 Configuration Manager 站台可以管理用戶端。 例如，Configuration Manager 無法管理 Configuration Manager 2007 用戶端、System Center 2012 Configuration Manager 用戶端或執行 Windows 2000 的用戶端。  

 如果您將執行 Windows 2000 的用戶端指派至 Configuration Manager 站台，則站台指派會失敗。 當您將 Configuration Manager 2007 用戶端或 System Center 2012 Configuration Manager 用戶端指派至 Configuration Manager (最新分支) 站台時，站台指派可成功支援自動用戶端升級。 不過，只有將較舊世代的用戶端升級至 Configuration Manager (最新分支) 用戶端之後，Configuration Manager 才能使用用戶端設定、應用程式或軟體更新來管理此用戶端。  

> [!NOTE]  
>  若要支援 Configuration Manager 2007 或 System Center 2012 Configuration Manager 用戶端至 Configuration Manager (最新分支) 站台的站台指派，您必須為階層設定自動用戶端升級。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中升級 Windows 電腦的用戶端](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

Configuration Manager 也會檢查您是否已將 Configuration Manager (最新分支) 用戶端指派至支援的站台。 下列為從舊版 Configuration Manager 移轉期間可能發生的案例。  

-   案例：您已使用自動站台指派，而您的界限與舊版 Configuration Manager 中定義的界限重疊。  

     在此情況下，用戶端會自動嘗試尋找 Configuration Manager (最新分支) 站台。  

     用戶端會先檢查 Active Directory 網域服務，如果找到已發佈的 Configuration Manager (最新分支) 站台，站台指派便會成功。 如果此方法失敗 (例如 Configuration Manager 站台未發佈，或者電腦是工作群組用戶端)，用戶端就會透過其指派的管理點檢查站台資訊。  

    > [!NOTE]  
    >  您可以使用 Client.msi 內容 **SMSMP=&lt;伺服器名稱>**，在用戶端安裝期間將管理點指派至用戶端。  

     如果兩種方法都失敗，則站台指派失敗，並且您必須手動指派用戶端。  

-   案例：您已使用特定站台碼指派 Configuration Manager (最新分支) 用戶端，而非自動站台指派，但是不小心指定了版本比 System Center 2012 R2 Configuration Manager 還舊的 Configuration Manager 站台碼。  

     在此情況下，站台指派會失敗，而您必須手動將用戶端重新指派至 Configuration Manager (最新分支) 站台。  

 必須符合以下條件之一才能檢查站台相容性：  

-   用戶端可以存取已發行至 Active Directory 網域服務的站台資訊。  

-   用戶端可以與站台中的管理點通訊。  

 如果無法成功完成站台的相容性檢查，則站台指派會失敗，而於再次執行站台相容性檢查並且成功之前，用戶端皆不受管理。  

 當用戶端已針對以網際網路為基礎的管理點設定時，會發生執行站台相容性檢查的例外情況。 在此案例中，不會執行站台相容性檢查。 如果您將用戶端指派至含有以網際網路為基礎的站台系統的站台，並且指定以網際網路為基礎的管理點，請確認您是否將用戶端指派至正確的站台。 如果您誤將用戶端指派至 Configuration Manager 2007 站台、System Center 2012 Configuration Manager 站台，或不具有以網際網路為基礎之站台系統角色的 Configuration Manager 站台，用戶端將不受管理。  

##  <a name="locating-management-points"></a>尋找管理點  
 在成功將用戶端指派至站台後，用戶端會找出站台中的管理點。  

 用戶端電腦會下載站台中可連線的管理點清單。 這會在以下情況發生：每次用戶端重新啟動時、每 25 個小時，或用戶端偵測到網路變更 (例如電腦與網路中斷連線再重新連線，或者電腦接收新的 IP 位址) 時。 清單中包括內部網路的管理點，以及是否接受透過 HTTP 或 HTTPS 的用戶端連線。 當用戶端電腦位在網際網路上而還沒有管理點清單時，用戶端會連線至指定的以網際網路為基礎的管理點，以取得管理點清單。 當用戶端具有指派站台的管理點清單時，接著會選取一個要與其連線的管理點：  

-   當用戶端位在內部網路並且具有有效的 PKI 憑證可供使用時，用戶端會在選擇 HTTP 管理點之前先選擇 HTTPS 管理點。 然後再根據其樹系成員資格找出最近的管理點。  

-   當用戶端位在網際網路上時，則會隨機選擇其中一個以網際網路為基礎的管理點。  

Configuration Manager 所註冊的行動裝置用戶端只會連線至其指派站台中的一個管理點，永遠不會連線至次要站台中的管理點。 這些站台一律會透過 HTTPS 連線，而管理點必須設定為接受透過網際網路的用戶端連線。 當行動裝置用戶端在主要站台中有一個以上的管理點時，Configuration Manager 會在指派期間隨機選擇這些管理點之一，而行動裝置用戶端會繼續使用相同的管理點。  

當用戶端已從站台中的管理點下載用戶端原則時，即成為受管理的用戶端。  

##  <a name="downloading-site-settings"></a>下載站台設定  
 在站台指派成功，並且用戶端已找到管理點後，使用 Active Directory 網域服務進行站台相容性檢查的用戶端電腦，會針對其指派站台下載與用戶端相關的站台設定。 這些設定包括用戶端憑證選擇準則、是否要使用憑證撤銷清單以及用戶端要求連接埠號碼。 用戶端會繼續定期檢查這些設定。  

 當用戶端電腦無法從 Active Directory 網域服務取得站台設定時，則會從其管理點下載。 用戶端電腦也可以在使用用戶端推入安裝時取得站台設定，或者您可以透過 CCMSetup.exe 以及用戶端安裝內容以手動方式加以指定。 如需用戶端安裝內容的詳細資訊，請參閱[關於 Configuration Manager 中的用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。  

##  <a name="downloading-client-settings"></a>下載用戶端設定  
 所有的用戶端皆會下載預設的用戶端設定原則，以及任何適用的自訂用戶端設定原則。 軟體中心仰賴 Windows 電腦的這些用戶端設定原則，並且在下載此設定資訊之前，不會通知使用者軟體中心無法成功執行。 視用戶端的設定而定，用戶端設定的初始下載可能需要一點時間，而在此程序完成之前，部分用戶端管理工作可能無法執行。  

##  <a name="verifying-site-assignment"></a>確認站台指派  
 您可以使用下列任何方法以確認站台指派是否成功：  

-   若是 Windows 電腦上的用戶端，請使用控制台中的 Configuration Manager，並確認站台碼正確顯示在 [站台] 索引標籤中。  

-   針對用戶端電腦，請在 [資產與合規性] 工作區 > [裝置] 節點中，確認電腦針對 [用戶端] 欄顯示 [是]，且 [站台碼] 欄顯示的是正確的主要站台碼。  

-   針對行動裝置用戶端，請在 [資產與相容性]  工作區中使用 [所有行動裝置]  集合以確認行動裝置的 [用戶端]  欄顯示 [是]  ，且 [站台碼]  欄顯示正確的主要站台碼。  

-   使用用戶端指派與行動裝置註冊的報告。  

-   針對用戶端電腦，請使用用戶端上的 LocationServices.log 檔案。  

##  <a name="roaming-to-other-sites"></a>漫遊至其他站台  
 若您將內部網路上的用戶端電腦指派至主要站台後，變更其網路位置以將其置於針對另一個站台所設定的界限群組，這些電腦將會漫遊至另一個站台。 若此站台為其指派之站台的次要站台，則用戶端可以使用次要站台中的管理點以下載用戶端原則並上傳用戶端資料，以避免在速度可能較慢的網路上傳送此資料。 但是，如果這些用戶端漫遊至另一個主要站台界限，或是次要站台不是其指派之站台的子系站台，這些用戶端會一律使用其指派站台內的管理點以下載用戶端原則以及上傳資料至其站台。  

 這些漫遊至其他站台 (所有主要站台與所有次要站台) 的用戶端電腦可隨時使用其他站台中的管理點進行內容位置要求。 目前站台中的管理點可提供用戶端一個發佈點清單，其中包含用戶端要求的內容。  

 針對已設為僅限網際網路用戶端管理的用戶端電腦，以及由 Configuration Manager 註冊的行動裝置與 Mac 電腦，這些用戶端只會與指派站台中的管理點通訊。 這些用戶端不會與次要站台內的管理點或是其他主要站台內的管理點進行通訊。  
