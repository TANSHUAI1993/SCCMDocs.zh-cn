---
title: 边界组的过程
titleSuffix: Configuration Manager
description: 将边界组配置为以逻辑方式整理称为边界的相关网络位置。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d4aa1c044c8ea68b934a6dad4f1f85cbe43ec19b
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458022"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>如何为 Configuration Manager 配置边界组

*适用范围：System Center Configuration Manager (Current Branch)*

本文介绍如何配置边界组的过程。 在开始之前，请确保了解边界组的相关概念。 有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。



## <a name="bkmk_create"></a> 创建边界组  

1.  在 Configuration Manager 控制台中的“管理”工作区中，展开“层次结构配置”，然后选择“边界组”节点。  

2.  在“主页”选项卡上的“创建”组中，选择“创建边界组”。  

3.  在“创建边界组”对话框的“常规”选项卡上，为此边界组指定“名称”。 （可选）包括“说明”。  

4.  选择“确定”保存新边界组，或继续到下一部分以配置边界组。  


## <a name="bkmk_config"></a> 配置边界组  

1.  在 Configuration Manager 控制台中的“管理”工作区中，展开“层次结构配置”，然后选择“边界组”节点。  

2.  选择想要修改的边界组，并选择功能区中的“属性”。 此操作将打开边界组“属性”窗口。  

配置下列设置：  
- [添加或删除边界](#bkmk_add)  
- [配置站点分配，并选择站点系统服务器](#bkmk_references)  
- [配置回退行为](#bkmk_bg-fallback)  
- [配置边界组选项](#bkmk_options)  


### <a name="bkmk_add"></a> 添加或删除边界

在边界组的“属性”窗口中，使用“常规”选项卡以修改作为此边界组成员的边界：  

- 若要添加边界，选择“添加”。 在“添加边界”窗口，选中一个或多个边界的复选框，并选择“确定”。  

- 要删除边界，请选择列表中的边界并选择“删除”。  


### <a name="bkmk_references"></a> 配置站点分配，并选择站点系统服务器

若要修改站点分配和关联的站点系统服务器配置，在边界组的“属性”窗口中切换到“引用”选项卡。  

- 若要启用此边界组供客户端用于站点分配，请选择“将此边界组用于站点分配”。 然后从“分配的站点”下拉列表中选择一个站点。 有关详细信息，请参阅[站点分配](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment)。  

- 要将可用的站点系统服务器与此边界组关联，请选择“添加”。 “添加站点系统”窗口仅列出具有支持的站点系统角色的服务器。 选中一个或多个服务器的复选框，然后选择“确定”。 它会将服务器添加为此边界组的关联站点系统服务器。  

    > [!NOTE]  
    >  你可从层次结构中的任何站点选择可用站点系统的任意组合。 所选的站点系统列在作为此边界组成员的每个边界的属性中的“站点系统”选项卡上。  

- 要从此边界组中删除服务器，请选择该服务器，然后选择“删除”。  

    > [!NOTE]  
    >  若要停止使用此边界组来关联站点系统，请删除列为关联站点系统服务器的所有服务器。  


### <a name="bkmk_bg-fallback"></a> 配置回退行为

若要配置回退行为，请切换到边界组“属性”窗口中的“关系”选项卡。  

- 若要创建与另一个边界组的关系：  

    - 选择“添加”。 在“回退边界组”窗口中，选择要配置的边界组。  

    - 设置下列站点系统角色的回退时间：  
        - 分发点  
        - 软件更新点  
        - 管理点  

        > [!Note]  
        > 例如，打开分支机构边界组的“属性”窗口。 在“回退边界组”窗口中，选择总部边界组。 将分发点的回退时间设置为 `20`。 保存此配置时，分支机构边界组中的客户端将在 20 分钟后开始搜索总部边界组分发点中的内容。  

    - 若要阻止回退到特定边界组，请选择边界组，并为站点系统角色类型选择“从不回退”。 此操作可以包括默认站点边界组。  

- 若要修改现有关系配置，请在列表中选择边界组，然后选择“更改”。 此操作将仅为此边界组打开“回退边界组”窗口。  
 
- 要删除关系，请选择列表中的边界组并选择“删除”。  

有关详细信息，请参阅[回退](/sccm/core/servers/deploy/configure/boundary-groups#fallback)。 


### <a name="bkmk_options"></a> 配置边界组选项
<!--1356193--> 从版本 1806 开始，若要为此边界组中的客户端配置其他选项，请切换到“选项”选项卡。有关详细信息，请参阅[对等下载适用的边界组选项](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions)。

- 在此边界组中允许对等下载：默认情况下启用此选项。 管理点向客户端提供包含对等源的内容位置的列表。  

    - **在对等下载期间，仅使用同一子网内的对等项**：此设置取决于上面那个选项。 如果启用此选项，管理点将仅包含与客户端在同一子网中的内容位置列表对等源。  


## <a name="bkmk_site-fallback"></a> 为自动站点分配配置回退站点  

如果客户端不在具有已分配站点的边界组中，则在安装时将其分配给此站点。

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2.  在功能区“主页”选项卡的“站点”组中，选择“层次结构设置”。  

3.  在“常规”选项卡上，选中“使用回退站点”复选框。 然后从“回退站点”下拉列表中选择一个站点。  

4.  选择“确定”保存配置。  

有关详细信息，请参阅[站点分配](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment)。


## <a name="bkmk_proc-prefer"></a> 启用对首选管理点的使用  

有关详细信息，请参阅[首选管理点](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_preferred)。

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。  

2. 在功能区“主页”选项卡的“站点”组中，选择“层次结构设置”。  

3. 在“常规”选项卡上，选择“客户端更愿意使用边界组中指定的管理点”。  

4. 选择“确定”保存配置。  

