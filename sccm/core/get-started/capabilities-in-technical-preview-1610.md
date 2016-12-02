---
title: "System Center Configuration Manager Technical Preview 1610 版中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1610 版中的可用功能。"
ms.custom: na
ms.date: 10/21/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c9fe6961a63495d08a3e58e3ddf46c5d316e2613
ms.openlocfilehash: 865b5078282bf240aa6a2aef5cb2662f2471fb71

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1610 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*



本文介绍 System Center Configuration Manager Technical Preview 1610 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    


**以下是可以试用的此版本的新功能。**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>按自动部署规则中的内容大小进行筛选
现在可以对自动部署规则中软件更新的内容大小进行筛选。 例如，可以将“内容大小 (KB)”筛选器设置为 **< 2048**，以仅下载小于 2 MB 的软件更新。 使用此筛选器可防止自动下载较大的软件更新，以便在带宽受到限制时更好地支持简化的 Windows 低级别维护。 有关详细信息，请参阅[低级别操作系统上的 Configuration Manager 和简化的 Windows 维护](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)。

#### <a name="to-configure-the-content-size-field"></a>配置内容大小字段
若要配置“内容大小 (KB)”字段，请在创建 ADR 时转到“创建自动部署规则向导”中的“软件更新”页面，或转到现有 ADR 的属性中的“软件更新”选项卡。

![内容大小字段](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>改进了“所需软件”对话框功能
当用户收到来自“暂停并提醒我：”设置的所需软件后，可以从下面的下拉值列表中进行选择：
- 以后：指定根据客户端代理设置中配置的通知设置安排通知。
- 固定时间：指定在选定时间之后再次显示通知。 例如，如果用户选择 30 分钟，通知将在 30 分钟后再次显示。

![客户端代理设置中的计算机代理页](media/computeragentsettings.png)

最长暂停时间始终基于沿部署时间轴推移的客户端代理设置中配置的通知值。 例如，如果将计算机代理页上的“部署截止时间大于 24 小时，请提醒用户，提醒间隔时间（小时）为”设置配置为 10 小时，且对话框启动时距离截止时间超过 24 小时，则用户将看到一组暂停选项，暂停时间最多不超过 10小时。 随着截止时间的临近，对话框显示的选项会变少，与部署时间轴的每个组件的相关客户端代理设置相一致。

此外，对于高风险部署，如用于部署操作系统的任务序列，最终用户会更频繁地收到通知。 这不是临时性的任务栏通知，每次通知用户需要维护关键软件后，用户的电脑上会显示类似于以下对话框：

![所需软件对话框](media/requiredsoftwaredialog.png)


更多相关信息：
- [用于管理高风险部署的设置](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [如何配置客户端设置](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>拒绝以前批准的应用程序请求

作为管理员，现在可以拒绝以前批准的应用程序请求。 一旦拒绝，用户以后再安装此应用程序时必须重新提交请求。 拒绝不会卸载该应用程序，而是在用户针对该应用程序发送新请求时强制执行审批操作。 以前，应用程序请求拒绝仅适用于尚未批准的应用程序请求。

#### <a name="try-it-out"></a>试试看
拒绝已批准的应用程序请求：

1.  在 Configuration Manager 控制台中，[创建和部署需要批准的应用程序](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications)。
2.  在客户端计算机上，打开“软件中心”并提交应用程序请求。
3.  在 Configuration Manager 控制台中，批准应用程序请求。
4.  拒绝已批准的应用程序请求：在 Configuration Manager 控制台中，导航到“软件库” > “概述” > “应用程序管理” > “批准请求”，然后选择要拒绝的应用程序请求。  在功能区上，单击“拒绝”。

## <a name="exclude-clients-from-automatic-upgrade"></a>从自动升级中排除客户端
Technical Preview 1610 引入了一种新设置，可用于排除客户端集合，使其不会自动安装更新后的客户端版本。  这适用于自动升级以及其他方法，例如基于软件更新的升级、登录脚本和组策略。 这可以用于在升级客户端时需格外谨慎的计算机的集合。 排除集合中的客户端会忽略安装更新客户端软件的请求。

### <a name="configure-exclusion-from-automatic-upgrade"></a>配置自动升级排除
配置自动升级排除：
1.  在 Configuration Manager 控制台中，打开“管理”>“站点配置”>“站点”下的“层次结构设置”，然后选择“客户端升级”选项卡。
2.  选中“从升级中排除指定的客户端”复选框，然后选中“排除集合”，然后选择要排除的集合。 只能选择排除单个集合。
3.  单击“确定”以关闭并保存配置。 然后，客户端更新策略后，排除集合中的客户端将不再自动安装客户端软件更新。

  ![用于自动升级排除的设置](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> 尽管用户界面声明无法通过任何方法升级客户端，但仍有两种方法可用于替代这些设置。 可使用客户端请求安装和手动客户端安装替代此配置。 有关更多详细信息，请参阅以下部分。


### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>如何升级排除集合中的客户端
只要某个集合被配置为排除，则只能通过上述两种方法中的一种来升级集合成员的客户端软件，它会替代排除设置：
 - **客户端请求安装** – 可以使用“客户端请求安装”来升级排除集合中的客户端。 由于该操作被视为管理员的意图，因此可以此升级客户端，而无需将整个集合从排除设置中删除。       
 - **手动客户端安装** – 可以手动升级排除集合中的客户端，方法是结合使用后列命令行开关和 ccmsetup：***/ignoreskipupgrade***

  如果尝试在不使用此开关的情况下手动升级排除集合中的客户端，客户端将不会安装新的客户端软件。 有关详细信息，请参阅[如何手动安装 Configuration Manager 客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually)。

有关客户端安装方法的详细信息，请参阅[如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。


## <a name="see-also"></a>另请参阅
[System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)



<!--HONumber=Nov16_HO1-->


