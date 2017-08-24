---
title: "LTSB 支持的配置 | Microsoft Docs"
description: "了解哪些操作系统和相关产品可配合 System Center Configuration Manager 的 Long-Term Servicing Branch 一起运作。"
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
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager 的 Long-Term Servicing Branch 支持的配置

*适用范围：System Center Configuration Manager (Long-Term Servicing Branch)*

使用本主题中的信息，了解哪些操作系统和产品依赖项受 Configuration Manager 的 Long-Term Servicing Branch (LTSB) 支持。
如果未在本主题或 LTSB 特定主题中另行声明，适用于 Current Branch 版本 1606 的相同配置和限制同样适用于 LTSB。  发生冲突时，使用适用于所使用版本的信息。 通常，LTSB 受到的限制比 Current Branch 更多。

## <a name="general-statement-of-support"></a>常规支持声明
此 Configuration Manager 分支支持以下产品和技术。 不过，将它们囊括在这一内容中并不表示对超出相应产品的单独支持生命周期的任何产品或版本延长支持。 不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 有关详细信息，请访问 [Microsoft 支持生命周期](http://go.microsoft.com/fwlink/p/?LinkId=208270)网站并参阅 [Microsoft 支持生命周期策略常见问题解答](http://go.microsoft.com/fwlink/p/?LinkId=31976)。

此外，不支持以下主题中未列出的产品和产品版本，除非它们已在 [Enterprise Mobility + Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/)（企业移动性和安全性博客）上公布。

**将来支持的限制：**LTSB 对未来的服务器和客户端操作系统及产品依赖项提供有限的支持。 已针对发布生命期确定 LTSB 平台列表：

**Windows：**
- 仅支持用于 Windows 的质量和安全更新。
- 不为 Windows 10 的 Current Branch (CB)、Current Branches for Business (CBB) 或 LTSB 添加任何支持。
-   不对 Windows Server 新的主版本提供支持。

**SQL Server：**
- SQL Server 仅支持质量和安全更新或次要升级（如服务包）。
- 不对 SQL Server 新的主版本提供支持。  

## <a name="site-systems-and-servers"></a>站点系统和服务器
LTSB 支持使用以下 Windows 计算机操作系统作为站点系统。  每个操作系统都具有与[站点系统服务器支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)中的同一条目相同的要求和限制。  例如，Windows 2012 R2 的服务器核心安装必须为 x64 版本，仅支持托管分发点，且不支持 PXE 或多播。

**支持的操作系统：**
- Windows Server 2016
- Windows Server 2012 R2 (x64)：标准版、数据中心版
- Windows Server 2012 (x64)：标准版、数据中心版
- Windows Server 2008 R2 SP1 (x64)：标准版、企业版、数据中心版
- Windows Server 2008 SP2（x86、x64）：标准版、企业版、数据中心版（请参阅注释 1）
- Windows 10 企业版 2015 长期服务（x86、x64）
- Windows 10 企业版 2016 长期服务（x86、x64）
- Windows 8.1（x86、x64）：专业版、企业版
- Windows 7 SP1（x86、x64）：专业版、企业版、旗舰版
- Windows Server 2012 的服务器核心安装
- Windows Server 2012 R2 的服务器核心安装    

*注释 1*：除分发点和拉取分发点外，站点服务器或站点系统角色均不支持此操作系统。 你可以继续使用操作系统作为分发点，直到此支持被宣布弃用或者此操作系统的扩展支持期到期为止。 有关详细信息，请参阅 [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)（在 Windows Server 2008 上安装 System Center Configuration Manager CB 和 LTSB 失败）。

## <a name="client-management"></a>客户端管理
以下各节介绍可以使用 LTSB 管理的客户端操作系统。 LTSB 不支持新增操作系统作为支持的客户端。

### <a name="windows-computers"></a>Windows 计算机
可以使用 LTSB，通过包括在 Configuration Manager 中的 Configuration Manager 客户端软件，管理以下 Windows 计算机操作系统。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中向 Windows 计算机部署客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。

**支持的操作系统：**
- Windows Server 2016
- Windows Server 2012 R2 (x64)：标准版、数据中心版（注释 1）
- Windows Server 2012 (x64)：标准版、数据中心版（注释 1）
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 SP1 (x64)：标准版、企业版、数据中心版（注释 1）
- Windows Storage Server 2008 R2（x86、x64）：工作组、标准版、企业版
- Windows Server 2008 SP2（x86、x64）：标准版、企业版、数据中心版（注释 1）
- Windows 10 企业版 2015 长期服务（x86、x64）
- Windows 10 企业版 2016 长期服务（x86、x64）
- Windows 8.1（x86、x64）：专业版、企业版
- Windows 7 SP1（x86、x64）：专业版、企业版、旗舰版
- Windows Server 2012 R2 的服务器核心安装 (x64)（注释 2）
- Windows Server 2012 的服务器核心安装 (x64)（注释 2）
- Windows Server 2008 R2 SP1 的服务器核心安装 (x64)
- Windows Server 2008 SP2 的服务器核心安装（x86、x64）

**（注释 1）**Configuration Manager 支持数据中心版本，但未经认证。  
**（注释 2）**若要支持客户端请求安装，运行此操作系统版本的计算机必须运行文件和存储服务服务器角色的文件服务器角色服务。 有关在 Server Core 计算机上安装 Windows 功能的详细信息，请参阅 Windows Server 2012 TechNet 库中的[在 Server Core 服务器上安装服务器角色和功能](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx)。

### <a name="windows-embedded"></a>Windows Embedded
可以在设备上安装客户端软件，使用 LTSB 管理以下 Windows Embedded 设备。  有关详细信息，请参阅[在 System Center Configuration Manager 中规划对 Windows Embedded 设备的客户端部署](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices)。

**要求和限制：**  

-   未启用写入筛选器的受支持 Windows Embedded 系统上支持所有客户端功能。  

-   使用下列其中一项的客户端受除电源管理以外的所有功能支持：  

    -   增强型写入筛选器 (EWF)    

    -   基于 RAM 文件的写入筛选器 (FBWF)    

    -   统一写入筛选器 (UWF)  

-   应用程序目录不受任何 Windows Embedded 设备支持。  

-   在能够监视基于 Windows XP 的 Windows Embedded 设备上检测到的恶意软件之前，必须在嵌入式设备上安装 Microsoft Windows WMI 脚本包。 使用 Windows Embedded Target Designer 安装此包。 文件 *WBEMDISP.DLL* 和 *WBEMDISP.TLB* 必须存在并在嵌入式设备上的 %windir%\System32\WBEM 文件夹中注册，以确保报告检测到的恶意软件。  

**支持的操作系统：**  
-   Windows 10 企业版 2016 长期服务（x86、x64）  
-   Windows 10 企业版 2015 长期服务（x86、x64）  
-   Windows Embedded 8.1 Industry（x86、x64）    
-   Windows Thin PC（x86、x64）    
-   Windows Embedded POSReady 7（x86、x64）    
-   Windows Embedded Standard 7 SP1（x86、x64）    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 可以使用 Configuration Manager 包括的 Configuration Manager 移动设备旧客户端管理 Windows CE 设备。  

**要求和限制：**  

-   移动设备客户端需要 0.78 MB 的存储空间来安装该客户端。 移动设备可能需要最多 256 KB 的额外存储空间用于登录。    

-   这些移动设备的功能因平台和客户端类型而异。 有关 Configuration Manager 对于移动设备旧客户端所支持的管理功能类型的信息，请参阅[为 System Center Configuration Manager 选择设备管理解决方案](/sccm/core/plan-design/choose-a-device-management-solution)。  

**支持的操作系统：**  

-   Windows CE 7.0（ARM 和 x86 处理器）  

**支持的语言包括：**  
-   中文（简体和繁体）    
-   英语（美国）    
-   法语（法国）    
-   德语    
-   意大利语    
-   日语  
-   朝鲜语  
-   葡萄牙语（巴西）  
-   俄语  
-   西班牙语（西班牙）  

### <a name="mac-computers"></a>Mac 计算机  
 可以使用 LTSB，通过用于 Mac 的 Configuration Manager 客户端来管理 Mac OS X 计算机。

Mac 客户端安装包未与 Configuration Manager 媒体一同提供。 可以将其作为“其他操作系统的客户端”的一部分，从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载。  

对 Mac 操作系统的支持仅限于本节中列出的这些操作系统。 支持不包括其他可能受 Current Branch 适用的 Mac 客户端安装包的将来更新支持的操作系统。

有关详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)。

