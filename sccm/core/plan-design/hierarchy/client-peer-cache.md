---
title: "客户端对等缓存 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 部署内容时，将对等缓存用于客户端内容源位置。"
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 89fcd16887ae77299f9d18472ee6a1ba56794eca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="peer-cache-for-configuration-manager-clients"></a>用于 Configuration Manager 客户端的对等缓存

*适用范围：System Center Configuration Manager (Current Branch)*

从 System Center Configuration Manager 版本 1610 开始，可以使用**对等缓存**来帮助管理向远程位置中客户端的内容部署。 对等缓存是内置 Configuration Manager 解决方案，使客户端能够直接从本地缓存将内容与其他客户端共享。   

> [!TIP]  
> 如 1610 版本中所述，对等缓存和“客户端数据源”仪表板均为预发行功能。 若要启用这些功能，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="overview"></a>概述
对等缓存客户端是能够使用对等缓存功能的 Configuration Manager 客户端。 具有可与其他客户端共享的内容的对等缓存客户端是对等缓存源。
 -  通过客户端设置，可以使客户端能够使用对等缓存。
 -  若要将内容共享为对等缓存源，那么对等缓存客户端需满足以下条件：
    -  必须已加入域。 但是，未加入域的客户端可以获取已加入域的对等缓存源中的内容。
    -  必须是正在查找该内容的客户端当前边界组的成员。 客户端使用回退来查找相邻边界组中的内容时，相邻边界组中的对等缓存客户端不包括在可用内容源位置的池中。 有关当前边界组和相邻边界组的详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups)。
 - Configuration Manager 客户端缓存中保留的每种类型的内容均可使用对等缓存提供给其他客户端。
 -  对等缓存不会代替其他解决方案（如 BranchCache）的使用，而是并行工作以便提供更多选项，用于扩展传统内容部署解决方案（如分发点）。 这是一种无需依赖于 BranchCache 的自定义解决方案，因此即使不启用或不使用 Windows BranchCache，此解决方案依然可正常运作。

### <a name="operations"></a>操作

将启用对等缓存的客户端设置部署到集合后，该集合的成员可以充当同一边界组中其他客户端的对等内容源：
 -  充当对等内容源的客户端会将可用缓存内容列表提交到其管理点。
 -  然后，当该边界组中的下一个客户端请求该内容时，具有内容的每个对等缓存源都将作为潜在内容源返回，同时还将返回该边界组中的分发点和其他内容源位置。
 -  根据正常操作过程，查找内容的客户端将从为其提供的源池中选择其中一个内容源，然后继续尝试获取内容。

> [!NOTE]
> 如果发生了向内容的相邻边界组的回退，则相邻边界组中的对等缓存内容源位置将不会添加到潜在内容源位置的客户端池中。  


虽然可以让所有客户端都加入为对等缓存源，但最佳做法还是仅选择最适合作为对等缓存源的那些客户端。  可以根据客户端的底盘类型、磁盘空间、网络连接等评估客户端的适用性。 有关可帮助选择要用于对等缓存的最佳客户端的详细信息，请参阅[这篇由 Microsoft 顾问撰写的博客](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/)。

**对对等缓存源的有限访问权限**  
从版本 1702 开始，当对等缓存源计算机满足以下任一条件时，对等缓存源计算机将拒绝对内容的请求：  
  -  处于低电量模式。
  -  请求内容时 CPU 负载超过 80%。
  -  磁盘 I/O 的 AvgDiskQueueLength 超过 10。
  -  该计算机没有其他可用连接。   

使用 System Center Configuration Manager SDK 时，可以使用对等源功能的客户端配置服务器 WMI 类 (*SMS_WinPEPeerCacheConfig*) 配置这些设置。

如果计算机拒绝对内容的请求，请求计算机会继续在其可用内容源位置池中的备用源中搜索内容。   



