---
title: "配置硬件清单 | Microsoft Docs"
description: "在 System Center Configuration Manager 中设置所有客户端或某个集合的硬件清单。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0baadb95ec8dbb945f1a611ebb95a03cec3199bd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

此过程会为硬件清单配置默认客户端设置，并应用于层次结构中的所有客户端。 如果你希望这些设置仅应用于某些客户端，请创建自定义设备客户端设置，并将它分配给包含要使用硬件清单的设备的集合。 请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

> [!NOTE]  
>  如果客户端设备从多组客户端设置收到硬件清单设置，则来自每组设置的硬件清单类会在客户端报告硬件清单时进行合并。  

### <a name="to-configure-hardware-inventory"></a>若要配置硬件清单  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置” > “默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认设置”对话框中，选择“硬件清单”。  

6.  在“设备设置”  列表中，配置以下各项：  

    -   **针对客户端启用硬件清单** - 选择“True”。  

    -   **硬件清单计划** - 单击“计划”指定客户端收集硬件清单的间隔。  

7.  配置所需的其他[硬件清单客户端设置](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)。  

当客户端设备下一次下载客户端策略时，会使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  
