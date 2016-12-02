---
title: "配置客户端设置 | System Center Configuration Manager"
description: "选择 System Center Configuration Manager 中的客户端设置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置客户端设置

*适用范围：System Center Configuration Manager (Current Branch)*

通过 Configuration Manager 控制台“管理”工作区中的“客户端设置”节点来管理 System Center Configuration Manager 中的所有客户端设置。 如果要为层次结构中未应用任何自定义设置的所有用户和设备配置设置，请修改默认设置。 如果要将不同设置仅应用于某些用户或设备，请创建自定义设置并将它们部署到集合。  

> [!NOTE]  
>  你还可以使用配置项目来管理客户端，以便评估、跟踪和修正设备的配置符合性。 有关详细信息，请参阅[使用 System Center Configuration Manager 确保设备的合规性](../../../compliance/understand/ensure-device-compliance.md)。  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> 如何配置默认客户端设置  

 使用以下过程为层次结构中的所有客户端配置默认客户端设置。  

#### <a name="to-configure-the-default-client-settings"></a>配置默认客户端设置  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” ，然后选择“默认客户端设置” 。  

3.  在“主页”  选项卡上，单击“属性” 。  

4.  在导航窗格中查看和配置每个设置组的客户端设置。 有关每种设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../core/clients/deploy/about-client-settings.md)。  

5.  单击 **确定** 关闭 **默认客户端设置** 对话框。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 若要为单一客户端启动策略检索，请参阅[如何管理 System Center Configuration Manager 中的客户端](../../../core/clients/manage/manage-clients.md)中的[为 Configuration Manager 客户端启动策略检索](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> 如何创建和部署自定义客户端设置  
 使用以下过程为所选的用户或设备集合配置和部署自定义设置。 部署这些自定义设置后，它们将覆盖默认客户端设置。  

> [!NOTE]  
>  在开始此过程之前，请确保有一个集合，其中包含需要这些自定义客户端设置的用户或设备。  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>配置和部署自定义客户端设置  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建自定义客户端设置” ，然后单击以下选项之一，具体情况取决于你是要为设备还是用户创建自定义客户端设置：  

    -   **创建自定义客户端设备设置**  

    -   **创建自定义客户端用户设置**  

4.  在“创建自定义设备设置”  或“创建自定义用户设置”  对话框中，为自定义设置指定唯一名称以及可选的描述。  

5.  选中显示一组设置的一个或多个可用复选框。  

6.  从导航窗格中单击第一个组设置，然后查看和配置可用自定义设置。 为任何其余组设置重复此过程。 有关每种客户端设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../core/clients/deploy/about-client-settings.md)。  

7.  单击“确定”  关闭“创建自定义设备设置”  或“创建自定义用户设置”  对话框。  

8.  选择刚刚创建的自定义客户端设置。 在“主页”  选项卡上的“客户端设置”  组中，单击“部署” 。  

9. 在“选择集合”  对话框中，选择包含要使用自定义设置配置的设备或用户的集合，然后单击“确定” 。 如果在详细信息窗格中单击“部署”  选项卡，你可以验证所选的集合。  

10. 查看刚刚创建的自定义客户端设置的顺序。 如果有多个自定义客户端设置，则会依据其序号应用这些设置。 如果存在任何冲突，则具有最低序号的设置优先于其他设置。 要更改序号，请在“主页”  选项卡上的“客户端设置”  组中单击“上移项目”  或“下移项目” 。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 若要为单一客户端启动策略检索，请参阅[如何管理 System Center Configuration Manager 中的客户端](../../../core/clients/manage/manage-clients.md)中的[为 Configuration Manager 客户端启动策略检索](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> 如何查看生成的客户端设置  
 如果已将多个客户端设置部署到同一设备、用户或用户组，则设置的优先顺序和组合可能会很复杂。 使用下列过程来查看计算出的产生的客户端设置。  

#### <a name="to-view-the-resultant-client-settings"></a>查看产生的客户端设置  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“设备” 、“用户” 或“用户集合” 。  

3.  在“客户端设置”  组中选择设备、用户或用户组，选择“产生的客户端设置” 。  或者，你可以右键单击设备、用户或用户组，选择“客户端设置” ，并单击“产生的客户端设置” 。  

4.  从左边窗格中选择一个客户端设置，产生的设置将会显示。  

    > [!NOTE]  
    >  若要查看产生的客户端设置，已登录用户必须对客户端设置具有读取权限。  

    > [!NOTE]  
    >  所显示的产生的设置为只读。 若要修改任何设置，请使用上面的过程。  



<!--HONumber=Nov16_HO1-->


