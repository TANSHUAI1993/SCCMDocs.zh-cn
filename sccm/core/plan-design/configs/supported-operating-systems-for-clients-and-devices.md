---
title: "支持的客户端和设备 | System Center Configuration Manager"
description: "了解 System Center Configuration Manager 对客户端和设备支持的操作系统。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 862291f52d5a1bb34fb5483806972fcf70f158a8

---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>System Center Configuration Manager 的客户端和设备支持的操作系统

*适用范围：System Center Configuration Manager (Current Branch)*




 System Center Configuration Manager 支持在多种 Windows、Mac 和 Linux 以及 UNIX 计算机上安装客户端软件。  

 **对所有客户端的要求和限制：**  

-   不支持更改任意 Configuration Manager 服务的启动类型或登录身份设置。 这样做可能会阻止关键服务正常运行。    

-   不支持在根以外的其他帐户下的计算机上安装或运行适用于 Linux 或 UNIX 的 Configuration Manager 客户端，或适用于 Mac 的客户端。 这样做可能会阻止关键服务正常运行。  

##  <a name="a-namebkmkwinclientosa-windows-computers"></a><a name="bkmk_WinClientos"></a> Windows 计算机  
 可以使用 Configuration Manager 包括的 Configuration Manager 客户端管理 Windows 计算机。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中向 Windows 计算机部署客户端](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

**支持的操作系统：**  

-  **Windows Server 2016** – 标准版、数据中心版 <sup>1</sup>
  - 从 Configuration Manager 版本 1606（或 2016 年 10 月发布的 1606 基线版本）开始，将支持 Windows Server 2016，并提供 KB3186654 中的修补程序汇总。  


-   **Windows Server 2012 R2** (x64) - 标准版、数据中心版 <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64) - 标准版、数据中心版 <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **带 SP1 的 Windows Server 2008 R2** (x64) – 标准版、企业版、数据中心版 <sup>1</sup>    

-   **Windows Storage Server 2008 R2**（x86、x64）- 工作组、标准版、企业版    

-   **Windows Server 2008 with SP2**（x86、x64） — 标准版、企业版、数据中心版  <sup>1</sup>    

-   **Windows 10 企业版 LTSB**（x86、x64）<sup>3</sup>    

-   **Windows 10**（x86、x64）– 专业版、企业版    

-   **Windows 8.1**（x86、x64）- 专业版、企业版    

-   **Windows 8**（x86、x64） - 专业版、企业版    

-   **Windows 7 SP1**（x86、x64）- 专业版、企业版、旗舰版    

-   **Windows Server 2012 R2 (x64) 的 Server Core 安装** <sup>2</sup>    

-   **Windows Server 2012 (x64) 的 Server Core 安装** <sup>2</sup>    

-   **Windows Server 2008 R2 的 Server Core 安装**  
    **（不带 Service Pack，或带 SP1）**(x64)    

