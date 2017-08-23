---
title: "Endpoint Protection 保護電腦免受惡意程式碼威脅的案例 | Microsoft Docs"
description: "了解如何在 Configuration Manager 中實作 Endpoint Protection，以保護電腦免受惡意程式碼的攻擊。"
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b98684d44874ff246e4d675039c6e443aee82a62
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="example-scenario-using-system-center-endpoint-protection-to-protect-computers-from-malware-in-system-center-configuration-manager"></a>範例案例: 使用 System Center Endpoint Protection 保護電腦免受 System Center Configuration Manager 中惡意程式碼的威脅

適用於：System Center Configuration Manager (最新分支)

此主題提供一個範例案例，示範如何在 Configuration Manager 中實作 Endpoint Protection 以保護組織的電腦免受惡意程式碼攻擊。  

 John 是 Woodgrove Bank 的 Configuration Manager 系統管理員。 該銀行目前使用 System Center Endpoint Protection 保護電腦，以防範惡意程式碼的攻擊。 此外，該銀行也使用 Windows 群組原則以確保公司內的所有電腦上皆已啟用 Windows 防火牆，且當 Windows 防火牆阻擋新程式時通知使用者。  

 因此，銀行要求 John 將 Woodgrove Bank 的反惡意程式碼軟體升級為 System Center Endpoint Protection，以便受益於最新的反惡意程式碼功能，同時透過 Configuration Manager 主控台來集中管理反惡意程式碼解決方案。 進行這項作業有下列需求：  

-   使用 Configuration Manager 來管理目前由群組原則所管理的 Windows 防火牆設定。  

-   使用 Configuration Manager 軟體，將惡意程式碼定義下載至電腦。 如果無法使用軟體更新，例如，如果電腦未連線到公司網路時，電腦就必須從 Microsoft Update 下載定義更新。  

-   使用者的電腦必須每天執行惡意程式碼的快速掃描。 但伺服器則必須於工作時間以外的星期六上午 1 點，執行完整的掃描。  

-   每次發生下列任一事件時，即傳送電子郵件警示：  

    -   在任何電腦上偵測到惡意程式碼  

    -   超過 5% 以上的電腦上偵測到相同的惡意程式碼威脅  

    -   在任何 24 小時的期間內偵測到 5 次以上相同的惡意程式碼威脅  

    -   在任何 24 小時期間內偵測到 3 種以上不同類型的惡意程式碼  

-   解除安裝現有的反惡意程式碼解決方案。  

 John 接著執行下列步驟來實作 Endpoint Protection：  

##  <a name="steps-to-implement-endpoint-protection"></a>若要實作 Endpoint Protection 的步驟  

