---
title: "创建远程连接配置文件 | Microsoft Docs"
description: "使用 System Center Configuration Manager 远程连接配置文件使用户可以远程连接到工作计算机。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 72fc94c6449649656a7e8b81659c2b5cc2551107
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的远程连接配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 远程连接配置文件，允许用户在未连接到域时或者其个人计算机通过 Internet 连接时以远程方式连接到工作计算机。  

 用户可以从以下设备类型连接到其工作电脑：  

-   运行 Microsoft Windows 的计算机  

-   运行 iOS 的设备  

-   运行 Android 的设备  

利用远程连接配置文件，你可以将远程桌面连接设置部署到 Configuration Manager 层次结构中的用户。 用户随后可使用公司门户，利用公司门户提供的远程桌面连接设置通过远程桌面访问他们的任何主要工作计算机。  

如果你希望用户使用公司门户连接到其工作电脑，则需要 Microsoft Intune。 如果你未使用 Intune，用户仍然能够使用远程连接配置文件中的信息，通过 VPN 连接使用远程桌面连接到其工作电脑。  

> [!IMPORTANT]  
>  当你使用 Configuration Manager 控制台指定远程连接配置文件设置时，这些设置将存储在客户端计算机的本地策略中。 这些设置可能会替代另一个应用程序配置的远程桌面设置。 此外，如果你使用 Windows 组策略配置远程桌面设置，则组策略中指定的设置将会替代使用 Configuration Manager 配置的设置。  

 在安装 Configuration Manager 时，将创建“远程电脑连接”新安全组。 当部署远程连接配置文件（其中包括你向其中部署配置文件的计算机的主要用户）时，将填充此组。 尽管本地管理员可向此组中添加用户名，但在下次评估已部署远程连接配置文件的符合性时，会将这些用户从组中删除。  

 如果你向此组中手动添加用户，用户可以启动远程连接，但不会在公司门户中发布连接信息。  

 如果你从组中手动删除 Configuration Manager 已添加的用户，Configuration Manager 将通过在下次评估远程连接配置文件的符合性时重新添加该用户来自动修正此更改。  

> [!IMPORTANT]  
>  如果用户和设备之间的用户设备相关性发生更改（例如，用户连接到的计算机不再是用户的主要设备），Configuration Manager 将禁用远程连接配置文件和 Windows 防火墙设置以防止连接到该计算机。  

## <a name="prerequisites"></a>先决条件  

