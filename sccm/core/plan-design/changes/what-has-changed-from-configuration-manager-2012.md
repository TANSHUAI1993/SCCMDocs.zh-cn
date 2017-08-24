---
title: "自 Configuration Manager 2012 以来的更改 | Microsoft Docs "
description: "识别与 System Center 2012 Configuration Manager 相比，System Center Configuration Manger 中更改的内容和新功能。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: "51"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3eb93a99533a1569d8f72ca01d6dfcdc75da20
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>自 System Center 2012 Configuration Manager 以来 System Center Configuration Manager 中更改的内容

*适用范围：System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager Current Branch 引入了自 System Center 2012 Configuration Manager 以来的重要更改。 本主题帮助识别 System Center Configuration Manager 的基线版本 1511 中的显著更改和新增功能。 若要了解有关 System Center Configuration Manager 后续更新中引入的更改，请参阅 [System Center Configuration Manager 增量版本中的新增功能](/sccm/core/plan-design/changes/whats-new-incremental-versions)。



 2015 年 12 月发布的 System Center Configuration Manager（版本 1511）是 Microsoft 发布的当前 Configuration Manager 产品的初始版本。 通常，它被称为 System Center Configuration Manager current branch。 *Current Branch* 表明这是支持产品增量更新的版本。 它还提供区分 Configuration Manager 此发布版本和早期版本的方法。  

 System Center Configuration Manager：  

-   不在产品名中使用年份或产品标识符，与 Configuration Manager 2007 或 System Center 2012 Configuration Manager 等过去版本不同。

-   支持增量产品内更新，也称为更新版本。 初始版本是版本 1511。 一年发布几次作为控制台内更新的后续版本，如版本 1610。
-   使用基线版本安装。 1511 是原始的基线版本，而新的基线版本也会不定期发布，如 1702。 基线版本可用于安装新的 System Center Configuration Manager 站点和层次结构，或从 Configuration Manager 2012 支持的版本升级。




##  <a name="bkmk_updates"></a> Configuration Manager 的控制台内更新  
 System Center Configuration Manager 使用称为“更新和服务”的控制台中服务方法，可轻松找到并安装建议的更新。  

 某些版本仅可用作（Configuration Manager 控制台内）现有站点的更新，而不能用于安装新的 Configuration Manager 站点。   
例如，仅可从 Configuration Manager 控制台获取 1610 更新。 它用于更新已运行 System Center Configuration Manager 版本的站点。

我们还会定期发布更新版本（如更新 1702）作为新的基线版本。 此类更新可用于在无需以较旧的基线版本（如 1511）开始的情况下安装新的层次结构，并且将版本升级到最新版本。


有关使用更新的详细信息，请参阅 [System Center Configuration Manager 的更新](../../../core/servers/manage/updates.md)。  
有关基线版本的详细信息，请参阅[基线版本和升级版本](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)。

##  <a name="bkmk_servicepoint"></a> 新站点系统角色：服务连接点  
 **Microsoft Intune 连接器**被启用其他功能的新站点系统角色（**服务连接点**）所替换。 服务连接点：  

-   在将 Intune 与 System Center Configuration Manager 本地移动设备管理相集成时，替换 Microsoft Intune 连接器。  

-   用作管理设备的联系点。  

-   将有关部署的使用情况数据上传到 Microsoft 云服务。  

-   使应用到部署的更新在 Configuration Manager 控制台中可用。  

此站点系统角色支持联机和脱机操作模式。 有关详细信息，请参阅 [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)。  

##  <a name="bkmk_usage"></a> 使用数据收集  
 System Center Configuration Manager 收集有关站点和基础结构的使用情况数据。 编译此信息并通过服务连接点将其提交给 Microsoft 云服务。 需要启用 Configuration Manager 下载部署的更新，此部署应用于你使用的 Configuration Manager 版本。 设置服务连接点时，可以指定收集到的数据级别以及它是自动提交（联机模式）还是手动提交（脱机模式）。  

 有关详细信息，请参阅[使用情况数据级别和设置](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)。  

##  <a name="bkmk_AMT"></a> Intel 主动管理技术 (AMT) 的支持  
 通过 System Center Configuration Manager，已删除了 Configuration Manager 控制台中基于 AMT 的计算机的本机支持。 使用[适用于 Microsoft System Center Configuration Manager 的 Intel SCS 外接程序](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)时，基于 AMT 的计算机保持完全托管。 使用外接程序可以在 Configuration Manager 能够合并这些更改之前使用用于管理 AMT 的最新功能，同时删除引入的限制。  

