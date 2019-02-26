---
title: 教程-部署 Office 365
titleSuffix: Configuration Manager
description: 使用桌面 Analytics 和 Configuration Manager 将 Office 365 部署到试验组的教程。
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: eb4170bddfbad34807c6fb82131fa09dc7c6b09f
ms.sourcegitcommit: ceec0e20bf801071f2a05233f984cf17acc3fd29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56754715"
---
# <a name="tutorial-deploy-office-365-to-pilot"></a>教程：将 Office 365 部署到试运行 

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

本教程使用桌面 Analytics 和 Configuration Manager 将 Office 365 专业增强版部署到试验组。 它会突出显示云服务，以提供见解来部署应用程序与在本地产品的集成。 使用 Desktop 分析来确定要在试验组中放置的最佳设备。 然后使用 Configuration Manager 以获取新的 Office。

在本教程中，您学习如何：  

> [!div class="checklist"]  
> * 在 Azure 门户中进行桌面分析设置  
> * 将 Configuration Manager 连接和配置设备设置  
> * 为 Office 365 专业增强版创建桌面分析部署计划  
> * 将 Office 365 专业增强版 Configuration Manager 中部署到试验组  

如果还没有 Azure 订阅，创建[免费帐户](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)在开始之前。 正确配置后，使用 Desktop Analytics 不会产生任何 Azure 费用。 

使用桌面分析*Log Analytics 工作区*在 Azure 订阅中。 工作区是实质上是包含帐户信息和帐户简单配置信息的容器。 有关详细信息，请参阅[管理的工作区](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json)。



## <a name="prerequisites"></a>先决条件

在开始本教程之前，请确保具备以下先决条件：  

- 有效的 Azure 订阅，使用**公司管理员**权限  

- 配置管理器中，更新汇总 4486457 或更高版本，且版本 1810年**完全权限管理员**角色  

