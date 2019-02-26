---
title: 设置混合 Azure AD
titleSuffix: Configuration Manager
description: 如果你的环境当前具有已加入域的 Windows 10 设备、 设置混合 Azure AD 之前启用共同管理
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec02f740485d3f8b466cde0a644aaaa8885b91f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754657"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>设置混合 Azure AD 进行共同管理

如果您有 Windows 10 设备启用共同管理配置管理器中之前已加入本地 Active Directory，首先将这些设备加入 Azure Active Directory (Azure AD)。 此过程称为混合 Azure AD 联接。 

在以下视频中，高级项目经理 Sandeep Deo 和产品营销经理 Adam Harbour 讨论并演示在 Azure AD 中配置设备：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

混合 Azure AD 加入过程会自动注册的本地已加入域的设备与 Azure AD。 有关此过程的详细信息，请参阅以下文章：
- [Azure Active Directory 中的设备管理简介](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [如何规划混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

混合 Azure AD 联接是共同管理的主要基础之一。 此过程可能难以实现对于某些客户，例如：
- 你的组织使用第三方标识解决方案 
- 复杂的设置了 Active Directory 联合身份验证服务 (ADFS)

解决这些难题可能需要一些指导。 本文可帮助缓解任何延迟。


## <a name="how-to-do-it"></a>如何执行此操作

创建你想要保护的标识时，设备是类似于用户。 若要在任何时间并在任何位置保护设备的标识，需要将该设备的标识引入 Azure AD。

根据您使用的域的类型，有两种主要方法来执行该操作。 配置混合 Azure AD 加入以下域类型之一：  
- [联合的域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [托管的域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

前面的两种方法可提供最佳体验。 有关更多详细信息，包括完全手动过程，请参阅以下文章：
- [手动配置混合 Azure AD 加入设备](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [ADFS 混合 Azure AD 直通身份验证](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview)，其中包括 Azure AD 发现  

有关故障排除指南，请参阅[故障排除指南的 Windows 10 混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)。



## <a name="case-study"></a>案例研究

具有超过 100000 个用户在其网络中的较大的欧洲软件公司采用了精细和分阶段的方法，用于启用混合 Azure AD 联接。

在规划阶段，因为混合 Azure AD 联接是支持共同管理，一个关键要素 Configuration Manager 管理员与标识团队合作。 此软件公司有多个 ADFS 规则，并且其中一些复杂。 若要解决这一挑战，标识团队之前，审阅现有 ADFS 规则启用混合 Azure AD 联接它们。 IT 团队还选择将 Azure AD Connect 升级到最新版本。 Azure AD Connect 现在提供自动化的流程，用于启用混合 Azure AD 联接。

在成功部署并在其预生产环境中测试之后, 此客户启用混合 Azure AD 联接的整个生产空间。 一周内，它们必须将每个 Windows 10 设备共同管理。



## <a name="contact-fasttrack"></a>请联系 FastTrack

如果您需要在进程中的任何点的 Azure AD 的协助设置，请转到[Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登录，并请求协助。 

有关详细信息，请参阅[求助于 FastTrack](/sccm/comanage/quickstart-fasttrack)。 

