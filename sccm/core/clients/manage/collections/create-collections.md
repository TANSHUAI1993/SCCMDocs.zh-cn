---
title: 创建集合
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中创建集合以更轻松地管理用户和设备的分组。
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e79ec4b19ad45c49438ef273bcaf031754cf7e7
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558127"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>如何在 Configuration Manager 中创建集合

适用范围：System Center Configuration Manager (Current Branch)

集合是用户组或设备组。 可使用集合执行任务，包括应用程序管理、部署符合性设置或安装软件更新。 还可以使用集合来管理客户端设置的组，或将它们与基于角色的管理结合使用来指定管理用户可以访问的资源。 Configuration Manager 包含几个内置集合。 有关详细信息，请参阅[集合简介](/sccm/core/clients/manage/collections/introduction-to-collections)。  

> [!NOTE]  
> 集合可以包含用户或设备，但不能同时包含两者。  


本文指导如何在 Configuration Manager 中创建集合。 还可以导入在此 Configuration Manager 站点或其他 Configuration Manager 站点上创建的集合。 有关如何导出和导入集合的详细信息，请参阅[如何管理集合](/sccm/core/clients/manage/collections/manage-collections)。  



## <a name="collection-rules"></a>集合规则

可以使用不同的规则在 Configuration Manager 中配置集合的成员。  


### <a name="direct-rule"></a>直接规则

用于选择要添加到集合的用户或计算机。 除非从 Configuration Manager 中删除资源，否则此成员身份不会更改。 在将资源添加到直接规则集合之前，Configuration Manager 必须已发现资源，否则必须先导入资源。 直接规则集合的管理开销高于查询规则集合，因为前者需要手动更改。


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

通过排除集合规则，可以从一个 Configuration Manager 集合中排除其他集合的成员。 如果排除的集合发生更改，Configuration Manager 会按计划更新当前集合的成员身份。

可以向集合添加多个排除集合规则。 如果集合同时包含包括集合和排除集合规则，并且存在冲突，则排除集合规则优先级较高。

#### <a name="example"></a>示例
创建一个集合，它具有一个包括集合规则和一个排除集合规则。 包括集合规则用于 Dell 台式机的集合。 排除集合用于具有 4 GB 以下 RAM 的计算机的集合。 新集合将包含至少具有 4 GB RAM 的 Dell 台式机。



## <a name="bkmk_create"></a>创建集合  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区。  

    - 要创建设备集合，请选择“设备集合”节点。 然后，在功能区的“主页”选项卡上的“创建”组中，选择“创建设备集合”。  

    - 要创建用户集合，请选择“用户集合”节点。 然后，在功能区的“主页”选项卡上的“创建”组中，选择“创建用户集合”。  

2. 在向导的“常规”页上，提供“名称”和“注释”。 在“限定集合”部分，选择“浏览”并选择限定集合。 所创建的集合只包含来自限定集合的成员。  

