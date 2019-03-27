---
title: 客户端通知
titleSuffix: Configuration Manager
description: 通过立即从中央 Configuration Manager 控制台执行操作来管理客户端。
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39135a1fa548c83e0ba9c7d2a98cf1e925217280
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197021"
---
# <a name="client-notification-in-configuration-manager"></a>Configuration Manager 中的客户端通知

适用范围：System Center Configuration Manager (Current Branch)

若要立即对远程客户端执行操作，请从 Configuration Manager 控制台发送客户端通知操作。 在单个设备或一组设备上启动这些操作。 



## <a name="actions"></a>操作

以下操作位于功能区上的“主页”选项卡的“设备”或“集合”组中。 


### <a name="install-client"></a>安装客户端

将打开“安装客户端向导”。 此向导使用客户端请求安装来安装 Configuration Manager 客户端。 有关详细信息，请参阅[客户端请求安装](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush)。

#### <a name="permissions"></a>权限
此操作需要“集合”对象上的“修改资源”和“读取”权限。 

默认情况下，以下内置角色具有这些权限：
- 应用程序管理员  
- 完全权限管理员  
- 基础结构管理员  
- 操作管理员  
- OS Deployment Manager  

向所有需要推送客户端的自定义角色添加这些权限。


### <a name="run-script"></a>运行脚本

将打开“运行脚本”向导以在所有集合中的客户端上运行 PowerShell 脚本。 有关详细信息，请参阅[创建和运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)。

#### <a name="permissions"></a>权限
此操作需要“集合”对象上的“运行脚本”权限。 

默认情况下，以下内置角色具有此权限：
- 完全权限管理员  
- 基础结构管理员  
- 操作管理员  

向所有需要运行脚本的自定义角色添加此权限。


### <a name="start-cmpivot"></a>启动 CMPivot

启动 **CMPivot**，以便针对目标设备运行实时查询。 有关详细信息，请参阅 [CMPivot](/sccm/core/servers/manage/cmpivot)。

#### <a name="permissions"></a>权限
此操作需要具有与[运行脚本](#run-script)操作相同的权限。 



## <a name="client-notification"></a>客户端通知

以下操作位于“客户端通知”菜单下，此菜单位于功能区上的“主页”选项卡的“设备”或“集合”组中。

在 1806 版或更早版本中，“客户端通知”选项仅在“设备集合”节点中或在查看了“设备集合”的成员身份时显示。 从 1810 版开始，可以直接从“设备”节点启动“客户端通知”。 不再要求必须在集合成员资格视图内。 <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions"></a>权限
<!--SCCMDocs-pr issue #2972-->
从 1810 版开始，客户端通知操作现在需要“集合”对象上的“通知资源”权限。 此权限适用于“客户端通知”菜单下的所有操作。 

默认情况下，以下内置角色具有此权限：
- 完全权限管理员  
- 基础结构管理员  

向所有需要使用客户端通知操作的自定义角色添加此权限。


### <a name="download-computer-policy"></a>下载计算机策略

刷新设备策略。 有关详细信息，请参阅[启动 Configuration Manager 客户端的策略检索](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval)。  


### <a name="download-user-policy"></a>下载用户策略

刷新用户策略。  


### <a name="collect-discovery-data"></a>收集发现数据

触发客户端发送发现数据记录 (DDR)。 有关详细信息，请参阅[检测信号发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat)。  


### <a name="collect-software-inventory"></a>收集软件清单

触发客户端运行软件清单周期。 有关详细信息，请参阅[软件清单简介](/sccm/core/clients/manage/inventory/introduction-to-software-inventory)。  


### <a name="collect-hardware-inventory"></a>收集硬件清单

触发客户端运行硬件清单周期。 有关详细信息，请参阅[硬件清单简介](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory)。  


### <a name="evaluate-application-deployments"></a>评估应用程序部署

触发客户端运行应用程序部署评估周期。 有关详细信息，请参阅[计划部署的重新评估](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments)。  


### <a name="evaluate-software-update-deployments"></a>评估软件更新部署

触发客户端运行软件更新部署评估周期。 有关详细信息，请参阅[软件更新简介](/sccm/sum/understand/software-updates-introduction)。  


### <a name="switch-to-the-next-software-update-point"></a>切换到下一个软件更新点

触发客户端切换到下一个可用的软件更新点。 有关详细信息，请参阅[软件更新点切换](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching)。  


### <a name="evaluate-device-health-attestation"></a>评估设备运行状况证明

触发 Windows 10 客户端检查和发送其最新的设备运行状况。 有关详细信息，请参阅[运行状况证明](/sccm/core/servers/manage/health-attestation)。  


### <a name="check-conditional-access-compliance"></a>检查条件访问符合性

触发客户端检查其是否符合条件访问。 有关详细信息，请参阅[管理对电脑的 Office 365 服务的访问](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)。  


### <a name="wake-up"></a>唤醒

从版本 1810 开始，触发休眠设备恢复全功率状态。


### <a name="restart"></a>重启

触发选定设备重启。 



## <a name="endpoint-protection"></a>Endpoint Protection

以下操作位于“Endpoint Protection”菜单下。 此菜单位于功能区上的“主页”选项卡的“集合”组中。当选择一个或多个设备时，这些操作位于功能区的“选定对象”选项卡上。

有关详细信息，请参阅 [Configuration Manager 中的 Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection)。

#### <a name="permissions"></a>权限
此操作需要“集合”对象上的“强制安全性”权限。 

默认情况下，以下内置角色具有此权限：
- 完全权限管理员  
- Endpoint Protection 管理员  
- 操作管理员  

向所有需要触发 Endpoint Protection 操作的自定义角色添加此权限。


### <a name="full-scan"></a>完整扫描

触发 Endpoint Protection 或 Windows Defender 运行*完整*反恶意软件扫描。  


### <a name="quick-scan"></a>快速扫描

触发 Endpoint Protection 或 Windows Defender 运行*快速*反恶意软件扫描。  


### <a name="download-definition"></a>下载定义

触发 Endpoint Protection 或 Windows Defender 下载最新的反恶意软件定义。  



## <a name="see-also"></a>另请参阅

- [如何管理客户端](/sccm/core/clients/manage/manage-clients)
- [如何管理集合](/sccm/core/clients/manage/collections/manage-collections)
