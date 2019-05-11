---
title: 桌面分析的常见问题
titleSuffix: Configuration Manager
description: Desktop 分析的常见问题。
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4596923f9a6a42ad98dc17257b22925ad0bc5eed
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2019
ms.locfileid: "64562444"
---
# <a name="desktop-analytics-faq"></a>桌面 Analytics 常见问题解答

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="windows-upgrade"></a>Windows 升级

### <a name="can-i-upgrade-windows-and-change-architecture"></a>可以升级 Windows 和体系结构更改？

桌面 Analytics 旨在最佳支持就地升级。 就地升级不支持从 32 位到 64 位体系结构的迁移。 如果你需要在此方案中的计算机迁移，请使用刷新方案。 桌面进行分析洞察仍然有价值，在此方案中，但你可以忽略特定于升级的指南。

有关详细信息，请参阅[使用新版本的 Windows 刷新现有的计算机](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)。

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>可以从 BIOS 到 UEFI 时更改升级 Windows？

是。 有关详细信息，请参阅[就地升级过程从 BIOS 转换为 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>可以使用 Windows 10 LTSC 使用 Desktop 分析？

虽然可以使用 Desktop 分析来帮助进行更新设备从 Windows 10 长期服务频道 (LTSC) 为 Windows 10 半年频道，桌面分析不支持 Windows 10 LTSC 的更新。 此通道的 Windows 10 不适合广泛使用，并使用桌面 Analytics 支持的目标，因此不会收到功能更新。 有关详细信息，请参阅[作为服务概述 Windows](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。

## <a name="privacy"></a>隐私

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>可以在客户端直接连接到 Microsoft 数据管理服务使用 Desktop 分析？

否，整个服务是由 Windows 诊断数据，这需要设备具有此直接连接提供支持。

### <a name="can-i-choose-the-data-center-location"></a>可以选择的数据中心位置吗？

Azure Log analytics:是的当设置 Desktop 分析和创建 Log Analytics 工作区。

Microsoft 数据管理服务和分析 Azure 存储：否，这两个服务托管在美国。

### <a name="where-is-my-organizations-data-stored"></a>我的组织的数据存储在什么位置？

从你的计算机的 Windows 诊断数据是加密、 发送和处理在 Microsoft 管理的安全数据中心位于美国。 我们的桌面分析相关数据的分析然后向你提供通过 Azure 门户中的桌面分析解决方案。 所有 Azure 区域都支持桌面分析。 选择国际化的 Azure 区域不会防止诊断数据发送到并处理在美国的 Microsoft 的安全数据中心。