4. 在“成员身份规则”页上的“添加规则”列表中，选择要用于此集合的成员身份规则的类型。 可以为每个集合配置多个规则。 每个规则的配置各不相同。 有关配置每个规则的详细信息，请参阅以下各部分：  
    - [直接规则](#bkmk-direct)
    - [查询规则](#bkmk-query)
    - [设备类别规则](#bkmk-category)
    - [包括集合规则](#bkmk-include)
    - [排除集合规则](#bkmk-exclude)

5. 同样，在“成员身份规则”页上，查看以下设置：

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

        从 1810 版开始，集合评估行为中的以下更改可改进站点性能：<!--3607726-->  

        - 以前，在基于查询的集合上配置计划时，站点将继续评估查询，无论你是否启用了“在此集合上计划完全更新”的集合设置。 若要完全禁用计划，必须将计划更改为“无”。 

            现在，当你禁用此设置时，站点将清除计划。 若要指定对计划进行集合评估，请启用“在此集合上计划完全更新”的选项。  

            在更新站点时，对于在其中指定计划的任何现有集合，站点将启用“在此集合上计划完全更新”的选项。 虽然此配置可能并非你所愿，但它是实际行为。 若要停止在计划上评估集合的站点，请禁用此选项。  

        - 你无法禁用“所有系统”等内置集合的评估，但现在可以配置计划。 此行为使你能够在满足需求的同时自定义此操作。 

            > [!Tip]  
            > 只会更改内置集合上的自定义计划的时间。 不会更改定期模式。 未来迭代可能会强制实施特定定期模式。  

6. 完成向导以创建新集合。 新集合会显示在“资产和符合性”  工作区的“设备集合”  节点中。  

> [!NOTE]  
> 必须刷新或重新加载 Configuration Manager 控制台才能查看集合成员。 直到第一次计划更新后，它们才会出现在集合中。 也可以手动为集合选择“更新成员资格”。 可能需要几分钟时间才能完成集合更新。  

        
### <a name="bkmk-direct"></a>配置直接规则  

1. 在“创建直接成员身份规则向导”  的“搜索资源” 页上，指定以下信息：  

    - **资源类**：选择要搜索并添加到集合的资源的类型。 例如， 
        - **系统资源**：搜索从客户端计算机返回的库存数据
        - **未知计算机**：从未知计算机返回的值中进行选择
        - **用户资源**：搜索 Configuration Manager 收集的用户信息
        - **用户组资源**：搜索 Configuration Manager 收集的用户组信息

    - **属性名称**：选择与要搜索的所选资源类关联的属性。 例如，  

        - 如果要按其 NetBIOS 名称来选择计算机，则在“资源类”列表中选择“系统资源”，并在“属性名称”列表中选择“NetBIOS 名称”。  

        - 如果要按其组织单位 (OU) 名称来选择用户，则在“资源类”列表中选择“用户资源”，并在“属性名称”列表中选择“用户组织单位名称”。  

    - **排除标记为过时的资源**：如果某个客户端计算机被标记为已过时，则不会在搜索结果中包括此值。  

    - **排除未安装 Configuration Manager 客户端的资源**：这些资源不会显示在搜索结果中。  

    - **值**：输入要搜索所选属性名称的值。 使用百分比字符 `%` 作为通配符。 例如，  
        - 若要搜索 NetBIOS 名称以“M”开头的计算机，请在此字段中输入 `M%`。  
        - 若要搜索 Contoso OU 中的用户，请在此字段中输入 `Contoso`。

2. 在“选择资源”页上，在“资源”列表中选择要添加到集合的资源，然后选择“下一步”。  


### <a name="bkmk-query"></a>配置查询规则  

在“查询规则属性”  对话框中，指定以下信息：  

- **名称**：为查询指定唯一名称。  

- **导入查询语句**：打开“浏览查询”对话框。 选择 [Configuration Manager 查询](/sccm/core/servers/manage/create-queries)用作集合的查询规则。   

- **资源类**：选择要搜索并添加到集合的资源的类型。 从“系统资源”  值中选择值以搜索从客户端计算机返回的清单数据，或从“未知计算机”  进行选择以选择未知计算机返回的值。  

- **编辑查询语句**：打开“查询语句属性”对话框，在其中可以创作查询以将其用作集合的规则。 有关查询的详细信息，请参阅[查询技术参考](/sccm/core/servers/manage/queries-technical-reference)。  


### <a name="bkmk-category"></a>设备类别规则

“选择设备类别”窗口中提供了以下操作：

- **创建**：指定名称以创建新类别
- **重命名**：为所选类别重命名
- **删除**：选择一个或多个类别，然后使用此操作将其从列表中删除

有关详细信息，请参阅[自动将设备分类到集合](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)。<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a>配置包括集合规则  

在“选择集合”对话框中，选择要包括在新集合中的集合，然后选择“确定”。  


### <a name="bkmk-exclude"></a>配置排除集合规则  

在“选择集合”对话框中，选择要从新集合中排除的集合，然后选择“确定”。  



## <a name="bkmk_import"></a>导入集合  

从站点导出集合时，Configuration Manager 将其另存为托管对象格式 (MOF) 文件。 使用此过程将该文件导入站点数据库。 需要集合类的创建权限。 

> [!Important]  
> - 请确保该文件仅包含集合数据、来自受信任的源且未被篡改。  
> 
> - 请确保该文件是从运行相同版本的 Configuration Manager 的站点导出的。  

有关导出集合的详细信息，请参阅 [如何管理集合](/sccm/core/clients/manage/collections/manage-collections)。


1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区。 选择“用户集合”或“设备集合”节点。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“导入集合”。  

3. 在“导入集合向导” 的“常规”页上，选择“下一步”。  

4. 在“MOF 文件名”页上，选择“浏览”。 浏览到包含要导入的集合信息的 MOF 文件。  

5. 完成向导以导入集合。 新集合会显示在“资产和符合性”  工作区的“用户集合”  或“设备集合”  节点中。 刷新或重新加载 Configuration Manager 控制台才能查看新导入的集合的集合成员。  

