---
title: "客户端对等缓存 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 部署内容时，将对等缓存用于客户端内容源位置。"
ms.custom: na
ms.date: 1/9/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f3e8cb3a7a4c1de9b8e9866ed192a8a0a7aec106
ms.openlocfilehash: 86129a7fd5bfac676b5f03336cf97d07747b48d1

---
# <a name="peer-cache-for-configuration-manager-clients"></a>用于 Configuration Manager 客户端的对等缓存

*适用范围：System Center Configuration Manager (Current Branch)*

从 System Center Configuration Manager 版本 1610 开始，可以使用**对等缓存**来帮助管理向远程位置中客户端的内容部署。 对等缓存是内置 Configuration Manager 解决方案，使客户端能够直接从本地缓存将内容与其他客户端共享。   

> [!TIP]  
> 1610 版本中，对等缓存和“客户端数据源”仪表板均为预发行功能。 若要启用这些功能，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

 -  通过客户端设置，可以使客户端能够使用对等缓存。
 -  若要共享内容，对等缓存客户端必须都是查找该内容的客户端当前边界组的成员。 客户端使用回退来查找相邻边界组中的内容时，相邻边界组中的对等缓存客户端不包括在可用内容源位置的池中。 有关当前边界组和相邻边界组的详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups)。
 -  Configuration Manager 客户端缓存中保留的每种类型的内容均可使用对等缓存提供给其他客户端。
 -  对等缓存不会代替其他解决方案（如 BranchCache）的使用，而是并行工作以便提供更多选项，用于扩展传统内容部署解决方案（如分发点）。 这是一种无需依赖于 BranchCache 的自定义解决方案，因此即使不启用或不使用 Windows BranchCache，此解决方案依然可正常运作。

将启用对等缓存的客户端设置部署到集合后，该集合的成员可以充当同一边界组中其他客户端的对等内容源：
 -  充当对等内容源的客户端会将可用缓存内容列表提交到其管理点。
 -  然后，当该边界组中的下一个客户端请求该内容时，具有内容的每个对等缓存源都将作为潜在内容源返回，同时还将返回该边界组中的分发点和其他内容源位置。
 -  根据正常操作过程，查找内容的客户端将从为其提供的源池中选择其中一个内容源，然后继续尝试获取内容。

> [!NOTE]
> 如果发生了向内容的相邻边界组的回退，则相邻边界组中的对等缓存内容源位置将不会添加到潜在内容源位置的客户端池中。  

虽然可以让所有客户端都加入对等缓存，但最佳做法还是仅选择最适合作为对等缓存源的那些客户端。  可以根据客户端的底盘类型、磁盘空间、网络连接等评估客户端的适用性。 有关可帮助选择要用于对等缓存的最佳客户端的详细信息，请参阅[这篇由 Microsoft 顾问撰写的博客](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/)。

为了帮助了解对等缓存的使用，可以查看“客户端数据源”仪表板。 请参阅[客户端数据源仪表板](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard)。


## <a name="requirements-and-considerations-for-peer-cache"></a>对等缓存的要求和注意事项
- 任何支持作为 Configuration Manager 客户端的 Windows 操作系统都支持对等缓存。 对等缓存不支持非 Windows 操作系统。

- 必须使用对每个客户端上的缓存文件夹具有**完全控制**的**网络访问帐户**来配置站点。 默认情况下，这是 ***%windir%\ccmcache***。

- 客户端只能传输来自其当前边界组中的对等缓存客户端中的内容。

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



<!--HONumber=Jan17_HO2-->


