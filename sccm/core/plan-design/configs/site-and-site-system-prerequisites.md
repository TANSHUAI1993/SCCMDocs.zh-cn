---
title: "站台必要條件 | Microsoft Docs"
description: "了解如何將 Windows 電腦設定為 System Center Configuration Manager 站台系統伺服器。"
ms.custom: na
ms.date: 1/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0b1d2d619d6cdaf36cc22ef461ea1505b5cacc41
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>System Center Configuration Manager 的站台和站台系統必要條件

*適用於：System Center Configuration Manager (最新分支)*


 Windows 電腦需要特定的設定，以支援當成 System Center Configuration Manager 站台系統伺服器來使用。  


 針對某些產品 (例如軟體更新點的 Windows Server Update Services (WSUS))，您需要參閱該產品文件來識別該產品使用的其他必要條件和限制。 這裡只包含直接套用以與 Configuration Manager 搭配使用的設定。   

> [!NOTE]  
>  針對 .NET Framework 4.0、4.5 與 4.5.1 的支援已於 2016 年 1 月到期。 如需詳細資訊，請參閱位於 support.microsoft.com 中的 [週期支援原則常見問題集 - Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) 。  

## <a name="bkmk_generalprerewq"></a> 一般站台伺服器需求和限制
**下列適用於所有站台系統伺服器：**

-   每個站台系統伺服器必須使用 64 位元作業系統。 唯一的例外是發佈點站台系統角色，您可以將它安裝在部分的 32 位元作業系統上。  

-   任何作業系統的 Server Core 安裝上不支援站台系統。 例外狀況是發佈點站台系統角色支援 Server Core 安裝，而沒有支援 PXE 或多點傳送。  

-   安裝站台系統伺服器之後，不支援變更：  

    -   站台系統電腦所在網域的網域名稱 (也稱為**網域重新命名**)。  

    -   電腦的網域成員資格。  

    -   電腦的名稱。  

  如果您必須變更其中任何一項，您必須先從電腦移除站台系統角色，然後在變更完成之後重新安裝角色。 如果這會影響站台伺服器電腦，您必須解除安裝站台，然後在變更完成之後重新安裝站台。  

-   Windows Server 叢集執行個體上不支援站台系統角色。 唯一的例外是站台資料庫伺服器。  

-   不支援變更任何 Configuration Manager 服務的啟動類型或 [登入身分] 設定。 如果這麼做，可能會導致重要服務無法正確執行。  

##  <a name="bkmk_2012Prereq"></a> Windows Server 2012 和更新版本作業系統的必要條件  
###  <a name="bkmk_2012sspreq"></a> 站台伺服器：管理中心網站和主要站台  
  **Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

-   遠端差異壓縮  

**Windows ADK：**  

-   在您安裝或升級管理中心網站或主要站台之前，您必須安裝您正在安裝或升級之 Configuration Manager 目標版本所需要的 Windows 評定及部署套件 (ADK) 版本。  

    -   Configuration Manager 1511 版需要 Windows 10 RTM (10.0.10240) 版本的 Windows ADK。  

