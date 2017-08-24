---
title: "将用户和设备与用户设备相关性相链接 | Microsoft Docs"
description: "将用户和设备与用户设备相关性相链接，并自动将应用部署到与用户关联的所有设备。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4e8e677851ad9ae7d027ab685e842a8ff5e35573
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中将用户和设备与用户设备相关性相链接

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (Configuration Manager) 中的用户设备相关性将一个用户与一个或多个设备关联。 这样，在将应用程序部署到某用户时无需知道该用户的设备名称。 你将应用程序部署到该用户，而不是部署到该用户的每个设备。 之后，用户设备相关性会自动确保在所有与该用户关联的设备上安装应用程序。  

 可以定义主要设备，它们通常是用户每天在工作中使用的设备。 当在用户和设备之间创建相关性时，你会获得更多的软件部署选项。 例如，某用户需要 Microsoft Visio，那么，你可以使用 Windows Installer 部署将它安装在该用户的主要设备上。 但是，在不是主要设备的设备上，可能要将 Visio 部署为虚拟应用程序。 在用户未登录时，你还可以使用用户设备相关性将软件预先部署在用户的设备上，以便在用户登录时，应用程序已安装好并且可以运行了。  

 必须管理计算机的用户设备相关性信息。 Configuration Manager 会自动为它注册的移动设备管理用户设备相关性。  

## <a name="manually-set-up-user-device-affinity"></a>手动设置用户设备相关性  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “设备”。  

3.  从列表中选择一个设备。 然后，在“主页”选项卡的“设备”组中选择“编辑主要用户”。  

4.  在“编辑主要用户”对话框中，搜索并选择要添加为所选设备的主要用户的用户。 选择“添加”。  

    > [!NOTE]  
    > “主要用户”列表显示已成为此设备的主要用户的用户，以及使用了哪种方法来指定每项用户 - 设备关系。  

## <a name="set-up-primary-devices-for-a-user"></a>设置用户的主要设备  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “用户”。  

3.  从列表中选择一个用户。 然后，在“设备”选项卡中选择“编辑主要设备”。  

4.  在“编辑主要设备”对话框中，搜索并选择要添加为所选用户的主要设备的设备。 选择“添加”。  

    > [!NOTE]  
    > “主要设备”列表显示已设置为此用户的主要设备的设备，以及使用了哪种方法来指定每项用户-设备关系。  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>自动创建用户设备相关性（仅针对 Windows PC）  
 Configuration Manager 从 Windows 事件日志中读取有关用户登录的数据。 若要自动创建用户设备相关性，必须在客户端计算机上启用本地安全策略中的这两个选项，以便将登录事件存储在 Windows 事件日志中：  

-   **审核帐户登录事件**  
-   **审核登录事件**  

 要配置这些设置，请使用 Windows 组策略。  

> [!IMPORTANT]  
> 如果错误导致 Windows 事件日志生成大量条目，则可能将创建新的事件日志。 如果出现这种情况，现有的登录事件可能不再可供 Configuration Manager 使用。  
>   
> 在 Windows XP 中打开“审核帐户登录事件”和“审核登录事件”设置时请小心。 默认情况下，保留策略为 7 天，这些事件很有可能将填满安全事件日志。 如果事件日志已满，标准用户将无法登录。 为了避免该问题，对于安全事件日志，请将策略“保留方法”值设置为“按需要覆盖事件”。 为了使用户设备相关性有足够的数据，还要将“安全事件日志大小上限”策略设置为合理的值（例如 5-20 MB）。  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>将站点设置为自动创建用户设备相关性  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置”。  

2.  若要修改默认的客户端设置，请选择“默认客户端设置”，然后，在“主页”选项卡的“属性”组中选择“属性”。 若要创建自定义客户端代理设置，请选择“客户端设置”节点，然后，在“主页”选项卡的“创建”组中选择“创建自定义客户端设备设置”。  

    > [!NOTE]  
    > 如果修改默认的客户端设置，则它们将部署到层次结构中的所有计算机。 有关配置客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

