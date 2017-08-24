---
title: "Technical Preview 1511 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1511 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: d0bde2c085cc9b330bc772e68081d629ca9e2f11
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1511-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1511 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview 1511 版中的可用功能。 此版本是技术预览版的基准安装版本，可以使用它安装新的技术预览站点，或者从早期的技术预览版升级。   在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

以下是可以试用的此版本的新功能。  

##  <a name="BKMK_WUfB"></a>在 Windows 10 中与 Windows Update for Business 集成  
 现在 Configuration Manager 能够区分通过 Windows Update for Business (WUfB) 直接连接的 Windows 10 计算机与连接到 WSUS 以获取 Windows 10 更新和升级的计算机。  对于通过 WUfB 连接的计算机，更新和升级可以按照管理用户通过组策略或 MDM 策略设置的频率来进行管理，这些更新/升级可以直接从 WUfB 进行安装。    
对于通过 WUfB 连接的计算机，Configuration Manager 无法报告符合性状态（包括 Windows 更新或定义更新）。 Configuration Manager 也无法将 Microsoft 更新或第三方更新部署到这些计算机。  

 **此方案的先决条件：**  

-   Windows 10 桌面专业版或 Windows 10 企业版的版本 1511 或更高版本  

-   要通过 [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx)进行管理的计算机。  

### <a name="try-it-out"></a>试试看！  
 尝试完成下面的任务，然后使用本主题顶部附近的反馈信息，让我们知道它的工作方式：  

1.  禁用 Windows 更新代理，以便它不会针对 WSUS 进行扫描（如果以前已启用）。   
    可以设置注册表项 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** ，以指示是否针对 WSUS 或 Windows 更新扫描计算机。  值是 2 时，它不会针对 WSUS 进行扫描。  

2.  记下新属性“UseWUServer” （Configuration Manager 资源浏览器中“Windows 更新”  节点下）。  

3.  基于 **UserWUServer** 属性为通过 WUfB 连接以获取更新和升级的所有计算机创建一个集合。  

4.  创建客户端代理设置以禁用软件更新工作流，并将该设置部署到直接连接到 WUfB 的计算机的集合。  

5.  通过 WUfB 进行管理的计算机会在符合性状态中显示 **未知** ，不会计入总体符合性百分比中。  

##  <a name="BKMK_Office365ProPlus"></a>通过 System Center Configuration Manager 管理 Office 365 ProPlus 客户端更新  
 Configuration Manager 现在能够使用 Configuration Manager 软件更新管理工作流来管理 Office 365 客户端更新。    
当 Microsoft 向 Windows Server 更新服务 (WSUS) 发布新的 Office 365 桌面客户端更新时，如果 Office 365 更新配置为目录同步的一部分，则 Configuration Manager 能够将更新同步到其目录。  Configuration Manager 站点服务器会下载 Office 365 客户端更新并将包分发到 Configuration Manager 分发点。  Configuration Manager 客户端随后会告知 Office 365 桌面客户端在何处获取更新以及何时启动更新安装过程。  

**此方案的先决条件：**  

### <a name="try-it-out"></a>试试看！  
 尝试完成下面的任务，然后使用本主题顶部附近的反馈信息，让我们知道它的工作方式：  

1.  可以将 Office 365 更新同步到 Configuration Manager 站点服务器并从 Configuration Manager 控制台查看它们。  

2.  可以审批并成功部署 Office 365 更新。  

3.  可以下载并成功将 Office 365 更新部署到客户端。  

