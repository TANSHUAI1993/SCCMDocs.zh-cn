---
title: 管理集合
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中执行常见集合管理任务。
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3099e61b28687ac2705d3da140af272d9de9fe2
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339040"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>如何管理 Configuration Manager 中的集合

适用范围：  System Center Configuration Manager (Current Branch)

使用本文中的概述信息可帮助执行 Configuration Manager 中的集合的管理任务。  

> [!NOTE]  
>  有关如何创建 Configuration Manager 集合的信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。



## <a name="bkmk_device"></a> 如何管理设备集合  

在“资产和符合性”  工作区中，选择“设备集合”  ，接着选择要管理的集合，然后选择管理任务。  


#### <a name="show-members"></a>显示成员
显示身为“设备”  节点下临时节点中所选集合的成员的所有资源。


#### <a name="add-selected-items"></a>添加所选的项
提供下列选项： 

- **将所选项目添加到现有设备集合**：打开“选择集合”  对话框。 选择想要将所选成员集合添加到其中的集合。 使用“包括集合”  成员身份规则可将所选集合包括在此集合中。  

- **将所选项目添加到新的设备集合**：将打开“创建设备集合向导”，可以在其中创建新的集合  。 使用“包括集合”  成员身份规则可将所选集合包括在此集合中。  


有关详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。


