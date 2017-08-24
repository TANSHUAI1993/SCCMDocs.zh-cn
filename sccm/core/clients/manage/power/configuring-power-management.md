---
title: "配置电源管理 | Microsoft Docs"
description: "在 System Center Configuration Manager 中设置电源管理。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e111ac2545dd9e0b96a50c10246bb75d286a737a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中配置电源管理

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中使用电源管理之前，必须执行下列配置步骤。  

## <a name="enable-and-configure-power-management-client-settings"></a>启用和配置电源管理客户端设置  
 此过程配置电源管理的默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建一个自定义设备客户端设置，并将其分配给包含要使用电源管理的计算机的集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>如何启用电源管理并配置客户端设置  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” 。  

3.  单击“默认客户端设置” 。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  在“默认客户端设置”  对话框中，单击“电源管理” 。  

6.  配置电源管理客户端设置的以下值：  

    -   **允许的设备的电源管理** – 从下拉列表中，选择“真”  以启用电源管理。  

7.  配置所需的客户端设置。 关于可以配置的电源管理客户端设置的列表，请参阅 [关于 System Center Configuration Manager 中的电源管理](../../../../core/clients/deploy/about-client-settings.md#power-management)主题中的[电源管理](../../../../core/clients/deploy/about-client-settings.md)部分。  

8.  单击“确定”  以关闭“默认客户端设置”  对话框。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  

## <a name="exclude-computers-from-power-management"></a>从电源管理中排除计算机  
 你可以阻止计算机集合接收电源管理设置。 如果一台计算机是从电源管理设置中排除的任何集合的成员，该计算机将不会应用电源管理设置，即使它是应用电源管理设置的另一集合的成员。  

 你可能出于任何下列原因之一要从电源管理中排除计算机：  

-   你的业务要求需要始终开启计算机。  

-   已创建不希望在其上应用电源管理设置的计算机的控制集合。  

-   某些计算机不能应用电源管理设置。  

-   你想要从电源管理中排除运行 Windows Server 的计算机。  

> [!NOTE]  
>  如果客户端设置中配置了“允许用户从电源管理中排除其设备”  选项，用户就可以使用软件中心从电源管理中排除自己的计算机。  

 要了解已从电源管理中排除了哪些计算机，请运行“排除的计算机” 报表。 有关此报表的详细信息，请参阅[如何在 System Center Configuration Manager 中监视和规划电源管理](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)主题中的[排除的计算机](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded)。  

> [!IMPORTANT]  
>  运行 Windows XP 或 Windows Server 2003 的计算机上应用的电源设置不会还原为初始值，即使从电源管理中排除该计算机。 在更高版本的 Windows 中，从电源管理中排除一台计算机会导致所有电源设置还原到其原始值。 无法将单个电源设置还原为其初始值。  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>若要从电源管理中排除计算机集合  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“设备集合” 。  

3.  在“设备集合”  列表中，选择要从电源管理中排除的集合，然后，在“主页”  选项卡上的“属性”  组中单击“属性” 。  

4.  在 *<Collection Name\>*“属性”对话框的“电源管理”选项卡上，选择“永远不将电源管理设置应用于此集合中的计算机”。  

5.  单击“确定”以关闭 *<Collection Name\>*“属性”对话框并保存设置。  
