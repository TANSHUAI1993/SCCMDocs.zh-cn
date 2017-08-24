---
title: "创建集合 | Microsoft Docs"
description: "在 System Center Configuration Manager 中创建集合以更轻松地管理用户和设备的分组。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44b4707b1a40624c51decf548d23ddd2164c5833
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建集合

*适用范围：System Center Configuration Manager (Current Branch)*

集合是用户组或设备组。 可使用集合执行任务，包括应用程序管理、部署符合性设置或安装软件更新。 还可以使用集合来管理客户端设置的组，或将它们与基于角色的管理结合使用来指定管理用户可以访问的资源。 Configuration Manager 包含几个内置集合。 有关详细信息，请参阅 [System Center Configuration Manager 中的集合简介](../../../../core/clients/manage/collections/introduction-to-collections.md)。  

> [!NOTE]  
>  集合可以包含用户或设备，但不能同时包含两者。  

 下表列出了可用于在 Configuration Manager 中配置集合的成员的规则。  

|成员身份规则类型|更多信息|  
|--------------------------|----------------------|  
|直接规则|用于选择要添加到集合的用户或计算机。 除非从 Configuration Manager 中删除资源，否则此成员身份不会更改。 Configuration Manager 必须已发现资源，否则则必须先导入资源，才能将资源添加到直接规则集合。 直接规则集合的管理开销高于查询规则集合，因为前者需要手动更改。|  
|查询规则|基于 Configuration Manager 按计划运行的查询来动态更新集合的成员身份。 例如，可以创建一个用户集合，其中的用户是 Active Directory 域服务中的人力资源组织单位的成员。 此集合会在向人力资源组织单位添加新用户或从中删除用户时自动更新。<br /><br /> 有关可用于构建集合的示例查询，请参阅[如何在 System Center Configuration Manager 中创建查询](../../../../core/servers/manage/create-queries.md)。|  
|包括集合规则|在 Configuration Manager 集合中包括其他集合的成员。如果所包括的集合有所更改，则当前集合的成员身份会按计划进行更新。<br /><br /> 可以向集合添加多个包括集合规则。<br /> |  
|排除集合规则|通过排除集合规则，可以从一个 Configuration Manager 集合中排除其他集合的成员。 如果排除的集合有所更改，则当前集合的成员身份会按计划进行更新。<br /><br /> 可以向集合添加多个排除集合规则。 如果集合同时包含集合和排除集合规则，并且存在冲突，则排除集合规则具有优先级。<br />              **示例：** 创建一个集合，它具有一个包括集合规则和一个排除集合规则。 包括集合规则用于 Dell 台式机的集合。 排除集合用于具有 4 GB 以下 RAM 的计算机的集合。 新集合将包含至少具有 4 GB RAM 的 Dell 台式机。|  

 使用以下过程有助于在 Configuration Manager 中创建集合。 还可以导入在此 Configuration Manager 站点或其他 Configuration Manager 站点上创建的集合。 有关如何导出和导入集合的信息，请参阅[如何在 System Center Configuration Manager 中管理集合](../../../../core/clients/manage/collections/manage-collections.md)。  

 有关为运行 Linux 和 UNIX 的计算机创建集合的信息，请参阅 [How to manage clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)（如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 服务器的客户端）。  

##  <a name="BKMK_1"></a> 若要创建设备集合  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “设备集合”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建设备集合”。  

4.  在“常规”页面上，提供“名称”和“注释”。 然后在“限定集合”中，选择“浏览”以选择限定集合。 集合将仅包含来自限定集合的成员。  

5.  在“创建设备集合向导”的“成员身份规则”页上的“添加规则”列表中，选择想用于此集合的成员身份规则的类型。 可以为每个集合配置多个规则。  

        
##### <a name="to-configure-a-direct-rule"></a>若要配置直接规则  

1.  在“创建直接成员身份规则向导”  的“搜索资源” 页上，指定以下信息：  

-   **资源类**：选择要搜索并添加到集合的资源的类型。 从“系统资源”  值进行选择以搜索从客户端计算机返回的清单数据，或从“未知计算机”  进行选择以选择未知计算机返回的值。  

-   **属性名称**：选择与要搜索的所选资源类关联的属性。 例如，如果要按其 NetBIOS 名称来选择计算机，则在“资源类”  列表中选择“系统资源”  ，并在“属性名称”  列表中选择“NetBIOS 名称”  。  

-   **排除标记为已过时的资源** - 如果某个客户端计算机被标记为已过时，则不会在搜索结果中包括此值。  

-   **排除未安装 Configuration Manager 客户端的资源** - 这些资源不会显示在搜索结果中。  

-   **值** ：输入你要在所选属性名称搜索的值。 可以使用百分比字符 **%** 作为通配符。 例如，若要搜索 NetBIOS 名称以“M”开头的计算机，请在此字段中输入“M%”。  

2.  在“选择资源”页上，在“资源”列表中选择要添加到集合的资源，然后选择“下一步”。  


##### <a name="to-configure-a-query-rule"></a>若要配置查询规则  

1.  在“查询规则属性”  对话框中，指定以下信息：  

-   “名称”：指定唯一名称。  

-   **导入查询语句** - 打开“浏览查询”对话框，在其中可以选择要用作集合的查询规则的 [Configuration Manager 查询](../../../../core/servers/manage/create-queries.md)。   

-   **资源类：**选择要搜索并添加到集合的资源的类型。 从“系统资源”  值中选择值以搜索从客户端计算机返回的清单数据，或从“未知计算机”  进行选择以选择未知计算机返回的值。  

