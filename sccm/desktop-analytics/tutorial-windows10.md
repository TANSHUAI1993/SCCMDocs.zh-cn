---
title: 教程-部署 Windows 10
titleSuffix: Configuration Manager
description: 使用桌面 Analytics 和 Configuration Manager 将 Windows 10 部署到试验组的教程。
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f49955fed92061fb856a5ff49203f1fa6c9d186
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285626"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>教程：将 Windows 10 部署到试点

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

本教程使用桌面 Analytics 和 Configuration Manager 将 Windows 10 部署到试验组。 它会突出显示要提供见解与内部部署产品部署 Windows 云服务的集成。 使用 Desktop 分析来确定要在试验组中放置的最佳设备。 然后使用 Configuration Manager 以获取当前的 Windows。

在本教程中，您学习如何：  

> [!div class="checklist"]  
> * 在 Azure 门户中进行桌面分析设置  
> * 将 Configuration Manager 连接和配置设备设置  
> * 创建适用于 Windows 10 桌面分析部署计划  
> * 使用配置管理器将 Windows 10 部署到试运行组  

如果还没有 Azure 订阅，创建[免费帐户](https://azure.microsoft.com/free)在开始之前。 正确配置后，使用 Desktop Analytics 不会产生任何 Azure 费用。

使用桌面分析*Log Analytics 工作区*在 Azure 订阅中。 工作区是实质上是包含帐户信息和帐户简单配置信息的容器。 有关详细信息，请参阅[管理的工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json)。



## <a name="prerequisites"></a>先决条件

在开始本教程之前，请确保具备以下先决条件：  

- 有效的 Azure 订阅，使用[**全局管理员**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator)权限  

    有关详细信息，请参阅[Desktop 分析先决条件](/sccm/desktop-analytics/overview#prerequisites)。

- Configuration Manager，版本 1902年更新汇总 (4500571) 或更高版本，具有**完全权限管理员**角色  

- 针对 Windows 10 的最新版本的安装介质

- 使用以下配置至少一个 Windows 10 设备：  

    - Windows 10 版本 1709年或更高版本，但小于你打算使用该安装媒体的版本

    - 最新的 Windows 10 累积质量更新  

    - Configuration Manager 客户端版本 1902年更新汇总 (4500571) 或更高版本  

- 若要配置到 Windows 诊断数据级别的业务审批**增强 （受限）** 试验设备上  

    有关详细信息，请参阅[Desktop 分析隐私](/sccm/desktop-analytics/privacy)。

- 从设备到以下 internet 终结点网络连接：

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` （在仅 Configuration Manager 服务器角色）
    - `https://fef.msua06.manage.microsoft.com` （在仅 Configuration Manager 服务器角色）

    有关详细信息，请参阅[如何启用数据共享桌面分析](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

> [!Important]  
> 这些系统必备组件都用于本教程的目的。 有关桌面 Analytics 和 Configuration Manager 的常规先决条件的详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。  



## <a name="set-up-desktop-analytics"></a>设置桌面分析

使用此过程中登录到桌面分析并将其配置你的订阅中。 此过程是一次性的过程来为你的组织设置 Desktop 分析。  

1. 打开[Desktop 分析门户](https://aka.ms/desktopanalytics)中的用户的 Microsoft 365 设备管理**全局管理员**权限。 选择**启动**。  

2. 上**接受服务协议**页上，查看服务协议，然后选择**接受**。  

3. 上**确认你的订阅**页上，需符合条件的许可证的列表适用于 Windows 设备运行状况分析功能的桌面。 选择“下一步”继续操作  。  

4. 上**授予用户访问权限**页：

    - **执行要管理目录角色为你的用户桌面 Analytics**:桌面分析自动分配**工作区所有者**并**工作区参与者**到组**Desktop 分析管理员**角色。 如果这些组已经**全局管理员**，没有任何更改。  

        如果不选择此选项，则桌面分析仍将用户添加为两个安全组的成员。 一个**全局管理员**需要手动分配**Desktop 分析管理员**角色的用户。  

        有关如何将 Azure Active Directory 中的管理员角色权限和权限分配给分配的详细信息**Desktop 分析管理员**，请参阅[在 Azure 中的管理员角色权限Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles)。  

    - 桌面分析会预先配置 Azure Active Directory 中的两个安全组：  

        - **工作区所有者**:要创建和管理工作区的安全组。 这些帐户需要对 Azure 订阅所有者访问权限。  

        - **工作区参与者**:要创建和管理此工作区中的部署计划的安全组。 它们不需要任何其他的 Azure 访问权限。  

        若要将用户添加到这两个组中，键入在其名称或电子邮件地址**输入名称或电子邮件地址**相应的组的部分。 完成后，选择**下一步**。

5. 在到页**设置工作区**:  

    > [!Note]  
    > 完成此步骤作为**工作区所有者**或**参与者**。 有关详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。  

    - 选择你的 Azure 订阅。  

    - 若要使用 Desktop 分析现有的工作区，选择它，并继续下一步。  

    - 若要为 Desktop 分析创建一个工作区，选择**添加工作区**。  

        1. 输入**工作区名称**。  

        2. 选择的下拉列表**选择此工作区的 Azure 订阅名称**，然后选择此工作区的 Azure 订阅。  

        3. **创建新**资源组或**使用现有**。  

        4. 选择**地区**从列表中，然后选择**添加**。  

6. 选择新的或现有工作区中，并选择**设置为桌面 Analytics 工作区**。  然后选择**继续**中**确认和授予访问权限**对话框。  

7. 在新的浏览器选项卡上，选择要用于登录的帐户。 选择选项**代表你的组织同意**，然后选择**接受**。  


    > [!Note]  
    > 此许可是将 MALogAnalyticsReader 应用程序分配工作区的 Log Analytics 读者角色。 此应用程序角色是桌面分析所需。 有关详细信息，请参阅[MALogAnalyticsReader 应用程序角色](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader)。  

8. 恢复到页面上**设置工作区**，选择**下一步**。  

9. 上**最后步骤**页上，选择**转到桌面分析**。 Azure 门户显示桌面分析**主页**页。  



## <a name="connect-configuration-manager"></a>连接 Configuration Manager

此过程用于更新配置管理器，连接到 Desktop 分析并配置设备设置。 此过程是一次性的过程来将你的层次结构附加到云服务。  

### <a name="update-configuration-manager"></a>更新 Configuration Manager

安装 Configuration Manager 版本 1902年更新汇总 (4500571) 以支持与桌面 Analytics 的集成。 有关此更新的详细信息，请参阅[更新的 Configuration Manager current branch，版本 1902年汇总](https://support.microsoft.com/help/4500571)。

1. 将站点更新版本 1902年的更新汇总。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。  

2. 更新客户端。 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  


### <a name="connect-to-the-service"></a>连接到服务

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。 选择**配置 Azure 服务**功能区中。  

2. 上**Azure 服务**页上的 Azure 服务向导配置以下设置：  

    - 指定**名称**Configuration Manager 中的对象  

    - 指定一个可选**说明**以帮助你识别该服务  

    - 选择**Desktop 分析**从可用服务列表  
  
   选择“下一步”  。  

3. 上**应用程序**页上，选择相应**Azure 环境**。 然后选择**浏览**为 web 应用。

4. 选择**创建**可以轻松地添加 Desktop 分析连接的 Azure AD 应用。

5. 配置中的以下设置**创建服务器应用程序**窗口：  

    - **应用程序名称**：Azure AD 中应用的友好名称。

    - **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它是访问令牌中用于由 Configuration Manager 客户端请求服务的访问权限。 默认情况下，此值为 `https://ConfigMgrService`。  

    - **密钥有效期**：从下拉列表中选择“1 年”或“2 年”   。 默认值为一年。  

    选择**登录**。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称  以供参考。

    > [!Note]  
    > 完成此步骤作为**公司管理员**。Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。  

    选择“确定”以在 Azure AD 中创建 Web 应用，并关闭“创建服务器应用程序”对话框  。 在服务器应用对话框中，选择**确定**。 然后选择**下一步**Azure 服务向导的应用页上。  

6. 上**诊断数据**页上，配置以下设置：  

    - **商用 ID**： 此值应自动填充你的组织 id  

    - **Windows 10 诊断数据级别**： 选择至少**增强 （受限）**  

    - **允许诊断数据中的设备名称**： 选择**启用**  
  
   选择“下一步”  。 **可用的功能**页显示桌面的分析功能，可使用前一页中的诊断数据设置。 选择“下一步”  。  

7. 上**集合**页上，配置以下设置：  

    - **显示名称**：Desktop 分析门户会显示此 Configuration Manager 连接，使用此名称。 使用它来区分不同的层次结构。 例如，*测试实验室*或*生产*。  

    - **目标集合**:此集合包含所有设备，配置管理器配置商业 ID 和诊断数据设置。 它是完整的配置管理器连接到桌面 Analytics 服务的设备集。  

    - **目标集合中的设备使用用户身份验证代理进行出站通信**:默认情况下，此值是**否**。 如果需要在环境中，将设置为**是**。  

    - **选择要与桌面 Analytics 同步的特定集合**:选择**添加**以包括其他集合。 这些集合是可在部署计划及分组 Desktop 分析门户中。 请确保包括试验和试验的排除集合。  

        这些集合继续作为其成员身份的更改进行同步。 例如，你的部署计划使用一组与 Windows 7 的成员身份规则。 在这些设备升级到 Windows 10 和 Configuration Manager 将评估集合成员身份时，这些设备将删除超出集合和部署计划。  

8. 完成向导。  

Configuration Manager 创建一个设置策略来配置目标集合中的设备。 此策略包括要使设备能够向 Microsoft 发送数据的诊断数据设置。 默认情况下，客户端每隔一小时更新策略。 收到后的新设置，它可以是几个小时，更多数据之前在桌面 Analytics 中可用。

> [!Note]  
> 有关这些设置的详细信息，请参阅[Windows 设置](/sccm/desktop-analytics/enroll-devices#windows-settings)。  

监视桌面分析你的设备的配置。 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**Desktop 分析服务**节点，然后选择**连接运行状况**仪表板。  

Configuration Manager 在创建连接的 60 分钟内同步集合。 在 Desktop 分析门户中，转到**全局试点**，并查看 Configuration Manager 设备集合。


## <a name="create-a-desktop-analytics-deployment-plan"></a>创建桌面分析部署计划

使用此过程在桌面 Analytics 中创建部署计划。

1. 打开[Desktop 分析门户](https://aka.ms/desktopanalytics)。 使用凭据至少具有**工作区参与者**权限。  

2. 选择**部署计划**管理组中。  

3. 在中**部署计划**窗格中，选择**创建**。  

4. 在中**创建部署计划**窗格中，配置以下设置：  

    - **名称**：唯一的名称为部署计划例如 `Windows 10 pilot`  

    - **产品和版本**:选择**Windows**产品和最新的可用建议的版本。 例如， **Windows 10，版本 （推荐） 1809年**。  

    - **设备组**:从配置管理器选项卡，选择一个或多个组，然后选择**设置为目标组**。 这些组是从 Configuration Manager 同步的集合。  

    - **准备情况规则**:这些规则帮助确定哪些设备有资格获得升级。 选择**WIndows OS**和配置下列设置：  

        - **我的计算机自动从 Windows Update 中获取驱动程序**:默认设置是**关闭**，建议部署与 Configuration Manager 时。  

        - **定义您的应用程序的低安装计数阈值**:默认设置是`2%`。 低于此阈值的应用程序将自动设置为*低安装计数*。 桌面分析在试用期间不会验证这些加载项。  

            如果百分比大于此阈值更高版本的计算机上安装应用，部署计划将标记应用作为*Noteworthy*。 然后可以决定要在试验阶段测试其重要性。  

    - **完成日期**:选择依据 Windows 应完全部署到所有目标设备的日期。  

5. 选择“创建”  。 其正在处理时，在部署计划列表中显示新的计划。 若要加快处理，请求按需数据刷新。 有关详细信息，请参阅[Desktop 分析常见问题](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)。

6. 选择其名称以打开部署计划。  

7. 在部署计划菜单上，在**准备**组中，选择**识别重要性**。  

    1. 上**应用程序**选项卡上，选择此选项可以仅显示**未检查**资产。  

    2. 选择每个应用，并选择**编辑**。 您可以选择多个应用在同一时间编辑。  

    3. 选择重要性级别从**重要性**列表。 如果您希望桌面分析在试运行过程中验证应用程序，选择**严重**或**重要**。 它不会验证应用程序标记为**不重要**。 评估其[兼容性](/sccm/desktop-analytics/compat-assessment)和其他计划见解分配重要性级别时。  

        如果将分配重要性级别，您还可以选择升级决策。  

    4. 选择**保存**时完成。  

8. 在部署计划菜单上，在**准备**组中，选择**标识试点**。  

    1. 为试点查看建议的设备。  

    2. 选择每个设备，然后选择**将添加到试验**。 如果您不同意建议，请选择**替换为**。  

        对于桌面分析如何使这些建议的详细信息中的右上角选择信息图标**标识试点**窗格。



## <a name="deploy-windows-10-in-configuration-manager"></a>部署 Windows 10 Configuration Manager 中

使用此过程将 Windows 10 Configuration Manager 中部署到试验组。

- 如果你还没有一个，首先[适用于 Windows 10 创建 OS 升级包](#bkmk_create-package)  

- 如果还没有一个，[适用于 Windows 10 创建 OS 升级任务序列](#bkmk_create-ts)  

- [部署任务序列](#bkmk_deploy-ts)使用 Desktop 分析部署计划  

- [安装任务序列](#bkmk_install-ts)从目标设备上的软件中心  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a> 适用于 Windows 10 创建 OS 升级包

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统升级包”节点    。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“添加操作系统升级包”    。 此操作将启动“添加操作系统升级向导”。  

3. 上**数据源**页上，指定网络**路径**安装源文件的操作系统升级包。 例如，`\\server\share\path`。  

    > [!NOTE]  
    > 安装源文件包含 setup.exe 和其他文件以及用于安装 OS 的文件夹。  

4. 上**常规**页上，指定一个唯一**名称**os 升级包。  

5. 完成添加操作系统升级包向导。  

#### <a name="distribute-content"></a>分发内容

接下来，将 OS 升级包分发到分发点。  

1. 在列表中选择 OS 升级包。 在功能区的“主页”  选项卡上，在“部署”  组中，选择“分发内容”  。 分发内容向导将打开。  

2. 上**常规**页上，验证列出的内容是你想要分发，然后选择的内容**下一步**。  

3. 上**内容目标**页上，选择**添加**，然后选择**分发点**。 选择现有分发点，并选择**确定**。 添加完内容目标，选择**下一步**。  

4. 完成分发内容向导。  


### <a name="bkmk_create-ts"></a> 适用于 Windows 10 创建 OS 升级任务序列

1. 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**操作系统**，然后选择**任务序列**。  

2. 上**主页**功能区选项卡，在**创建**组中，选择**创建任务序列**。  

3. 上**创建新的任务序列**的创建任务序列向导中，选择页**从升级包升级操作系统**，然后选择**下一步**。  

4. 上**任务序列信息**页上，指定**任务序列名称**标识任务序列。  

5. 上**升级 Windows 操作系统**页上，指定以下设置，然后选择**下一步**:  

    - **升级包**：指定包含 OS 升级源文件的升级包。  

    - **版本索引**：如果包中有多个 OS 版本索引可用，请选择所需的版本索引。 默认情况下，该向导会选择第一个索引。  

    - **产品密钥**：指定要安装的 OS 的 Windows 产品密钥。 请指定编码的批量许可证密钥或标准产品密钥。 如果使用标准产品密钥，请用短划线 (-) 将每五个字符分隔为一组。 例如：XXXXX-XXXXX-XXXXX-XXXXX-XXXXX  。 在对批量许可证版本进行升级时，则可能不需要产品密钥。  

        > [!Note]  
        > 此产品密钥可以是多次激活密钥 (MAK) 或通用批量授权密钥 (GVLK)。 GVLK 也叫密钥管理服务 (KMS) 客户端安装密钥。 有关详细信息，请参阅[规划批量激活](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 客户端设置密钥的列表，请参阅 Windows Server 激活指南的[附录 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。

6. 上**包括更新**页上，选择**下一步**不安装任何软件更新。  

7. 上**安装应用程序**页上，选择**下一步**不安装任何应用程序。

8. 完成创建任务序列向导。  


### <a name="bkmk_deploy-ts"></a> 部署任务序列使用 Desktop 分析部署计划

1. 在 Configuration Manager 控制台中，转到**软件库**，展开**Desktop 分析服务**，然后选择**部署计划**节点。  

2. 选择 Windows 10 试验部署计划，并选择**部署计划的详细信息**功能区中。  

3. 在中**试验状态**磁贴中，选择**任务序列**从下拉列表中，然后选择**部署**。  

4. 上**常规**部署软件向导，选择页面**浏览**旁边**软件**字段。 选择你的 Windows 10 就地升级任务序列，然后选择**下一步**。  

    > [!Note]  
    > 通过桌面 Analytics 集成，Configuration Manager 自动创建的试验部署计划的集合。 它可能需要 10 分钟的时间为此集合可以使用它之前进行同步。<!-- 3887891 -->
    >
    > 此集合被保留的桌面分析部署计划设备。 不支持对此集合的手动更改。<!-- 3866460, SCCMDocs-pr 3544 -->  

5. 上**内容**页上，选择**添加**，然后选择**分发点**。 选择可用的分发点以承载安装内容，并选择**确定**。 然后选择“下一步”  。  

6. 上**部署设置**页上，选择**下一步**以接受默认设置。 （可用安装。）  

7. 上**计划**页上，选择**下一步**以接受默认设置。 （适用越早越好）。  

8. 上**的用户体验**页上，选择**下一步**以接受默认设置。 （在软件中心中显示，并且仅显示关于计算机重启的通知。）  

9. 上**警报**页上，选择**下一步**以接受默认设置。  

10. 完成向导。  


### <a name="bkmk_install-ts"></a> 从软件中心安装任务序列

1. 登录到设备的试验部署计划的成员。  

2. 打开**软件中心**和适用于 Windows 10 安装可用的操作系统。  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>后续步骤

转到下一步的文章，了解有关桌面分析部署计划的详细信息。
> [!div class="nextstepaction"]  
> [部署计划](/sccm/desktop-analytics/about-deployment-plans)
