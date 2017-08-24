---
title: "在 Windows 10 中与适用于企业的 Windows 更新集成 | Microsoft Docs"
description: "将可使组织中基于 Windows 10 的设备保持最新状态的 Windows Update for Business 用于连接到 Windows 更新服务的设备。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 26e73a69d5e6ca69e766fcf3cedd992353c92cd6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>在 Windows 10 中与 Windows Update for Business 集成

*适用范围：System Center Configuration Manager (Current Branch)*

当基于 Windows 10 的设备直接连接到 Windows Update (WU) 服务时，Windows Update for Business (WUfB) 能够让你使组织中的这些设备始终具有最新的安全防御和 Windows 功能。 Configuration Manager 能够区分使用 WUfB 和 WSUS 来获取软件更新的 Windows 10 计算机。  

 当 Configuration Manager 客户端配置为从 WU 接收更新后（其中包括 WUfB 或 Windows 预览体验成员），一些 Configuration Manager 功能将不再可用：  

-   Windows Update 符合性报告:  

    -   Configuration Manager 将不会察觉发布到 WU 的更新。 配置为从 WU 接收更新的 Configuration Manager 客户端将会在 Configuration Manager 控制台中将这些更新显示为“未知”。  

    -   针对总体符合性状态的故障排除会很困难，因为“未知”  状态曾仅用于尚未报告从 WSUS 返回的扫描状态的客户端。  现在，它还包括从 WU 接收更新的 Configuration Manager 客户端。  

    -   基于更新符合性状态的条件性访问（用于企业资源）对从 WU 接收更新的客户端将无法按预期方式运行，因为它们将永远不会满足 Configuration Manager 的符合性。  

    -   定义更新符合性是整体更新符合性报告的一部分，也无法按预期方式工作。  定义更新符合性也是条件性访问评估的一部分  

-   基于更新符合性状态的 Defender 的总体 Endpoint Protection 报告将不会返回准确的结果，因为缺少扫描数据。  

-   Configuration Manager 将无法将 Microsoft 更新（如 Office、IE 和 Visual Studio）部署到连接 WUfB 以接收更新的客户端。  

-   Configuration Manager 将无法将发布到 WSUS 并通过 Configuration Manager 管理的第三方更新部署到连接 WUfB 以接收更新的客户端。  

-   使用软件更新基础结构的 Configuration Manager 完整客户端部署将不能用于连接 WUfB 以接收更新的客户端。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>标识使用 WUfB for Windows 10 更新的客户端  
 使用以下步骤标识使用 WUfB 以获取 Windows 10 更新和升级的客户端，将这些客户端配置为停止使用 WSUS 来获取更新，并部署客户端代理设置来禁用这些客户端的软件更新工作流。  

 **先决条件**  

-   运行 Windows 10 桌面专业版或 Windows 10 企业版的版本 1511 或更高版本的客户端  

-   部署了[Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) ，并且客户端使用 WUfB 来获取 Windows 10 更新和升级。  

#### <a name="to-identify-clients-that-use-wufb"></a>标识使用 WUfB 的客户端  

1.  禁用 Windows 更新代理，以便它不会针对 WSUS 进行扫描（如果以前已启用）。   
    可以设置注册表项 **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**，以指示是否针对 WSUS 或 Windows 更新扫描计算机。  如果值是 2，不会针对 WSUS 进行扫描。  

2.  存在新属性“UseWUServer”（Configuration Manager 资源浏览器中“Windows 更新”节点下）。  

3.  基于 **UserWUServer** 属性为通过 WUfB 连接以获取更新和升级的所有计算机创建一个集合。  

4.  创建客户端代理设置以禁用软件更新工作流，并将该设置部署到直接连接到 WUfB 的计算机的集合。  

5.  通过 WUfB 管理的计算机会在符合性状态中显示“未知”，且不会计入总体符合性百分比中。  

## <a name="configure-windows-update-for-business-deferral-policies"></a>配置 Windows Update for Business 延迟策略
<!-- 1290890 -->
从 Configuration Manager 版本 1706 开始，针对 Windows 10 功能更新或直接由 Windows Update for Business 托管的 Windows 10 设备的质量更新，可以配置延迟策略。 你可以在“软件库” > “Windows 10 维护服务”下方的新“Windows Update for Business 策略”节点中管理延迟策略。

