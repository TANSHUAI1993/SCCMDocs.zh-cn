---
title: "配置软件清单 | Microsoft Docs"
description: "配置软件清单，并从 Configuration Manager 中的软件清单中排除文件夹。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e60cec71c425e5e42d450cbeee366528d4b42405
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置软件清单

*适用范围：System Center Configuration Manager (Current Branch)*

 此过程将为软件清单配置默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要使用软件清单的计算机集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

## <a name="to-configure-software-inventory"></a>若要配置软件清单  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置”、“默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认设置”对话框中，选择“软件清单”。  

6.  在“设备设置”  列表中，配置以下值：  

    -   **启用客户端上的软件清单** - 从下拉列表中选择“True”。  

    -   **软件清单和文件收集日程安排** – 配置客户端收集软件清单和文件的间隔。   

7.  配置所需的客户端设置。 有关可以配置的软件清单客户端设置的列表，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md#software-inventory)主题中的[软件清单](../../../../core/clients/deploy/about-client-settings.md)部分。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  


## <a name="to-exclude-folders-from-software-inventory"></a>从软件清单中排除文件夹  

1.  使用 Notepad.exe，创建名为 **Skpswi.dat**的空文件。  

2.  右键单击 **Skpswi.dat** 文件，然后单击“属性” 。 在 Skpswi.dat 文件的文件属性中，选择“隐藏”  属性。  

3.  将 **Skpswi.dat** 文件放置在要从软件清单中排除的每个客户端硬盘或文件夹结构的根目录中。  

> [!NOTE]  
>  除非在客户端计算机上删除此文件，否则软件清单将不会再次列出该客户端驱动器清单。