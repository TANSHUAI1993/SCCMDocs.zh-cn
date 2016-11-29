---
title: "发布站点数据 | System Center Configuration Manager"
description: "了解如何将 Configuration Manager 站点发布到 Active Directory 域服务。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cda87a3bdcbba342f111b68af75369ca14744441


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>发布 System Center Configuration Manager 的站点数据

*适用范围：System Center Configuration Manager (Current Branch)*

为 System Center Configuration Manager 扩展 Active Directory 架构之后，可以将 Configuration Manager 站点发布到 Active Directory 域服务 (AD DS)，以便 Active Directory 计算机能够安全地从受信任来源检索站点信息。 尽管基本 Configuration Manager 功能无需将站点信息发布到 AD DS，但此配置可以减少管理开销。  

-   **将站点配置为发布到 AD DS 时**，Configuration Manager 客户端可使用对全局目录服务器的 LDAP 查询通过 Active Directory 发布来自动查找管理点。  

-   **站点未发布到 AD DS 时**，客户端必须有备用机制来查找其默认管理点。  

有关客户端如何查找管理点的信息，请参阅[了解客户端如何查找 System Center Configuration Manager 的站点资源和服务](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

## <a name="configure-sites-to-publish-to-ad-ds"></a>将站点配置为发布到 AD DS  
 高级步骤如下：  

-   必须在要发布站点数据的每个林中[扩展 System Center Configuration Manager 的 Active Directory 架构](../../../../core/plan-design/network/extend-the-active-directory-schema.md)，并确保存在“系统管理”。  

-   必须为每个将要发布数据的主站点的计算机帐户授予对   **系统管理** 容器及其所有子对象的 **完全控制** 权限。  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>使 Configuration Manager 站点能够将站点信息发布到 Active Directory 林：  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置”  ，并单击“站点” 。 选择要配置为发布其站点数据的站点，然后在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

3.  在站点属性的“发布”  选项卡上，选择此站点将向其中发布站点数据的林。  

4.  单击“确定”  保存配置。  

 使用以下过程配置用于发布的 Active Directory 林：  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>针对发布配置 Active Directory 林：  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“Active Directory 林” 。 如果 Active Directory 林发现之前已运行，你将在结果窗格中看到每个发现的林。 当 Active Directory 林发现运行时，将发现本地林和任何受信任林。 只有不受信任的林才必须手动添加。  

    -   要配置以前发现的林，请在结果窗格中选择该林，然后在“主页”  选项卡上的“属性”  组中单击“属性”  以打开林属性。 继续执行步骤 3。  

    -   要配置未列出的新林，请在“主页”  选项卡上的“创建”  组中单击“添加林”  以打开“添加林”  对话框。 继续执行步骤 3。  

3.  在“常规”  选项卡上，为要发现的林完成配置，并指定“Active Directory 林帐户” 。  

    > [!NOTE]  
    >  Active Directory 林发现需要全局帐户才能发现和发布到不受信任林。 如果不使用站点服务器的计算机帐户，则只能选择全局帐户。  

4.  如果你打算允许站点将站点数据发布到此林，请在“发布”  选项卡上完成用于发布到此林的配置。  

    > [!NOTE]  
    >  如果使站点能够发布到林，你必须为 Configuration Manager 扩展该林的 Active Directory 架构，并且 Active Directory 林帐户必须对该林中的“系统”容器具有“完全控制”权限。  

5.  完成配置此林以用于 Active Directory 林发现的操作后，单击 **OK** 保存配置。  



<!--HONumber=Nov16_HO1-->


