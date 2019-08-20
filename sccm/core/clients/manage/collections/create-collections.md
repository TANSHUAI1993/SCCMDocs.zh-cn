---
title: 创建集合
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中创建集合以更轻松地管理用户和设备的分组。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bec2d55cdf7ff5d405ee689c821735413e8a9ff
ms.sourcegitcommit: 4241c15a277c57b5480dea70fc30f1ed46ffd4f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69490093"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>如何在 Configuration Manager 中创建集合

适用范围：  System Center Configuration Manager (Current Branch)

集合是用户组或设备组。 集合可用于执行管理应用程序、部署合规性设置或安装软件更新等任务。 还可以使用集合来管理客户端设置的组，或将它们与基于角色的管理结合使用来指定管理用户可以访问的资源。 Configuration Manager 包含几个内置集合。 有关详细信息，请参阅[集合简介](/sccm/core/clients/manage/collections/introduction-to-collections)。  

> [!NOTE]  
> 集合可以包含用户或设备，但不能同时包含两者。  


本文介绍了如何在 Configuration Manager 中创建集合。 也可以导入在当前或其他 Configuration Manager 站点上创建的集合。 有关如何导出和导入集合的详细信息，请参阅[如何管理集合](/sccm/core/clients/manage/collections/manage-collections)。  


## <a name="collection-rules"></a>集合规则

在 Configuration Manager 中，可以使用不同类型的规则来配置集合成员。  


### <a name="direct-rule"></a>直接规则

直接规则可用于选择要添加到集合的用户或计算机。 除非从 Configuration Manager 中删除资源，否则成员身份不会改变。 在将资源添加到直接规则集合之前，Configuration Manager 必须已发现资源，否则必须先导入资源。 直接规则集合的管理开销高于查询规则集合，因为前者需要手动更改。


### <a name="query-rule"></a>查询规则

基于 Configuration Manager 按计划运行的查询来动态更新集合的成员身份。 例如，可以创建一个用户集合，其中的用户是 Active Directory 域服务中的人力资源组织单位的成员。 此集合会在向人力资源组织单位添加新用户或从中删除用户时自动更新。

有关可用于构建集合的示例查询，请参阅[如何创建查询](/sccm/core/servers/manage/create-queries)。


### <a name="device-category-rule"></a>设备类别规则

通过将设备类别与设备集合相关联，可以更轻松地管理设备。 

有关详细信息，请参阅[自动将设备分类到集合](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)。<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>包括集合规则

包括 Configuration Manager 集合中其他集合的成员。 如果所含集合发生更改，Configuration Manager 会按计划更新当前集合的成员身份。

可以向集合添加多个包括集合规则。


### <a name="exclude-collection-rule"></a>排除集合规则

排除集合规则可用于从一个 Configuration Manager 集合中排除其他集合的成员。 如果排除的集合发生更改，Configuration Manager 会按计划更新当前集合的成员身份。

可以向集合添加多个排除集合规则。 如果集合同时包含包括集合和排除集合规则，并且存在冲突，则排除集合规则优先级较高。

#### <a name="example"></a>示例
创建一个集合，它具有一个包括集合规则和一个排除集合规则。 包括集合规则用于 Dell 台式机的集合。 排除集合适用于 RAM 小于 4GB 的计算机集合。 新集合包含 RAM 至少为 4GB 的 Dell 台式机。



## <a name="bkmk_create"></a>创建集合  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。  

    - 要创建设备集合，请选择“设备集合”节点   。 然后，在功能区的“主页”  选项卡上，选择“创建”  组中的“创建设备集合”  。  

    - 要创建用户集合，请选择“用户集合”节点   。 然后，在功能区的“主页”  选项卡上，选择“创建”  组中的“创建用户集合”  。  

2. 在向导的“常规”  页上，提供“名称”  和“注释”  。 在“限定集合”  部分中，选择“浏览”  ，并选择限定集合。 要创建的集合只包含限定集合中的成员。  

