---
title: "监视客户端 - 结合使用 Windows Analytics 和 Configuration Manager | Microsoft Docs"
description: "Windows Analytics 是在 Operations Management Suite 上运行的一组解决方案，借助这些解决方案，可以利用环境中的设备报告的 Windows 遥测数据获取关于环境当前状态的宝贵见解。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>结合使用 Windows Analytics 和 Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) 是在 [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) 上运行的一组解决方案。 通过这些解决方案可以形成对环境当前状态的见解。 环境中的设备报告 Windows 遥测数据。 可通过 [Operations Management Suite Web 门户](https://mms.microsoft.com)中的解决方案访问和分析此数据。 对于[升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)，还可通过将升级就绪情况连接到 Configuration Manager，直接在 Configuration Manager 控制台的监视节点中获取此数据。

Windows Analytics 使用的 Windows 遥测数据不会直接传输到 Configuration Manager 站点服务器。 客户端计算机将 Windows 遥测数据发送到遥测服务。 然后，相关数据将传输到组织的其中一个 OMS 工作区中托管的 Windows Analytics 解决方案。 随后 Configuration Manager 可以通过上下文中的链接将你转到 Web 门户中的相关数据，或者直接显示已连接到 Configuration Manager 的解决方案中的数据。 此外，还可以直接从 Operation Management Suite Web 门户查询此数据。

>[!Important]
>Configuration Manager 站点服务器报告给 Microsoft 的 [Configuration Manager 诊断和使用情况数据](../../plan-design/diagnostics/diagnostics-and-usage-data.md)完全独立于 Windows Analytics 和 Windows 遥测。

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>将客户端配置为向 Windows Analytics 报告数据

若要使客户端设备向 Windows Analytics 报告数据，设备必须配置与为组织托管 Windows Analytics 数据的 Operations Management Suite 工作区关联的商业 ID 键。 设备还必须配置为报告与特定解决方案或你想要使用的解决方案对应的遥测级别的遥测数据。 

### <a name="configure-windows-analytics-client-settings"></a>配置 Windows Analytics 客户端设置
若要配置 Windows Analytics，请在 Configuration Manager 控制台中选择“管理” > “客户端设置”，双击“创建自定义设备客户端设置”，然后选中“Windows Analytics”。  

然后，导航到“Windows Analytics”设置选项卡，配置以下内容：
  -  **商用 ID**  
商用 ID 键可用于将你管理的设备中的信息映射到托管你组织的 Windows Analytics 数据的 OMS 工作区。 如果已配置用于 Upgrade Readiness 的商用 ID 键，请使用此 ID。 如果还没有配置商用 ID 键，请参阅[生成商用 ID 键]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key)。

  -  **Windows 10 设备的遥测级别**   
若要了解每个 Windows 10 遥测级别收集的信息，请参阅[在组织中配置 Windows 遥测](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels)。

  -  **选择加入 Windows 7、8 和 8.1 设备上商业数据收集**   
若要了解选择加入后从这些操作系统中收集的数据，请从 Microsoft 下载并参阅 PDF 文件 [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965)（Windows 7、Windows 8 和 Windows 8.1 评估人员遥测事件和字段）。

  -  **配置 Internet Explore 数据收集**  
在运行 Windows 8.1 或更低版本的设备上，启用 Internet Explorer 数据收集后，Upgrade Readiness 可以检测可能会阻止顺利升级到 Windows 10 的 Web 应用程序不兼容问题。 可以每 Internet 区域启用一次 Internet Explorer 数据收集。 有关 Internet 区域的详细信息，请参阅[关于 URL 安全区域](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx)。

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>使用升级就绪情况识别 Windows 10 兼容性问题

借助升级就绪情况（以前称为 Upgrade Analytics），用户能够分析设备对 Windows 10 的准备情况及兼容情况。 通过此评估可以使升级更流畅。 将 Configuration Manager 连接到升级就绪情况后，可以直接在 Configuration Manager 控制台中访问此客户端升级兼容性数据。 然后可以从设备列表中设定要升级或修正的设备。

有关如何配置和连接到升级就绪情况的详细信息，请参阅[升级就绪情况](../../clients/manage/upgrade/upgrade-analytics.md)。

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>使用 Windows Analytics 确定 Windows 信息保护策略中的缺口

配置了 [Windows 信息保护](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) 策略的 Windows 10 版本 1703 及更高版本的设备报告关于可访问环境中的公司数据，但不属于 WIP 策略应用程序规则考虑范围的应用程序的遥测数据。 环境中的用户可能需要这些应用程序来保持工作效率，但无法访问这些应用程序，因此，了解其正在访问公司数据可帮助维护 Configuration Manager 中的 Windows 信息保护策略。 

可以使用此 [Operations Management Suite 查询](https://go.microsoft.com/fwlink/?linkid=849952)访问该 Windows 信息保护数据。