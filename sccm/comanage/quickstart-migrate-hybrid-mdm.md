---
title: 从混合 MDM 迁移
titleSuffix: Configuration Manager
description: 混合 MDM 已被停用，需要安装 Intune 独立版才能进行共同管理。
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754687"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>从混合 MDM 迁移以进行共同管理

混合移动设备管理 (MDM) 是已停用的功能。 对混合 MDM 的支持将于 2019 年 9 月 1 日结束。 有关详细信息，请参阅如何配合使用[混合 MDM 和 Configuration Manager 以及 Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management)。

Intune 独立版是建议的部署拓扑，是进行共同管理的必备版本。 若要启用共同管理，请从 Intune 混合配置迁移到 Intune 独立版。 

在下面的视频中，首席项目经理 Andrew McMurray 和高级产品市场营销经理 Mayunk Jain 介绍并演示如何从混合 MDM 进行迁移：

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>操作说明

使用分阶段方法时，迁移到 Intune 独立版的成功率最高。 使用分阶段迁移时，将迁移一小部分用户和设备，而大部分用户和设备仍通过混合 MDM 进行托管。 一旦确认迁移成功，即可开始将更多的资源迁移到 Intune。

若要开始迁移，请使用 [Microsoft Intune 数据导入工具](/sccm/mdm/deploy-use/migrate-import-data)在 Intune 独立版租户中收集和自动执行从 Configuration Manager 重新创建对象的过程。 接下来，为特定的一组用户更改你的 MDM 机构，并在 Intune 独立版中测试此功能。 此验证完成后，为所有用户将你的 MDM 机构更改为 Intune 独立版。

> [!Important]  
> 如果使用 Configuration Manager 中的本地条件访问，则此功能目前需要 Intune 混合版。  

有关此迁移过程的详细信息，请参阅[将混合 MDM 用户和设备迁移到 Intune 独立版](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。



## <a name="case-studies"></a>案例研究

Microsoft IT 在最近三个月内已将 130,000 名用户从 Intune 混合版迁移到 Intune 独立版。 有关详细信息，请参阅 [Microsoft 如何使用条件访问 - 终结点区域 1812](https://youtu.be/offk-KH7eIA?t=651)。 此视频是 Microsoft 公司副总裁 Brad Anderson 和 Microsoft 首席信息安全官 Bret Arsenault（他个人曾监管迁移）之间的对话。 

一家大型制药公司在数周内已将 10,000 名用户从 Intune 混合版迁移到 Intune 独立版。

印度的一家大型 IT 咨询公司在不到一个月的时间内已将 40,000 名用户从 Intune 混合版迁移到 Intune 独立版。



## <a name="contact-fasttrack"></a>联系 FastTrack

在此过程中，如果在任何时间点需要获得从混合 MDM 中迁移的相关帮助，请转到 [Microsoft FastTrack](https://Microsoft.com/FastTrack/)，登录并请求协助。 

有关详细信息，请参阅[从 FastTrack 获取帮助](/sccm/comanage/quickstart-fasttrack)。 

