---
title: "创建集合 | System Center Configuration Manager"
description: "在 System Center Configuration Manager 中创建集合以更轻松地管理用户和设备的分组。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f73f0e58b82d1aab1f64f3695dd5c3a61e933d2a


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建集合

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中创建集合以表示用户或设备的逻辑分组。 可以使用集合来帮助执行许多任务，包括应用程序管理、部署符合性设置或安装软件更新。 还可以使用集合来管理客户端设置的组，或将它们与基于角色的管理结合使用来指定管理用户可以访问的资源。 Configuration Manager 包含几个内置集合。 有关详细信息，请参阅 [System Center Configuration Manager 中的集合简介](../../../../core/clients/manage/collections/introduction-to-collections.md)。  

> [!NOTE]  
>  单个集合可以包含用户或设备，但不能同时包含两者。  

 下表列出了可用于在 Configuration Manager 中配置集合的成员的规则。  

|成员身份规则类型|更多信息|  
|--------------------------|----------------------|  
|直接规则|直接规则使你可以选择要作为成员添加到集合的用户或计算机。 此规则使你可以直接控制哪些资源是集合的成员。 除非从 Configuration Manager 中删除资源，否则此成员身份不会更改。 Configuration Manager 必须已发现资源，否则则必须先导入资源，才能将资源添加到直接规则集合。 直接规则集合的管理开销高于查询规则集合，因为你必须手动对此集合类型进行更改。|  
|查询规则|查询规则基于 Configuration Manager 按计划运行的查询来动态更新集合的成员身份。 例如，可以创建一个用户集合，其中的用户是 Active Directory 域服务中的人力资源组织单位的成员。 与直接规则集合不同，此集合成员身份会在向人力资源组织单位添加新用户或从中删除用户时自动更新。<br /><br /> 有关可用于构建集合的示例查询，请参阅[如何在 System Center Configuration Manager 中创建查询](../../../../core/servers/manage/create-queries.md)。|  
|包括集合规则|通过包括集合规则，可以在一个 Configuration Manager 集合中包括其他集合的成员。如果所包括的集合的成员身份有所更改，则当前集合的成员身份会按计划进行更新。<br /><br /> 可以向集合添加多个包括集合规则。<br />              **示例：** 创建一个具有两个包括集合规则的集合。 第一个包括集合规则用于便携式计算机的集合，第二个包括集合规则用于台式机的集合。 新集合会包含便携式计算机集合和台式机集合中的所有成员。|  
|排除集合规则|通过排除集合规则，可以从一个 Configuration Manager 集合中排除其他集合的成员。 如果排除的集合的成员身份更改，当前集合的成员身份会按计划进行更新。<br /><br /> 可以向集合添加多个排除集合规则。 如果集合同时包含包括集合和排除集合规则，并且存在冲突，则排除集合规则优先于包括集合规则。<br />              **示例：** 创建一个集合，它具有一个包括集合规则和一个排除集合规则。 包括集合规则用于 Dell 台式机的集合。 排除集合用于具有 4 GB 以下 RAM 的计算机的集合。 新集合将包含至少具有 4 GB RAM 的 Dell 台式机。|  

 使用以下过程有助于在 Configuration Manager 中创建集合。 还可以导入在此 Configuration Manager 站点或其他 Configuration Manager 站点上创建的集合。 有关如何导出集合的信息，请参阅[如何在 System Center Configuration Manager 中管理集合](../../../../core/clients/manage/collections/manage-collections.md)。  

 有关为运行 Linux 和 UNIX 的计算机创建集合的信息，请参阅 [How to manage clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)（如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 服务器的客户端）。  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> 创建设备集合  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“设备集合” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建设备集合” 。  

4.  在“创建设备集合向导”  的“常规” 页上，指定以下信息：  

    -   **名称**：为集合指定唯一名称。  

    -   **备注**：为集合指定描述。  

    -   **限定集合**：单击“浏览”  可选择限定集合。 所创建的集合只包含来自限定集合的成员。  

