---
title: 配置客户端设置
titleSuffix: Configuration Manager
description: 选择 System Center Configuration Manager 中的客户端设置。
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03485b4be2295676d125f3f3e28d2cd7d62728d3
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420050"
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置客户端设置

适用范围：*System Center Configuration Manager (Current Branch)*

可以从“管理” > “客户端设置”管理 System Center Configuration Manager 中的所有客户端设置。 如果要为层次结构中未应用任何自定义设置的所有用户和设备配置设置，请修改默认设置。 如果要将不同设置仅应用于某些用户或设备，请创建自定义设置并将它们部署到集合。  

有关每种客户端设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../core/clients/deploy/about-client-settings.md)。

> [!NOTE]  
>  你还可以使用配置项目来管理客户端，以便评估、跟踪和修正设备的配置符合性。 有关详细信息，请参阅[使用 System Center Configuration Manager 确保设备的合规性](../../../compliance/understand/ensure-device-compliance.md)。  

##  <a name="configure-the-default-client-settings"></a>配置默认客户端设置    

1. 在 Configuration Manager 控制台中，选择“管理” > “客户端设置” > “默认客户端设置”。  

2. 在“主页”选项卡上，选择“属性”。  

3. 在导航窗格中查看和配置每个设置组的客户端设置。  

   当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 若要为单一客户端启动策略检索，请参阅[如何管理 System Center Configuration Manager 中的客户端](../../../core/clients/manage/manage-clients.md)中的[为 Configuration Manager 客户端启动策略检索](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

##  <a name="create-and-deploy-custom-client-settings"></a>创建和部署自定义客户端设置  
部署这些自定义设置后，它们将覆盖默认客户端设置。 在开始此过程之前，请确保有一个集合，其中包含需要这些自定义客户端设置的用户或设备。  

1. 在 Configuration Manager 控制台中，选择“管理” > “客户端设置”。  

2. 在“主页”选项卡上的“创建”组中，选择“创建自定义客户端设备设置”，然后选择以下任意选项：  

   -   **创建自定义客户端设备设置**  

   -   **创建自定义客户端用户设置**  

3. 指定唯一名称和选项说明。  

4. 选择显示一组设置的一个或多个复选框。  

5. 从导航窗格中选择每组设置，然后配置可用设置，再单击“确定”。   

6. 选择创建的自定义客户端设置。 在“主页”选项卡上的“客户端设置”组中，选择“部署”。  

7. 在“选择集合”对话框中，选择合适的集合，然后选择“确定”。 如果在详细信息窗格中单击“部署”  选项卡，你可以验证所选的集合。  

8. 查看已创建的自定义客户端设置的顺序。 如果有多个自定义客户端设置，则会依据其序号应用这些设置。 如果存在任何冲突，则具有最低序号的设置优先于其他设置。 若要更改序号，请在“主页”选项卡上的“客户端设置”组中选择“上移项目”或“下移项目”。  

   当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 若要为单一客户端启动策略检索，请参阅[如何管理 System Center Configuration Manager 中的客户端](../../../core/clients/manage/manage-clients.md)中的[为 Configuration Manager 客户端启动策略检索](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  



##  <a name="view-client-settings"></a>查看客户端设置  
 如果已将多个客户端设置部署到同一设备、用户或用户组，则设置的优先顺序和组合会很复杂。 查看客户端设置：  

1.  在 Configuration Manager 控制台中，依次选择“资产和符合性” > “设备” > “用户”或“用户集合”。  

3.  在“客户端设置”  组中选择设备、用户或用户组，选择“产生的客户端设置” 。  

4.  从左边窗格中选择一个客户端设置，然后设置将会显示。 在此视图中，设置是只读的。 

    > [!NOTE]  
    >  若要查看客户端设置，必须对“客户端设置”具有读取权限。  

    