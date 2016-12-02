---
title: "从软件清单中排除文件夹 | System Center Configuration Manager"
description: "从 System Center Configuration Manager 中的软件清单中排除文件夹。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07328e086a09e924a4807b05759937929152bda9


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>如何从 System Center Configuration Manager 中的软件清单中排除文件夹

*适用范围：System Center Configuration Manager (Current Branch)*

使用以下步骤为站点配置 System Center Configuration Manager 软件清单。  

 此过程将为软件清单配置默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要用使用软件清单的计算机的集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

### <a name="to-configure-software-inventory"></a>若要配置软件清单  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” 。  

3.  单击“默认客户端设置” 。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  在“默认设置”  对话框中，单击“软件清单” 。  

6.  在“设备设置”  列表中，配置以下值：  

    -   **启用客户端上的软件清单** - 从下拉列表中选择“True”。  

    -   **软件清单和文件收集日程安排** – 配置客户端收集软件清单和文件的间隔。 使用默认值为“7 天”  ，或单击“日程安排”  以配置自定义间隔。  

7.  配置所需的客户端设置。 有关可以配置的软件清单客户端设置的列表，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md#BKMK_SoftInventoryDeviceSettings)主题中的[软件清单](../../../../core/clients/deploy/about-client-settings.md)部分。  

8.  单击“确定”  以关闭“配置客户端设置”  对话框。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Nov16_HO1-->