### <a name="external-dependencies"></a>外部依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|远程桌面网关服务器。|如果要允许用户从公司域的外部在 Internet 上连接，你必须安装和配置远程桌面网关服务器。<br /><br /> 如果远程桌面或终端服务设置由另一个应用程序或组策略设置管理，远程连接配置文件可能无法正常工作。 当你通过 Configuration Manager 控制台部署远程连接配置文件时，其设置将存储在客户端计算机的本地策略中。 这些设置可能会替代另一个应用程序配置的远程桌面设置。 此外，如果你使用组策略设置来配置远程桌面设置，则组策略设置中指定的设置将会替代 Configuration Manager 配置的设置。<br /><br /> 有关如何安装和配置远程桌面网关服务器的详细信息，请参阅 Windows Server 文档。|  
|如果客户端计算机运行基于主机的防火墙，该防火墙必须启用 Mstsc.exe 程序。|在配置远程连接配置文件时，你必须启用“对 Windows 域和专用网络上的连接允许 Windows 防火墙例外”  设置。 启用了此设置后，Configuration Manager 将自动配置 Windows 防火墙以启用 Mstsc.exe 程序。 但是，如果客户端计算机运行其他基于主机的防火墙，你必须手动配置此防火墙依赖关系。<br /><br /> 用于配置 Windows 防火墙的组策略设置可能会覆盖在 Configuration Manager 中设置的配置。 如果使用组策略来配置 Windows 防火墙，请确保组策略设置不会阻止 Mstsc.exe 程序。|  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|Configuration Manager 连接到 Microsoft Intune（称为混合配置）。|有关将 Configuration Manager 连接到 Microsoft Intune 的详细信息，请参阅“使用 Configuration Manager 和 Microsoft Intune 管理移动设备”。|  
|为了使用户连接到公司网络上的工作计算机，该计算机必须是用户的主设备。|有关用户设备相关性的详细信息，请参阅[将用户和设备同用户设备相关性相链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。|  
|必须授予特定的安全权限来管理远程连接配置文件。|“符合性设置管理员”  安全角色包括管理远程连接配置文件所需的权限。 有关详细信息，请参阅 <br />[配置基于角色的管理](/sccm/core/servers/deploy/configure/configure-role-based-administration)。|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>远程连接配置文件的安全和隐私注意事项  

### <a name="security-considerations"></a>安全注意事项  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|手动指定用户设备相关性，而不是允许用户确定其主设备。 此外，不要启用基于使用情况的配置。|由于你必须启用“允许工作计算机的所有主要用户进行远程连接”  然后才能部署远程连接配置文件，因此请始终手动指定用户设备相关性。 不考虑从用户或从极可信赖的设备中收集的信息。 如果部署远程连接配置文件，并且受信任的管理用户未指定用户设备相关性，则未授权用户可能会收到提升的权限，然后能够远程连接到计算机。<br /><br /> 如果确实启用基于使用情况的配置，则会通过未受 Configuration Manager 保护的状态消息收集此信息。 为了帮助减轻此威胁，请在客户端计算机和管理点之间使用服务器消息块 (SMB) 签名或 Internet 协议安全性 (IPsec)。|  
|限制站点服务器计算机上的本地管理员权限。|在站点服务器上具有本地管理权限的用户可向 Configuration Manager 自动创建和维护的“远程 PC 连接”安全组中手动添加成员。 由于添加到此组的成员会接收远程桌面权限，因此这可能会导致权限提升。|  

### <a name="privacy-considerations"></a>隐私注意事项  

-   如果用户从公司门户中发起与工作计算机的连接，则会下载一个扩展名为 .rdp 或 .wsrdp 的文件，其中包含发起“远程桌面”会话所需的设备名称和远程桌面网关服务器名称。 文件扩展名取决于设备的操作系统。 例如，Windows 7 和 Windows 8 操作系统使用 .rdp 文件，Windows 8.1 使用 .wsrdp 文件。  

-   用户可选择打开或保存 .rdp 文件。 如果用户选择打开 .rdp 文件，则文件可能存储在 Web 浏览器缓存中，具体情况视为浏览器配置的保留设置而定。 如果用户选择保存文件，则不会将文件存储在浏览器缓存中。 系统会保存文件，直至用户将其手动删除为止。  

-   会自动下载并以本地方式保存 .wsrdp 文件。 用户下次运行“远程桌面”会话时，会覆盖此文件。  

-   在配置远程连接配置文件之前，请考虑隐私要求。  


## <a name="create-a-remote-connection-profile"></a>创建远程连接配置文件

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “远程连接配置文件”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建远程连接配置文件” 。  

4.  在 **创建远程连接配置文件向导** 的“常规” 页上，使用最多 256 个字符为每个配置文件指定名称和可选描述。  

5.  在“配置文件”设置页面上，为远程连接配置文件指定以下设置：  

    -   **远程桌面网关服务器的完整名称和端口(可选)** - 指定用于连接的远程桌面网关服务器的名称。  

        > [!NOTE]  
        >  Configuration Manager 不支持在此框中使用国际化域名指定服务器。  
        >   
        >  服务器名称的长度不能超过 256 个字符，可以包含用句点分隔的大写字符、小写字符、数字字符以及“–”  和“_”  字符。  

    -   **只允许通过网络级别身份验证运行远程桌面的计算机中的连接**  

6.  为下列每个连接设置选择“已启用”  或“已禁用”  ：  

    -   **允许至工作计算机的远程连接**  

    -   **允许工作计算机的所有主要用户进行远程连接**  

    -   **对 Windows 域和专用网络上的连接允许 Windows 防火墙例外**  

    > [!IMPORTANT]  
    >  所有三个设置必须相同，然后你才能继续通过向导的此页。  

7.  在“摘要”页上，查看要执行的操作，然后完成向导。  

 新的远程连接配置文件将显示在“资产和符合性”  工作区的“远程连接配置文件”  节点中。  

部署远程连接配置文件  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “远程连接配置文件”。  

3.  在“远程连接配置文件”  列表中，选择要部署的远程连接配置文件，然后，在“主页”  选项卡上的“部署”  组中单击“部署” 。  

4.  在“部署远程连接配置文件”  对话框中，指定下列信息：  

    -   **集合** - 单击“浏览”  以选择要在其中部署远程连接配置文件的设备集合。  

    -   **在支持时修正非符合性规则** - 启用此选项，以便在设备上发现远程连接配置文件不符合（例如，不存在时）时自动修正该配置文件。  

    -   **允许维护时段外的修正** - 如果为你向其中部署远程连接配置文件的集合配置了维护时段，请启用此选项以让 Configuration Manager 在维护时段外修正远程连接配置文件。 有关维护时段的详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。  

    -   **生成警报** - 启用此选项以配置一个警报，如果在指定日期和时间之前远程连接配置文件符合性小于指定百分比，则生成该警报。 你也可以指定是否希望将警报发送到 System Center Operations Manager。  

    -   **指定此配置基线的符合性评估计划** - 指定在设备上对部署的远程连接配置文件进行评估所依据的计划。 你可以指定简单计划或自定义计划。  

    > [!TIP]  
    >  如果设备离开向其中部署了远程连接配置文件的集合，则会在该设备上禁用远程连接配置文件设置。 但是，要使此进程正常发生，你必须已至少部署了一个配置项目或包含站点中的配置项目的配置基线。  
    >   
    >  当用户登录时，设备将评估配置文件。  
    >   
    >  如果两个远程连接配置文件部署到同一设备集合，在其中一个配置文件中选中“在支持时修正非符合性规则”  ，在另外一个配置文件中，取消选中相同的选项，并且两个远程连接配置文件包含不同的连接设置，则取消选中此选项的配置文件可能会替代另一个配置文件中的设置。 Configuration Manager 不支持这种类型的远程连接配置文件部署。  

5.  单击“确定”  关闭“部署远程连接配置文件”  对话框并创建部署。  

## <a name="monitor-a-remote-connection-profile"></a>监视远程连接配置文件  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>在 Configuration Manager 控制台中查看符合性结果  

1.  在 Configuration Manager 控制台中，单击“监视” > “部署”。  

3.  在“部署”  列表中，选择要查看其符合性信息的远程连接配置文件部署。  

4.  你可以在主页上查看有关远程连接配置文件部署符合性的摘要信息。 若要查看更详细的信息，请选择远程连接配置文件部署，然后在“主页”  选项卡上的“部署”  组中，单击“查看状态”  以打开“部署状态”  页。  

     “部署状态”  页包含下列选项卡：  

    -   **符合：** 显示基于受影响资产数量的远程连接配置文件的符合性。 你可以双击规则以在“资产和符合性”  工作区中的“用户”  节点下创建一个临时节点。 此节点包含符合远程连接配置文件的所有设备。 “资产详细信息”  窗格也显示符合此配置文件的设备。 双击列表中的设备以显示其他信息。  

        > [!IMPORTANT]  
        >  如果某个远程连接配置文件在客户端设备上不适用，则不会评估该配置文件。 但是，它返回的状态为符合。  

    -   **错误：** 显示基于受影响资产数量的所选远程连接配置文件部署的所有错误的列表。 你可以双击规则以在“资产和符合性”  工作区的“用户”  节点下创建一个临时节点。 此节点包含对于此配置文件生成了错误的所有设备。 当你选择某台设备时，“资产详细信息”  窗格将显示受所选问题影响的设备。 双击列表中的设备以显示有关问题的其他信息。  

    -   **不符合：** 显示基于受影响资产数量的远程连接配置文件内所有不符合规则的列表。 你可以双击规则以在“资产和符合性”  工作区的“用户”  节点下创建一个临时节点。 此节点包含不符合此配置文件的所有设备。 当你选择某台设备时，“资产详细信息”  窗格将显示受所选问题影响的设备。 双击列表中的设备以显示有关问题的其他信息。  

    -   **未知：** 显示没有为所选远程连接配置文件部署报告符合性的所有设备的列表，以及设备的当前客户端状态。  

5.  在“部署状态”  页上，你可以查看有关所部署的远程连接配置文件的符合性的详细信息。 将在“部署”  节点下创建一个临时节点，该节点可帮助你快速再次找到此信息。  

### <a name="view-compliance-results-with-reports"></a>使用报表查看符合性结果  
 Configuration Manager 中包括内置报表，可用于监视有关远程连接配置文件的信息。 这些报表的报表类别为“符合性和设置管理” 。  

> [!IMPORTANT]  
>  在符合性设置报表中使用参数“设备筛选器”  和“用户筛选器”  时，你必须使用通配符 (%) 字符。  

 有关如何在 Configuration Manager 中配置报表的详细信息，请参阅 [System Center Configuration Manager 中的报表](/sccm/core/servers/manage/reporting)。  