**支持的版本：**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux 和 UNIX 服务器
可使用 LTSB，通过适用于 Linux 和 UNIX 的 Configuration Manager 客户端管理 Linux 和 UNIX 服务器。

Linux 和 UNIX 客户端安装包未与 Configuration Manager 媒体一同提供。 可以将其作为“其他操作系统的客户端”的一部分，从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载。 除了客户端安装包，客户端下载内容还包括在每台计算机上管理客户端安装的“install”脚本。

对 Linux 和 UNIX 操作系统的支持仅限于本节中列出的这些操作系统。 支持不包括其他可能受 Current Branch 适用的 Linux 和 UNIX 客户端安装包的将来更新支持的操作系统。

**要求和限制：**  

-   若要查看适用于 Linux 和 UNIX 客户端的操作系统文件依赖项，请参阅[将客户端部署到 Linux 和 UNIX 服务器的先决条件](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu)。  
-   有关运行 Linux 或 UNIX 的计算机支持的管理功能概述，请参阅[在 System Center Configuration Manager 中如何将客户端部署到 UNIX 和 Linux 服务器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)。  
-   对于支持的 Linux 和 UNIX 版本，列出的版本包括所有后续的次要版本。 例如，若指示支持 CentOS 版本 6，则其中还包括 CentOS 6 的任何后续次要版本，如 CentOS 6.3。 同样，若列出对使用 Service Pack 的操作系统（例如 SUSE Linux Enterprise Server 11 SP1）的支持，则其还支持包括该操作系统后续的 Service Pack。
-   有关客户端安装包和通用代理的信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 UNIX 和 Linux 服务器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)。


