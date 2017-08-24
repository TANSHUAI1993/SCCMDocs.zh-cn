---
title: "升级就绪情况 | System Center Configuration Manager"
description: "将 Upgrade Readiness 与 Configuration Manager 进行集成。 在管理控制台中访问升级兼容性数据。 设定要升级或修正的设备。"
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angerobe
ms.date: 7/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: b1f4cd4a6f19a02d2b2dc3f9a841aeeb2a1403dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>将 Upgrade Readiness 与 System Center Configuration Manager 进行集成

*适用范围：System Center Configuration Manager (Current Branch)*

借助升级就绪情况（以前称为 Upgrade Analytics），用户能够评估和分析设备对 Windows 10 的准备情况。 将 Upgrade Readiness 与 Configuration Manager 进行集成，以便在 Configuration Manager 管理控制台中访问客户端升级兼容性数据。 可以从设备列表中设定要升级或修正的设备。

Upgrade Readiness 是 Microsoft Operations Management Suite (OMS) 中的解决方案。 有关 Upgrade Readiness 的详细信息，请参阅 [Upgrade Readiness 入门](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness)。

## <a name="configure-clients"></a>配置客户端

必须执行几个配置步骤以确保客户端可以向 Upgrade Readiness 提供数据：

-  按[在你的组织中配置 Windows 遥测](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization)中所述方法配置客户端遥测设置。
-  安装[升级就绪情况入门](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness)的*部署兼容性更新和相关知识库*部分所述的知识库。

    > [!NOTE]
    > 用户可下载脚本以自动执行多个客户端安装任务。 有关脚本的信息，请参阅 [Upgrade Readiness 入门](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness)的“运行 Upgrade Readiness 部署脚本”部分。

## <a name="connect-to-upgrade-readiness"></a>连接到升级就绪情况

### <a name="prerequisites"></a>先决条件

从 Current Branch 版本 1706 开始，“Azure 服务向导”可简化用于 Configuration Manager 的 Azure 服务的配置过程。 若要使用此向导，需要配置 Azure Web 应用。 有关详细信息，请参阅 [Azure 服务向导](/sccm/core/servers/deploy/configureazure-services-wizard)。

### <a name="use-the-azure-wizard-to-create-the-connection"></a>使用 Azure 向导创建连接

1.  在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后单击“Azure 服务”。
2.  在“主页”选项卡上的“Azure 服务”组中，单击“配置 Azure 服务”。
3.  在 Azure 服务页面上键入一个友好的名称。 还可键入说明。 然后选择“升级就绪情况连接器”，并单击“下一步”。
4.  在“应用”页上指定 Azure 环境。 单击“浏览”设置服务器应用。
5.  单击“导入”连接到 Azure Web 应用。
    -  键入“Azure AD 租户名称”。
    -  键入“Azure AD 租户 ID”。
    -  键入“应用程序名称”。
    -  键入“客户端 ID”。
    -  键入“密钥”。
    -  选择“密钥到期”日期。
    -  为“应用程序 ID URI”键入任意 URL。
    -  单击“验证”，然后单击“确定”。

6.  在“配置”页上指定到升级就绪情况的连接。 选择以下值：  
    -  Azure 订阅
    -  Azure 资源组
    -  Windows Analytics 工作区
8.  单击“下一步” 。 可以在“摘要”页中查看连接。 

## <a name="complete-upgrade-readiness-tasks"></a>完成 Upgrade Readiness 任务  

创建连接后，请按[升级就绪情况入门](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness)中所述的方法执行这些任务。  

1. 将 UpgradeReadiness 服务添加到 OMS 工作区。  
2. 生成商用 ID。  
3. 订阅 Upgrade Readiness。   

## <a name="use-the-upgrade-readiness-deployment-script"></a>使用 Upgrade Readiness 部署脚本  

可以自动执行多个 Upgrade Readiness 任务，并使用 Microsoft **Upgrade Readiness 部署脚本**解决数据共享问题。  
Upgrade Readiness 部署脚本可执行以下操作：  

- 设置商用 ID 键 + CommercialDataOptIn + RequestAllAppraiserVersions 键。  
- 验证用户计算机是否可向 Microsoft 发送数据。  
- 检查计算机是否正在等待重启。   
- 确认是否已安装最新版本的知识库包 10.0.x（需要 10.0.14913 或后续版本）。  
- 如果已启用，开启详细模式进行故障排除。  
- 开始收集 Microsoft 评估组织的升级准备情况所需的遥测数据。  
- 启用后，在 cmd 窗口中会显示脚本的进度。 通过它可以查看问题（各个步骤成功还是失败）和/或写入日志文件。  

