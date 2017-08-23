---
title: "如何在 System Center Configuration Manager 中建立 VPN 設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中建立 VPN 設定檔。"
ms.custom: 
ms.date: 4/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: "15"
author: lleonard-msft
caps.handback.revision: "0"
ms.author: alleonar
ms.manager: angrobe
ms.openlocfilehash: 359fcfd9754fb5c81763bc44cac45376ea3ab0b8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中建立 VPN 設定檔

*適用於：System Center Configuration Manager (最新分支)*

適用於不同裝置平台之連線類型的資訊，描述於 [System Center Configuration Manager 中的 VPN 設定檔](../../protect/deploy-use/vpn-profiles.md)。  

針對協力廠商 VPN 連線，請先發佈 VPN 應用程式，再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們執行此動作。 若要了解如何部署應用程式，請參閱[使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications.md)。

### <a name="create-a-vpn-profile"></a>建立 VPN 設定檔   

1.  在 Configuration Manager 主控台中，選擇 [資產與合規性] > [合規性設定] > [公司資源存取] > [VPN 設定檔]。  

3.  在 [常用] 索引標籤的 [建立] 群組中，選擇 [建立 VPN 設定檔]。  


1.  完成 [一般] 頁面。 ，並注意下列事項：  

    - 請勿在 VPN 設定檔名稱中使用字元 \\/:*?&lt;>&#124;, 或空格字元。 Windows Server VPN 設定檔不支援這些字元。  

     -   選取 [從檔案匯入現有的 VPN 設定檔項目] 匯入已匯出至 XML 檔案的 VPN 設定檔資訊 (僅限 Windows 8.1 和 Windows RT)。  

1.  在 [連線] 頁面上，指定：  

    -   **連線類型**︰選擇 VPN 連線類型。 您可以從下表中，選擇連線類型。  

    -   **伺服器清單**：新增要用於 VPN 連線的新伺服器。 根據連線類型而定，您可以新增一或多部 VPN 伺服器，並指定預設伺服器。  

        > [!NOTE]  
        >  執行 iOS 的裝置並不支援使用多部 VPN 伺服器。 如果您設定多部 VPN 伺服器，然後將 VPN 設定檔部署至 iOS 裝置，則只會使用預設伺服器。  

     下表提供連線類型的選項。 如需詳細資訊，請參閱您的 VPN 伺服器文件。

| &nbsp;&nbsp;選項&nbsp;&nbsp; | 詳細資訊 | &nbsp;&nbsp;連線&nbsp;類型&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**領域**     |您想要使用之驗證領域的名稱。 驗證領域是 Pulse Secure 連線類型所使用的驗證資源群組。|Pulse Secure|    
|**角色**        |有權存取此連線的使用者角色。 |Pulse Secure|  
|**登入群組或網域** |您想要連線之登入群組或網域的名稱。|Dell SonicWALL Mobile Connect|  
|**指紋**  |將用來確認是否可以信任 VPN 伺服器的字串 (例如 "Contoso Fingerprint Code")。<br /><br /> 指紋可以是：<br /><br /> - 傳送至用戶端，讓它知道信任連線時呈現該相同指紋的任何伺服器。<br /><br /> - 如果裝置還沒有指紋，則會提示使用者信任所連線的 VPN 伺服器，同時顯示指紋 (使用者手動驗證指紋，並選擇 [信任] 以連線)。|檢查點行動 VPN|  
|**透過 VPN 連線傳送所有網路流量** |如果未選取此選項，您可以針對連線 (如 **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 和 **L2TP** 連線類型) 指定其他路由，這稱為分割或 VPN 通道處理。<br /><br /> 只有公司網路的連線會透過 VPN 通道傳送。 當您連線至網際網路上的資源時不會使用 VPN 通道。 |全部|  
|**連線特定 DNS 尾碼** |連線的連線特定網域名稱系統 (DNS) 尾碼。|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**連線到公司 Wi-Fi 網路時略過 VPN**  |裝置連線到公司 Wi-Fi 網路時，不會使用 VPN 連線。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**連線到家用 Wi-Fi 網路時略過 VPN**  |裝置連線到家用 Wi-Fi 網路時，不會使用 VPN 連線。|全部|  
|**每個應用程式 VPN (iOS 7 及更新版本、Mac OS X 10.9 及更新版本)** |將這個 VPN 連線與 iOS 應用程式產生關聯，以在執行應用程式時開啟連線。 部署應用程式時，您可以將 VPN 設定檔與該應用程式產生關聯。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
|**自訂 XML (選用)** |指定設定 VPN 連線的自訂 XML 命令。<br /><br /> 範例：<br /><br /> 針對 **Pulse Secure**：<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> 針對 **CheckPoint Mobile VPN**：<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> 針對 **Dell SonicWALL Mobile Connect**：<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> 針對 **F5 Edge Client**：<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> 如需如何撰寫自訂 XML 命令的詳細資訊，請參閱相關製造商的 VPN 文件。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

> [!NOTE]  
>  如需建立行動裝置 VPN 設定檔的特定資訊，請參閱[建立 VPN 設定檔](../../mdm/deploy-use/create-vpn-profiles.md)  

完成精靈。 新的 VPN 設定檔會顯示在 [資產與合規性] 工作區的 [VPN 設定檔] 節點中。

### <a name="next-steps"></a>後續步驟

- 針對協力廠商 VPN 連線，請先發佈 VPN 應用程式，再部署 VPN 設定檔。 如果您未部署應用程式，則系統會在使用者嘗試連線至 VPN 時提示他們執行此動作。 若要了解如何部署應用程式，請參閱[使用 System Center Configuration Manager 部署應用程式](../../apps/deploy-use/deploy-applications.md)。

- 部署 VPN 設定檔 (如[如何在 System Center Configuration Manager 中部署設定檔](deploy-wifi-vpn-email-cert-profiles.md)中所述)。  