- 使用以下配置至少一个 Windows 10 设备：  

    - Windows 10 版本 1709，或者更高版本

    - 最新的 Windows 10 累积质量更新  

    - Configuration Manager 客户端版本 1810年 4486457 或更高版本的更新汇总  

    - Windows 安装程序基于版本的 Office，Office 2013 等  

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
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  
    - `https://graph.windows.net` （在 Configuration Manager 服务器角色）
    - `https://fef.bmsub01.manage-beta.microsoft.com` （在 Configuration Manager 服务器角色）

    有关详细信息，请参阅[如何启用数据共享桌面分析](/sccm/desktop-analytics/enable-data-sharing#endpoints)。  

> [!Important]  
> 这些系统必备组件都用于本教程的目的。 有关桌面 Analytics 和 Configuration Manager 的常规先决条件的详细信息，请参阅[先决条件](/sccm/desktop-analytics/overview#prerequisites)。  



## <a name="set-up-desktop-analytics"></a>设置桌面分析

使用此过程中登录到桌面分析并将其配置你的订阅中。 此过程是一次性的过程来为你的组织设置 Desktop 分析。  

1. 打开[Desktop 分析门户](https://aka.ms/m365aprod)中的用户的 Microsoft 365 设备管理**公司管理员**权限。 选择**启动**。  

2. 上**接受服务协议**页上，查看服务协议，然后选择**接受**。  

3. 上**确认你的订阅**页上，需符合条件的许可证的列表适用于 Windows 设备运行状况分析功能的桌面。 选择**下一步**以继续。  

4. 上**授予用户访问权限**页上，桌面分析预配置 Azure Active Directory 中的两个安全组：  

    - **工作区所有者**:创建和管理工作区。 这些帐户需要对 Azure 订阅所有者访问权限。  

    - **工作区参与者**:创建和管理此工作区中的部署计划。 它们不需要任何其他的 Azure 访问权限。  
  
   若要将用户添加到这两个组中，键入在其名称或电子邮件地址**输入名称或电子邮件地址**相应的组的部分。 完成后，选择**下一步**。 

5. 在到页**设置工作区**:  

    - 若要使用 Desktop 分析现有的工作区，选择它，并继续下一步。  

    - 若要为 Desktop 分析创建一个工作区，选择**添加工作区**。  

        1. 输入**工作区名称**。  

        2. 选择的下拉列表**选择此工作区的 Azure 订阅名称**，然后选择此工作区的 Azure 订阅。  

        3. 选择**地区**从列表中，然后选择**添加**。  

6. 选择新的或现有工作区中，并选择**设置为桌面 Analytics 工作区**。  然后选择**继续**中**确认和授予访问权限**对话框。  

7. 在新的浏览器选项卡上，选择要用于登录的帐户。 选择选项**代表你的组织同意**，然后选择**接受**。  

8. 恢复到页面上**设置工作区**，选择**下一步**。  

9. 上**最后步骤**页上，选择**转到桌面分析**。 Azure 门户显示桌面分析**主页**页。  


### <a name="create-an-app-in-azure-ad-for-configuration-manager"></a>在 Azure AD 中为 Configuration Manager 创建应用  

1. 在中[Azure 门户](http://portal.azure.com)，请转到**Azure Active Directory**，然后选择**应用注册**。 然后选择**新建应用程序注册**。  

2. 在中**创建**面板中，配置以下设置：  

    - **名称**： 唯一名称标识的应用，例如： `Desktop-Analytics-Connection`  

    - **应用程序类型**:**Web 应用 / API**  

    - **登录 URL**： 此值不是使用由配置管理器中，但所需的 Azure AD。 输入一个唯一且有效的 URL，例如： `https://configmgrapp`  
  
    选择“创建”。  

3. 选择应用，并记下**应用程序 ID**。 此值是用于配置 Configuration Manager 连接的 GUID。  

4. 选择**设置**上的应用，并选择**密钥**。 在中**密码**部分中，输入**密钥说明**，指定一个过期**持续时间**，然后选择**保存**。 复制**值**的密钥，用于进行配置的配置管理器连接。 

    > [!Important]  
    > 这是唯一的机会来复制密钥值。 如果您不立即将其复制，需要创建另一个密钥。  
    > 
    > 将密钥值保存在安全的位置。  

5. 在应用上**设置**面板中，选择**所需的权限**。  

    1. 上**所需的权限**面板中，选择**添加**。  

    2. 在中**添加 API 访问权限**面板中，**选择 API**。  

    3. 搜索**配置管理器微服务**API。 选择它，，然后选择**选择**。  

    4. 上**启用访问权限**面板中，选择这两个应用程序权限：**CM 集合数据写入**并**读取 CM 集合数据**。 然后选择**选择**。  

    5. 上**添加 API 访问权限**面板中，选择**完成**。  

6. 上**所需的权限**页上，选择**授予权限**。 选择**是**。  

7. 复制 Azure AD 租户 id。 此值是用于配置 Configuration Manager 连接的 GUID。 选择**Azure Active Directory**在主菜单中，然后选择**属性**。 复制**Directory ID**值。  



## <a name="connect-configuration-manager"></a>连接 Configuration Manager

此过程用于更新配置管理器，连接到 Desktop 分析并配置设备设置。 此过程是一次性的过程来将你的层次结构附加到云服务。  


### <a name="update-configuration-manager"></a>更新 Configuration Manager

安装 Configuration Manager 版本 1810年更新汇总 (4486457) 以支持与桌面 Analytics 的集成。 有关此更新的详细信息，请参阅[更新的 Configuration Manager current branch，版本 1810年汇总](https://support.microsoft.com/help/4486457)。

1. 使用版本 1810 的更新汇总更新站点。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。  

2. 更新客户端。 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  


### <a name="connect-to-the-service"></a>连接到服务

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。 选择**配置 Azure 服务**功能区中。  

2. 上**Azure 服务**页上的 Azure 服务向导配置以下设置：  

    - 指定**名称**Configuration Manager 中的对象  

    - 指定一个可选**说明**以帮助你识别该服务  

    - 选择**Desktop 分析**从可用服务列表  
  
   选择“下一步”。  

3. 上**应用程序**页上，选择相应**Azure 环境**。 然后选择**导入**为 web 应用。 配置中的以下设置**导入应用**窗口：  

    - **Azure AD 租户名称**:此名称是它如何命名已在配置管理器  

    - **Azure AD 租户 ID**:**Directory ID**从 Azure AD 复制   

    - **客户端 ID**：**应用程序 ID**复制从 Azure AD 应用   

    - **机密密钥**:键**值**复制从 Azure AD 应用   

    - **密钥到期日期**：密钥的同一个到期日期   

    - **应用 ID URI**：此设置应自动填充以下值： `https://cmmicrosvc.manage.microsoft.com/`  
  
   选择**验证**，然后选择**确定**以关闭导入应用窗口中。 选择**下一步**Azure 服务向导的应用页上。  

4. 上**诊断数据**页上，配置以下设置：  

    - **商用 ID**： 此值应自动填充你的组织 id  

    - **Windows 10 诊断数据级别**： 选择至少**增强 （受限）**  

    - **允许诊断数据中的设备名称**： 选择**启用**  
  
   选择“下一步”。 **可用的功能**页显示桌面的分析功能，可使用前一页中的诊断数据设置。 选择“下一步”。  

5. 上**集合**页上，配置以下设置：  

    - **显示名称**：Desktop 分析门户会显示此 Configuration Manager 连接，使用此名称。 使用它来区分不同的层次结构。 例如，*测试实验室*或*生产*。  

    - **目标集合**:此集合包含所有设备，配置管理器配置商业 ID 和诊断数据设置。 它是完整的配置管理器连接到桌面 Analytics 服务的设备集。  

    - **目标集合中的设备使用用户身份验证代理进行出站通信**:默认情况下，此值是**否**。 如果需要在环境中，将设置为**是**。   

    - **选择要与桌面 Analytics 同步的特定集合**:选择**添加**以包括其他集合。 这些集合是可在部署计划及分组 Desktop 分析门户中。 请确保包括试验和试验的排除集合。  

        这些集合继续作为其成员身份的更改进行同步。 例如，你的部署计划使用一组与 Windows 7 的成员身份规则。 在这些设备升级到 Windows 10 和 Configuration Manager 将评估集合成员身份时，这些设备将删除超出集合和部署计划。  

6. 完成向导。  

Configuration Manager 创建一个设置策略来配置目标集合中的设备。 此策略包括要使设备能够向 Microsoft 发送数据的诊断数据设置。 默认情况下，客户端每隔一小时更新策略。 收到后的新设置，它可以是几个小时，更多数据之前在桌面 Analytics 中可用。

监视桌面分析你的设备的配置。 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**Microsoft 365 维护**节点，然后选择**连接运行状况**仪表板。  

Configuration Manager 同步创建连接的 15 分钟内，任何桌面分析部署计划。 在 Configuration Manager 控制台中，转到**软件库**工作区中，展开**Microsoft 365 维护**节点，然后选择**部署计划**节点。 



## <a name="create-a-desktop-analytics-deployment-plan"></a>创建桌面分析部署计划

使用此过程在桌面 Analytics 中创建部署计划。

1. 打开[Desktop 分析门户](https://aka.ms/m365aprod)。 使用凭据至少具有**工作区参与者**权限。  

2. 选择**部署计划**管理组中。  

3. 在中**部署计划**窗格中，选择**创建**。  

4. 在中**创建部署计划**窗格中，配置以下设置：  

    - **名称**：唯一的名称为部署计划例如 `Office 365 pilot`  

    - **产品和版本**:选择**Office**产品和最新的可用建议的版本。 例如， **Office 365 客户端、 版本 （推荐） 1808年**。  

    - **设备组**:选择一个或多个组，然后选择**设置为目标组**。 与分组**sccm**作为源是集合从 Configuration Manager 同步。  

    - **准备情况规则**:这些规则帮助确定哪些设备有资格获得升级。 选择**Office 应用程序**和配置下列设置：  

        - 更新 Office 365 专业增强版从 32 位到 64 位。 此设置仅适用于运行 Windows 的 64 位版本的设备。 默认设置为“是”。  

        - 从较旧版本的 Office 更新时，保留旧不推荐使用 Office 应用程序。 即使在较新的 Office 版本中不存在这些应用程序，此行为也适用。 默认设置是**否**。  

        - 低安装 Office 加载项的计数阈值。默认阈值为`2%`。 低于此阈值的外接程序将自动设置为*低安装计数*。 桌面分析在试用期间不会验证这些加载项。 

            如果外接程序安装在大于此阈值为较高百分比的计算机外, 接程序作为将标记部署计划*Noteworthy*。 然后可以决定要在试验阶段测试其重要性。   

    - **完成日期**:选择依据 Office 应完全部署到所有目标设备的日期。  

5. 选择“创建”。 其正在处理时，在部署计划列表中显示新的计划。 处理可以需要长达 48 小时，然后才能继续执行下一步。  

6. 选择其名称以打开部署计划。  

7. 在部署计划菜单上，在**准备**组中，选择**识别重要性**。  

    1. 上**Office 加载项**选项卡上，选择此选项可以仅显示**未检查**资产。  

    2. 选择每个外接程序，并选择**编辑**。 您可以选择多个应用在同一时间编辑。   

    3. 选择重要性级别从**重要性**列表。 如果您希望桌面分析在试运行过程中验证外接程序，选择**严重**或**重要**。 它不会验证加载项标记为**不重要**。 分配重要性级别时，请考虑兼容性风险和其他计划见解。  

        如果将分配重要性级别，您还可以选择升级决策。  

    4. 选择**保存**时完成。  

8. 在部署计划菜单上，在**准备**组中，选择**标识试点**。  

    1. 为试点查看建议的设备。  

    2. 选择每个设备，然后选择**将添加到试验**。 如果您不同意建议，请选择**替换为**。  

        对于桌面分析如何使这些建议的详细信息中的右上角选择信息图标**标识试点**窗格。



## <a name="deploy-office-365-in-configuration-manager"></a>部署 Office 365 中配置管理器

使用此过程以将 Office 365 专业增强版 Configuration Manager 中部署到试验组。

- 如果你还没有一个，首先[创建用于 Office 365 专业增强版的应用](#bkmk_create-app)  

- [将应用部署](#bkmk_deploy-app)使用 Desktop 分析部署计划  

- [安装应用](#bkmk_install-app)从目标设备上的软件中心  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> 创建 Office 365 专业增强版应用

1. 在 Configuration Manager 控制台中，转到**软件库**，然后选择**Office 365 客户端管理**节点。 选择**Office 365 安装程序**磁贴的仪表板上。  

2. 上**应用程序设置**页上，提供**名称**为此应用程序。 例如，`Office 365 ProPlus`。 （可选） 指定**说明**。 指定**内容位置**安装文件，然后选择**下一步**。  

3. 上**Office 设置**页上，选择**转到 Office 自定义工具**。 配置 Office 365 安装任何必需的部署设置：  

    1. 在中**产品和版本**组中，选择**Office 365 ProPlus**从列表中，然后选择**添加**。  

    2. 在中**语言**组中，选择的主要语言。  

    3. 在中**更新和升级**组中，请确保将设置改为**卸载任何 MSI 版本的 Office，包括 Visio 和 Project**是**上**。  

    4. 根据需要由你的组织配置的任何其他设置。  

    5. 完成后，选择**评审**右上角。 查看配置的设置，并选择**提交**。  

5. 选择“下一步”。 上**部署**页上，选择**否**若要立即部署。 （下一步的过程使用 Desktop 分析部署计划的部署。）选择**下一步**并完成向导。  


### <a name="bkmk_deploy-app"></a> 部署 Office 365 使用 Desktop 分析部署计划

1. 在 Configuration Manager 控制台中，转到**软件库**，展开**Desktop 分析服务**，然后选择**部署计划**节点。  

2. 选择 Office 365 试验部署计划，并选择**部署计划的详细信息**功能区中。  

3. 在中**试验状态**磁贴中，选择**应用程序**从下拉列表中，然后选择**部署**。  

4. 上**常规**部署软件向导，选择页面**浏览**旁边**软件**字段。 例如，选择 Office 365 应用程序中， **Office 365 专业增强版**。 通过桌面 Analytics 集成，Configuration Manager 自动创建的试验部署计划的集合。 选择“下一步”。  

5. 上**内容**页上，选择**添加**，然后选择**分发点**。 选择可用的分发点以承载安装内容，并选择**确定**。 然后选择“下一步”。  

6. 上**部署设置**页上，选择**下一步**以接受默认设置。 （可用安装。）  

7. 上**计划**页上，选择**下一步**以接受默认设置。 （适用越早越好）。  

8. 上**的用户体验**页上，选择**下一步**以接受默认设置。 （在软件中心中显示，并且仅显示关于计算机重启的通知。）  

9. 上**警报**页上，选择**下一步**以接受默认设置。  

10. 完成向导。  


### <a name="bkmk_install-app"></a> 从软件中心安装 Office 365

1. 登录到设备的试验部署计划的成员。  

2. 打开**软件中心**和安装可用的应用适用于 Office 365。  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->




## <a name="next-steps"></a>后续步骤

转到下一步的文章，了解有关桌面分析部署计划的详细信息。
> [!div class="nextstepaction"]  
> [部署计划](/sccm/desktop-analytics/deployment-plans)  