为 System Center Configuration Manager 删除的集成 AMT 包括带外管理。 不再使用带外管理点站点系统角色或者该角色不再可用。  

请注意，System Center 2012 Configuration Manager 中的带外管理不受此更改的影响。

##  <a name="bkmk_out"></a> 弃用的功能  
 将从 Configuration Manager 控制台删除一些功能，如基于计算机的 [Intel 主动管理技术 (AMT) 的本机支持](#bkmk_AMT)。 将完全删除其他功能，如网络访问保护。 此外，不再支持某些较旧的 Microsoft 产品，如 Windows Vista、Windows Server 2008 和 SQL Server 2008。  

 有关弃用功能的列表，请参阅 [System Center Configuration Manager 的已删除和已弃用的功能](../../../core/plan-design/changes/removed-and-deprecated-features.md)。  

 有关受支持的产品、操作系统和配置的详细信息，请参阅 [System Center Configuration Manager 支持的配置](../../../core/plan-design/configs/supported-configurations.md)。  

## <a name="client-deployment"></a>客户端部署  
 System Center Configuration Manager 引入了新功能，用于在使用新软件升级站点的其余部分之前，对 Configuration Manager 客户端的新版本进行测试。 可以设置在其中试验新客户端的预生产集合。 对预生产中的新客户端软件感到满意后，可以将客户端提升为使用新版本自动升级站点的其余部分。  

 有关如何测试客户端的详细信息，请参阅[如何在 System Center Configuration Manager 中的预生产集合中测试客户端升级](../../../core/clients/manage/upgrade/test-client-upgrades.md)。  

## <a name="operating-system-deployment"></a>操作系统部署  

请注意对操作系统部署进行的以下更改：

-   在“创建任务序列向导”中，单击“从升级包升级操作系统”，然后将有一个新的可用任务序列类型。 它创建将计算机从 Windows 7、Windows 8 或 Windows 8.1 升级到 Windows 10 的步骤。 有关详细信息，请参阅 [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)。  

-   当部署操作系统时，Windows PE 对等缓存则变为可用。 运行部署操作系统的任务序列的计算机可使用 Windows PE 对等缓存从本地对等计算机（对等缓存源）中获取内容，而无需从分发点下载内容。 这有助于最大限度减小没有本地分发点的分支机构场景中的广域网 (WAN) 流量。 有关详细信息，请参阅 [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)。  

-   现在可将 Windows 的状态作为环境中的一种服务进行查看。 还可以创建维护服务计划以形成部署环，并在新版本发布时，确保 Windows 10 Current Branch 计算机保持最新。 此外，当 Windows 10 客户端对其 Current Branch (CB) 或 Current Branch for Business (CBB) 版本的支持即将到期时，用户可以查看警报。 有关详细信息，请参阅 [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md)。  

## <a name="application-management"></a>应用程序管理  

请注意对应用程序管理进行的以下更改：

-   通过 System Center Configuration Manager，可部署运行 Windows 10 及更高版本设备的通用 Windows 平台 (UWP) 应用。 请参阅[使用 System Center Configuration Manager 创建 Windows 应用程序](../../../apps/get-started/creating-windows-applications.md)。  

-   软件中心具有富有现代感的全新外观。 此前仅出现在应用程序目录中的应用（用户可用的应用）现在将出现在“应用程序”选项卡下的软件中心中。 这将使这些部署更易于被发现，并且用户不必参考应用程序目录。 此外，不再需要启用了 Silverlight 的浏览器了。 请参阅[规划和配置 System Center Configuration Manager 中的应用程序管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。  

-   通过 MDM 的新 Windows Installer 安装程序类型让你可以创建基于 Windows Installer 的应用并将其部署到运行 Windows 10 的已注册 PC 上。 请参阅[使用 System Center Configuration Manager 创建 Windows 应用程序](../../../apps/get-started/creating-windows-applications.md)。  

-   当为内部的 iOS 应用创建应用程序时，只需要为该应用指定安装程序 (.ipa) 文件。 不再需要指定相应的属性列表 (.plist) 文件。 请参阅[使用 System Center Configuration Manager 创建 iOS 应用程序](../../../apps/get-started/creating-ios-applications.md)。  

-   在 Configuration Manager 2012 中，若要在 Windows 应用商店中指定应用的链接，可以直接指定该链接，或者浏览到安装有该应用的远程计算机。 在 System Center Configuration Manager 中，仍然可以直接输入链接，但是可以直接从 Configuration Manager 控制台浏览应用商店以查找应用，而不用浏览到引用计算机。  

## <a name="software-updates"></a>软件更新  

请注意对软件更新进行的以下更改：

-   System Center Configuration Manager 现在可以检测计算机的软件更新管理方法之间的差异。 具体而言，它能区分连接到 Windows Update for Business (WUfB) 进行软件更新管理的 Windows 10 计算机和连接到 Windows Server Update Services (WSUS) 进行软件更新管理的计算机。 **UseWUServer** 属性为新属性，它指定了计算机是否由 WUfB 管理。 你可以在集合中使用此设置从软件更新管理中删除这些计算机。 有关详细信息，请参阅 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)。  

-   现在可从 Configuration Manager 控制台计划和运行 WSUS 清理任务。 在**软件更新点组件**属性中，当选择运行 WSUS 清理任务时，它将在下一次软件更新同步时运行。 过期的软件更新将设置为在 WSUS 服务器上被拒绝的状态，计算机上的 Windows 更新代理将不再扫描这些软件更新。 有关详细信息，请参阅 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)。  

