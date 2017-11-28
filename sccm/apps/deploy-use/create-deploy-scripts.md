---
title: "创建和运行脚本"
titleSuffix: Configuration Manager
description: "在客户端设备上创建并运行 Powershell 脚本。"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: BrucePerlerMS
ms.author: bruceper
manager: angrobe
ms.openlocfilehash: 964f6d39c4c1afc82ff4336821740923d27cd569
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台创建并运行 PowerShell 脚本

*适用范围：System Center Configuration Manager (Current Branch)*

现在可以更好地将运行 Powershell 脚本的能力与 System Center Configuration Manager 集成。 Powershell 的优势是创建复杂而易懂的自动执行脚本，并能与较大社区分享。 脚本简化了自定义工具生成，便于软件管理，并让你快速完成常见任务，能够更轻松、更一致地完成大型工作。

将此集成到 System Center Configuration Manager，可以使用“运行脚本”功能来执行以下操作：

- 创建并编辑用于 Configuration Manager 的脚本。
- 通过角色和安全作用域管理脚本使用  
- 在集合或独立的本地托管 Windows 电脑上运行脚本。
- 从客户端设备获取快速聚合的脚本结果。
- 监视脚本执行，并查看脚本输出中生成的报告。

>[!IMPORTANT]
>脚本有如此强大的功能，记得在使用它们时仔细小心。 我们内置了额外的保护措施来帮助你；分离的角色和作用域。 运行脚本之前请务必验证脚本的准确性，并确保它们来自受信任的源，以防发生意外的脚本执行操作。 请注意扩展字符或其他混淆，并了解一下保护脚本的相关信息。

