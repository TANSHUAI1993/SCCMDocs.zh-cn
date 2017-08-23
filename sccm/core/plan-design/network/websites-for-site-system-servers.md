---
title: "站台系統的網站 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中站台系統伺服器的預設和自訂網站。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 886ff3b8e867fc340c79648a57feae81653b0ccd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager 中站台系統伺服器的網站

*適用對象：System Center Configuration Manager (最新分支)*

一些 Configuration Manager 站台系統角色都需要 Microsoft Internet Information Services (IIS)，並使用預設 IIS 網站來裝載主機站台系統服務。 若您必須在同一部伺服器上執行其他 Web 應用程式，但設定與 Configuration Manager 不相容時，請考慮為 Configuration Manager 使用自訂網站。  

> [!TIP]  
>  保障安全性的最佳做法是為需要 IIS 的 Configuration Manager 站台系統設定專用伺服器。 當您在 Configuration Manager 站台系統上執行其他應用程式時，會增加該部電腦的攻擊面。  




##  <a name="BKMK_What2Know"></a> 選擇使用自訂網站前的須知事項  
 站台系統角色預設會在 IIS 中使用 **預設網站** 。 此設定在安裝站台系統角色時即自動完成。 不過，在主要站台，您可以選擇改用自訂網站。 當您使用自訂網站時：  

-   自訂網站的啟用對象為整個站台，而非個別站台系統或角色。  

-   在主要站台上，每一部裝載適用之站台系統角色的電腦都必須設好名為 **SMSWEB**的自訂網站。 只有在建立了此網站且於該電腦上設定了站台系統角色之後，用戶端才可能與該電腦上的站台系統角色相通訊。  

-   因為次要站台在其主要站台設定為要使用自訂網站時，即會自動設定為使用自訂網站，所以也必須在需要 IIS 的每部次要站台系統伺服器上，於 IIS 中建立自訂網站。  


  **使用自訂網站的必要條件：**  

 在您啟用在站台使用自訂網站的選項前，您必須：  

-   在每部需要 IIS 之站台系統伺服器的 IIS 中，建立名為 **SMSWEB** 的自訂網站。 不論主要站台和任何子次要站台，都要進行這項作業。  

-   將自訂網站設定為回應您針對 Configuration Manager 用戶端通訊 (用戶端要求通訊埠) 設定的相同連接埠。  

-   針對每個使用自訂資料夾的自訂網站或預設網站，將您所用的預設文件類型複本，放在裝載網站的根資料夾中。 例如，在使用預設設定的 Windows Server 2008 R2 電腦上，**iisstart.htm** 是數個可用的預設文件類型之一。 您可在預設網站的根目錄中找到此檔案，然後將這個檔案的複本 (或是您使用之預設文件類型的複本) 放在裝載 SMSWEB 自訂網站的根資料夾中。 如需預設文件類型的相關資訊，請參閱 IIS 的 [Default Document &lt;defaultDocument\>](http://www.iis.net/configreference/system.webserver/defaultdocument) (預設文件 <預設文件>)。  

**關於 IIS 需求：**
**下列站台系統角色要求 IIS 和網站裝載站台系統服務：**  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   發佈點  

-   註冊點  

-   註冊 Proxy 點  

-   後援狀態點  

-   管理點  

-   軟體更新點  

-   狀態移轉點  

其他考量：  

-   當主要站台的自訂網站已啟用時，就會將指派給該站台的用戶端導向為與自訂網站通訊，而非適用站台系統伺服器上的預設網站  

-   如果您會將自訂網站用於一個主要站台，請考慮針對您階層內所有網站都使用自訂網站，以確保用戶端可在階層內順利漫遊。 (當用戶端電腦移到由其他站台所管理的新網路區段時，即為漫遊。 漫遊可能會影響用戶端可從本機存取而非透過 WAN 連結存取的資源)。  

-   使用 IIS 但不接受像是 Reporting Services 點等用戶端連線的網站系統角色，也會使用 SMSWEB 網站，而非使用預設網站。  

-   自訂網站要求您指派不同於電腦預設網站所用的連接埠號碼。 如果預設網站和自訂網站都嘗試使用相同的 TCP/IP 連接埠，就無法同時執行兩個網站。  

-   您在 IIS 中為自訂網站設定的 TCP/IP 連接埠必須符合站台的用戶端要求連接埠。  

## <a name="switch-between-default-and-custom-websites"></a>在預設網站和自訂網站之間切換  
雖然可隨時選取或取消選取在主要站台使用自訂網站的核取方塊 (此方塊位於站台 [屬性] 的 [一般] 索引標籤上)，仍須在進行這項變更前謹慎規劃。 當此設定變更時，主要站台和子次要站台上的所有適用站台系統角色都必須解除安裝，再重新安裝：  

下列角色會 **自動重新安裝**：  

-   管理點  

-   發佈點  

-   軟體更新點  

-   後援狀態點  

-   狀態移轉點  

下列角色則必須 **手動重新安裝**：  

-   應用程式類別目錄 Web 服務點  

-   應用程式類別目錄網站點  

-   註冊點  

-   註冊 Proxy 點  

此外：  

-   從使用預設網站變更為使用自訂網站時，Configuration Manager 不會移除舊的虛擬目錄。 如果您要移除 Configuration Manager 使用的檔案，就必須手動刪除建立於預設網站下的虛擬目錄。  

-   如果您將站台變更為使用自訂網站，就必須將已指派給站台的用戶端重新設定為使用自訂網站的新用戶端要求連接埠。 請參閱[如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../../core/clients/deploy/configure-client-communication-ports.md)。  

## <a name="set-up-custom-websites"></a>設定自訂網站  
因為建立自訂網站的步驟對於不同作業系統版本有所差異，所以請參考您的作業系統版本文件以取得準確步驟，但在適用時使用下列資訊：  

-   網站名稱必須是：**SMSWEB**。  

-   設定 HTTPS 時，必須先指定 SSL 憑證才可儲存設定。  

-   建立自訂網站後，請從 IIS 中的其他網站移除您所用的自訂網站連接埠：  

    1.  編輯其他網站的 [繫結]，以移除符合指派給 **SMSWEB** 網站的連接埠。  

    2.  啟動 **SMSWEB** 網站。  

    3.  重新啟動站台的站台伺服器上 **SMS_SITE_COMPONENT_MANAGER** 服務。  
