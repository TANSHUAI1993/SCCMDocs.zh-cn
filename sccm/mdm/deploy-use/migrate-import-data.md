---
title: "将数据导入 Microsoft Intune"
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: 4b5f788a611b9df7c12f788099d82fadbf1e4af9
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>将 Configuration Manager 数据导入 Microsoft Intune 

*适用范围：System Center Configuration Manager (Current Branch)*    

在仅限云的配置中[将混合 MDM 用户和设备迁移到 Intune 独立版](migrate-hybridmdm-to-intunesa.md)过程中的第一步，建议使用 Intune 数据导入程序工具。 如果需要，可以跳过这一步，并转到[准备 Intune 以便进行用户迁移](migrate-prepare-intune.md)阶段。 但是，该工具执行以下功能，可以在下一阶段节省大量时间： 
1.  收集有关从 Configuration Manager 层次结构选择的对象的数据。 
2.  提供可以选择用于导入的对象的详细信息以及无法导入某个对象的原因。
3.  将所选的对象导入 Microsoft Intune 租户。 

数据导入程序工具不会以任何方式更改 Configuration Manager 环境，因此，可以将对象导入 Intune 并验证一切是否都按照预期运行，同时也不会有让混合 MDM 设备处于不受管理状态的风险。 

## <a name="what-objects-can-this-tool-import"></a>此工具可以导入哪些对象？
导入工具可以在 Configuration Manager 中收集有关以下对象类型的信息，并提供有关所收集的对象是否可以导入的信息： 
- 配置项目
- 证书配置文件
- 电子邮件配置文件
- VPN 配置文件
- Wi-Fi 配置文件
- 相容性策略
- 应用
- 部署

> [!Note]    
> 导入部署仅适用于正在导入的其他对象类型。 例如，如果导入 VPN 配置文件和部署，则只能导入所选 VPN 配置文件的部署。 Intune 中的部署称为分配。 如果想要为之前已导入的对象导入部署，则需要再次导入该对象或在 Azure 上 Intune 中手动创建分配。 例如，如果导入 VPN 配置文件但没有导入部署，则需要再次运行此工具并选择 VPN 配置文件和部署，或者在 Azure 上 Intune 中手动创建分配。  如果重新运行此工具，则会创建重复的对象，可以稍后在 Azure 上 Intune 中删除该对象。  

> [!Important]    
> 如果部署的集合基于已复制到 Azure Active Directory (AAD) 的 Active Directory 组，则该工具自动将已迁移对象定向到此组，如果在运行工具时选择了适当部署的话。 当有更复杂的集合或直接成员资格集合时，须手动在 AAD 中重新创建它们，并在 Azure 上 Intune 中手动将对象分配定向到它们。


## <a name="things-to-know-before-you-run-the-tool"></a>运行工具前需知事项
- 运行此工具不会以任何方式更改 Configuration Manager 环境。
- 我们建议首先使用试用版租户测试数据导入过程。 然后，在确认所需数据已导入后，可以通过生产 Intune 租户进行相同的进程。
- 数据导入程序仅导入 Configuration Manager 数据一次。 它不会对 Configuration Manager 或 Intune 中的对象保持跟踪。 但是，如果在同一计算机上再次运行导入程序，它会说明哪些对象之前导入过。 此工具不知晓该对象是否仍存于 Intune 中，或者是否已更改。 如果多次将数据导入 Intune 中，最终可能有重复的对象。
- 不是所有的配置文件设置都可以导入。 例如，无法导入展台模式或 PFX 设置。 
- 如果 Configuration Manager 策略的设置不适用于所选的平台，则工具将在导入期间忽略这些设置。 忽略这些设置有助于确保 Intune 能够导入并支持此策略。 
- 此工具将尝试提供无法导入某个对象的原因。 某些情况下，在将对象导入 Intune 之前，可以返回 Configuration Manager 控制台、修复问题，并再次启动 Configuration Manager 对象发现扫描，然后导入该对象。 有时可能需要或想要在 Intune 中手动重新创建这些对象。
- 存在一些依赖于其他对象的配置文件。 如果要导入依赖于另一个对象的配置文件（如依赖于证书的电子邮件配置文件），则必须同时导入这两个对象。
- 运行此工具后，可能需要执行其他手动步骤。 例如，将应用和策略定向到 AAD 组。 