|程序|參考|  
|-------------|---------------|  
|John 檢閱 Configuration Manager 中 Endpoint Protection 基本概念的相關可用資訊。|如需 Endpoint Protection 的概觀資訊，請參閱 [System Center Configuration Manager 中的 Endpoint Protection](endpoint-protection.md)。|  
|John 檢閱使用 Endpoint Protection 的必要先決條件並進行實作。|如需 Endpoint Protection 先決條件的詳細資訊，請參閱 [Endpoint Protection 規劃](../plan-design/planning-for-endpoint-protection.md)。|  
|John 只在 Woodgrove Bank 階層頂端的一個站台系統伺服器上，安裝了 Endpoint Protection 站台系統角色。|如需如何安裝 Endpoint Protection 站台系統角色的詳細資訊，請參閱[設定 Endpoint Protection](configure-endpoint-protection.md) 中的＜先決條件＞。|  
|John 會將 Configuration Manager 設定為使用 SMTP 伺服器傳送電子郵件警示。<br /><br /> **注意：**僅有當您想要在產生 Endpoint Protection 警示時收到電子郵件通知的情況下，才必須設定 SMTP 伺服器。|如需詳細資訊，請參閱[設定 Endpoint Protection 警示](endpoint-configure-alerts.md)。|  
|John 會建立一個裝置集合，其中包含所有電腦與伺服器，以安裝 Endpoint Protection 用戶端。 他將此集合命名為 [Endpoint Protection 保護的所有電腦]。<br /><br /> **提示︰**您無法設定使用者集合的警示。|如需如何建立集合的詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../core/clients/manage/collections/create-collections.md)。|  
|他會設定下列警示集合： <br /><br />1) **偵測到惡意程式碼**：針對此情況，John 會設定「嚴重」的警示嚴重性。 <br /><br />2) **數台電腦上偵測到相同類型的惡意程式碼**：針對此情況，John 會設定「嚴重」的警示嚴重性，並指定當超過 5% 的電腦有偵測到惡意程式碼就會產生警示。 <br /><br />3) **某台電腦在指定的間隔內重複偵測到相同類型的惡意程式碼**：針對此情況，John 會設定「嚴重」的警示嚴重性，並指定當 24 小時內偵測到 5 次以上的惡意程式碼就會產生警示。 <br /><br />4) **某台電腦在指定的間隔內偵測到多種類型的惡意程式碼**：針對此情況，John 會設定「嚴重」的警示嚴重性，並指定當 24 小時內產生 3 種以上的惡意程式碼類型時就會產生警示。<br /><br /> **警示嚴重性**的值表示在 Configuration Manager 主控台中會顯示的警示等級，以及 John 在電子郵件訊息中會收到的警示等級。<br /><br /> John 還另外選取了 [在 Endpoint Protection 儀表板中檢視此集合] 選項，以便在 Configuration Manager 主控台中監視警示。|請參閱[設定 System Center Configuration Manager 中的 Endpoint Protection](endpoint-configure-alerts.md) 之＜設定 Endpoint Protection 的警示＞。|  
|John 還使用自動部署規則，將 Configuration Manager 軟體更新設定為每天下載及部署 3 次定義更新。|如需詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Endpoint Protection](endpoint-definitions-configmgr.md) 之＜使用 Configuration Manager 軟體更新來傳遞定義更新＞一節。|  
|John 會檢查預設反惡意程式碼原則中的設定，其中包含來自 Microsoft 所建議的安全性設定。 對於每天皆會執行快速掃描的電腦，他變更了下列設定：<br /><br /> 1) **在用戶端電腦上執行每日快速掃描**：**是**。<br /><br /> 2) **每日快速掃描排程時間**：**上午 9 點**。<br /><br /> John 注意到預設已選取 [從 Microsoft Update 發佈的更新]  作為定義更新的來源。 如此一來，當電腦無法收到 Configuration Manager 軟體更新時，即可從 Microsoft Update 下載定義，以滿足業務需求。|請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。|  
|John 建立了一個集合，只包含名稱為 **Woodgrove Bank 伺服器**的 Woodgrove Bank 伺服器。|請參閱[如何在 System Center Configuration Manager 中建立集合](../../core/clients/manage/collections/create-collections.md)。|  
|John 建立了名稱為 **Woodgrove Bank 伺服器原則**的自訂反惡意程式碼原則。 他只新增了 [排程掃描]  設定，且進行了下列變更：<br /><br /> **掃描類型**：  **完整**<br /><br /> **掃描日期**：  **星期六**<br /><br /> **掃描時間**： **上午 1 點**<br /><br /> **在用戶端電腦上執行每日快速掃描**：  **否**。|請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。|  
|John 會將 **Woodgrove Bank 伺服器原則** 自訂反惡意程式碼原則，部署至 **Woodgrove Bank 伺服器** 集合。|請參閱 [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md) (如何建立和部署 Endpoint Protection 的反惡意程式碼原則) 主題中的＜將反惡意程式碼原則部署到用戶端電腦＞。|  
|John 會為 Endpoint Protection 建立一組新的自訂用戶端裝置設定，並將其命名為 [Woodgrove Bank Endpoint Protection 設定]。<br /><br /> **注意：**如果不想在階層中的所有用戶端上安裝及啟用 Endpoint Protection，請確定預設用戶端設定中的 [在用戶端電腦上管理 Endpoint Protection 用戶端] 與 [在用戶端電腦上安裝 Endpoint Protection 用戶端] 選項，皆已設定為 [否]。|如需詳細資訊，請參閱[設定 Endpoint Protection 的自訂用戶端設定](endpoint-protection-configure-client.md)。|  
|John 為 Endpoint Protection 設定了下列設定：<br /><br /> ： **是**<br /><br /> 此設定與值可確保任何已安裝的現有 Endpoint Protection 用戶端，都會變成由 Configuration Manager 所管理。<br /><br /> **在用戶端電腦上安裝 Endpoint Protection 用戶端**：  **是**。<br /><br /> **安裝 Endpoint Protection 之前，自動移除先前安裝的反惡意程式碼軟體**：  **是**。<br /><br /> 此設定與值可在安裝及啟用 Endpoint Protection 之前，移除現有反惡意程式碼軟體，以滿足業務需求。|如需詳細資訊，請參閱[設定 Endpoint Protection 的自訂用戶端設定](endpoint-protection-configure-client.md)。|  
|John 將 [Woodgrove Bank Endpoint Protection 設定] 的用戶端設定，部署至 [Endpoint Protection 保護的所有電腦] 集合。|請參閱 [Configuring Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md) (在 Configuration Manager 中設定 Endpoint Protection) 之＜設定 Endpoint Protection 的自訂用戶端設定＞。|  
|John 使用 [建立 Windows 防火牆原則精靈] 來建立原則，方法是為該網域設定檔設定下列設定：<br /><br /> 1) **啟用 Windows 防火牆**：**是**<br /><br /> 2)<br />                    **當 Windows 防火牆阻擋新程式時通知使用者**： **是**|請參閱[如何建立及部署 System Center Configuration Manager 中 Endpoint Protection 的 Windows 防火牆原則](../../protect/deploy-use/create-windows-firewall-policies.md)。|  
|John 將新的防火牆原則部署到之前所建立的 [Endpoint Protection 保護的所有電腦] 集合中。|請參閱[如何建立及部署 System Center Configuration Manager 中 Endpoint Protection 的 Windows 防火牆原則](create-windows-firewall-policies.md)的＜建立 Windows 防火牆原則＞一節。|  
|John 會使用適用於 Endpoint Protection 的管理工作，來管理反惡意程式碼與 Windows 防火牆原則、必要時對電腦執行隨選掃描、強制電腦下載最新的定義，並指定在偵測到惡意程式碼時要採取的任何進一步動作。|請參閱[如何在 System Center Configuration Manager 中管理 Endpoint Protection 的反惡意程式碼原則及防火牆設定](endpoint-antimalware-firewall.md)。|  
|John 使用下列方法來監視 Endpoint Protection 的狀態，以及 Endpoint Protection 所採取的動作：<br /><br /> 1) 使用 [監視] 工作區中 [安全性] 下的 [Endpoint Protection 狀態] 節點。<br /><br /> 2) 使用 [資產與相容性] 工作區中的 [Endpoint Protection] 節點。<br /><br /> 3) 使用 Configuration Manager 的內建報告。|請參閱[如何監視 System Center Configuration Manager 中的 Endpoint Protection](monitor-endpoint-protection.md)。|  

 根據公司給 John 的業務需求，他向主管回報已成功實作 Endpoint Protection，並確認 Woodgrove Bank 的電腦現已受保護可免受反惡意程式的威脅。