5.  在“成员身份规则”  的“常规” 页上，指定以下信息：  

    -   在“添加规则”  列表中，选择要用于此集合的成员身份规则的类型。 可以为每个集合配置多个规则。  

         使用以下过程可配置每种成员身份规则类型。  

        ##### <a name="to-configure-a-direct-rule"></a>若要配置直接规则  

        1.  在“创建直接成员身份规则向导”  的“搜索资源” 页上，指定以下信息：  

            -   **资源类**：在列表中，选择你要搜索并添加到集合的资源的类型。 从“系统资源”  值进行选择以搜索从客户端计算机返回的清单数据，或从“未知计算机”  进行选择以选择未知计算机返回的值。  

            -   **属性名称**：在列表中，选择与要搜索的所选资源类关联的属性。 例如，如果要按其 NetBIOS 名称来选择计算机，则在“资源类”  列表中选择“系统资源”  ，并在“属性名称”  列表中选择“NetBIOS 名称”  。  

            -   **排除标记为已过时的资源** - 如果某个客户端计算机被标记为已过时，则不会在搜索结果中包括此值。  

            -   **排除未安装 Configuration Manager 客户端的资源** - 如果搜索结果包括未安装 Configuration Manager 客户端的资源，则此值将不会显示在搜索结果中。  

            -   **值** ：输入你要在所选属性名称搜索的值。 可以使用百分比字符 **%** 作为通配符。 例如，如果要搜索 NetBIOS 名称以“M”开头的计算机，请在此字段中输入 **M%**。  

        2.  在“创建直接成员身份规则向导”  的“选择资源” 页上，在“资源”  列表中选择要添加到集合的资源，然后单击“下一步” 。  

        3.  完成“创建直接成员身份规则向导” 。  

        ##### <a name="to-configure-a-query-rule"></a>若要配置查询规则  

        1.  在“查询规则属性”  对话框中，指定以下信息：  

            -   **名称**：为查询规则指定唯一名称。  

            -   **导入查询语句** - 打开“浏览查询”对话框，在其中可以选择要用作集合的查询规则的 Configuration Manager 查询。 有关如何创建这些查询和一些示例，请参阅[如何在 System Center Configuration Manager 中创建查询](../../../../core/servers/manage/create-queries.md)。  

            -   **资源类** ：在列表中，选择你要搜索并添加到集合的资源的类型。 从“系统资源”  值中选择值以搜索从客户端计算机返回的清单数据，或从“未知计算机”  进行选择以选择未知计算机返回的值。  

            -   **编辑查询语句** - 打开“查询语句属性”对话框，在其中可以创作要用作集合的规则的查询。 有关查询的详细信息，请参阅 [System Center Configuration Manager 的查询技术参考](../../../../core/servers/manage/queries-technical-reference.md)。  

        2.  单击“确定”  以关闭“查询规则属性”  对话框并保存查询成员身份规则。  

        ##### <a name="to-configure-an-include-collection-rule"></a>若要配置包括集合规则  

        1.  在“选择集合”  对话框框中，选择你要包括在新集合中的集合。  

        2.  单击“确定”  以关闭“选择集合”  对话框并保存包括成员身份规则。  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>若要配置排除集合规则  

        1.  在“选择集合”  对话框框中，选择你要从新集合中排除的集合。  

        2.  单击“确定”  以关闭“选择集合”  对话框并保存排除成员身份规则。  

    -   **对此集合使用增量更新** - 选择此选项可定期从以前的集合评估中只扫描新资源或更改的资源，并且只使用这些资源更新集合成员身份，而与完全集合评估无关。 增量更新按 10 分钟间隔进行。  

        > [!IMPORTANT]  
        >  借助使用以下类的查询规则配置的集合不支持增量更新：  
        >   
        >  -   SMS_G_System_CollectedFile  
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

    -   **对此集合计划完全更新** - 选择此选项可计划集合成员身份的定期完全评估。  

6.  完成向导以创建新集合。 新集合会显示在“资产和符合性”  工作区的“设备集合”  节点中。  

> [!NOTE]  
>  必须刷新或重新加载 Configuration Manager 控制台才能查看集合成员。 但是，直到进行首次计划更新，或是你为集合手动选择“更新成员身份”  之后，成员才会出现在集合中。 根据集合规则的复杂性和 Configuration Manager 数据库中的条目数，集合更新可能需要几分钟才能完成。  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> 创建用户集合  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“用户集合” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建用户集合” 。  

4.  在“创建用户集合向导”  的“常规” 页上，指定以下信息：  

    -   **名称**：为集合指定唯一名称。  

    -   **备注**：为集合指定描述。  

    -   **限定集合**：单击“浏览”  可选择限定集合。 所创建的集合只包含来自限定集合的成员。  