## <a name="compliance-settings"></a>符合性设置  

请注意对符合性设置进行的以下更改：

-   System Center Configuration Manager 改进了用于创建配置项目的工作流。 现在，当创建配置项目并选择受支持的平台时，只有与该平台相关的设置才可用。 请参阅[System Center Configuration Manager 中的符合性设置入门](../../../compliance/get-started/get-started-with-compliance-settings.md)。  

-   **创建配置项目**向导现在可以更轻松地选择你想要创建的配置项目类型。 此外，新的和更新的配置项目可用于：  

    -   使用 Configuration Manager 客户端管理的 Windows 10 设备。  

    -   使用 Configuration Manager 客户端管理的 Mac OS X 设备。  

    -   使用 Configuration Manager 客户端管理的 Windows 台式计算机和服务器计算机。  

    -   未使用 Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备。  

    -   未使用 Configuration Manager 客户端管理的 Windows Phone 设备。  

    -   未使用 Configuration Manager 客户端管理的 iOS 和 Mac OS X 设备。  

    -   未使用 Configuration Manager 客户端管理的 Android 和 Samsung KNOX 标准版设备。  

 请参阅[如何在 System Center Configuration Manager 中创建配置项目](../../../compliance/deploy-use/create-configuration-items.md)。  

-   支持使用 Microsoft Intune 注册或使用 Configuration Manager 客户端管理的 Mac OS X 计算机上的管理设置。 请参阅[如何为没有使用 System Center Configuration Manager 客户端管理的 iOS 和 Mac OS X 设备创建配置项目](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)。  

## <a name="protect-data-and-site-infrastructure"></a>保护数据和站点基础结构  
System Center Configuration Manager 支持与 Windows Hello 企业版（以前为 Microsoft Passport for Windows）集成。 Windows Hello 企业版是运行 Windows 10 的设备上使用 Active Directory 或 Azure Active Directory 帐户取代密码、智能卡或虚拟智能卡进行登录的一种替代方法。 请参阅 [System Center Configuration Manager 中的 Windows Hello 企业版设置](../../../protect/deploy-use/windows-hello-for-business-settings.md)。

## <a name="mobile-device-management-with-microsoft-intune"></a>使用 Microsoft Intune 进行移动设备管理  
 System Center Configuration Manager 引入了改进移动设备管理体验的内容，其中包括：  

-   对用户可以注册的设备数设置限制。  

-   指定公司门户用户在注册或使用应用之前必须接受的条款和条件。  

-   添加了设备注册管理器角色，以帮助管理大量设备。  

有关 Configuration Manager 和 Intune 的移动设备管理功能的详细信息，请参阅 [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md)（System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)）。  

## <a name="on-premises-mobile-device-management"></a>本地移动设备管理  
 现在可以使用本地 Configuration Manager 基础结构管理移动设备。 所有设备管理和管理数据都在本地处理并且不是 Microsoft Intune 或其他云服务的一部分。 此类设备管理不需要客户端软件。 Configuration Manager 管理具有内置于设备操作系统的功能的设备。  

 若要了解详细信息，请参阅[在 System Center Configuration Manager 中使用本地基础结构管理移动设备](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。
