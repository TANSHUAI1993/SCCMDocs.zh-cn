---
title: "配置要同步的分类和产品 | Microsoft Docs"
description: "按照以下步骤在 Configuration Manager 控制台中配置要同步的分类和产品。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 2da61e6e06850b36543b9fd41bd9a7d2368006fb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

*适用范围：System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>  请仅在顶层站点上使用本部分中的过程。  

 在 Configuration Manager 中，将根据你在软件更新点组件属性中指定的设置在同步过程期间检索软件更新元数据。 首次同步软件更新后，或者当发布新产品和分类时，必须转到这些属性以选择新项。 使用下列过程来配置要同步的分类和产品。  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

1.  在 **Configuration Manager** 控制台中，导航到“管理” > “站点配置” > “站点”。

2. 选择管理中心站点或独立主站点。  

3.  在“主页”  选项卡上的“设置”  组中，单击“配置站点组件” ，再单击“软件更新点” 。

4.  在“分类”  选项卡上，指定要为其同步软件更新的软件更新分类。  

    > [!NOTE]  
    >  每个软件更新都是利用更新分类定义的，此分类能帮助组织不同的更新类型。 同步过程中，将对指定的分类的软件更新元数据进行同步。 Configuration Manager 使你可将软件更新与下列更新分类进行同步：  
    >   
    > - **关键更新**：针对特定的问题指定广泛发布的更新，以解决与安全性无关的关键错误。  
    > - **定义更新**：指定对病毒定义文件或其他定义文件的更新。  
    > - **功能包**：指定新的产品功能，这些功能在产品版本以外分配，而且通常包含在下一个完整的产品版本中。  
    > - **安全更新**：针对特定于产品而且与安全性相关的问题指定广泛发布的更新。  
    > - **服务包**：指定一组累积的将应用于应用程序的修补程序。 这些修补程序可以包括：安全更新、关键更新、软件更新等。  
    > - **工具**：指定可帮助完成一项或多项任务的实用程序或功能。  
    > - **更新汇总**：指定一组累积的修补程序，它们打包在一起以便于部署。 这些修补程序可以包括安全更新、关键更新、其他更新等。 更新汇总通常解决特定领域的问题，例如安全性或产品组件问题。  
    > - **更新**：指定对已安装的应用程序或文件的更新。  
    > - **升级**：为 Windows 10 特性和功能指定升级。 软件更新点和站点必须运行最低具有[修补程序 3095113](https://support.microsoft.com/kb/3095113) 的 WSUS 4.0 来获取“升级”分类。    
    >       

    > [!NOTE]    
    > 从 Configuration Manager 版本 1706 开始，还可以选择“包括 Microsoft Surface 驱动程序和固件更新”复选框来同步 Microsoft Surface 驱动程序。 所有软件更新点都必须运行 Windows Server 2016 才能成功同步 Surface 驱动程序。     
    >    
    > 这是预发行功能。 预发行功能包含在产品中，用于在生产环境中进行早期测试，但不应将其视为生产就绪。 必须启用此功能，使其可供使用。 有关详细信息，请参阅[使用更新中的预发行功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。

5.  在“产品”  选项卡上，指定要为其同步软件更新的产品，然后单击“关闭” 。  

    > [!NOTE]  
    >  每个软件更新的元数据都定义了更新适用于的产品。 产品是指特定版本的操作系统或应用程序，例如 Microsoft Windows Server 2012。 产品家族是指从中派生单个产品的基本操作系统或应用程序。 产品系列的示例是 Windows，而 Windows Server 2012 是其成员之一。 可以指定产品系列或产品系列中的各个产品。 你选择的产品越多，同步软件更新所需的时间就越长。  
    >   
    >  在软件更新适用于多个产品，而且至少选择了一个要同步的产品时，即使没有选择某些产品，所有产品都将出现在 Configuration Manager 控制台中。 例如，Windows Server 2012 是你选择的唯一操作系统，而且软件更新应用于 Windows 8 和 Windows Server 2012，那么，这两个产品都将显示在 Configuration Manager 控制台中。  

    > [!IMPORTANT]  
    >  Configuration Manager 存储产品和产品系列的列表，你在初次安装软件更新点时可以从此列表中进行选择。 如果某些产品和产品系列是在发布 Configuration Manager 之后发布的，那么，在完成软件更新同步（这将更新可供你从中进行选择的可用产品和产品系列的列表）之前，可能无法选择它们。  

## <a name="next-steps"></a>后续步骤
启动软件更新同步以根据新条件检索软件更新。 有关详细信息，请参阅[同步软件更新](synchronize-software-updates.md)。
