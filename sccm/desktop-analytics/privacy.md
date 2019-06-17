---
title: 桌面的分析数据隐私
titleSuffix: Configuration Manager
description: 桌面分析是一种致力于客户数据隐私
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb109bc126902f4d68b876860e8d5ec3ff514bb8
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67146017"
---
# <a name="desktop-analytics-data-privacy"></a>桌面的分析数据隐私

桌面分析是完全致力于保护客户数据隐私，主要集中在这些原则：

- **透明度：** 我们完全记录 Windows 诊断事件。 请查看与你公司的安全性和符合性团队。 Windows 诊断数据查看器可以查看从给定的设备发送的诊断数据。 有关详细信息，请参阅[诊断数据查看器概述](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview)。  

- **控制：** 控制诊断数据以与 Microsoft 共享的级别。 Windows 10 版本 1709，添加新的策略以限制到 Desktop 分析所需的最低增强的诊断数据。  

- **安全性：** Microsoft 通过强大的安全性和加密保护数据。  

- **信任：** 桌面的分析支持 Microsoft [Privacy Statement](https://privacy.microsoft.com/privacystatement)并[联机服务条款](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)。  



## <a name="diagnostic-data-flow"></a>诊断数据的流

下图显示了如何诊断数据从各个设备通过诊断数据服务，Azure Log Analytics 存储和 Log Analytics 工作区：

![说明设备中的诊断数据的流的关系图](media/da-data-flow.png)

1. 登录到 Azure 门户，并载入到 Desktop 分析。 创建 Azure AD 应用以通过 Configuration Manager 连接。 如果设置了桌面分析时，所选的位置中创建的 Azure Log Analytics 工作区。  

2. 将 Configuration Manager 连接和注册设备  

    1. 使用 Azure AD 应用程序详细信息在 Configuration Manager 中配置桌面分析云服务。  

    2. 在 15 分钟内，Configuration Manager 使用桌面 Analytics 同步设备集合和部署计划。 它会重复此过程每隔一小时。  

    3. Configuration Manager 设置的目标集合中的商业 ID、 诊断数据级别和其他设置的设备。 此配置指定要显示在桌面分析工作区中的设备。  

    4. 将兼容性更新部署到所有目标设备。  

3. 设备将诊断数据发送到 Windows 的 Microsoft 诊断数据管理服务。 此服务被托管在美国。  

4. 每一天，Microsoft 会生成 IT 为中心的见解的快照。 此快照将 Windows 中的诊断数据与你为注册的设备的输入相结合。 此过程发生在临时存储中，仅供 Desktop 分析。 在美国的 Microsoft 数据中心托管临时存储。 快照隔离的商用 id。  

5. 然后，快照会复制到相应的 Azure Log Analytics 工作区。  

6. 桌面 Analytics 在 Azure Log Analytics 存储中存储你的输入。 这些配置包括部署计划，以及升级和重要性的资产决策。  



## <a name="other-resources"></a>其他资源

与隐私相关的桌面分析经常询问的问题，请参阅[隐私常见问题解答](/sccm/desktop-analytics/faq#privacy)。

有关相关的隐私方面的详细信息，请参阅以下文章：

- [Windows 10 和 IT 决策制定者 GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [在你的组织中配置 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7、 Windows 8 和 Windows 8.1 appraiser 诊断数据事件和字段](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10，版本 1809年基本级别 Windows 诊断事件和字段](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10 版本 1709年增强的诊断数据的事件和使用的桌面 Analytics 字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [诊断数据查看器概述](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [许可条款和文档](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [安全和隐私在 Microsoft Azure 数据中心](https://azure.microsoft.com/global-infrastructure/)  

- [可信云中的置信度](https://azure.microsoft.com/overview/trusted-cloud/)  

- [信任中心](https://www.microsoft.com/trustcenter)  
