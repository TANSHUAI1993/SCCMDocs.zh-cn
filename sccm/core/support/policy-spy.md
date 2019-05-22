---
title: 策略 Spy
titleSuffix: Configuration Manager
description: 使用 Policy Spy 查看 Configuration Manager 客户端上的策略系统并对其进行故障排除。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 297aa9f8756b0c7214381e5e688f26cc21645fc4
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500855"
---
# <a name="policy-spy"></a>策略 Spy

适用范围：System Center Configuration Manager (Current Branch)

Policy Spy 是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 它是用于查看 Configuration Manager 客户端上的策略系统并对其进行故障排除的工具。 运行 **PolicySpy.exe**，打开用户界面。 有关命令行用法的详细信息，请参阅[命令行语法](#bkmk_policyspy-syntax)。

> [!Important]  
> 以管理员身份运行 Policy Spy。 如果没有**以管理员身份运行**，则会在“客户端信息”中看到以下错误：  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> 命令行语法

主要通过用户界面使用 Policy Spy。 它提供有限的命令行选项来支持自动化和批处理。

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>选项：`/export`
此选项以无提示方式导出本地计算机或远程计算机的策略。 `<ExportFilename>` 是该工具用于保存 XML 导出策略的文件名。 如果指定 `<computername>` 选项，Policy Spy 会导出该计算机的策略，而不导出本地计算机的策略。

> [!Note]  
> 此命令行选项不提供用于指定用户凭据的方法。 若要使用备用凭据访问远程计算机，请通过 **runas** 命令使用所需的安全凭据打开新的命令提示符。  


## <a name="usage"></a>用法

### <a name="tools-menu"></a>“工具”菜单

“工具”菜单中提供以下操作：  

- **远程打开**：连接到远程计算机上的 Configuration Manager 客户端策略。 使用“连接”对话框检索远程计算机的名称和可选的用户凭据。 如果连接失败，则会在“客户端信息”窗格中显示错误信息。 如果连接再次失败，请尝试通过在“编辑”菜单中选择“刷新”或按 F5 进行连接。  

- **打开文件**：打开由“导出策略”选项创建的策略导出文件 (XML)。 该工具使用与显示实时策略完全相同的方式显示导出的策略。 它禁用了一些仅在连接到实际客户端时才适用的功能。  

- **请求计算机分配**：在目标计算机上触发计算机策略分配请求。 此功能在查看导出的策略时禁用。  

- **评估计算机策略**：在目标计算机上触发计算机策略评估。 此功能在查看导出的策略时禁用。  

- **请求用户分配**：为当前登录的用户触发用户策略分配请求。 此功能仅在查看本地计算机上的策略时可用。  

- **评估用户策略**：为当前登录的用户触发用户策略评估。 此功能仅在查看本地计算机上的策略时可用。  

- **重置策略**：删除所有非默认策略并重置站点的策略 Cookie。 它随后会触发计算机策略分配请求。 此功能在查看导出的策略时禁用。  

- **导出策略**：将目标计算机的策略导出到 XML 文件。 可使用 Policy Spy 在任何计算机上查看此文件。 若要打开导出文件，请在“工具”菜单中选择“打开文件”。 此功能在查看导出的策略时禁用。  


### <a name="edit-menu"></a>“编辑”菜单

“编辑”菜单中提供以下操作：  

- **删除**：删除在“结果”窗格中选定的实例。 仅策略实例支持此操作。 如果尝试删除策略实例以外的任何内容，该工具会显示错误消息。 此功能在查看导出的策略时禁用。  

- **刷新**：刷新所有结果以查看最新信息。 在刷新之前展开的所有树节点随后会自动展开。 如果 Policy Spy 未成功连接到目标计算机的策略，它会尝试重新连接。 此功能在查看导出的策略时禁用。  

- **清除事件**：清除“事件”选项卡中的所有项目。  



## <a name="results-pane"></a>“结果”窗格

“结果”窗格显示目标计算机上策略系统的不同视图。 通过单击以下四个选项卡之一访问这些视图： 
- [实际](#bkmk_policyspy-actual)
- [已请求](#bkmk_policyspy-requested)
- [默认值](#bkmk_policyspy-default)
- [事件](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> 实际

此选项卡显示客户端的当前策略。 当前策略可确定客户端的行为及其客户端代理的行为，例如软件分发和库存。 该选项卡以树格式显示结果，其中包含针对计算机命名空间的根节点和每个特定于用户的命名空间。 展开命名空间节点以显示类列表。 展开类以显示实例列表。 类列表仅包含拥有实例的类。


### <a name="bkmk_policyspy-requested"></a> 已请求

此选项卡显示客户端从其分配的站点检索到的策略分配。 该选项卡以树格式显示结果，其中包含针对计算机命名空间的根节点和每个特定于用户的命名空间。 展开命名空间节点时会显示以下节点：  

- **配置**：显示从 CCM_Policy_Config 派生的配置类列表，其中包含策略对象、分配等。  

- **设置**：显示策略生成的所有有效设置。 设置在“配置”节点下显示。 

> [!Note]   
> 可存在具有相同名称的多个实例，因为客户端未将这些设置合并到最终结果集中。 Policy Spy 通过使用 RealKey 属性（而不使用其真正的策略密钥）来显示此节点下的实例。 将这些实例与“实际”选项卡中显示的结果集关联。  


### <a name="bkmk_policyspy-default"></a> 默认

此选项卡显示与“已请求”选项卡相同的信息。它还包括 DefaultMachine 和 DefaultUser 命名空间的内容。


### <a name="bkmk_policyspy-events"></a> 事件

此选项卡实时显示策略代理事件。 该视图为从 CCM_PolicyAgent_Event 派生的所有事件创建 WMI 事件订阅。 该视图最多显示 200 个事件。 它会根据需要从列表顶部删除最旧的事件。 如果选择列表中的最后一项，则列表会在添加新事件时自动向下滚动。 否则，视图会保持其当前位置，你必须向下滚动或按 End 键才能查看新事件。 查看导出的策略时，此视图始终为空。



## <a name="client-info-pane"></a>“客户端信息”窗格
“客户端信息”窗格显示目标计算机的属性列表。 它显示以下属性（如果可用）：  
- 名称
- ID
- 版本
- 站点
- 分配的 MP
- 常驻 MP
- 代理 MP
- 代理状态



## <a name="details-pane"></a>细节窗格
“详细信息”窗格显示有关当前选择的详细信息。 如果没有选择处于活动状态，它会显示有关 Policy Spy 本身的信息，包括版本。 否则，它会显示选定项目的托管对象格式 (MOF) 表示形式。

Policy Spy 使用自己的 MOF 生成例程来创建比 WMI 生成的纯文本 MOF 更加用户友好的 HTML 显示。 此行为允许 Policy Spy 添加以下功能，让 MOF 变得更易读：  

- 语法突出显示  

- 缩进对象和数组  

- 属性排列为系统组、继承组和本地组。 默认情况下，它会折叠系统组和继承组。 你可立即查看实例实际使用的属性。  

- 将 MOF 或纯文本 MOF 复制到剪贴板。 此功能对于通过直接调用 MofComp 工具将 MOF 粘贴到其他应用程序而言有用。  

对于从 CCM_Policy_Policy 派生的 Policy 对象的实例，“详细信息”窗格会在显示的 MOF 下方显示策略正文。 如果客户端未下载策略正文，Policy Spy 会显示超链接。 单击该链接可直接从客户端的管理点下载策略正文。 如果该工具成功下载策略正文，则会将该超链接替换为回复内容。 否则，Policy Spy 会更新显示内容，指明请求失败。

