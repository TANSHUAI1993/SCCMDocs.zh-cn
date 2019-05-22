---
title: 客户端 Spy
titleSuffix: Configuration Manager
description: 使用客户端 Spy 排查 Configuration Manager 客户端上的软件分发、清单和软件计数问题。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: adb826a13e96947bba29a3a0928301517d446bc6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495785"
---
# <a name="client-spy"></a>客户端 Spy

适用范围：System Center Configuration Manager (Current Branch)

客户端 Spy 是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 该工具可用于排查 Configuration Manager 客户端上的软件分发、清单和软件计数问题。 

该工具检索的大部分信息都与软件部署有关：
- 当前所有软件部署 
- 软件分发历史记录
- 客户端缓存配置
- 缓存项
- 挂起的所需部署
- 可用部署  

它还显示以下清单信息
- 最新清单周期日期
- 上一个报表日期
- 软件清单主要和次要版本
- 文件收集
- 硬件清单
- IDMIF 收集
- 发现数据记录 (DDR) 

还会显示软件计数规则。 

> [!Note]   
> 为提高性能，该工具仅在选中每个选项卡时收集相关信息。 同样，单击“刷新”时，它仅刷新当前显示的选项卡的信息。



## <a name="usage"></a>用法


### <a name="tools-menu"></a>“工具”菜单

“工具”菜单中提供以下操作：  

#### <a name="connect"></a>连接
从另一台计算机检索信息。  

- 默认情况下，该工具显示当前计算机中的信息。 

- 使用远程计算机名、用户名和帐户密码进行连接。 该工具与远程计算机上的 IPC$ 共享建立连接。 当工具退出或连接到另一台计算机时，它会删除连接。  

- 它需要一个拥有足够凭据的帐户来获取信息。  

- 如果未指定用户名和密码，则客户端 Spy 使用当前登录用户的安全性上下文尝试建立连接。  

- 连接到远程计算机时，显示的所有选项卡都显示来自远程计算机的信息。

