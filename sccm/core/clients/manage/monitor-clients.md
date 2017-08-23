---
title: "監視用戶端 - Configuration Manager | Microsoft Docs"
description: "取得如何在 System Center Configuration Manager 中監視用戶端的詳細指引。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: "23"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 08a4d9b29871b49e3118aef949572cef64940f96
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中監視用戶端

*適用於：System Center Configuration Manager (最新分支)*


 在您站台的 Windows 電腦和裝置上安裝 System Center Configuration Manager 用戶端應用程式之後，即可在 Configuration Manager 主控台中監視其健康情況和活動。  

##  <a name="bkmk_about"></a> 關於用戶端狀態  
 Configuration Manager 提供下列類型的資訊作為用戶端狀態：  

-   **用戶端線上狀態** - 從 Configuration Manager 1602 版開始，此狀態指出電腦是否在線上。 當電腦已連線到受指派的管理點時，就會被視為在線上。  為了表示用戶端在線上，它會傳送類似 Ping 的訊息給管理點。 如果管理點在 5 分鐘左右未收到訊息，該用戶端就會被視為離線。  

-   **用戶端活動** - 此狀態指出用戶端在過去 7 天是否積極使用 Configuration Manager。 如果用戶端在 7 天內未要求原則更新、傳送活動訊號訊息或傳送硬體清查，就會被視為非作用中。  

