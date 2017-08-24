---
title: "手动部署软件更新 | Microsoft Docs"
description: "若要手动部署更新，请从 Configuration Manager 控制台选择更新并进行手动部署，或者将更新添加到一个更新组并部署该组。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: 2a0d5f12b99689749833c109d4fa399f99451d8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManualDeploy"></a>手动部署软件更新  

*适用范围：System Center Configuration Manager (Current Branch)*

 手动软件更新部署是从 Configuration Manager 控制台中选择软件更新并手动启动部署过程的过程。 或者，你可以将选择的软件更新添加到更新组，然后手动部署更新组。 在创建将管理进行中的每月软件更新部署的 ADR 之前，你通常将使用手动部署以用所需的软件更新使客户端设备保持最新。 你还将使用手动方法来部署带外软件更新。 如果需要帮助以确定适合的部署方式，请参阅[部署软件更新](deploy-software-updates.md)。

 以下部分提供手动部署软件更新的步骤。  

##  <a name="BKMK_1SearchCriteria"></a>步骤 1：指定软件更新的搜索条件  
 Configuration Manager 控制台中可能会显示数千个软件更新。 手动部署软件更新的工作流中的第一步是标识想要部署的软件更新。 例如，你可以提供条件，以检索在 50 多台客户端设备上所需要的具有“安全”或“严重”软件更新分类的所有软件更新。  

> [!IMPORTANT]  
>  可包含在单一软件更新部署中的软件更新的最大数目为 1000。  

#### <a name="to-specify-search-criteria-for-software-updates"></a>指定软件更新的搜索条件  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”工作区中，展开“软件更新”，并单击“所有软件更新”。 此时会显示同步的软件更新。  

    > [!NOTE]  
    >  在“所有软件更新”节点上，Configuration Manager 只显示分类为“严重”和“安全”并且已在过去 30 天内发布的软件更新。  

3.  在搜索窗格中，使用以下一个或两个步骤进行筛选以标识所需的软件更新：  

    -   在搜索文本框中，键入将筛选软件更新的搜索字符串。 例如，键入特定软件更新的文章 ID 或公告 ID，或者输入将出现在一些软件更新的标题中的字符串。  

    -   单击“添加条件”，选择想要用于筛选软件更新的条件，单击“添加”，然后为此条件提供值。  

4.  单击“搜索”以筛选软件更新。  

    > [!TIP]  
    >  你可以选择在“搜索”选项卡上以及在“保存”组中保存筛选条件。  

##  <a name="BKMK_2UpdateGroup"></a>步骤 2：创建包含软件更新的软件更新组  
 软件更新组提供了一种有效方法，供你在准备部署过程中组织软件更新。 可将软件更新手动添加到软件更新组，或者，Configuration Manager 可以使用 ADR 将软件更新自动添加到新的或现有的软件更新组。 使用以下过程将软件更新手动添加到新软件更新组中。  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>将软件更新手动添加到新软件更新组中  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”工作区中，单击“软件更新”。  

3.  选择要添加到新软件更新组中的软件更新。  

4.  在“主页”选项卡上的“更新”组中，单击“创建软件更新组”。  

5.  指定软件更新组的名称并根据需要提供描述。 使用名称和描述提供足够的信息，供你确定软件更新组中软件更新的类型。 要继续，请单击“创建”。  

6.  单击“软件更新组”节点以显示新软件更新组。  

7.  选择软件更新组，在“主页”选项卡内的“更新”组中，单击“显示成员”以显示组中所包含的软件更新的列表。  

##  <a name="BKMK_3DownloadContent"></a>步骤 3：下载软件更新组的内容  
 根据需要，在部署软件更新之前，你可以下载包含在软件更新组中的软件更新的内容。 你可以选择执行此操作，以便能够在部署软件更新之前验证内容在分发点上是否可用。 这将有助于你避免内容交付的任何意外问题。 你可以跳过此步骤，内容将在部署过程中下载和复制到分发点。 使用以下过程下载软件更新组中的软件更新的内容。  



#### <a name="to-download-content-for-the-software-update-group"></a>下载软件更新组的内容
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>监视内容状态
1. 若要监视软件更新的内容状态，请单击 Configuration Manager 控制台中的“监视”。  

2. 在“监视”工作区中，展开“分发状态”，然后单击“内容状态”。  