#### <a name="software-distribution"></a>软件分发
显示“[软件分发](#software-distribution)”选项卡，并隐藏其他选项卡。 默认情况下，客户端 Spy 显示“软件分发”选项卡。

#### <a name="inventory"></a>清单
显示“清单”选项卡并隐藏其他选项卡。

#### <a name="software-metering"></a>软件计数
显示“软件计数”选项卡并隐藏其他选项卡。

#### <a name="save-current-tab-to-file"></a>将当前选项卡另存为文件
将当前显示的选项卡中的信息另存为指定的文本文件。 

#### <a name="save-all-tabs-to-file"></a>将所有选项卡另存为文件
将所有选项卡中的信息另存为指定的文本文件。 它只保存所用帐户可以看到的信息。



## <a name="software-distribution-tab"></a>“软件分发”选项卡

配置以下四个选项卡上的设置：
- [软件分发执行请求](#bkmk_exec-requests)
- [软件分发历史记录](#bkmk_history)
- [软件分发缓存信息](#bkmk_cache-info)
- [软件分发挂起的执行](#bkmk_pending-exec)


### <a name="bkmk_exec-requests"></a> 软件分发执行请求

此选项卡显示所有现有部署，包括面向设备和面向用户的部署。

“软件分发执行请求”选项卡中的每个树项都包含以下四个属性：
- 播发 ID。 对于可用部署，此值可能为空。 
- 包 ID 
- 程序名称 
- 用户。 这可能是目标用户 SID 或发起请求的用户的 SID。 如果都是系统请求，则显示的用户是“系统”。 

对于每个运行请求，还会在子树结构中显示以下信息：
- 程序名称 
- 包 ID 
- 包名称 
- 请求创建时间 
- 状态 
- 运行状态（如果状态为“正在运行”） 
- 执行上下文（用户或管理员） 
- 历史记录状态（“成功”、“失败”或“未运行”） 
- LastRunTime（如果之前未运行程序，则为“从未”） 
- RetryCount（如果状态为“正在等待重试”） 
- ContentAccess（如果状态为“正在等待重试”，则为“重试计数”） 
- FailureCode（如果状态为“正在等待重试”） 
- FailureReason（如果状态为“正在等待重试”） 

如果请求需要内容，则状态为“正在等待内容”。 “软件分发缓存信息”选项卡显示此下载请求的详细信息。

如果运行请求是下载请求，还会显示下载的字节数。

> [!Note]   
> 它使用不同的图标来表示运行请求的不同状态。


### <a name="bkmk_history"></a> 软件分发历史记录

此选项卡包含有关之前运行的所有程序的信息。 这些信息存储在注册表中。

此树的主要分支是不同的用户历史记录（包括系统）。 它显示一个子树，其中包含已从其中为每个用户运行程序的包的列表。 

每个包子树的包 ID 和包名称都会显示已运行程序的列表。 它显示每个程序的以下属性： 
- 程序名
- 运行状态
- 上次运行时间
- 故障代码
- 失败原因  

若程序成功运行，故障代码和失败原因为空。


### <a name="bkmk_cache-info"></a> 软件分发缓存信息

#### <a name="cache-config"></a>缓存配置
包含有关 Configuration Manager 客户端缓存的信息。 此信息包括缓存位置、缓存大小以及当前是否正在使用。 

#### <a name="cached-items"></a>缓存项
包含由当前缓存中的所有项组成的子树。 每个树项都包含有关各项的以下信息： 
- 项在缓存中的位置（文件夹）
- 当前状态
- 包 ID
- 包名称
- 包版本
- 包大小
- 当前引用计数
- 最后引用时间 (UTC)  

#### <a name="downloading-items"></a>下载项
下载项是指客户端当前正在下载的项。 每个下载项都显示缓存项所显示的相同信息，以及下载的千字节数。 


### <a name="bkmk_pending-exec"></a> 软件分发挂起的执行

此选项卡包含过去和未来所需部署的详细信息以及可用部署列表。

每个树分支对应具有可用部署的每个用户帐户（包括系统）。

对于每个用户，子树包含以下三项：  

#### <a name="mandatory-advertisements-with-future-executions"></a>具有未来执行的必需播发
这些是仍有程序要运行的必需播发。 它们可以是可从定期、一次性或多次计划播发。 每个播发都会显示播发 ID、下次运行时间以及播发运行时间表。 

#### <a name="optional-advertisements"></a>可选播发
显示所有已发布播发的列表。 它还显示每个播发的详细信息（如播发 ID、程序名和包名称）。 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>没有未来计划执行的过去的必需播发
这是客户端上存在的播发列表，这些播发没有未来计划运行的程序。 会显示播发 ID、包名称和程序名。 针对任何可选播发显示其子树项。

> [!Note]  
> 包名称信息仅适用于在正在查看的计算机上拥有关联的播发策略的包。 如果包不再有关联的可用策略，将显示消息“包名称不再可用”。  



## <a name="inventory-tab"></a>“清单”选项卡

只有一个选项卡包含清单信息。 主树包含以下五项：  

- **软件清单**：包含上一个周期的开始日期、上一个报表的日期以及上一个报表的次要和主要版本。  

- **文件集合**：包含上一个周期的开始日期、上一个报表的日期以及上一个报表的次要和主要版本。  

- **硬件清单**：包含上一个周期的开始日期、上一个报表的日期以及上一个报表的次要和主要版本。  

- **IDMIF 收集**：包含上一个周期的开始日期、上一个报表的日期以及上一个报表的次要和主要版本。  

- **DDR**：包含上一个周期的开始日期、上一个报表的日期以及上一个报表的次要和主要版本。 DDR 信息也会显示在子树中。



## <a name="software-metering-tab"></a>“软件计数”选项卡

此选项卡以子树的形式显示信息，并包含所有软件计数规则。 它将每个规则显示为节点，通过文件名和规则 ID 进行标识。 展开树中的每个节点，并查看以下信息：
- 资源管理器文件名 
- 原始文件名
- 规则 ID
- 文件版本
- 语言


