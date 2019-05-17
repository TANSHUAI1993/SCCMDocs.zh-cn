---
title: 配置硬件清单
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中设置所有客户端或某个集合的硬件清单。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fecaa5a9fb74c9f8d473cc9dba6a307800fd70f9
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499954"
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置硬件清单

适用范围：System Center Configuration Manager (Current Branch)

此过程会为硬件清单配置默认客户端设置，并应用于层次结构中的所有客户端。 如果你希望这些设置仅应用于某些客户端，请创建自定义设备客户端设置，并将它分配给包含要使用硬件清单的设备的集合。 请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

> [!NOTE]  
>  如果客户端设备从多组客户端设置收到硬件清单设置，则来自每组设置的硬件清单类会在客户端报告硬件清单时进行合并。 此外，不检查具有更高优先级的自定义客户端设置中的类并不会禁止客户端清点该类。 

若要在除少数系统之外的大多数系统上禁用特定硬件清单类，需要在默认客户端设置中取消选中该类。 然后创建自定义客户端设置以启用该类，并将其部署到目标系统。


### <a name="to-configure-hardware-inventory"></a>若要配置硬件清单  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置” > “默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认设置”对话框中，选择“硬件清单”。  

6.  在“设备设置”  列表中，配置以下各项：  

    -   **针对客户端启用硬件清单** - 选择“是”。  

    -   **硬件清单计划** - 单击“计划”指定客户端收集硬件清单的间隔。  

7.  配置所需的其他[硬件清单客户端设置](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)。  

当客户端设备下一次下载客户端策略时，会使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [如何在 System Center Configuration Manager 中管理客户端](../../../../core/clients/manage/manage-clients.md)。  
