---
title: "简介 | Microsoft Docs"
description: "获取基本信息，作为对 System Center Configuration Manager 的简介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76f907b17df0dd2f102e34ca3cfb3ffc813c0004
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-system-center-configuration-manager"></a>System Center Configuration Manager 简介

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 作为 Microsoft System Center 管理解决方案套件中的一种产品，有助于在本地和云中管理设备和用户。  

**使用 Configuration Manager 有助于：**   
-   减少手动任务并让你专注处理高价值项目，从而提高 IT 工作效率和效率。  
-   最大程度实现硬件和软件投资。  
-   在适当时间提供正确的软件，从而提高用户的工作效率。  

**Configuration Manager 可实现以下各项，帮助提供更有效的 IT 服务：**  

-   安全和可伸缩的软件部署。  
-   符合性设置管理。  
-   服务器、台式计算机、笔记本电脑和移动设备的全面资产管理。  

**Configuration Manager 扩展现有的 Microsoft 技术和解决方案并与之协同工作。**  

例如，Configuration Manager 可与以下各项集成：  

-   Microsoft Intune，管理各种移动设备平台。  
-   Windows Server 更新服务 (WSUS)，管理软件更新。  
-   证书服务。  
-   Exchange Server 和 Exchange Online。  
-   Windows 组策略。
-   DNS。   
-   Windows 自动部署工具包 (Windows ADK) 和用户状态迁移工具 (USMT)。  
-   Windows 部署服务 (WDS)。  
-   远程桌面和远程协助。  

Configuration Manager 也可使用：  

-   Active Directory 域服务来获得安全性、服务定位和配置，并使用它来发现要管理的用户和设备。  
-   Microsoft SQL Server 作为分布式变更管理数据库，并与 SQL Server Reporting Services (SSRS) 集成以生成报表来监视和跟踪管理活动。  
-   站点系统角色，可扩展管理功能并使用 Internet Information Services (IIS) 的 Web 服务。
-   后台智能传输服务 (BITS) 和 BranchCache 来帮助管理可用的网络带宽。  

若要成功使用 Configuration Manager，必须首先全面规划和测试管理功能，之后才在生产环境中使用 Configuration Manager。 Configuration Manager 是一款功能强大的管理应用程序，可能会潜在地影响组织中的每台计算机。 如果在部署和管理 Configuration Manager 时经过了仔细规划并考虑了业务要求，Configuration Manager 可降低管理开销和总拥有成本。  

请参阅以下主题以及本主题中的其他部分来详细了解 Configuration Manager。  


**本文档库中的相关主题：**  