### <a name="monitoring"></a>monitoring   
为了帮助了解对等缓存的使用，可以查看“客户端数据源”仪表板。 请参阅[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。

从版本 1702 开始，可以使用以下三个报表来查看对等缓存使用。 在控制台中，转到“监视” > “报表” > “报表”。 所有报表均为一种类型的**软件分发内容**：
1.  **对等缓存源内容拒绝**：  
使用此报告来了解边界组中对等缓存源拒绝内容请求的频率。
 - **已知问题：**在向下钻取结果（如 *MaxCPULoad* 或 *MaxDiskIO*）时，可能会收到一个错误，表明找不到该报表或详细信息。 若要解决此问题，请使用以下两个直接显示结果的报表。

2. **按条件的对等缓存源内容拒绝**：  
使用此报告来了解指定边界组的拒绝详细信息或拒绝类型。 你可指定

  - **已知问题：**不能从可用的参数中进行选择，而必须手动输入。 输入*边界组名称*和*拒绝类型*的值，如第一个报表所示。 例如，对于*拒绝类型*，你可以输入 *MaxCPULoad* 或 *MaxDiskIO*。

3. **对等缓存源内容拒绝详细信息**：   
  使用此报告来了解在被拒绝时所请求的内容。

 - **已知问题：**不能从可用的参数中进行选择，而必须手动输入。 输入在第一个报表（对等缓存源内容拒绝）中显示的*拒绝类型*值，然后输入你希望了解相关详细信息的内容源的*资源 ID*。  查找内容源的资源 ID：  

    1. 在第二个报表（按条件的对等缓存源内容拒绝）的结果中查找显示为*对等缓存源*的计算机名称。  
    2. 接下来，转到“资产和合规性” > “设备”，然后搜索该计算机名称。 使用资源 ID 列中的值。  


## <a name="requirements-and-considerations-for-peer-cache"></a>对等缓存的要求和注意事项
-   任何支持作为 Configuration Manager 客户端的 Windows 操作系统都支持对等缓存。 对等缓存不支持非 Windows 操作系统。

-   客户端只能传输来自其当前边界组中的对等缓存客户端中的内容。

-   在版本 1706 之前，客户端在其中使用对等缓存的每个站点必须使用[网络访问帐户](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account)进行配置。 从版本 1706 开始，不再需要帐户，但有一个例外。  例外情况是：客户端使用对等缓存从软件中心获取并运行任务序列，并且该任务序列将客户端重新启动到 WinPE。  在此情况下，如果客户端处于 WinPE 中，则仍需要网络访问帐户，以便它可以访问对等缓存源以获取内容。

    在需要时，对等缓存源计算机使用网络访问帐户对来自对等方的下载请求进行身份验证，且该帐户仅需要域用户权限即可实现此目的。

-   因为对等缓存内容源的当前边界由该客户端上次提交的硬件清单决定，所以漫游到网络位置且在其他边界组中的客户端可能仍被视为其以前的边界组成员，以符合对等缓存的目的。 这可能导致提供给客户端的对等缓存内容源不在其直接网络位置中。 建议排除可能有此配置的客户端作为对等缓存源加入。

## <a name="to-configure-client-peer-cache-client-settings"></a>配置客户端对等缓存客户端设置
1.  在 Configuration Manager 控制台中，转到“管理” > “客户端设置”，然后打开要使用的设备客户端设置对象。 还可以修改默认客户端设置对象。
2.  从可用设置的列表中，选择“客户端缓存设置”。
3.  将“在完整的 OS 中启用 Configuration Manager 客户端以共享内容”设置为“是”。
4.  配置以下设置以定义要用于对等缓存的端口：  
  -  **初始网络广播的端口**
  -  **启用 HTTPS，以进行客户端对等通信**
  -  **用于从对等中下载内容的端口 (HTTP/HTTPS)**

在启用了对等缓存的每台计算机上，如果 Windows 防火墙正在使用中，则 Configuration Manager 会将其配置为允许使用所配置的端口。