4.  可以使用控制台中监视或报告来验证 Office 365 更新的符合性。  

 有关详细步骤，请参阅 [使用 System Center Configuration Manager Technical Preview 管理 Office 365 客户端更新](https://technet.microsoft.com/library/mt628083.aspx)。  

##  <a name="BKMK_AlwasyOn"></a>支持 SQL Server AlwaysOn，实现数据库的高度可用性  
 Configuration Manager 现在支持使用 SQL Server AlwaysOn 可用性组托管站点数据库。  在安装新站点时，可以指示安装程序使用可用性组，而不是普通的 SQL Server 实例。  

> [!NOTE]  
>  成功配置和使用可用性组要求你熟悉配置 SQL Server 可用性组，并依赖 SQL Server 文档库中提供文档和过程。  

配置和使用可用性组的高级流程包括：  

1.  在 SQL Server 中配置可用性组。  

2.  安装新 Configuration Manager 站点，并在安装过程中通过指定组终结点来指示站点使用可用性组。  

**此方案的先决条件：**  

-   需要受 Configuration Manager Technical Preview 支持的 SQL Server 版本  

-   在安装 Configuration Manager 之前必须创建和配置 SQL Server 可用性组  

-   此可用性组必须具有一个主副本，并且可以具有最多两个同步辅助副本  

-   此可用性组必须具有至少一个终结点  

-   你必须具有一个可用性组中的每个 SQL Server 均可以访问的网络位置。 配置可用性组时，此位置由安装程序使用，并且可在安装完成后删除。  

**此版本的已知问题：**  

-   无法成功向已用作站点数据库的可用性组添加新的副本成员。 相反，必须在添加新的副本成员后重新安装站点。  

-   对于这种方案，你可能需要在管理点服务器上（ **从 SQL Server 2012 功能包** ）安装[SQL Server 2012 的本机客户端](http://www.microsoft.com/download/details.aspx?id=29065)。 这可以防止 SQL 连接错误（记录在管理点服务器上的“mp_getauth.log”  中）。  

### <a name="try-it-out"></a>试试看！  
尝试完成以下任务，然后使用本主题顶部附近的反馈信息，让我们知道它们的工作方式：  

-   我可以安装一个主站点，该主站点使用为 SQL AlwaysOn 可用性组配置的数据库服务器  

-   我可以将我的 SQL AlwaysOn 可用性组故障转移到组中的新副本，并且主站点仍正常运行  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>为 Configuration Manager 配置 SQL Server AlwaysOn  
 使用以下步骤来首先创建和配置可用性组，然后安装一个使用该可用性组的新 Configuration Manager 站点。  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>创建一个 SQL Server AlwaysOn 可用性组  
创建 [SQL Server 可用性组](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx)的过程记录在 SQL Server 文档库中。  创建可用性组时，确保满足使用 Configuration Manager 的以下要求：  

-   最多包含三个成员：  

    -   一个主副本和最多两个辅助副本  

    -   辅助副本必须同步。  

        > [!TIP]  
        >  我们建议将辅助副本配置为只读。 这可让你将辅助副本用于报告等功能，同时保持主副本的性能，以便进行站点操作。  

-   至少一个终结点。 安装 Configuration Manager 站点时，将使用此终结点的虚拟名称。  

    > [!TIP]  
    >  尽管组中可以包含多个终结点，但 Configuration Manager 只能使用其中一个。  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>安装使用可用性组的 Configuration Manager 站点  
若要安装使用 SQL Server 可用性组的站点：  

1.  Configuration Manager 安装程序发出提示时，替代以下内容：  

    -   **SQL Server 名称**：输入在创建可用性组时配置的终结点的虚拟名称。 虚拟名称应为完整的 DNS 名称，如 **&lt;endpointServer\>.fabrikam.com**。  

    -   **实例**：此值应保留空白。 在此配置中没有任何实例。  

    -   **数据库**：输入在可用性组的主副本上创建的数据库的名称。  

2.  接下来，你必须提供一个组中的每个 SQL Server 均可以访问的网络位置：  

    -   每个 SQL Server 的计算机帐户和服务帐户均要求完全控制对此位置的访问权限。  

    -   此位置仅在安装过程中使用，并且可在安装程序完成和安装站点之后将其取消共享或删除。  

3.  提供此信息后，使用常规过程和配置完成安装。  

##  <a name="BKMK_ClusterServerUpdates"></a>为服务器群集提供服务  
现在，你可以创建包含群集中的服务器的集合，然后配置将在你向群集部署更新时使用的群集设置。 你可以在任何给定时间控制处于联机状态的服务器的百分比，还可将预先部署和后期部署 PowerShell 脚本配置为运行自定义操作。  

**此版本的已知问题：**  

-   报告不可用于检查群集服务器的软件更新部署状态。  

-   “群集设置”  页中的维护序列选项已禁用，并且在此版本中不可用。  

### <a name="try-it-out"></a>试试看！  
尝试完成下面的任务，然后使用本主题顶部附近的反馈信息，让我们知道它的工作方式：  

-   我可以创建表示服务器群集的集合。 对于此测试，可以将收集成员身份规则配置为在此集合中具有 2 台计算机。  

-   我可以指定群集中只有 50% 的服务器可以在群集服务的任何时刻处于脱机状态。 使用过程中的示例脚本来指定预先部署脚本和后期部署脚本。  

-   将更新部署到此集合。 查看 C:\temp 中的 start.txt 和 end.txt 文件，并验证群集中的服务器上的部署开始和结束时间。 有关详细信息，请查看 UpdatesDeployment.log 文件。  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>若要创建服务器群集的集合  

1.  [创建一个设备集合](https://technet.microsoft.com/library/gg712295.aspx)，使其包含群集中的所有服务器。  

2.  在“资产和符合性”工作区中，单击“设备集合”，右键单击包含群集中的服务器的集合，然后单击“属性”。  

3.  在“常规”选项卡上，选择“所有设备属于同一服务器集群”，然后单击“设置”。  

4.  在“群集设置”页面，选择可以同时脱机安装软件更新的服务器的百分比。 不管你提供的百分比为何，可能只有一台群集服务器在某个时候会处于脱机状态。 当选择一次同时服务的服务器数量时，Configuration Manager 会向下取整。 例如，如果你选择 51%，并且群集中有 4 台服务器，则将有 2 台服务器会同时处于脱机状态。  

5.  指定是否使用部署前（节点排出）脚本或部署后（节点恢复）脚本。  

    > [!TIP]  
    >  以下是可用于测试当前时间写入文本文件的部署前和部署后脚本的示例：  
    >   
    >  **前期部署**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **后期部署**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>若要将软件更新部署到服务器群集  

1.  将[软件更新部署](https://technet.microsoft.com/library/gg712304.aspx)到服务器群集集合。  

2.  [监视软件更新部署](https://technet.microsoft.com/library/gg712304.aspx)。  
