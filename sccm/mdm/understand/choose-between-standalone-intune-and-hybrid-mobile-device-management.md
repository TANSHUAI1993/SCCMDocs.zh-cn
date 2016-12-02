---
title: "选择 Intune 独立版或混合 MDM | System Center Configuration Manager"
description: "选择是使用 Intune 和 Configuration Manager 部署混合移动设备管理还是运行 Intune 独立版。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>在 Microsoft Intune 独立版与使用 System Center Configuration Manager 实现的混合移动设备管理之间做出选择

*适用范围：System Center Configuration Manager (Current Branch)*

在使用 Microsoft Intune 实现移动设备管理 (MDM) 方面，一个最常见的问题是“应该通过 Intune 和 Configuration Manager 部署混合 MDM 还是应该在只涉及云的配置中运行 Intune 独立版本？” 这个决策非常重要，因为在实施后进行改变并非易事。  

 Intune 独立版部署不涉及任何本地基础结构，并通过 Web 控制台进行管理。 这种部署敏捷轻量，首选云的组织会比较偏好这种方式。  

 混合 MDM 部署涉及 Intune 和 Configuration Manager，通过经验丰富的 Configuration Manager 管理员所熟悉的工具进行管理。 这种部署通过“单一管理平台”管理 MDM 和传统客户端，并可在大规模环境中进行扩展。  

##  <a name="what-does-intune-standalone-mean"></a>什么是 Intune 独立版？  
 Intune 就其核心而言是一种云服务。 它在北美、欧洲和亚洲设有托管的 Intune 数据中心，可以向移动设备提供安全策略、电子邮件和 Wi-fi 配置文件、应用程序、清单等。  

 实施 Intune 独立版不需要任何本地基础结构。 所有配置、管理、部署和报表通过基于 Web 的控制台完成，并且可从世界上任何地方访问该控制台。  

 若要使用本地应用程序，如 Microsoft Exchange 和网络设备注册服务 (NDES)，可通过本地连接器连接到 Intune 服务。  

 由于 Intune 是一种云服务，可在较短时间内实现其构建和部署。  

##  <a name="what-does-hybrid-mdm-mean"></a>什么是混合 MDM？  
 对希望充分利用 Configuration Manager 投资的组织、需要实现精细控制的客户或应用需求超出 Intune 范围的客户，可使用一种混合实现，这种方式通过 Intune 来管理移动设备。  

 混合部署需要 Microsoft System Center 2012 Configuration Manager SP1 或更高版本。  

 通过服务连接点站点系统角色（以前称为 Microsoft Intune Connector）将 Intune 服务连接到 Configuration Manager，该角色安装在 Configuration Manager 层次结构的管理中心或主站点。 一个 Intune 租户只能连接到一个 Configuration Manager 层次结构且一个 Configuration Manager 层次结构只能连接到一个 Intune 租户。  

 在混合 MDM 配置中，一些处理操作和存储开销通过 Configuration Manager 本地基础结构来执行。 此效率方面的提升使混合 MDM 在扩展方面优于 Intune 独立版。  

 在混合部署中，Configuration Manager 管理员可以使用自己熟悉的工具。 如果实施混合 MDM，移动设备便可使用一些高级功能，如基于角色的管理控制 (RBAC)、SQL Server Reporting Services (SSRS)、通过集合成员身份查询完成的复杂设备和用户分组。  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>规划选择和 Intune 部署时间表  
 Intune 的创新和发展速度很快，会每月发布更新，提供新增或增强的功能、增强的规模、通过 Azure 门户实现的新的管理控制台经验以及通过 Azure Active Directory 实现的动态组等。 鉴于此，任何设计决策应考虑到该产品的未来发展方向。  

 随着 Intune 独立服务的短期、中期和长期发展，该服务也将逐渐推出混合配置当前所提供的许多独特功能。  

 如果正在独立服务和混合部署二者之间做抉择，应考虑部署时间表。 在部署到生产之前，客户一般会经历多次部署迭代，包括设计、构建、用户验收测试和试验阶段，这通常需要花费数月时间。 鉴于此，选择 Intune 层次结构设计时，要考虑实际的部署时间，还要考虑服务的短期、中期和长期方向。  

 随着 Intune 服务不断发展，我们的目标是简化配置选择。 将来，只有需通过单一管理控制台同时管理传统客户端和移动设备的客户需要选择混合 MDM 环境。  我们正在努力提升可伸缩性，通过 Azure 门户添加基于角色的访问和通过深化 Azure Active Directory 集成实现动态组，这些些都是我们在短期和中期更新中希望完成的目标。  

 最后，我们也会努力确保不管用户当前做出何种配置选择，都能够在混合和独立配置之间轻松顺畅地切换。 目前，切换 MDM 机构需要 Microsoft 技术支持人员提供手动干预，同时需要租户执行大量工作。 为简化此操作，我们正在朝着混合部署和 Intune 独立部署并存的目标努力，如果实现此目标，将能够在两种类型的管理之间转移用户，而无需在选择一种配置后放弃另外一种。  而且，将无需再致电寻求支持，也无需再注销和重新注册设备。  

