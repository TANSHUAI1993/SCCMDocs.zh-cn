---
title: 从混合 MDM 迁移
titleSuffix: Configuration Manager
description: 混合 MDM 已弃用，Intune 独立版是所必需的共同管理。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84625c12c9cac643fe5a895c066632f44ffeacdc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754687"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>从混合 MDM 进行共同管理迁移

混合移动设备管理 (MDM) 功能已弃用。 支持混合 MDM 的两端上的 1 年 9 月 2019年。 有关详细信息，请参阅[使用 Configuration Manager 和 Microsoft Intune 的混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。

Intune 独立版是建议的部署拓扑，并且需要进行共同管理。 如果你想要启用共同管理，迁移至 Intune 独立版从 Intune 混合配置。 

在以下视频中，首席计划经理 Andrew McMurray 和高级产品营销经理 Mayunk Jain 讨论和演示从混合 MDM 迁移：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>如何执行此操作

迁移到 Intune 独立版将是最成功时，使用分阶段的方法。 分阶段迁移时，您将移动用户和设备的一小部分而大部分用户和设备依然在混合 mdm。 一旦您验证迁移成功，可以开始了解更多的资源迁移到 Intune。

若要开始迁移，请使用[Microsoft Intune 数据导入程序工具](/sccm/mdm/deploy-use/migrate-import-data)收集和自动执行重新创建你的 Intune 独立版租户中的对象从 Configuration Manager 的过程。 接下来，更改 MDM 机构的一组特定的用户，并在 Intune 独立版中测试的功能。 完成此验证后，将 MDM 机构更改为 Intune 独立版的所有用户。

> [!Important]  
> 如果使用的本地条件性访问 Configuration Manager 中，此功能当前需要 Intune 混合版。  

有关此迁移过程的详细信息，请参阅[将混合 MDM 用户及其设备迁移至 Intune 独立版](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。



## <a name="case-studies"></a>案例研究

Microsoft IT 最近已移 130,000 用户从 Intune 混合版至 Intune 独立版中三个月。 有关详细信息，请参阅[Microsoft 如何使用条件性访问的终结点区域 1812年](https://youtu.be/offk-KH7eIA?t=651)。 本视频是 Microsoft 公司副总裁 Brad Anderson 和 Microsoft 的首席信息安全官 Bret Arsenault，个人曾经迁移之间的对话。 

大型医药公司 10,000 个用户从移动 Intune 混合版至 Intune 独立版数周内。

大型 IT 咨询公司在印度迁移 40000 用户从 Intune 混合版到 Intune 独立版中不超过一个月。



## <a name="contact-fasttrack"></a>请联系 FastTrack

如果需要从进程中的任何点在混合 MDM 迁移的帮助，请转到[Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登录，并请求协助。 

有关详细信息，请参阅[求助于 FastTrack](/sccm/comanage/quickstart-fasttrack)。 