-   **Windows Server 2008 SP2 的服务器核心安装**（x86、x64）  

 <sup>1</sup> Configuration Manager 支持数据中心版本，但未经认证。 对于特定于 Windows Server Datacenter Edition 的问题，未提供修补程序支持。  

 <sup>2</sup> 若要支持客户端请求安装，运行此操作系统版本的计算机必须运行文件的文件服务器角色服务和存储服务服务器角色。 有关在 Server Core 计算机上安装 Windows 功能的详细信息，请参阅 Windows Server 2012 TechNet 库中的[在 Server Core 服务器上安装服务器角色和功能](http://go.microsoft.com/fwlink/p/?LinkId=299359)。  

 <sup>3</sup> 使用此操作系统要求 1602 或更高版本。  

##  <a name="a-namebkmkembeddedosa-windows-embedded"></a><a name="bkmk_EmbeddedOS"></a> Windows Embedded  
 可以通过在设备上安装 Configuration Manager 客户端软件管理 Windows Embedded 设备。  有关详细信息，请参阅[在 System Center Configuration Manager 中规划对 Windows Embedded 设备的客户端部署](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

**要求和限制：**  

-   未启用写入筛选器的受支持 Windows Embedded 系统上支持所有客户端功能。  

-   使用下列其中一项的客户端受除电源管理以外的所有功能支持：  

    -   增强型写入筛选器 (EWF)    

    -   基于 RAM 文件的写入筛选器 (FBWF)    

    -   统一写入筛选器 (UWF)  

-   应用程序目录不受任何 Windows Embedded 设备支持。  

-   在能够监视基于 Windows XP 的 Windows Embedded 设备上检测到的恶意软件之前，必须在嵌入式设备上安装 Microsoft Windows WMI 脚本包。 使用 Windows Embedded Target Designer 安装此包。 必须存在文件 **WBEMDISP.DLL** 和 **WBEMDISP.TLB** 且必须在嵌入式设备上的 **%windir%\System32\WBEM** 文件夹中注册，以确保报告检测到的恶意软件。  

**支持的操作系统：**  

-   **Windows 10 企业版**（x86、x64）  

-   **Windows 10 IoT 企业版**（x86、x64）  

-   **Windows Embedded 8.1 Industry**（x86、x64）    

-   **Windows Embedded 8 Industry**（x86、x64）    

-   **Windows Embedded 8 标准版**（x86、x64）    

-   **Windows Embedded 8 专业版**（x86、x64）    

-   **Windows Thin PC**（x86、x64）    

-   **Windows Embedded POSReady 7**（x86、x64）    

-   **Windows Embedded Standard 7 SP1**（x86、x64）    

-   **WEPOS 1.1 SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce"></a>Windows CE  
 可以使用 Configuration Manager 包括的 Configuration Manager 移动设备旧客户端管理 Windows CE 设备。  

**要求和限制**  

-   移动设备客户端需要 0.78 MB 的存储空间以安装该客户端。 移动设备上的日志记录可能需要高达 256 KB 的额外存储空间。    

-   这些移动设备的功能因平台和客户端类型而异。 有关 Configuration Manager 对于移动设备旧客户端所支持的管理功能的详细信息，请参阅[为 System Center Configuration Manager 选择设备管理解决方案](../../../core/plan-design/choose-a-device-management-solution.md)。  

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

## <a name="mac-computers"></a>Mac 计算机  
 可以使用适用于 Mac 的 Configuration Manager 客户端管理 Mac OS X 计算机。  

 Mac 客户端安装包未与 Configuration Manager 媒体一同提供。 可以将其作为其他操作系统的客户端的一部分，从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载。  

**要求和限制：**  

 必须使用适用于 Mac（版本 5.0.8333.1 或更高）的 Configuration Manager 客户端，必须单独下载此客户端。 与 Windows 客户端不同的是，在安装时，Mac 客户端未包含在 Configuration Manager 软件中。 若要下载 Mac 客户端，请转到 [Microsoft System Center Configuration Manager - 适用于其他操作系统的客户端](http://go.microsoft.com/fwlink/?LinkID=525184)。  

 有关详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Mac](../../../core/clients/deploy/deploy-clients-to-macs.md)。  

**支持的版本：**  

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

##  <a name="a-namebkmklinuxosa-linux-and-unix-servers"></a><a name="bkmk_LinuxOS"></a> Linux 和 UNIX 服务器  
 可以使用适用于 Linux 和 UNIX 的 Configuration Manager 客户端管理 Linux 和 UNIX 服务器。  

 Linux 和 UNIX 客户端安装包未与 Configuration Manager 媒体一同提供。 可以将其作为其他操作系统的客户端的一部分，从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载。 除了客户端安装包，客户端下载内容还包括在每台计算机上管理客户端安装的“install”脚本。  

**要求和限制：**  

-   若要查看适用于 Linux 和 UNIX 客户端的操作系统文件依赖项，请参阅[将客户端部署到 Linux 和 UNIX 服务器的先决条件](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)。  

-   有关运行 Linux 或 UNIX 的计算机支持的管理功能概述，请参阅[在 System Center Configuration Manager 中如何将客户端部署到 UNIX 和 Linux 服务器](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

-   对于支持的 Linux 和 UNIX 版本，列出的版本包括所有后续的次要版本。 例如，若指示支持 CentOS 版本 6，则其中还包括 CentOS 6 的任何后续次要版本，如 CentOS 6.3。 同样，若列出对使用 Service Pack 的操作系统（例如 SUSE Linux Enterprise Server 11 SP1）的支持，则其还支持包括该操作系统后续的 Service Pack。  

-   有关客户端安装包和通用代理的信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 UNIX 和 Linux 服务器](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

**支持的版本：**通过使用指示的 .tar 文件，支持以下版本。  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|版本 5.3（电源）|ccm-Aix53ppc.&lt;build\>.tar|  
|版本 6.1（电源）|ccm-Aix61ppc.&lt;build\>.tar|  
|版本 7.1（电源）|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|||  
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

|||  
|-|-|  
|版本 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|版本 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|版本 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|版本 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|版本 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|版本 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|版本 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|版本 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|版本 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|版本 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|版本 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|版本 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|版本 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|版本 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

##  <a name="a-namebkmkintuneosa-mobile-devices-enrolled-by-microsoft-intune"></a><a name="bkmk_IntuneOS"></a> Microsoft Intune 注册的移动设备  
 有关在将 Microsoft Intune 与 Configuration Manager 集成时可以管理的计算机和设备的详细信息，请参阅 Microsoft Intune 文档库中的以下两个主题：  

-   [Microsoft Intune 中的移动设备管理功能](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Microsoft Intune 中的 Windows PC 管理功能](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="a-namebkmkonpremosa-on-premises-mobile-device-management"></a><a name="bkmk_OnpremOS"></a> 本地移动设备管理  
 Configuration Manager 提供有内置功能来管理本地设备，无需安装客户端软件。  有关详细信息，请参阅[在 System Center Configuration Manager 中使用本地基础结构管理移动设备](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

 **要求和限制：**  

-   必须在层次结构顶层站点上配置**服务连接点**  

 **支持的操作系统：**  

-   **Windows 10 Pro**（x86、x64）  

-   **Windows 10 Pro Enterprise**（x86、x64）  

-   **Windows 10 IoT 企业版**（x86、x64）

-   **Windows 10 移动版**  

-   **Windows 10 移动企业版**  

-  **Windows 10 IoT 移动企业版**

##  <a name="a-namebkmkexsrvconosa-exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Exchange Server 连接器  
 Configuration Manager 支持连接到 Exchange Server 的设备的有限管理，无需安装客户端软件。  有关详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

 **要求和限制：**  

-   当使用连接到运行 Exchange Server 或 Exchange Online 的服务器、使用支持 Exchange Active Sync (EAS) 的设备的 Exchange Server 连接器时，Configuration Manager 提供对移动设备的有限管理。  

-   有关 Configuration Manager 支持用于 Exchange Server 连接器管理的移动设备的管理功能的详细信息，请参阅“确定如何在 Configuration Manager 中管理移动设备”。  

**支持的 Exchange Server 版本：**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)** - 这包括 Business Productivity Online Standard Suite  



<!--HONumber=Nov16_HO1-->


