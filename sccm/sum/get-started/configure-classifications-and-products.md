---
title: 配置分类和产品
titleSuffix: Configuration Manager
description: 按照以下步骤在 Configuration Manager 控制台中配置要同步的软件更新分类和产品。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/15/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1d984598288434aa1e81c6bd2c51a315edfa551
ms.sourcegitcommit: fd16fc2b681608fd6def5bad2cedffbcd1f2423a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2019
ms.locfileid: "56405686"
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

适用范围：System Center Configuration Manager (Current Branch)


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
    > - **关键更新**：指定为特定问题广泛发布的修复，旨在解决与安全无关的关键 bug。  
    > - **定义更新**：指定广泛发布且频率较高的软件更新，其中包含对产品的定义数据库的新增内容。  
    > - **功能包**：指定新的产品功能，这些功能首次在产品版本以外分发，而且通常包含在下一个完整的产品版本中。  
    > - **安全更新**：指定一个广泛发布的修复程序，旨在修复特定于产品的安全相关漏洞。  
    > - **服务包**：指定一个经过测试、逐渐累积的集合，其中包含所有的修补程序、安全更新、关键更新和应用于某个产品的更新。 此外，服务包可能还包含旨在解决产品发布以来内部发现的问题的其他修补程序。  
    > - **工具**：指定可帮助完成一项或多项任务的实用程序或功能。  
    > - **更新汇总**：指定为便于部署而一起打包的修补程序、安全更新、关键更新和其他更新的经过测试的累积集合。 更新汇总通常解决特定领域的问题，例如安全性或产品组件问题。  
    > - **更新**：指定广泛发布的针对特定问题的修补程序。 更新解决了非关键且与安全无关的 bug。  
    > - **升级**：为 Windows 10 特性和功能指定升级。 软件更新点和站点必须运行最低具有[修补程序 3095113](https://support.microsoft.com/kb/3095113) 的 WSUS 4.0 来获取“升级”分类。    
    >       

    > [!NOTE]    
    > 从 Configuration Manager 版本 1706 开始，可以选中“包括 Microsoft Surface 驱动程序和固件更新”复选框来同步 Microsoft Surface 驱动程序。<!--1098490--> 所有软件更新点都必须运行 Windows Server 2016 才能成功同步 Surface 驱动程序。 如果启用 Surface 驱动程序后，在运行 Windows Server 2012 的计算机上启用软件更新点，则驱动程序更新的扫描结果不准确。 这会导致在 Configuration Manager 控制台和 Configuration Manager 报表中显示不正确的符合性数据。  
    >  
    > 此功能在 1706 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从版本 1710 开始，此功能不再属于预发行功能。  
    >  
    > 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  

5.  在“产品”  选项卡上，指定要为其同步软件更新的产品，然后单击“关闭” 。  

    > [!NOTE]  
    >  每个软件更新的元数据都定义了更新适用于的产品。 产品是指特定版本的操作系统或应用程序，例如 Microsoft Windows Server 2012。 产品家族是指从中派生单个产品的基本操作系统或应用程序。 产品系列的示例是 Windows，而 Windows Server 2012 是其成员之一。 可以指定产品系列或产品系列中的各个产品。 选择的产品越多，同步软件更新所需的时间就越长。  
    >   
    >  在软件更新适用于多个产品，而且至少选择了一个要同步的产品时，即使没有选择某些产品，所有产品也会出现在 Configuration Manager 控制台中。 例如，Windows Server 2012 是你选择的唯一操作系统，而且软件更新适用于 Windows 8 和 Windows Server 2012，那么，这两个产品都会显示在 Configuration Manager 控制台中。  

    > [!IMPORTANT]  
    >  Configuration Manager 存储产品和产品系列的列表，你在初次安装软件更新点时可以从此列表中进行选择。 如果某些产品和产品系列是在发布 Configuration Manager 之后发布的，那么，在完成软件更新同步（这将更新可供你从中进行选择的可用产品和产品系列的列表）之前，可能无法选择它们。  

## <a name="next-steps"></a>后续步骤
启动软件更新同步以根据新条件检索软件更新。 有关详细信息，请参阅[同步软件更新](synchronize-software-updates.md)。
