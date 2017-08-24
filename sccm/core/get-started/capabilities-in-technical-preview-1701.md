---
title: "Technical Preview 1701 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview（版本 1701）中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b330c97a0853d1673f1cf7e0691891b72407fa51
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1701 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*



本文介绍了 System Center Configuration Manager Technical Preview（版本 1701）中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    


**以下是可以试用的此版本的新功能。**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>软件更新点的边界组改进
从此预览版开始，现在可使用边界组将客户端与软件更新点关联。 这属于将边界组更改扩展到管理其他站点系统角色的持续工作中的一部分。  Technical Preview 1609 和版本 1610 中的 Current Branch 首次引入了边界组更改。  

在此预览版中，可使用新边界组行为管理客户可使用的软件更新点，方法类似于管理客户端可使用的分发点：  

- 配置边界组，使其与一个或多个托管软件更新点的服务器关联。
- 正在寻找新软件更新点的客户端将尝试使用与其当前边界组关联的软件更新点。
- 如果客户端无法获取当前软件更新点，并无法从当前边界组找到软件更新点，客户端会使用“回退”行为扩展可使用的软件更新点的可用池。    

若要深入了解边界组，请参阅 Current Branch 内容中的[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。

但是在此预览版中，仅部分实现了软件更新点的边界组。 可添加软件更新点和配置包含软件更新点的邻居边界组，但是尚不支持软件更新点的回退时间，并且在启动回退前，客户端需要等待 2 个小时。

下面介绍了此 Technical Preview 中软件更新点的行为：  

-   **新客户端使用边界组选择软件更新点，**安装版本 1701 后所安装的客户端从那些与客户端边界组关联的软件更新点中选取一个。

  这将替代以前的行为，即客户端从共享客户端林的软件更新点列表中随机选取一个。   

-   **以前安装的客户端继续使用当前的软件更新点，直到它们回退找到新的软件更新点。**
回退前，以前安装的客户端以及已具有软件更新点的客户端将继续使用该软件更新点。 这包括未与客户端当前边界组关联的软件更新点。 它们不会直接尝试从当前边界组查找和使用软件更新点。

  仅在客户端无法获取其当前软件更新点和启动回退时，已具有软件更新点的客户端才会开始使用这个新边界组行为。
切换到新行为时发生这种延迟是故意为之的。 原因在于软件更新点的更改可导致网络带宽的大量使用，因为客户端会与新软件更新点同步数据。 过渡中的延迟有助于在所有客户端同时切换到新软件更新点时避免网络饱和。

-   **回退时间配置：**此 Technical Preview 中不支持配置客户端启动回退以搜索新软件更新点的时间。 这包括配置“回退时间(以分钟为单位)”和“从不回退”，可以针对不同边界组关系进行配置。

  但是，客户端可将客户端尝试连接到其当前软件更新点的当前行为保留 2 小时，然后再启动回退以查找可用的新软件更新点。

  客户端使用回退时，将使用回退的边界组配置创建可用软件更新点的池。 该池包括客户端当前边界组、邻居边界组和客户端站点默认边界组中的所有软件更新点。

- **配置默认站点边界组：**  
 考虑将软件更新点添加到 Default-Site-Boundary-Group&lt;sitecode>。 这可确保非另一边界组成员的客户端可回退以查找软件更新点。


若要管理边界组的软件更新点，请使用 [Current Branch 文档中的流程](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups)，但请记住，你可以配置的回退时间还不能用于软件更新点。


## <a name="hardware-inventory-collects-uefi-information"></a>硬件清单将收集 UEFI 信息
新的硬件清单类 (**SMS_Firmware**) 和属性 (**UEFI**) 可帮助确定是否以 UEFI 模式启动计算机。 如果以 UEFI 模式启动计算机，则 **UEFI** 属性设为 **TRUE**。 默认情况下，这在硬件清单中处于启用状态。 有关硬件清单的详细信息，请参阅[如何配置硬件清单](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

## <a name="improvements-to-operating-system-deployment"></a>对操作系统部署的改进
我们对操作系统部署做了以下改进，大部分改进根据用户语音反馈进行的。
- [**支持更多应用程序执行“安装应用程序”任务序列步骤**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t)：增加了应用程序的最大数量，因此可以在“安装应用程序”任务序列步骤中安装最多 99 个应用程序。 以前的最大数量为 9 个应用程序。
- [**在“安装应用”任务序列步骤中选择多个应用**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step)：在任务序列编辑器中向“安装应用程序”任务序列步骤添加应用程序时，现在可从“选择要安装的应用程序”面板选择多个应用程序。
- [**过期独立介质**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media)：创建独立介质时，可使用新选项对介质设置可选开始日期和到期日期。 默认情况下，这些设置处于禁用状态。 独立介质运行前，该日期将与计算机上的系统时间进行比较。 如果系统时间早于开始时间或晚于过期时间，则独立介质不会启动。 也可通过使用 New-CMStandaloneMedia PowerShell cmdlet 启用这些选项。
- [**独立介质中支持额外内容**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic)：独立介质中现在支持额外内容。 可选择将额外的包、驱动程序包和应用程序，以及任务序列中引用的其他内容暂存在介质中。 以前，仅任务序列中引用的内容才暂存在独立介质中。
- [**“自动应用驱动程序”任务序列步骤可配置超时**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout)：在发出 HTTP 目录请求时，新任务序列变量现在可在“自动应用驱动程序”任务序列步骤中配置超时值。 下面是可用的变量和默认值（以秒为单位）：
   - SMSTSDriverRequestResolveTimeOut 默认值：60
   - SMSTSDriverRequestConnectTimeOut 默认值：60
   - SMSTSDriverRequestSendTimeOut 默认值：60
   - SMSTSDriverRequestReceiveTimeOut 默认值：480
- [**任务序列步骤现在会显示包 ID**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste)：任何引用包、驱动程序包、操作系统映像、启动映像或操作系统升级包的任务序列步骤现在将显示引用对象的包 ID。 任务序列步骤引用应用程序时，将显示对象 ID。
- **通过内部版本号跟踪 Windows 10 ADK**：现在可通过内部版本号跟踪 Windows 10 ADK，确保自定义 Windows 10 启动映像时有更多受支持的体验。 例如，如果站点使用适用于 Windows 10 的 Windows ADK（版本 1607），那么控制台中仅可自定义版本号为 10.0.14393 的启动映像。 若要深入了解如何自定义 WinPE 版本，请参阅[自定义启动映像](/sccm/osd/get-started/customize-boot-images)。
- **默认启动映像源路径无法再进行更改**：默认启动映像由 Configuration Manager 托管，并且无法再在 Configuration Manager 控制台中或通过使用 Configuration Manager SDK 更改默认启动映像源路径。 可继续为自定义启动映像配置自定义源路径。

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>使用基于云的分发点托管软件更新
从此预览版本开始，可使用基于云的分发点来托管软件更新包。 但是，因为可将客户端配置为从 Microsoft 更新直接下载软件更新，所以请考虑将软件更新包部署到基于云的分发点时将产生的额外费用。

若要深入了解如何使用基于云的分发点，请参阅 Configuration Manager 的 Current Branch 内容中的[使用基于云的分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)。

## <a name="validate-device-health-attestation-data-via-management-points"></a>通过管理点验证设备运行状况证明数据

从此预览版本开始，可配置管理点以验证云或本地运行状况证明服务的运行状况证明报告数据。 通过“管理点组件属性”对话框中的新“高级选项”，可“添加”、“编辑”或“删除”“本地设备运行状况证明服务 URL”。 还可将客户端代理的“自定义设备设置”指定为“使用本地运行状况证明服务”。  将此设置设为“是”将启用向本地管理点（而不是基于云的服务）报告。

### <a name="try-it-out"></a>试试看

- **在管理点上启用本地设备运行状况证明**<br>  在 Configuration Manager 控制台中，导航到管理点，打开“管理点组件属性”，然后单击“高级选项”选项卡。 单击“添加”，然后为“本地设备运行状况证明服务 URL”指定本地 URL（例如 https://10.10.10.10）。
- **为客户端代理启用本地管理点运行状况证明报告**<br>在 Configuration Manager 控制台中，选择“管理” > “客户端设置”，然后双击或创建新的“自定义设备设置”。 选择“计算机代理”，然后将“使用本地运行状况证明服务”设为“是”。 如果将“启用与设备运行状况证明服务的通信”设为“是”，并将“使用本地运行状况证明”设为“否”，则管理点将使用基于云的设备运行状况证明服务。

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>将 OMS 连接器用于 Microsoft Azure 政府云
在此 Technical Preview 中，现在可使用 Microsoft Operations Management Suite (OMS) 连接器连接 Microsoft Azure 政府云上的 OMS 工作区。  

为此，请修改配置文件，使其指向政府云，然后安装 OMS 连接器。

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>设置连接到 Microsoft Azure 政府云的 OMS 连接器
1.  在任何安装了 Configuration Manager 控制台的计算机上，编辑以下配置文件，使其指向政府云：***&lt;CM 安装路径>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **编辑：**

    将设置名称 FairFaxArmResourceID 的值更改为等于“https://management.usgovcloudapi.net/”

   - **初始：**&lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **编辑后：**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  将设置名称 FairFaxAuthorityResource 的值更改为等于“https://login.microsoftonline.com/”

  - **原始：**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **编辑后：**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.  保存包含这两种更改的文件后，请在同一台计算机上重启 Configuration Manager 控制台，然后使用该控制台安装 OMS 连接器。 若要安装连接器，请使用[将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) 中的信息，选择 Microsoft Azure 政府云上的 **Microsoft Operations Management Suite**。

3.  OMS 连接器安装后，使用任何连接到站点的控制台时，可使用与政府云的连接。

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>在混合 MDM 的创建向导中，不再以 Android 和 iOS 版本为目标

自用于混合移动设备管理 (MDM) 的此技术预览起，为 Intune 托管设备创建新策略和配置文件时，无需再将特定版本的 Android 和 iOS 作为目标。 转而选择下述某个设备类型：

- Android
- Samsung KNOX 标准版 4.0 及更高版本
- iPhone
- iPad

此更改会影响以下项的创建向导：

- 配置项目
- 相容性策略
- 证书配置文件
- 电子邮件配置文件
- VPN 配置文件
- Wi-Fi 配置文件

由于此更改，混合部署可为 Android 和 iOS 新版本更快提供支持，无需新的 Configuration Manager 版本或扩展。 Intune 独立版中支持新版本后，用户就可将其移动设备升级到此版本。

为防止从 Configuration Manager 先前版本升级时出现问题，移动操作系统版本仍在这些项的属性页中可用。 如果仍需以特定版本为目标，可创建新项，然后在新创建的项的属性页上指定目标版本。
