---
title: 桌面分析数据隐私
titleSuffix: Configuration Manager
description: 桌面分析提交给客户数据隐私
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aef08fb2d4c404ea66ded3d1a49d30af68fe4a95
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379739"
---
# <a name="desktop-analytics-data-privacy"></a>桌面分析数据隐私

桌面分析已完全提交给客户数据隐私，并中心于以下原则：

- **透明化**我们会完全记录 Windows 诊断事件。 查看公司的安全和合规性团队。 Windows 诊断数据查看器允许您查看从给定设备发送的诊断数据。 有关详细信息，请参阅[诊断数据查看器概述](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview)。  

- **控件**可以控制要与 Microsoft 共享的诊断数据级别。 Windows 10 版本1709添加了新策略，以将增强的诊断数据限制为桌面分析所需的最小值。  

- **安全**Microsoft 通过强大的安全性和加密来保护你的数据。  

- **建立**桌面分析支持 Microsoft[隐私声明](https://privacy.microsoft.com/privacystatement)和[在线服务条款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)。  



## <a name="diagnostic-data-flow"></a>诊断数据流

下图显示了诊断数据如何通过诊断数据服务、Azure Log Analytics 存储和 Log Analytics 工作区从单个设备流动：

![阐释来自设备的诊断数据流的关系图](media/da-data-flow.png)

1. 登录到 Azure 门户，并载入桌面分析。 创建 Azure AD 应用以连接 Configuration Manager。 设置桌面分析时，会在所选位置创建 Azure Log Analytics 工作区。  

2. 连接 Configuration Manager 并注册设备  

    1. 在 Configuration Manager 中配置桌面分析云服务，其中包含 Azure AD 应用详细信息。  

    2. 15分钟内 Configuration Manager 会将设备集合和部署计划与桌面分析同步。 此过程每小时重复一次。  

    3. Configuration Manager 设置目标集合中设备的商业 ID、诊断数据级别和其他设置。 此配置指定要在桌面分析工作区中显示的设备。  

    4. 将兼容性更新部署到所有目标设备。  

3. 设备将诊断数据发送到适用于 Windows 的 Microsoft 诊断数据管理服务。 此服务托管在美国中。  

4. Microsoft 每天都会生成一个以 IT 为中心的见解的快照。 此快照将来自 Windows 的诊断数据与已注册设备的输入合并在一起。 此过程发生在暂时性存储中，后者仅供桌面分析使用。 临时存储在 Microsoft 数据中心中的美国。 快照按商业 ID 隔离。  

5. 然后，将快照复制到相应的 Azure Log Analytics 工作区。  

6. 桌面分析在 Azure Log Analytics 存储中存储输入。 这些配置包括部署计划，以及用于升级和重要性的资产决策。  



## <a name="other-resources"></a>其他资源

有关桌面分析的隐私相关常见问题解答，请参阅[隐私常见问题解答](/sccm/desktop-analytics/faq#privacy)。

有关相关隐私方面的详细信息，请参阅以下文章：

- [Windows 10 和 IT 决策者的 GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [在组织中配置 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7、Windows 8 和 Windows 8.1 人员诊断数据事件和字段](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10 版本1809基本级别 Windows 诊断事件和字段](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10 版本1709增强的诊断数据事件和桌面分析所使用的字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [诊断数据查看器概述](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [许可条款和文档](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Microsoft Azure 数据中心的安全和隐私](https://azure.microsoft.com/global-infrastructure/)  

- [可信云中的置信度](https://azure.microsoft.com/overview/trusted-cloud/)  

- [信任中心](https://www.microsoft.com/trustcenter)  
