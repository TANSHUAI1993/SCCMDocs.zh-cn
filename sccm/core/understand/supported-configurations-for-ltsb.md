---
title: "支援的 LTSB 設定 | Microsoft Docs"
description: "了解哪些作業系統和相依產品與 System Center Configuration Manager 的長期維護分支搭配運作。"
ms.custom: na
ms.date: 5/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 31bddee83b2365cfa903077ffaa1d7116b194378
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 長期維護分支的支援設定

*適用於：System Center Configuration Manager (長期維護分支)*

本主題中的資訊可用來了解 Configuration Manager 長期維護分支 (LTSB) 所支援的作業系統和產品相依性。
如果未在本主題或 LTSB 特定主題中指出，則套用至最新分支 1606 版的相同設定和限制也會套用至 LTSB。  發生衝突時，請使用適用於您所使用版本的資訊。 一般而言，LTSB 比最新分支更為受限。

## <a name="general-statement-of-support"></a>一般支援陳述
此 Configuration Manager 分支支援下列產品和技術。 不過，本內容對這些產品和技術的包含，並不代表對任何產品或版本超出產品個別支援週期的支援延伸。 已超出其支援週期的產品不支援搭配 Configuration Manager 使用。 如需詳細資訊，請前往 [Microsoft 支援週期](http://go.microsoft.com/fwlink/p/?LinkId=208270)網站，並閱讀 [Microsoft 支援週期原則 - 常見問題集](http://go.microsoft.com/fwlink/p/?LinkId=31976)。

此外，除非已在 [Enterprise Mobility + Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/) (企業行動力 + 安全性部落格) 上公告下列主題中未列出的產品和產品版本，否則不予支援。

**未來支援的限制：**LTSB 具有未來伺服器和用戶端作業系統和產品相依性的有限支援。 在版本的生命週期，LTSB 的平台清單是固定的︰

**Windows：**
- 只會支援 Windows 的品質和安全性更新。
- 不支援最新分支 (CB)、最新商務分支 (CBB) 或 Windows 10 的 LTSB。
-   不支援 Windows Server 的新主要版本。

**SQL Server：**
- SQL Server 僅支援品質和安全性更新或次要升級 (例如 Service Pack)。
- 不支援 SQL Server 的新主要版本。  

## <a name="site-systems-and-servers"></a>站台系統和伺服器
LTSB 支援使用下列 Windows 電腦作業系統作為站台系統。  每個作業系統都有與[支援的站台系統伺服器作業系統](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)中相同項目相同的需求和限制。  例如，Windows 2012 R2 的 Server Core 安裝必須是 x64 版本、僅支援裝載發佈點，而且不支援 PXE 或多點傳送。

**支援的作業系統：**
- Windows Server 2016
- Windows Server 2012 R2 (x64)：Standard、Datacenter
- Windows Server 2012 (x64)：Standard、Datacenter
- Windows Server 2008 R2 (含 SP1) (x64)：Standard、Enterprise、Datacenter
- Windows Server 2008 (含 SP2) (x86、x64)：Standard、Enterprise、Datacenter *(請參閱註 1)*
- Windows 10 Enterprise 2015 LTSB (x86、x64)
- Windows 10 Enterprise 2016 LTSB (x86、x64)
- Windows 8.1 (x86、x64)：專業版、企業版
- Windows 7 (含 SP1) (x86、x64)：專業版、企業版、旗艦版
- Windows Server 2012 的 Server Core 安裝
- Windows Server 2012 R2 的 Server Core 安裝    

*註 1*︰此作業系統不支援站台伺服器或站台系統角色，但發佈點和提取發佈點為例外。 您能持續將此作業系統作為發佈點使用，直到宣告此項支援已遭取代，或此作業系統的延伸支援期限過期。 如需詳細資訊，請參閱 [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (在 Windows Server 2008 上安裝 System Center Configuration Manager CB 和 LTSB 失敗)。

## <a name="client-management"></a>用戶端管理
下列各節識別您可以使用 LTSB 管理的用戶端作業系統。 LTSB 不支援將新的作業系統新增為支援的用戶端。

### <a name="windows-computers"></a>Windows 電腦
您可以使用 LTSB，利用 Configuration Manage 包含的 Configuration Manager 用戶端軟體來管理下列 Windows 電腦作業系統。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。

**支援的作業系統：**
- Windows Server 2016
- Windows Server 2012 R2 (x64)：Standard、Datacenter (附註 1)
- Windows Server 2012 (x64)：Standard、Datacenter (附註 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 (含 SP1) (x64)：Standard、Enterprise、Datacenter (附註 1)
- Windows Storage Server 2008 R2 (x86、x64)：Workgroup、Standard、Enterprise
- Windows Server 2008 (含 SP2) (x86、x64)：Standard、Enterprise、Datacenter (附註 1)
- Windows 10 Enterprise 2015 LTSB (x86、x64)
- Windows 10 Enterprise 2016 LTSB (x86、x64)
- Windows 8.1 (x86、x64)：專業版、企業版
- Windows 7 (含 SP1) (x86、x64)：專業版、企業版、旗艦版
- Windows Server 2012 R2 的 Server Core 安裝 (x64) (附註 2)
- Windows Server 2012 的 Server Core 安裝 (x64) (附註 2)
- Windows Server 2008 R2 SP1 的 Server Core 安裝 (x64)
- Windows Server 2008 SP2 的 Server Core 安裝 (x86、x64)

**(附註 1)** Datacenter 版本受到支援，但未經 Configuration Manager 認證。  
**(附註 2)** 為了支援用戶端推入安裝，執行此作業系統版本的電腦必須執行檔案和存放服務伺服器角色的檔案伺服器角色服務。 如需在 Server Core 電腦上安裝 Windows 功能的相關資訊，請參閱 Windows Server 2012 TechNet 文件庫中的[在 Server Core 伺服器上安裝伺服器角色和功能](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx)。

### <a name="windows-embedded"></a>Windows Embedded
您可以使用 LTSB，以在裝置上安裝用戶端軟體來管理下列 Windows Embedded 裝置。  如需詳細資訊，請參閱[規劃將用戶端部署至 System Center Configuration Manager 中的 Windows Embedded 裝置](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices)。

**需求和限制：**  

-   在未啟用寫入篩選器的支援 Windows Embedded 系統上，會支援用戶端的所有功能。  

-   針對所有功能 (電源管理除外)，支援使用下列其中一項的用戶端：  

    -   增強式寫入篩選器 (EWF)    

    -   RAM 檔案型寫入篩選器 (FBWF)    

    -   整合寫入篩選器 (UWF)  

-   所有 Windows Embedded 裝置都不支援應用程式類別目錄。  

-   您必須先在內嵌裝置上安裝 Microsoft Windows WMI 指令碼封裝，才能在以 Windows XP 為基礎的 Windows Embedded 裝置上監視偵測到的惡意程式碼。 使用 Windows Embedded Target Designer 安裝這個封裝。 *WBEMDISP.DLL* 和 *WBEMDISP.TLB* 檔案必須存在，且在內嵌裝置的 %windir%\System32\WBEM 資料夾中註冊，以確保會報告偵測到的惡意程式碼。  

**支援的作業系統：**  
-   Windows 10 Enterprise 2016 LTSB (x86、x64)  
-   Windows 10 Enterprise 2015 LTSB (x86、x64)  
-   Windows Embedded 8.1 Industry (x86、x64)    
-   Windows Thin PC (x86、x64)    
-   Windows Embedded POSReady 7 (x86、x64)    
-   Windows Embedded Standard 7 (含 SP1) (x86、x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 您可以使用 Configuration Manager 包含的舊版 Configuration Manager 行動裝置用戶端來管理 Windows CE 裝置。  

**需求和限制：**  

-   行動裝置用戶端需要 0.78 MB 的儲存空間來安裝用戶端。 行動裝置可能需要最多 256 KB 的額外儲存空間才能登入。    

-   這些行動裝置的功能因平台和用戶端類型而異。 如需 Configuration Manager 針對行動裝置舊版用戶端所支援之管理功能類型的資訊，請參閱[選擇 System Center Configuration Manager 的裝置管理解決方案](/sccm/core/plan-design/choose-a-device-management-solution)。  

**支援的作業系統：**  

-   Windows CE 7.0 (ARM 和 x86 處理器)  

**支援的語言包括：**  
-   中文 (簡體及繁體)    
-   英文 (美國)    
-   法文 (法國)    
-   德文    
-   義大利文    
-   日文  
-   韓文  
-   葡萄牙文 (巴西)  
-   俄文  
-   西班牙文 (西班牙)  

### <a name="mac-computers"></a>Mac 電腦  
 您可以使用 LTSB，利用適用於 Mac 的 Configuration Manager 用戶端來管理 Mac OS X 電腦。

Configuration Manager 媒體不提供 Mac 用戶端安裝套件。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=525184)作為「其他作業系統的用戶端」下載的一部分來下載。  

Mac 作業系統支援僅限本節所列的作業系統， 並不包含最新分支之未來 Mac 用戶端安裝套件更新可能支援的其他作業系統。

如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)。

**支援的版本：**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux 和 UNIX 伺服器
您可以使用 LTSB，利用適用於 Linux 和 UNIX 的 Configuration Manager 用戶端來管理 Linux 和 UNIX 電腦。

Configuration Manager 媒體不提供 Linux 和 UNIX 用戶端安裝套件。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=525184)作為「其他作業系統的用戶端」下載的一部分來下載。 除了用戶端安裝套件外，所下載的用戶端也包括特定的安裝指令碼，可用來管理各電腦上用戶端的安裝程序。

Linux 和 UNIX 作業系統支援僅限本節所列的作業系統， 並不包含最新分支之未來 Linux 和 UNIX 用戶端套件更新可能支援的其他作業系統。

**需求和限制：**  

-   若要檢閱 Linux 和 UNIX 用戶端的作業系統檔案相依性，請參閱[將用戶端部署至 Linux 和 UNIX 伺服器的必要條件](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu)。  
-   如需執行 Linux 或 UNIX 之電腦的支援管理功能概觀，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)。  
-   如需支援的 Linux 和 UNIX 版本，列出的版本會包含所有後續的次要版本。 例如，其中指定支援 CentOS 第 6 版，這也包括 CentOS 6 的任何後續次要版本，例如 CentOS 6.3。 同樣地，當列出支援使用 Service Pack 的作業系統時，例如 SUSE Linux Enterprise Server 11 SP1，則支援會包含該作業系統版本的後續 Service Pack。
-   如需用戶端安裝套件和 Universal Agent 的資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)。


