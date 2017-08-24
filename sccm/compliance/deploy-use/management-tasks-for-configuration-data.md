---
title: "管理配置数据 | Microsoft Docs"
description: "在 System Center Configuration Manager 中创建配置项目和基线后，可使用其他命令执行各种操作。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1a6084834384e695b49a71fe23833049c86f8dbc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-configuration-data-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中管理配置数据

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中创建配置项目和配置基线后，后续命令可帮助你执行各种操作。  

## <a name="manage-configuration-items"></a>管理配置项目  

-   在“资产和符合性”工作区中，展开“符合性设置” > “配置项目”，选择要管理的配置项目，然后选择管理任务。  

|管理任务|详细信息|  
|---------------------|-------------|  
|**创建子配置项目**|打开“创建子配置项目向导”  ，从所选的配置项目中创建子配置项目。<br /><br /> 你不能从移动设备配置项目中创建子配置项目。<br /><br /> 有关详细信息，请参阅[创建子配置项目](../../compliance/deploy-use/create-child-configuration-items.md)。|  
|**修订版本历史记录**|打开“配置项目修订版本历史记录”  对话框，从中你能查看并管理所选配置项目之前的修订版本。|  
|**查看 XML 定义**|在新窗口中显示所选配置项目的 XML 定义。 当你想手动创建配置数据时，此信息将很有帮助。|  
|**导出**|以 cabinet (.cab) 文件格式导出配置项目，前提是该配置项目是在该站点创建的。 然后，可以将其导入到相同或不同的 Configuration Manager 站点。 配置数据被转换为 DCM Digest。|  
|**复制**|使用指定的名称创建所选配置项目的副本。 新的配置项目与原始配置项目间不保留任何关系。 这意味着重复配置项目不继续继承原始配置项目的配置信息。|  
|**删除**|打开“删除配置项目”  对话框，从中你能查看关于此配置项目的任何引用。<br /><br /> 在删除配置项目之前，你必须删除所有关于此配置项目的引用。|  

## <a name="manage-configuration-baselines"></a>管理配置基线  

-   在“资产和符合性”工作区中，展开“符合性设置” > “配置基线”，选择要管理的配置基线，然后选择管理任务。  


|管理任务|详细信息|  
|---------------------|-------------|  
|**显示成员**|显示所有被配置基线引用的配置项目。|  
|**计划摘要**|配置计划，**Configuration Baselines** 控制台中的“配置基线”节点中显示的数据将根据该计划更新站点数据库的最新信息。|  
|**运行摘要**|摘要造成“配置基线”  节点中的数据被来自站点数据库中最新的数据刷新。 此操作可能需要几分钟才能完成。 在能查看控制台中最新数据前，你可能需要单击“刷新”  。|  
|**查看 XML 定义**|在新窗口中显示所选配置基线的 XML 定义。 当你想手动创建配置数据时，此信息将很有帮助。|  
|**启用**|为符合性监视启用配置基线。|  
|**禁用**|禁用配置基线，那么它不会再在客户端计算机上进行符合性评估。 引用该配置基线的配置基线也将会被禁用。|  
|**导出**|以 cabinet (.cab) 文件格式导出配置基线，前提是它是在该站点创建的。 然后，可以将其导入到相同或不同的 Configuration Manager 站点。 配置数据被转换为 DCM Digest。<br /><br /> 有关如何导入配置数据的信息，请参阅[导入配置数据](../../compliance/deploy-use/import-configuration-data.md)。|  
|**复制**|使用指定名称创建所选配置基线的副本。 新的配置基线与原始的配置基线间不保留任何关系。|  
|**删除**|打开“删除配置基线”  对话框，从中你能查看关于此配置基线的任何引用。<br /><br /> 在删除配置基线之前，你必须删除所有关于此配置基线的引用。|  
|**部署**|打开“部署配置基线”  对话框，从中你能部署一个或多个配置基线到层次结构中的设备上。<br /><br /> 有关详细信息，请参阅[部署配置基线](../../compliance/deploy-use/deploy-configuration-baselines.md)。|  
