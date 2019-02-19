---
title: 支持的客户端和设备
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 在客户端和设备上支持的操作系统版本。
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 100fdd8e9032b1d16ae79b3cd52ffba3b3609446
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140154"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Configuration Manager 在客户端和设备上支持的操作系统版本

适用范围：System Center Configuration Manager (Current Branch)

 Configuration Manager 支持在 Windows、Mac、Linux 和 UNIX 计算机上安装客户端软件。  

#### <a name="requirements-and-limitations-for-all-clients"></a>对所有客户端的要求和限制  

-   不支持更改任意 Configuration Manager 服务的启动类型或“登录身份”设置。 此更改可能会阻止关键服务正常运行。    

-   不支持在根以外的其他帐户下的计算机上安装或运行适用于 Linux 或 UNIX 的 Configuration Manager 客户端，或适用于 Mac 的客户端。 这样做可能会阻止关键服务正常运行。  



##  <a name="windows-computers"></a>Windows 计算机  

 若要管理以下 Windows OS 版本，请使用 Configuration Manager 随附的客户端。 有关详细信息，请参阅[如何将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。  


### <a name="supported-client-os-versions"></a>受支持的客户端 OS 版本

-   **Windows 10**  

    有关详细信息，请参阅 [Windows 10 支持](/sccm/core/plan-design/configs/support-for-windows-10)。  

-   **Windows 8.1** (x86, x64)：Professional、Enterprise    

-   **带 SP1 的 Windows 7** (x86, x64)：Professional、Enterprise 和 Ultimate    


### <a name="supported-server-os-versions"></a>受支持的服务器 OS 版本

-  **Windows Server 2019**：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>  
    （自 Configuration Manager 版本 1806 起。）

-  **Windows Server 2016**：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>  

-   **Windows Storage Server 2016**：标准版、工作组版  

-   **Windows Server 2012 R2** (x64)：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64)：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **带 SP1 的 Windows Server 2008 R2**  (x64)：标准版、企业版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64)：工作组版、标准版、企业版    

-   **带 SP2 的 Windows Server 2008** (x86, x64)：标准版、企业版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>    


