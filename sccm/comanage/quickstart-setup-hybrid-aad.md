---
title: 设置混合 Azure AD
titleSuffix: Configuration Manager
description: 如果环境当前具有加入域的 Windows 10 设备，请在启用共同管理之前设置混合 Azure AD
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754657"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>设置混合 Azure AD 以进行共同管理

如果 Windows 10 设备已联接本地 Active Directory，则在 Configuration Manager 中启用共同管理之前，请先将这些设备联接到 Azure Active Directory (Azure AD)。 此过程称为混合 Azure AD 联接。 

在下面的视频中，高级项目经理 Sandeep Deo 和产品营销经理 Adam Harbour 介绍并演示了如何在 Azure AD 中配置设备：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

混合 Azure AD 联接过程会自动将已加入域的本地设备注册到 Azure AD。 有关此过程的详细信息，请参阅以下文章：
- [Azure Active Directory 中的设备管理简介](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [如何规划混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

混合 Azure AD 联接是共同管理的一个重要基础方面。 某些客户可能在实现这一过程中遇到阻碍，例如：
- 组织使用第三方标识解决方案 
- 设置 Active Directory 联合身份验证服务 (ADFS) 很复杂

解决这些难题可能需要一些指导。 本文可帮助你解决这些问题。


## <a name="how-to-do-it"></a>操作说明

在创建要保护的标识时，设备类似于用户。 若要在任何位置随时保护设备的标识，需要将该设备的标识引入 Azure AD。

根据使用的域类型，可以通过两种主要方法来实现。 为以下任一域类型配置混合 Azure AD 联接：  
- [联盟域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [托管域](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

上述两种方法提供了最佳体验。 有关更多详细信息，包括完整的手动操作过程，请参阅以下文章：
- [手动配置已联接混合 Azure AD 的设备](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [混合 Azure AD 的 ADFS 传递身份验证](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview)，其中包括 Azure AD 发现  

有关故障排除指南，请参阅 [Windows 10 混合 Azure AD 联接故障排除指南](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)。



## <a name="case-study"></a>案例研究

欧洲一家大型软件公司的网络中拥有超过 100,000 名用户，该公司采用了细化的分阶段方法来启用混合 Azure AD 联接。

在规划阶段，混合 Azure AD 联接是支持共同管理的关键要素，因此 Configuration Manager 管理员与标识团队一起协作。 这家软件公司存在很多 ADFS 规则，其中一些规则相当复杂。 为应对这一挑战，标识团队在启用混合 Azure AD 联接之前审核了现有的 ADFS 规则。 IT 团队还选择将 Azure AD Connect 升级到最新版本。 Azure AD Connect 现在提供了一个自动化流程，用于启用混合 Azure AD 联接。

成功部署并在预生产环境中测试之后，此客户为整个生产环境启用了混合 Azure AD 联接。 在一周内，他们实现了所有 Windows 10 设备的共同管理。



## <a name="contact-fasttrack"></a>联系 FastTrack

如果在这一过程中的任何时候需要获得有关设置 Azure AD 的帮助，请转到 [Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登录并请求协助。 

有关详细信息，请参阅[从 FastTrack 获取帮助](/sccm/comanage/quickstart-fasttrack)。 