**支持的版本：**   
使用指示的 .tar 文件，支持以下版本。  
### <a name="aix"></a>AIX  

|版本|文件|  
|-|-|  
|版本 5.3（电源）|ccm-Aix53ppc.&lt;build\>.tar|  
|版本 6.1（电源）|ccm-Aix61ppc.&lt;build\>.tar|  
|版本 7.1（电源）|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|版本|文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|版本|文件|    
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|版本|文件|  
|-|-|  
|版本 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|版本 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|版本 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|版本 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|版本|文件|    
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|版本|文件|  
|-|-|  
|版本 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|版本 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|版本|文件|   
|-|-|  
|版本 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|版本 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|版本 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|版本 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|版本 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|版本|文件|  
|-|-|  
|版本 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|版本 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|版本|文件|    
|-|-|  
|版本 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="exchange-server-connector"></a>Exchange Server 连接器
 LTSB 支持连接到 Exchange Server 实例的设备的有限管理，无需安装客户端软件。 有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。

 **要求和限制：**  

-   Configuration Manager 提供对移动设备的有限管理。 当使用连接到运行 Exchange Server 或 Exchange Online 的服务器、支持 Exchange Active Sync (EAS) 的设备的 Exchange Server 连接器时，便可使用有限管理。  

-   有关 Configuration Manager 对于 Exchange Server 连接器管理的移动设备所支持的管理功能的详细信息，请参阅[为 System Center Configuration Manager 选择设备管理解决方案](/sccm/core/plan-design/choose-a-device-management-solution)。  

**支持的 Exchange Server 版本：**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB 不支持管理通过联机服务（如 Exchange Online (Office 365)）连接的设备。


## <a name="configuration-manager-console"></a>Configuration Manager 控制台
LTSB 支持以下操作系统运行 Configuration Manager 控制台。 托管控制台的每台计算机都必须具有最低为 4.5.2 的 .NET Framework 版本，Windows 10 除外，它要求的最低版本为 .NET Framework 4.6。

**支持的操作系统：**
- Windows Server 2016
- Windows Server 2012 R2 (x64)：标准版、数据中心版
- Windows Server 2012 (x64)：标准版、数据中心版
- Windows Server 2008 R2 SP1 (x64)：标准版、企业版、数据中心版
- Windows Server 2008 SP2（x86、x64）：标准版、企业版、数据中心版
- Windows 10 企业版 2016 长期服务（x86、x64）
- Windows 10 企业版 2015 长期服务（x86、x64）
- Windows 8.1（x86、x64）：专业版、企业版
- Windows 7 SP1（x86、x64）：专业版、企业版、旗舰版


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>站点数据库和报表点支持的 SQL Server 版本
LTSB 支持以下版本的 SQL Server，以托管站点数据库和报表点。 对于支持的每个版本，用于 Current Branch 的 [SQL Server 版本支持](/sccm/core/plan-design/configs/support-for-sql-server-versions)中出现的相同配置要求和限制适用于 LTSB。  这包括 SQL Server 群集或 SQL Server AlwaysOn 可用性组的使用。  

**支持的版本：**

- SQL Server 2016：标准版、企业版
- SQL Server 2014 SP2：标准版、企业版
- SQL Server 2014 SP1：标准版、企业版
- SQL Server 2012 SP3：标准版、企业版
- SQL Server 2008 R2 SP3：标准版、企业版、数据中心版
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>对 Active Directory 域的支持
所有 LTSB 站点系统必须均为受支持的 Windows Active Directory 域的成员。 对 Active Directory 域的支持与[对 Active Directory 域的支持](/sccm/core/plan-design/configs/support-for-active-directory-domains)中显示的域具有相同的要求和限制，但限于以下域功能级别：

**支持的级别：**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>适用于 Long-Term Servicing Branch 的其他支持主题
以下 Current Branch 主题中的信息适用于 LTSB：
- [大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [站点和站点系统先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [高可用性选项](/sccm/protect/understand/high-availability-options)
- [推荐硬件](/sccm/core/plan-design/configs/recommended-hardware)
- [对 Windows 功能和网络的支持](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [对虚拟化环境的支持](/sccm/core/plan-design/configs/support-for-virtualization-environments)
