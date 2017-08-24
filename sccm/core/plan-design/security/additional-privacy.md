---
title: "System Center Configuration Manager 隐私声明 - 其他信息 | Microsoft Docs"
description: "了解 Microsoft 如何收集和使用来自 System Center Configuration Manager 部署的数据。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: ef7b3656f9b4a31e07227aa4e864448d0dd1fcdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>关于 System Center Configuration Manager 隐私的其他信息

*适用范围：System Center Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>更新和服务
System Center Configuration Manager 引入了新更新模型，有助于你将当前的 Configuration Manager 部署保持为最新更新和功能。 安装后，此功能将在管理员选择的站点服务器上添加称作服务连接点的新站点系统角色。 有关收集的信息内容及其使用方式详情，请参阅本文中的“使用情况数据”部分。


## <a name="usage-data"></a>使用情况数据
System Center Configuration Manager 收集有关自身的诊断和使用情况数据，Microsoft 使用这些数据改进将来版本的安装体验、质量和安全性。
诊断和使用情况数据可用于每个 System Center Configuration Manager 层次结构。 它包含在每个主站点和管理中心站点每周运行一次的 SQL Server 查询。 层次结构使用管理中心站点时，主站点中的数据随后会复制到该站点。 在层次机构的顶层站点上，服务连接点在检查更新时提交此信息。 如果服务连接点处于脱机模式下，则将使用服务连接工具传输信息。

Configuration Manager 仅从站点 SQL Server 数据库收集数据，而不会直接从客户端或站点服务器收集数据。

管理员可以通过转到 Configuration Manager 控制台的“使用情况数据”部分更改收集数据的级别。

