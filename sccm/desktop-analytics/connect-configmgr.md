---
title: 连接 Configuration Manager
titleSuffix: Configuration Manager
description: 使用桌面分析连接 Configuration Manager 的操作方法指南。
ms.date: 07/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 138cf7b8cc6c1279e72d7c620154f703581a9f49
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386619"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>如何通过桌面分析连接 Configuration Manager

桌面分析与 Configuration Manager 紧密集成。 首先，确保站点是最新的，以支持最新功能。 然后，在 Configuration Manager 中创建桌面分析连接。 最后，监视连接的运行状况。


## <a name="bkmk_hotfix"></a>更新站点

首先，请确保 Configuration Manager 站点运行的版本至少为1902。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。

还需要安装版本1902更新汇总（4500571），以支持与桌面分析集成。 有关此更新的详细信息，请参阅[版本 1902 Configuration Manager 当前分支的更新汇总](https://support.microsoft.com/help/4500571)。

1. 用版本1902的更新汇总更新站点。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。  

2. 更新客户端。 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  



## <a name="bkmk_connect"></a>连接到服务

使用此过程将 Configuration Manager 连接到桌面分析并配置设备设置。 此过程是将层次结构连接到云服务的一次性过程。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。 在功能区中选择 "**配置 Azure 服务**"。  

    > [!Tip]  
    > 在 Configuration Manager 控制台中，打开 "**软件库**" 工作区，然后选择 "**桌面分析服务**" 节点。 在 "*新到桌面分析"* 框中，选择第二个链接，将*Configuration Manager 连接到桌面分析服务*。  

2. 在 Azure 服务向导的 " **Azure 服务**" 页上，配置以下设置：  

    - 指定 Configuration Manager 中的对象名称。  

    - 指定可选说明以帮助标识服务。  

    - 从可用服务列表中选择 "**桌面分析**"。  
  
   选择“下一步”。  

3. 在 "**应用**" 页上，选择相应的**Azure 环境**。 然后选择 "**浏览**" "web 应用"。  

4. 如果你有想要为此服务重用的现有应用，请从列表中选择它，然后选择 **"确定"** 。  

5. 在大多数情况下，你可以使用此向导创建用于桌面分析连接的应用。 选择“创建”。<!-- 3572123 -->  

    > [!Tip]  
    > 如果无法从此向导创建应用，可以在 Azure AD 中手动创建应用，然后将其导入 Configuration Manager。 有关详细信息，请参阅[创建和导入用于 Configuration Manager 的应用](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager)。  

6. 在 "**创建服务器应用程序**" 窗口中配置以下设置：  

    - **应用程序名称**： Azure AD 中应用的友好名称。

    - **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它位于 Configuration Manager 客户端使用的访问令牌中，用于请求访问服务。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **密钥有效期**：从下拉列表中选择“1 年”或“2 年”。 默认值为一年。  

    选择 **"登录"** 。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称以供参考。
        
    > [!Note]  
    > 以**全局管理员身份**完成此步骤。 Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。  

    选择“确定”以在 Azure AD 中创建 Web 应用，并关闭“创建服务器应用程序”对话框。 在 "服务器应用" 对话框中，选择 **"确定"** 。 然后在 Azure 服务向导的 "应用" 页上选择 "**下一步**"。  

7. 在 "**诊断数据**" 页上，配置以下设置：  

    - **商业 id**：此值应自动填充你组织的 ID。 如果不是这样，请确保将代理服务器配置为允许所有所需的[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)，然后再继续。 或者，通过[桌面分析门户](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID)手动检索商业 ID。  

    - **Windows 10 诊断数据级别**：至少选择 "**基本**"。 查看[诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **允许诊断数据中的设备名称**：选择 "**启用**"  

        > [!Note]  
        > 从 Windows 10 版本1803开始，默认情况下，设备名称不会发送给 Microsoft。 如果不发送设备名称，它将在桌面分析中显示为 "未知"。 此行为可能会导致难以识别和评估设备。  

   选择“下一步”。 "**可用功能**" 页显示了可用于上一页中的诊断数据设置的桌面分析功能。 选择 "**下一步**" 继续或单击 "**上**一步" 进行更改。  

    ![Azure 服务向导中的 "可用功能示例" 页](media/available-functionality.png)

8. 在 "**集合**" 页上，配置以下设置：  

    - **显示名称**：桌面分析门户显示此 Configuration Manager 使用此名称的连接。 使用它来区分不同的层次结构。 例如，*测试实验室*或*生产环境*。  

    - **目标集合**：此集合包括 Configuration Manager 配置商业 ID 和诊断数据设置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。  

    - **目标集合中的设备使用用户身份验证的代理进行出站通信**：默认情况下，此值为 "**否**"。 如果你的环境中需要，请将设置为 **"是"** 。  

    - **选择要与桌面分析同步的特定集合**：选择 "**添加**" 以包括**目标集合**层次结构中的其他集合。 这些集合在桌面分析门户中提供，用于将部署计划分组。 请确保包括试验和试点排除集合。  <!-- 4097528 -->  

        > [!Tip]  
        > "选择集合" 窗口仅显示受**目标集合**限制的集合。
        >
        > 在下面的示例中，选择 "CollectionA" 作为目标集合。 然后，当你添加其他集合时，你将看到 CollectionA、CollectionB 和 CollectionC。 不能添加 CollectionD。
        >
        > - CollectionA：受 "**所有系统**" 集合的限制
        >     - CollectionB：受 CollectionA 的限制
        >         - CollectionC：受 CollectionB 的限制
        > - CollectionD：受 "**所有系统**" 集合的限制

        > [!Important]  
        > 这些集合将继续同步，因为其成员身份更改。 例如，你的部署计划使用具有 Windows 7 成员身份规则的集合。 当这些设备升级到 Windows 10，并 Configuration Manager 评估集合成员身份时，这些设备将拖出收集和部署计划。  


9. 完成向导。  

Configuration Manager 创建设置策略，以在目标集合中配置设备。 此策略包括诊断数据设置，使设备能够将数据发送到 Microsoft。 默认情况下，客户端每隔一小时更新一次策略。 接收到新设置后，可能需要几个小时才能在桌面分析中使用这些数据。



## <a name="bkmk_monitor"></a>监视连接运行状况

监视设备的配置以进行桌面分析。 在 Configuration Manager 控制台中，打开 "**软件库**" 工作区，展开 " **Desktop Analytics 服务**" 节点，然后选择 "**连接运行状况**" 仪表板。  

有关详细信息，请参阅[监视连接运行状况](/sccm/desktop-analytics/troubleshooting#monitor-connection-health)。

Configuration Manager 在创建连接的60分钟内同步集合。 在桌面分析门户中，中转到 "**全局试验**"，并查看 Configuration Manager 设备集合。



## <a name="next-steps"></a>后续步骤

转到下一篇文章，将设备注册到桌面分析。
> [!div class="nextstepaction"]  
> [注册设备](/sccm/desktop-analytics/enroll-devices)  
