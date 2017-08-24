---
title: "发布站点数据 | Microsoft Docs"
description: "了解如何将 Configuration Manager 站点发布到 Active Directory 域服务。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bcfb002c503485f03ba27d7346acb61d0d3c6087
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>发布 System Center Configuration Manager 的站点数据

*适用范围：System Center Configuration Manager (Current Branch)*

在为 System Center Configuration Manager 扩展 Active Directory 架构后，可将 Configuration Manager 站点发布到 Active Directory 域服务 (AD DS)。 这使 Active Directory 计算机能以从受信任的源中安全地检索站点信息。 尽管无需将站点信息发布到 AD DS 即可使用基本的 Configuration Manager 功能，但这么做可以减少管理开销。  

-   **将站点配置为发布到 AD DS 时**，Configuration Manager 客户端可通过 Active Directory 发布来自动查找管理点。 它们对全局编录服务器使用 LDAP 查询。  

-   **站点未发布到 AD DS 时**，客户端必须有备用机制来查找其默认管理点。  

有关客户端如何查找管理点的信息，请参阅[了解客户端如何查找 System Center Configuration Manager 的站点资源和服务](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

## <a name="configure-sites-to-publish-to-ad-ds"></a>将站点配置为发布到 AD DS  
 高级步骤如下：  

-   必须在要发布站点数据的每个林中[扩展 System Center Configuration Manager 的 Active Directory 架构](../../../../core/plan-design/network/extend-the-active-directory-schema.md)。 此外，还需确保存在“系统管理”容器。  

-   必须为每个将发布数据的主站点的计算机帐户授予对“系统管理”容器及其所有子对象的“完全控制”权限。  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>使 Configuration Manager 站点能够将站点信息发布到 Active Directory 林

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，并单击“站点” 。 选择要发布其站点数据的站点。 然后，在“主页”选项卡上的“属性”组中，单击“属性”。  

3.  在站点属性的“发布”选项卡上，选择此站点要将站点数据发布到其中的林。  

4.  单击“确定”  保存配置。  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>针对发布设置 Active Directory 林  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“Active Directory 林” 。 如果 Active Directory 林发现之前已运行，你将在结果窗格中看到每个发现的林。 当 Active Directory 林发现运行时，将发现本地林和任何受信任林。 只有不受信任的林才必须手动添加。  

    -   若要设置先前发现的林，请在结果窗格中选择林。 然后在“主页”选项卡上的“属性”组中，单击“属性”以打开林属性。 继续执行步骤 3。  

    -   若要设置未列出的新林，请在“主页”选项卡上的“创建”组中，单击“添加林”以打开“添加林”对话框。 继续执行步骤 3。  

3.  在“常规”选项卡上，为要发现的林完成配置，并指定“Active Directory 林帐户”。  

    > [!NOTE]  
    >  Active Directory 林发现需要全局帐户才能发现和发布到不受信任林。 如果不使用站点服务器的计算机帐户，则只能选择全局帐户。  

4.  如果你打算允许站点将站点数据发布到此林，请在“发布”  选项卡上完成用于发布到此林的配置。  

    > [!NOTE]  
    >  如果允许站点发布到林，则必须为 Configuration Manager 扩展该林的 Active Directory 架构。 Active Directory 林帐户必须对该林中的“系统”容器拥有“完全控制”权限。  

5.  完成配置此林以用于 Active Directory 林发现的操作后，单击 **OK** 保存配置。  