3. 选择以前标识的软件更新包，以下载软件更新组中的软件更新。  

4. 在“主页”选项卡上的“内容”组中，单击“查看状态”。  

##  <a name="BKMK_4DeployUpdateGroup"></a>步骤 4：部署软件更新组  
 确定想要部署的软件更新并将这些软件更新添加到软件更新组中之后，你可以手动部署软件更新组中的软件更新。 使用以下过程手动部署软件更新组中的软件更新。  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>手动部署软件更新组中的软件更新  

1.  在 Configuration Manager 控制台中，单击“软件库”。  

2.  在“软件库”工作区中，展开“软件更新”，并单击“软件更新组”。  

3.  选择打算部署的软件更新组。  

4.  在“主页”选项卡上的“部署”组中，单击“部署”。 “部署软件更新向导”将会打开。  

5.  在“常规”页上，配置下列设置：  

    -   名称：指定部署的名称。 部署必须具有唯一名称，以描述部署的目的以及将其与 Configuration Manager 站点中的其他部署区分开来。 默认情况下，Configuration Manager 会用以下格式为部署自动提供名称：**Microsoft 软件更新 -** <日期><时间>  

    -   说明：指定部署的说明。 描述概述了部署和任何其他相关信息，以帮助在 Configuration Manager 站点内的其他项中标识和区分该部署。 描述字段是可选字段，最多不超过 256 个字符，默认情况下具有空白值。  

    -   软件更新/软件更新组：验证所显示的软件更新组或软件更新是否正确。  

    -   选择部署模板：指定是否要应用以前保存的部署模板。 你可以将部署模板配置为包含多个公用软件更新部署属性，然后在部署后续软件更新时应用模板，以确保类似部署保持一致并节省时间。  

    -   集合：指定部署的集合（如果适用）。 集合的成员会收到部署中定义的软件更新。  

6.  在“部署设置”页上配置下列设置：  

    -   署类型：指定软件更新部署的部署类型。 选择“必需”以创建强制性软件更新部署，部署会在配置的安装截止时间之前在客户端上自动安装软件更新。 选择“可用”以创建可供用户从软件中心中安装的可选软件更新部署。  

        > [!IMPORTANT]  
        >  创建软件更新部署之后，你稍后无法更改部署的类型。  

        > [!NOTE]  
        >  部署为“所需”的软件更新组将在后台下载，并且享有 BITS 设置（如果配置）。  
        > 但是，部署为“可用”的软件更新组将在前台下载，并且将忽略 BITS 设置。  

    -   “使用 LAN 唤醒来唤醒所需部署的客户端”：指定在截止时间是否启用 LAN 唤醒，以将唤醒数据包发送到需要部署中的一个或多个软件更新的计算机。 在安装截止时间处于睡眠模式的任何计算机将被唤醒，以便软件更新安装可以启动。 处于睡眠模式且不需要部署中的任何软件更新的客户端不会启动。 默认情况下，此设置未启用，并且只有将“部署类型”设置为“必需”时才可用。  

        > [!WARNING]  
        >  必须针对“LAN 唤醒”配置计算机和网络，然后才能使用此选项。  

    -   详细信息级别：指定客户端计算机报告的状态消息的详细信息级别。  

7.  在“计划”页上，配置下列设置：  

    -   **计划评估**：指定是按照 UTC 还是按照运行 Configuration Manager 控制台的计算机的本地时间来计算可用的时间和安装截止时间。  

        > [!NOTE]  
        >  选择本地时间，并为“软件可用时间”或“安装截止时间”选择“尽快”时，将使用运行 Configuration Manager 控制台的计算机上的当前时间来计算更新可用的时间或在客户端上安装更新的时间。 如果客户端位于其他时区，当客户端的时间达到评估时间时将发生这些操作。  

    -   软件可用时间：选择以下设置之一以指定将向客户端提供软件更新的时间：  

        -   尽快：选择此设置以尽快向客户端提供部署中的软件更新。 创建部署时，会更新客户端策略，通知客户端在其下一个客户端策略轮询周期进行部署，然后为安装提供软件更新。  

        -   特定时间：选择此设置以在特定日期和时间向客户端提供部署中的软件更新。 创建部署时，会更新客户端策略，通知客户端在其下一个客户端策略轮询周期进行部署。 但是，直到过了指定的日期和时间，才可以安装部署中的软件更新。  

    -   安装截止时间：选择以下设置之一以指定部署中的软件更新的安装截止时间。  

        > [!NOTE]  
        >  只有在“部署设置”页上将“部署类型”设置为“必需”时才可以配置安装截止时间设置。  

        -   尽快：选择此设置以尽快自动安装部署中的软件更新。  

        -   特定时间：选择此设置以在特定日期和时间自动安装部署中的软件更新。  

        > [!NOTE]  
        >  实际安装截止时间是你配置的特定时间加上随机的一段时间（最多为 2 小时）。 这可以减少目标集合中同时安装部署中软件更新的所有客户端计算机的潜在影响。  
        >   
        >  你可以配置“计算机代理”客户端设置和“禁用截止时间随机化”，以对所需的软件更新禁用安装随机化延迟。 有关详细信息，请参阅 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)。  