##  <a name="pros-and-cons-of-intune-standalone"></a>Intune 独立版的利弊  

|利|弊|  
|----------|----------|  
|快速构建和部署<br /><br /> 无需本地基础结构<br /><br /> 更为频繁的更新和功能发布<br /><br /> 低学习曲线<br /><br /> 可从外部使用管理员控制台|报表功能有限<br /><br /> 安全角色限制有限<br /><br /> 无外部工具（如 PowerShell 等）<br /><br /> 应用清单有限<br /><br /> 基本的用户和设备分组功能<br /><br /> 需要 Silverlight|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>混合 MDM 的利弊  

|利|弊|  
|----------|----------|  
|可扩展<br /><br /> 高级工具（如 Configuration Manager 控制台、PowerShell 和日志记录等）<br /><br /> 基于角色的访问控制 (RBAC)<br /><br /> 高级报表<br /><br /> “单一管理平台”同时管理 MDM 和传统客户端<br /><br /> 扩展的应用清单<br /><br /> 高级的用户和设备分组<br /><br /> 支持多个本地 Exchange 和 Exchange Online 连接器<br /><br /> 支持多个 NDES/CRP 角色<br /><br /> 能够将设备标记为“公司所有”<br /><br /> 更强的故障排除能力<br /><br /> 订阅中包括 Configuration Manager 用户 CAL|本地复杂性（配置和管理）<br /><br /> 陡峭的学习曲线<br /><br /> 需维护发布的更新和功能<br /><br /> 其他许可要求（例如 Windows、SQL Server 等）|  

##  <a name="planning-decisions"></a>规划决策  
 ![混合决策](../../mdm/understand/media/hybrid-decisions.png)  

