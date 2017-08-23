---
title: "軟體更新的必要條件 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中軟體更新的必要條件。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 179f076f228daa5adf612275a822cd379b0ce1e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 軟體更新的必要條件

*適用於：System Center Configuration Manager (最新分支)*

本主題列出 System Center Configuration Manager 中軟體更新的必要條件。 其中每項必要條件的外部相依性和內部相依性分別列在不同表格中。  

## <a name="software-update-dependencies-external-to-configuration-manager"></a>Configuration Manager 軟體更新的外部相依性  
 下列各節列出軟體更新的外部相依性。  

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)  
 站台系統伺服器上必須安裝 Internet Information Services (IIS)，才能執行軟體更新點、管理點和發佈點。 如需詳細資訊，請參閱[站台系統角色的必要條件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 WSUS 是在用戶端上進行軟體更新同步處理和軟體更新相容性評估掃描的必要條件。 必須在建立軟體更新點站台系統角色之前安裝 WSUS 伺服器。 下列版本的 WSUS 支援軟體更新點：  

-   WSUS 4 (Windows Server 2012 和 Windows Server 2012 R2 中的角色)  

-   WSUS 3.2 (Windows Server 2008 R2 中的角色)  

 一個站台上有多個軟體更新點時，請確認所有更新點均執行相同版本的 WSUS。  

> [!WARNING]  
>  從 WSUS 4.0 開始才支援 [升級] 軟體更新分類。 在您同步處理這個新分類並能夠評估 Windows 10 服務計劃中的 Windows 10 電腦前，請務必在您的軟體更新點與站台伺服器上安裝適用於 WSUS 的 [Hotfix 3095113](https://support.microsoft.com/kb/3095113) 。 此 Hotfix 可讓以 Windows Server 2012 或 Windows Server 2012 R2 為基礎之伺服器上的 WSUS 同步並發佈 Windows 10 的功能升級。 如需詳細資訊，請參閱[將 Windows 作為服務管理](../../osd/deploy-use/manage-windows-as-a-service.md)。  
>   
>  如果您在安裝 [Hotfix 3095113](https://support.microsoft.com/kb/3095113)之前以 **[升級]** 分類同步處理軟體更新，請參閱[安裝 KB 3095113 之前從同步處理升級類別復原](#BKMK_RecoverUpgrades)。  

### <a name="wsus-administration-console"></a>WSUS 管理主控台  
 如果軟體更新點位於遠端站台系統伺服器上，且站台伺服器尚未安裝 WSUS，則必須在 Configuration Manager 站台伺服器上安裝 WSUS 管理主控台。  

> [!IMPORTANT]  
>  站台伺服器和軟體更新點必須執行相同版本的 WSUS。  

> [!IMPORTANT]  
>  請勿使用 WSUS 管理主控台進行 WSUS 設定。 Configuration Manager 會連線至軟體更新點上執行的 WSUS 並進行適當的設定。  

### <a name="windows-update-agent-wua"></a>Windows Update 代理程式 (WUA)  
 用戶端上必須要有 WUA 用戶端，才能連線至 WSUS 伺服器並擷取必須進行相容性掃描的軟體更新清單。  

 安裝 Configuration Manager 時，會下載最新版的 WUA。 如果已安裝 Configuration Manager 用戶端，則會在必要時升級 WUA。 不過，如果安裝失敗，則必須使用其他方法升級 WUA。  

## <a name="software-update-dependencies-internal-to-configuration-manager"></a>Configuration Manager 軟體更新的內部相依性  
 下列各節列出 Configuration Manager 中軟體更新的內部相依性。  

### <a name="management-points"></a>管理點  
 管理點會在用戶端電腦與 Configuration Manager 站台之間傳送資訊。 這些管理點是軟體更新的必要條件。  

### <a name="software-update-point"></a>軟體更新點  
 您必須在 WSUS 伺服器上安裝軟體更新點，才能在 Configuration Manager 中部署軟體更新。 如需詳細資訊，請參閱[安裝和設定軟體更新點](../get-started/install-a-software-update-point.md)。

### <a name="distribution-points"></a>發佈點  
 必須要有發佈點，才能儲存軟體更新的內容。 如需安裝發佈點及管理內容之方式的詳細資訊，請參閱[管理內容與內容基礎結構](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="client-settings-for-software-updates"></a>軟體更新的用戶端設定  
 用戶端預設會啟用軟體更新。 不過，還有其他設定可以控制用戶端評估軟體更新相容性的方式和時間，以及控制軟體更新的安裝方式。  

 如需詳細資訊，請參閱下列各項：  

-   [軟體更新的用戶端設定](../get-started/manage-settings-for-software-updates.md#a-namebkmkclientsettingsa-client-settings-for-software-updates)。  

-   [軟體更新用戶端設定](../../core/clients/deploy/about-client-settings.md#software-updates)主題。  

### <a name="reporting-services-point"></a>Reporting Services 點  
 Reporting Services 點站台系統角色可以顯示軟體更新的報告。 這個角色是選用項目，但建議使用。 如需建立 Reporting Services 點之方式的詳細資訊，請參閱[設定報告](../../core/servers/manage/configuring-reporting.md)。  

##  <a name="BKMK_RecoverUpgrades"></a> 安裝 KB 3095113 之前從同步處理升級類別復原  
 在您同步處理 [Hotfix 3095113](https://support.microsoft.com/kb/3095113) Hotfix 3095113 **[升級]** 。 如果在啟用 **[升級]** 分類時並未安裝 Hotfix，WSUS 會尋找 Windows 10 組建 1511 功能升級，即使該升級無法正確下載及部署相關聯套件。 如果您同步處理任何的升級，而沒有先安裝 [Hotfix 3095113](https://support.microsoft.com/kb/3095113)，您將會在 WSUS 資料庫 (SUSDB) 中填入無法使用的資料，必須先清除那些資料才能正確部署升級。  使用下列程序從此問題中復原。  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>從安裝 KB 3095113 之前就同步處理升級分類復原  

1.  刪除使用「升級」分類的軟體更新。 您可以使用類似下列範例指令碼的 PowerShell 指令碼：  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  您必須先在 Configuration Manager 階層的所有軟體更新點上執行該指令碼，再進行下一個步驟。  

     若要大量刪除使用「升級」分類的軟體更新，您可以修改 PowerShell 指令碼來從 txt 檔案讀取多個 GUID。  

2.  取消核取 [軟體更新點元件內容] 中的 [升級] 分類 (如需詳細資訊，請參閱[設定分類和產品](../get-started/configure-classifications-and-products.md))，然後開始軟體更新同步處理 (如需詳細資訊，請參閱[同步處理軟體更新](../get-started/synchronize-software-updates.md)。  

3.  在您的軟體更新點和站台伺服器上安裝適用於 WSUS 的 [Hotfix 3095113](https://support.microsoft.com/kb/3095113) 。  

4.  選取 [軟體更新點元件內容] 中的 [升級] 分類 (如需詳細資訊，請參閱[設定分類和產品](../get-started/configure-classifications-and-products.md))，然後開始軟體更新同步處理 (如需詳細資訊，請參閱[同步處理軟體更新](../get-started/synchronize-software-updates.md)。  

## <a name="next-steps"></a>後續步驟
[準備軟體更新管理](../get-started/prepare-for-software-updates-management.md)