3.  对于“用户和设备相关性”，进行如下设置：  

    -   **用户设备相关性阈值(分钟)**。 设置在创建用户设备相关性之前使用设备的分钟数。  

    -   **用户设备相关性阈值(天)**。 设置基于使用情况的相关性阈值的测量天数。  

    -   **利用使用情况数据自动配置用户设备相关性**。 要让站点自动创建用户设备相关性，请从下拉列表中选择 **True**。 如果选择 **False**，则必须批准所有的用户设备相关性分配。  

    > [!TIP]  
    > **例如：**如果将“用户设备相关性阈值(分钟)”指定为 **60** 分钟，并将“用户设备相关性阈值(天)”指定为 **5** 天，那么，用户必须在 5 天内使用设备至少 60 分钟，才能自动创建用户设备相关性。  

在自动创建用户设备相关性之后，Configuration Manager 会继续监视用户设备相关性阈值。 如果用户使用设备的时间降到所设置的阈值以下，则将删除用户设备相关性。 请将“用户设备相关性阈值(天)”的值设置为至少 **7** 天，以避免出现这种情况：在用户未登录时（例如在周末时），可能会丢失自动配置的用户设备相关性。  

## <a name="import-user-device-affinities-from-a-file"></a>从文件导入用户设备相关性  
 若要一次创建许多关系，可以导入具有多个用户设备相关性详细信息的文件。 对本过程而言，主体设备必须已被发现，而且作为 Configuration Manager 数据库中的资源存在，否则本过程将会失败。  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “用户”或“设备”。  

2.  在“主页”选项卡的“创建”组中，选择“导入用户设备相关性”。  

3.  在“导入用户设备相关性向导”的“选择映射”页上，设置下列信息：  

    -   **文件名**。 指定逗号分隔值 (CSV) 文件，该文件包含要创建用户设备相关性的用户和设备的列表。 在该文件中，每个用户和设备对都必须位于各自的行中，其值由逗号分隔。 使用格式：<*Domain*>&#92;<*user name*>,<*device NetBIOS name*>。  

    -   **此文件有供参考的列标题**。 如果 .csv 文件具有顶行标题，请选择此选项，在导入过程中将忽略标题行。  

4.  如果导入的文件在每行上包含两个以上的项目，则可以使用“列”和“分配”来指定哪些列代表用户和设备，以及在导入过程中要忽略哪些列。  

5.  选择“下一步”，然后完成“导入用户设备相关性向导”。  

## <a name="let-users-create-their-own-device-affinities"></a>让用户创建自己的设备相关性  
 通过后续过程，你可以设置来让用户可在软件中心应用中创建自己的用户设备相关性。  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>将站点设置为允许用户创建的用户设备相关性请求  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置”。  

2.  若要修改默认的客户端设置，请选择“默认客户端设置”，然后，在“主页”选项卡的“属性”组中选择“属性”。 若要创建自定义客户端代理设置，请选择“客户端设置”节点，然后，在“主页”选项卡的“创建”组中选择“创建自定义客户端用户设置”。  

    > [!NOTE]  
    > 如果修改默认的客户端设置，则它们将部署到层次结构中的所有计算机。 有关配置客户端设置的详细信息，请参阅[配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

3.  选择客户端设置“用户和设备相关性”  ，然后在“允许用户定义其主要设备”  下拉列表中，选择“真” 。  

### <a name="set-up-a-user-device-affinity"></a>设置用户设备相关性  

1.  在“应用程序目录”中，选择“我的系统”。  

2.  选择“我经常使用此计算机工作”选项。  

## <a name="manage-user-device-affinity-requests-from-users"></a>管理来自用户的用户设备相关性请求  
 在将客户端设置“利用使用情况数据自动配置用户设备相关性”  设为“假” 时，你必须批准所有的用户设备相关性分配。  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>批准或拒绝用户设备相关性请求  

1.  在 Configuration Manager 控制台中，选择“资产和符合性”。  

2.  在“资产和符合性”  工作区中，选择要为其管理相关性请求的用户或设备集合。  

3.  在“主页”选项卡的“集合”组中，选择“管理相关性请求”。  

4.  在“管理用户设备相关性请求”对话框中，选择一个相关性请求，然后选择“批准”或“拒绝”。  