4. 在“成员身份规则”  页上的“添加规则”  列表中，选择要用于此集合的成员身份规则的类型。 可以为每个集合配置多个规则。 每个规则的配置各不相同。 若要详细了解如何配置每个规则，请参阅本文的以下部分：  
    - [直接规则](#bkmk-direct)
    - [查询规则](#bkmk-query)
    - [设备类别规则](#bkmk-category)
    - [包括集合规则](#bkmk-include)
    - [排除集合规则](#bkmk-exclude)

5. 同样，在“成员身份规则”  页上，审阅以下设置。

    - **对此集合使用增量更新**：选择此选项可定期扫描并仅更新上一次集合评估中的新资源或已更改的资源。 此过程独立于完整的集合评估。 默认情况下，按 5 分钟的间隔进行增量更新。  

        > [!IMPORTANT]  
        >  具有使用以下类的查询规则的集合不支持增量更新：  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails（仅用于用户集合）  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails（仅用于用户集合）  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **对此集合计划完全更新**：计划集合成员身份的定期完全评估。  

        自版本 1810 起，集合评估行为的以下更改可提升站点性能：<!--3607726-->  

        - 以前，在基于查询的集合上配置计划时，站点将继续评估查询，无论你是否启用了“在此集合上计划完全更新”  的集合设置。 若要完全禁用计划，必须将计划更改为“无”  。

            现在，当你禁用此设置时，站点将清除计划。 若要指定对计划进行集合评估，请启用“在此集合上计划完全更新”  的选项。  

            在更新站点时，对于在其中指定计划的任何现有集合，站点将启用“在此集合上计划完全更新”  的选项。 尽管此配置可能并不是你的本意，但它是更新站点之前计划的实际行为。 若要停止在计划上评估集合的站点，请禁用此选项。  

        - 你无法禁用“所有系统”  等内置集合的评估，但现在可以配置计划。 此行为使你能够在满足需求的同时自定义此操作。 

            > [!TIP]  
            > 在内置集合中，只会更改自定义计划的时间  。 不会更改定期模式  。 未来迭代可能会强制实施特定定期模式。  

6. 完成向导以创建新集合。 新集合会显示在“资产和符合性”  工作区的“设备集合”  节点中。  

> [!NOTE]  
> 必须刷新或重新加载 Configuration Manager 控制台才能查看集合成员。 直到第一次计划更新后，它们才会出现在集合中。 也可以手动为集合选择“更新成员资格”  。 集合更新可能需要几分钟才能完成。  

        
### <a name="bkmk-direct"></a>配置直接规则  

1. 在“创建直接成员身份规则向导”  的“搜索资源”  页上，指定以下信息。  

    - **资源类**：选择要搜索并添加到集合的资源的类型。 例如：
        - **系统资源**：搜索从客户端计算机返回的清单数据。
        - **未知计算机**：在从未知计算机返回的值中进行选择。
        - **用户资源**：搜索 Configuration Manager 收集的用户信息。
        - **用户组资源**：搜索 Configuration Manager 收集的用户组信息。

    - **属性名称**：选择与要搜索的所选资源类关联的属性。 例如：  

        - 如果要按其 NetBIOS 名称来选择计算机，则在“资源类”列表中选择“系统资源”，并在“属性名称”列表中选择“NetBIOS 名称”     。  

        - 若要按组织单位 (OU) 名称来选择用户，请选择“资源类”  列表中的“用户资源”  ，以及“特性名称”  列表中的“用户 OU 名称”  。  

    - **排除标记为过时的资源**：如果某个客户端计算机被标记为已过时，则不会在搜索结果中包括此值。  

    - **排除未安装 Configuration Manager 客户端的资源**：这些资源不会显示在搜索结果中。  

    - **值**：输入要搜索所选属性名称的值。 使用百分比字符 (%) 作为通配符。 例如：  
        - 若要搜索 NetBIOS 名称以“M”开头的计算机，请在此字段中输入“M%”  。  
        - 例如，若要搜索 Contoso OU 中的用户，请在此字段中输入“Contoso”  。

2. 在“选择资源”  页上的“资源”  列表中，依次选择要添加到集合的资源和“下一步”  。  


### <a name="bkmk-query"></a>配置查询规则  

在“查询规则属性”  对话框中，指定以下信息。  

- **名称**：为查询指定唯一名称。  

- **导入查询语句**：打开“浏览查询”对话框  。 选择 [Configuration Manager 查询](/sccm/core/servers/manage/create-queries)用作集合的查询规则。   

- **资源类**：选择要搜索并添加到集合的资源的类型。 从“系统资源”  中选择值，以搜索从客户端计算机返回的清单数据；或从“未知计算机”  中选择值，以选择未知计算机返回的值。  

- **编辑查询语句**：打开“查询语句属性”  对话框，可以在其中编写用作集合规则的查询。 若要详细了解查询，请参阅[查询简介](/sccm/core/servers/manage/introduction-to-queries)。  


### <a name="bkmk-category"></a>设备类别规则

可以在“选择设备类别”  窗口中执行以下操作。

- **创建**：指定名称以新建类别。
- **重命名**：重命名选定类别。
- **删除**：选择一个或多个类别，并使用此操作将其从列表中删除。

有关详细信息，请参阅[自动将设备分类到集合](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)。<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a>配置包括集合规则  

在“选择集合”  对话框中，依次选择要添加到新集合的集合和“确定”  。  


### <a name="bkmk-exclude"></a>配置排除集合规则  

在“选择集合”  对话框中，依次选择要从新集合中排除的集合和“确定”  。  



## <a name="bkmk_import"></a>导入集合  

如果你从站点导出集合，Configuration Manager 将它另存为托管对象格式 (MOF) 文件。 使用此过程将该文件导入站点数据库。 必须对集合类拥有“创建”  权限，才能完成此过程。

> [!IMPORTANT]  
> - 请确保文件只包含集合数据、来自受信任的源且未遭篡改。  
> 
> - 请确保文件是从运行你使用的相同版本 Configuration Manager 的站点导出。  

有关导出集合的详细信息，请参阅 [如何管理集合](/sccm/core/clients/manage/collections/manage-collections)。


1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区。 选择“用户集合”  或“设备集合”  节点。  

2. 在功能区的“主页”  选项卡上，选择“创建”  组中的“导入集合”  。  

3. 在“导入集合向导”  的“常规”  页上，选择“下一步”  。  

4. 在“MOF 文件名”  页上，选择“浏览”  。 浏览到包含要导入的集合信息的 MOF 文件。  

5. 完成向导以导入集合。 新集合会显示在“资产和符合性”  工作区的“用户集合”  或“设备集合”  节点中。 刷新或重新加载 Configuration Manager 控制台才能查看新导入的集合的集合成员。  

## <a name="bkmk_aadcollsync"></a> 将集合成员资格结果同步到 Azure Active Directory 组
*（从版本 1906 开始，作为预发行功能引入）*
<!--3607475-->
> [!NOTE]
> 将集合成员身份同步到 Azure Active Directory (Azure AD) 组是首次在版本 1906 中引入的预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)一文。

可以将集合成员身份同步到 Azure Active Directory (Azure AD) 组。 借助此同步，可以通过基于集合成员身份结果创建 Azure AD 组成员身份来使用云中的现有本地分组规则。 可以同步设备集合。 只有具有 Azure Active Directory 记录的设备才会反映在 Azure AD 组中。 同时支持已联接混合 Azure AD 的设备和已联接 Azure Active Directory 的设备。

Azure AD 同步每五分钟执行一次。 这是一个单向过程，从 Configuration Manager 同步到 Azure AD。 Azure AD 中所做的更改不会反映在 Configuration Manager 集合中，但 Configuration Manager 不会将其覆盖。 例如，如果 Configuration Manager 集合有两台设备，并且 Azure AD 组有三台不同的设备，则在同步后，Azure AD 组有五个设备。


### <a name="prerequisites"></a>先决条件

- [云管理](/sccm/core/servers/deploy/configure/azure-services-wizard)
- [Azure Active Directory 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>在 Azure AD 中创建组和设置所有者

1. 转到 [https://portal.azure.com](https://portal.azure.com)。
1. 导航到“Azure Active Directory”   > “组”   > “所有组”  。
1. 单击“新建组”，然后键入“组名称”，并可以选择填写“组说明”    。
1. 确保已分配“成员身份类型”   。
1. 选择“所有者”，然后添加将在 Configuration Manager 中创建同步关系的标识  。
1. 单击“创建”  以完成创建 Azure AD 组。

### <a name="enable-collection-synchronization-for-the-azure-service"></a>为 Azure 服务启用集合同步

1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “Azure 服务”     。
1. 右键单击在其中创建了组的 Azure AD 租户，然后选择“属性”  。
1. 在“集合同步”  选项卡中，选中“启用 Azure 目录组同步”  对应的框。
1. 单击“确定”  以保存设置。

### <a name="enable-the-collection-to-synchronize"></a>启用集合以进行同步

1. 在 Configuration Manager 控制台中，转到“资产和符合性” > “概览” > “设备集合”    。
1. 右键单击要同步的集合，然后单击“属性”  。 
1. 在“AAD 组同步”  选项卡中，单击“添加”  。
1. 从下拉菜单中，选择在其中创建了 Azure AD 组的“租户”  。
1. 在“名称开头为”字段中键入搜索条件  ，然后单击“搜索”  。
  - 如果系统提示你登录，请使用指定为 Azure AD 组的所有者的标识。
1. 选择目标组，然后单击“确定”以添加该组并再次单击“确定”以退出集合的属性   。
1. 你将需要等待大约 5 到 7 分钟，然后才能验证 Azure 门户中的组成员身份。
   - 若要启动完全同步，请右键单击该集合，然后选择“同步成员身份”  。


### <a name="verify-the-azure-ad-group-membership"></a>验证 Azure AD 组成员身份

1. 转到 [https://portal.azure.com](https://portal.azure.com)。
1. 导航到“Azure Active Directory”   > “组”   > “所有组”  。
1. 查找你创建的组，然后选择“成员”  。 
1. 确认成员反映在 Configuration Manager 集合中。
   - 只有具有 Azure AD 标识的设备才会显示在该组中。


![将集合同步到 Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="bkmk_powershell"></a> 使用 PowerShell

可以使用 PowerShell 来创建和导入集合。 有关详情，请参阅：

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>后续步骤

[管理集合](/sccm/core/clients/manage/collections/manage-collections)
