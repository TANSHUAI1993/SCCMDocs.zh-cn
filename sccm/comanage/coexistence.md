---
title: 第三方 MDM 共存
titleSuffix: Configuration Manager
description: 了解如何结合使用第三方 MDM 服务与 Configuration Manager
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6abf4c81d03d5887294c85337b403a6fb17dca98
ms.sourcegitcommit: 23852dda81bb8496dd10c0a8ec4f740a8e15efc3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873366"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>第三方 MDM 与 Configuration Manager 共存

同时使用 Configuration Manager 和 Microsoft Intune 来管理 Windows 10 设备，这种功能称为[“共同管理”](/sccm/comanage/overview)。 使用 Configuration Manager 管理设备并注册第三方 MDM 服务，这种功能称为“共存”。 如果没有在两者之间进行适当协调，为一个设备设置两个管理权限可能会很有挑战性。 通过共同管理，Configuration Manager 和 Intune 共同平衡[工作负荷](/sccm/comanage/workloads)，以确保没有冲突。 由于第三方服务中不存在这种交互，因此共存的管理功能存在一些限制。

在加入 Azure Active Directory 的设备上，Configuration Manager 客户端可以与第三方 MDM 服务共存。 设备可以是下列两种类型之一：

- 仅限[已联接 Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)。 （此类型有时称为“已加入云域”）  

- [混合域加入](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)：设备已加入本地 Active Directory，且已向 Azure Active Directory 注册。  

> [!Note]  
> 它不支持[个人拥有的设备](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device)。  

如果 Configuration Manager 客户端检测到第三方 MDM 服务也在管理设备，它会自动停用 Configuration Manager 中的特定工作负荷。 此行为可便于 MDM 服务接管这些职能。 它还防止客户端上出现冲突设置，冲突设置可能会对设备和用户体验造成不利影响。 在这种情况下，Configuration Manager 中的以下工作负荷会遭停用：

- 用于 VPN、WiFi、电子邮件和证书设置的资源访问策略
- 应用程序管理（包括旧包）
- 软件更新扫描和安装
- 终结点保护（Windows Defender 的一套反恶意软件防护功能）
- 用于条件访问的合规性策略
- 设备配置
- Office 即点即用管理

Configuration Manager 客户端通过继续执行以下只读操作，避免与第三方管理机构发生冲突：

- 硬件和软件清单
- 资产智能
- 软件计数
- 电源管理报告

若要详细了解使用 Configuration Manager 和 Intune 进行共同管理的优势，请参阅[共同管理优势](/sccm/comanage/overview#benefits)。