-   **编辑查询语句** - 打开“查询语句属性”对话框，在其中可以创作要用作集合的规则的查询。 有关查询的详细信息，请参阅 [System Center Configuration Manager 的查询技术参考](../../../../core/servers/manage/queries-technical-reference.md)。  

    
##### <a name="to-configure-an-include-collection-rule"></a>若要配置包括集合规则  

在“选择集合”对话框中，选择要包括在新集合中的集合，然后选择“确定”。  

##### <a name="to-configure-an-exclude-collection-rule"></a>若要配置排除集合规则  

在“选择集合”对话框中，选择要从新集合中排除的集合，然后选择“确定”。  

-   **对此集合使用增量更新** - 选择此选项可定期从以前的集合评估中只扫描新资源或更改的资源，而与完全集合评估无关。 增量更新按 10 分钟间隔进行。  

> [!IMPORTANT]  
>  借助使用以下类的查询规则配置的集合不支持增量更新：  
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

-   **对此集合计划完全更新** - 选择集合成员身份的定期完全评估。  

6.  完成向导以创建新集合。 新集合会显示在“资产和符合性”  工作区的“设备集合”  节点中。  

> [!NOTE]  
>  必须刷新或重新加载 Configuration Manager 控制台才能查看集合成员。 但是，直到进行首次计划更新，或是如果为集合手动选择“更新成员身份”之后，成员才会出现在集合中。 可能需要几分钟时间才能完成集合更新。  

##  <a name="BKMK_2"></a> 若要创建用户集合  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “用户集合”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建用户集合”。  

4.  在向导的“常规”页面上，提供“名称”和“注释”。 然后在“限定集合”中，选择“浏览”以选择限定集合。 集合将仅包含来自限定集合的成员。  

5.  在“成员身份规则”页上，指定以下内容：  

    -   在“添加规则”  列表中，选择要用于此集合的成员身份规则的类型。 可以为每个集合配置多个规则。  

##### <a name="to-configure-a-direct-rule"></a>若要配置直接规则  

1.  在“创建直接成员身份规则向导”的“搜索资源”页上，指定：  

-   **资源类**：选择要搜索并添加到集合的资源的类型。 从“用户资源”值中进行选择以搜索 Configuration Manager 收集的用户信息，或从“用户组资源”中进行选择以搜索 Configuration Manager 收集的用户组信息。  

-   **属性名称**：选择与要搜索的资源类关联的属性。 例如，如果要按其组织单位 (OU) 名称来选择用户，则在“资源类”  列表中选择“用户资源”  ，并在“属性名称”  列表中选择“用户组织单位名称”  。  

-   **值：**输入想要搜索的值。 可以使用百分比字符 **%** 作为通配符。 例如，如果要搜索 Contoso OU 中的用户，请在此字段中输入“Contoso”。  

2.  在“选择资源”页上，在“资源”列表中选择要添加到集合的资源。  

##### <a name="to-configure-a-query-rule"></a>若要配置查询规则  

1.  在“查询规则属性”对话框中，提供：  

-   **名称**：唯一名称。  

-   **导入查询语句** - 打开“浏览查询”对话框，在其中可以选择要用作集合的查询规则的 [Configuration Manager 查询](../../../../core/servers/manage/queries-technical-reference.md)。  

-   **资源类**：选择要搜索并添加到集合的资源的类型。 从“用户资源”值中进行选择以搜索 Configuration Manager 收集的用户信息，或从“用户组资源”中进行选择以搜索 Configuration Manager 收集的用户组信息。  

-   **编辑查询语句** - 打开“查询语句属性”对话框，在其中可以[创作查询](../../../../core/servers/manage/queries-technical-reference.md)以将其用作集合的规则。  

##### <a name="to-configure-an-include-collection-rule"></a>若要配置包括集合规则  

在“选择集合”对话框中，选择要包括在新集合中的集合，然后选择“确定”。  

##### <a name="to-configure-an-exclude-collection-rule"></a>若要配置排除集合规则  

在“选择集合”对话框中，选择要从新集合中排除的集合，然后选择“确定”。  


-   **对此集合使用增量更新** - 选择此选项可定期从以前的集合评估中只扫描新资源或更改的资源，而与完全集合评估无关。 增量更新按 10 分钟间隔进行。  

> [!IMPORTANT]  
>  借助使用以下类的查询规则配置的集合不支持增量更新：  
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

-   **对此集合计划完全更新** - 选择集合成员身份的定期完全评估。  

6.  完成向导。 新集合会显示在“资产和符合性”  工作区的“用户集合”  节点中。  

> [!NOTE]  
>  必须刷新或重新加载 Configuration Manager 控制台才能查看集合成员。 但是，直到进行首次计划更新，或是你为集合手动选择“更新成员身份”  之后，成员才会出现在集合中。 可能需要几分钟时间才能完成集合更新。  

##  <a name="BKMK_3"></a> 若要导入集合  

1.  在 Configuration Manager 控制台中，依次选择“资产和符合性” > “用户集合”或“设备集合”。  

3.  在“主页”选项卡上的“创建”组中，选择“导入集合”。  

4.  在“导入集合向导” 的“常规”页上，选择“下一步”。  

5.  在“MOF 文件名”页上，选择“浏览”，然后浏览到包含要导入的集合信息的 MOF 文件。  

    > [!NOTE]  
    >  要导入的文件必须已从运行与此相同的 Configuration Manager 版本的站点导出。 有关导出集合的详细信息，请参阅[如何在 System Center Configuration Manager 中管理集合](../../../../core/clients/manage/collections/manage-collections.md)。  

6.  完成向导以导入集合。 新集合会显示在“资产和符合性”  工作区的“用户集合”  或“设备集合”  节点中。 刷新或重新加载 Configuration Manager 控制台才能查看新导入的集合的集合成员。  