有关详细信息，请参阅[System Center Configuration Manager 的诊断和使用情况数据](http://go.microsoft.com/fwlink/?LinkID=626566)文章中有关使用情况数据级别和设置的“了解详情”一文。


## <a name="customer-experience-improvement-program"></a>客户体验改善计划
客户体验改善计划 (CEIP) 从 Configuration Manager 管理控制台中收集有关你的硬件配置以及你使用软件和服务的方式的基本信息，以便确定趋势和使用模式。 CEIP 还收集你遇到的错误的类型和编号、软件和硬件性能以及服务的速度。 我们不会收集你的姓名、地址或其他联系信息。 不从客户端计算机中收集任何 CEIP 数据。

我们使用此信息来提高 Microsoft 软件和服务的质量、可靠性和性能。

有关 CEIP 收集、处理或传输的信息的详情，请参阅 [CEIP 隐私声明](http://go.microsoft.com/fwlink/?LinkID=525211)。

## <a name="operations-management-suite-connector"></a>Operations Management Suite 连接器
Microsoft Operations Management Suite 连接器可将数据（如集合）从 System Center Configuration Manager 同步到 Microsoft Operations Management Suite。 管理员配置此功能后，Microsoft Azure 订阅 ID 和密钥会存储在 Configuration Manager 数据库中。 Azure Active Directory 客户端密钥和 Microsoft Operations Management Suite 工作区共享的密钥均存储在本地 System Center Configuration Manager 数据库中。 System Center Configuration Manager 和 Microsoft Operations Management Suite 之间的所有通信都使用 HTTPS。 除随机化遥测数据之外，不会向 Microsoft 提供有关集合的任何其他信息。 有关 Microsoft Operations Management Suite 收集的信息的详细信息，请参阅 [Log Analytics 数据安全](http://go.microsoft.com/fwlink/?LinkId=823545)。

## <a name="asset-intelligence"></a>资产智能
资产智能使 IT 管理员能够定义、跟踪和主动管理与配置标准的符合性。 对部署以及物理和虚拟应用程序的使用进行计量和报告可帮助组织做出更明智的软件许可业务决策，并保持与许可协议的相容性。 从 Configuration Manager 客户端收集使用数据之后，管理员可以使用不同的功能来查看数据，包括集合、查询和报告。

在每次同步过程中，将从 Microsoft 下载已知软件的目录。 IT 管理员可以选择向 Microsoft 发送以下相关信息：在其组织中发现的要进行研究以及添加到目录中的未分类软件标题。 在上传此信息之前，对话框会显示要上传的数据。 无法取消上载的数据。 资产智能不会向 Microsoft 发送关于用户和计算机或许可证使用的信息。

上载软件标题后，Microsoft 研究员会对此资料进行标识和分类，然后向使用此功能的所有其他客户以及目录的其他消费者提供该资料。 任何已上传的软件标题都将公开。 应用程序及其分类会成为目录的一部分，然后可供目录的其他用户下载。 在配置资产智能数据收集以及确定是否将信息提交给 Microsoft 之前，请考虑组织的隐私要求。

System Center Configuration Manager 中的资产智能默认不启用。 上载未分类的标题决不会自动发生，系统并不打算自动进行此任务。 你必须手动选择并批准上载每个软件标题。

## <a name="endpoint-protection"></a>Endpoint Protection
Microsoft Cloud Protection Service，以前称作 Microsoft Active Protection Service 或 MAPS。
适用的产品：System Center Configuration Manager 的 System Center Endpoint Protection 和 Endpoint Protection 功能（用于管理 System Center Endpoint Protection 和 Windows Defender for Windows 10）。 用于 Linux 的 System Center Endpoint Protection 和用于 Mac 的 System Center Endpoint Protection 还未实现此功能。

Microsoft Cloud Protection Service 反恶意软件社区是一个包括 System Center Endpoint Protection 用户的自愿性全球在线社区。 加入 Microsoft Cloud Protection Service 时，System Center Endpoint Protection 会自动向 Microsoft 发送信息。 Microsoft 使用信息来确定调查潜在威胁的软件，并帮助提高 System Center Endpoint Protection 的效率。 此社区帮助阻止新的恶意软件感染的传播。 如果 Microsoft Cloud Protection Service 报告中包括有关恶意软件或 Endpoint Protection 客户端可删除的有害软件的详细信息，Microsoft Cloud Protection Service 将下载最新的签名来解决此问题。 Microsoft Cloud Protection Service 还可发现“误报”（即最初被确定为恶意软件，但结果并非如此）并解决这些误报问题。

Microsoft Cloud Protection Service 报告中包含有关可疑恶意软件的信息，例如文件名、加密哈希、供应商、大小和日期戳。 此外，Microsoft Cloud Protection Service 可能会收集完整的 URL 以指明文件的来源。 这些 URL 有时可能包含个人信息，例如窗体中输入的搜索词或数据。 报告中可能还包括 Endpoint Protection 通知存在有害软件时你采取的操作。 Microsoft Cloud Protection Service 报告中包含此信息有助于 Microsoft 评估 Endpoint Protection 检测并删除恶意软件和有害软件的有效性，以及识别新的恶意软件。

如果有基本或高级的成员资格，则可以加入 Microsoft Cloud Protection Service。 基本成员报告中包含上述信息。 高级成员报告更加全面，可能包括有关 Endpoint Protection 检测到的软件的其他详细信息，例如此类软件的位置、文件名、软件操作方式以及软件影响计算机的方式。 这些报告以及来自其他加入 Microsoft Cloud Protection Service 的 Endpoint Protection 用户的报告有助于 Microsoft 研究人员更快地发现新威胁。 之后，将为符合分析条件的程序创建恶意软件定义，而更新后的定义将通过 Microsoft 更新提供给所有用户。

为了帮助检测和修复某些种类的恶意软件感染，产品会定期向 Microsoft Cloud Protection Service 发送有关用户的电脑安全状态的信息。 此信息包括有关用户的电脑的安全设置信息以及日志文件，描述在电脑启动时所加载的驱动程序和其他软件。
还会发送一个专门识别用户电脑的数字。 Microsoft Cloud Protection Service 可能还会收集潜在恶意软件文件连接到的 IP 地址。

Microsoft Cloud Protection Service 报告可用于改进 Microsoft 软件和服务。 这些报告还可用于进行统计或其他测试或分析目的，以及用于生成定义。 只有根据业务需要必须使用报告的 Microsoft 员工、承包商、合作伙伴和供应商才有权访问这些报告。

Microsoft Cloud Protection Service 不会有意收集个人信息。 就算 Microsoft Cloud Protection Service 收集到任何个人信息，Microsoft 也不会使用该信息来识别用户的身份或与用户联系。

有关可在产品文档中找到的收集数据的其他详细信息，请参阅 [System Center Configuration Manager 中的 Endpoint Protection](http://go.microsoft.com/fwlink/?LinkId=823547)。

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>站点层次结构 - 包含 Bing 地图的地理视图
站点层次结构 - 地理视图允许用户使用 Microsoft Bing 地图提供的地图查看 Configuration Manager 物理服务器拓扑。 为了启用此功能，会将你提供的位置信息从服务器发送到 Bing 地图 Web 服务。

Microsoft 使用该信息来运行和改进 Microsoft Bing 地图以及其他 Microsoft 站点和服务。 有关详细信息，请参阅 [Microsoft 隐私声明](http://go.microsoft.com/fwlink/?LinkId=823548)。
你可以选择不为站点层次结构使用地理视图。 “层次结构图表”视图允许你查看层次结构，且不使用 Bing 地图服务。

## <a name="microsoft-intune-subscription"></a>Microsoft Intune 订阅
购买了 Microsoft Intune 订阅的客户可以使用 Configuration Manager 管理其通过 Microsoft Intune 连接的移动设备。 [Microsoft Online Services 隐私声明](http://go.microsoft.com/fwlink/?LinkId=262214)适用于 Microsoft Online Services，包括 Microsoft Intune。 如果客户已拥有 Microsoft Intune 订阅，[Microsoft Online Services 隐私声明](http://go.microsoft.com/fwlink/?LinkId=262214)应配合本隐私声明释读。

与 Microsoft Intune 之间的所有通信都使用 HTTPS。 若要配置 Microsoft Intune 订阅以及下载配置 iOS 支持所需的证书签名请求 (CSR)，管理员必须使用其组织帐户和密码登录到 Microsoft Intune。 这些凭据未存储在 Configuration Manager 内。 与 Microsoft Intune 之间的所有其他通信都使用 Microsoft Intune 自动生成的 PKI 证书进行身份验证。

为了管理连接到 Microsoft Intune 的设备，会将某些信息发送到 Microsoft Intune 以及从 Microsoft Intune 接收某些信息。 此信息包括分配给服务的所有用户的用户主体名称 (UPN)，以及 Microsoft Intune 托管的那些设备的设备清单信息。 分配给 Manage.Microsoft.com 分发点的内容的元数据（例如应用程序名称、发布者和版本）会发送到 Microsoft Intune。 分配给 Manage.Microsoft.com 分发点的实际二进制内容在上传到 Microsoft Intune 之前会被加密。

默认情况下未配置此功能。 管理员控制传输到 Manage.Microsoft.com 分发点的内容以及分配给服务的用户。 随时可以删除此功能。
