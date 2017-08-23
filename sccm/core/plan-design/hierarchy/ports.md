---
title: "Configuration Manager 使用的連接埠 | Microsoft Docs"
description: "了解 System Center Configuration Manager 用於連線的必要和可自訂連接埠。"
ms.custom: na
ms.date: 3/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 78caa69e10f5d386daab1e61e484d4d134469708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="ports-used-in-system-center-configuration-manager"></a>System Center Configuration Manager 中使用的連接埠

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 是分散式用戶端/伺服器系統。 Configuration Manager 具有分散式特性，因此可以在站台伺服器、站台系統及用戶端之間建立連線。 某些連線使用不可設定的連接埠，有些則支援您指定的自訂連接埠。 如果使用防火牆、路由器、Proxy 伺服器或 IPsec 之類的連接埠篩選技術，則必須驗證所需連接埠是否可用。  

> [!NOTE]  
>  如果使用 SSL 橋接功能支援以網際網路為基礎的用戶端，除了連接埠需求外，可能還必須允許某些 HTTP 動詞和標頭來周遊防火牆。   

 Configuration Manager 會使用下列連接埠清單，且不包括標準 Windows 服務的資訊，例如 Active Directory 網域服務或 Kerberos 驗證的群組原則設定。 如需 Windows Server 服務和連接埠的詳細資訊，請參閱 [Windows Server 系統的服務概觀與網路連接埠需求](http://go.microsoft.com/fwlink/p/?LinkID=123652)。  

##  <a name="BKMK_ConfigurablePorts"></a> 您可以設定的連接埠  
 Configuration Manager 可讓您設定用於下列通訊類型的連接埠：  

-   應用程式類別目錄網站點對應用程式類別目錄 Web 服務點  

-   註冊 Proxy 點對註冊點  

-   執行 IIS 的用戶端對站台系統  

-   用戶端對網際網路 (如 Proxy 伺服器設定)  

-   軟體更新點對網際網路 (如 Proxy 伺服器設定)  

-   軟體更新點對 WSUS 伺服器  

-   網站伺服器對網站資料庫伺服器  

-   Reporting Services 點  

    > [!NOTE]  
    >  您必須在 SQL Server Reporting Services 中設定 Reporting Services 點站台系統角色所用的連接埠。 然後，Configuration Manager 會在與 Reporting Services 點通訊期間使用這些連接埠。 請務必檢閱這些連接埠，以定義用於 IPsec 原則或設定防火牆的 IP 篩選資訊。  

根據預設，用戶端對站台系統通訊所使用的 HTTP 連接埠是連接埠 80，且預設的 HTTPS 連接埠是 443。 您可以在安裝期間變更用戶端對站台系統的 HTTP 或 HTTPS 通訊連接埠，也可以在 Configuration Manager 站台的站台內容中進行變更。  

您必須在 SQL Server Reporting Services 中設定 Reporting Services 點站台系統角色所用的連接埠。 然後，Configuration Manager 會在與 Reporting Services 點通訊期間使用這些連接埠。 在您定義 IP 篩選資訊以用於 IPsec 原則或設定防火牆時，請務必檢閱這些連接埠。  

##  <a name="BKMK_NonConfigurablePorts"></a> 不可設定的連接埠  
Configuration Manager 不允許設定用於下列通訊類型的連接埠：  

-   網站對網站  

-   網站伺服器對網站伺服器  

-   Configuration Manager 主控台對 SMS 提供者  

-   Configuration Manager 主控台對網際網路  

-   與 Microsoft Intune 和雲端式發佈點等雲端服務的連線  

##  <a name="BKMK_CommunicationPorts"></a> Configuration Manager 用戶端和站台系統使用的連接埠  
下列各節詳細說明 Configuration Manager 中用於通訊的連接埠。 章節標題中的箭頭代表通訊方向：  

-   -- > 表示其中一部電腦起始通訊，而另一部電腦一律會回應  

-   &lt; -- > 表示兩部電腦皆可起始通訊  

###  <a name="BKMK_PortsAI"></a> Asset Intelligence 同步處理點 -- > Microsoft  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a> Asset Intelligence 同步處理點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2， **可用的替代連接埠**)|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a> 應用程式類別目錄 Web 服務點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> 應用程式類別目錄網站點 -- > 應用程式類別目錄 Web 服務點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> 用戶端 -- > 應用程式類別目錄網站點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> 用戶端 -- &gt; 用戶端  
 除下表所列的連接埠外，當用戶端設定了喚醒 Proxy 時，喚醒 Proxy 也會使用其中一個用戶端傳至其他用戶端的網際網路控制訊息通訊協定 (ICMP) 回應要求訊息。

此通訊用於確認網路上的另一台用戶端電腦是否處於喚醒狀態。 ICMP 有時稱為 TCP/IP Ping 命令。 ICMP 沒有 UDP 或 TCP 通訊協定號碼，因此未列在下表中。 不過，這些用戶端電腦或子網路內中介網路裝置上的所有主機型防火牆都必須允許 ICMP 流量，否則喚醒 Proxy 通訊不會成功。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|網路喚醒|9 (請參閱註 2，**可用的替代連接埠**)|--|  
|喚醒 proxy|25536 (請參閱註 2，**可用的替代連接埠**)|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> 用戶端 -- &gt; Configuration Manager 原則模組 (網路裝置註冊服務)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)||80|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a> 用戶端 -- > 雲端發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a> 用戶端 -- > 發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsClient-DP2"></a> 用戶端 -- > 設定用於多點傳送的發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|多點傳送通訊協定|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> 用戶端 -- > 設定用於 PXE 的發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|動態主機設定通訊協定 (DHCP)|67 和 68|--|  
|簡單式檔案傳輸通訊協定 (TFTP)|69 (請參閱註 4，**Trivial FTP (TFTP) 精靈**)|--|  
|開機資訊交涉階層 (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a> 用戶端 -- > 後援狀態點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsClient-GCDC"></a> 用戶端 -- > 通用類別目錄的網域控制站  
 Configuration Manager 用戶端屬於工作群組電腦或設定僅用於網際網路通訊時，不會與通用類別目錄伺服器通訊。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|通用類別目錄 LDAP|--|3268|  
|通用類別目錄 LDAP SSL|--|3269|  

###  <a name="BKMK_PortsClient-MP"></a> 用戶端 -- > 管理點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|用戶端通知 (後援至 HTTP 或 HTTPS 之前的預設通訊)|--|10123 (請參閱註 2，**可用的替代連接埠**)|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsClient-SUP"></a> 用戶端 -- > 軟體更新點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 或 8530 (請參閱註 3， **Windows Server Update Services**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 或 8531 (請參閱註 3， **Windows Server Update Services**)|  

###  <a name="BKMK_PortsClient-SMP"></a> 用戶端 -- > 狀態移轉點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  
|伺服器訊息區 (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a> Configuration Manager 主控台 -- > 用戶端  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|遠端控制 (控制)|--|2701|  
|遠端協助 (RDP 和 RTC)|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a> Configuration Manager 主控台 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a> Configuration Manager 主控台 -- > Reporting Services 點  


|說明|UDP|TCP|
|-----------------|---------|---------|   
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsConsole-Site"></a> Configuration Manager 主控台 -- > 站台伺服器  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (與 WMI 的初始連線，用於尋找提供者系統)|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a> Configuration Manager 主控台 -- > SMS 提供者  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager 原則模組 (網路裝置註冊服務) -- > 憑證登錄點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsDist_MP"></a> 發佈點 -- > 管理點  
 在下列情況中，發佈點會與管理點通訊：  

-   報告預先設置內容的狀態  

-   報告摘要資料的使用方式  

-   報告內容驗證  

-   報告套件下載 (提取發佈點) 的狀態

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 2，**可用的替代連接埠**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection 點 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection 點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> 註冊 Proxy 點 -- > 註冊點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> 註冊點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server 連接器 -- &gt; Exchange Online  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|Windows 透過 HTTPS 的遠端管理|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server 連接器 -- > 內部部署 Exchange Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 HTTP 的 Windows 遠端管理|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac 電腦 -- > 註冊 Proxy 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a> 管理點 -- > 網域控制站  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|輕量型目錄存取通訊協定 (LDAP)|--|389|  
|LDAP (安全通訊端層 [SSL] 連線)|636|636|  
|通用類別目錄 LDAP|--|3268|  
|通用類別目錄 LDAP SSL|--|3269|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsMP-Site"></a> 管理點 &lt; -- > 站台伺服器  
 (請參閱註 5， **網站伺服器與網站系統之間的通訊**)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 端點對應程式|--|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  
|伺服器訊息區 (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a> 管理點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> 行動裝置 -- > 註冊 Proxy 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> 行動裝置 -- > Microsoft Intune  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a> Reporting Services 點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> 服務連接點 -- > Microsoft Intune  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|
如需詳細資訊，請參閱服務連接點的[網際網路存取需求](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)。

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> 站台伺服器 &lt; -- > 應用程式類別目錄 Web 服務點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> 站台伺服器 &lt; -- > 應用程式類別目錄網站點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-AISP"></a> 站台伺服器 &lt; -- > Asset Intelligence 同步處理點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-Client"></a> 站台伺服器 -- > 用戶端  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|網路喚醒|9 (請參閱註 2，**可用的替代連接埠**)|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a> 站台伺服器 -- > 雲端發佈點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a> 站台伺服器 -- > 發佈點  
 (請參閱註 5， **網站伺服器與網站系統之間的通訊**)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-DC"></a> 站台伺服器 -- > 網域控制站  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|輕量型目錄存取通訊協定 (LDAP)|--|389|  
|LDAP (安全通訊端層 [SSL] 連線)|636|636|  
|通用類別目錄 LDAP|--|3268|  
|通用類別目錄 LDAP SSL|--|3269|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> 站台伺服器 &lt; -- > 憑證登錄點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> 站台伺服器 &lt; -- > Endpoint Protection 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> 站台伺服器 &lt; -- > 註冊點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> 站台伺服器 &lt; -- > 註冊 Proxy 點  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-FSP"></a> 站台伺服器 &lt; -- > 後援狀態點  
 (請參閱註 5， **網站伺服器與網站系統之間的通訊**)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortSite-Internet"></a> 站台伺服器 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 1，**Proxy 伺服器連接埠**)|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> 站台伺服器 &lt; -- > 發行憑證授權單位 (CA)  
 當您想要藉由使用憑證登錄點來部署憑證設定檔時，可使用此項通訊。 並非階層中的每部站台伺服器都會使用這種通訊。 反之，只有階層的頂層站台伺服器會加以使用。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC 端點對應程式|135|135|  
|RPC (DCOM)|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-RSP"></a> 站台伺服器 &lt; -- > Reporting Services 點  
 (請參閱註 5， **網站伺服器與網站系統之間的通訊**)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-Site"></a> 站台伺服器 &lt; -- > 站台伺服器  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a> 站台伺服器 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

 如果站台會使用遠端 SQL Server 來裝載站台資料庫，則在安裝該站台時，您必須在站台伺服器和 SQL Server 之間開啟下列連接埠：  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-Provider"></a> 站台伺服器 -- > SMS 提供者  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  
|RPC|--|DYNAMIC (請參閱註 6， **動態連接埠**)|  

###  <a name="BKMK_PortsSite-SUP"></a> 站台伺服器 &lt; -- > 軟體更新點  
 (請參閱註 5， **網站伺服器與網站系統之間的通訊**)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|超文字傳輸通訊協定 (HTTP)|--|80 或 8530 (請參閱註 3， **Windows Server Update Services**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 或 8531 (請參閱註 3， **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSite-SMP"></a> 站台伺服器 &lt; -- > 狀態移轉點  
 (請參閱註 5， **網站伺服器與網站系統之間的通訊**)  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  
|RPC 端點對應程式|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> SMS 提供者 -- &gt; SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  

###  <a name="BKMK_PortsSUP-Internet"></a> 軟體更新點 -- > 網際網路  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 (請參閱註 1，**Proxy 伺服器連接埠**)|  

###  <a name="BKMK_PortsSUP-WSUS"></a> 軟體更新點 -- > 上游 WSUS 伺服器  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|超文字傳輸通訊協定 (HTTP)|--|80 或 8530 (請參閱註 3， **Windows Server Update Services**)|  
|安全超文字傳輸通訊協定 (HTTPS)|--|443 或 8531 (請參閱註 3， **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 進行站台間的資料庫複寫時，其中一個站台上的 SQL Server 必須直接與其父站台或子站台的 SQL Server 通訊。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server 服務|--|1433 (請參閱註 2，**可用的替代連接埠**)|  
|SQL Server Service Broker|--|4022 (請參閱註 2，**可用的替代連接埠**)|  

> [!TIP]  
>  Configuration Manager 不需要使用連接埠 UDP 1434 的 SQL Server 瀏覽器。  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> 狀態移轉點 -- > SQL Server  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|透過 TCP SQL|--|1433 (請參閱註 2，**可用的替代連接埠**)|  



###  <a name="BKMY_PortNotes"></a> Configuration Manager 用戶端和站台系統使用的連接埠附註  

1.  **Proxy 伺服器連接埠**：您無法設定此連接埠，但可以透過設定的 Proxy 伺服器進行路由。  

2.  **可用的替代連接埠**：您可以在 Configuration Manager 中定義此值的替代連接埠。 如果定義自訂連接埠，請在定義 IPsec 原則或設定防火牆的 IP 篩選器資訊時替代該自訂連接埠。  

3.  **Windows Server Update Services (WSUS)**：針對用戶端通訊，可以安裝 WSUS 以使用連接埠 80/443 或連接埠 8530/8531。 當您在 Windows Server 2012 或 Windows Server 2016 中執行 WSUS 時，預設會將 WSUS 設定為針對 HTTP 使用連接埠 8530，並針對 HTTPS 使用連接埠 8531。  

     安裝完成後，您可以變更連接埠。 您不需要在整個網站階層都使用相同的連接埠號碼。  

    -   如果 HTTP 連接埠是80，HTTPS 連接埠必須是 443。  

    -   如果 HTTP 連接埠使用其他任何號碼，則 HTTPS 連接埠必須比該連接埠號碼多 1 (或以上)，例如 8530 和 8531。   

    > [!NOTE]  
    >  當您設定軟體更新點使用 HTTPS 時，也必須開啟 HTTP 連接埠。 未加密的資料，例如特定更新的 EULA，會使用 HTTP 連接埠。  

4.  **Trivial FTP (TFTP) 精靈**：Trivial FTP (TFTP) 精靈系統服務不需要使用者名稱或密碼，而且是 Windows 部署服務 (WDS) 的一部分。 Trivial FTP 精靈服務支援下列 RFC 定義的 TFTP 通訊協定：  

    -   RFC 350：TFTP  

    -   RFC 2347：選項延伸模組  

    -   RFC 2348：區塊大小選項  

    -   RFC 2349：逾時間隔，以及傳輸大小選項  

     簡單式檔案傳輸通訊協定的設計可支援無磁碟開機環境。 TFTP 精靈會接聽 UDP 連接埠 69，但會從動態配置的高連接埠回應。 因此，啟用此連接埠可讓 TFTP 服務接收傳入的 TFTP 要求，但不會讓所選伺服器回應這些要求。 除非您將 TFTP 伺服器設為從連接埠 69 回應，否則無法讓所選伺服器回應輸入的 TFTP 要求。  

5.  **站台伺服器與站台系統之間的通訊**：根據預設，站台伺服器和站台系統之間的通訊是雙向的。 網站伺服器會起始通訊以設定網站系統，然後多數網站系統會連回網站伺服器以傳送狀態資訊。 Reporting Service 點及發佈點不會傳送狀態資訊。 安裝好站台系統後，如果您在站台系統內容中選取 [要求站台伺服器起始與此站台系統的連線]，站台系統將不會起始與站台伺服器的通訊。 反之，站台伺服器會起始通訊，並使用站台系統安裝帳戶來驗證站台系統伺服器。  

6.  **動態連接埠**：動態連接埠 (也稱為暫時連接埠) 會使用由作業系統版本定義的連接埠編號範圍。 如需有關預設連接埠範圍的詳細資訊，請參閱 [Windows Server 系統的服務概觀和網路連接埠需求](http://go.microsoft.com/fwlink/p/?LinkId=317965)。  

##  <a name="BKMK_AdditionalPorts"></a> 其他連接埠清單  
 下列各節提供有關 Configuration Manager 使用之連接埠的其他資訊。  

###  <a name="BKMK_ClientShares"></a> 用戶端對伺服器共用  
 用戶端一律使用伺服器訊息區塊 (SMB) 連線至 UNC 共用。 例如：  

-   指定 CCMSetup.exe **/source:** 命令列內容的手動用戶端安裝  

-   從 UNC 路徑下載定義檔案的 Endpoint Protection 用戶端

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|伺服器訊息區 (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> Microsoft SQL Server 的連線  
 如為 SQL Server 資料庫引擎和網站間複寫通訊，可以使用預設 SQL Server 連接埠或指定自訂連接埠：  

-   網站間通訊使用：  

    -   SQL Server Service Broker，預設為連接埠 TCP 4022。  

    -   SQL Server 服務，預設為連接埠 TCP 1433。  

-   SQL Server 資料庫引擎與不同 Configuration Manager 站台系統角色之間的站台內通訊預設為連接埠 TCP 1433。  

- Configuration Manager 使用相同的連接埠及通訊協定，與裝載站台資料庫的各個 SQL 可用性群組複本通訊，如同複本是獨立的 SQL Server 執行個體。

當您使用 Azure，而站台資料庫位於內部或外部負載平衡器後方時，請在各複本上設定下列防火牆例外，並為下列連接埠新增負載平衡規則：
 - 透過 TCP 的 SQL：TCP 1433
 - SQL Server Service Broker：TCP 4022
 - 伺服器訊息區 (SMB)：TCP 445
 - RPC 端點對應程式：TCP 135

> [!WARNING]  
>  Configuration Manager 不支援動態連接埠。 由於 SQL Server 具名執行個體預設使用動態連接埠連線至資料庫引擎，因此，當您使用具名執行個體時，必須手動設定要用於網站間通訊的靜態連接埠。  

 下列網站系統角色會直接與 SQL Server 資料庫通訊：  

-   應用程式類別目錄 Web 服務點  

-   憑證登錄點角色  

-   註冊點角色  

-   管理點  

-   網站伺服器  

-   Reporting Services 點  

-   SMS 提供者  

-   SQL Server --> SQL Server  

SQL Server 裝載來自多個網站的資料庫時，每個資料庫都必須使用不同的 SQL Server 執行個體，而且每個執行個體都必須設定一組唯一的連接埠。  

如果 SQL Server 電腦上有啟用防火牆，請務必將防火牆設為允許部署使用連接埠。 此外，請將位於網路 (與 SQL Server 通訊的電腦之間的網路) 上其他位置的防火牆，設為允許上述相同連接埠。  

如需如何將 SQL Server 設為使用特定連接埠的範例，請參閱 SQL Server TechNet 文件庫中的 [如何：將伺服器設為在特定 TCP 連接埠上接聽 (SQL Server 組態管理員)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 。  


### <a name="bkmk_discovery"> </a> 探索和發行
下列連接埠用於探索和發行站台資訊：
 - 輕量型目錄存取通訊協定 (LDAP)：389
 - LDAP (安全通訊端層 [SSL] 連線)：636


 - 通用類別目錄 LDAP：3268
 - 通用類別目錄 LDAP SSL：3269


 - RPC 端點對應程式：135
 - RPC：動態配置的高 TCP 連接埠


 - TCP: 1024: 5000
 - TCP:  49152: 65535


###  <a name="BKMK_External"></a> Configuration Manager 進行的外部連線  
 Configuration Manager 用戶端或站台系統可以進行下列外部連線：  

-   [Asset Intelligence 同步處理點 -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Endpoint Protection 點 -- &gt; 網際網路](#BKMK_PortsEndpointProtection_Internet)  

-   [用戶端 -- &gt; 通用類別目錄網域控制站](#BKMK_PortsClient-GCDC)  

-   [Configuration Manager 主控台 -- &gt; 網際網路](#BKMK_PortsConsole-Internet)  

-   [管理點 -- &gt; 網域控制站](#BKMK_PortsMP-DC)  

-   [站台伺服器 -- &gt; 網域控制站](#BKMK_PortsSite-DC)  

-   [站台伺服器 &lt; -- &gt; 發行憑證授權單位 (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [軟體更新點 -- &gt; 網際網路](#BKMK_PortsSUP-Internet)  

-   [軟體更新點 -- &gt; 上游 WSUS 伺服器](#BKMK_PortsSUP-WSUS)  

-   [服務連接點 -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> 支援以網際網路為基礎的用戶端之站台系統的安裝需求  
 支援以網際網路為基礎之用戶端的管理點和發佈點、軟體更新點，以及備援狀態點均使用下列連接埠進行安裝及修復：  

-   站台伺服器 --> 站台系統：使用 UDP 和 TCP 連接埠 135 的 RPC 端點對應程式。  

-   站台伺服器 --> 站台系統：RPC 動態 TCP 連接埠。  

-   站台伺服器 &lt; --> 站台系統：使用 TCP 連接埠 445 的伺服器訊息區塊 (SMB)。

發佈點上的應用程式和套件安裝需要下列 RPC 連接埠：  

-   站台伺服器 --> 發佈點：使用 UDP 和 TCP 連接埠 135 的 RPC 端點對應程式。

-   站台伺服器 --> 發佈點：RPC 動態 TCP 連接埠。  

使用 IPsec 協助保護網站伺服器和網站系統之間的流量。 如果必須限制與 RPC 搭配使用的動態連接埠，可以使用 Mircrosoft RPC 設定工具 (rpccfg.exe) 為這些 RPC 封包設定有限的連接埠範圍。 如需 RPC 設定工具的詳細資訊，請參閱 [如何設定 RPC 使用特定連接埠，以及如何使用 IPsec 以協助保護這些連接埠](http://go.microsoft.com/fwlink/p/?LinkId=124096)。  

> [!IMPORTANT]  
>  安裝這些站台系統之前，請確認站台系統伺服器上正在執行遠端登錄服務；如果站台系統在另一個沒有信任關係的 Active Directory 樹系中，則需確認您已指定站台系統安裝帳戶。  

###  <a name="BKMK_PortsClientInstall"></a> Configuration Manager 用戶端安裝使用的連接埠  
安裝用戶端期間所使用的連接埠依用戶端部署方法而有所不同。 如需每種用戶端部署方法的連接埠清單，請參閱 [System Center Configuration Manager 中用戶端適用的 Windows 防火牆和連接埠設定](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)主題中的 **Configuration Manager 用戶端部署期間使用的連接埠**。 如需如何在用戶端上設定 Windows 防火牆以進行用戶端安裝及安裝後通訊的詳細資訊，請參閱 [System Center Configuration Manager 中用戶端適用的 Windows 防火牆和連接埠設定](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)。  

###  <a name="BKMK_MigrationPorts"></a> 移轉使用的連接埠  
執行移轉的站台伺服器會在來源階層使用數個連接埠連接至適用的站台，以收集從來源站台 SQL Server 資料庫取得的資料，並共用發佈點。  

 如需這些連接埠的資訊，請參閱[在 System Center 2012 Configuration Manager 中進行移轉的必要條件](../../../core/migration/prerequisites-for-migration.md)主題中的[移轉的必要設定](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations)一節。  

###  <a name="BKMK_ServerPorts"></a> Windows Server 使用的連接埠  
 下表列出 Windows Server 使用的部分重要連接埠及其功能。 如需完整的 Windows Server 服務和網路連接埠需求清單，請參閱 [Windows Server 系統的服務概觀和網路連接埠需求](http://go.microsoft.com/fwlink/p/?LinkID=123652)。  

|說明|UDP|TCP|  
|-----------------|---------|---------|  
|網域名稱系統 (DNS)|53|53|  
|動態主機設定通訊協定 (DHCP)|67 和 68|--|  
|NetBIOS 名稱解析|137|--|  
|NetBIOS Datagram Service|138|--|  
|NetBIOS Session Service|--|139|  
