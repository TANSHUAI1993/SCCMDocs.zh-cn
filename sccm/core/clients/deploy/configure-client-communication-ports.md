---
title: "設定用戶端通訊連接埠 | Microsoft Docs"
description: "在 System Center Configuration Manager 中設定用戶端通訊連接埠。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstack
ms.author: robstackmsft
manager: angrobe
ms.openlocfilehash: 63e033fdb436930ac5f37e7408ca9292bc444560
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-communication-ports-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中設定用戶端通訊連接埠

*適用對象：System Center Configuration Manager (最新分支)*

您可以變更 System Center Configuration Manager 用戶端用來與使用 HTTP 和 HTTPS 的站台系統進行通訊的要求連接埠號碼。 雖然可能已針對防火牆設定 HTTP 或 HTTPS，使用 HTTP 或 HTTPS 的用戶端通知，比您使用自訂連接埠號碼需要更多管理點電腦的 CPU 使用量和記憶體。 如果您使用傳統的喚醒封包喚醒用戶端，也可以指定要使用的站台連接埠號碼。  

 當您指定 HTTP 和 HTTPS 要求連接埠，您可以同時指定預設連接埠號碼及替代連接埠號碼。 用戶端會在與預設連接埠通訊失敗後，自動嘗試替代連接埠。 您可以指定 HTTP 和 HTTPS 資料通訊的設定。  

 用戶端要求連接埠的預設值是 HTTP 流量 80  ，HTTPS 流量 443  。 只有在您不想要使用這些預設值時再進行修改。 使用自訂連接埠的一般案例是您在 IIS 中使用自訂網站，而不是使用預設網站。 如果您在 IIS 中變更預設網站的預設連接埠號碼，而其他應用程式也會使用預設網站時，可能會執行失敗。  

> [!IMPORTANT]  
>  除非了解後果，否則請勿變更 Configuration Manager 中的連接埠號碼。 範例：  
>   
>  -   如果您將用戶端要求服務的連接埠號碼變更為站台設定，而現有的用戶端未重新設定為使用新的連接埠號碼時，這些用戶端將會變成未受管理。  
> -   設定非預設的連接埠號碼前，請確定防火牆和所有中介網路裝置皆可支援此設定，並且視需要重新設定。 如果您會在網際網路上管理用戶端，而且會變更預設的 HTTPS 連接埠號碼 443，網際網路上的路由器和防火牆可能會封鎖此通訊。  

 為確定用戶端不會在您變更要求連接埠號碼之後不受管理，必須將用戶端設定為使用新的要求連接埠號碼。 變更主要站台的要求連接埠時，所有連接的次要站台都會自動繼承相同的連接埠設定。 使用本主題中的程序，設定主要站台上的要求連接埠。  

> [!NOTE]  
>  如需如何在執行 Linux 與 UNIX 的電腦上設定用戶端要求連接埠的資訊，請參閱[設定 Linux 和 UNIX 用戶端要求連接埠](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations)。  

 當 Configuration Manager 站台發佈至 Active Directory 網域服務時，將會自動以其站台連接埠設定來設定可存取此資訊的新用戶端和現有用戶端，您不需要採取進一步的動作。 無法存取這個已發佈到 Active Directory 網域服務之資訊的用戶端，包括工作群組用戶端、來自其他 Active Directory 樹系的用戶端、已設定為只使用網際網路的用戶端，以及目前位於網際網路上的用戶端。 如果您在安裝這些用戶端後變更預設連接埠號碼，請使用下列其中一種方法，重新安裝這些用戶端和安裝新的用戶端：  

-   使用「用戶端推入安裝精靈」重新安裝用戶端。 用戶端推入安裝會自動為用戶端設定最新的站台連接埠設定。 如需如何使用用戶端推送安裝精靈的詳細資訊，請參閱 [如何使用用戶端推入安裝 Configuration Manager 用戶端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。  

-   使用 CCMSetup.exe 以及 CCMHTTPPORT 和 CCMHTTPSPORT 的 client.msi 安裝內容，重新安裝用戶端。 如需這些內容的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties.md)。  

-   使用在 Active Directory 網域服務搜尋 Configuration Manager 用戶端安裝內容的方法，重新安裝用戶端。 如需詳細資訊，請參閱[關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

 若要為現有的用戶端重新設定連接埠號碼，您也可以使用隨安裝媒體 (在 SMSSETUP\Tools\PortConfiguration 資料夾中) 提供的指令碼 PORTSWITCH.VBS。  

> [!IMPORTANT]  
>  對於目前位於網際網路的現有和新用戶端，您必須使用 CCMHTTPPORT 和 CCMHTTPSPORT 的 CCMSetup.exe client.msi 內容來設定非預設連接埠號碼。  

 變更站台上的要求連接埠後，使用全站台用戶端推入安裝方法安裝的新用戶端，會自動設定使用該站台目前的連接埠號碼。  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>設定站台的用戶端通訊連接埠號碼  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，展開 [站台設定] ，按一下 [站台] ，然後選取要設定的主要站台。  

3.  在 [首頁]  索引標籤上按一下 [內容] ，然後按一下 [連接埠]  索引標籤。  

4.  選取任一項目，然後按一下 [內容] 圖示以顯示 [連接埠詳細資料]  對話方塊。  

5.  在 [連接埠詳細資料]  對話方塊中，指定項目的連接埠號碼和描述，然後按一下 [確定] 。  

6.  如果您會使用 **SMSWeb** 做為執行 IIS 之站台系統的自訂站台名稱，請選取 [使用自訂站台]  。  

7.  按一下 [確定]  關閉站台的內容對話方塊。  

 為階層中的所有主要站台重複此程序。
