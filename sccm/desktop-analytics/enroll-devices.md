---
title: 在桌面分析中注册设备
titleSuffix: Configuration Manager
description: 了解如何在桌面分析中注册设备。
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59cd27ac63430a8b9073e7b178b53f9a5cc23da6
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70377893"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>如何在桌面分析中注册设备

> [!Note]  
> 此信息与预览版服务相关，该服务可能会在商业发布之前进行大量修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

[将 Configuration Manager 连接](/sccm/desktop-analytics/connect-configmgr)到桌面分析时，将配置设置以将设备注册到桌面分析。 你可以随时更改这些设置。 同时确保设备是最新的。



## <a name="update-devices"></a>更新设备

对于桌面分析的最佳体验，需要满足两种类型的更新：

- [兼容性更新](#bkmk_appraiser)  
- [连接的用户体验和遥测服务](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a>兼容性更新

兼容性组件（人员）在 Windows 设备上运行诊断，以评估其与最新版本的 Windows 10 的兼容性状态。

Microsoft 会定期递增此组件的更新，但关联的 KB 数不会改变。 请确保始终具有最新版本的更新。

首次安装兼容性更新后，重新启动设备。

> [!Tip]  
> 使用 Configuration Manager 自动安装这些更新的最新版本。 有关详细信息，请参阅[部署软件更新](/sccm/sum/deploy-use/deploy-software-updates)。  

> [!Note]  
> 有一个相关的可选更新（ [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513)）。 此更新提供较新的兼容性更新配置和定义。 有关详细信息，请参阅[适用于 Windows 的最新兼容性定义更新](https://support.microsoft.com/help/3150513)。  

#### <a name="windows-10"></a>Windows 10

Windows 10 包括兼容性组件。 若要获取最新的兼容性更新，请安装最新的 Windows 10 累积更新。

#### <a name="windows-81"></a>Windows 8.1

下载更新：[KB 2976978](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

在参与 Windows 客户体验改善计划 Windows 8.1 系统上运行诊断。 这些诊断帮助确定升级到 Windows 10 时是否可能存在兼容性问题。

有关详细信息，请参阅[Windows 8.1 中保持 Windows 最新的兼容性更新](https://support.microsoft.com/help/2976978)。

#### <a name="windows-7-with-service-pack-1"></a>带有 Service Pack 1 的 Windows 7

下载更新：[KB 2952664](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

在参与 Windows 客户体验改善计划的 Windows 7 Service Pack 1 （SP1）系统上运行诊断。 这些诊断帮助确定升级到 Windows 10 时是否可能存在兼容性问题。

有关详细信息，请参阅[windows 7 中的使 windows 保持最新状态的兼容性更新](https://support.microsoft.com/help/2952664)。


### <a name="bkmk_diagtrack"></a>连接的用户体验和遥测服务

启用 Windows 诊断数据后，连接的用户体验和遥测服务（DiagTrack）将收集系统、应用程序和驱动程序数据。 Microsoft 会分析这些数据，并通过桌面分析将其共享回来。

为了获得最佳体验，请根据操作系统版本安装以下更新。

> [!Note]  
> 安装这些更新时，会出现以下行为：
> 
> - 注册到桌面分析的设备会在服务中的不到一小时内显示  
> - 设备快速报告 Windows 功能和质量更新的状态  
>
> 如果没有这些更新，可能需要超过48小时的时间才能将设备报告到桌面分析。  


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

安装10月2018每月汇总， [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

安装10月2018每月汇总， [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>设备注册

桌面分析服务没有要安装的代理。 设备注册需要在要监视的设备上配置设置。 这些设置可控制设备应该向哪个桌面分析实例发送其数据，以及其他配置选项。

> [!Note]  
> 如果已在使用 Windows Analytics，请将此工作区用于桌面分析。 需要重新注册以前在 Windows Analytics 中注册的设备到桌面分析。
>
> 每个租户 Azure AD 只能有一个桌面分析工作区。 设备只能将诊断数据发送到一个工作区。  

Configuration Manager 提供了用于管理这些设置并将其部署到客户端的集成体验。 为获得最佳体验，请使用 Configuration Manager。

将 Configuration Manager 连接到桌面分析时，将设置为注册设备。 有关详细信息，请参阅[如何通过桌面分析连接 Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_connect)。

若要更改这些设置，请使用以下过程：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点。 选择 "连接到桌面分析"，然后选择功能区中的 "**属性**"。

2. 在 "**诊断数据**" 页上，根据需要更改以下设置：  

    - **商业 id**：此值应自动填充你组织的 ID。 如果不是这样，请确保将代理服务器配置为允许所有所需的[终结点](/sccm/desktop-analytics/enable-data-sharing#endpoints)，然后再继续。 或者，通过[桌面分析门户](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID)手动检索商业 ID。   

    - **Windows 10 诊断数据级别**：有关详细信息，请参阅[诊断数据级别](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)。  

    - **允许诊断数据中的设备名称**：有关详细信息，请参阅[设备名称](#device-name)。  

    对此页进行更改时，"**可用功能**" 页将显示桌面分析功能的预览，其中包含所选的诊断数据设置。  

3. 在 "**桌面分析连接**" 页上，根据需要更改以下设置：

    - **显示名称**：桌面分析门户显示此 Configuration Manager 使用此名称的连接。  

    - **目标集合**：此集合包括 Configuration Manager 配置商业 ID 和诊断数据设置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。  

    - **目标集合中的设备使用用户身份验证的代理进行出站通信**：默认情况下，此值为 "**否**"。 如果你的环境中需要，请将设置为 **"是"** 。 有关详细信息，请参阅[代理服务器身份验证](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication)。  

    - **选择要与桌面分析同步的特定集合**：选择 "**添加**" 以包括**目标集合**层次结构中的其他集合。 这些集合在桌面分析门户中提供，用于将部署计划分组。 请确保包括试验和试点排除集合。  <!-- 4097528 -->

        > [!Important] 
        > 这些集合将继续同步，因为其成员身份更改。 例如，你的部署计划使用具有 Windows 7 成员身份规则的集合。 当这些设备升级到 Windows 10，并 Configuration Manager 评估集合成员身份时，这些设备将拖出收集和部署计划。  


### <a name="windows-settings"></a>Windows 设置

Configuration Manager 在 "本地策略" 路径`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`下设置以下 Windows 设置：

| 策略   | 值  |
|----------|--------|
| **CommercialId** | 为了使设备在桌面分析中显示，请将其配置为组织的商业 ID。 |
| **AllowTelemetry**  | 为`1` "**基本**" `2` 、"**增强**" `3`或 "**完整**诊断数据" 设置。 桌面分析至少需要基本诊断数据。 Microsoft 建议使用桌面分析的 "增强（受限）" 级别。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization)。 |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *适用于 Windows 10 及更高版本1709及更高版本*：仅当 AllowTelemetry 设置为`2`时，此设置才适用。 它将发送给 Microsoft 的增强诊断数据事件限制为仅限桌面分析所需的那些事件。 有关详细信息，请参阅 windows [10 版本1709增强的诊断数据事件和 Windows Analytics 使用的字段](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)。|
| **AllowDeviceNameInTelemetry** | *适用于 Windows 10 及更高版本1803及更高版本*：要使设备能够继续发送设备名称，需要单独选择加入。<br> <br>注意:默认情况下，设备名称不会发送给 Microsoft。 如果不发送设备名称，它将在桌面分析中显示为 "未知"。 此行为可能会导致难以识别和评估设备。 有关详细信息，请参阅[设备名称](#device-name)。 |
| **CommercialDataOptIn** | *适用于 Windows 7 和 Windows 8.1*：桌面分析需要`1`值。 有关详细信息，请参阅[Windows 7 中的商业数据选择加入](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\))。 |

在组策略编辑器中的以下路径查看这些设置：**计算机配置** > **管理模板** **Windows 组件**数据收集**和预览生成。**  >  > 

> [!Important]  
> 在大多数情况下，只使用 Configuration Manager 来配置这些设置。 不要同时在域组策略对象中应用这些设置。 有关详细信息，请参阅[冲突解决](#conflict-resolution)。<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>设备名称

从 Windows 10 版本1803开始，默认情况下不再收集设备名称。 使用诊断数据收集设备名称需要单独选择加入。 如果没有设备名称，则在评估升级到新版本的 Windows 时，更难识别哪些设备需要关注。

如果不发送设备名称，它将在桌面分析中显示为 "未知"。

![显示 "未知" 名称的桌面分析设备列表](media/unknown-device-name.png)

"桌面分析" 的 "Configuration Manager 设置" 中有一个选项，用于配置此选项：**允许诊断数据中的设备名称**。 此 Configuration Manager 设置控制 Windows 策略设置 AllowDeviceNameInTelemetry。
 

### <a name="conflict-resolution"></a>冲突解决

通常，使用 Configuration Manager 集合来面向桌面分析设置和注册。 使用直接成员身份或查询来包括或排除集合中的设备。 有关详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。

如果值尚不存在，Configuration Manager 仅配置 Windows 设置。 如果需要为一组独特的设备配置不同的设置，可以使用[组策略](#windows-settings)。 组策略设定的设置优先于 Configuration Manager 设置。

如果使用 Windows Analytics 和 Desktop Analytics 设置以 Configuration Manager 客户端为目标，则桌面分析的设置优先。

配置诊断数据级别时，请设置设备的上限。 默认情况下，在 Windows 10 版本1803及更高版本中，用户可以选择设置较低的级别。 你可以使用 "组策略" 设置来控制此行为，**配置遥测选择加入 "用户界面**"。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。



## <a name="next-steps"></a>后续步骤

转到下一篇文章，在桌面分析中创建部署计划。
> [!div class="nextstepaction"]  
> [创建部署计划](/sccm/desktop-analytics/create-deployment-plans)  
