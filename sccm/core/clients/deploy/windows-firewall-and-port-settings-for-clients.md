---
title: "Windows 用戶端防火牆和連接埠設定 | Microsoft Docs"
description: "在 System Center Configuration Manager 中選取用戶端的 Windows 防火牆和連接埠設定。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 79686514efcba344c4babc3d3be03b48adca7132
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="windows-firewall-and-port-settings-for-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager 中用戶端適用的 Windows 防火牆和連接埠設定

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中執行 Windows 防火牆的用戶端，通常需要您將其設定為例外，以允許它們與站台進行通訊。 您必須設定的例外，取決於您搭配 Configuration Manager 用戶端使用哪些管理功能。  

 使用以下各節識別這些管理功能，以及取得有關如何在 Windows 防火牆設定這些例外的詳細資訊。  

##  <a name="BKMK_ModifyingWindowsFirewall"></a> 修改 Windows 防火牆准許的連接埠和程式  
 使用下列程序可在 Windows 防火牆上為 Configuration Manager 用戶端修改連接埠和程式。  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>修改 Windows 防火牆准許的連接埠和程式  

1.  在執行 Windows 防火牆的電腦上開啟 [控制台]。  

2.  以滑鼠右鍵按一下 [Windows 防火牆] ，然後按一下 [開啟] 。  

3.  設定必要的例外，以及所需的自訂程式和連接埠。  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Configuration Manager 所需的程式和連接埠  
 下列 Configuration Manager 功能需要 Windows 防火牆上的例外：  

### <a name="queries"></a>查詢  
 如果您在執行 Windows 防火牆的電腦上執行 Configuration Manager 主控台，則第一次執行的查詢會失敗，且作業系統會顯示一個對話方塊，詢問您是否要解除封鎖 statview.exe。 如果您解除封鎖 statview.exe，將可順利執行以後的查詢，不會發生錯誤。 您也可以在執行查詢前，於 Windows 防火牆的 [例外]  索引標籤上手動將 Statview.exe 新增至程式和服務清單。  

### <a name="client-push-installation"></a>用戶端推入安裝  
 若要使用用戶端推入來安裝 Configuration Manager 用戶端，請將以下例外新增至 Windows 防火牆：  

-   傳出和傳入：檔案及印表機共用   

-   傳入：Windows Management Instrumentation (WMI)   

### <a name="client-installation-by-using-group-policy"></a>使用群組原則安裝用戶端  
 若要使用群組原則安裝 Configuration Manager 用戶端，請在 Windows 防火牆新增 [檔案及印表機共用] 以當作例外。  

### <a name="client-requests"></a>用戶端要求  
 若要讓用戶端電腦與 Configuration Manager 站台系統進行通訊，請在 Windows 防火牆新增下列各項以當作例外：  

 傳出：TCP 連接埠 80  (適用於 HTTP 通訊)  

 傳出：TCP 連接埠 443  (適用於 HTTPS 通訊)  

> [!IMPORTANT]  
>  這些連接埠為預設的連接埠號碼，可在 Configuration Manager 中變更。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../../core/clients/deploy/configure-client-communication-ports.md)。 如果這些連接埠已變更為非預設值，您也必須在 Windows 防火牆設定相符的例外。  

### <a name="client-notification"></a>用戶端通知  
 若要讓管理點通知用戶端電腦有關其必須在系統管理使用者在 Configuration Manager 主控台選取用戶端動作時採取某項動作 (例如下載電腦原則或起始惡意程式碼掃描)，請在 Windows 防火牆新增下列各項以當作例外：  

 傳出：TCP 連接埠 10123   

 如果此通訊不成功，Configuration Manager 會自動改回使用現有 HTTP 或 HTTPS 的用戶端對管理點通訊連接埠：  

 傳出：TCP 連接埠 80  (適用於 HTTP 通訊)  

 傳出：TCP 連接埠 443  (適用於 HTTPS 通訊)  

> [!IMPORTANT]  
>  這些連接埠為預設的連接埠號碼，可在 Configuration Manager 中變更。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端通訊連接埠](../../../core/clients/deploy/configure-client-communication-ports.md)。 如果這些連接埠已變更為非預設值，您也必須在 Windows 防火牆設定相符的例外。  

### <a name="remote-control"></a>遠端控制  
 若要使用 Configuration Manager 遠端控制，請允許下列連接埠：  

-   傳入：TCP 連接埠 2701  

