---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: 将升级就绪情况与 Configuration Manager 集成来访问 Windows 10 升级兼容性数据和目标设备以进行升级或修正。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/04/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 0ba5a484fe11185b46125de0d8764bce153f577d
ms.sourcegitcommit: a2ecd84d93f431ee77848134386fec14031aed6a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55230845"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>将升级就绪情况与 Configuration Manager 集成

适用范围：System Center Configuration Manager (Current Branch)

升级就绪情况是 [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness) 的一部分。 可以使用它来访问和分析环境中的设备对升级至 Windows 10 的准备情况。 将升级就绪情况与 Configuration Manager 集成，以便在 Configuration Manager 控制台中访问客户端升级兼容性数据。 然后使用此数据创建集合，并设定要升级或修正的设备。



## <a name="configure-clients"></a>配置客户端

升级就绪情况依赖于 Windows Analytics 数据。 为了使升级就绪情况接收充足的数据，请配置以下先决条件：

- 为所有客户端配置“商用 ID 键”  

- 配置 Windows 10 客户端以便 Windows Analytics 报告至少基本级别的数据  

- 对于运行 Windows 7 或 8.1 的客户端：  

    - 安装更新，如[升级就绪情况入门](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)中所述  

    - 启用 Windows Analytics 客户端设置  

使用 Configuration Manager 客户端设置来配置这些设置。 有关详细信息，请参阅[使用 Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics)。

> [!NOTE]  
> 部署正确的先决条件更新和配置客户端设置应足以应对大多数环境。 如果升级就绪情况并未从环境中的设备接收数据，使用[升级就绪情况部署脚本](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script)也许可以解决部分问题。 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>将 Configuration Manager 连接至 Upgrade Readiness

使用 [Azure 服务向导](/sccm/core/servers/deploy/configure/azure-services-wizard)简化用于 Configuration Manager 的 Azure 服务的配置过程。 若要将 Configuration Manager 和升级就绪情况相连，请在 [Azure 门户](https://portal.azure.com)中创建“Web 应用/API”类型的 Azure Active Directory (Azure AD) 应用注册。 有关如何创建应用注册的详细信息，请参阅[向 Azure AD 租户注册应用程序](/azure/active-directory/active-directory-app-registration)。 

在 Azure 门户中，向新注册的 Web 应用提供以下权限：
- 向包含升级就绪情况数据的 Log Analytics 工作区的资源组提供读者权限
- 向托管升级就绪情况数据的 Log Analytics 工作区提供参与者权限

Azure 服务向导使用此应用注册来允许 Configuration Manager 与 Azure AD 进行安全通信，并将你的基础结构连接至升级就绪情况数据。

> [!IMPORTANT]  
> 将权限赋予应用本身，而不是 Azure AD 用户标识。 它是代表 Configuration Manager 基础结构访问数据的注册应用。 要授予权限，需要在分配权限时，在“添加用户”区域中搜索应用注册的名称。 
> 
> 此过程与向 Configuration Manager 提供 Log Analytics 权限相同。 在使用 Azure 服务向导将应用注册导入 Configuration Manager 之前，必须完成这些步骤。
> 
> 有关详细信息，请参阅[将 Configuration Manager 连接到 Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm)。


### <a name="use-the-azure-wizard-to-create-the-connection"></a>使用 Azure 向导创建连接

按照[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)中的说明，导入上述创建的 Web 应用注册，从而创建和升级就绪情况之间的连接。 

如果 Web 应用导入成功并且 Azure 门户的权限分配正确，“配置”页将预填充以下值：   
-  Azure 订阅  
-  Azure 资源组  
-  Windows Analytics 工作区  

多个资源组或工作区现支持下列情况： 
- 如果注册的 Azure AD Web 应用在多个资源组上拥有“参与者”权限   
- 如果所选资源组具有多个 Log Analytics 工作区  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>在 Configuration Manager 中查看并使用 Upgrade Readiness 信息

将 Upgrade Readiness 与 Configuration Manager 进行集成后，可查看客户端升级就绪状态的分析。

1. 在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“升级就绪情况”节点。  

2. 查看数据。 例如：  
    - 升级就绪状态  
    - 报告数据的 Windows 设备的百分比  

3. 筛选仪表板以查看特定集合中设备的数据。  

4. 查看处于特定就绪状态的设备，并创建这些设备的动态集合。 然后使用该集合升级这些设备，或采取措施修正处于受阻状态的设备。  

> [!Note]  
> 该站点将数据与升级就绪情况同步，每周一次。<!--SCCMDocs issue 732--> 手动触发同步：
> 1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。  
> 2. 从列表中选择升级就绪情况连接。  
> 3. 在功能区中，选择要同步的选项。  



## <a name="next-steps"></a>后续步骤

- [将 Windows 升级到最新版本](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [创建用于升级 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
