---
title: "从软件清单中排除文件夹 | Microsoft Docs"
description: "从 System Center Configuration Manager 中的软件清单中排除文件夹。"
ms.custom: na
ms.date: 12/04/2016
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
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>如何从 System Center Configuration Manager 中的软件清单中排除文件夹

*适用范围：System Center Configuration Manager (Current Branch)*

 此过程将为软件清单配置默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要使用软件清单的计算机集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

### <a name="to-configure-software-inventory"></a>若要配置软件清单  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置”、“默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认设置”对话框中，选择“软件清单”。  

6.  在“设备设置”  列表中，配置以下值：  

    -   **启用客户端上的软件清单** - 从下拉列表中选择“True”。  

    -   **软件清单和文件收集日程安排** – 配置客户端收集软件清单和文件的间隔。   

7.  配置所需的客户端设置。 有关可以配置的软件清单客户端设置的列表，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md#software-inventory)主题中的[软件清单](../../../../core/clients/deploy/about-client-settings.md)部分。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  



<!--HONumber=Dec16_HO1-->