-   如需此需求的詳細資訊，請參閱[作業系統部署的基礎結構需求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會將 Microsoft Visual C++ 2013 可轉散發套件安裝在要安裝站台伺服器的每部電腦上。  

-   管理中心網站和主要站台需要適用之可轉散發檔案的 x86 和 x64 版本。  

###  <a name="bkmk_2012secpreq"></a> 站台伺服器：次要站台  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

-   遠端差異壓縮  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會將 Microsoft Visual C++ 2013 可轉散發套件安裝在要安裝站台伺服器的每部電腦上。  

-   次要站台只需要 x64 版本。  

**預設站台系統角色：**  

-   根據預設，次要站台會安裝**管理點**和**發佈點**。  

-   請確定次要站台伺服器符合這些站台系統角色的必要條件。  

###  <a name="bkmk_2012dbpreq"></a> 資料庫伺服器  
**遠端登錄服務：**  

-   在安裝 Configuration Manager 站台期間，您必須在裝載站台資料庫的電腦上啟用遠端登錄服務。  

**SQL Server：**  

-   在您安裝管理中心網站或主要站台之前，您必須安裝支援的 SQL Server 版本來裝載站台資料庫。  

-   安裝次要站台之前，您可以安裝支援的 SQL Server 版本。  

-   如果您選擇讓 Configuration Manager 安裝 SQL Server Express 作為次要站台安裝的一部分，請確定電腦是否符合執行 SQL Server Express 的需求。  

###  <a name="bkmk_2012smsprovpreq"></a> SMS 提供者伺服器  
**Windows ADK：**  

-   安裝 SMS 提供者執行個體的電腦必須具有您正在安裝或升級之 Configuration Manager 目標版本所需要的 Windows ADK 版本。  

    -   Configuration Manager 1511 版需要 Windows 10 RTM (10.0.10240) 版本的 Windows ADK。  

-   如需此需求的詳細資訊，請參閱[作業系統部署的基礎結構需求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

###  <a name="bkmk_2012acwspreq"></a> 應用程式類別目錄網站點  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2：  

    -   ASP.NET 4.5  

**IIS 設定：**  

-   一般 HTTP 功能：  

    -   預設文件  

    -   靜態內容  

-   應用程式開發：  

    -   ASP.NET 3.5 (及自動選取的選項)  

    -   ASP.NET 4.5 (及自動選取的選項)  

    -   .NET 擴充性 3.5  

    -   .NET 擴充性 4.5  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

###  <a name="bkmk_2012ACwsitepreq"></a> 應用程式類別目錄 Web 服務點  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2：  

    -   ASP.NET 4.5：  

        -   HTTP 啟動 (及自動選取的選項)  

**IIS 設定：**  

-   一般 HTTP 功能：  

    -   預設文件  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

-   應用程式開發：  

    -   ASP.NET 3.5 (及自動選取的選項)  

    -   .NET 擴充性 3.5  

    -   ASP.NET 4.5 (及自動選取的選項)  

    -   .NET 擴充性 4.5  

**電腦記憶體：**  

-   裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

-   此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

###  <a name="bkmk_2012AIpreq"></a> Asset Intelligence 同步處理點  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2012crppreq"></a> 憑證登錄點  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2：  

    -   HTTP 啟動  

**IIS 設定：**  

-   應用程式開發：  

    -   ASP.NET 3.5 (及自動選取的選項)  

    -   ASP.NET 4.5 (及自動選取的選項)  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

    -   IIS 6 WMI 相容性  

###  <a name="bkmk_2012dppreq"></a> 發佈點  
**Windows Server 角色和功能：**  

-   遠端差異壓縮  

**IIS 設定：**  

-   應用程式開發：  

    -   ISAPI 擴充程式  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

    -   IIS 6 WMI 相容性  

**PowerShell：**  

-   於 Windows Server 2012 或更新版本上，在您安裝發佈點之前需要 PowerShell 3.0 或 4.0。  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會在裝載發佈點的每部電腦上安裝 Microsoft Visual C++ 2013 可轉散發套件。  

-   安裝的版本取決於電腦平台 (x86 或 x64)。  

**Microsoft Azure：**  

-   您可以使用 Microsoft Azure 中的雲端服務來裝載發佈點。  

**支援 PXE 或多點傳送：**  

-   安裝和設定 Windows 部署服務 (WDS) Windows Server 角色。  

    > [!NOTE]  
    >  當您設定發佈點以在執行 Windows Server 2012 或更新版本的伺服器上支援 PXE 或多點傳送時，WDS 會自動安裝與設定。  

> [!NOTE]  
> 發佈點站台系統角色不需要背景智慧型傳送服務 (BITS)。 在發佈點電腦上設定 BITS 時，發佈點電腦上的 BITS 不會用來協助使用 BITS 的用戶端下載內容。  

###  <a name="bkmk_2012EPPpreq"></a> Endpoint Protection 點  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

###  <a name="bkmk_2012Enrollpreq"></a> 註冊點  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 (或更新版本)  

-   .NET Framework 4.5.2：  

     此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 當 .NET Framework 的重新開機擱置中時，在伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

    -   HTTP 啟動 (及自動選取的選項)  

    -   ASP.NET 4.5  


**IIS 設定：**  

-   一般 HTTP 功能：  

    -   預設文件  

-   應用程式開發：  

    -   ASP.NET 3.5 (及自動選取的選項)  

    -   .NET 擴充性 3.5  

    -   ASP.NET 4.5 (及自動選取的選項)  

    -   .NET 擴充性 4.5  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

**電腦記憶體：**  

-   裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

-   此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

###  <a name="bkmk_2012EnrollProxpreq"></a> 註冊 Proxy 點  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 (或更新版本)  

-   .NET Framework 4.5.2  

     此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 當 .NET Framework 的重新開機擱置中時，在伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

**IIS 設定：**  

-   一般 HTTP 功能：  

    -   預設文件  

    -   靜態內容  

-   應用程式開發：  

    -   ASP.NET 3.5 (及自動選取的選項)  

    -   ASP.NET 4.5 (及自動選取的選項)  

    -   .NET 擴充性 3.5  

    -   .NET 擴充性 4.5  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

**電腦記憶體：**  

-   裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

-   此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

###  <a name="bkmk_2012FSPpreq"></a> 後援狀態點  
需要預設 IIS 設定，再加上下列各項：  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

###  <a name="bkmk_2012MPpreq"></a> 管理點  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

-   BITS 伺服器擴充功能 (和自動選取的選項) 或背景智慧型傳送服務 (BITS) (及自動選取的選項)  

**IIS 設定：**  

-   應用程式開發：  

    -   ISAPI 擴充程式  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

    -   IIS 6 WMI 相容性  

###  <a name="bkmk_2012RSpoint"></a> Reporting Services 點  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services：**  

-   您必須安裝並設定至少一個 SQL Server 執行個體以支援 SQL Server Reporting Services，才能安裝 Reporting Services 點。  

-   您用於 SQL Server Reporting Services 的執行個體可以是用於站台資料庫的相同執行個體。  

-   此外，您使用的執行個體可以與其他 System Center 產品共用，只要其他 System Center 產品不限制共用 SQL Server 執行個體即可。  

###  <a name="bkmk_SCPpreq"></a> 服務連接點  
**Windows Server 角色和功能：**  

-   .NET Framework 4.5.2  

     此站台系統角色安裝時，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 當 .NET Framework 的重新開機擱置中時，在伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會在裝載發佈點的每部電腦上安裝 Microsoft Visual C++ 2013 可轉散發套件。  

-   站台系統角色需要使用 x64 版本。  

###  <a name="bkmk_2012SUPpreq"></a> 軟體更新點  
**Windows Server 角色和功能：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

需要預設 IIS 設定。

**Windows Server Update Services：**  

-   您必須在電腦上安裝 Windows Server 角色 Windows Server Update Services，才能安裝軟體更新點。  

-   如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。  

### <a name="state-migration-point"></a>狀態移轉點  
需要預設 IIS 設定。  

##  <a name="bkmk_2008"></a> Windows Server 2008 R2 和 Windows Server 2008 的必要條件  
Windows Server 2008 和 Windows Server 2008 R2 現在屬於延伸支援，而不再屬於主流支援，如 [Microsoft 支援週期](https://support.microsoft.com/lifecycle)中詳述。 如需這些作業系統作為 Configuration Manager 站台系統伺服器的未來支援詳細資訊，請參閱 [System Center Configuration Manager 的已移除和已淘汰功能](../../../core/plan-design/changes/removed-and-deprecated-features.md)。  

**以下適用於所有 .NET Framework 需求：**  

-   安裝 .NET Framework 的完整版本，然後才能安裝站台系統角色。 例如，請參閱 [Microsoft .NET Framework 4 (獨立安裝程式)](http://go.microsoft.com/fwlink/p/?LinkId=193048)。 .NET Framework 4 Client Profile 不足以滿足這項需求。  

**以下適用於所有 Windows Communication Foundation (WCF) 啟動需求：**  

-   您可以設定 WCF 啟動，做為站台系統伺服器上 .NET Framework Windows 功能的一部分。 例如，在 Windows Server 2008 R2 上，執行 [新增功能精靈] 以在伺服器上安裝其他功能。 在 [選取功能] 頁面上，依序展開 [NET Framework 3.5.1 功能] 和 [WCF 啟動]，然後核取 [HTTP 啟動] 和 [非 HTTP 啟動] 方塊，啟用這些選項。  

###  <a name="bkmk_2008sspreq"></a> 站台伺服器：管理中心網站和主要站台  
**.NET Framework：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

**Windows 功能：**  

-   遠端差異壓縮  

**Windows ADK：**  

-   在您安裝或升級管理中心網站或主要站台之前，您必須安裝您正在安裝或升級之 Configuration Manager 目標版本所需要的 Windows ADK 版本。  

    -   Configuration Manager 1511 版需要 Windows 10 RTM (10.0.10240) 版本的 Windows ADK。  

-   如需此需求的詳細資訊，請參閱[作業系統部署的基礎結構需求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會將 Microsoft Visual C++ 2013 可轉散發套件安裝在要安裝站台伺服器的每部電腦上。  

-   管理中心網站和主要站台需要適用之可轉散發檔案的 x86 和 x64 版本。  

###  <a name="bkmk_2008secpreq"></a> 站台伺服器：次要站台  
**.NET Framework：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會將 Microsoft Visual C++ 2013 可轉散發套件安裝在要安裝站台伺服器的每部電腦上。  

-   次要站台只需要 x64 版本。  

**預設站台系統角色：**  

-   根據預設，次要站台會安裝**管理點**和**發佈點**。  

-   請確定次要站台伺服器符合這些站台系統角色的必要條件。  

###  <a name="bkmk_2008dbpreq"></a> 資料庫伺服器  
**遠端登錄服務：**  

-   在安裝 Configuration Manager 站台期間，您必須在裝載站台資料庫的電腦上啟用遠端登錄服務。  

**SQL Server：**  

-   在您安裝管理中心網站或主要站台之前，您必須安裝支援的 SQL Server 版本來裝載站台資料庫。  

-   安裝次要站台之前，您可以安裝支援的 SQL Server 版本。  

-   如果您選擇讓 Configuration Manager 安裝 SQL Server Express 作為次要站台安裝的一部分，請確定電腦是否符合執行 SQL Server Express 的需求。  

###  <a name="bkmk_2008smsprovpreq"></a> SMS 提供者伺服器  
**Windows ADK：**  

-   安裝 SMS 提供者執行個體的電腦必須具有您正在安裝或升級之 Configuration Manager 目標版本所需要的 Windows ADK 版本。  

    -   Configuration Manager 1511 版需要 Windows 10 RTM (10.0.10240) 版本的 Windows ADK。  

-   如需此需求的詳細資訊，請參閱[作業系統部署的基礎結構需求](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment)。  

###  <a name="bkmk_2008acwspreq"></a> 應用程式類別目錄網站點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

**IIS 設定：**

需要預設 IIS 設定，再加上下列各項：  

-   一般 HTTP 功能：  

    -   靜態內容  

    -   預設文件  

-   應用程式開發：  

    -   ASP.NET (及自動選取的選項)  

         在某些情況下，例如安裝 IIS 時或在安裝 .NET Framework 4.5.2 版之後重新設定 IIS 時，您必須明確啟用 ASP.NET 4.5 版。 例如，在執行 .NET Framework 4.0.30319 版的 64 位元電腦上，執行下列命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

###  <a name="bkmk_2008ACwsitepreq"></a> 應用程式類別目錄 Web 服務點  
**.NET Framework：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

**Windows Communication Foundation (WCF) 啟動：**  

-   HTTP 啟動  

-   非 HTTP 啟動  

**IIS 設定：**

需要預設 IIS 設定，再加上下列各項：  

-   應用程式開發：  

    -   ASP.NET (及自動選取的選項)  

         在某些情況下，例如安裝 IIS 時或在安裝 .NET Framework 4.5.2 版之後重新設定 IIS 時，您必須明確啟用 ASP.NET 4.5 版。 例如，在執行 .NET Framework 4.0.30319 版的 64 位元電腦上，執行下列命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

**電腦記憶體：**  

-   裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

-   此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

###  <a name="bkmk_2008AIpreq"></a> Asset Intelligence 同步處理點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2008crppreq"></a> 憑證登錄點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

-   HTTP 啟動  

**IIS 設定：**

需要預設 IIS 設定，再加上下列各項：  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

    -   IIS 6 WMI 相容性  

###  <a name="bkmk_2008dppreq"></a> 發佈點  
**IIS 設定：**

您可以使用預設 IIS 設定或自訂設定。 若要使用自訂的 IIS 組態，您必須啟用 IIS 的下列選項：  

-   應用程式開發：  

    -   ISAPI 擴充程式  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

    -   IIS 6 WMI 相容性  

當您使用自訂的 IIS 設定時，您可以移除不必要的選項，如下所示：  

-   一般 HTTP 功能：  

    -   HTTP 重新導向  

-   IIS 管理指令碼及工具  

**Windows 功能：**  

-   遠端差異壓縮  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會在裝載發佈點的每部電腦上安裝 Microsoft Visual C++ 2013 可轉散發套件。  

-   安裝的版本取決於電腦平台 (x86 或 x64)。  

**Microsoft Azure：**  

-   您可以使用 Azure 中的雲端服務來裝載發佈點。  

**支援 PXE 或多點傳送：**  

-   安裝和設定 Windows 部署服務 (WDS) Windows Server 角色。  

    > [!NOTE]  
    >  當您設定發佈點以在執行 Windows Server 2012 或更新版本的伺服器上支援 PXE 或多點傳送時，WDS 會自動安裝與設定。  

> [!NOTE]  
> 發佈點站台系統角色不需要背景智慧型傳送服務 (BITS)。 在發佈點電腦上設定 BITS 時，發佈點電腦上的 BITS 不會用來協助使用 BITS 的用戶端下載內容。  


###  <a name="bkmk_2008EPPpreq"></a> Endpoint Protection 點  
**.NET Framework：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

###  <a name="bkmk_2008Enrollpreq"></a> 註冊點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

     此站台系統角色安裝時，如果伺服器還沒有安裝支援的 .NET Framework 版本，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 當 .NET Framework 的重新開機擱置中時，在伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

**Windows Communication Foundation (WCF) 啟動：**  

-   HTTP 啟動  

-   非 HTTP 啟動  

**IIS 設定：**

需要預設 IIS 設定，再加上下列各項：  

-   應用程式開發：  

    -   ASP.NET (及自動選取的選項)  

         在某些情況下，例如安裝 IIS 時或在安裝 .NET Framework 4.5.2 版之後重新設定 IIS 時，您必須明確啟用 ASP.NET 4.5 版。 例如，在執行 .NET Framework 4.0.30319 版的 64 位元電腦上，執行下列命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**電腦記憶體：**  

-   裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

-   此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

###  <a name="bkmk_2008EnrollProxpreq"></a> 註冊 Proxy 點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

     此站台系統角色安裝時，如果伺服器還沒有安裝支援的 .NET Framework 版本，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 當 .NET Framework 的重新開機擱置中時，在伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

**Windows Communication Foundation (WCF) 啟動：**  

-   HTTP 啟動  

-   非 HTTP 啟動  

**IIS 設定：**

需要預設 IIS 設定，再加上下列各項：  

-   應用程式開發：  

    -   ASP.NET (及自動選取的選項)  

         在某些情況下，例如安裝 IIS 時或在安裝 .NET Framework 4.5.2 版之後重新設定 IIS 時，您必須明確啟用 ASP.NET 4.5 版。 例如，在執行 .NET Framework 4.0.30319 版的 64 位元電腦上，執行下列命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**電腦記憶體：**  

-   裝載此站台系統角色的電腦必須有至少 5% 的電腦可用記憶體可用來讓站台系統角色處理要求。  

-   此站台系統角色與另一個需求相同的站台系統角色共存時，電腦的這項記憶體需求不會增加，而會保持在最少 5%。  

###  <a name="bkmk_2008FSPpreq"></a> 後援狀態點  
**IIS 設定：**

需要預設 IIS 設定，再加上下列各項：  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

###  <a name="bkmk_2008MPpreq"></a> 管理點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

**IIS 設定：**

您可以使用預設 IIS 設定或自訂設定。 每個您啟用來支援行動裝置的管理點，需要針對 ASP.NET 進行額外的 IIS 組態 (和其自動選取的選項)。

在某些情況下，例如安裝 IIS 時或在安裝 .NET Framework 4.5.2 版之後重新設定 IIS 時，您必須明確啟用 ASP.NET 4.5 版。 例如，在執行 .NET Framework 4.0.30319 版的 64 位元電腦上，執行下列命令：**%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  


若要使用自訂的 IIS 組態，您必須啟用 IIS 的下列選項：  

-   應用程式開發：  

    -   ISAPI 擴充程式  

-   安全性：  

    -   Windows 驗證  

-   IIS 6 管理相容性：  

    -   IIS 6 Metabase 相容性  

    -   IIS 6 WMI 相容性  


當您使用自訂的 IIS 設定時，您可以移除不必要的選項，如下所示：  

-   一般 HTTP 功能：  

    -   HTTP 重新導向  

-   IIS 管理指令碼及工具  

**Windows 功能：**  

-   BITS 伺服器擴充功能 (和自動選取的選項) 或背景智慧型傳送服務 (BITS) (及自動選取的選項)  

###  <a name="bkmk_2008RSpoint"></a> Reporting Services 點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services：**  

-   您必須安裝並設定至少一個 SQL Server 執行個體以支援 SQL Server Reporting Services，才能安裝 Reporting Services 點。  

-   您用於 SQL Server Reporting Services 的執行個體可以是用於站台資料庫的相同執行個體。  

-   此外，您使用的執行個體可以與其他 System Center 產品共用，只要其他 System Center 產品不限制共用 SQL Server 執行個體即可。  

###  <a name="bkmk_2008SCPpreq"></a> 服務連接點  
**.NET Framework：**  

-   .NET Framework 4.5.2  

     此站台系統角色安裝時，如果伺服器還沒有安裝支援的 .NET Framework 版本，Configuration Manager 會自動安裝 .NET Framework 4.5.2。 此安裝可以將伺服器置於重新開機擱置狀態。 當 .NET Framework 的重新開機擱置中時，在伺服器重新開機且安裝完成之前，.NET 應用程式可能會失敗。  

**Visual C++ 可轉散發套件：**  

-   Configuration Manager 會在裝載發佈點的每部電腦上安裝 Microsoft Visual C++ 2013 可轉散發套件。  

-   站台系統角色需要使用 x64 版本。  

###  <a name="bkmk_2008SUPpreq"></a> 軟體更新點  
**.NET Framework：**  

-   .NET Framework 3.5 SP1 (或更新版本)  

-   .NET Framework 4.5.2  

**IIS 設定：**

需要預設 IIS 設定。  

**Windows Server Update Services：**  

-   您必須在電腦上安裝 Windows Server 角色 Windows Server Update Services，才能安裝軟體更新點。  

-   如需詳細資訊，請參閱[在 System Center Configuration Manager 中規劃軟體更新](../../../sum/plan-design/plan-for-software-updates.md)。

###  <a name="bkmk_2008SMPpreq"></a> 狀態移轉點  
**IIS 設定：**

需要預設 IIS 設定。  
