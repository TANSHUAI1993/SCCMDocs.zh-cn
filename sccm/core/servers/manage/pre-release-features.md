---
title: 预发行功能
titleSuffix: Configuration Manager
description: 预发行功能是指 Current Branch 中的功能，用于在生产环境中的早期测试。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04d23383d13e981d8a48f88e84444df1ac4915fe
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386038"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager 中的预发行功能

*适用范围：System Center Configuration Manager (Current Branch)*

预发行功能是指 Current Branch 中的功能，用于在生产环境中的早期测试。 这些功能完全受支持，但仍在积极开发中。 可能会在移出预发行类别后，对它们进行更改。



## <a name="give-consent"></a>同意  

同意使用预发行功能之后，才能使用。 同意是对每个层次结构执行的一次性操作，不能撤消。 除非同意，否则不能启用更新随附的新的预发行功能。 启用预发行功能后，将无法关闭。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2. 单击功能区中的“层次结构设置”。  

3. 在“层次结构设置属性”的“常规”选项卡上，启用“同意使用预发行功能”的选项。 单击" **确定**"。  



## <a name="enabling-pre-release-features"></a>启用预发行功能

安装包含预发行功能的更新时，这些功能和此次更新包含的常规功能在“更新和维护服务向导”中可见。

#### <a name="if-you-have-given-consent"></a>如果已同意
在“更新和维护服务向导”中，启用预发行功能。 请选择预发行功能，就像选择任何其他功能那样。     

（可选）等待稍后从“管理”工作区的“更新和维护服务”下的“功能”节点中启用预发行功能。 选择一项功能，然后在功能区中单击“开”。 同意后才可使用该选项。

#### <a name="if-you-havent-given-consent"></a>如果尚未同意
在“更新和维护服务向导”中，预发行功能可见，但不能启用。 安装更新后，这些功能在“功能”节点中可见。 但是，只有同意后才能启用。


> [!Important]  
> 在多站点层次结构中，只能从管理中心站点启用可选功能或预发布功能。 此行为确保层次结构中不会出现冲突。 <!--507197-->  
> 
> 如果在独立主站点中同意这样做，并通过安装新的管理中心站点扩展层次结构，则还必须在管理中心站点也同意这样做。  

启用预发行功能时，配置管理器层次结构管理器 (HMAN) 必须在该功能可用之前处理更改。 更改的处理通常是即时的。 根据 HMAN 处理周期，可能最多需要 30 分钟才能完成。 处理更改后，重启控制台，然后再使用该功能。



## <a name="pre-release-features"></a>预发行功能

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| 功能          | 添加为预发行功能 | 添加为完整版功能 |  
|------------------|----------------------|-------------------------|
| 增强的 HTTP 站点系统<!--1356889,1358228-->|版本 1806|![尚未发行](media/red_x.png)|
| 适用于共同托管设备的移动应用<!--1357892-->|[版本 1806](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)|![尚未发行](media/red_x.png)|
| 包转换管理器<!--1357861-->|版本 1806|![尚未发行](media/red_x.png)|
| iOS 支持 Cisco AnyConnect 4.0.07x 及更高版本<!--1357393-->|[版本 1802](/sccm/mdm/deploy-use/create-vpn-profiles)| [具有更新 4163547 的版本 1802](/sccm/mdm/deploy-use/create-vpn-profiles) |
| 分阶段部署<!--1356837-->|[版本 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|[版本 1806](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|
| 运行任务序列步骤 <!-- 1261338 --> |  [版本 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[版本 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender 攻击防护 <!-- 1355468 --> |  [版本 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[版本 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| 用于条件访问符合性策略的“设备运行状况证明”评估 <!-- 1235616 --> |  [版本 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[版本 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| 从 Configuration Manager 控制台创建并运行 PowerShell 脚本 <!-- 1236459 --> |  [版本 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[版本 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| 管理 Microsoft Surface 驱动程序更新 <!-- 1098490 --> |  [版本 1706](/sccm/sum/get-started/configure-classifications-and-products) | [版本 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| 使用 Configuration Manager 进行 Device Guard 管理 <!-- 1319346 --> |  [版本 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![尚未发行](media/red_x.png)|
| 任务序列内容预缓存 <!-- 1021244 --> |  [版本 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [版本 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| 在安装应用程序之前检查运行的可执行文件 <!-- 1284624 --> |   [版本 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[版本 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| 数据仓库服务点 <!-- 1277922 --> |  [版本 1702](/sccm/core/servers/manage/data-warehouse) |[版本 1706](/sccm/core/servers/manage/data-warehouse)|
| 用于向客户端进行内容分发的对等缓存 <!-- 1101436 --> |  [版本 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [版本 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| 云管理网关 <!-- 1101764 --> |  [版本 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[版本 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Microsoft Operations Management Suite 连接器 <!-- 1236739 --> | [版本 1606](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) |[版本 1802](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)|
| 维护群集感知集合（为服务器组提供服务） <!-- 1081776 --> | [版本 1602](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups)|![尚未发行](media/red_x.png)|
| 对由 System Center Configuration Manager 管理的电脑进行条件访问 <!--  --> | [版本 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [版本 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> 若要详细了解必须先启用的非预发布功能，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。  
> 
> 若要详细了解仅在技术预览分支中可用的功能，请参阅[技术预览版](/sccm/core/get-started/technical-preview)。  