>[!TIP]
>PowerShell 与版本 1706 一起引入，是一项预发行功能。 要启用脚本，请参阅 [System Center Configuration Manager 中的预发布功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="prerequisites"></a>先决条件

- 要运行 PowerShell 脚本，客户端必须运行 PowerShell 3.0 或更高版本。 但是，如果运行的脚本包含 PowerShell 较高版本的功能，则运行该脚本的客户端必须运行该版本的 PowerShell。
- Configuration Manager 客户端必须从版本 1706 运行客户端，否则稍后才能运行脚本。
- 要使用这些脚本，你必须是相应 Configuration Manager 安全角色的成员。
- 导入并编写脚本 - 对于“完全权限管理员”安全角色中的“SMS 脚本”，帐户必须具有“创建”权限。
- 批准或拒绝脚本 - 对于“完全权限管理员”安全角色中的“SMS 脚本”，帐户必须具有“批准”权限。
- 运行脚本 - 对于“符合性设置管理员”安全角色中的“集合”，你的帐户必须具有“运行脚本”权限。

有关 Configuration Manager 安全角色的详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。

## <a name="limitations"></a>限制

“运行脚本”目前支持：

- 脚本语言：PowerShell
- 参数类型：整数和字符串

## <a name="run-script-authors-and-approvers"></a>“运行脚本”的创建者和审批者

“运行脚本”使用了“脚本创建者”和“脚本审批者”的概念，分别作为实现脚本和执行脚本的角色。 将创建者和审批者两个角色进行区分，使“运行脚本”这个强大的工具能够进行重要过程检查。

### <a name="scripts-roles-control"></a>脚本角色控制

默认情况下，用户不能批准他们创建的脚本。 由于这些脚本功能非常强大、用途多样，并且可以部署到多个设备，因此你可以将脚本创建者和脚本批准者之间的角色相互分开。 这些角色可以额外提升安全级别，避免在没有监督的情况下运行脚本。 你可以关闭此辅助批准，方便进行测试。

### <a name="approve-or-deny-a-script"></a>“批准”或“拒绝”脚本

脚本必须被“脚本审批者”角色批准，然后才能运行。 批准脚本：

1. 在 Configuration Manager 控制台中，单击“软件库”。
2. 在“软件库”工作区中，单击“脚本”。
3. 在“脚本”列表中，选择想要批准或拒绝的脚本，然后在“主页”选项卡“脚本”组中，单击“批准/拒绝”。
4. 在“批准或拒绝脚本”对话框中，选择“批准”或“拒绝”脚本，并根据需要输入有关你的决定的批注。  如果拒绝脚本，它将无法在客户端设备上运行。 <br>
![脚本 - 批准](./media/run-scripts/RS-approval.png)
5. 完成向导。 在“脚本”列表中可以看到“批准状态”列中发生的变化，具体要取决于你执行的操作。

### <a name="allow-users-to-approve-their-own-scripts"></a>允许用户批准他们自己的脚本

此批准主要用于脚本开发中的测试阶段。

1. 在 Configuration Manager 控制台中，单击“管理” 。
2. 在“管理”工作区中，展开“站点配置”，然后单击“站点”。
3. 在站点列表中，选择你的站点，然后在“主页”选项卡的“站点”组中，单击“层次结构设置”。
4. 在“层次结构设置属性”对话框的“常规”选项卡中，清除“不允许脚本创建者批准他们自己的脚本”复选框。

>[!IMPORTANT]
>最好是不允许脚本创建者审批自己的脚本。 仅实验室环境中允许此操作。 请仔细考虑在生产环境中更改此设置的潜在影响。

## <a name="security-scopes"></a>安全作用域
*（随版本 1710 一起引入）*  
“运行脚本”使用安全作用域（Configuration Manager 中的一项现有功能）通过分配代表用户组的标记来控制脚本的创作和执行。 有关使用安全作用域的详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="create-a-script"></a>创建脚本

1. 在 Configuration Manager 控制台中，单击“软件库”。
2. 在“软件库”工作区中，单击“脚本”。
3. 在“主页”选项卡的“创建”组中，单击“创建脚本”。
4. 在“创建脚本”向导的“脚本”页上，配置以下设置：
    - 脚本名称 - 输入脚本的名称。 虽然可以创建具有相同名称的多个脚本，但使用重复名称会让你难以在 Configuration Manager 控制台中查找所需的脚本。
    - 脚本语言 - 目前，仅支持 PowerShell 脚本。
    - 导入 - 将 PowerShell 脚本导入到控制台。 该脚本将在“脚本”字段中显示。
    - 清除 - 从“脚本”字段中删除当前脚本。
    - 脚本 - 显示当前导入的脚本。 你可以在此字段中根据需要编辑脚本。
1. 完成向导。 新脚本将显示在“脚本”列表，且状态显示为“正等待审批”。 在客户端设备上运行此脚本之前，必须先批准它。

## <a name="script-parameters"></a>脚本参数
*（随版本 1710 一起引入）*  
将参数添加到脚本可以为你的工作提供更高的灵活性。 以下内容概述“运行脚本”功能的当前功能以及“字符串”和“整数”数据类型的脚本参数。 也提供了预设值列表。 如果脚本具有不受支持的数据类型，你将收到一个警告。

在“创建脚本” 对话框中，单击“脚本”下的“脚本参数”。

你的每一个脚本参数都有自己的对话框，用于添加更多细节以及验证信息。

### <a name="parameter-validation"></a>参数验证

脚本中的每一个参数都有一个“脚本参数属性”对话框，可以在此处添加该参数的验证信息。 添加验证信息后，如果为参数输入了和验证不符的值，那么将收到错误消息。

#### <a name="example-firstname"></a>示例：FirstName

在此示例中，你可以设置字符串参数“FirstName”的属性。 请注意可选字段“自定义错误”。 此字段可用于添加有关特定字段的用户指南以及针对和字符串参数交互的用户指南，此示例中字符串参数为“FirstName”。

![脚本参数 - 字符串](./media/run-scripts/RS-parameters-string.png)

## <a name="script-examples"></a>脚本示例

以下几个示例对你希望用于此功能的脚本进行了说明。

### <a name="create-a-folder"></a>创建一个文件夹

``` powershell
New-Item "c:\scripts" -type folder name
```

### <a name="create-a-file"></a>创建文件

```powershell
New-Item "c:\scripts\new_file.txt" -type file name
```

### <a name="ping-a-given-computer"></a>对给定计算机执行 Ping 操作

此脚本采用了一个字符串，并将其作为“ping”操作的参数。

``` powershell
Param
(
 [String][Parameter(Mandatory=$True, Position=1)] $Computername
)

Ping $Computername
```

### <a name="get-battery-status"></a>获取电池状态

此脚本使用 WMI 对计算机查询它的电池状态。

``` powershell
Write-Output (Get-WmiObject -Class Win32_Battery).BatteryStatus

```

## <a name="run-a-script"></a>运行脚本

脚本经批准后，就可以在你选择的集合上运行了。 脚本执行开始之后，它通过高优先级系统快速启动，并在一小时内执行。 使用较慢的状态消息系统返回脚本结果。

1. 在 Configuration Manager 控制台中，单击“资产和符合性” 。
2. 在“资产和符合性”工作区中，单击“设备集合”。
3. 在“设备集合”列表中，单击要在其中运行脚本的设备集合。
4. 在“主页”选项卡的“所有系统”组中，单击“运行脚本”。
5. 在“运行脚本”向导的“脚本”页，从列表中选择一个脚本。 仅显示已批准的脚本。
6. 单击“下一步”，然后完成向导。

>[!IMPORTANT]
>如果脚本未运行（例如因为目标客户端关闭），则在这一小时内你必须再次运行它。

### <a name="target-machine-execution"></a>目标计算机执行
脚本在目标客户端上作为“系统”或“计算机”帐户执行。 此帐户的网络访问权限是受限的。 必须对通过该脚本进行的任何远程系统访问和访问位置进行相应的预配置。

## <a name="work-flow-and-monitoring"></a>工作流和监视

下面是“运行脚本”作为工作流所包含的内容：创建、批准、运行和监视。

![运行脚本 - 工作流](./media/run-scripts/RS-run-scripts-work-flow.png)

### <a name="script-monitoring"></a>脚本监视

在设备集合上启动脚本运行以后，请使用采用以下过程来监视该操作。 从版本 1710 开始就可以在脚本执行时进行实时监视，也能返回至某个给定“运行脚本”执行的报告。

1. 在 Configuration Manager 控制台中，单击“监视” 。
2. 在“监视”工作区中，单击“脚本状态”。 ![脚本监视器 - 脚本运行状态](./media/run-scripts/RS-monitoring-three-bar.png)
3. 在“脚本状态”列表中，可以查看在客户端设备上运行的每个脚本的结果。 脚本退出代码为“0”通常表示脚本已成功运行。

## <a name="see-also"></a>另请参阅

- [为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)
