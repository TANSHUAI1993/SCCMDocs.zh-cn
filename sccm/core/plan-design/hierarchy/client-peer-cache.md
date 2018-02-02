---
title: "客户端对等缓存"
titleSuffix: Configuration Manager
description: "使用 System Center Configuration Manager 部署内容时，将对等缓存用于客户端内容源位置。"
ms.custom: na
ms.date: 12/07/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 424f4030f2dd2a337a29d48ca831fa3a791de610
ms.sourcegitcommit: e121d8d3dd82b9f2dde2cb5206cbee602ab8e107
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="peer-cache-for-configuration-manager-clients"></a>用于 Configuration Manager 客户端的对等缓存

*适用范围：System Center Configuration Manager (Current Branch)*

从 System Center Configuration Manager 版本 1610 开始，可以使用**对等缓存**来帮助管理向远程位置中客户端的内容部署。 对等缓存是内置 Configuration Manager 解决方案，使客户端能够直接从本地缓存将内容与其他客户端共享。   

> [!TIP]  
> 此功能在 1610 版本中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从版本 1710 开始，此功能不再属于预发行功能。

## <a name="overview"></a>概述
对等缓存客户端是能够使用对等缓存功能的 Configuration Manager 客户端。 具有可与其他客户端共享的内容的对等缓存客户端是对等缓存源。
 -  通过客户端设置，可以使客户端能够使用对等缓存。
 -  若要将内容共享为对等缓存源，那么对等缓存客户端需满足以下条件：
    -  必须已加入域。 但是，未加入域的客户端可以获取已加入域的对等缓存源中的内容。
    -  必须是正在查找该内容的客户端当前边界组的成员。 客户端使用回退来查找相邻边界组中的内容时，相邻边界组中的对等缓存客户端不包括在内容源位置列表中。 有关当前边界组和相邻边界组的详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups)。
 - Configuration Manager 客户端使用对等缓存将缓存中每种类型的内容提供给其他客户端。 此内容包括 Office 365 文件和快速安装文件。<!--SMS.500850-->
 -  对等缓存不替代 BranchCache 等其他解决方案的使用。 可结合使用对等缓存与其他解决方案，获得相较传统内容部署解决方案更丰富的方案，例如分发点。 对等缓存属于自定义解决方案，独立于 BranchCache。  如果未启用或使用 Windows BranchCache，对等缓存仍能正常发挥作用。

### <a name="operations"></a>操作

若要启用对等缓存，将客户端设置部署到集合。 然后，该集合的成员会充当同一边界组中其他客户端的对等内容源。
 -  充当对等内容源的客户端会将可用缓存内容列表提交到其管理点。
 -  当边界组中的下一客户端请求该内容时，包含该内容且处于联机状态的每个对等缓存源返回到潜在的内容源列表中。 此列表还包括分发点及该边界组中的其他内容源位置。
 -  按照常规进程，寻找内容的客户端从提供的列表中选择一个源。 然后，客户端尝试获取该内容。

> [!NOTE]
> 如果客户端回退到内容的相邻边界组，则相邻边界组中的对等缓存内容源位置将不会添加到潜在内容源位置的列表中。  


最佳做法是仅选择最适合的客户端作为对等缓存源。 根据底盘类型、磁盘空间和网络连接性等属性评估客户端的适用性。 有关可帮助选择要用于对等缓存的最佳客户端的详细信息，请参阅[这篇由 Microsoft 顾问撰写的博客](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/)。

**对对等缓存源的有限访问权限**  
从版本 1702 开始，当对等缓存源计算机满足以下任一条件时，对等缓存源计算机将拒绝对内容的请求：  
  -  处于低电量模式。
  -  请求内容时 CPU 负载超过 80%。
  -  磁盘 I/O 的 AvgDiskQueueLength 超过 10。
  -  该计算机没有其他可用连接。   

在 Configuration Manager SDK 中，使用对等源功能的客户端配置服务器 WMI 类 (SMS_WinPEPeerCacheConfig) 配置这些设置。

如果计算机拒绝对内容的请求，请求计算机会继续在可用内容源位置列表中搜索内容。   



### <a name="monitoring"></a>监视   
为了帮助了解对等缓存的使用，可以查看“客户端数据源”仪表板。 请参阅[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。

从版本 1702 开始，可以使用以下三个报表来查看对等缓存使用。 在控制台中，转到“监视” > “报表” > “报表”。 所有报表均为一种类型的**软件分发内容**：
1.  **对等缓存源内容拒绝**：  
使用此报告来了解边界组中对等缓存源拒绝内容请求的频率。
 - **已知问题：**在向下钻取结果（如 *MaxCPULoad* 或 *MaxDiskIO*）时，可能会收到一个错误，表明找不到该报表或详细信息。 若要解决此问题，请使用以下两个直接显示结果的报表。

2. **按条件的对等缓存源内容拒绝**：  
使用此报告来了解指定边界组的拒绝详细信息或拒绝类型。 你可指定

  - **已知问题：**不能从可用的参数中进行选择，而必须手动输入。 输入*边界组名称*和*拒绝类型*的值，如第一个报表所示。 例如，对于*拒绝类型*，你可以输入 *MaxCPULoad* 或 *MaxDiskIO*。

3. **对等缓存源内容拒绝详细信息**：   
  使用此报表来了解客户端在被拒绝时所请求的内容。

 - **已知问题：**不能从可用的参数中进行选择，而必须手动输入。 如“对等缓存源内容拒绝”报表中所示，输入“拒绝类型”的值。 然后输入想要了解其详细信息的内容源的源 ID。  查找内容源的资源 ID：  

    1. 在按条件的对等缓存源内容拒绝报表的结果中查找显示为对等缓存源的计算机名称。  
    2. 接下来，转到“资产和合规性” > “设备”，然后搜索该计算机名称。 使用资源 ID 列中的值。  


## <a name="requirements-and-considerations-for-peer-cache"></a>对等缓存的要求和注意事项
-   任何支持作为 Configuration Manager 客户端的 Windows 操作系统都支持对等缓存。 对等缓存不支持非 Windows 操作系统。

-   客户端只能传输来自其当前边界组中的对等缓存客户端中的内容。

-   在版本 1706 之前，客户端在其中使用对等缓存的每个站点必须使用[网络访问帐户](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account)进行配置。 从版本 1706 开始，不再需要帐户，但有一个例外。  例外情况是：启用对等缓存的客户端从软件中心运行任务序列，并且该任务序列将重新启动到启动映像。 在此方案中，客户端仍需要网络访问帐户。 客户端位于 Windows PE 中时，它使用网络访问帐户从对等缓存源获取内容。

    如有必要，对等缓存源计算机将使用网络访问帐户对来自对等项的下载请求进行身份验证。 为此，此帐户只需域用户权限。

-   客户端的上一次硬件清单提交可确定对等缓存内容源的当前边界。 出于对等缓存的目的，漫游到其他边界组的客户端可能仍是其以前边界组的成员。 此行为可能导致提供给客户端的对等缓存内容源不在其直接网络位置中。 建议排除可能有此配置的客户端作为对等缓存源加入。
-    从版本 1706 开始，对等缓存客户端首先验证对等缓存内容源是否处于联机状态，然后再尝试下载内容。 <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>配置客户端对等缓存客户端设置
有关配置客户端设置的信息，请参阅[客户端缓存设置](/sccm/core/clients/deploy/about-client-settings#client-cache-settings)。 有关详细信息，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。

在使用 Windows 防火墙且启用了对等缓存的客户端上，Configuration Manager 会配置在客户端设置中指定的防火墙端口。
