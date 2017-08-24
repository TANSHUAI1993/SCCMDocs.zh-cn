---
title: "使用 Configuration Manager 创建和运行脚本 | Microsoft Docs"
description: "使用 Configuration Manager 在客户端设备上创建和运行脚本。"
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: ed84f7900eee5c04728d0e4d1b46027c36327bec
ms.sourcegitcommit: b41d3e5c7f0c87f9af29e02de3e6cc9301eeafc4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台创建并运行 PowerShell 脚本

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中，除了使用软件包和程序部署脚本之外，还可以使用以下功能执行下面的各项操作：

- 将 PowerShell 脚本导入到 Configuration Manager
- 从 Configuration Manager 控制台编辑脚本（仅针对未签名的脚本）
- 将脚本标记为“已批准”或“已拒绝”，以提高安全性
- 在 Windows 客户端 PC 和本地托管的 Windows PC 的集合上运行脚本。 不过，你不需要部署脚本，它们可以在客户端设备上近乎实时地运行。
- 在 Configuration Manager 控制台中检查脚本返回的结果。

>[!TIP]
>在该 Configuration Manager 版本中，脚本是预发布功能。 要启用脚本，请参阅 [System Center Configuration Manager 中的预发布功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="prerequisites"></a>先决条件

要运行 PowerShell 脚本，客户端必须运行 PowerShell 3.0 或更高版本。 但是，如果运行的脚本包含 PowerShell 较高版本的功能，则运行该脚本的客户端必须运行该版本。

Configuration Manager 客户端必须从版本 1706 运行客户端，否则稍后才能运行脚本。

要使用这些脚本，你必须是相应 Configuration Manager 安全角色的成员。

- 导入并编写脚本 - 对于“符合性设置管理员”安全角色中的“SMS 脚本”，你的帐户必须具有“创建”权限。
- 批准或拒绝脚本 - 对于“符合性设置管理员”安全角色中的“SMS 脚本”，你的帐户必须具有“批准”权限。
- 运行脚本 - 对于“符合性设置管理员”安全角色中的“集合”，你的帐户必须具有“运行脚本”权限。

有关 Configuration Manager 安全角色的详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。

默认情况下，用户不能批准他们创建的脚本。 由于这些脚本功能非常强大、用途多样，并且可以部署到多个设备，因此你可以将脚本创建者和脚本批准者之间的角色相互分开。 这些角色可以额外提升安全级别，避免在没有监督的情况下运行脚本。 你可以关闭此辅助批准，方便进行测试。

## <a name="allow-users-to-approve-their-own-scripts"></a>允许用户批准他们自己的脚本

1. 在 Configuration Manager 控制台中，单击“管理” 。
2. 在“管理”工作区中，展开“站点配置”，然后单击“站点”。
3. 在站点列表中，选择你的站点，然后在“主页”选项卡的“站点”组中，单击“层次结构设置”。
4. 在“层次结构设置属性”对话框的“常规”选项卡中，清除“不允许脚本创建者批准他们自己的脚本”复选框。

## <a name="import-and-edit-a-script"></a>导入和编辑脚本

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

### <a name="script-examples"></a>脚本示例

以下示例对你希望用于此功能的脚本进行了说明。

#### <a name="create-a-folder"></a>创建一个文件夹

New-Item "c:\scripts" - 键入文件名称 
 
 
#### <a name="create-a-file"></a>创建文件

New-Item c:\scripts\new_file.txt - 键入文件名称


## <a name="approve-or-deny-a-script"></a>批准或拒绝脚本

在可以运行脚本之前，必须先通过审批。 批准脚本：

1. 在 Configuration Manager 控制台中，单击“软件库”。
2. 在“软件库”工作区中，单击“脚本”。
3. 在“脚本”列表中，选择想要批准或拒绝的脚本，然后在“主页”选项卡“脚本”组中，单击“批准/拒绝”。
4. 在“批准或拒绝脚本”对话框中，“批准”或“拒绝”脚本，并根据需要输入有关你决定的批注。 如果拒绝脚本，它将无法在客户端设备上运行。
5. 完成向导。 在“脚本”列表中可以看到“批准状态”列中发生的变化，具体要取决于你执行的操作。

## <a name="run-a-script"></a>运行脚本
脚本经批准后，就可以在你选择的集合上运行了。

1. 在 Configuration Manager 控制台中，单击“资产和符合性”。
2. 在“资产和符合性”工作区中，单击“设备集合”。
3. 在“设备集合”列表中，单击要在其中运行脚本的设备集合。
4. 在“主页”选项卡的“所有系统”组中，单击“运行脚本”。
5. 在“运行脚本”向导的“脚本”页，从列表中选择一个脚本。 仅显示已批准的脚本。
6. 单击“下一步”，然后完成向导。

>[!IMPORTANT]
>该脚本的给定运行时间为一小时。 如果它在此时间段内没有运行（如电脑已关闭的情况），则必须再次运行它。

## <a name="next-steps"></a>后续步骤

在客户端设备中运行脚本后，使用此过程来监视操作成功与否。

1. 在 Configuration Manager 控制台中，单击“监视”。
2. 在“监视”工作区中，单击“脚本状态”。
3. 在“脚本状态”列表中，可以查看在客户端设备上运行的每个脚本的结果。 脚本退出代码为“0”通常表示脚本已成功运行。
