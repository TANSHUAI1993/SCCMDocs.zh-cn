---
title: 验证状态转换示例
titleSuffix: Configuration Manager
description: 请参阅 Configuration Manager 中的资产智能验证状态转换示例。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f2fb577fc4799dfb1e9c1d6585df4ed244ebfab5
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890288"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>资产智能的验证状态转换示例

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 中的资产智能验证状态不是静态的，可能会因执行的管理操作而变化，这些操作会影响存储在资产智能目录中的数据。 此主题提供了可能的验证状态转换的示例。

##  <a name="BKMK_UncategorizedIsCategorized"></a> 管理用户对未分类的目录项目进行分类  

|**状态转换**|**状态转换描述**|  
|--------------------------|--------------------------------------|  
|**未分类**|将 System Center Online 或管理用户先前未分类的已列出清单的软件标题输入到资产智能目录中。|  
|**未分类** 到 **用户定义**|管理用户对未分类的项目进行分类。|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> 管理用户对已分类的目录项目进行重新分类  

|**状态转换**|**状态转换描述**|  
|--------------------------|--------------------------------------|  
|**已验证**|目录项目已由 System Center Online 研究人员定义，并存在于资产智能目录中。|  
|**已验证** 到 **用户定义**|管理用户对已验证的目录项目进行重新分类。|  

> [!NOTE]  
>  因为从 System Center Online 获取的分类信息存储在数据库中且不能删除，所以管理用户可以在以后还原为 System Center Online 分类。  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> System Center Online 对用户定义的目录项目进行重新分类  

|**状态转换**|**状态转换描述**|  
|--------------------------|--------------------------------------|  
|**未分类**|将 System Center Online 或管理用户先前未分类的已列出清单的软件标题输入到资产智能目录中。|  
|**用户定义**|管理用户对未分类的项目进行分类。|  
|**用户定义** 到 **可更新**|在资产智能目录的后续手动批量更新期间，System Center Online 以不同的方式对用户定义的目录项目进行分类。<br /><br /> 管理用户可以使用“软件详细信息冲突解决”  对话框来决定是否使用新的分类信息或以前用户定义的值。|  
|**可更新** 到 **已验证**|管理员可以使用“软件详细信息冲突解决”  对话框来使用上一次目录更新期间从 System Center Online 接收到的新分类信息。|  
|或||  
|**可更新** 到 **用户定义**|管理员使用“软件详细信息冲突解决”  对话框来使用先前用户定义的值。|  

> [!NOTE]  
>  因为从 System Center Online 获取的分类信息存储在数据库中且不能删除，所以管理用户可以在以后还原为 System Center Online 分类。  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> 将未分类的目录项目提交给 System Center Online 以进行分类  

|**状态转换**|**状态转换描述**|  
|--------------------------|--------------------------------------|  
|**未分类**|将 System Center Online 或管理用户先前未分类的已列出清单的软件标题输入到资产智能数据库中。|  
|**未分类** 到 **挂起**|将未分类的项目提交给 System Center Online 以由管理用户进行分类。|  
|**挂起** 到 **已验证**|System Center Online 对项目进行分类。 管理用户使用批量目录更新或资产智能目录同步将项目导入资产智能目录。 两项功能都可使用资产智能同步点站点系统角色来完成。|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> 将用户定义的目录项目提交给 System Center Online 以进行分类  

|**状态转换**|**状态转换描述**|  
|--------------------------|--------------------------------------|  
|**未分类**|将管理用户或 System Center Online 先前未分类的已列出清单的软件标题输入到资产智能数据库中。|  
|**用户定义**|对未分类的项目进行分类。|  
|**用户定义** 到 **挂起**|将用户定义的项目提交给 System Center Online 以进行分类。|  
|**挂起** 到 **可更新**|在后续目录同步期间，System Center Online 以不同的方式对用户定义的目录项目进行分类。 可以使用“解决冲突”  操作来决定是使用新分类信息还是以前的用户定义值。 有关解决冲突的详细信息，请参阅[解决软件冲突详细信息](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)。|  
|**可更新** 到 **已验证**|可以使用“解决冲突”  操作并选择上次目录更新期间从 System Center Online 接收到的新分类信息。 有关解决冲突的详细信息，请参阅[解决软件冲突详细信息](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)。|  
|或||  
|**可更新** 到 **用户定义**|使用“解决冲突”  操作，并选择使用以前的用户定义值。 有关解决冲突的详细信息，请参阅[解决软件冲突详细信息](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)。|  

> [!NOTE]  
>  因为从 System Center Online 获取的分类信息存储在数据库中且不能删除，所以你可以在以后还原为 System Center Online 分类。  
