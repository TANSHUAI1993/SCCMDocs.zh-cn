---
title: CMG 常见问题解答
description: 使用本文解答有关云管理网关的常见问题
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 3b178ce27b91701d52d5ea350de85216e1250442
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>有关云管理网关的常见问题解答

*适用范围：System Center Configuration Manager (Current Branch)*

本文解答了有关云管理网关的常见问题。 有关详细信息，请参阅[规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。


## <a name="frequently-asked-questions"></a>常见问题

### <a name="what-certificates-do-i-need"></a>我需要什么证书？

有关更多详细信息，请参阅[云管理网关的证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)。


### <a name="do-i-need-azure-expressroute"></a>我需要 Azure ExpressRoute 吗？

通过 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 可将本地网络扩展到 Microsoft 云中。 ExpressRoute 或其他此类虚拟网络连接对 Configuration Manager 云管理网关不是必需的。 云管理网关的设计允许基于 Internet 的客户端通过 Azure 服务与本地站点系统进行通信，而无需其他网络配置。 有关详细信息，请参阅[规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

如果组织使用 ExpressRoute，则安全性最佳做法是隔离云管理网关的 Azure 订阅。 此配置可确保云管理网关服务不以这种方式意外连接。 有关详细信息，请参阅[云管理网关的安全和隐私](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)。


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>我需要维护 Azure 虚拟机吗？

不需要维护。 云管理网关的设计使用 Azure 平台即服务 (PaaS)。 通过使用你提供的订阅，Configuration Manager 可创建必要的虚拟机 (VM)、存储和网络。 Azure 可保护和更新虚拟机。 与服务架构 (IaaS) 一样，这些 VM 不是本地环境的一部分。 云管理网关是将 Configuration Manager 环境扩展到云端的 PaaS。 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>我已经在使用 IBCM 了。 如果添加 CMG，客户端会有何种行为？

如果已经部署[基于 Internet 的客户端管理](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM)，还可以部署云管理网关。 客户端会收到这两个服务的策略。 当它们漫游到 Internet 上时，会随机选择并使用这些基于 Internet 的服务之一。


## <a name="next-steps"></a>后续步骤

- [规划云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [设置云管理网关](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [云管理网关的证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [云管理网关的安全和隐私](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [云管理网关的大小和扩展数量](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)