---
title: Office 365 客户端管理仪表板
titleSuffix: Configuration Manager
description: 从 Office 365 客户端管理仪表板查看 Office 365 客户端信息
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e4f843d8984cbf27fed4e309af523855ab14002
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70380239"
---
# <a name="office-365-client-management-dashboard"></a>Office 365 客户端管理仪表板

从 Configuration Manager 1802 版开始，可以从 Office 365 客户端管理仪表板查看 Office 365 客户端信息。 选中图形部分时，Office 365 客户端管理仪表板会显示相关设备的列表。 <!--1357281 -->

## <a name="prerequisites"></a>先决条件

Office 365 客户端管理仪表板中显示的数据来自硬件清单。 启用硬件清单，并选择“Office 365 ProPlus 配置”  硬件清单类，以便在仪表板中显示数据。
 
1. 启用硬件清单（如果尚未启用）。 有关详细信息，请参阅[配置硬件清单](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。
2. 在 Configuration Manager 控制台中，导航到“管理”   > “客户端设置”   > “默认客户端设置”  。  
3. 在“主页”  选项卡上的“属性”  组中，单击“属性”  。  
4. 在**默认客户端设置**对话框中，单击**硬件清单**。  
5. 在**设备设置**列表中，单击**设置类**。  
6. 在“硬件清单类”  对话框中，选择“Office 365 ProPlus 配置”  。  
7. 单击**确定**以保存所做的更改并关闭**硬件清单类**对话框。 

Office 365 客户端管理仪表板在硬件清单得到报告的同时开始显示数据。

## <a name="viewing-the-office-365-client-management-dashboard"></a>查看 Office 365 客户端管理仪表板

若要在 Configuration Manager 控制台中查看 Office 365 客户端管理仪表板，请依次转到“软件库”   > “概述”   > “Office 365 客户端管理”  。 在仪表板顶部，使用“集合”  下拉列表设置按特定集合的成员筛选仪表板数据。 从 Configuration Manager 1802 版开始，选择图形部分时，Office 365 客户端管理仪表板会显示相关设备的列表。

Office 365 客户端管理仪表板提供以下信息的相关图表：

- Office 365 客户端数
- Office 365 客户端版本
- Office 365 客户端语言
- Office 365 客户端频道 有关详细信息，请参阅 [Office 365 专业增强版的更新频道概述](/DeployOffice/overview-of-update-channels-for-office-365-proplus)。


## <a name="bkmk_o365_readiness"></a>Office 365 专业增强版集成的就绪情况
<!--3735402-->
从 Configuration Manager 1902 版开始，可以使用仪表板识别准备升级到 Office 365 专业增强版的设备，且识别的可信度非常高。 通过此集成可以深入了解环境中所用 Office 加载项和宏的任何潜在兼容性问题。 然后使用 Configuration Manager 将 Office 部署到已就绪的设备。

Office 365 客户端管理仪表板包含新磁贴“Office 365 专业增强版升级就绪情况”  。 此磁贴是处于以下状态的设备的条形图：
- 未评估
- 升级准备就绪
- 需要评审

选择一个状态，钻取到设备列表。 此准备情况报表显示更多设备相关详细信息。 包括用于说明 Office 加载项和宏的兼容性状态的列。

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Office 365 专业增强版集成就绪情况的先决条件

- 在客户端设置中启用硬件清单。 有关详细信息，请参阅[先决条件](#prerequisites)部分。  

- 设备需要连接到 Office 内容分发网络 (CDN) 才能下载加载项就绪情况文件。 有关详细信息，请参阅[内容分发网络](https://docs.microsoft.com/office365/enterprise/content-delivery-networks)。 如果设备无法下载此文件，说明加载项状态为“需要审核”  。  

    > [!Note]  
    > 此功能没有数据发送给 Microsoft。  

### <a name="bkmk_ort"></a>详细的宏就绪情况

默认情况下，扫描代理会查看每个设备上最近使用的 (MRU) 文件列表。 它对此列表中支持宏的文件计数。 这些文件包括下列类型：
- 启用宏的 Office 文件格式，例如启用了宏的 Excel 工作簿 (.xlsm) 或启用了宏的 Word 文档 (.docm)  
- 不指示是否有宏内容的旧版 Office 格式。 例如，Excel 97-2003 工作簿 (.xls)。

如果需要更详细的评估，请部署“Office Readiness Toolkit”  。 此工具分析宏文件中的代码。 它会检查是否存在任何潜在的兼容性问题。 例如，文件是否使用了较新版 Office 中已更改的功能。 运行 Office Readiness Toolkit 后，Configuration Manager 可以使用其结果。 这些额外的数据可提高设备就绪情况计算的准确度。 有关详细信息，请参阅[使用 Readiness Toolkit 评估 Office 365 专业增强版的应用程序兼容性](https://aka.ms/readinesstoolkit)。

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 专业增强版升级就绪情况仪表板

（从版本 1906 中引入） 

<!--4021125-->
为了帮助你确定哪些设备已准备好升级到 Office 365 专业增强版，我们从版本 1906 开始推出了就绪情况仪表板。 它包括 Configuration Manager 当前分支版本 1902 中发布的“Office 365 专业增强版升级就绪情况”  磁贴。 此仪表板上的以下新磁贴有助于评估 Office 加载项和宏就绪情况：

- 部署
- 设备准备情况
- 加载项就绪情况
- 加载项支持语句
- 版本数排名靠前的加载项
- 包含宏的设备数
- 宏就绪情况
- 宏公告

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>使用 Office 365 专业增强版升级就绪情况仪表板
 
1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“Office 365 客户端管理”   。
1. 选择**Office 365 ProPlus 升级就绪情况**"节点。
1. 更改**集合**和**目标 Office 体系结构**，以更改仪表板中的信息中继。

![Office 365 专业增强版升级就绪情况仪表板](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Office 365 专业增强版升级就绪情况仪表板](./media/4021125-office-365-to-add-ins.png)

![Office 365 专业增强版升级就绪情况仪表板](./media/4021125-office-365-macro-advisories.png)

## <a name="next-steps"></a>后续步骤

[使用 Configuration Manager 管理 Office 365 专业增强版](/sccm/sum/deploy-use/manage-office-365-proplus-updates)
