---
title: 在 Desktop 分析中注册设备
titleSuffix: Configuration Manager
description: 了解如何在桌面分析中注册设备。
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5d5e6665b0ddd2e7726af4b8ac8929d5019fedf
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802438"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>如何在桌面分析中注册设备

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

当您[配置管理器连接](/sccm/desktop-analytics/connect-configmgr)到 Desktop 分析配置设置，以设备注册到 Desktop 分析。 您可以随时更改这些设置。 此外请确保设备是最新。



## <a name="update-devices"></a>更新设备

有两种类型的更新需要适用于桌面分析的最佳体验：

- [兼容性的更新](#bkmk_appraiser)  
- [连接的用户体验和遥测服务](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> 兼容性的更新

兼容性组件 （人员） 在要评估其与最新版本的 Windows 10 的兼容性状态的 Windows 设备上运行诊断。

Microsoft 定期递增此组件的更新，但不会更改关联的 KB 数。 请确保您始终具有最新版本的更新。

在安装第一次的兼容性更新后，重启设备。

> [!Tip]  
> 使用 Configuration Manager 自动安装这些更新的最新版本。 有关详细信息，请参阅[部署软件更新](/sccm/sum/deploy-use/deploy-software-updates)。  

> [!Note]  
> 没有相关的可选更新， [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513)。 此更新提供更新的配置和较旧的兼容性更新的定义。 有关详细信息，请参阅[Windows 的最新兼容性定义更新](https://support.microsoft.com/help/3150513)。  

#### <a name="windows-10"></a>Windows 10

Windows 10 包括兼容性组件。 若要获取最新的兼容性更新，请安装最新的 Windows 10 累积更新。

#### <a name="windows-81"></a>Windows 8.1

下载更新：[KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

参与 Windows 客户体验改善计划的 Windows 8.1 系统上运行诊断程序。 这些诊断帮助确定是否在升级到 Windows 10 时，可能会遇到兼容性问题。

有关详细信息，请参阅[兼容性更新使 Windows 保持最新 Windows 8.1 中](https://support.microsoft.com/help/2976978)。

#### <a name="windows-7-with-service-pack-1"></a>带有 Service Pack 1 的 Windows 7

下载更新：[KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

参与 Windows 客户体验改善计划的 Service Pack 1 (SP1) 系统与 Windows 7 上运行诊断程序。 这些诊断帮助确定是否在升级到 Windows 10 时，可能会遇到兼容性问题。

有关详细信息，请参阅[兼容性更新使 Windows 保持最新 Windows 7 中](https://support.microsoft.com/help/2952664)。


### <a name="bkmk_diagtrack"></a> 连接的用户体验和遥测服务

使用 Windows 诊断数据启用，互连用户体验与遥测数据服务 (DiagTrack) 收集系统、 应用程序和驱动程序数据。 Microsoft 会分析此数据，并回给你通过桌面分析共享它。

为获得最佳体验，安装以下更新取决于操作系统版本。

> [!Note]  
> 在安装这些更新时，预期以下行为：
> 
> - Desktop 分析到注册的设备显示在该服务在不到一小时内  
> - 设备快速报告状态功能和质量更新 Windows 和 Office  
>
> 如果没有这些更新，这些过程可能需要 48 小时内，使设备能够向桌面分析报告。  


#### <a name="windows-10"></a>Windows 10

安装最新的 Windows 10 累积更新。

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8.1

安装 2018 年 10 月每月汇总， [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

安装 2018 年 10 月每月汇总， [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>设备注册

Desktop 分析服务已安装任何代理。 设备注册需要在想要监视的设备上配置设置。 这些设置控制设备应该向哪些桌面分析实例发送其数据，而其他配置选项。

> [!Note]  
> 如果你已经在使用 Windows Analytics，用于桌面分析该相同的工作区。 您需要重新注册到桌面 Analytics 以前在 Windows Analytics 中注册的设备。
>
> 只能有一个桌面 Analytics 工作区，每个 Azure AD 租户。 设备只可以将诊断数据发送到一个工作区。  

Configuration Manager 提供管理以及将这些设置部署到客户端的集成的体验。 为获得最佳体验，使用配置管理器。

时将配置管理器连接到桌面 Analytics，你配置的设置，以注册设备。 有关详细信息，请参阅[如何将 Configuration Manager 和桌面分析](/sccm/desktop-analytics/connect-configmgr#bkmk_connect)。

若要更改这些设置，请使用以下过程：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。 选择与桌面 Analytics 的连接，然后选择**属性**功能区中。

2. 上**诊断数据**页上，根据需要对以下设置进行更改：  

    - **商用 ID**： 不应需要更改或编辑此值。 有关解决问题的商业 ID 的详细信息，请参阅[商业 ID 配置](/sccm/desktop-analytics/troubleshooting#commercial-id-configuration)。  

    - **Windows 10 诊断数据级别**:有关详细信息，请参阅[诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)。  

    - **允许诊断数据中的设备名称**:有关详细信息，请参阅[设备名称](#device-name)。  

    到此页上，进行更改时**可用的功能**页显示与所选诊断数据设置 Desktop 分析功能的预览。  

3. 上**Microsoft 365 分析连接**页上，根据需要对以下设置进行更改：

    - **显示名称**：Desktop 分析门户会显示此 Configuration Manager 连接，使用此名称。  

    - **目标集合**:此集合包含所有设备，配置管理器配置商业 ID 和诊断数据设置。 它是完整的配置管理器连接到桌面 Analytics 服务的设备集。  

    - **目标集合中的设备使用用户身份验证代理进行出站通信**:默认情况下，此值是**否**。 如果需要在环境中，将设置为**是**。 有关详细信息，请参阅[代理服务器身份验证](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication)。  

    - **选择要与桌面 Analytics 同步的特定集合**:选择**添加**以包括其他集合。 这些集合是可在部署计划及分组 Desktop 分析门户中。 请确保包括试验和试验的排除集合。  

        这些集合继续作为其成员身份的更改进行同步。 例如，你的部署计划使用一组与 Windows 7 的成员身份规则。 在这些设备升级到 Windows 10 和 Configuration Manager 将评估集合成员身份时，这些设备将删除超出集合和部署计划。  


### <a name="windows-settings"></a>Windows 设置

配置管理器设置下的以下 Windows 设置`Microsoft\Windows\DataCollection`:

| 策略   | 值  |
|----------|--------|
| **CommercialId** | 为了使设备才会显示在桌面分析，请将其配置与你的组织商业 id。 |
| **AllowTelemetry**  | 设置`1`有关**基本**，`2`有关**增强**，或`3`对于**完整**诊断数据。 桌面分析要求至少基本的诊断数据。 Microsoft 建议你使用与桌面 Analytics 的增强 （受限） 级别。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization)。 |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *适用于 Windows 10 版本 1709年及更高版本*:此设置仅适用 AllowTelemetry 设置为时`2`。 它限制到所需的桌面分析仅对这些事件发送给 Microsoft 的增强诊断数据事件。 有关详细信息，请参阅[Windows 10 版本 1709年增强的诊断数据的事件和使用的 Windows Analytics 字段](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)。|
| **AllowDeviceNameInTelemetry** | *适用于 Windows 10，版本 1803年和更高版本*:单独参加需要使设备能够继续发送设备名称。<br> <br>注意：默认情况下，设备名称不是发送给 Microsoft。 如果不发送设备名称，它显示在桌面分析为"未知"。 此行为可以使难以确定和评估设备。 有关详细信息，请参阅[设备名称](#device-name)。 |
| **CommercialDataOptIn** | *适用于 Windows 7 和 Windows 8.1*:值为`1`Desktop 分析需要进行。 有关详细信息，请参阅[商业数据自愿加入 Windows 7 中](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\))。 |

在组策略编辑器中的以下路径中查看这些设置：**计算机配置** > **管理模板** > **Windows 组件** > **数据集合和预览生成**。

> [!Important]  
> 在大多数情况下，仅使用配置管理器配置这些设置。 不会还应用域组策略对象中的这些设置。 有关详细信息，请参阅[冲突解决](#conflict-resolution)。<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>设备名称

从 Windows 10，版本 1803，开始设备名称不能再收集默认情况下。 收集诊断数据的设备名称需要单独参加。 不包含设备名称会更加困难，以便识别哪些设备评估升级到 Windows 或 Office 的新版本时需要注意。

如果不发送设备名称，它显示在桌面分析为"未知"。

![显示"未知"的名称的桌面分析设备列表](media/unknown-device-name.png)

没有用于桌面分析来配置此选项的配置管理器设置中的一个选项：**允许诊断数据中的设备名称**。 此 Configuration Manager 设置控制的 Windows 策略设置，AllowDeviceNameInTelemetry。
 

### <a name="conflict-resolution"></a>冲突解决方法

一般情况下，使用 Configuration Manager 集合以面向桌面分析设置和注册。 使用直接成员身份或查询中包括或排除设备集合。 有关详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。

如果值尚不存在，configuration Manager 仅配置 Windows 设置。 如果需要配置唯一的一组设备的不同设置，则可以使用[组策略](#windows-settings)。 针对由组策略的设置优先于配置管理器设置。

如果你面向 Configuration Manager 客户端使用 Windows Analytics 和 Desktop 分析设置，桌面分析的设置优先。

在配置的诊断数据级别时，您设置设备的上限。 默认情况下，在 Windows 10，版本 1803年和更高版本，用户可以选择设置较低级别。 您可以控制使用组策略设置，此行为**配置遥测参加设置用户界面**。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。



## <a name="next-steps"></a>后续步骤

转到下一步的文章，在桌面 Analytics 中创建部署计划。
> [!div class="nextstepaction"]  
> [创建部署计划](/sccm/desktop-analytics/create-deployment-plans)  
