---
title: "配置硬件清单 | Microsoft Docs"
description: "在 System Center Configuration Manager 中设置所有客户端或某个集合的硬件清单。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: f39714e53e1b38c162e2c0418356d223432fdd87


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

使用以下步骤为站点配置 System Center Configuration Manager 硬件清单。  

 此过程会为硬件清单配置默认客户端设置，并应用于层次结构中的所有客户端。 如果你希望这些设置仅应用于某些客户端，请创建自定义设备客户端设置，并将它分配给包含要使用硬件清单的设备的集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

> [!NOTE]  
>  如果客户端设备从多组客户端设置收到硬件清单设置，则来自每组设置的硬件清单类会在客户端报告硬件清单时进行合并。  

### <a name="to-configure-hardware-inventory"></a>若要配置硬件清单  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” 。  

3.  单击“默认客户端设置” 。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  在“默认设置”  对话框中，单击“硬件清单” 。  

6.  在“设备设置”  列表中，配置以下各项：  

    -   **启用客户端上的硬件清单** - 从下拉列表中选择“True” 。  

    -   **硬件清单计划** - 指定客户端收集硬件清单的间隔。 使用默认值为“7 天”  ，或单击“日程安排”  以配置自定义间隔。  

7.  配置所需的任何其他客户端设置。 有关可以配置的硬件清单客户端设置的列表，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md)主题中的[硬件清单](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)部分。  

8.  单击“确定”  来关闭“默认设置”  对话框。  

 当客户端设备下一次下载客户端策略时，会使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Dec16_HO3-->


