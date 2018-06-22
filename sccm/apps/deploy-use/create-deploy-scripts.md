---
title: 创建和运行脚本
titleSuffix: Configuration Manager
description: 在客户端设备上创建并运行 Powershell 脚本。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fcf3bc335efc4c7436842b29d30c67c118ceb05d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339020"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台创建并运行 PowerShell 脚本

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1236459-->
System Center Configuration Manager 具有运行 Powershell 脚本的集成功能。 Powershell 的优势是创建复杂而易懂的自动执行脚本，并能与较大社区分享。 脚本简化了自定义工具生成，便于软件管理，并让你快速完成常见任务，能够更轻松、更一致地完成大型工作。  

> [!TIP]  
> 此功能在 1706 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从 1802 版开始，此功能不再属于预发行功能。  


> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


将此集成到 System Center Configuration Manager，可以使用“运行脚本”功能执行以下操作：

- 创建并编辑用于 System Center Configuration Manager 的脚本。
- 通过角色和安全作用域管理脚本使用。 
- 在集合或独立的本地托管 Windows 电脑上运行脚本。
- 从客户端设备获取快速聚合的脚本结果。
- 监视脚本执行，并查看脚本输出中生成的报告。

>[!WARNING]
>脚本有如此强大的功能，记得在使用它们时仔细小心。 我们内置了额外的保护措施来帮助你；分离的角色和作用域。 运行脚本之前请务必验证脚本的准确性，并确保它们来自受信任的源，以防发生意外的脚本执行操作。 请注意扩展字符或其他混淆，并了解一下保护脚本的相关信息。 [详细了解 PowerShell 脚本安全性](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>先决条件

- 要运行 PowerShell 脚本，客户端必须运行 PowerShell 3.0 或更高版本。 但是，如果运行的脚本包含 PowerShell 较高版本的功能，则运行该脚本的客户端必须运行该版本的 PowerShell。
- Configuration Manager 客户端必须从版本 1706 运行客户端，否则稍后才能运行脚本。
- 要使用这些脚本，你必须是相应 Configuration Manager 安全角色的成员。
- 导入并编写脚本 - 帐户必须对“SMS 脚本”具有“创建”权限。
- 批准或拒绝脚本 - 帐户必须对“SMS 脚本”具有“批准”权限。
- 运行脚本 - 帐户必须对“集合”具有“运行脚本”权限。

有关 Configuration Manager 安全角色的详细信息，请参阅：</br>
[运行脚本的安全作用域](#BKMK_Scopes)</br>
[运行脚本的安全角色](#BKMK_ScriptRoles)</br>
[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。

## <a name="limitations"></a>限制

“运行脚本”目前支持：

- 脚本语言：PowerShell
- 参数类型：整数、字符串和列表。


>[!WARNING]
>请注意，使用参数时会打开外围应用，可能存在 PowerShell 注入攻击风险。 可通过多种方法缓解和解决此问题，例如，使用正则表达式验证参数输入或使用预定义参数。 常见最佳做法是不在 PowerShell 脚本 中包含机密（不包含密码等）。 [详细了解 PowerShell 脚本安全性](/sccm/apps/deploy-use/learn-script-security)<!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>“运行脚本”的创建者和审批者

“运行脚本”使用了“脚本创建者”和“脚本审批者”的概念，分别作为实现脚本和执行脚本的角色。 将创建者和审批者两个角色进行区分，使“运行脚本”这个强大的工具能够进行重要过程检查。 还有一个“脚本运行者”角色允许执行脚本，但不允许创建或批准脚本。 请参阅[为脚本创建安全角色](#BKMK_ScriptRoles)。

### <a name="scripts-roles-control"></a>脚本角色控制

默认情况下，用户不能批准他们创建的脚本。 由于这些脚本功能非常强大、用途多样，并且可能部署到多个设备，因此可以将脚本创建者和脚本批准者之间的角色相互分开。 这些角色可以额外提升安全级别，避免在没有监督的情况下运行脚本。 可以关闭辅助批准，方便进行测试。

### <a name="approve-or-deny-a-script"></a>“批准”或“拒绝”脚本

脚本必须被“脚本审批者”角色批准，然后才能运行。 批准脚本：

1. 在 Configuration Manager 控制台中，单击“软件库”。
2. 在“软件库”工作区中，单击“脚本”。
3. 在“脚本”列表中，选择想要批准或拒绝的脚本，然后在“主页”选项卡“脚本”组中，单击“批准/拒绝”。
4. 在“批准或拒绝脚本”对话框中，选择“批准”或“拒绝”脚本。 （可选）输入有关你决定的注释。  如果拒绝脚本，它将无法在客户端设备上运行。 <br>
![脚本 - 批准](./media/run-scripts/RS-approval.png)
1. 完成向导。 在“脚本”列表中可以看到“批准状态”列中发生的变化，具体要取决于你执行的操作。

### <a name="allow-users-to-approve-their-own-scripts"></a>允许用户批准他们自己的脚本

此批准主要用于脚本开发中的测试阶段。

1. 在 Configuration Manager 控制台中，单击“管理”。
2. 在“管理”工作区中，展开“站点配置”，然后单击“站点”。
3. 在站点列表中，选择你的站点，然后在“主页”选项卡的“站点”组中，单击“层次结构设置”。
4. 在“层次结构设置属性”对话框的“常规”选项卡中，清除“不允许脚本创建者批准他们自己的脚本”复选框。

>[!IMPORTANT]
>最好是不允许脚本创建者审批自己的脚本。 仅实验室环境中允许此操作。 请仔细考虑在生产环境中更改此设置的潜在影响。

## <a name="security-scopes"></a>安全作用域
*（随版本 1710 一起引入）*  
“运行脚本”使用安全作用域（Configuration Manager 中的一项现有功能）通过分配代表用户组的标记来控制脚本的创作和执行。 有关使用安全作用域的详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="bkmk_ScriptRoles"></a>为脚本创建安全角色
默认情况下，用于运行脚本的三个安全角色不在 Configuration Manager 中创建。 要创建脚本运行者、脚本创建者和脚本审批者角色，请执行下列所述步骤。

1. 在 Configuration Manager 控制台中，转到“管理” >“安全性” >“安全角色”
2. 右键单击一个角色，然后单击“复制”。 复制的角色已分配有权限。 确保仅获取所需的权限。 
3. 为自定义角色提供“名称”和“说明”。 
4. 按如下所述为安全角色分配权限。  

### <a name="security-role-permissions"></a>安全角色权限  

**角色名称**：脚本运行者  
- **说明**：这些权限仅允许此角色运行之前创建且已由其他角色批准的脚本。  
- **权限**：确保将以下项设置为“是”。  

|类别|权限|状态|
|---|---|---|
|收集|运行脚本|是|
|站点|读取|是|
|SMS 脚本|创建|是|
|SMS 脚本|读取|是|


**角色名称**：脚本创建者  
- **说明**：这些权限允许此角色编写脚本，但不能批准或运行脚本。  
- **权限**：确保设置以下权限。
 
|类别|权限|状态|
|---|---|---|
|收集|运行脚本|否|
|站点|读取|是|
|SMS 脚本|创建|是|
|SMS 脚本|读取|是|
|SMS 脚本|删除|是|
|SMS 脚本|修改|是|


**角色名称**：脚本审批者  
- **说明**：这些权限允许此角色批准脚本，但不能创建或运行脚本。  
- **权限**：确保设置以下权限。  

|类别|权限|状态|
|---|---|---|
|收集|运行脚本|否|
|站点|读取|是|
|SMS 脚本|读取|是|
|SMS 脚本|批准|是|
|SMS 脚本|修改|是|

     
**脚本创建者角色的 SMS 脚本权限示例**  

 ![脚本创建者角色的 SMS 脚本权限示例](./media/run-scripts/script_authors_permissions.png)

   

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
5. 完成向导。 新脚本将显示在“脚本”列表，且状态显示为“正等待审批”。 在客户端设备上运行此脚本之前，必须先批准它。 

> [!IMPORTANT]
    >避免在使用“运行脚本”功能时编写设备重启或 Configuration Manager 代理重启的脚本。 执行此操作可能会导致连续的重启状态。 如有需要，从 Configuration Manager 版本 1710 起，已经对启用重启设备的客户端通知功能提供了增强。 [等待重新启动列](/sccm/core/clients/manage/manage-clients#Restart-clients)可以帮助识别需要重启的设备。 
<!--SMS503978  -->

## <a name="script-parameters"></a>脚本参数
*（随版本 1710 一起引入）*  
将参数添加到脚本可以为你的工作提供更高的灵活性。 以下内容概述“运行脚本”功能的当前功能以及“字符串”和“整数”数据类型的脚本参数。 也提供了预设值列表。 如果脚本具有不受支持的数据类型，你将收到一个警告。

在“创建脚本” 对话框中，单击“脚本”下的“脚本参数”。

你的每一个脚本参数都有自己的对话框，用于添加更多细节以及验证信息。

>[!IMPORTANT]
> 参数值不能包含单引号。 </br></br>
> 在 Configuration Manager 版本 1802 中存在一个已知问题，即无法将带空格的参数正确传递给脚本。 如果在参数中使用空格，则只能将参数中的第一项传递给脚本，而空格后的所有项均不会传递。 要解决此问题，管理员可采用将空格替换为其他字符并进行转换的编写脚本的方法，或使用其他方法。


### <a name="parameter-validation"></a>参数验证

脚本中的每一个参数都有一个“脚本参数属性”对话框，可以在此处添加该参数的验证信息。 添加验证信息后，如果为参数输入了和验证不符的值，那么将收到错误消息。

#### <a name="example-firstname"></a>示例：FirstName

在此示例中，你可以设置字符串参数“FirstName”的属性。

![脚本参数 - 字符串](./media/run-scripts/RS-parameters-string.png)


“脚本参数属性”对话框的验证部分包含供你使用的以下字段：

- 最小长度 - FirstName 字段的最小字符数。
- 最大长度 - FirstName 字段的最大字符数
- RegEx - 正则表达式的简称。 有关使用正则表达式的详细信息，请参阅下一部分中的“使用正则表达式验证”。
- 自定义错误 - 用于添加你自己的自定义错误消息，该消息将取代任何系统验证错误消息。

#### <a name="using-regular-expression-validation"></a>使用正则表达式验证

正则表达式是一种紧凑的编程形式，用于检查一串字符的编码验证。 例如，可以通过将 `[^A-Z]` 放入“RegEx”字段，来检查“FirstName”字段中是否缺少大写字母字符。

.NET Framework 支持此对话框的正则表达式处理。 有关使用正则表达式的指南，请参阅 [.NET 正则表达式](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions)。 


## <a name="script-examples"></a>脚本示例

以下几个示例对你希望用于此功能的脚本进行了说明。

### <a name="create-a-new-folder-and-file"></a>创建新文件夹和文件

如果提供命名输入，此脚本会在文件夹中创建一个新文件夹和一个文件。

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName,
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>获取 OS 版本

此脚本使用 WMI 来查询计算机的 OS 版本。

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>运行脚本

经批准后，脚本就可以在单个设备或集合上运行。 脚本开始执行后，它通过会在一小时内超时的高优先级系统快速启动。 然后使用状态消息系统返回脚本结果。

要为脚本选择目标集合：

1. 在 Configuration Manager 控制台中，单击“资产和符合性”。
2. 在“资产和符合性”工作区中，单击“设备集合”。
3. 在“设备集合”列表中，单击要在其中运行脚本的设备集合。
4. 选择所选集合，单击“运行脚本”。
5. 在“运行脚本”向导的“脚本”页，从列表中选择一个脚本。 仅显示已批准的脚本。
6. 单击“下一步”，然后完成向导。

>[!IMPORTANT]
>如果脚本未运行（例如，因为目标设备关闭），则在这一小时内你必须再次运行。

### <a name="target-machine-execution"></a>目标计算机执行

脚本在目标客户端上作为“系统”或“计算机”帐户执行。 此帐户的网络访问权限是受限的。 必须对通过该脚本进行的任何远程系统访问和访问位置进行相应的预配置。

## <a name="script-monitoring"></a>脚本监视

在设备集合上启动脚本运行以后，请使用采用以下过程来监视该操作。 从版本 1710 开始，你可以在脚本执行时进行实时监视，也可以返回至某个给定“运行脚本”执行的报告。 <br>

![脚本监视器 - 脚本运行状态](./media/run-scripts/RS-monitoring-three-bar.png)

1. 在 Configuration Manager 控制台中，单击“监视”。
2. 在“监视”工作区中，单击“脚本状态”。
3. 在“脚本状态”列表中，可以查看在客户端设备上运行的每个脚本的结果。 脚本退出代码为“0”通常表示脚本已成功运行。
    - 从 Configuration Manager 1802 开始，脚本输出截断为 4 KB，以便提供更好的显示体验。  <!--510013-->
      ![脚本监视器 - 截断的脚本](./media/run-scripts/Script-monitoring-truncated.png) 

## <a name="script-output"></a>脚本输出

- 从 Configuration Manager 1802 版开始，脚本输出重新使用 JSON 格式。 此格式一致返回可读的脚本输出。 
- 收到未知结果或客户端脱机的脚本不会在图表或数据集中显示。 <!--507179-->
- 由于脚本输出截断为 4 KB，因此请避免返回大型脚本输出。 <!--508488-->
- 在低级别版本的客户端上运行 Configuration Manager 1802 版或更高版本时，某些脚本输出格式设置功能可能不可用。 <!--508487-->
    - 如果 Configuration Manager 客户端版本低于 1802，你会得到一个字符串输出。
    -  对于 Configuration Manager 客户端 1802 及更高版本，你会得到 JSON 格式。
        - 例如，你可能得到两个结果，在一个客户端版本上显示 TEXT，在另一个版本上显示 "TEXT"（输出括在双引号中），这两个结果将作为两个不同的类别放入图表中。
        - 如果需要解决此问题，请考虑针对两个不同的集合运行脚本。 一个集合包含 1802 以前的客户端，另一个集合包含 1802 及更高版本的客户端。 或者，你可以将脚本中的枚举对象转换为字符串值，以便它们以 JSON 格式正确显示。 
- 将脚本中的枚举对象转换为字符串值，以便它们以 JSON 格式正确显示。 <!--508377-->![将枚举对象转换为字符串值](./media/run-scripts/enum-tostring-JSON.png)



## <a name="see-also"></a>另请参阅

- [为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)