**支援的版本：**   
使用指定的 .tar 檔可支援下列版本。  
### <a name="aix"></a>AIX  

|版本|檔案|  
|-|-|  
|5.3 版 (Power)|ccm-Aix53ppc.&lt;組建\>.tar|  
|6.1 版 (Power)|ccm-Aix61ppc.&lt;組建\>.tar|  
|7.1 版 (Power)|ccm-Aix71ppc.&lt;組建\>.tar|  

### <a name="centos"></a>CentOS  

|版本|檔案|  
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="debian"></a>Debian  

|版本|檔案|    
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 8 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 8 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|版本|檔案|  
|-|-|  
|11iv2 版 IA64|ccm-HpuxB.11.23i64.&lt;組建\>.tar|  
|11iv2 版 PA-RISC|ccm-HpuxB.11.23PA.&lt;組建\>.tar|  
|11iv3 版 IA64|ccm-HpuxB.11.31i64.&lt;組建\>.tar|  
|11iv3 版 PA-RISC|ccm-HpuxB.11.31PA.&lt;組建\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|版本|檔案|    
|-|-|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|版本|檔案|  
|-|-|  
|第 4 版 x86|ccm-RHEL4x86.&lt;組建\>.tar|  
|第 4 版 x64|ccm-RHEL4x64.&lt;組建\>.tar|  
|第 5 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 5 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 6 版 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 6 版 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 7 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="solaris"></a>Solaris  