### <a name="remote-assistance-and-remote-desktop"></a>遠端協助和遠端桌面  
 若要從 Configuration Manager 主控台起始 [遠端協助]，請在用戶端電腦的 Windows 防火牆將自訂程式 **Helpsvc.exe** 和輸入自訂連接埠 TCP **135** 新增至准許的程式和服務清單中。 您也必須准許 [遠端協助]  和 [遠端桌面] 。 如果您從用戶端電腦起始 [遠端協助]，Windows 防火牆會自動設定並准許 [遠端協助]  和 [遠端桌面] 。  

### <a name="wake-up-proxy"></a>喚醒 Proxy  
 如果您啟用喚醒 Proxy 用戶端設定，則會使用一個名為 ConfigMgr Wake-up Proxy 的新服務，透過點對點通訊協定檢查子網路上的其他電腦是否為執行中狀態，並視需要喚醒這些電腦。 這類通訊會使用下列連接埠：  

 傳出：UDP 連接埠 25536   

 傳出：UDP 連接埠 9   

 這些連接埠號碼為預設值，可在 Configuration Manager 中使用 [喚醒 Proxy 連接埠號碼 (UDP)] 和 [網路喚醒連接埠號碼 (UDP)] 的 [電源管理] 用戶端設定進行變更。 如果您指定 [電源管理] ：[喚醒 Proxy 的 Windows 防火牆例外]  用戶端設定，會自動在 Windows 防火牆為用戶端設定這些連接埠。 不過，如果用戶端執行不同的防火牆，您必須手動將這些連接埠號碼設定為例外。  

 除了這些連接埠，喚醒 Proxy 也會在用戶端電腦之間使用網際網路控制訊息通訊協定 (ICMP) 回應要求訊息。 此通訊用於確認網路上的另一台用戶端電腦是否處於喚醒狀態。 ICMP 有時稱為 TCP/IP Ping 命令。  

 如需喚醒 Proxy 的詳細資訊，請參閱[規劃如何在 System Center Configuration Manager 中喚醒用戶端](../../../core/clients/deploy/plan/plan-wake-up-clients.md)。  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Windows 事件檢視器、Windows 效能監視器和 Windows 診斷  
 若要從 Configuration Manager 主控台存取 Windows 事件檢視器、Windows 效能監視器和 Windows 診斷，請在 Windows 防火牆將 [檔案及印表機共用] 設為例外。  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Configuration Manager 用戶端部署期間使用的連接埠  
 下表列出用戶端安裝程序執行期間使用的連接埠。  

