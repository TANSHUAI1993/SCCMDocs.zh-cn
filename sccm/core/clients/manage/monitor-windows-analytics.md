---
title: 使用 Windows Analytics 监视客户端
titleSuffix: Configuration Manager
description: Windows Analytics 是一组解决方案，使你能够有效深入了解当前环境状态。
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 194a26a4fee7a8a7c97a91db4b579c9db03c1787
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129776"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>结合使用 Windows Analytics 和 Configuration Manager

适用范围：System Center Configuration Manager (Current Branch)

[Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) 是一组解决方案，使你能够深入了解当前环境状态。 环境中的 Windows 设备向 Microsoft 报告数据，你可以通过这些解决方案访问和分析数据。 例如，通过将[升级就绪情况](/sccm/core/clients/manage/upgrade-readiness)连接到 Configuration Manager，可以直接访问 Configuration Manager 控制台的“监视”工作区中的数据。

Windows Analytics 使用的数据不会直接传输到 Configuration Manager 站点服务器。 客户端计算机将数据发送到 Windows 云服务。 然后此服务会将相关数据将传输到组织的其中一个工作区中托管的 Windows Analytics 解决方案。 然后，Configuration Manager 会通过上下文链接将你定向到 Web 门户中的相关数据。 它也可以直接显示作为连接到 Configuration Manager 的解决方案一部分的数据。

> [!Important]  
> Configuration Manager 向 Microsoft 报告诊断和使用情况数据。 此数据独立于 Windows Analytics 数据。 有关详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>将客户端配置为向 Windows Analytics 报告数据

对于向 Windows Analytics 报告数据的客户端设备，向其配置商用 ID 键。 此键是托管 Windows Analytics 数据的 Azure Log Analytics 工作区。 还必须将设备配置为以适合你想要使用的特定解决方案的级别来报告数据。 

### <a name="configure-windows-analytics-client-settings"></a>配置 Windows Analytics 客户端设置
配置 Windows Analytics： 
1. 在 Configuration Manager 控制台中，转到“管理”工作区，然后选择“客户端设置”节点。  
2. 在功能区中，选择“创建自定义设备客户端设置”。  
3. 向此自定义设备客户端设置策略添加“Windows Analytics”组。  

有关创建自定义设备客户端设置的详细信息，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。

选择“Windows Analytics”设置选项卡，然后配置以下设置：  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>使用 Configuration Manager 管理 Windows 遥测设置
将此设置配置为“是”以在 Windows 客户端上配置 Windows 诊断数据设置。   

#### <a name="commercial-id-key"></a>商用 ID 键
商用 ID 键可用于将你管理的设备中的信息映射到托管你组织的 Windows Analytics 数据的 Log Analytics 工作区。 如果已配置用于升级就绪情况的商用 ID 键，请使用此 ID。 如果还没有配置商用 ID 键，请参阅[复制商用 ID 键](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key)。

#### <a name="windows-10-telemetry"></a>Windows 10 遥测
有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization##diagnostic-data-level)。

> [!Note]  
> 还可以将 Windows 10 数据收集级别设置为“增强(受限)”。 该设置使你能够在环境中获得对设备的可操作见解，而无需设备通过 Windows 10 版本 1709 或更高版本报告“增强”级别的所有数据。 “增强(受限)”级别包括来自基本级别的指标，以及从与 Windows Analytics 相关的“增强”级别中收集的数据子集。

#### <a name="windows-81-and-earlier-telemetry"></a>Windows 8.1 和早期的遥测   
有关详细信息，请参阅 [Windows 7、 Windows 8 和 Windows 8.1 评估程序遥测事件和字段](https://go.microsoft.com/fwlink/?LinkID=822965)。

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>启用 Windows 8.1 和早期 Internet Explorer 数据收集
在运行 Windows 8.1 或更早版本的设备上，Internet Explorer 可收集有关 Web 应用的数据。 升级就绪情况可通过此数据检测可能会阻止顺利升级到 Windows 10 的 Web 应用程序不兼容问题。 启用基于 Internet 区域的 Internet Explorer 数据收集。 有关 Internet 区域的详细信息，请参阅[关于 URL 安全区域](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\))。



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>使用升级就绪情况识别 Windows 10 兼容性问题

借助升级就绪情况，用户能够分析设备对 Windows 10 的准备情况及兼容情况。 通过此评估可以使升级更流畅。 将 Configuration Manager 连接到升级就绪情况后，可以直接在 Configuration Manager 控制台中访问此客户端升级兼容性数据。 然后从设备列表中设定要升级或修正的设备。

有关如何配置和连接到升级就绪情况的详细信息，请参阅[升级就绪情况](/sccm/core/clients/manage/upgrade-readiness)。



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>使用 Windows Analytics 确定 Windows 信息保护策略中的缺口

可以使用 [Windows 信息保护](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) 策略配置 Windows 10 版本 1703 及更高版本的设备。 它们报告在环境中访问公司数据的应用程序的诊断数据，但不包括在策略应用程序规则中。 用户可能需要这些应用程序来保持工作效率，但 WIP 阻止用户的访问。 此信息可用于维护 Configuration Manager 中的 Windows 信息保护策略。 