### <a name="prerequisites"></a>先决条件
由 Windows Update for Business 托管的 Windows 10 设备必须具有 Internet 连接。

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>创建 Windows Update for Business 延迟策略
1. 在“软件库” > “Windows 10 维护服务” > “Windows Update for Business 策略”中
2. 在“主页”选项卡的“创建”组中，选择“创建 Windows Update for Business 策略”，以打开“创建 Windows Update for Business 策略向导”。
3. 在“常规”页上，提供策略的名称和描述。
4. 在“延迟策略”页上，配置是否要延迟或暂停功能更新。    
    功能更新通常是针对 Windows 的新增功能。 在配置“分支就绪级别”设置后，你可以根据其可用性定义是否要延迟从 Microsoft 接收功能更新以及延迟时长。
    - 分支就绪级别：设置设备将为其接收 Windows 更新的分支（Current Branch 或 Current Branch for Business）。
    - 延迟期(天)：指定功能更新将被延迟的天数。 你可以自更新发布之日起，在 180 天内延迟接收这些功能更新。
    - 暂停功能更新启动：选择是否要暂停设备接收功能更新，暂停时间为自暂停更新之日起的 60 天内。 在设置的最大天数过后，暂停功能将自动过期，并且设备将扫描 Windows 更新以获取适用的更新。 在此扫描之后，你可以再次暂停更新。 通过清除该复选框，可以取消暂停功能更新。   
5. 选择是否要延迟或暂停质量更新。     
    质量更新通常是对现有 Windows 功能的修复和改进，通常会在每个月的第一个星期二发布，虽然 Microsoft 可以在任何时候发布。 你可以根据其可用性定义是否要延迟接收质量更新，以及它的延迟时长。
    - 延迟期(天)：指定功能更新将被延迟的天数。 你可以自更新发布之日起，在 180 天内延迟接收这些功能更新。
    - 暂停质量更新启动：选择是否要暂停设备接收质量更新，暂停时间为自暂停更新之日起的 35 天内。 在设置的最大天数过后，暂停功能将自动过期，并且设备将扫描 Windows 更新以获取适用的更新。 在此扫描之后，你可以再次暂停更新。 通过清除该复选框，可以取消暂停质量更新。
6. 选择“安装来自其他 Microsoft 产品的更新”，可启用使延迟设置适用于 Microsoft 更新以及 Windows 更新的组策略设置。
7. 选择“包括 Windows 更新中的驱动程序”，可自动更新 Windows 更新中的驱动程序。 如果清除此设置，则不会从 Windows 更新下载驱动程序更新。
8. 完成向导以创建新的延迟策略。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>部署 Windows Update for Business 延迟策略
1. 在“软件库” > “Windows 10 维护服务” > “Windows Update for Business 策略”中
2. 在“主页”选项卡的“部署”组中，选择“部署 Windows Update for Business 策略”。
3. 配置下列设置：
    - 要部署的配置策略：选择要部署的 Windows Update for Business 策略。
    - 集合：单击“浏览”，可选择要在其中部署策略的集合。
    - 在支持时修正非符合性规则：选择该选项，可自动修正 Windows Management Instrumentation (WMI)、注册表、脚本和 Configuration Manager 所注册移动设备的所有设置的任何非符合性规则。
    - 允许维护时段外的修正：如果已为你向其部署策略的集合配置了维护时段，启用此选项可以让符合性设置在维护时段外修正值。 有关维护时段的详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。
    - 生成警报：配置一个警报，在指定日期和时间之前配置基线符合性小于指定百分比时，生成一个警报。 你也可以指定是否希望将警报发送到 System Center Operations Manager。
    - 随机延迟(小时)：指定延迟时段，以免网络设备注册服务的处理负荷过重。 默认值为 64 小时。
    - 计划：指定在客户端计算机上对部署的配置文件进行评估所依据的符合性评估计划。 该计划可以是简单计划或自定义计划。 当用户登录时，客户端计算机将评估配置文件。
4.  完成向导以部署配置文件。
