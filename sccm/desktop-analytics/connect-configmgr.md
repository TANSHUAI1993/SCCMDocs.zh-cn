---
title: 连接 Configuration Manager
titleSuffix: Configuration Manager
description: 与 Desktop 分析连接的配置管理器操作方法指南。
ms.date: 04/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 905ea779082387996858727ef8c50f1835b3d61c
ms.sourcegitcommit: 65753c51fbf596f233fc75a5462ea4a44005c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/03/2019
ms.locfileid: "66463017"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>如何将 Configuration Manager 和桌面分析

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

桌面 Analytics 与 Configuration Manager 紧密集成。 首先，请确保站点保持最新状态，以支持最新功能。 Configuration Manager 中，然后创建桌面 Analytics 连接。 最后，监视连接的运行状况。


## <a name="bkmk_hotfix"></a> 更新站点

首先，请确保至少运行 Configuration Manager 站点版本 1810年。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。

此外需要安装版本 1810年更新汇总 2 (4488598) 以支持与桌面 Analytics 的集成。 有关此更新的详细信息，请参阅[Configuration Manager current branch，版本 1810年更新汇总 2](https://support.microsoft.com/help/4488598)。

1. 使用版本 1810 的更新汇总更新站点。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。  

2. 更新客户端。 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  



## <a name="bkmk_connect"></a> 连接到服务

使用此过程将配置管理器连接到桌面 Analytics，并配置设备设置。 此过程是一次性的过程来将你的层次结构附加到云服务。  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。 选择**配置 Azure 服务**功能区中。  

2. 上**Azure 服务**页上的 Azure 服务向导配置以下设置：  

    - 指定 Configuration Manager 中的对象名称  。  

    - 指定可选说明以帮助标识服务  。  

    - 选择**Desktop 分析**从可用服务列表。  
  
   选择“下一步”  。  

3. 上**应用程序**页上，选择相应**Azure 环境**。 然后选择**浏览**为 web 应用。  

4. 如果有现有应用程序想要重复使用此服务，从列表中，选择它，然后选择**确定**。  

5. 在大多数情况下，可以使用此向导创建桌面 Analytics 连接的应用。 选择“创建”  。<!-- 3572123 -->  

    > [!Tip]  
    > 如果无法通过此向导创建应用程序，可以在 Azure AD 中手动创建应用程序，然后导入 Configuration Manager。 有关详细信息，请参阅[创建和导入应用程序为 Configuration Manager](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager)。  

6. 配置中的以下设置**创建服务器应用程序**窗口：  

    - **应用程序名称**：Azure AD 中应用的友好名称。

    - **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它是访问令牌中用于由 Configuration Manager 客户端请求服务的访问权限。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **密钥有效期**：从下拉列表中选择“1 年”或“2 年”   。 默认值为一年。  

    选择**登录**。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称  以供参考。
        
    > [!Note]  
    > 完成此步骤作为**公司管理员**。Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。  

    选择“确定”以在 Azure AD 中创建 Web 应用，并关闭“创建服务器应用程序”对话框  。 在服务器应用对话框中，选择**确定**。 然后选择**下一步**Azure 服务向导的应用页上。  

7. 上**诊断数据**页上，配置以下设置：  

    - **商用 ID**： 此值应自动填充你的组织 id。 如果没有，请确保你的代理服务器配置为允许所需的所有[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)然后再继续。 或者，从商业 ID 来检索**连接的服务**窗格中的[Desktop 分析门户](https://aka.ms/m365aprod)。  

    - **Windows 10 诊断数据级别**： 选择至少**增强 （受限）**  

    - **允许诊断数据中的设备名称**： 选择**启用**  

        > [!Note]  
        > 从 Windows 10 1803年版开始，设备名称不是发送给 Microsoft 默认情况下。 如果不发送设备名称，它显示在桌面分析为"未知"。 此行为可以使难以确定和评估设备。  

   选择“下一步”  。 **可用的功能**页显示桌面的分析功能，可使用前一页中的诊断数据设置。 选择**下一步**以继续或**上一步**进行更改。  

    ![Azure 服务向导中的示例中可用的功能页](media/available-functionality.png)

8. 上**集合**页上，配置以下设置：  

    - **显示名称**：Desktop 分析门户会显示此 Configuration Manager 连接，使用此名称。 使用它来区分不同的层次结构。 例如，*测试实验室*或*生产*。  

    - **目标集合**:此集合包含所有设备，配置管理器配置商业 ID 和诊断数据设置。 它是完整的配置管理器连接到桌面 Analytics 服务的设备集。  

    - **目标集合中的设备使用用户身份验证代理进行出站通信**:默认情况下，此值是**否**。 如果需要在环境中，将设置为**是**。  

    - **选择要与桌面 Analytics 同步的特定集合**:选择**外**以包括其他集合从你**目标集合**层次结构。 这些集合是可在部署计划及分组 Desktop 分析门户中。 请确保包括试验和试验的排除集合。  <!-- 4097528 -->  

        > [!Important]  
        > 这些集合继续作为其成员身份的更改进行同步。 例如，你的部署计划使用一组与 Windows 7 的成员身份规则。 在这些设备升级到 Windows 10 和 Configuration Manager 将评估集合成员身份时，这些设备将删除超出集合和部署计划。  


9. 完成向导。  

Configuration Manager 创建一个设置策略来配置目标集合中的设备。 此策略包括要使设备能够向 Microsoft 发送数据的诊断数据设置。 默认情况下，客户端每隔一小时更新策略。 收到后的新设置，它可以是几个小时，更多数据之前在桌面 Analytics 中可用。



## <a name="bkmk_monitor"></a> 监视连接运行状况

监视桌面分析你的设备的配置。 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**Desktop 分析服务**节点，然后选择**连接运行状况**仪表板。  

有关详细信息，请参阅[监视连接运行状况](/sccm/desktop-analytics/troubleshooting#monitor-connection-health)。

Configuration Manager 在创建连接的 60 分钟内同步集合。 在 Desktop 分析门户中，转到**全局试点**，并查看 Configuration Manager 设备集合。



## <a name="next-steps"></a>后续步骤

转到下一步的文章，设备注册到 Desktop 分析。
> [!div class="nextstepaction"]  
> [注册设备](/sccm/desktop-analytics/enroll-devices)  