8.  在“用户体验”页上，请配置下列设置：  

    -   用户通知：指定是否在配置的“软件可用时间”在客户端计算机上软件中心中显示软件更新通知，以及是否在客户端计算机上显示用户通知。 在“部署设置”页上将“部署类型”设置为“可用”时，你无法选择“在软件中心和所有通知中隐藏”。  

    -   截止时间行为：*仅当“部署设置”页上的“部署类型”设置为“必需”时才可用。*    
    指定到达软件更新部署的截止时间时要发生的行为。 指定是否安装部署中的软件更新。 另外，指定是否在安装软件更新后执行系统重启而不考虑配置的维护时段。 有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    -   设备重启行为：*仅当部署设置页上的部署类型*设置为“必需”时才可用。    
    指定安装软件更新后是否在服务器和工作站上抑制系统重启，以及是否需要重启系统以完成安装。  

        > [!IMPORTANT]  
        >  在服务器环境中，或者在不希望默认重启安装软件更新的计算机的情况下，抑制系统重启可能很有用。 但是，执行此操作可能会使计算机处于不安全状态，而允许强制重启有助于确保立即完成软件更新安装。

    -   **Windows Embedded 设备的写入筛选器处理**：将软件更新部署到启用了写入筛选器的 Windows Embedded 设备时，你可以指定将软件更新安装在临时覆盖区上并稍后提交更改，或者在安装截止时或在维护时段内提交更改。 如果在安装截止时或在维护时段内提交更改，则需要重新启动，而且更改将保留在设备上。  

        > [!NOTE]  
        >  将软件更新部署到 Windows Embedded 设备时，确保设备是配置了维护时段的集合的成员。  

    - **重启时的软件更新部署重新评估行为**：从 Configuration Manager 版本 1606 开始，选择此设置可配置软件更新部署，使客户端在安装软件更新并重启后立即运行软件更新符合性扫描。 这使客户端可以检查在客户端重新启动之后成为适用状态的其他软件更新，以及随后在相同维护时段期间安装它们（并成为符合状态）。

9. 在“警报”页上，配置 Configuration Manager 和 System Center Operations Manager 为此部署生成警报的方式。 只有在“部署设置”页上将“部署类型”设置为“必需”时，才可以配置警报。  

    > [!NOTE]  
    >  你可以从“软件库”工作区的“软件更新”节点中查看最新软件更新警报。  

10. 在“下载设置”页上配置下列设置：  

    - 指定当客户端连接到慢速网络或正在使用回退内容位置时是否将下载和安装软件更新。  

    - 指定当软件更新的内容在首选分发点上不可用时客户端是否下载和安装回退分发点中的软件更新。  

    - **允许客户端与同一子网上的其他客户端共享内容**：指定是否为内容下载启用 BranchCache。 有关 BranchCache 的详细信息，请参阅[内容管理的基本概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)。  

    - 如果软件更新当前在分发点上不可用，邻域或站点组从 Microsoft 更新下载内容：如果软件更新在分发点上不可用，选择此设置，可使连接到 Intranet 的客户端从 Microsoft 更新下载软件。 基于 Internet 的客户端可随时访问 Microsoft 更新，获取软件更新内容。

    - 指定是否允许客户端在安装截止日期之后下载内容（如果客户端使用按流量计费的 Internet 连接）。 Internet 提供商有时根据你在按流量计费的 Internet 连接上发送和接收的数据量计费。  

    > [!NOTE]  
    >  客户端请求部署中的软件更新的管理点中的内容位置。 下载行为取决于在此页面上配置分发点、部署包和设置的方式。 有关详细信息，请参阅 [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md)。  