|步骤|决策|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**计划管理多少台设备？**<br /><br /> Intune 独立版最多可支持 50000 个设备。 混合 MDM 最多可支持 300000 个设备。<br /><br /> 对于大规模的部署（独立版或混合 MDM），建议联系 Microsoft 帐户团队。 Microsoft 帐户团队可帮助联系 Intune 专家，专家会就规模和限制提供进一步建议。|  
|![混合 2](../../mdm/understand/media/hybrid-2.png)|**是否需要精细访问控制？(RBAC)**<br /><br /> 已向 System Center 2012 Configuration Manager 添加基于角色的访问控制 (RBAC)。 RBAC 允许 Configuration Manager 管理员设计和部署复杂的权限集，限制管理员只能访问 Configuration Manager 对象和函数。<br /><br /> Intune 独立版只提供两种管理员角色：完全访问权限和只读访问权限。<br /><br /> 如果组织需让特定管理员管理特定用户、设备、函数或对象，那么需要使用配置有 RBAC 的 Configuration Manager。<br /><br /> 如果组织具有一个小型管理团队，且无需复杂的精细访问控制，那么具有内置安全角色的 Intune 是最佳选择。|  
|![混合 3](../../mdm/understand/media/hybrid-3.png)|**是否需要高级报表功能？**<br /><br /> 通过 Configuration Manager 实现的混合 MDM 包含使用 SQL Server Reporting Services (SSRS) 的高级报表功能。 Configuration Manager 附带 34 个内置 MDM 报表和 400 多个标准 Configuration Manager 报表。 借助 SSRS，管理员和业务分析人员还能够撰写自己的自定义报表。 此外，业务流程工具等外部工具可查询 Configuration Manager 数据库以提供自定义警报等特定功能。 如果是 Configuration Manager 运行的报表，所有报表还可包含非 MDM 数据，例如可并行显示移动设备清单和传统 PC 清单。<br /><br /> Intune 独立版提供 9 个报表。 这些报表不可自定义，且提供的输入变量有限。 报表可打印或导出为 CSV 或 HTML 格式。<br /><br /> 如果组织需要高级报表功能，并且具备用于管理 SSRS 的带宽和知识，则混合 MDM 是最佳选择。<br /><br /> 如果组织需要易于使用的报表引擎和预定义的报表，则 Intune 独立版的报表功能足以满足需求。|  
|![混合 4](../../mdm/understand/media/hybrid-4.png)|**是否要在无 Internet 访问的情况下管理 Windows 10 设备？**<br /><br /> 在 Configuration Manager (Current Branch) 中，只需使用本地基础结构通过 MDM 渠道便可管理 Windows 10 设备。<br /><br /> 本地移动设备管理功能旨在实现针对无 Internet 连接的客户端的 MDM 管理，主要面向单一用途设备（如网亭设备）和 IoT 设备。<br /><br /> 由于 Intune 独立版只涉及云，所以管理的所有设备必须具有 Internet 访问权限。 如果组织希望通过本地移动设备管理来管理 Windows 10 设备，则需要采用混合 MDM 配置。 请注意，本地移动设备管理不支持同时管理 Internet 和 intranet 移动设备。|  
|![混合 5](../../mdm/understand/media/hybrid-5.png)|**是否需要完整应用清单？**<br /><br /> 默认情况下，Intune 独立版仅收集由 Intune 管理和部署的应用的应用清单。 即清单报表不包含用户通过非 Intune 公司门户渠道安装的旁加载应用的信息。<br /><br /> 通过 Configuration Manager 实现的混合 MDM 允许管理员将某些设备指定为“公司所有”。 当设备设置为公司所有的设备后，系统会收集扩展应用清单，由此提供对设备完整应用列表的访问权限。<br /><br /> 如果组织需要个人通过托管设备安装的应用的相关信息，则需要混合 MDM。 在基于此选择做出决策之前，请考虑对最终用户的隐私可能造成的影响。|  
|![混合 6](../../mdm/understand/media/hybrid-6.png)|**是否希望采用传统的“胖客户端”方式管理 PC？**<br /><br /> 混合 MDM 相较于独立配置的一个优点是“单一管理平台”管理。 这意味着，组织可通过 Configuration Manager 控制台这一个管理工具来管理全部的台式计算机、服务器和移动设备。 此外，通过 Configuration Manager 客户端，非移动设备可实现许多高级管理功能，如硬件和软件清单、软件更新管理、软件部署和操作系统部署。<br /><br /> 如果组织需要管理传统的 Windows、Linux/UNIX 和 Mac 客户端，Configuration Manager 是首选管理平台。<br /><br /> Intune 独立版也提供传统 PC 管理（Windows 7、8.1 和 10），这是通过 Intune PC 管理客户端来实现的。 它提供基本的 PC 管理，包括硬件清单、Windows 更新、Endpoint Protection 和简单的软件部署。 客户端不与 Configuration Manager 协同工作，所以可同时用于 Intune 独立版部署和混合 MDM 部署。|  
|![混合 7](../../mdm/understand/media/hybrid-7.png)|**是否需要管理本地基础结构？**<br /><br /> 本地基础结构需要一定的管理开销，并具有一定的复杂性。 管理和维护 Configuration Manager 的基础结构需要具备大量的知识、丰富的经验，并需要较大的投资。<br /><br /> 混合 MDM 需要至少一个单一 Configuration Manager 主站点，需配有数据库角色、报表服务角色和服务连接点角色。 如果需要传统的 PC 管理，则还可能需要配置管理点、分发点、软件更新点和应用程序目录角色。 高级功能，如证书部署、Mac 管理和 Endpoint Protection 会添加更多角色，同时也会增加复杂性。<br /><br /> Configuration Manager 层次结构需要大量的管理和维护，以确保正常运行和发挥功能。<br /><br /> 如果不想支出 Configuration Manager 层次结构的开销，则 Intune 独立部署是最佳选择。|  
|![混合 8](../../mdm/understand/media/hybrid-8.png)|**是否需要外部工具？**<br /><br /> Configuration Manager 是一种成熟的企业级产品，无需使用控制台便可通过多种方式与服务交互。 混合 MDM 部署允许管理员使用 Configuration Manager SDK 或 PowerShell 以编程方式管理移动设备。 还允许管理员使用多种工具，如 System Center Orchestrator、PowerBI 和各种第三方加载项。<br /><br /> 在 Intune 独立部署中，必须通过 Silverlight 控制台执行所有管理，且不能使用外部工具。|  
|![混合 9](../../mdm/understand/media/hybrid-9.png)|**是否需要快速的 MDM 功能更新？**<br /><br /> 尽管 Configuration Manager (Current Branch) 能够高效提供更新和功能，但 Intune 等云服务的发展可实现更快的生产部署。<br /><br /> Intune 独立版可能会先于混合 MDM 部署实现新功能。<br /><br /> 如果组织想保持领先，则 Intune 独立版会是一个好的选择，因为它会以最快的方式提供最新的 MDM 功能。|



<!--HONumber=Nov16_HO1-->