|版本|檔案|   
|-|-|  
|第 9 版 SPARC|ccm-Sol9sparc.&lt;組建\>.tar|  
|第 10 版 x86|ccm-Sol10x86.&lt;組建\>.tar|  
|第 10 版 SPARC|ccm-Sol10sparc.&lt;組建\>.tar|  
|第 11 版 x86|ccm-Sol11x86.&lt;組建\>.tar|  
|第 11 版 SPARC|ccm-Sol11sparc.&lt;組建\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|版本|檔案|  
|-|-|  
|第 9 版 x86|ccm-SLES9x86.&lt;組建\>.tar|  
|第 10 版 SP1 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 10 版 SP1 x86|ccm-Universalx64.&lt;組建\>.tar|  
|第 11 版 SP1 x86|ccm-Universalx86.&lt;組建\>.tar|  
|第 11 版 SP1 x64|ccm-Universalx64.&lt;組建\>.tar|  
|第 12 版 x64|ccm-Universalx64.&lt;組建\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|版本|檔案|    
|-|-|  
|10.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|10.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|12.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|12.04 版 LTS x64|ccm-Universalx64.&lt;組建\>.tar|  
|14.04 版 LTS x86|ccm-Universalx86.&lt;組建\>.tar|  
|14.04 版 LTS x64|ccm-Universalx64.&lt;版本\>.tar|  