## <a name="to-run-the-upgrade-readiness-deployment-script"></a>运行 Upgrade Readiness 部署脚本：  

1. 下载 [Upgrade Readiness 部署脚本](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409)并提取 UpgradeReadiness.zip。 仅当计划在故障排除模式下运行脚本时，才需要“诊断”文件夹中的文件。  
2. 在 RunConfig.bat 中编辑这些参数：  
- 日志信息的存储位置。 示例：%SystemDrive%\URDiagnostics. 可以将日志信息存储在远程文件共享或本地目录中。 如果阻止脚本为给定路径创建日志文件，则它将使用 Windows 目录在驱动器中创建日志文件。  
- 商用 ID 键。  
- 默认情况下，该脚本会将日志信息发送到控制台和日志文件。 若要更改默认行为，请使用下列选项之一：  
    - logMode = 0 仅在控制台中记录  
    - logMode = 1 在文件和控制台中记录  
    - logMode = 2 仅在文件中记录  
    - 若要进行故障排除，请将 **isVerboseLogging** 设置为 **$true**，以生成有助于诊断问题的日志信息。 默认情况下，**isVerboseLogging** 设置为 **$false**。 确保诊断文件夹安装在与脚本相同的目录中以使用此模式。  
    - 请在用户需要重启计算机时通知用户。 默认情况下，此选项设置为关闭。  

3. 在 RunConfig.bat 中完成编辑参数后，请以管理员身份运行脚本。  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>在 Configuration Manager 中查看 Microsoft Upgrade Readiness 属性  

1.  在 Configuration Manager 控制台中，导航到“云服务”，然后选择“OMS 连接器”以打开“OMS 连接属性”页。  

2.  该页中有两个选项卡：
  * “Azure Active Directory”选项卡显示“租户”、“客户端 ID”、“客户端机密密钥的过期”，使你可以在客户端密钥到期时**验证****客户端密钥**。
  * “Upgrade Readiness”选项卡显示“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”。

## <a name="view-and-use-the-upgrade-information"></a>查看和使用升级信息

将 Upgrade Readiness 与 Configuration Manager 进行集成后，可查看客户端升级准备情况的分析，然后采取措施。

1. 在 Configuration Manager 控制台中，选择“监视” > “概述” > “Upgrade Readiness”。
2. 查看数据，其中包括升级就绪状态和报告遥测的 Windows 设备的百分比。
3. 你可以筛选仪表板以查看特定集合中设备的数据。
4. 可以查看处于特定就绪状态的设备，并为这些设备创建动态集合，以便可在就绪时升级这些设备，或采取措施使其处于就绪状态。

## <a name="create-a-connection-to-upgrade-readiness-1702-and-earlier"></a>创建到升级就绪情况的连接（1702 及早期版本）

在 Configuration Manager 的 1706 分支之前，创建到升级就绪情况底连接需要以下步骤。

### <a name="prerequisites"></a>先决条件

- 若要添加连接，Configuration Manager 环境必须先在[联机模式](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/)下配置[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)。 将连接添加到环境时，它还会在运行此站点系统角色的计算机上安装 Microsoft Monitoring Agent。
- 将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具，并获得[来自此注册的客户端 ID](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/)。
- 在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。
- 在 Azure 门户中，向已注册的 Web 应用提供访问 OMS 的权限，如[向 Configuration Manager 提供 OMS 权限](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms)中所述。

    > [!IMPORTANT]
    > 配置访问 OMS 的权限时，请务必选择**参与者**角色，并向其分配注册应用的资源组的权限。

### <a name="create-the-connection"></a>创建连接

1.  在 Configuration Manager 控制台中，选择“管理” > “云服务” > “Upgrade Readiness 连接器” > “创建 Upgrade Analytics 连接”以启动“添加 Upgrade Analytics 连接向导”。
3.  在“Azure Active Directory”屏幕上，提供“租户”、“客户端 ID”以及“客户端密钥”，然后选择“下一步”。
4.  在“Upgrade Readiness”屏幕上，填写“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”，提供连接设置。
5.  在“摘要”屏幕上验证连接设置，然后选择“下一步”。

    > [!NOTE]
    > 必须将 Upgrade Readiness 连接到层次结构中的顶层站点。 如果将 Upgrade Readiness 连接到独立主站点，然后将管理中心站点添加到环境，则必须删除 OMS 连接并在新层次结构中重新创建。