11. 如果已经执行[步骤 3：下载软件更新组的内容](#BKMK_3DownloadContent)，则不会显示“部署包”、“分发点”和“语言选择”页，并且可以跳到向导的步骤 15。  

    > [!IMPORTANT]  
    >  不会重新下载以前已经下载到站点服务器上的内容库中的软件更新。 甚至当你为软件更新创建新的部署包时也是如此。 如果以前已经下载了所有软件更新，则向导将跳到“语言选择”页（步骤 15）。  

12. 在“部署包”页上，选择现有部署包，或者配置以下设置以指定新部署包：  

    1.  名称：指定部署包的名称。 这必须是描述包内容的唯一名称。 它被限制为不超过 50 个字符。  

    2.  说明：指定提供有关该部署包的信息的说明。 该说明仅限于 127 个字符。  

    3.  “包源”：指定软件更新源文件的位置。  键入源位置的网络路径，例如 **\\\server\sharename\path**，或单击“浏览”来查找网络位置。 在进入到下一页之前，必须为部署包源文件创建共享文件夹。  

        > [!NOTE]  
        >  其他软件部署包不能使用你指定的部署包源位置。  

        > [!IMPORTANT]  
        >  SMS 提供程序计算机帐户和运行向导下载软件更新的用户都必须对下载位置具有“写” NTFS 权限。 你应该仔细限制对此下载位置的访问，以减少攻击者篡改软件更新源文件的风险。  

        > [!IMPORTANT]  
        >  在 Configuration Manager 创建部署包之后，可在部署包属性中更改包源位置。 但是，如果你执行此操作，则必须首先将原始包源中的内容复制到新包源位置。  

    4.  发送优先级：指定部署包的发送优先级。 Configuration Manager 在将包发送到分发点时将使用部署包的发送优先级。 部署包按优先级顺序发送：高、中或低。 具有相同优先级的包按照其创建顺序发送。 如果没有囤积，则将立即处理包，而不考虑其优先级。  

13. 在“分发点”页上，指定将承载软件更新文件的分发点或分发点组。 有关分发点的详细信息，请参阅[分发点配置](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)。  

14. 在“下载位置”页上，指定是从 Internet 中还是从本地网络中下载软件更新文件。 配置下列设置：  

    -   从 Internet 下载软件更新：选择此设置以从 Internet 上的指定位置下载软件更新。 默认情况下将启用此设置。  

    -   从本地网络上的位置下载软件更新：选择此设置以从本地文件夹或共享的网络文件夹下载软件更新。 当运行向导的计算机无法访问 Internet 时，此设置很有用。 能够访问 Internet 的任何计算机可以先下载软件更新，然后将它们存储本地网络上的某个位置，以便在以后安装时访问。  

15. 在“语言选择”页上，为已选定要下载的软件更新选择语言。 只有在提供了与选择的语言对应的软件更新时才能下载软件更新。 并非特定于语言的软件更新是随时都能下载的。 默认情况下，向导会选择你已在软件更新点的属性中配置的语言。 在继续进入下一页之前，必须选择至少一种语言。 如果仅选择软件更新不支持的语言，则软件更新的下载将会失败。  

16. 在“摘要”页上查看设置。 若要将设置保存到部署模板中，请单击“另存为模板”，输入名称并选择要包括在模板中的设置，然后单击“保存”。 若要更改已配置的设置，请单击关联的向导页面，然后更改设置。  

    > [!WARNING]  
    >  模板名称可以包含字母数字 ASCII 字符，以及 **\\**（反斜杠）或 **‘**（单引号）。  

17. 单击“下一步”以部署软件更新。  

 完成向导后，Configuration Manager 会将软件更新下载到站点服务器上的内容库、将软件更新分发到已配置的分发点，然后将软件更新组部署到目标集合中的客户端。 有关部署过程的详细信息，请参阅 [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess)。

## <a name="next-steps"></a>后续步骤
[监视软件更新](monitor-software-updates.md)