> [!IMPORTANT]  
>  如果站台系統和用戶端電腦之間有防火牆，請確認防火牆是否准許您所選用戶端安裝方法所需連接埠的流量通過。 例如，防火牆通常會阻止用戶端推入安裝無法順利執行，因為防火牆會封鎖伺服器訊息區 (SMB) 和遠端程序呼叫 (RPC)。 在此案例中，請使用不同的用戶端安裝方法，例如手動安裝 (執行 CCMSetup.exe) 或以群組原則為基礎的用戶端安裝。 這些替代用戶端安裝方法不需要 SMB 或 RPC。  

 如需有關如何在用戶端電腦上設定 Windows 防火牆的資訊，請參閱 [修改 Windows 防火牆准許的連接埠和程式](#BKMK_ModifyingWindowsFirewall)。  

### <a name="ports-that-are-used-for-all-installation-methods"></a>所有安裝方法使用的連接埠  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|若已為用戶端指派後援狀態點，則從用戶端電腦到後援狀態點都會使用超文字傳輸協定 (HTTP)。|--|80 (請參閱附註 1， **可用的替代連接埠**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>搭配用戶端推入安裝使用的連接埠  
 除了下表所列的連接埠，用戶端推入安裝也會在站台伺服器與用戶端電腦之間使用網際網路控制訊息通訊協定 (ICMP) 回應要求訊息，確認網路上是否存在該用戶端電腦。 ICMP 有時稱為 TCP/IP Ping 命令。 ICMP 沒有 UDP 或 TCP 通訊協定號碼，因此未列在下表中。 不過，任何中介網路裝置 (如防火牆) 都必須准許 ICMP 流量，才可順利進行用戶端推入安裝。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|站台伺服器和用戶端電腦之間的伺服器訊息區 (SMB)。|--|445|  
|站台伺服器和用戶端電腦之間的 RPC 端點對應程式。|135|135|  
|站台伺服器和用戶端電腦之間的 RPC 動態連接埠。|--|動態|  
|若透過 HTTP 連線，則從用戶端電腦到管理點都會使用超文字傳輸協定 (HTTP)。|--|80 (請參閱附註 1， **可用的替代連接埠**)|  
|若透過 HTTPS 連線，則從用戶端電腦到管理點都會使用超文字傳輸協定 (HTTPS)。|--|433 (請參閱註 1， **可用的替代連接埠**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>搭配以軟體更新點為基礎之安裝所使用的連接埠  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|從用戶端電腦到軟體更新點的超文字傳輸協定 (HTTP)。|--|80 或 8530 (請參閱附註 2， **Windows Server Update Services**)|  
|從用戶端電腦到軟體更新點的安全超文字傳輸通訊協定 (HTTP)。|--|443 或 8531 (請參閱附註 2， **Windows Server Update Services**)|  
|當您指定 CCMSetup 命令列內容 **/source:&lt;路徑\>** 時，來源伺服器和用戶端電腦間會使用伺服器訊息區 (SMB)。|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>搭配以群組原則為基礎之安裝所使用的連接埠  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|若透過 HTTP 連線，則從用戶端電腦到管理點都會使用超文字傳輸協定 (HTTP)。|--|80 (請參閱附註 1， **可用的替代連接埠**)|  
|若透過 HTTPS 連線，則從用戶端電腦到管理點都會使用超文字傳輸協定 (HTTPS)。|--|433 (請參閱註 1， **可用的替代連接埠**)|  
|當您指定 CCMSetup 命令列內容 **/source:&lt;路徑\>** 時，來源伺服器和用戶端電腦間會使用伺服器訊息區 (SMB)。|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>搭配手動安裝和以登入指令碼為基礎之安裝所使用的連接埠  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|在執行 CCMSetup.exe 之用戶端電腦和網路共用之間的伺服器訊息區 (SMB)。<br /><br /> 當您安裝 Configuration Manager 時，會從管理點的 *&lt;安裝路徑\>*\Client 資料夾複製用戶端安裝來源檔案，並自動共用。 不過，您可以在網路的任何電腦上複製這些檔案，並建立新共用。 此外，您可以在本機執行 CCMSetup.exe (例如使用卸除式媒體)，以避免產生此網路流量。|--|445|  
|當您透過 HTTP 連線，且未指定 CCMSetup 命令列內容 **/source:&lt;路徑\>** 時，從用戶端電腦到管理點都會使用超文字傳輸通訊協定 (HTTP)。|--|80 (請參閱附註 1， **可用的替代連接埠**)|  
|當您透過 HTTPS 連線，且未指定 CCMSetup 命令列內容 **/source:&lt;路徑\>** 時，從用戶端電腦到管理點都會使用安全超文字傳輸通訊協定 (HTTPS)。|--|433 (請參閱註 1， **可用的替代連接埠**)|  
|當您指定 CCMSetup 命令列內容 **/source:&lt;路徑\>** 時，來源伺服器和用戶端電腦間會使用伺服器訊息區 (SMB)。|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>搭配以軟體發佈為基礎之安裝所使用的連接埠  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|發佈點和用戶端電腦之間的伺服器訊息區 (SMB)。|--|445|  
|若透過 HTTP 連線，則從用戶端到發佈點都會使用超文字傳輸協定 (HTTP)。|--|80 (請參閱附註 1， **可用的替代連接埠**)|  
|若透過 HTTPS 連線，則從用戶端到發佈點都會使用安全超文字傳輸協定 (HTTPS)。|--|433 (請參閱註 1， **可用的替代連接埠**)|  

## <a name="notes"></a>附註  
 **1 可用的替代連接埠** 在 Configuration Manager 中，您可以定義此值的替代連接埠。 如果已定義自訂連接埠，便可以在您定義 IPsec 原則的 IP 篩選資訊或設定防火牆時，替換該自訂連接埠。  

 **2 Windows Server Update Services** 您可以在預設網站 (連接埠 80) 或自訂網站 (連接埠 8530) 安裝 Windows Server Update Service (WSUS)。  

 安裝後，即可變更連接埠。 您不需要在整個網站階層都使用相同的連接埠號碼。  

 如果 HTTP 連接埠是80，HTTPS 連接埠必須是 443。  

 如果 HTTP 連接埠使用其他任何號碼，則 HTTPS 連接埠必須是該連接埠號碼加 1。 例如，8530 和 8531。
