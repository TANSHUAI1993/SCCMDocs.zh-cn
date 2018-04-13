---
title: 部署应用程序
titleSuffix: Configuration Manager
description: 创建或模拟将应用程序部署到设备或用户集合
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0101ba0eade5775577f52920f301a782afd7bbda
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 部署应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中，创建或模拟将应用程序部署到设备或用户集合。 此部署向 Configuration Manager 客户端提供有关如何以及何时安装软件的说明。 

至少必须为应用程序创建一种部署类型，然后才能部署该应用程序。 有关详细信息，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications)。

 还可以模拟应用程序部署。 该模拟测试部署的适用性，无需安装或卸载应用程序。 模拟部署将评估部署类型的检测方法、要求和依赖关系，然后在“监视”工作区的“部署”节点中报告结果。 有关详细信息，请参阅[模拟应用程序部署](/sccm/apps/deploy-use/simulate-application-deployments)。

> [!IMPORTANT]
>  可以模拟所需应用程序的部署，但不能模拟包或软件更新的部署。   
>  已注册 MDM 的设备不支持模拟部署、用户体验或计划设置。



## <a name="deploy-an-application"></a>部署应用程序

1.  在 Configuration Manager 控制台中，转到“软件库” > “应用程序管理” > “应用程序”。

2.  在“应用程序”  列表中，选择要部署的应用程序。 然后，在 **主页** 选项卡上，在 **部署** 组中，单击 **部署**。

### <a name="specify-general-information-about-the-deployment"></a>指定关于部署的常规信息

在“部署软件”向导的“常规”页上，指定以下信息：

- **软件**：此值显示要部署的应用程序。 单击“浏览”以选择其他应用程序。
- **集合**：单击“浏览”以选择要在其中部署应用程序的集合。
- **使用与此集合关联的默认分发点组**：将应用程序内容存储在集合的默认分发点组上。 如果未将所选集合与分发点组关联，则此选项为灰色。
- **为依赖项自动分发内容**：如果应用程序中的任何部署类型包含依赖项，则该站点也会将从属应用程序内容发送到分发点。

    >[!IMPORTANT]
    > 如果在部署了主应用程序之后更新从属应用程序，则该站点不会自动分发依赖项的任何新内容。

- **注释(可选)**：（可选）输入此部署的描述。

### <a name="specify-content-options-for-the-deployment"></a>为部署指定内容选项

在“内容”页上，单击“添加”将与此部署关联的内容添加到分发点或分发点组。 如果在“常规”页上选择“使用与此集合关联的默认分发点”，则会自动填充此选项。 只有应用程序管理员安全角色的成员可以修改它。

### <a name="specify-deployment-settings"></a>指定部署设置

在“部署软件”向导的“部署设置”页上，指定以下信息：

- **操作**：从下拉列表，选择此部署的目的，“安装”或“卸载”应用程序。

    > [!NOTE]
    >  如果将应用程序部署到设备两次，一次使用“安装”操作，一次使用“卸载”操作，则使用“安装”操作的应用程序部署优先。

  创建后，无法更改部署操作。

- 目的：从下拉列表中，选择以下选项之一：  
    - **可用**：如果将应用程序部署到用户，则用户将在软件中心看到发布的应用程序，并可根据需要进行安装。
    - **必需**：依据计划自动部署应用程序。 如果应用程序部署状态未隐藏，则使用该应用程序的所有人均可跟踪其部署状态，并于截止时间前从软件中心安装该应用程序。

    > [!NOTE]   
    >  将部署操作设置为“卸载”时，部署目的将自动设置为“必需”。 无法更改此行为。  

- **无论用户是否登录都按计划进行自动部署**：如果部署到用户，请选择此选项以将应用程序部署到用户的主要设备。 在该部署运行之前，此设置不需要用户登录。 如果用户必须与安装进行交互，请勿选择此选项。 只有当部署的目的是“必须” 时，此选项才可用。