-   [System Center Configuration Manager 的特性和功能](../../core/plan-design/changes/features-and-capabilities.md)  
-   [为 System Center Configuration Manager 选择设备管理解决方案](../../core/plan-design/choose-a-device-management-solution.md)  
-   [自 System Center 2012 Configuration Manager 以来 System Center Configuration Manager 中更改的内容](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [System Center Configuration Manager 基础知识](../../core/understand/fundamentals.md)  
-   [通过构建自己的实验室环境来评估 System Center Configuration Manager](/sccm/core/get-started/set-up-your-lab)
-   [查找使用 System Center Configuration Manager 的帮助](../../core/understand/find-help.md)  
-   [System Center Configuration Manager 中已删除和已弃用的功能](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="BKMK_Console"></a> Configuration Manager 控制台  
 安装 Configuration Manager 后，使用 Configuration Manager 控制台来配置站点和客户端，以及运行和监视管理任务。 此控制台是主要管理位置，并允许你管理多个站点。  

 你可以使用控制台来运行对特定客户端管理任务提供支持的辅助控制台，如：  

-   **资源浏览器**，用于查看硬件和软件清单信息。  
-   **远程控制**，用于远程连接到客户端计算机以执行故障排除任务。  

可在其他计算机上安装 Configuration Manager 控制台，并且通过使用基于 Configuration Manager 角色的管理，限制访问并限制管理用户可以在控制台中看到的内容。  

有关详细信息，请参阅[安装 System Center Configuration Manager 控制台](../../core/servers/deploy/install/install-consoles.md)。

##  <a name="BKMK_ApplicationCatalog"></a> 应用程序目录、软件中心和公司门户  
 **应用程序目录** 是一个网站，用户可在其中浏览并请求适用于基于 Windows 的电脑的软件。 要使用应用程序目录，你必须为站点安装应用程序目录 Web 服务点和应用程序目录网站点。  

 **软件中心**是在基于 Windows 的计算机上安装 Configuration Manager 客户端时所安装的一个应用程序。 用户运行此应用程序来请求软件，并管理 Configuration Manager 为其部署的软件。 软件中心使用户能够执行下列操作：  

-   从应用程序目录中浏览和安装软件。  
-   查看其软件请求历史记录。  
-   配置 Configuration Manager 在设备上安装软件的时间。  
-   配置远程控制的访问权限设置（如果管理用户启用了远程控制）。  

**公司门户**是一个应用或网站，提供与应用程序目录类似的功能，但适用于通过 Microsoft Intune 注册的移动设备。  

有关详细信息，请参阅 [System Center Configuration Manager 中的应用程序管理入门](../../apps/understand/introduction-to-application-management.md)。  

###  <a name="BKMK_Client"></a> Configuration Manager 属性（在 Windows 电脑上）  
 在 Windows 计算机上安装 Configuration Manager 客户端时，将在控制面板中安装 Configuration Manager。 通常，不必配置此应用程序，因为客户端配置是在 Configuration Manager 控制台中执行的。 此应用程序可帮助管理用户和技术支持排除个别客户端的问题。  

 有关客户端部署的详细信息，请参阅 [System Center Configuration Manager 中的客户端安装方法](../../core/clients/deploy/plan/client-installation-methods.md)。  

##  <a name="BKMK_ExampleScenarios"></a> Configuration Manager 的示例方案  
 以下示例方案演示名为 Trey Research 的公司如何使用 System Center Configuration Manager 来使用户：  

-   工作效率更高。  
-   统一设备的符合性管理以获得更流畅的管理体验。
-   简化设备管理以降低 IT 运营成本。  

在所有方案中，Adam 是 Configuration Manager 的主要管理员。  

###  <a name="BKMK_ScenarioEmpower"></a>示例方案：通过确保从任何设备访问应用程序来提高用户的工作效率  
 Trey Research 希望确保员工能够尽可能高效地访问所需的应用程序。 Adam 将这些公司要求映射到以下方案：  

|要求|当前客户端管理状态|将来的客户端管理状态|  
|-----------------|-------------------------------------|------------------------------------|  
|新员工从第一天起就能高效工作。|员工加入公司时，必须在第一次登录后等待安装应用程序。|员工加入公司时，在登录后应用程序已安装就绪，可供使用。|  
|员工可快速轻松地请求其他所需的软件。|员工需要其他应用程序时，向技术支持提交票证。 然后通常需要两天时间，等待票证得到处理并安装应用程序。|员工需要其他应用程序时，可从网站中请求这些应用程序。 如果没有许可限制，则会立即安装应用程序。 如果有许可限制，则用户必须首先请求批准，然后才能安装应用程序。<br /><br /> 网站仅向用户显示允许他们安装的应用程序。|  
|如果员工的移动设备符合所监视和实施的安全策略，则员工可以在工作中使用这些设备。<br /><br /> 这些策略包括强制实施强密码、处于非活动状态一段时间后锁定设备，以及远程擦除丢失或被盗设备。|员工将其移动设备连接到 Exchange Server 来获得电子邮件服务。 但很少有报告来确认这些设备符合默认 Exchange ActiveSync 邮箱策略中的安全策略。 除非 IT 确认符合策略，否则个人使用移动设备存在会被禁止的风险。|IT 组织可报告移动设备与必需设置的安全符合性。 这种确认使用户能够继续在工作中使用其移动设备。 用户可在其移动设备丢失或被盗时远程擦除移动设备，并且支持人员可擦除报告为丢失或被盗的任何用户的移动设备。<br /><br /> 在 PKI 环境提供移动设备注册以实现额外的安全性和控制。|  
|员工即使不在办公桌前也可高效工作。|员工不在办公桌前并且没有便携计算机时，无法使用公司范围内可用的网亭计算机来访问其应用程序。|员工可使用网亭计算机来访问其应用程序和数据。|  
|通常，业务连续性优先于安装所需的应用程序和软件更新。|在白天安装所需的应用程序和软件更新，并频繁打断用户的工作，因为用户的计算机在安装期间速度会慢，或者会重启。|用户可配置其工作时间以防止在用户使用计算机时安装所需的软件。|  

 为了满足要求，Adam 使用以下 Configuration Manager 管理功能和配置选项：  

-   应用程序管理  
-   移动设备管理  

他通过使用下表中的配置步骤来实施这些项目：  

|配置步骤|结果|  
|-------------------------|-------------|  
|Adam 确保新用户具有 Active Directory 用户帐户，并在 Configuration Manager 中为这些用户创建基于查询的新集合。 然后，他通过创建将用户帐户映射到这些用户将使用的主计算机的文件，为他们定义用户设备相关性，然后将此文件导入 Configuration Manager。<br /><br /> 已在 Configuration Manager 中创建新用户必须具有的应用程序。 然后，他将目的为“必需”的应用程序部署到包含新用户的集合。|由于存在用户设备相关性信息，因此在用户登录前，应用程序会安装在每个用户的一台或多台主计算机上。<br /><br /> 用户成功登录后，应用程序立即可供使用。|  
|Adam 安装和配置应用程序目录站点系统角色，以便用户可以浏览要安装的应用程序。 他创建目的为“可用”的应用程序部署，然后将这些应用程序部署到包含新用户的集合。<br /><br /> 对于许可证数量受限的应用程序，Adam 将这些应用程序配置为要求批准。|用户现在可以使用应用程序目录浏览允许他们安装的应用程序。 然后，用户可以立即安装应用程序，或者请求批准并返回应用程序目录，以在技术支持批准其请求后安装这些应用程序。|  
|Adam 在 Configuration Manager 中创建 Exchange Server 连接器，以管理连接至公司的本地 Exchange Server 的移动设备。 他使用安全设置来配置此连接器，这些安全设置包括要求强密码以及在一段不活动期后锁定移动设备。<br /><br /> 为了对运行 Windows Phone 8、Windows RT 以及 iOS 的设备进行额外的管理，Adam 获取了 Microsoft Intune 订阅。 然后安装了服务连接点站点系统角色。 对于这些设备，该移动设备管理解决方案为公司提供了更大的管理支持。 这包括使应用程序可供用户安装在这些设备上以及广泛的设置管理。 此外，通过使用由 Intune 自动创建和部署的 PKI 证书，确保移动设备连接安全。<br /><br /> 通过配置服务连接点和订阅使用 Configuration Manager 后，Adam 给拥有这些移动设备的用户发送了一封电子邮件，请他们单击链接以开始注册流程。<br /><br /> 对于通过 Microsoft Intune 注册的移动设备，Adam 使用符合性设置来配置这些移动设备的安全设置。 这些设置包括要求设置强密码以及在一段不活动期后锁定移动设备。|借助这两个移动设备管理解决方案，IT 组织现在可以提供关于正在公司网络上使用的移动设备的报表信息，以及它们与配置的安全设置的符合性。<br /><br /> 用户会获得演示，了解在其移动设备丢失或被盗时如何使用应用程序目录或公司门户远程擦除移动设备。 支持人员还会获得指引，了解如何通过使用 Configuration Manager 控制台为用户远程擦除移动设备。<br /><br /> 此外，对于通过 Microsoft Intune 注册的移动设备，Adam 现在可以为用户部署要安装的移动应用程序、收集这些设备的更多清单数据以及凭借能够访问更多的设置而对这些设备进行更好的管理控制。|  
|Trey Research 拥有一些供办事处的来访员工使用的网亭计算机。 员工希望无论自己在何处登录，都可以使用其应用程序。 但是，Adam 不希望在每台计算机上均以本地方式安装所有应用程序。<br /><br /> 为此，Adam 创建了具有两种部署类型的必需的应用程序：<br /><br /> **第一种：**应用程序的本地完全安装，这类应用程序必须仅安装在用户的主要设备上。<br /><br /> **第二种：**应用程序的虚拟版本，这类应用程序不得安装在用户的主要设备上。|来访员工登录网亭计算机时，会在网亭计算机的桌面上见到以图标形式显示的他们所必需的应用程序。 运行应用程序时，它会以虚拟应用程序的形式进行流式处理。 因此，他们可以与坐在自己的台式机前工作一样高效。|  
|Adam 使用户了解到他们可以在软件中心配置自己的工作时间，并可选择选项以防在此期间以及计算机处于演示模式下时进行软件部署活动。|由于用户可以控制 Configuration Manager 将软件部署到其计算机上的时间，因此用户在其工作日中能始终更为高效。|  

 通过确保从任何设备均可访问应用程序，这些配置步骤和结果使 Trey Research 成功使其员工具有更高的生产力。  

###  <a name="BKMK_ScenarioUnify"></a> 示例方案：统一设备的符合性管理  
 Trey Research 希望获得统一的客户端管理解决方案，该方案确保其计算机运行自动保持更新的防病毒软件。 即：  

-   Windows 防火墙已启用。  
-   已安装关键软件更新。  
-   已设置特定的注册表项。  
-   托管的移动设备无法安装或运行未签名的应用程序。  

该公司还希望将此保护扩展到 Internet，以保护从 Intranet 移至 Internet 的便携式计算机。  

Adam 将这些公司要求映射到以下方案：  

|要求|当前客户端管理状态|将来的客户端管理状态|  
|-----------------|-------------------------------------|------------------------------------|  
|在所有计算机上运行具有最新定义文件的防恶意软件并启用 Windows 防火墙。|不同计算机运行不同的反恶意软件解决方案，这些解决方案并非始终保持最新。 尽管在默认情况下已启用 Windows 防火墙，但用户有时会将其禁用。<br /><br /> 如果在用户计算机上检测到恶意软件，则将要求他们与技术支持联系。|在所有计算机上运行相同的防恶意软件解决方案，该解决方案会自动下载最新的定义更新文件，并在用户将 Windows 防火墙禁用时自动将其重新启用。<br /><br /> 如果检测到恶意软件，则将自动通过电子邮件通知技术支持。|  
|在关键软件更新发布的首个月内，在所有计算机上安装这些关键的软件更新。|尽管在计算机上已安装软件更新，但许多计算机不会自动安装关键软件更新，而会直到关键软件更新已发布两个月或三个月后才安装。 这将使这些计算机在此期间内容易受到攻击。<br /><br /> 对于未安装关键软件更新的计算机，技术支持首先会发出要求用户安装更新的电子邮件。 对于仍然不符合规定的计算机，工程师会远程连接到这些计算机并手动安装缺失的软件更新。|在指定月份将当前符合率提升到 95% 以上，而不用发出电子邮件或要求技术支持手动安装这些更新。|  
|定期检查特定应用程序的安全设置并在必要时进行修正。|计算机运行依赖于计算机的组成员身份的复杂启动脚本，以重置特定应用程序的注册表值。<br /><br /> 由于这些脚本仅在启动时运行并且有些计算机会持续数日保持开启状态，因此技术支持无法及时检查是否存在配置漂移。|注册表值会接受检查并自动修正，而不依赖计算机组成员身份或重启计算机。|  
|移动设备无法安装或运行不安全的应用程序。|要求用户不通过 Internet 下载和运行可能不安全的应用程序。 但是没有落实用于监视或强制实施该要求的控制措施。|使用 Microsoft Intune 或 Configuration Manager 管理的移动设备会自动防止安装或运行未签名的应用程序。|  
|必须保持从 Intranet 移至 Internet 的便携式计算机的安全。|对于外出的用户，他们常常无法每天都通过 VPN 连接进行连接。 这会导致这些笔记本电脑不符合安全要求。|Internet 连接会是便携式计算机保持符合安全要求的全部要求。 用户不必登录或使用 VPN 连接。|  

 为了满足要求，Adam 使用以下 Configuration Manager 管理功能和配置选项：  

-   Endpoint Protection  
-   软件更新  
-   符合性设置  
-   移动设备管理  
-   基于 Internet 的客户端管理  

他通过使用下表中的配置步骤来实施这些项目：  

|配置步骤|结果|  
|-------------------------|-------------|  
|Adam 配置 Endpoint Protection。 启用客户端设置以卸载其他反恶意软件解决方案，并启用 Windows 防火墙。 他配置自动部署规则，以便计算机定期检查和安装最新的定义更新。|单一的防恶意软件解决方案有助于以最小的管理开销保护所有的计算机。 由于检测到反恶意软件时会自动通过电子邮件通知技术支持，因此可以快速解决问题。 这有助于防止其他计算机遭受攻击。|  
|为了便于提升符合率，Adam 运用自动部署规则，定义服务器的维护时段，并且调查为休眠的计算机使用 LAN 唤醒的优点和缺点。|关键软件更新的符合性提高，而用户或技术支持手动安装软件更新的要求降低。|  
|Adam 使用符合性设置来检查是否存在指定的应用程序。 检测到应用程序后，配置项目随即会检查注册表值并在注册表值不符时自动对其进行修正。|通过使用部署到所有计算机并且每日均会执行符合性检查的配置项目和配置基线，不再需要依赖计算机成员身份和计算机重启的单独脚本。|  
|Adam 为已注册的移动设备使用符合性设置并配置 Exchange Server 连接器，从而禁止在移动设备上安装和运行未签名的应用程序。|由于禁止未签名的应用程序，移动设备会自动防范可能有害的应用程序。|  
|Adam 确保站点系统服务器和计算机均具有 Configuration Manager 针对 HTTPS 连接而要求的 PKI 证书。 然后安装外围网络中的附加站点系统角色，这些角色接受来自 Internet 的客户端连接。|Configuration Manager 将继续自动管理从 Intranet 移至 Internet 的计算机（当这些计算机具有 Internet 连接时）。 这些计算机并不依赖用户登录他们的计算机或连接至 VPN。<br /><br /> 这些计算机会继续在防恶意软件和 Windows 防火墙、软件更新以及配置项目方面得到管理。 结果，符合性级别将自动提升。|  

 这些配置步骤和结果导致 Trey Research 公司成功统一了设备的符合性管理。  

###  <a name="BKMK_ScenarioSimplify"></a> 示例方案：简化设备的客户端管理  
 Trey Research 希望所有新计算机均能自动安装他们公司的运行 Windows 7 的基本计算机映像。 在这些计算机上安装操作系统映像后，必须就用户安装的附加软件对计算机进行管理和监视。 如果计算机上存储着高度机密的信息，则必须对该类计算机实施比其他计算机具有更多限制的管理策略。 例如，技术支持工程师不得远程连接到这类计算机，必须使用 BitLocker PIN 条目才能重启，并且仅限本地管理员才能安装软件。  

 Adam 将这些公司要求映射到以下方案：  

|要求|当前客户端管理状态|将来的客户端管理状态|  
|-----------------|-------------------------------------|------------------------------------|  
|新计算机已安装 Windows 7。|技术支持为用户安装和配置了 Windows 7，然后将计算机发往用户各自的位置。|新计算机会直接发往最终目的地，接入网络，并自动安装和配置 Windows 7。|  
|必须管理和监视计算机。 这包括收集有助于确定许可要求的硬件和软件清单数据。|通过使用自动客户端请求安装来部署 Configuration Manager 客户端。 技术支持将调查安装故障以及未在预期时间发送清单数据的客户端。<br /><br /> 故障频发，因为未满足安装依赖性以及客户端上的 WMI 损坏。|从计算机中收集的客户端安装和清单数据更为可靠，仅需较少的技术支持干预。 报表将针对许可证信息展示软件的使用情况。|  
|有些计算机必须具有更为严格的管理策略。|由于存在更为严格的管理策略，因此目前不通过 Configuration Manager 来管理这些计算机。|通过使用 Configuration Manager 来管理这些计算机以应对异常情况，无需额外的管理开销。|  

 为了满足要求，Adam 使用以下 Configuration Manager 管理功能和配置选项：  

-   操作系统部署  
-   客户端部署和客户端状态  
-   符合性设置  
-   客户端设置  
-   清单方法和资产智能  
-   基于角色的管理  

他通过使用下表中的配置步骤来实施这些项目：  

|配置步骤|结果|  
|-------------------------|-------------|  
|Adam 从装有 Windows 7 并按公司规范配置的计算机中捕获操作系统映像。 然后，通过使用未知的计算机支持和 PXE，他将操作系统部署到新的计算机。 他还将 Configuration Manager 客户端作为操作系统部署的一部分进行安装。|无需技术支持工程师的干预，新的计算机能够更快速地启动并正常运行。|  
|Adam 配置自动站点范围的客户端请求安装，在所发现的任何计算机上安装 Configuration Manager 客户端。 这确保未利用客户端映像化的任何计算机仍然安装客户端，使计算机受 Configuration Manager 管理。<br /><br /> Adam 配置客户端状态，以自动修正所发现的任何客户端问题。 他还配置客户端设置以启用对所需清单数据的收集，以及配置资产智能。|与等待 Configuration Manager 发现计算机，然后尝试在计算机上安装客户端源文件相比，将客户端与操作系统一起安装更为快速和可靠。 但是，通过启用自动客户端请求选项，为已安装操作系统的计算机提供备用方法，以在计算机连接到网络时安装客户端。<br /><br /> 客户端设置确保客户端定期向站点发送其清单信息。 除了客户端状态测试之外，这有助于在最大程度减少技术支持干预的情况下让客户端保持运行。 例如，会检测并自动修正 WMI 损坏。<br /><br /> 资产智能报表帮助监视软件的使用情况和许可证。|  
|Adam 为必须具有更严格策略设置的计算机创建集合。 然后为此集合创建自定义客户端设备设置，包括禁用远程控制、启用 BitLocker PIN 输入和仅允许本地管理员安装软件。<br /><br /> Adam 配置基于角色的管理，这样一来，技术支持工程师无法查看此计算机集合。 这有助于确保不会意外地将这些计算机作为标准计算机进行管理。|这些计算机现在由 Configuration Manager 管理，但具有无需新站点的特定设置。<br /><br /> 技术支持工程师无法查看这些计算机的集合。 这有助于降低向这些计算机发送适用于标准计算机的部署和脚本的可能性。|  

 这些配置步骤和结果导致 Trey Research 成功简化了设备的客户端管理。  

##  <a name="BKMK_NextSteps"></a> 后续步骤  
 在安装 Configuration Manager 之前，可以熟悉特定于 Configuration Manager 的一些基本概念和术语。  

-   如果已熟悉 System Center 2012 Configuration Manager，请参阅[自 System Center 2012 Configuration Manager 以来 System Center Configuration Manager 中更改的内容](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)了解新功能。  
-   有关 System Center Configuration Manager 的高级技术概述，请参阅 [System Center Configuration Manager 基础知识](../../core/understand/fundamentals.md)。  

熟悉了基本概念后，使用 System Center Configuration Manager 文档帮助成功部署和使用 Configuration Manager。  