#### <a name="server-core"></a>服务器核心
以下版本专指 OS 的服务器核心安装。 <sup>[注 3](#bkmk_note3)</sup>  

Windows Server 半年频道版本是服务器核心安装，如 Windows Server 版本 1809。 作为 Configuration Manager 客户端，它们与相关的 Windows 10 半年频道版本一样受到相同的支持。 有关详细信息，请参阅 [Windows 10 支持](/sccm/core/plan-design/configs/support-for-windows-10)。


-   **Windows Server 2019** (x64) <sup>[注 2](#bkmk_note2)</sup>  

-   **Windows Server 2016** (x64) <sup>[注 2](#bkmk_note2)</sup>   

-   **Windows Server 2012 R2** (x64) <sup>[注 2](#bkmk_note2)</sup>     

-   **Windows Server 2012** (x64) <sup>[注 2](#bkmk_note2)</sup>     

-   **Windows Server 2008 R2**（不含 Service Pack 或含 SP1 (x64)）     

-   **Windows Server 2008 SP2**（x86、x64）   

#### <a name="bkmk_note1"></a>注释 1
 Configuration Manager 测试并支持 Windows Server Datacenter 版本，但没有 Windows Server 正式认证。 对于 Windows Server Datacenter Edition 专属问题，我们未提供 Configuration Manager 修补程序支持。 若要详细了解 Windows Server 认证计划，请参阅 [Windows Server Catalog](https://www.windowsservercatalog.com/)。 

#### <a name="bkmk_note2"></a>注释 2
 若要支持[客户端请求安装](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation)，请添加文件和存储服务服务器角色的文件服务器服务。 若要详细了解如何在服务器核心上安装 Windows 功能，请参阅[使用 Windows PowerShell cmdlet 安装角色、角色服务和功能](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installwps)。  

#### <a name="bkmk_note3"></a>注释 3
 任何版本的 Windows Server Core 上都不支持新的软件中心应用。<!--SCCMDocs issue 683-->



##  <a name="windows-embedded-computers"></a>Windows Embedded 计算机  

 通过在设备上安装 Configuration Manager 客户端来管理 Windows Embedded 设备。 有关详细信息，请参阅[规划对 Windows Embedded 设备的客户端部署](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices)。  


### <a name="requirements-and-limitations"></a>要求和限制

-   未启用写入筛选器的 Windows Embedded 系统上支持所有客户端功能。  

-   使用下列其中一项的客户端受除电源管理以外的所有功能支持：  

    -   增强型写入筛选器 (EWF)    

    -   基于 RAM 文件的写入筛选器 (FBWF)    

    -   统一写入筛选器 (UWF)  

-   应用程序目录不受任何 Windows Embedded 设备支持。  


### <a name="supported-os-versions"></a>支持的操作系统版本  

-   **Windows 10 企业版**（x86、x64）  

-   **Windows 10 IoT 企业版**（x86、x64）  
    此版本包括长期服务频道 (LTSC)。 有关详细信息，请参阅 [Windows 10 IoT 企业版概述](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

-   **Windows Embedded 8.1 Industry**（x86、x64）    

-   **Windows Embedded 8 标准版**（x86、x64）    

-   **Windows Thin PC**（x86、x64）    

-   **Windows Embedded POSReady 7**（x86、x64）    

-   **Windows Embedded Standard 7 SP1**（x86、x64）    



## <a name="windows-ce-computers"></a>Windows CE 计算机

 使用 Configuration Manager 附带的 Configuration Manager 移动设备旧客户端管理 Windows CE 设备。  


### <a name="requirements-and-limitations"></a>要求和限制  

-   安装移动设备客户端需要 0.78 MB 的存储空间。 登录可能需要高达 256 KB 的额外存储空间。    

-   这些移动设备的功能因平台和客户端类型而异。 有关支持的管理功能的详细信息，请参阅[选择设备管理解决方案](/sccm/core/plan-design/choose-a-device-management-solution)。  


### <a name="supported-os-versions"></a>支持的操作系统版本  

-   Windows CE 7.0（ARM 和 x86 处理器）  

#### <a name="supported-languages-include"></a>支持的语言包括

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

 使用适用于 Mac 的 Configuration Manager 客户端管理 macOS 计算机。  

 Mac 客户端安装包未与 Configuration Manager 媒体一同提供。 可从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载**适用于其他操作系统的客户端**。  

 有关详细信息，请参阅[如何将客户端部署到 Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)。  


### <a name="supported-versions"></a>支持的版本

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

-   **Mac OS X 10.13** (macOS High Sierra)

- **macOS Mojave (10.14)** 


##  <a name="linux-and-unix-servers"></a>Linux 和 UNIX 服务器  

> [!Important]  
> 自 2018 年 3 月 22 日起，Configuration Manager 的 Linux 和 UNIX 客户端停用。 有关详细信息，请参阅 [Linux 和 Unix 客户端支持停止公告](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support)。  

 使用适用于 Linux 和 UNIX 的 Configuration Manager 客户端管理 Linux 和 UNIX 服务器。  

 Linux 和 UNIX 客户端安装包未与 Configuration Manager 媒体一同提供。 可从 [Microsoft 下载中心](http://go.microsoft.com/fwlink/?LinkID=525184)下载**适用于其他操作系统的客户端**。 除了客户端安装包，客户端下载内容还包括在每台计算机上管理客户端安装的脚本。  


### <a name="requirements-and-limitations"></a>要求和限制

-   若要查看适用于 Linux 和 UNIX 客户端的操作系统文件依赖项，请参阅[将客户端部署到 Linux 和 UNIX 服务器的先决条件](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU)。  

-   有关支持的 Linux 或 UNIX 管理功能概述，请参阅[如何将客户端部署到 UNIX 和 Linux 服务器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)。  

-   对于支持的 Linux 和 UNIX 版本，列出的版本包括所有后续的次要版本。 例如，CentOS 6 版本包括 CentOS 6.3。 同样，对使用 Service Pack 的操作系统（例如 SUSE Linux Enterprise Server 11 SP1）的支持包括该操作系统版本的后续 Service Pack。  

-   有关客户端安装包和通用代理的信息，请参阅[如何将客户端部署到 UNIX 和 Linux 服务器](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)。  


### <a name="supported-versions"></a>支持的版本

使用指示的 .tar 文件，支持以下版本。  

#### <a name="aix"></a>AIX  

|版本|TAR 文件|  
|-|-|  
|版本 6.1（电源）|ccm-Aix61ppc.&lt;build\>.tar|  
|版本 7.1（电源）|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|版本|TAR 文件|  
|-|-|  
|版本 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|版本|TAR 文件|  
|-|-|  
|版本 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|版本 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|版本 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|版本 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|版本|TAR 文件|  
|-|-|  
|版本 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|版本|TAR 文件|  
|-|-|  
|版本 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  



##  <a name="bkmk_OnpremOS"></a>本地移动设备管理  

 Configuration Manager 提供内置功能来管理本地设备，无需安装客户端软件。 有关详细信息，请参阅[使用本地基础结构管理移动设备](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)。  


### <a name="requirements-and-limitations"></a>要求和限制

-   在层次结构顶层站点上配置服务连接点。  


### <a name="supported-operating-systems"></a>支持的操作系统

- **Windows 10 Pro**（x86、x64）  

- **Windows 10 Pro Enterprise**（x86、x64）  

- **Windows 10 IoT 企业版**（x86、x64）  
    此版本包括长期服务频道 (LTSC)。 有关详细信息，请参阅 [Windows 10 IoT 企业版概述](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 移动版**  

- **Windows 10 移动企业版**  

- **Windows 10 IoT 移动企业版**  

- **Surface Hub 的 Windows 10 协同版**  



##  <a name="bkmk_ExSrvConOS"></a> Exchange Server 连接器  

Configuration Manager 支持连接到 Exchange Server 的设备的有限管理，无需安装 Configuration Manager 客户端。 有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  


### <a name="supported-versions-of-exchange-server"></a>受支持的 Exchange Server 版本

- **Exchange Online (Office 365)**：此版本包括 Business Productivity Online Standard Suite  

- **Exchange Server 2016**（从版本 1802 开始）  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** 或 **Exchange Server 2010 SP2** 
