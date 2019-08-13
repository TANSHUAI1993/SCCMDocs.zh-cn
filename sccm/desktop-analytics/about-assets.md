---
title: 桌面分析中的资产
titleSuffix: Configuration Manager
description: 了解桌面分析中的设备、驱动程序和应用。
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96e76eb9a1874daa9af844d598808e30bb1a45d2
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68956244"
---
# <a name="assets-in-desktop-analytics"></a>桌面分析中的资产

> [!Note]  
> 此信息与预览版服务相关, 该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

设备将数据报告到桌面分析后, 会提供以下资产的清单:

- 设备
- 安装的应用  

在服务门户中, 在 "桌面分析" 菜单中选择 "**资产**"。


## <a name="devices"></a>设备

"**设备**" 选项卡显示你的组织中注册到桌面分析的所有设备的关键信息。 您可以对任何列或筛选特定值进行排序。

> [!NOTE]  
> 如果仪表板未报告你希望为环境显示的设备数, 请参阅[桌面分析故障排除](/sccm/desktop-analytics/troubleshooting)。  

在部署计划中, 有关设备的更多详细信息。 有关详细信息, 请参阅[计划资产](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>应用

"**应用**" 选项卡显示服务在 Windows 设备上检测到的所有已安装的应用。

在超过 2% 的已注册设备上安装**值得注意**的应用。

通过设置下列类别之一来配置应用的**重要性**:

- 严重
- 重要提示
- 忽略
- 未查看
- 不重要<!-- 3587232 -->

    > [!Tip]
    > 有关 "不重要" 类别的详细信息, 请参阅[系统和应用商店应用的自动升级决策](/sccm/desktop-analytics/about-deployment-plans#bkmk_plan-autoapp)。

从列表中选择应用, 然后选择 "**编辑**"。 此操作显示应用的详细信息。 选择 "**重要性**" 下拉菜单并设置一个值。 你还可以分配一个**所有者**。 如果进行了任何更改, 请选择 "**保存**"。

在部署计划中, 还可以设置**升级决策**。 有关详细信息, 请参阅[计划资产](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>后续步骤

- [了解桌面分析部署计划](/sccm/desktop-analytics/about-deployment-plans)  

- [了解安全性和功能更新](/sccm/desktop-analytics/about-updates)  

- [桌面分析中的兼容性评估](/sccm/desktop-analytics/compat-assessment)  
