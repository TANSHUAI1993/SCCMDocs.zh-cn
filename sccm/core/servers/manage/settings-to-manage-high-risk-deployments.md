---
title: 管理高风险部署
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中配置部署验证站点设置以便在管理员创建高风险部署时发出警告。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4d617bdea9c63010c96cef6f91e5123b27641e9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130116"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>用于管理 Configuration Manager 的高风险部署的设置

适用范围：System Center Configuration Manager (Current Branch)


使用 Configuration Manager，可以配置部署验证站点设置。 这些设置在管理员创建高风险任务序列部署时发出警告。 其中一项高风险部署是：  

-   自动安装的部署  

-   可能产生意外结果  

例如，其用途为“必需”的部署操作系统的任务序列被认为是高风险部署。  

若要降低不需要的高风险部署的风险，可以在这些部署验证设置中配置大小限制：  

- **集合大小限制**：创建部署时，隐藏包含的客户端数多于限制的集合。  

  - **默认大小**：创建部署时，此设置默认隐藏包含的客户端数多于此限制的集合。 创建部署时，仍然可以查看这些集合，但会默认隐藏这些集合。 默认值为 100。 要忽略此设置，请输入值 0。  

  - **最大大小**：创建部署时，此设置总是隐藏客户端数多于此限制的集合。 默认值为 0，将忽略此设置。 “最大大小”  值必须大于“默认大小”  值。  

    例如，将“默认大小”设置为 100，将“最大大小”设置为 1000。 创建高风险部署时，“选择集合”窗口仅显示包含的客户端数少于 100 个的集合。 如果清除“隐藏成员数大于站点最低大小配置的集合”设置，则该窗口显示包含的客户端数少于 1000 的集合。  

- **包含站点系统服务器的集合**：目标集合包含具有站点系统角色的计算机时，创建部署前将阻止部署或要求验证。 部署被阻止时，选择一个符合部署验证条件的不同集合，以继续创建部署。  

> [!NOTE]  
>  高风险部署始终局限于自定义集合、你所创建的集合和内置“未知计算机”集合。 创建高风险部署时，无法选择“所有系统”等内置集合。  

### <a name="configure-deployment-verification-for-a-site"></a>配置站点的部署验证  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，选择“站点”，然后选择要配置的主站点。  

2.  单击功能区中的“属性”，然后切换到“部署验证”选项卡。  

3.  在设置要使用的配置之后，请单击“确定”以保存配置。  


### <a name="see-also"></a>另请参阅  
 [卸载站点和层次结构](/sccm/core/servers/deploy/configure/configure-sites-and-hierarchies)