- **发送唤醒数据包**：如果将部署目的设置为“必需”，则会在客户端运行部署前，将唤醒数据包发送到计算机。 此包可在安装截止时将计算机从休眠中唤醒。 使用此选项前，必须针对“LAN 唤醒”配置计算机和网络。
- **允许客户端使用按流量计费的 Internet 连接在安装截止时间之后下载内容，这可能会导致附加成本**：只有当部署目的是“必需”时，此选项才可用。
- **自动关闭在“部署类型属性”对话框的“安装行为”选项卡中指定的任何运行中的可执行文件**：有关详细信息，请参阅[如何在安装应用程序之前检查正在运行的可执行文件](#how-to-check-for-running-executable-files-before-installing-an-application)。

- **如果用户请求此应用程序，则需要管理员批准**：对于 1710 及较早版本，管理员在用户安装前会批准该应用程序的任何用户请求。 如果部署目的为“必需”或者应用程序部署到了设备集合，则此选项为灰色。  

    > [!NOTE]
    >  应用程序批准请求显示在“软件库”  工作区中“应用程序管理”  下的“批准请求”  节点中。 如果请求未在 45 天内获批准，则会将其删除。 重新安装客户端可能会取消任何待批准的请求。  
    >  批准安装应用程序后，可在 Configuration Manager 控制台中“拒绝”该请求。 此操作不会导致客户端从任何设备卸载应用程序，但会阻止用户从软件中心安装应用程序的新副本。

- **管理员必须在设备上批准对此应用程序的请求**：从版本 1802 开始，管理员会批准该应用程序的任何用户请求，然后用户才能将其安装到请求的设备上。 如果管理员批准请求，则用户只能在该设备上安装应用程序。 用户必须提交另一个请求才能在另一台设备上安装应用程序。 如果部署目的为“必需”或者应用程序部署到了设备集合，则此选项为灰色。 <!--1357015-->  

    这是一个可选功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。 如果未启用此功能，将看到以前的经验。  

    > [!Important]  
    > Configuration Manager 客户端也必须是 1802 版。 还必须使用新的软件中心。  

    > [!Note]  
    > 在 Configuration Manager 控制台的“软件库”工作区中，查看“应用程序管理”下的“批准请求”。 每个请求的列表现均提供“设备”列。 当针对此请求执行操作时，“应用程序请求”对话框还将包括用户从中提交请求的设备名称。  
    >  如果请求未在 45 天内获批准，则会将其删除。 重新安装客户端可能会取消任何待批准的请求。  
    >  批准安装应用程序后，可在 Configuration Manager 控制台中“拒绝”该请求。 此操作不会导致客户端从任何设备卸载应用程序，但会阻止用户从软件中心安装应用程序的新副本。

- **自动升级此应用程序的任何取代版本**：客户端使用取代应用程序升级应用程序的任何取代版本。    

    > [!NOTE]  
    > 从版本 1802 开始，对于“可用”或“必需”安装目的，可启用或禁用此选项。 <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>为部署指定计划设置

在“部署软件”向导的“计划”页上，设置何时部署此应用程序或将其提供给客户端设备。
根据部署操作是设置为“可用”还是“必需”，此页上的选项会有所不同。

在某些情况下，可能会希望为用户提供更多时间（超出所设置的任何截止时间）来安装所需的应用程序部署或软件更新。 当计算机长时间关闭并需要安装许多应用程序时，通常需要此行为。 例如，如果用户从假期返回，则他们可能需要等待很长时间，因为安装的应用程序部署已过期。 为了帮助解决此问题，现在可通过将 Configuration Manager 客户端设置部署到集合来定义强制的宽限期。

若要配置宽限期，请执行以下操作：

- 在客户端设置的“计算机代理”页上，将“部署截止时间后强制的宽限期(小时)”这一新属性的值配置为介于 **1** 和 **120** 小时之间。
- 在所需应用程序部署的“计划”页上，选择“根据用户首选项延迟此部署的强制执行，延迟时间以客户端设置中定义的宽限期为依据”。 强制宽限期适用于启用此选项的所有部署，并针对部署了客户端设置的设备。

到达应用程序安装截止时间后，客户端将在用户配置的第一个非业务时段内安装该应用程序，用户以该宽限期为依据配置了该窗口。 但是，用户仍可打开软件中心并在任何所需时间安装该应用程序。 一旦过了宽限期，对于未完成的部署，强制将恢复为正常行为。

如果部署的应用程序取代另一个应用程序，则可以设置安装截止时间，届时用户会收到新应用程序。 设置“安装截止时间”以升级具有取代应用程序的用户。

### <a name="specify-user-experience-settings-for-the-deployment"></a>为部署指定用户体验设置

在“部署软件”向导的“用户体验”页上，指定有关用户如何与应用程序安装交互的信息。

将应用程序部署到启用了写入筛选器的 Windows Embedded 设备时，可以指定将应用程序安装在临时覆盖上并稍后提交更改。 还可指定在安装截止时间或在维护时段内提交更改。 如果在安装截止时间或维护时段内提交更改，则必须重启设备。 设备上将保留这些更改。

>[!NOTE]
    >  将应用程序部署到 Windows Embedded 设备时，确保它是具有维护时段的集合的成员。 有关维护时段和 Windows Embedded 设备的详细信息，请参阅[创建 Windows Embedded 应用程序](../../apps/get-started/creating-windows-embedded-applications.md)。
    > 如果部署目的设置为“可用”  ，则不使用选项“软件安装”  和“系统重新启动(如果要求完成安装)” 。 你还可以配置在安装应用程序时用户看到的通知的级别。

### <a name="specify-alert-options-for-the-deployment"></a>为部署指定警报选项

在“部署软件”向导的“警报”页上，设置 Configuration Manager 和 System Center Operations Manager 为此部署生成警报的方式。 你可以配置用于报告警报的阈值，并在部署持续时间内关闭报告。

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>将该部署与 iOS 应用配置策略关联

在“应用配置策略”页上，单击“新建”，将此部署与 iOS 应用配置策略（如果已创建策略）相关联。 有关此类型策略的详细信息，请参阅[使用应用配置策略配置 iOS 应用](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md)。

### <a name="deployment-properties"></a>部署属性

从“监视”工作区的“部署”节点查找此新部署。 你可以从应用程序详细信息窗格的“部署”  选项卡中编辑此部署的属性或删除部署。



## <a name="delete-an-application-deployment"></a>删除应用程序部署

1.  在 Configuration Manager 控制台中，转到“软件库” > “应用程序管理” > “应用程序”。
3.  在“应用程序”列表中，选择其中含有删除的部署的应用程序。
4.  在 <application name\> 列表的“部署”选项卡中，选择要删除的应用程序部署。 然后，在“部署”选项卡的“部署”组中，单击“删除” 。

删除应用程序部署时，不会删除已安装的应用程序的任何实例。 要删除这些应用程序，必须使用“卸载”将应用程序部署到计算机。 如果删除应用程序部署，或从部署到的集合中删除资源，则应用程序将不再显示在软件中心中。



## <a name="user-notifications-for-required-deployments"></a>所需部署的用户通知
通过“暂停并提醒我”设置收到所需软件后，可从下面的下拉值列表中进行选择：
- **以后**：指定根据客户端设置中配置的通知设置安排通知。
- **固定时间**：指定在选定时间之后再次显示通知。 例如，如果选择 30 分钟，则通知在 30 分钟后再次显示。

![默认客户端设置中的计算机代理组](media/ComputerAgentSettings.png)

最长推迟时间始终基于沿部署时间轴推移的客户端设置中配置的通知值。 例如：
- 在“计算机代理”页上，将“部署截止时间大于 24 小时，每(小时)提醒用户”设置配置为 10 小时。
- 客户端将在部署截止时间前 24 小时之前显示通知对话框。
- 该对话框显示推迟选项，但不会超过 10 小时。 
- 随着部署截止时间的临近，该对话框显示更少选项。 这些选项会与部署时间轴的每个组件的相关客户端代理设置相一致。

对于高风险部署，如用于部署操作系统的任务序列，用户会更频繁地收到通知。 这不是临时性的任务栏通知，每次通知需要维护关键软件时，将显示如下所示的对话框：

![所需软件对话框会通知你关键的软件维护](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>如何在安装应用程序之前检查正在运行的可执行文件

在部署类型的“属性”对话框中，在“安装行为”选项卡上，指定一个或多个可执行文件。 如果其中一个可执行文件正在客户端上运行，则会阻止部署类型的安装。 在客户端安装部署类型之前，用户必须关闭正在运行的可执行文件。 对于所需部署，客户端可自动关闭正在运行的可执行文件。

1. 为任何部署类型打开“属性”对话框。
2. 在“*<deployment type name>* 属性”对话框的“安装行为”选项卡上，单击“添加”。
3. 在“添加或编辑可执行文件”对话框中，输入可执行文件的名称，如果正在运行，则阻止应用程序的安装。 或者，你还可以为应用程序输入友好名称，以帮助你在列表中识别它。
4. 单击“确定”，然后关闭“*<deployment type name>* 属性” 对话框。
5. 部署应用程序时，在部署软件向导的“部署设置”页上，选择“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何运行中的可执行文件”。

客户端收到部署后，将应用以下行为：

- 如果应用程序已部署为“可用”，最终用户尝试安装它时，客户端会提示其先关闭指定的正在运行的可执行文件，然后才能继续安装。

- 如果应用程序已部署为“必需”，并指定“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的正在运行的可执行文件”，则用户会看到一个对话框，通知他们在应用程序安装截止时间到达时将自动关闭指定的可执行文件。 可在“客户端设置” > “计算机代理”中计划这些对话框。 如果不希望最终用户看到这些消息，请选择部署属性的“用户体验”选项卡上的“在软件中心和所有通知中隐藏”。

- 如果应用程序已部署为“必需”，且未指定“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何正在运行的可执行文件”，如果正在运行一个或多个指定的应用程序，则应用安装失败。



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>在加入 Azure AD 的设备上部署用户可用的应用程序
<!-- 1322613 -->
如果将应用程序以可用的方式部署到用户，从版本 1802 开始，他们可以通过 Azure Active Directory (Azure AD) 设备上的软件中心浏览和安装应用程序。  

#### <a name="prerequisites"></a>先决条件

- 在管理点上启用 HTTPS  

- 将站点与 [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) 集成以实现**云管理**  

    - 配置 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- 将应用程序以可用方式部署到 Azure AD 的用户集合中  

- 将任何应用程序内容分发到[云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- 在[计算机代理](/sccm/core/clients/deploy/about-client-settings#computer-agent)组中启用客户端设置“使用新的软件中心”  

- 客户端 OS 必须是 Windows 10，并加入到 Azure AD。 已加入纯云域或混合 Azure AD。  

- 若要支持基于 Internet 的客户端：  

    - [云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - 启用客户端设置：[客户端策略](/sccm/core/clients/deploy/about-client-settings#client-policy)组中的“从 Internet 客户端启用用户策略请求”  

- 支持 Intranet 上的客户端：  

    - 将云分发点添加到客户端使用的边界组  

    - 客户端必须能够解析已启用 HTTPS 的管理点的完全限定的域名 (FQDN)  



## <a name="next-steps"></a>后续步骤

   -  [用于管理高风险部署的设置](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)
   -  [软件中心用户指导](/sccm/core/understand/software-center)

