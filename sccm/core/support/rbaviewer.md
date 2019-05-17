---
title: 基于角色的管理工具
titleSuffix: Configuration Manager
description: 使用基于角色的管理和审核工具在 Configuration Manager 中建模和审核安全角色和作用域。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 533d055db3a68360c3c18d0e30e0718bf42c2a7c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500807"
---
# <a name="role-based-administration-and-auditing-tool"></a>基于角色的管理和审核工具

适用范围：System Center Configuration Manager (Current Branch)

基于角色的管理和审核工具是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 使用此工具执行以下任务：

- 建模具有特定权限的安全角色  

- 审核其他用户拥有的安全作用域和安全角色



## <a name="requirements"></a>要求

- 在 Configuration Manager 控制台所在的同一台计算机上运行它  

- 你具有“完全权限管理员”、“只读分析员”或“安全管理员”角色  

- 将帐户分配给所有安全作用域和所有集合  

- （可选）要分析报表文件夹的安全性，必须具有 SQL 访问权限  

- （可选）要分析报表钻取，请在具有报表点角色的站点系统服务器上运行此工具



## <a name="procedures"></a>过程


### <a name="model-permissions-for-a-new-role"></a>为新角色的权限建模

使用以下过程为要创建的新角色的权限建模： 

1. 运行 RBAViewer.exe。  

2. 选择要基于其进行构建，或从空权限集启动的基本安全角色。 选择必要的权限。  

3. 单击“分析”以查看此自定义角色将看到的用户界面。  

    > [!Note]  
    > 要查看是否存在符合要求的现有安全角色，请切换到“相似性”选项卡。  

4. 单击“导出”将角色另存为 XML 文件。 然后将其导入 Configuration Manager 控制台。 有关详细信息，请参阅[创建自定义安全角色](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)。


### <a name="audit-existing-security-scopes"></a>审核现有安全作用域

使用以下过程来审核 Configuration Manager 中的所有现有管理用户、集合和安全作用域：

1. 运行 RBAViewer.exe。  

2. 选择工具栏中的“审核 RBA”按钮。  

    1. 若要在树状视图中查看限于集合的关系，请切换到“集合摘要”选项卡。  

    2. 若要查看分配到安全角色的对象，请切换到“范围摘要”选项卡。  


### <a name="audit-a-specific-user"></a>审核特定用户

使用以下过程来审核特定用户的基于角色的管理配置：

1. 运行 RBAViewer.exe。  

2. 选择工具栏中的“运行方式”按钮。  

3. 输入特定用户名以检查该帐户的权限。  

4. 该工具显示分配给用户或用户所属安全组的安全角色。 它还显示此用户可以看到的对象以及它们可以在控制台中执行的操作。  



## <a name="see-also"></a>另请参阅

- [基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)
- [配置基于角色的管理](/sccm/core/servers/deploy/configure/configure-role-based-administration)
