---
title: "配置客户端状态 | Microsoft Docs"
description: "在 System Center Configuration Manager 中选择客户端状态设置。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 060d63ab8bce9c3bb39d2db404580b9f59416d33
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置客户端状态

*适用范围：System Center Configuration Manager (Current Branch)*

在可以监视 System Center Configuration Manager 客户端状态和修正所发现的问题之前，必须配置站点，以指定用于将客户端标记为不活动的参数，以及配置选项以便在客户端的活动程度低于指定的阈值时向你发出警报。 还可以禁止计算机自动修正客户端状态发现的任何问题。  

##  <a name="BKMK_1"></a>配置客户端状态  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，单击“客户端状态” ，然后，在“主页”  选项卡中，在“客户端状态”  组中单击“客户端状态设置” 。  

3.  在“客户端状态设置属性”  对话框中，指定下列值以确定客户端活动程度：  

    > [!NOTE]  
    >  如果不符合任何设置，则将客户端标记为不活动。  

    -   **以下几天的客户端策略请求:** 指定自客户端请求策略以来的天数。 默认值为 **7** 天。  

    -   **以下几天的检测信号发现:** 指定自客户端计算机将检测信号发现记录发送到站点数据库以来的天数。 默认值为 **7** 天。  

    -   **以下几天的硬件清单:** 指定自客户端计算机将硬件清单记录发送到站点数据库以来的天数。 默认值为 **7** 天。  

    -   **以下几天的软件清单:** 指定自客户端计算机将软件清单记录发送到站点数据库以来的天数。 默认值为 **7** 天。  

    -   **以下几天的状态消息:** 指定自客户端计算机将状态消息发送到站点数据库以来的天数。 默认值为 **7** 天。  

4.  在“客户端状态设置属性”  对话框中，指定下列值以确定将客户端状态历史记录数据保留多长时间：  

    -   **保留以下几天的客户端状态历史记录:** 指定要将客户端状态历史记录在站点数据库中保留多长时间。 默认值为 **31** 天。  

5.  单击“确定”  以保存属性和关闭“客户端状态设置属性”  对话框。  

##  <a name="BKMK_Schedule"></a>配置客户端状态的计划  

1.  在 Configuration Manager 控制台中，单击“监视” 。  

2.  在“监视”  工作区中，单击“客户端状态” ，然后，在“主页”  选项卡中，在“客户端状态”  组中单击“计划客户端状态更新” 。  

3.  在“计划客户端状态更新”  对话框中，配置所要的客户端状态更新间隔，然后单击“确定”。  

    > [!NOTE]  
    >  如果更改客户端状态更新的计划，则此更新将在下一次计划的客户端状态更新（对于以前配置的计划而言）之后才会生效。  

##  <a name="BKMK_2"></a>配置客户端状态的警报  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“设备集合” 。  

3.  在“设备集合”  列表中，选择要为其配置警报的集合，然后，在“主页”  选项卡中，在“属性”  组中单击“属性” 。  

    > [!NOTE]  
    >  无法为用户集合配置警报。  

4.  在“&lt;集合名称\>”的“属性”对话框的“警报”选项卡上，单击“添加”。  

    > [!NOTE]  
    >  仅在与你关联的安全角色具有警报的权限时，“警报”  选项卡才可见。  

5.  在“添加新的集合警报”  对话框中，选择要在客户端状态阈值低于特定值时生成的警报，然后单击“确定” 。  

6.  在“警报”  选项卡的“条件”  列表中，选择每个客户端状态警报，然后指定下列信息。  

    -   **警报名称** - 接受默认名称，或者输入新的警报名称。  

    -   **警报严重性** – 从下拉列表中，选择将显示在 Configuration Manager 控制台中的警报级别。  

    -   **引发警报** - 指定警报的阈值百分比。  

7.  单击“确定”关闭“&lt;集合名称\>”的“属性”对话框。  

##  <a name="BKMK_3"></a>禁止计算机自动修正问题  

1.  在要禁止其自动修正问题的客户端计算机上打开注册表编辑器。  

    > [!WARNING]  
    >  如果不正确地使用注册表编辑器，可能导致严重问题，或许需要您重新安装操作系统。 Microsoft 不保证能够解决因注册表编辑器使用不当而导致的问题。 使用注册表编辑器的风险由您自己承担。  

2.  导航到“HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly” 。  

3.  为此注册表项输入下列值之一：  

    -   **True** - 客户端计算机不会自动修正发现的任何问题。 但是，你在“监视”  工作区中仍会收到与此客户端相关的任何问题的警报。  

    -   **False** – 客户端计算机将自动修正发现的问题并且将在“监视”工作区中发出警报。 此为默认设置。  

4.  关闭注册表编辑器。  

 还可以使用 CCMSetup **NotifyOnly** 安装属性来安装客户端，以禁止它们自动修正问题。 有关此客户端安装属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  