## <a name="prerequisites"></a>先决条件
- 对于 Configuration Manager 版本 1610 或更高版本 - 我们建议指定顶级站点并通过有权访问站点层次结构中所有对象的用户来运行此工具。 该工具仅发现运行该工具的用户有权访问的对象。 
- 须从有权访问 SMS 提供程序（用于收集 Configuration Manager 数据）和 Internet（用于将对象导入到 Intune）的计算机上，运行此工具。
- 全局管理员首次运行此工具时，须使用以下参数 intunedataimporter.exe -GlobalConsent。 然后，全局管理员或 Intune 管理员才可以运行此工具。  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>下载数据导入程序工具
可以从 GitHub 的 ConfigMgrTools/Intune-Data-Importer 存储库中下载数据导入程序工具。 使用以下过程下载该工具。

1. 转到 [Intune 数据导入程序 GitHub](https://go.microsoft.com/fwlink/?linkid=858194) 页。
2. 依次单击“克隆或下载”、“下载 ZIP”，并保存已压缩的 ZIP 文件。 
3. 提取 ZIP 文件的内容。

## <a name="run-the-data-importer-tool"></a>运行数据导入程序工具
在运行数据导入程序工具之前，须使用全局管理员帐户在 Azure 中为数据导入程序工具授权，让其能够访问资源。 然后，才能使用全局管理员或 Intune 管理员帐户运行此工具。     

数据导入程序工具的向导可分为三个主要步骤。 此部分将提供帮助信息，辅助完成向导中的每个步骤，并确保将 Configuration Manager 数据成功地导入 Intune 中。 每个步骤都从上一个步骤结束的地方继续开始。

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>为数据导入程序工具授权，使其能够访问资源
1.  全局管理员首次运行此工具时，须使用以下参数：intunedataimporter.exe -GlobalConsent 
2. 当工具启动时，将显示一个登录屏幕，须使用 Azure 中全局管理员角色的帐户登录。 
3. 单击“接受”，在 Azure 中创建具有 Microsoft Graph 中适当权限的应用程序。 数据导入程序工具需要具有这些权限，才能将对象导入 Microsoft Intune。   

   > [!Important]
   > 单击“接受”时，即表示同意工具有权执行以下操作：
   > - 读取所有组
   > - 登录并读取用户配置文件
   > - 读取并写入 Intune 设备配置和策略
   > - 读取并写入 Intune 应用
   > - 读取并写入 Intune 基于角色的管理控制策略
   > - 读取并写入 Intune 设备
   > - 读取并写入 Intune 配置
1. 接受同意后，其他任何全局管理员或 Intune 管理员都可运行此工具，从而将数据从 Configuration Manager 导入 Azure 上 Intune 中。    
        
    > [!Note]
    > 如果事先没有获得全局管理员同意，则在 Intune 管理员运行数据导入程序工具，并登录到 Intune 订阅之后，该工具会显示“无法访问此应用程序”。

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>阶段 1：发现 Configuration Manager 对象和收集数据
在阶段 1 中，选择要发现的对象并让该工具收集有关所选对象的信息。 
1. 打开工具并单击“开始”。  
2. 阅读信息，然后单击“下一步”。 
3. 针对站点和该站点上想要导入的对象，提供以下信息。 
    - **站点服务器名称**：提供要导入对象的站点服务器的完全限定的域名。 该工具仅发现运行该工具的用户有权访问的对象。 通常指定顶级站点并通过有权访问站点层次结构中所有对象的用户来运行此工具。
    - **站点代码**：为站点服务器提供站点代码。 可以在 Configuration Manager 控制台顶部找到三个字母的代码。
    - **要导入的对象类型**：选择想要工具收集的对象。 可以选择“选择全部”来选择所有对象，或者选择个别对象类型。 
4.  单击“下一步”，开始发现站点中的对象。 此工具显示了每个对象类型的进度。 
    - 当工具发现没有与所选对象类型有关的数据时，进度栏将立即对该对象类型显示已完成。
    - 没有选择的对象不会在“收集”数据页面上显示。 
    - 可以再次运行工具，查看未收集或在收集过程中取消收集的对象。

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>阶段 2：解决问题并选择要导入的对象  
在阶段 2 中，审阅工具查找到的对象，解决阻止将对象导入 Intune 的问题，并选择要导入的对象。 如果已修复问题，请返回到向导的“发现环境”页面重新发现对象。 
5.  单击“下一步”，审阅已收集的对象。 每个已收集的对象类型都有项目选择页面。 

    > [!Tip]     
    > 在每个项目选择页面上，可以创建筛选器，帮助查找想要导入的对象。 但是，请注意以下事项：
    > - 当位于项目选择页面且视图经过筛选时，“选择全部”复选框仅适用于已显示的项目。 使用该复选框时，不能包括任何由于筛选器而隐藏的对象。
    > - 即使为对象进行排序或筛选，对象也始终划分在其父项之下。


6.  在每个项目选择页面上，依据“可导入”列对对象进行排序，并审阅不可导入的对象。 “说明”列中详细说明了工具无法导入该对象的原因。 
7.  现在须决定是否要修复不可导入对象的任何问题。 如果修复了一个或多个问题，请单击“上一步”，直到从 Configuration Manager 页面转到选择数据，并再次收集数据查看是否已解决问题。 可以继续修复问题，直到对可导入的对象感到满意。 
8.  在每个项目选择页面上，选择想要导入的对象。 已列出以下各列：
    - **名称**：Configuration Manager 对象的名称。 
    - **可导入**：指定对象是否可导入。 可以仅选择在“可导入”列中标为“是”的对象。 
    - **平台**：指定受对象支持的平台。
    - **已导入**：指定是否已在此计算机上使用该工具导入过该对象。 
    - **说明**：说明无法导入对象的原因。
    - **配置基线**（针对配置项目）：指定与配置项目关联的配置基线。
    - **所需证书**（针对配置文件和策略）：指定证书是否与对象关联。 当证书与对象相关联时，也需要导入证书。
9.  选择要导入的对象之后，这些对象将在“摘要”页中列出。 可以执行以下操作： 
    - **导出详细信息**：创建包含屏幕上所显示的信息的 .csv 文件。 可以保留此文件，作为记录。 
    - **导出错误数据**：导出压缩文件，该文件包含工具无法转换或导入的数据的相关信息。 

### <a name="phase-3-import-selected-object-to-intune"></a>阶段 3：将所选对象导入 Intune
在阶段 3 中，将登录到 Intune，并导入所选对象。 
10. 依次单击“下一步”、“登录到 Intune”，登录到 Intune 租户以导入数据。 须使用全局管理员或 Intune 管理员帐户登录。 登录之后，导入过程将启动。

    > [!Important]
    > 我们建议首先使用试用版租户测试数据导入过程。 然后，在确认所需数据已导入后，可以通过生产 Intune 租户进行相同的进程。

12. “进度”页提供导入对象时的进度。 导入完成时，单击“下一步”。 
13. “完成”页上会列出已导入的对象。 检查在导入过程中遇到错误的任何对象的状态。 可以执行以下操作： 
    - **导出详细信息**：创建包含屏幕上所显示的信息的 .csv 文件。 可以保留此文件，作为记录。 
    - **导出错误数据**：导出压缩文件，该文件包含工具无法转换或导入的数据的相关信息。

## <a name="next-steps"></a>后续步骤
将数据导入到 Intune 之后，须采取步骤[准备 Intune 以便进行用户迁移](migrate-prepare-intune.md)。 