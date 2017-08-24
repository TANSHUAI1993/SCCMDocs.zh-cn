---
title: "Technical Preview 1601 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1601 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: ef0db5b11ae2be5edcb4db87400c5c273c89972e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1601-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1601 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍 System Center Configuration Manager Technical Preview 1601 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

 **此 Technical Preview 中的已知问题：**  

-   使用“客户端更新选项”将预生产客户端升级到生产客户端时，复选框的文本显示客户端版本为零 (0)，而不是实际的客户端内部版本号。 正确的预生产客户端版本显示在该选项的上方，该版本为你选择此选项后升级到生产客户端的版本号。  

-   更新到 Technical Preview 1601 并选择在预生产集合中测试 Configuration Manager 客户端时，不会升级该集合的客户端包。 此问题仅针对 Technical Preview 1601。  

     若要解决此问题，请执行以下操作之一：  

    -   在主站点的数据库上运行以下 SQL 脚本：  

        ```  
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   将新的分发点站点系统角色添加到实验室站点。 新的分发点会使用新的客户端包升级预生产集合。  

**以下是可以试用的此版本的新功能。**  

##  <a name="bkmk_hybrid1"></a>对 Microsoft Intune 集成的改进  
在 1601 技术预览版中，我们添加了对以下功能的支持：  

### <a name="improvements-to-conditional-access"></a>对条件访问的改进  

-   **对由 System Center Configuration Manager 管理的电脑的条件访问支持**  

     你现在可以为 System Center Configuration Manager 管理的 PC 设置条件访问策略，这要求 PC 符合合规性策略，以便能够访问 Exchange Online 和 SharePoint Online 服务。  凭借此新功能，你还可以通过合规性策略在 Azure AD 上注册 PC，以及对此注册进行监视和报告。  

    > [!NOTE]  
    >  Windows 10 尚不支持条件访问。  

    以下是使用此功能的先决条件：  

    -   Azure Active Directory Premium 订阅和 ADFS 同步。  

    -   Microsoft Intune 订阅。 应在 Configuration Manager 控制台中配置 Microsoft Intune 订阅。  

    -   [Azure AD 自动注册的先决条件](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)。  

    要使用该选项，你必须在 Configuration Manager 中创建具有以下所述特定规则的合规性策略，并在 Intune 控制台中设置条件访问策略。  此外，为确保仅允许合规的电脑访问，必须将 Windows 电脑要求设置为“设备必须合规”选项。 下面是适用于 System Center Configuration manager 管理的 PC 的合规性策略规则。  

    -   **需要在 Azure ActiveDirectory 中注册：**此规则检查用户的设备是否在加入到 Azure AD 的地方运行，如果不是，则在 Azure AD 中自动注册该设备。 仅 Windows 8.1 支持自动注册。 对于 Windows 7 PC，请部署 MSI 来执行自动注册。 有关详细信息，请参阅[此处](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)。  

    -   **在晚于特定天数的截止日期之前安装所有必需的更新：**此规则检查用户的设备是否在截止日期及指定的宽限期内具有所需的所有更新（在“所需的自动更新”规则中指定），并自动安装任何挂起的所需更新。  

    -   **需要使用 BitLocker 驱动器加密功能：**此规则检查设备的主驱动器（例如 C:\\）是否使用 BitLocker 进行了加密。 如果主驱动器上未启用 Bitlocker 加密，则将阻止设备对电子邮件和 SharePoint 服务的访问。  

    -   **需要反恶意软件：**此规则检查是否已启用并正在运行反恶意软件（仅限 System Center Endpoint Protection 或 Windows Defender）。  
         如果未启用，则将阻止对电子邮件和 SharePoint 服务的访问。  

    因不合规而被阻止的最终用户将在 SCCM 软件中心查看合规性信息，并且在纠正合规性问题之后启动新的策略评估。  

-   **使用运行状况证明服务的条件访问：**现在可以根据运行状况证明服务报告的设备运行状况来限制对电子邮件和 0365 服务的访问。  此外，设备健康状况报告中包含由 Intune 管理的设备。  

    在 configuration manager 控制台中添加了新的合规性规则，该规则允许你根据设备的健康状况指定应允许还是阻止设备进行访问。  要创建此规则，请打开“创建合规性策略向导”，然后添加新规则。  选择“运行状况证明服务报告为正常”作为条件，并将值设置为“True”。  这可以确保只有报告为健康的设备才可以访问你的公司资源。 有关运行状况证明服务和如何在 Intune 中报告设备的运行状况的详细信息，请参阅[设备运行状况证明](#bkmk_devicehealth)。  

-   **新合规性策略设置：**新合规性策略设置有助于提高用于访问公司电子邮件和 SharePoint 服务的设备的安全性：  

    -   **需要自动更新：**可以要求运行 Windows 8.1 或更高版本的设备允许自动安装更新，还可以指定要安装的更新的类别。  你可以选择仅安装标记为重要的更新，或者安装所有建议的更新。  

         要创建自动更新规则，请打开“创建合规性策略向导”，然后添加新规则。  选择“所需更新的最小分类”作为条件，并将值设置为以下可用值之一：“无”、“建议”和“重要”。  

        -   **无：**不自动安装更新。  

        -   **建议：**安装所有建议的更新  

        -   **重要：**仅安装归类为重要的更新。  

    -   **需要提供密码来解锁移动设备：**如果该设置设定为“是”，那么最终用户必须输入密码才能访问他们的设备。  

         要为解锁移动设备的密码创建规则，请打开“创建合规性策略向导”，然后添加新规则。 选择“需要提供密码来解锁空闲设备”作为条件，并将值设置为“True”。  

    -   **需要提供密码之前处于非活动状态的分钟数：**指定用户必须重新输入其密码前的空闲时间。  

         要创建此规则，请打开“创建合规性策略向导”，然后添加新规则。 选择“需要提供密码之前处于非活动状态的分钟数”作为条件，并将值设置为以下可用选项之一：1 分钟、5 分钟、15 分钟、30 分钟、1 小时。  

-   **替代默认规则 - 始终允许已注册 Intune 且合规的设备访问本地 Exchange：**  

     选中此选项时，允许已在 Intune 中注册且符合合规性策略的设备访问内部部署的 Exchange。 此规则将覆盖“默认规则”，这意味着，即使将“默认规则”设置为隔离或阻止访问，已注册并符合要求的设备也仍然能够访问内部部署的 Exchange。  
     当你希望已注册且合规的设备始终可通过内部部署的 Exchange 访问电子邮件时，使用该设置。  

     受以下平台支持：Windows Phone 8 及更高版本、iOS 6 及更高版本。 Android 4.0 及更高版本、Samsung KNOX Standard 4.0 及更高版本。  

     要使用此选项，请转到本地 Exchange 的“配置条件访问策略向导”的“常规”页面。  

##  <a name="bkmk_clientStatus"></a>客户端联机状态  
从技术预览 1601 版开始，可以在 Configuration Manager 控制台上一眼识别客户端是联机还是脱机。 通过控制台设备列表中已更新的图标和列，你可以评估你的环境中客户端的状态，由此识别问题区域及其他需要你注意的问题。  

如果客户端当前连接到 Configuration Manager 管理点站点系统角色，则处于联机状态。 只要管理点接收到来自客户端的类似于 ping 的消息，客户端就处于联机状态。 如果管理点有 5 分钟左右未接收到一条消息，则客户端的状态更改为脱机。  

### <a name="icons-for-client-status"></a>客户端状态图标  

|||  
|-|-|  
|![客户端的联机状态图标](media/online-status-icon.png)|客户端处于联机状态。|  
|![客户端的脱机状态图标](media/offline-status-icon.png)|客户端处于脱机状态。|  
|![客户端的未知状态图标](media/unknown-status-icon.png)|客户端状态未知。|  

### <a name="prerequisites"></a>先决条件  
 客户端联机状态无先决条件。 只要安装了 Configuration Manager 技术预览 1601 版，就可以开始使用它。  

### <a name="limitations"></a>限制  
 客户端联机状态仅适用于安装了 Configuration Manager 客户端的 Windows 计算机。 Mac 计算机、Linux 或 UNIX 计算机，或使用本地移动设备管理管理的设备不支持客户端联机状态。  

### <a name="to-view-client-online-status"></a>要查看客户端联机状态  

1.  在 Configuration Manager 控制台中，转到“资产和符合性”>“概览”>“设备”。  

2.  在列标题中右键单击，然后单击一个客户端联机状态字段，以便将其添加到设备视图。 这些字段是：  

    -   **设备联机状态** 将指示客户端当前是联机还是脱机。  

    -   **上次联机时间**表示客户端联机状态从脱机更改为联机时的时间。  

    -   **上次脱机时间**表示状态从联机更改为脱机时的时间。  

 要显示客户端状态的最新更改，请刷新控制台。  

##  <a name="bkmk_appmgmt1601"></a>对应用程序管理的改进  
 在 1601 技术预览版中，我们添加了对以下功能的支持：  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>管理批量采购的适用于 iOS 设备的应用程序  
 一些应用商店使你能够为你想在公司中运行的应用购买多个许可证。 这有助于降低跟踪多个已购买应用副本的管理成本。  

 Configuration Manager 现在可通过从应用商店中导入许可证信息以及跟踪已使用的许可证数量来帮助你管理通过这样的计划所购买的应用。  

 有关详细信息，请参阅[使用 Configuration Manager 管理通过批量采购计划购买的应用](https://technet.microsoft.com/library/mt627954.aspx)。  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS - 应用程序的应用配置<br />混合  
 一些 iOS 应用程序支持预配置应用程序应连接到的设置，如服务器或数据库。 Configuration Manager 现在支持将应用配置策略部署到设备，即使用户对此信息一无所知，也可立即使用此应用。 开发人员必须在其应用中启动此功能。  

 已公开发布的有限数量的应用当前支持预配置的设置；你可能还具有内部开发的特定行业应用支持这些设置。  

#### <a name="prerequisites-for-this-scenario"></a>此方案的先决条件  

-   必须已将 Microsoft Intune 订阅添加到 Configuration Manager。  

-   您必须将有效的 Apple APNs 证书添加到 Intune 订阅。  

-   你必须部署支持应用程序配置的 iOS 应用程序。  

#### <a name="try-it-out"></a>试试看！  
 满足上述先决条件后，必须创建使用 iOS 部署类型的 Configuration Manager 应用程序。 你使用的应用程序必须支持应用程序配置。 请参阅应用程序的供应商文档了解你可以配置哪些特定项目（名称/值对）。  

 然后，在应用程序部署过程中将应用程序配置策略与 iOS 部署类型相关联。 还可以为现有应用程序和集合部署“应用程序配置策略”节点的策略。  

 尝试完成以下任务，然后使用本主题顶部附近的反馈信息，让我们知道它们的工作方式：  

-   如果你的 iOS 应用程序支持应用程序配置，请查阅该应用程序供应商的文档以了解配置此应用程序所必须指定的名称和值对。  

-   启动“创建应用程序配置策略”向导。 在向导的“iOS 策略”页面，请尝试添加从应用程序供应商文档找到的名称和值对，或者导入包含所需的值的 XML 文件。  

-   在“部署软件”向导的“应用程序配置策略”页面，将创建的应用程序配置策略与应用程序中兼容的部署类型相关联。  

##  <a name="bkmk_compliance1601"></a>对合规性设置的改进  
 在 1601 技术预览版中，我们添加了对以下功能的支持：  

### <a name="microsoft-edge-browser-settings"></a>Microsoft Edge 浏览器设置  
 已将新的 Microsoft Edge 浏览器设置添加到 **Windows 8.1 和 Windows 10**配置项目（设置仅适用于 Windows 10 设备）。  

 要查看这些新设置，请在“创建配置项目”向导的配置项目“设备设置”页面中选择“Microsoft Edge”。  

 有关详细信息，请参阅[如何为不使用 System Center Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备创建配置项目](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Windows 10 Team 设备的合规性设置  
 使用这些新的合规性设置来配置运行 Windows 10 Team 的设备，例如 Surface Hub 设备。  

 要查看这些新设置，请在“创建配置项目”向导的配置项目“设备设置”页面中选择“Windows 10 协同版”。  

 有关详细信息，请参阅[如何为不使用 System Center Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备创建配置项目](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android - Samsung KNOX 标准版的展台模式<br />混合  
 你可以使用展台模式锁定设备，从而只允许某些功能运行。 例如，你可以让设备只运行一个指定的托管应用，也可以禁用设备上的音量按钮。 这些设置可用于设备的演示模型，也可用于专门执行一个功能的设备（如销售点设备）。 这些设置不适用于 **Windows 8.1 和 Windows 10** 配置项目中的 Samsung KNOX 标准版设备（设置仅适用于 Windows 10 设备）。  

 要查看这些新设置，请在“创建配置项目”向导的配置项目“设备设置”页面中选择“展台模式 - Samsung KNOX”。  

 有关详细信息，请参阅[如何为不使用 System Center Configuration Manager 客户端管理的 Windows 8.1 和 Windows 10 设备创建配置项目](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)。  
