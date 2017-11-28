---
title: Upgrade Readiness
titleSuffix: Configuration Manager
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
ms.openlocfilehash: df2950551e527788aeb01d57cdbf01ad19817ccd
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>将 Upgrade Readiness 与 System Center Configuration Manager 进行集成

*适用范围：System Center Configuration Manager (Current Branch)*

Upgrade Readiness（以前称为 Upgrade Analytics）是 [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) 的一部分，让你能够访问和分析环境中的设备对升级至 Windows 10 的准备情况。 可以配置特定版本。 可以将 Upgrade Readiness 与 Configuration Manager 进行集成，以便在 Configuration Manager 管理控制台中访问客户端升级兼容性数据。 可以使用基于该数据创建的动态集合来设定要升级或修正的设备。

Upgrade Readiness 是 [Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview) 中运行的解决方案。 有关 Upgrade Readiness 的详细信息，请参阅[使用 Upgrade Readiness 管理 Windows 升级](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness)。

## <a name="configure-clients"></a>配置客户端

Upgrade Readiness 和所有 Windows 分析解决方案类似，依赖于 Windows 遥测数据。 为了使 Upgrade Readiness 接收充足的遥测数据，必须满足以下先决条件：

- 所有客户端必须配置有“商业 ID 键”。 
- Windows 10 客户端必须将遥测配置为至少报告基础级别遥测。
-  运行较早版本 Windows 的客户端必须安装 [Upgrade Readiness 入门](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)中所述的特定 KB。 同时必须在“客户端设置”中启用遥测。

可以在“客户端设置”中配置商业 ID 键和 Windows 遥测。 若要了解详细信息，请参阅[结合使用 Windows Analytics 和 Configuration Manager](../monitor-windows-analytics.md)。

>[!NOTE]
>如果 Upgrade Readiness 并未按预期从环境中的设备接收遥测数据，使用 [Upgrade Readiness 部署脚本](/windows/deployment/upgrade/upgrade-readiness-deployment-script)也许可以处理部分问题。 但是对于大多数部署了正确 KB 的环境来说，在“客户端设置”中配置好商业 ID 键和遥测就足够了。

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>将 Configuration Manager 连接至 Upgrade Readiness

从 Current Branch 版本 1706 开始，[Azure 服务向导](../../../servers/deploy/configure/azure-services-wizard.md)可简化用于 Configuration Manager 的 Azure 服务的配置过程。 若要将 Configuration Manager 和 Upgrade Readiness 相连，必须在 [Azure 门户](https://portal.azure.com)中创建“Web 应用/API”类型的 Azure AD 应用注册。 要了解有关如何创建应用注册的详细信息，请参阅[向 Azure Active Directory 租户注册应用程序](/azure/active-directory/active-directory-app-registration)。 在 Azure 门户，还需在资源组（包含承载 Upgrade Readiness 数据的 OMS 工作区）中赋予新注册的 Web 应用“参与者”的权限。 Azure 服务向导将使用此应用注册来允许 Configuration Manager 与 Azure AD 进行安全通信，并将你的基础结构连接至 Upgrade Readiness 数据。

>[!IMPORTANT]
>“参与者”权限必须赋予应用本身而不是 Azure AD 用户标识。 这是因为它是注册应用，而非代表 Configuration Manager 基础结构访问数据的 Azure AD 用户。 要执行此操作，需要在分配权限时，在“添加用户”边栏选项卡中搜索应用注册的名称。 当[向 Configuration Manager 授予对 OMS 的权限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)以便连接到 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm)时，也必须遵循此流程。 在使用 Azure 服务向导将应用注册导入 Configuration Manager 之前，必须完成这些步骤。

### <a name="use-the-azure-wizard-to-create-the-connection"></a>使用 Azure 向导创建连接

按照[配置用于 Configuration Manager 的 Azure 服务](../../../servers/deploy/configure/azure-services-wizard.md)中的说明，导入上述创建的 Web 应用注册，从而创建和 Upgrade Readiness 之间的连接。 

如果 Web 应用导入成功并且 Azure 门户的权限分配正确，“配置”页上将预填充以下值。 
-  Azure 订阅
-  Azure 资源组
-  Windows Analytics 工作区

仅当已注册 Azure AD Web 应用在多个资源组上具备“参与者”权限，或者所选资源组包含多个 OMS 工作区时，多个资源组或工作区才可用。
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>在 Configuration Manager 中查看并使用 Upgrade Readiness 信息

将 Upgrade Readiness 与 Configuration Manager 进行集成后，可查看客户端升级就绪状态的分析。

1. 在 Configuration Manager 控制台中，选择“监视” > “概述” > “Upgrade Readiness”。
2. 查看数据，其中包括升级就绪状态和报告遥测的 Windows 设备的百分比。
3. 你可以筛选仪表板以查看特定集合中设备的数据。
4. 可以查看处于特定就绪状态的设备，并为这些设备创建动态集合，以便在就绪时升级这些设备，或采取措施修复升级受阻的设备。

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>使用 Upgrade Readiness 连接器（1702 及更早版本）

若要在 1702 或更早版本的 Configuration Manager 中创建和 Upgrade Readiness 之间的连接，需执行一些不同的步骤并满足一些不同的要求。

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
