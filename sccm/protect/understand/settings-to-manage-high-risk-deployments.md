---
title: "管理高风险部署 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中配置站点设置以便在管理员创建高风险部署时警告他们。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8b5564f39f07a67a3c9278379ed59ca415603d21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>用于管理 System Center Configuration Manager 的高风险部署的设置

*适用范围：System Center Configuration Manager (Current Branch)*


借助 System Center Configuration Manager，可以配置会在管理员创建高风险任务序列部署时警告他们的站点设置。 其中一项高风险部署是：  

-   自动安装的部署  

-   可能产生意外结果  

 例如，其用途为“必需”的部署操作系统的任务序列被认为是高风险部署。  

 若要降低不需要的高风险部署的风险，可以在这些部署验证设置中配置大小限制：  

-   **集合大小限制**：创建部署时隐藏包含的客户端多于限制的集合。  

    -   **默认大小**：创建部署时，此设置默认隐藏其客户端数多于限制的集合。 创建部署时，你仍然可以查看这些集合，但它们在默认情况下是隐藏的。 默认值为 100。 输入值 0 可忽略此设置。  

    -   **最大大小**：创建部署时，此设置总是隐藏其客户端多于限制的集合。 默认值为 0，将忽略此设置。 “最大大小”  值必须大于“默认大小”  值。  

     例如，将“默认大小”设置为 100，将“最大大小”设置为 1000。 当创建高风险部署时，“选择集合”窗口仅显示包含的客户端少于 100 个的集合。 如果清除“隐藏成员数大于站点最低大小配置的集合”设置，则该窗口显示包含的客户端少于 1000 个的集合。  

-   **包含站点系统服务器的集合**：目标集合包含具有站点系统角色的计算机时，创建部署前将阻止部署或要求验证。 部署被阻止时，必须选择一个符合部署验证条件的不同集合。  

> [!NOTE]  
>  高风险部署始终局限于自定义集合、你所创建的集合和内置“未知计算机”  集合。 创建高风险部署时，无法选择“所有系统” 等内置集合。  

### <a name="to-configure-deployment-verification-for-a-site"></a>若要配置站点的部署验证  

1.  在 Configuration Manager 控制台中，选择“管理” >“站点配置” > “站点”，然后选择主站点进行配置。  

2.  在“主页”选项卡上的“属性”组中，选择“属性”，然后选择“部署验证”选项卡。  

3.  在设置要使用的配置之后，选择“确定”保存配置。  

### <a name="see-also"></a>另请参阅  
 [配置 System Center Configuration Manager 的站点和层次结构](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)