-   **用戶端檢查** - 此狀態指出 Configuration Manager 用戶端在電腦上執行的定期評估是否成功。  此評估會檢查電腦，並且可以修復它所發現的部分問題。 如需詳細資訊，請參閱 [Checks and remediations made by client check](#BKMK_ClientHealth)(由用戶端檢查所進行的檢查與補救)。  

     在執行 Windows 7 的電腦上，用戶端檢查會做為排定的工作執行。 在更新版本的作業系統上，用戶端檢查會在 Windows 維護期間自動執行。  

     您可以設定不在特定電腦上執行補救，例如攸關業務的伺服器。 此外，若有其他想要評估的項目，您可以使用 Configuration Manager 相容性設定來提供全面的解決方案，以監視組織中電腦的整體健全狀況、活動和相容性。 如需相容性設定的詳細資訊，請參閱[在 System Center Configuration Manager 中規劃和設定相容性設定](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

##  <a name="bkmk_indStatus"></a> 監視個別用戶端的狀態  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [裝置] 或在 [裝置集合] 底下選擇一個集合。  

     從 Configuration Manager 1602 版開始，每個資料列開頭的圖示都會指出裝置的線上狀態︰  

    |||  
    |-|-|  
    |![用戶端的線上狀態圖示](../../../core/clients/manage/media/online-status-icon.png)|裝置在線上。|  
    |![用戶端的離線狀態圖示](../../../core/clients/manage/media/offline-status-icon.png)|裝置已離線。|  
    |![用戶端的未知狀態圖示](../../../core/clients/manage/media/unknown-status-icon.png)|線上狀態不明。|  
    |![未安裝用戶端](../../../core/clients/manage/media/client-not-installed.png)|用戶端未安裝在裝置上。|  

2.  如需更詳細的線上狀態，只要在欄標題上按一下滑鼠右鍵，然後按一下您想要新增的線上狀態欄位，即可將用戶端線上狀態資訊新增到裝置檢視。 您可以新增的欄包括  

    -   **裝置線上狀態** 指出用戶端目前在線上還是離線。 (此資訊與圖示所提供的相同)。  

    -   **上次上線時間** ：指出用戶端線上狀態變更為線上的時間。  

    -   **上次離線時間** ：指出狀態變更為離線的時間。  

3.  按一下清單窗格中的個別用戶端，即可在詳細資料窗格中看到更多狀態，包括用戶端活動及用戶端檢查的相關資訊。  

##  <a name="bkmk_allStatus"></a> 監視所有用戶端的狀態  

1.  在 Configuration Manager 主控台中，按一下 [監視] > [用戶端狀態]。 在主控台的這個頁面上，您可以檢閱整個站台的用戶端活動和用戶端檢查的整體統計資料。  您也可以選擇不同的集合來變更資訊的範圍。  

2.  若要向下切入到所回報之統計資料的詳細資料，請按一下所回報資訊的名稱 (例如 [通過用戶端檢查或沒有結果的使用中用戶端])，然後檢閱個別用戶端的相關資訊。  

3.  按一下 [用戶端活動] 以查看描述您 Configuration Manager 站台中用戶端活動的圖表。  

4.  按一下 [用戶端檢查] 以查看描述您 Configuration Manager 站台中用戶端狀態的圖表。  

 您可以設定警示，以便在用戶端檢查結果或用戶端活動低於集合中指定的百分比，或在指定百分比的用戶端上進行補救失敗時，發出通知。 如需如何設定用戶端狀態的資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端狀態](../../../core/clients/deploy/configure-client-status.md)。  

##  <a name="BKMK_ClientHealth"></a> 依照用戶端檢查進行檢查及補救  
 下列檢查和補救可以由用戶端檢查來執行。  

|用戶端檢查|補救動作|詳細資訊|  
|------------------|------------------------|----------------------|  
|確認最近有執行用戶端檢查|執行用戶端檢查|確認過去三天內是否至少執行一次用戶端檢查。|  
|確認已安裝用戶端必要條件|安裝用戶端必要條件|確認是否已安裝用戶端必要條件。 閱讀用戶端安裝資料夾中的檔案 ccmsetup.xml，以探索必要條件。|  
|WMI 存放庫完整性測試|重新安裝 Configuration Manager 用戶端|確認 Configuration Manager 用戶端項目是否存在於 WMI 中。|  
|確認用戶端服務正在執行|啟動用戶端 (SMS Agent Host) 服務|沒有其他資訊|  
|WMI 事件接收測試。|重新啟動用戶端服務|確認是否遺失 Configuration Manager 相關 WMI 事件接收測試|  
|確認 Windows Management Instrumentation (WMI) 服務已存在|沒有補救措施|沒有其他資訊|  
|確認已正確安裝用戶端|重新安裝用戶端|沒有其他資訊|  
|WMI 存放庫讀取和寫入測試|重設 WMI 存放庫，並重新安裝 Configuration Manager 用戶端|此用戶端檢查的補救，只會在執行 Windows Server 2003、Windows XP (64 位元) 或更舊版本的電腦上執行。|  
|確認反惡意程式碼服務啟動類型為自動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認反惡意程式碼端服務正在執行|啟動反惡意程式碼服務|沒有其他資訊|  
|確認 Windows Update 服務啟動類型為自動或手動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認用戶端服務 (SMS Agent Host) 啟動類型為自動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認 Windows Management Instrumentation (WMI) 服務正在執行。|啟動 Windows Management Instrumentation 服務|沒有其他資訊|  
|確認 Microsoft SQL CE 資料庫是否狀況良好|重新安裝 Configuration Manager 用戶端|沒有其他資訊|  
|Microsoft Policy Platform WMI 完整性測試|修復 Microsoft Policy Platform|沒有其他資訊|  
|確認 Microsoft Policy Platform 服務存在|修復 Microsoft Policy Platform|沒有其他資訊|  
|確認 Microsoft Policy Platform 服務啟動類型為手動。|將服務啟動類型重設為手動|沒有其他資訊|  
|確認背景智慧型傳送服務已存在|沒有補救措施|沒有其他資訊|  
|確認背景智慧型傳送服務啟動類型為自動或手動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認網路檢查服務啟動類型為手動|將服務啟動類型重設為手動 (如果已安裝)|沒有其他資訊|  
|確認 Windows Management Instrumentation (WMI) 服務啟動類型為自動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認 Windows Update 服務在 Windows 8 電腦上的啟動類型為自動或手動|將服務啟動類型重設為手動|沒有其他資訊|  
|確認用戶端 (SMS Agent Host) 服務是否存在。|沒有補救措施|沒有其他資訊|  
|確認 Configuration Manager 遠端控制服務啟動類型為自動或手動|將服務啟動類型重設為自動|沒有其他資訊|  
|確認 Configuration Manager 遠端控制服務正在執行|啟動遠端控制服務|沒有其他資訊|  
|確認用戶端 WMI 提供者狀況良好|重新啟動 Windows Management Instrumentation 服務|此用戶端檢查的補救措施僅適用於執行 Windows Server 2003、Windows XP (64 位元) 或更早版本的電腦。|  
|確認喚醒 Proxy 服務 (ConfigMgr Wake-up Proxy) 正在執行|啟動 ConfigMgr Wakeup Proxy 服務|此用戶端檢查只有在支援的作業系統上的 [電源管理] ：[啟用喚醒 Proxy]  用戶端設定已設為 [是]  時才能進行。|  
|確認喚醒 Proxy 服務 (ConfigMgr Wake-up Proxy) 啟動類型為自動|將 ConfigMgr Wakeup Proxy 服務啟動類型重設為自動|此用戶端檢查只有在支援的作業系統上的 [電源管理] ：[啟用喚醒 Proxy]  用戶端設定已設為 [是]  時才能進行。|  

## <a name="client-deployment-log-files"></a>用戶端部署記錄檔
如需用戶端部署及管理作業所使用之記錄檔的相關資訊，請參閱 [System Center Configuration Manager 中的記錄檔](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)。