5.  在“创建用户集合向导”  的“成员身份规则” 页上，指定以下信息：  

    -   在“添加规则”  列表中，选择要用于此集合的成员身份规则的类型。 可以为每个集合配置多个规则。  

         使用以下过程可配置每种成员身份规则类型。  

        ##### <a name="to-configure-a-direct-rule"></a>若要配置直接规则  

        1.  在“创建直接成员身份规则向导”  的“搜索资源” 页上，指定以下信息：  

            -   **资源类**：在列表中，选择你要搜索并添加到集合的资源的类型。 从“用户资源”值中进行选择以搜索 Configuration Manager 收集的用户信息，或从“用户组资源”中进行选择以搜索 Configuration Manager 收集的用户组信息。  

            -   **属性名称**：在列表中，选择与要搜索的所选资源类关联的属性。 例如，如果要按其组织单位 (OU) 名称来选择用户，则在“资源类”  列表中选择“用户资源”  ，并在“属性名称”  列表中选择“用户组织单位名称”  。  

            -   **值** ：输入你要在所选属性名称中搜索的值。 可以使用百分比字符 **%** 作为通配符。 例如，如果要搜索 Contoso OU 中的用户，请在此字段中输入 **Contoso** 。  

        2.  在“创建直接成员身份规则向导”  的“选择资源” 页上，在“资源”  列表中选择要添加到集合的资源，然后单击“下一步” 。  

        3.  完成“创建直接成员身份规则向导” 。  

        ##### <a name="to-configure-a-query-rule"></a>若要配置查询规则  

        1.  在“查询规则属性”  对话框中，指定以下信息：  

            -   **名称**：为查询规则指定唯一名称。  

            -   **导入查询语句** - 打开“浏览查询”对话框，在其中可以选择要用作集合的查询规则的 Configuration Manager 查询。 有关查询的详细信息，请参阅 [System Center Configuration Manager 的查询技术参考](../../../../core/servers/manage/queries-technical-reference.md)。  

            -   **资源类**：在列表中，选择你要搜索并添加到集合的资源的类型。 从“用户资源”值中进行选择以搜索 Configuration Manager 收集的用户信息，或从“用户组资源”中进行选择以搜索 Configuration Manager 收集的用户组信息。  

            -   **编辑查询语句** - 打开“查询语句属性”对话框，在其中可以创作要用作集合的规则的查询。 有关查询的详细信息，请参阅 [System Center Configuration Manager 的查询技术参考](../../../../core/servers/manage/queries-technical-reference.md)。  

        2.  单击“确定”  以关闭“查询规则属性”  对话框并保存查询成员身份规则。  

        ##### <a name="to-configure-an-include-collection-rule"></a>若要配置包括集合规则  

        1.  在“选择集合”  对话框框中，选择你要包括在新集合中的集合。  

        2.  单击“确定”  以关闭“选择集合”  对话框并保存包括成员身份规则。  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>若要配置排除集合规则  

        1.  在“选择集合”  对话框框中，选择你要从新集合中排除的集合。  

        2.  单击“确定”  以关闭“选择集合”  对话框并保存排除成员身份规则。  

    -   **对此集合使用增量更新** - 选择此选项可定期从以前的集合评估中只扫描新资源或更改的资源，并且只使用这些资源更新集合成员身份，而与完全集合评估无关。 增量更新按 10 分钟间隔进行。  

        > [!IMPORTANT]  
        >  借助使用以下类的查询规则配置的集合不支持增量更新：  
        >   
        >  -   SMS_G_System_CollectedFile  
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

    -   **对此集合计划完全更新** - 选择此选项可计划集合成员身份的定期完全评估。  

6.  完成向导以创建新集合。 新集合会显示在“资产和符合性”  工作区的“用户集合”  节点中。  

> [!NOTE]  
>  必须刷新或重新加载 Configuration Manager 控制台才能查看集合成员。 但是，直到进行首次计划更新，或是你为集合手动选择“更新成员身份”  之后，成员才会出现在集合中。 根据集合规则的复杂性和 Configuration Manager 数据库中的条目数，集合更新可能需要几分钟才能完成。  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> 导入集合  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“用户集合”  或“设备集合” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“导入集合” 。  

4.  在“导入集合向导”  的“常规” 页上，单击“下一步” 。  

5.  在“MOF 文件名”  页上，单击“浏览”  ，然后浏览到包含要导入的集合信息的 MOF 文件。  

    > [!NOTE]  
    >  要导入的文件必须已从运行与此相同的 Configuration Manager 版本的站点导出。 有关导出集合的详细信息，请参阅[如何在 System Center Configuration Manager 中管理集合](../../../../core/clients/manage/collections/manage-collections.md)。  

6.  完成向导以导入集合。 新集合会显示在“资产和符合性”  工作区的“用户集合”  或“设备集合”  节点中。  

> [!NOTE]  
>  必须刷新或重新加载 Configuration Manager 控制台才能查看新导入的集合的集合成员。  



<!--HONumber=Nov16_HO1-->


