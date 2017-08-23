---
title: "System Center Configuration Manager 中的 VPN 設定檔 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 VPN 設定檔，將 VPN 設定部署至組織中的使用者。"
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e07a80c1a59043b74cda7219f78c5fef66989ba8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 VPN 設定檔

*適用於：System Center Configuration Manager (最新分支)*


在 System Center Configuration Manager (也稱為 ConfigMgr 或 SCCM) 中使用 VPN 設定檔，將 VPN 設定部署至組織中的使用者。 透過部署這些設定，即可最小化連線到公司網路上資源所需的使用者工作。  

 例如，您想要以連線至企業網路上檔案共用所需的設定佈建所有執行 Windows RT 作業系統的裝置。 您可以建立VPN 設定檔，其中含有連線至企業網路所需的設定，然後將此設定檔部署至階層中所有擁有執行 Windows RT 之裝置的使用者。 Windows RT 裝置的使用者會看見可用網路清單中的 VPN 連線，並且可以輕鬆連線至此網路。  

 當您建立 VPN 設定檔時，您可以在其中加入各種安全性設定，包括藉由使用 System Center Configuration Manager 憑證設定檔佈建的伺服器驗證憑證和用戶端驗證憑證。 如需憑證設定檔的詳細資訊，請參閱 [Certificate profiles in System Center Configuration Manager](introduction-to-certificate-profiles.md) (System Center Configuration Manager 中的憑證設定檔)。  

 下列各節會說明如果使用 Configuration Manager，可用 VPN 設定檔設定哪些裝置。

 若要檢視您可以使用 Configuration Manager 搭配 Microsoft Intune 來設定的裝置，請參閱[行動裝置上的 VPN 設定檔](/sccm/mdm/deploy-use/create-vpn-profiles)。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>使用 Configuration Manager 時的 VPN 設定檔  
 下表說明針對不同裝置平台可以設定的 VPN 設定檔。  

|連線類型|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|否|否|否|否|  
|**Pulse Secure**|是|否|是|是|  
|**F5 Edge Client**|[是]|否|是|是|  
|**Dell SonicWALL Mobile Connect**|[是]|否|是|[是]|  
|**Check Point Mobile VPN**|是|否|是|是|  
|**Microsoft SSL (SSTP)**|是|[是]|是|否|  
|**Microsoft Automatic**|是|[是]|是|否|  
|**IKEv2**|是|[是]|是|否|  
|**PPTP**|是|[是]|是|否|  
|**L2TP**|是|[是]|是|否|  

### <a name="next-steps"></a>後續步驟  
 使用下列主題可協助您規劃、設定、操作及維護 Configuration Manager 中的 VPN 設定檔。  

-   [System Center Configuration Manager 中的 VPN 設定檔必要條件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中的 VPN 設定檔安全性及隱私權](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
