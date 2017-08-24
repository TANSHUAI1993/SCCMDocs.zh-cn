---
title: "迁移源层次结构 | Microsoft Docs"
description: "配置源层次结构和源站点，使用户可以将数据迁移到 System Center Configuration Manager 环境。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 80c43ab93ee5a2de6bf8d7993dfd46f0005d2df8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>配置源层次结构和源站点以迁移到 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

为了能够将数据迁移到 System Center Configuration Manager 环境，必须配置支持的 Configuration Manager 源层次结构，以及该层次结构中一个或多个包含要迁移的数据的源站点。  

> [!NOTE]  
>  迁移的操作在目标层次结构中的顶层站点上运行。 如果在使用连接到主子站点的 Configuration Manager 控制台时配置迁移，必须留出时间让配置复制到管理中心站点，开始运行，然后将状态复制回连接到的主站点。  

 使用下列部分中的信息和过程来指定源层次结构以及添加其他源站点。 完成这些过程之后，可以创建迁移作业，并开始将数据从源层次结构迁移到目标层次结构。  

-   [为迁移指定源层次结构](#BKBM_ConfigSrcHierarchy)  

-   [确定源层次结构的其他源站点](#BKBM_ConfigSrcSites)  

##  <a name="BKBM_ConfigSrcHierarchy"></a>为迁移指定源层次结构  
 要将数据迁移到目标层次结构，必须指定支持的源层次结构，其中包含要迁移的数据。 默认情况下，该层次结构的顶层站点成为源层次结构的源站点。 如果从 Configuration Manager 2007 层次结构中迁移，则在从初始源站点中收集了数据后，便可以为迁移配置其他源站点。 如果从 System Center 2012 Configuration Manager 或 System Center Configuration Manager 层次结构中迁移，则不必设置其他源站点以从源层次结构中迁移数据。 这是因为 Configuration Manager 的这些版本使用在源层次结构的顶层站点可用的共享数据库。 共享数据库包含你可以迁移的所有信息。  

 使用下列过程来为迁移指定源层次结构以及确定 Configuration Manager 2007 层次结构中的其他源站点。  

 使用连接到目标层次结构的 Configuration Manager 控制台运行此过程：  

### <a name="to-configure-a-source-hierarchy"></a>配置源层次结构   

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“迁移” ，然后单击“源层次结构” 。  

3.  在“主页”  选项卡上的“迁移”  组中，单击“指定源层次结构” 。  

4.  在“指定源层次结构”  对话框中，为“源层次结构” 选择“新源层次结构” 。  

5.  对于“顶层 Configuration Manager 站点服务器”，输入受支持的源层次结构的顶层站点的名称或 IP 地址。  

6.  指定具有下列权限的源站点访问帐户：  

    -   源站点帐户：对源层次结构中指定顶层站点的 SMS 提供程序的“读取”  权限。 必须拥有对源层次结构中网站的**修改**和**删除**权限，才能执行分发点共享和升级操作。

    -   源站点数据库帐户：对源层次结构中指定顶层站点的 SQL Server 数据库的“读取”  和“执行”  权限。  

     如果指定使用计算机帐户，Configuration Manager 将使用目标层次结构的顶层站点的计算机帐户。 对于此选项，请确保此帐户是源层次结构的顶层站点所在域中“分布式 COM 用户”安全组的成员。  

7.  要在源层次结构和目标层次结构之间共享分发点，请选中“为源站点服务器启用分发点共享”  复选框。 如果此时不启用分发点共享，则可在数据收集完成后通过编辑源站点的凭据来启用分发点共享。  

8.  单击“确定”  保存配置。 这将打开“数据收集状态”  对话框，并且数据收集将自动开始。  

9. 数据收集完成后，单击“关闭”  以关闭“数据收集状态”  对话框并完成配置。  

##  <a name="BKBM_ConfigSrcSites"></a>确定源层次结构的其他源站点  
 在配置支持的源层次结构时，会将该层次结构的顶层站点自动配置为源站点，并且会自动从该站点中收集数据。 接下来要进行的操作取决于源层次结构运行的 Configuration Manager 版本：  

-   对于 Configuration Manager 2007 源层次结构，在初始源站点的数据收集完成后，便可以开始从该初始源站点中进行迁移，或者配置源层次结构中的其他源站点。 若要迁移仅从子站点中可用的数据，请为 Configuration Manager 2007 层次结构配置其他源站点。 例如，要迁移的内容是在源层次结构中的子站点上创建，并且在源层次结构的顶层站点上不可用，则可以配置其他源站点来收集有关该内容的数据。  

-   针对 System Center 2012 Configuration Manager 或 System Center Configuration Manager 源层次结构，则无需配置其他源站点。 这是因为 Configuration Manager 的这些版本使用在源层次结构的顶层站点可用的共享数据库。 共享数据库包含从该源层次结构中的所有站点迁移的所有信息。 这样，你将可以在源层次结构的顶层站点中找到可迁移的数据。  

在为 Configuration Manager 2007 源层次结构配置其他源站点时，必须在源层次结构中按自上而下的顺序配置其他源站点。 在将父站点的任何子站点配置为源站点之前，你必须将该父站点配置为源站点。  

使用下列过程来为 Configuration Manager 2007 源层次结构配置其他源站点：  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>确定源层次结构中的其他源站点 

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“迁移” ，然后单击“源层次结构” 。  

3.  选择要配置为源站点的站点。  

4.  在“主页”  选项卡上的“源站点”  组中，单击“配置” 。  

5.  在“源站点凭据”  对话框中，为源站点访问帐户指定具有以下权限的帐户：  

    -   源站点帐户：对源层次结构中指定顶层站点的 SMS 提供程序的“读取”  权限。 必须拥有对源层次结构中网站的**修改**和**删除**权限，才能执行分发点共享和升级操作。  

    -   源站点数据库帐户：对源层次结构中指定顶层站点的 SQL Server 数据库的“读取”  和“执行”  权限。  

    如果指定使用计算机帐户，Configuration Manager 将使用目标层次结构的顶层站点的计算机帐户。 对于此选项，请确保此帐户是源层次结构的顶层站点所在域中“分布式 COM 用户”安全组的成员。  

6.  要在源层次结构和目标层次结构之间共享分发点，请选中“为源站点服务器启用分发点共享”  复选框。 如果此时不启用分发点共享，则可在数据收集完成后通过编辑源站点的凭据来启用分发点共享。  

7. 单击“确定”  保存配置。 这将打开“数据收集状态”  对话框，并且数据收集将自动开始。  

8.  数据收集完成后，单击“关闭”  完成配置。  
