---
title: "定义边界 | Microsoft Docs"
description: "了解如何在 Intranet 上定义可包含你要管理的设备的网络位置。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bed70809008fde5e2b0215f4dce049402edf83ba
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>将网络位置定义为 System Center Configuration Manager 的边界

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 边界是网络上的位置，其中包含你要管理的设备。 设备所在的边界相当于 Active Directory 站点，或由安装在设备上的 Configuration Manager 客户端指定的网络 IP 地址。
 - 你可以手动创建单个边界。 但是，Configuration Manager 不支持以边界的形式直接输入超网。 作为替代，请使用 IP 地址范围边界类型。
 - 可以将 [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) 方法配置成为每个 IP 子网和其发现的 Active Directory 站点自动发现并创建边界。 当 Active Directory 林发现确定分配给 Active Directory 站点的超网时，Configuration Manager 将超网转换为 IP 地址范围边界。  

设备使用 Configuration Manager 管理员感知不到的 IP 地址的情况并不罕见。 当不确定设备的网络位置时，请通过在设备上使用 **IPCONFIG** 命令确认设备所报告的自身位置。  

当你创建边界时，边界会自动获得一个名称，该名称基于边界的类型和作用域。 你无法修改此名称。 作为替代方式，你可以指定一个描述以帮助在 Configuration Manager 控制台中标识该边界。  

每个边界都可供层次结构中的每个站点使用。 创建边界之后，你可以修改其属性以执行以下操作：  
-   将边界添加到一个或多个边界组。  
-   更改边界的类型或作用域。  
-   查看边界“站点系统”  选项卡以了解哪些站点系统服务器（分发点、状态迁移点和管理点）与边界相关联。  

## <a name="to-create-a-boundary"></a>创建边界  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” > “边界”  

2.  在“主页”  选项卡上的“创建”  组中，单击“创建边界”  **Boundary.**。  

3.  在“创建边界”对话框的“常规”  选项卡上，你可以指定“描述”  以便通过友好名称或引用来标识边界。  

4.  为此边界选择“类型”  ：  

    -   如果选择“IP 子网” ，你必须为此边界指定“子网 ID”  。  
        > [!TIP]  
        >  你可以指定“网络”  和“子网掩码”  以便自动指定“子网 ID”  。 在保存边界时，只会保存子网 ID 值。  

    -   如果选择“Active Directory 站点” ，则必须指定或“浏览”  到站点服务器的本地林中的 Active Directory 站点。  

        > [!IMPORTANT]  
        >  如果为边界指定 Active Directory 站点，则边界包括作为该 Active Directory 站点成员的每个 IP 子网。 如果 Active Directory 站点的配置在 Active Directory 中发生变化，则此边界中包括的网络位置也会更改。  

    -   如果选择“IPv6 前缀” ，你必须以 IPv6 前缀格式指定“前缀”  。  

    -   如果选择“IP 地址范围” ，你必须指定包括 IP 子网的一部分或包括多个 IP 子网的“起始 IP 地址”  和“结束 IP 地址”  。    

5.  单击“确定”  保存新边界。  

## <a name="to-configure-a-boundary"></a>配置边界  

1.  在 Configuration Manager 控制台中，单击“管理” > “层次结构尊重” > “边界”  

2.  选择要修改的边界。  

3.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

4.  在边界的“属性”  对话框中，选择“常规”  选项卡以编辑边界的“描述”  或“类型”  。 你也可以通过编辑边界的网络位置来更改边界的作用域。 例如，对于 Active Directory 站点边界，你可以指定新的 Active Directory 站点名称。  

5.  选择“站点系统”  选项卡以查看与此边界关联的站点系统。 你无法从边界的属性中更改此配置。  

    > [!TIP]  
    >  对于列为边界的站点系统的站点系统服务器，站点系统服务器必须关联为包含此边界的至少一个边界组的站点系统服务器。 这配置在边界组的“引用”  选项卡上。  

6.  选择“边界组”  选项卡以修改此边界的边界组成员身份：  

    -   要将此边界添加到一个或多个边界组，请单击“添加” ，选中一个或多个边界组的复选框，然后单击“确定” 。  

    -   要从某个边界组中删除此边界，请选择该边界组，然后单击“删除” 。  

7.  单击“确定”  关闭边界属性并保存配置。  