### <a name="exchange-server-connector"></a>Exchange Server 連接器
 LTSB 支援有限制地管理連線至您 Exchange Server 執行個體的裝置，而不需要安裝用戶端軟體。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。

 **需求和限制：**  

-   Configuration Manager 提供有限的行動裝置管理。 當您使用具備適用於 Exchange Active Sync (EAS) 的 Exchange Server 連接器功能的裝置，且該裝置連線到執行 Exchange Server 或 Exchange Online 的伺服器時，就會提供有限的管理。  

-   如需 Configuration Manager 針對 Exchange Server 連接器所管理的行動裝置所支援之管理功能的詳細資訊，請參閱[選擇 System Center Configuration Manager 的裝置管理解決方案](/sccm/core/plan-design/choose-a-device-management-solution)。  

**支援的 Exchange Server 版本：**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB 不支援管理透過線上服務連線的裝置，例如 Exchange Online (Office 365)。


## <a name="configuration-manager-console"></a>Configuration Manager 主控台
LTSB 支援下列作業系統執行 Configuration Manager 主控台。 裝載主控台的每部電腦都必須有最低 .NET Framework 4.5.2 版，但需要最低 .NET Framework 4.6 版的 Windows 10 除外。

**支援的作業系統：**
- Windows Server 2016
- Windows Server 2012 R2 (x64)：Standard、Datacenter
- Windows Server 2012 (x64)：Standard、Datacenter
- Windows Server 2008 R2 (含 SP1) (x64)：Standard、Enterprise、Datacenter
- Windows Server 2008 (含 SP2) (x86、x64)：Standard、Enterprise、Datacenter
- Windows 10 Enterprise 2016 LTSB (x86、x64)
- Windows 10 Enterprise 2015 LTSB (x86、x64)
- Windows 8.1 (x86、x64)：專業版、企業版
- Windows 7 (含 SP1) (x86、x64)：專業版、企業版、旗艦版


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>站台資料庫和報告點支援的 SQL Server 版本
LTSB 支援下列 SQL Server 版本來裝載站台資料庫和報告點。 針對每個支援版本，出現在最新分支的 [SQL Server 版本的支援](/sccm/core/plan-design/configs/support-for-sql-server-versions)中的相同設定需求和限制會套用至 LTSB。  這包含使用 SQL Server Cluster 或 SQL Server AlwaysOn 可用性群組。  

**支援的版本：**

- SQL Server 2016：Standard、Enterprise
- SQL Server 2014 SP2：Standard、Enterprise
- SQL Server 2014 SP1：Standard、Enterprise
- SQL Server 2012 SP3：Standard、Enterprise
- SQL Server 2008 R2 SP3：Standard、Enterprise、Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Active Directory 網域的支援
所有 LTSB 站台系統都必須是支援的 Windows Active Directory 網域成員。 Active Directory 網域支援的需求和限制與 [Active Directory 網域的支援](/sccm/core/plan-design/configs/support-for-active-directory-domains)中出現的需求和限制相同，但限制為下列網域功能等級︰

**支援的層級：**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>適用於長期維護分支的其他支援主題
下列＜最新分支＞主題中的資訊適用於 LTSB︰
- [大小和縮放比例](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [站台和站台系統必要條件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [高可用性選項](/sccm/protect/understand/high-availability-options)
- [建議的硬體](/sccm/core/plan-design/configs/recommended-hardware)
- [Windows 功能和網路支援](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [虛擬化環境支援](/sccm/core/plan-design/configs/support-for-virtualization-environments)