#### <a name="install-client"></a>安装客户端
将打开“安装客户端向导”  。 此向导使用客户端请求安装在所选集合中的所有计算机上安装 Configuration Manager 客户端。 有关详细信息，请参阅[客户端请求安装](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。


#### <a name="run-script"></a>运行脚本
将打开“运行脚本”  向导以在所有集合中的客户端上运行 PowerShell 脚本。 有关详细信息，请参阅[创建和运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。


#### <a name="manage-affinity-requests"></a>管理相关性请求
将打开“管理用户设备相关性请求”  对话框。 在其中批准或拒绝待定的请求，以为所选集合中的设备建立用户设备相关性。 有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)


#### <a name="clear-required-pxe-deployments"></a>清除所需的 PXE 部署
从所选集合的所有成员中清除任何所需的 PXE 启动部署。 有关详细信息，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。


#### <a name="update-membership"></a>更新成员身份
计算结果为所选集合的成员身份。 对于具有很多成员的集合，此更新可能需要一些时间才能完成。 使用“刷新”  操作，在更新完成后将显示更新为新的集合成员。


#### <a name="add-resources"></a>添加资源
将打开“将资源添加到集合”  对话框。 搜索要添加到所选集合的新资源。 当更新正在进行时，选定集合的图标显示沙漏符号。


#### <a name="client-notification"></a>客户端通知
有关详细信息，请参阅[客户端通知](/sccm/core/clients/manage/client-notification)。


#### <a name="endpoint-protection"></a>Endpoint Protection
有关详细信息，请参阅[客户端通知](/sccm/core/clients/manage/client-notification)。


#### <a name="export"></a>导出
此时将打开“导出集合向导”  ，可帮助你将此集合导出到托管对象格式 (MOF) 文件。 然后可将该文件存档或导入到另一个 Configuration Manager 站点。 导出集合时，不会导出引用的集合。 所选集合使用“包括”  或“排除”  规则来引用被引用的集合。


#### <a name="copy"></a>复制
创建所选集合的副本。 新集合使用所选集合作为限定集合。


#### <a name="refresh"></a>刷新
刷新视图。


#### <a name="delete"></a>删除
删除所选的集合。 你还可以从站点数据库删除集合中的所有资源。 

不能删除 Configuration Manager 中内置的集合。 有关内置集合列表，请参阅[集合简介](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections)。


#### <a name="simulate-deployment"></a>模拟部署
打开“模拟应用程序部署向导”  。 通过此向导，无需安装或卸载应用程序即可测试应用程序部署的结果。 有关详细信息，请参阅[如何模拟应用程序部署](/sccm/apps/deploy-use/simulate-application-deployments)。


#### <a name="deploy"></a>部署
显示下列选项：  

- **应用程序**：打开“部署软件向导”  。 选择并配置所选集合的应用程序部署。 有关详细信息，请参阅[如何部署应用程序](/sccm/apps/deploy-use/deploy-applications)。  

- **程序**：打开“部署软件向导”  。 选择并配置所选集合的包和程序部署。 有关详细信息，请参阅[包和程序](/sccm/apps/deploy-use/packages-and-programs)。  

- **配置基线**：打开“部署配置基线”对话框  。 配置所选集合的一个或多个配置基线的部署。 有关详细信息，请参阅[如何部署配置基线](/sccm/compliance/deploy-use/deploy-configuration-baselines)。  

- **任务序列**：打开“部署软件向导”  。 选择并配置所选集合的任务序列部署。 有关详细信息，请参阅[管理任务序列以自动执行任务](/sccm/osd/deploy-use/deploy-a-task-sequence)。  

- **软件更新**：打开“部署软件更新向导”  。 配置所选集合中到资源的软件更新部署。 有关详细信息，请参阅[管理软件更新](/sccm/sum/understand/software-updates-introduction)。  


#### <a name="clear-server-group-deployment-locks"></a>清除服务器组部署锁定
手动解除集合的所有服务器组部署锁定。 有关详细信息，请参阅[为服务器组提供服务](/sccm/sum/deploy-use/service-a-server-group)。


#### <a name="move"></a>移动
将所选集合移动到“设备集合”  节点中的另一个文件夹。 


#### <a name="properties"></a>属性
有关详细信息，请参阅[集合设置](#BKMK_CollProp)。  


## <a name="bkmk_user"></a> 如何管理用户集合  

在“资产和符合性”  工作区中，选择“用户集合”  ，接着选择要管理的集合，然后选择管理任务。  

> [!Note]  
> 以下操作适用于用户集合，但行为与设备集合相同。 除了它们适用于用户集合和其中的用户外。 有关详细信息，请参阅[如何管理设备集合](#bkmk_device)下的相应操作。  

- **显示成员**  
- **添加所选项**  
    - 将所选项目添加到现有用户集合   
    - 将所选项目添加到新用户集合   
- **管理相关性请求**  
- **更新成员身份**  
- **添加资源**  
- **导出**  
- **复制**  
- 刷新   
- **删除**  
- **模拟部署**  
- **部署**  
    - **应用程序**  
    - 程序   
    - 配置基线 
- **移动**  
- <bpt id="p1">**</bpt>Properties<ept id="p1">**</ept>


##  <a name="BKMK_CollProp"></a> 集合属性  

打开集合的“属性”  对话框，即可查看和配置以下选项：  

#### <a name="general"></a>常规
查看和配置有关所选集合的常规信息，包括集合名称和限定集合。

#### <a name="membership-rules"></a>成员身份规则
配置成员身份规则，以定义此集合的成员身份。 有关详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。  

#### <a name="power-management"></a>电源管理
配置分配给所选集合中的计算机的电源管理计划。 有关详细信息，请参阅[电源管理简介](/sccm/core/clients/manage/power/introduction-to-power-management)。  

#### <a name="deployments"></a>部署
显示已部署到所选集合的成员的任何软件。  

#### <a name="maintenance-windows"></a>维护时段
查看和配置应用于所选集合的成员的维护时段。 有关详细信息，请参阅[如何使用维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)。

#### <a name="collection-variables"></a>集合变量
配置应用到此集合并可供任务序列使用的变量。 有关详细信息，请参阅[如何设置任务序列变量](/sccm/osd/understand/using-task-sequence-variables#bkmk_set)。  

#### <a name="distribution-point-groups"></a>分发点组
将关联到所选集合的成员的一个或多个分发点组。 有关详细信息，请参阅[管理内容和内容基础结构](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure)。

#### <a name="security"></a>安全
显示可通过关联角色和安全作用域访问所选集合的管理用户。 有关详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。  

#### <a name="alerts"></a>警报 
配置何时对于客户端状态和 Endpoint Protection 生成警报。 有关详细信息，请参阅[如何配置客户端状态](/sccm/core/clients/deploy/configure-client-status)和[如何监视 Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection)。  
## <a name="bkmk_powershell"></a> 使用 PowerShell

PowerShell 可用于管理集合。  有关详情，请参阅：

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)
