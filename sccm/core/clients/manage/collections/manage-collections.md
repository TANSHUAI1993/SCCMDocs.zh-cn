---
title: "管理集合 | Microsoft Docs"
description: "在 System Center Configuration Manager 中执行常见集合管理任务。"
ms.custom: na
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 4d44f98eb0755619cdd2101203a13725186b835b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理集合

*适用范围：System Center Configuration Manager (Current Branch)*

使用本主题中的概述信息可帮助执行 System Center Configuration Manager 中的集合的管理任务。  

> [!NOTE]  
>  有关如何创建 Configuration Manager 集合的信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)。  

## <a name="how-to-manage-device-collections"></a>如何管理设备集合  
 在“资产和符合性”  工作区中，选择“设备集合” ，接着选择要管理的集合，然后选择管理任务。  

 使用下表以详细了解可能需要一些信息才能让你选择的管理任务。  

|管理任务|详细信息|更多信息|  
|---------------------|-------------|----------------------|  
|**显示成员**|显示身为“设备”  节点下临时节点中所选集合的成员的所有资源。|无更多信息。|  
|**添加所选项**|提供了下列选项，可执行以下操作之一：<br /><br /> - <br />                    **将所选项添加到现有设备集合** - 将打开“选择集合”对话框，可以从中选择想要将所选集合的成员添加到的集合。 使用“包括集合”  成员身份规则可将所选集合包括在此集合中。<br /><br /> - **将所选项添加到新的设备集合** - 将打开“创建设备集合向导”，可以在其中创建新的集合。 使用“包括集合”  成员身份规则可将所选集合包括在此集合中。|[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)|  
|**安装客户端**|将打开“安装客户端向导”，它使用客户端推送安装在所选集合中的所有计算机上安装 Configuration Manager 客户端。|[如何部署客户端到 Windows 计算机](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**管理相关性请求**|将打开“管理用户设备相关性请求”  对话框，你可以在其中批准或拒绝挂起的请求，以为所选集合中的设备建立用户设备相关性。|[在 System Center Configuration Manager 中将用户和设备与用户设备关联相链接](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**清除所需的 PXE 部署**|从所选集合的所有成员中清除任何所需的 PXE 启动部署。|[操作系统部署简介](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**更新成员身份**|评估所选集合的成员身份。 对于具有很多成员的集合，此更新可能需要一些时间才能完成。 使用“刷新”  操作，在更新完成后将显示更新为新的集合成员。|无更多信息。|  
|**添加资源**|将打开“将资源添加到集合”  对话框，你可以在其中搜索要添加到所选集合的新资源。<br /><br /> 所选集合的图标将在更新正在进行时显示为沙漏符号。|无更多信息。|  
|**客户端通知**|指示所选设备集合中的所有客户端下载计算机或用户策略。|无更多信息。|  
|**Endpoint Protection**|执行完整或快速反恶意软件扫描，或将最新反恶意软件定义下载到所选集合中的计算机。|[System Center Configuration Manager 中的 Endpoint Protection](../../../../protect/deploy-use/endpoint-protection.md)|  
|**导出**|将打开“导出集合向导”，可帮助将此集合导出到托管对象格式 (MOF) 文件，然后可以在其他 Configuration Manager 站点上存档或使用该文件。<br /><br /> 导出集合时，不会导出所选集合使用“包括”  或“排除”  规则引用的集合。|无更多信息。|  
|**复制**|创建所选集合的副本。 新集合使用所选集合作为限定集合。|无更多信息。|  
|**删除**|删除所选集合。 你还可以从站点数据库删除集合中的所有资源。<br /><br /> 不能删除 Configuration Manager 中内置的集合。|有关内置集合的列表，请参阅 [System Center Configuration Manager 中的集合简介](../../../../core/clients/manage/collections/introduction-to-collections.md)。|  
|**模拟部署**|打开“模拟应用程序部署向导”  ，在其中你无需安装或卸载应用程序就能测试应用程序部署的结果。|[如何使用 System Center Configuration Manager 模拟应用程序部署](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**部署**|显示下列选项：<br /><br /> - <br />                    **应用程序** - 将打开“部署软件向导”，可以在其中选择和配置所选集合的应用程序部署。<br /><br /> - <br />                    **程序** - 将打开“部署软件向导”  ，你可以在其中选择和配置所选集合的包和程序部署。<br /><br /> - **配置基线** - 将打开“部署配置基线”对话框，可以在其中配置部署所选集合的一个或多个配置基线。<br /><br /> - <br />                    **任务序列** - 将打开“部署软件向导”  ，你可以在其中选择和配置所选集合的任务序列部署。<br /><br /> - <br />                    **软件更新** - 将打开“部署软件更新向导”，可以在其中配置部署所选集合中的资源的软件更新。|[如何使用 System Center Configuration Manager 部署应用程序](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [System Center Configuration Manager 中的包和程序](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [如何在 System Center Configuration Manager 中部署配置基线](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [管理任务序列以在 System Center Configuration Manager 中自动执行任务](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [在 System Center Configuration Manager 中管理软件更新](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>如何管理用户集合  
 在“资产和符合性”  工作区中，选择“用户集合” ，接着选择要管理的集合，然后选择管理任务。  

 使用下表以详细了解可能需要一些信息才能让你选择的管理任务。  

|管理任务|详细信息|更多信息|  
|---------------------|-------------|----------------------|  
|**显示成员**|显示身为“用户”  节点下临时节点中所选集合的成员的所有资源。|无更多信息。|  
|**添加所选项**|通过此选项可执行以下操作之一：<br /><br /> - <br />                    **将所选项添加到现有用户集合** - 将打开“选择集合”对话框，可以从中选择想要将所选集合的成员添加到的集合。 使用“包括集合”  成员身份规则可将所选集合包括在此集合中。<br /><br /> - **将所选项添加到新的用户集合** - 将打开“创建用户及和向导”，可以在其中创建新的集合。 使用“包括集合”  成员身份规则可将所选集合包括在此集合中。|[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)|  
|**管理相关性请求**|将打开“管理用户设备相关性请求”  对话框，你可以在其中批准或拒绝挂起的请求，以为所选集合中的用户建立用户设备相关性。|[在 System Center Configuration Manager 中将用户和设备与用户设备关联相链接](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**更新成员身份**|评估所选集合的成员身份。 对于具有很多成员的集合，此更新可能需要一些时间才能完成。 使用“刷新”  操作，在更新完成后将显示更新为新的集合成员。<br /><br /> 所选集合的图标将在更新正在进行时显示为沙漏符号。|无更多信息。|  
|**添加资源**|将打开“将资源添加到集合”  对话框，你可以在其中搜索要添加到所选集合的新资源。|无更多信息。|  
|**导出**|将打开“导出集合向导”，可帮助将此集合导出到托管对象格式 (MOF) 文件，然后可以在其他 Configuration Manager 站点上存档或使用该文件。<br /><br /> 导出集合时，不会导出所选集合使用“包括”  或“排除”  规则引用的集合。|无更多信息。|  
|**复制**|创建所选集合的副本。 新集合使用所选集合作为限定集合。|无更多信息。|  
|**删除**|删除所选集合。 你还可以从站点数据库删除集合中的所有资源。<br /><br /> 不能删除 Configuration Manager 中内置的集合。|有关内置集合的列表，请参阅 [System Center Configuration Manager 中的集合简介](../../../../core/clients/manage/collections/introduction-to-collections.md)。|  
|**模拟部署**|打开“模拟应用程序部署向导”  ，在其中你无需安装或卸载应用程序就能测试应用程序部署的结果。|[如何使用 System Center Configuration Manager 模拟应用程序部署](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**部署**|显示下列选项：<br /><br /> - **应用程序** - 将打开“部署软件向导”，可以在其中选择和配置所选集合的应用程序部署。<br /><br /> - <br />                    **程序** - 将打开“部署软件向导”  ，你可以在其中选择和配置所选集合的包和程序部署。<br /><br /> - **配置基线** - 将打开“部署配置基线”对话框，可以在其中配置部署所选集合的一个或多个配置基线。|[如何使用 System Center Configuration Manager 部署应用程序](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [System Center Configuration Manager 中的包和程序](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [如何在 System Center Configuration Manager 中部署配置基线](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> 集合属性  
 打开集合的“属性”  对话框，即可查看和配置集合的以下属性。  

|选项卡名称|更多信息|  
|--------------|----------------------|  
|**常规**|让你能够查看和配置有关所选集合的常规信息，包括集合名称和限定集合。|  
|**成员身份规则**|让你能够配置定义此集合成员身份的成员身份规则。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../../core/clients/manage/collections/create-collections.md)。|  
|**电源管理**|让你能够配置向所选集合中计算机分配的电源管理计划。 有关详细信息，请参阅[电源管理简介](../../../../core/clients/manage/power/introduction-to-power-management.md)。|  
|**部署**|显示已部署到所选集合的成员的任何软件。|  
|**维护时段**|让你能够查看和配置应用于所选集合的成员的维护时段。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中使用维护时段](../../../../core/clients/manage/collections/use-maintenance-windows.md)。|  
|**集合变量**|让你能够配置应用于此集合并可由任务序列使用的变量。 有关详细信息，请参阅[任务序列内置变量](../../../../osd/understand/task-sequence-built-in-variables.md)。|  
|**分发点组**|让你能够将一个或多个分发点组关联到所选集合的成员。 有关详细信息，请参阅[管理 System Center Configuration Manager 的内容和内容基础结构](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|**安全**|显示可通过关联角色和安全作用域访问所选集合的管理用户。|  
|**监视器**|让你能够配置何时对于客户端状态和 Endpoint Protection 生成警报。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端状态](../../../../core/clients/deploy/configure-client-status.md)和[如何在 System Center Configuration Manager 中监视 Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md)。|  
