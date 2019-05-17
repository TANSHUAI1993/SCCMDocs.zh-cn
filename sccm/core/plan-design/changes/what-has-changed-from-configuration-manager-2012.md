---
title: 自 Configuration Manager 2012 以来的更改
description: 识别与 System Center 2012 Configuration Manager 相比，System Center Configuration Manger 中更改的内容和新功能。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb6071e576a12773c0aa5627dad80700db843f43
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496106"
---
# <a name="whats-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>自 System Center 2012 Configuration Manager 以来 System Center Configuration Manager 中更改的内容

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager Current Branch 引入了自 System Center 2012 Configuration Manager 以来的重要更改。 本文确定了 System Center Configuration Manager 基线版本 1511 中的显著更改和新增功能。 若要了解有关 System Center Configuration Manager 后续更新中引入的更改，请参阅 [System Center Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。

2015 年 12 月发布的 System Center Configuration Manager（版本 1511）是 Microsoft 发布的当前 Configuration Manager 产品的初始版本。 它通常被称为 System Center Configuration Manager Current Branch。 Current Branch 表明此版本支持产品增量更新。 它还提供区分 Configuration Manager 此发布版本和早期版本的方法。  

System Center Configuration Manager：  

- 不在产品名称中使用年份或产品标识符，与 Configuration Manager 2007 或 System Center 2012 Configuration Manager 等旧版本不同。  

- 支持增量产品内更新，也称为更新版本。 初始版本是版本 1511。 一年发布几次作为控制台内更新的后续版本，如版本 1810。  

- 使用基线版本安装。 1511 是原始的基线版本，而新的基线版本也会不定期发布，如 1902。 基线版本可用于安装新的 System Center Configuration Manager 站点和层次结构，或从 Configuration Manager 2012 支持的版本升级。  



##  <a name="bkmk_updates"></a> Configuration Manager 的控制台内更新  

System Center Configuration Manager 使用称为“更新和服务”的控制台中服务方法，可轻松找到并安装建议的更新。  

一些版本只用作现有站点的更新（在 Configuration Manager 控制台内），而无法用于安装新 Configuration Manager 站点。 例如，仅可从 Configuration Manager 控制台获取 1810 更新。 它用于更新已运行 System Center Configuration Manager 版本的站点。

我们还会定期发布更新版本（如更新 1902）作为新的基线版本。 此类更新可用于在无需以较旧的基线版本（如 1802）开始的情况下安装新的层次结构，并且将版本升级到最新版本。


若要详细了解如何使用更新，请参阅 [Configuration Manager 更新](/sccm/core/servers/manage/updates)。  
若要详细了解基线版本，请参阅[基线版本和更新版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)。



##  <a name="bkmk_servicepoint"></a> 新站点系统角色：服务连接点  

**Microsoft Intune 连接器**被启用其他功能的新站点系统角色（**服务连接点**）所替换。 服务连接点：  

- 在将 Intune 与 System Center Configuration Manager 本地移动设备管理相集成时，替换 Microsoft Intune 连接器。  

- 用作管理设备的联系点。  

- 将有关部署的使用情况数据上传到 Microsoft 云服务。  

- 使应用到部署的更新在 Configuration Manager 控制台中可用。  

此站点系统角色支持联机和脱机操作模式。 有关详细信息，请参阅[关于服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。  



##  <a name="bkmk_usage"></a> 使用数据收集  

Configuration Manager 收集站点和基础设施的使用情况数据。 编译此信息并通过服务连接点将其提交给 Microsoft 云服务。 根据要求，必须将 Configuration Manager 启用为下载可供部署的更新，以应用于所使用的 Configuration Manager 版本。 设置服务连接点时，可以指定收集到的数据级别，以及是自动提交（联机模式）还是手动提交（脱机模式）数据。  

有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。  



##  <a name="bkmk_AMT"></a> Intel 主动管理技术 (AMT) 的支持  

Configuration Manager Current Branch 已从 Configuration Manager 控制台中删除对基于 AMT 的计算机的本机支持。 使用[适用于 Microsoft System Center Configuration Manager 的 Intel SCS 外接程序](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)时，基于 AMT 的计算机保持完全托管。 使用外接程序可以在 Configuration Manager 能够合并这些更改之前使用用于管理 AMT 的最新功能，同时删除引入的限制。  

带外管理随适用于 Configuration Manager 的集成 AMT 一起删除。 带外管理点站点系统角色不再可用。  

> [!Note]   
> System Center 2012 Configuration Manager 中的带外管理不受此更改的影响。  



##  <a name="bkmk_out"></a> 弃用的功能  

[对基于 Intel 主动管理技术 (AMT) 的计算机的本机支持](#bkmk_AMT)等一些功能从 Configuration Manager 控制台中删除。 网络访问保护等另一些功能遭完全删除。 此外，不再支持一些旧版 Microsoft 产品，如 Windows Vista、Windows Server 2008 和 SQL Server 2008。  

有关已弃用功能列表，请参阅[已删除项和已弃用项](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)。  

若要详细了解受支持的产品、操作系统和配置，请参阅[受支持的配置](/sccm/core/plan-design/configs/supported-configurations)。  



## <a name="client-deployment"></a>客户端部署  

Configuration Manager 引入了新功能，用于在使用新软件升级站点的其余部分之前，测试 Configuration Manager 客户端的新版本。 可以设置在其中试验新客户端的预生产集合。 对预生产中的新客户端软件感到满意后，便能将客户端提升为使用新版本自动升级站点的其余部分。  

若要详细了解如何测试客户端，请参阅[如何在预生产集合中测试客户端升级](/sccm/core/clients/manage/upgrade/test-client-upgrades)。  



## <a name="os-deployment"></a>OS 部署  

请注意以下 OS 部署变更：

- 在“创建任务序列向导”中，新增以下任务序列类型：通过升级包升级操作系统。 它创建将计算机从 Windows 7、Windows 8 或 Windows 8.1 升级到 Windows 10 的步骤。 有关详细信息，请参阅[将 Windows 升级到最新版本](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)。  

- 现在可以在部署操作系统时使用 Windows PE 对等缓存。 如果运行任务序列来部署 OS，计算机可使用 Windows PE 对等缓存从对等缓存源中获取内容，而无需从分发点下载内容。 此行为有助于最大限度减小没有本地分发点的分支机构方案中的 WAN 流量。 有关信息，请参阅[准备 Windows PE 对等缓存来减少 WAN 流量](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)。  

- 现在可将 Windows 的状态作为环境中的一种服务进行查看。 还可以通过创建服务计划来形成部署环，并确保在新内部版本发布时 Windows 10 Current Branch 计算机为最新。 此外，还可以在对 Windows 10 客户端内部版本的支持即将结束时查看警报。 有关详细信息，请参阅[管理 Windows 即服务](/sccm/osd/deploy-use/manage-windows-as-a-service)。  



## <a name="application-management"></a>应用程序管理  

请注意对应用程序管理进行的以下更改：

- 借助 Configuration Manager，可以为运行 Windows 10 及更高版本的设备部署通用 Windows 平台 (UWP) 应用。 有关详细信息，请参阅[创建 Windows 应用](/sccm/apps/get-started/creating-windows-applications)。  

- 软件中心具有富有现代感的全新外观。 用户可用应用之前仅出现在应用目录中，现在出现在软件中心内的“应用”选项卡下。此行为让这些部署更易于被发现，并免去了用户参考应用目录的麻烦。 此外，不再必须使用已启用 Silverlight 的浏览器了。 有关详细信息，请参阅[规划和配置应用程序管理](/sccm/apps/plan-design/plan-for-and-configure-application-management)。  

- 通过 MDM 的新 Windows Installer 安装程序类型让你可以创建基于 Windows Installer 的应用并将其部署到运行 Windows 10 的已注册 PC 上。 有关详细信息，请参阅[创建 Windows 应用](/sccm/apps/get-started/creating-windows-applications)。  

- 当为内部的 iOS 应用创建应用程序时，只需要为该应用指定安装程序 (.ipa) 文件。 不再需要指定相应的属性列表 (.plist) 文件。 请参阅[创建 iOS 应用](/sccm/apps/get-started/creating-ios-applications)。  

- 在 Configuration Manager 2012 中，若要在 Windows 应用商店中指定应用的链接，可以直接指定该链接，或者浏览到安装有该应用的远程计算机。 在 Configuration Manager Current Branch 中，虽仍能直接输入链接，但现在可以直接在 Configuration Manager 控制台中浏览应用商店以查找应用，而不用转到引用计算机。  



## <a name="software-updates"></a>软件更新  

请注意对软件更新进行的以下更改：

- Configuration Manager 现在可以为计算机检测软件更新管理方法差异。 具体而言，它可以区分连接到适用于企业的 Windows 更新 (WUfB) 的 Windows 10 计算机和连接到 WSUS 的计算机。 **UseWUServer** 属性为新属性，它指定了计算机是否由 WUfB 管理。 你可以在集合中使用此设置从软件更新管理中删除这些计算机。 有关详细信息，请参阅 [Integration with Windows Update for Business in Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)。  

- 现在可从 Configuration Manager 控制台计划和运行 WSUS 清理任务。 在“软件更新点组件”属性中，如果你选择运行 WSUS 清理任务，它便会在下一次软件更新同步时运行。 过期的软件更新被设置为，在 WSUS 服务器上处于拒绝状态，计算机上的 Windows 更新代理不再扫描这些软件更新。 有关详细信息，请参阅 [Schedule and run the WSUS clean up task](/sccm/sum/deploy-use/software-updates-maintenance)。  



## <a name="compliance-settings"></a>符合性设置  

请注意对符合性设置进行的以下更改：

- Configuration Manager 改进了用于创建配置项目的工作流。 现在，当创建配置项目并选择受支持的平台时，只有与该平台相关的设置才可用。 请参阅[符合性设置入门](/sccm/compliance/get-started/get-started-with-compliance-settings)。  

- **创建配置项目**向导现在可以更轻松地选择你想要创建的配置项目类型。 此外，新的和更新的配置项目可用于：  

    - 使用 Configuration Manager 客户端管理的 Windows 10 设备  

    - 使用 Configuration Manager 客户端管理的 Mac OS X 设备  

    - 使用 Configuration Manager 客户端管理的 Windows 台式计算机和服务器计算机  

    - 未使用 Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备  

    - 未使用 Configuration Manager 客户端管理的 Windows Phone 设备  

    - 未使用 Configuration Manager 客户端管理的 iOS 和 Mac OS X 设备  

    - 未使用 Configuration Manager 客户端管理的 Android 和 Samsung KNOX 标准版设备  
  
    有关详细信息，请参阅[如何创建配置项目](/sccm/compliance/deploy-use/create-configuration-items)。  

- 支持在 Mac OS X 计算机上管理设置，这些计算机要么是使用 Microsoft Intune 进行注册，要么是使用 Configuration Manager 客户端进行管理。 请参阅[如何为不使用 Configuration Manager 客户端管理的 iOS 和 Mac OS X 设备创建配置项目](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)。  



## <a name="on-premises-mobile-device-management"></a>本地移动设备管理  

现在可以使用本地 Configuration Manager 基础结构管理移动设备。 所有设备和管理数据都在本地处理，并且不属于 Microsoft Intune 或其他云服务。 此类设备管理不需要客户端软件。 Configuration Manager 使用设备 OS 内置的功能来管理设备。  

有关详细信息，请参阅[使用本地基础结构管理移动设备](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)。
