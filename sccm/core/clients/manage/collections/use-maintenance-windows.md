---
title: "使用维护时段 | System Center Configuration Manager"
description: "使用集合和维护时段在 System Center Configuration Manager 中有效管理客户端。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c29d8a1bc0d224113a1c906893308d5582894a01


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>如何在 Configuration Manager 中使用维护时段

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的维护时段提供一种方法，通过该方法，管理用户可定义可对设备集合的成员执行各种 Configuration Manager 操作的时间段。 可以使用维护时段来帮助确保在不会影响组织工作效率的时间段进行客户端配置更改。  

 以下 Configuration Manager 操作支持维护时段：  

-   软件部署  

-   软件更新部署  

-   符合性设置部署和评估  

-   操作系统部署  

-   任务序列部署  

 将为具有开始日期、开始和完成时间以及定期模式的集合配置维护时段。 每个维护时段的持续时间必须小于 24 小时。 默认情况下，不允许在维护时段外进行部署所导致的计算机重启，但你可以在每个部署的设置中替代默认设置。 维护时段仅影响部署程序的运行时间；配置为在本地下载并运行的应用程序可在维护时段外下载内容。  

 如果客户端计算机是配置了维护时段的设备集合的成员，那么，只有在允许的最长运行时间未超出为维护时段配置的持续时间时，部署程序才会运行。 如果程序未能运行，则会生成警报，并且将在具有可用时间的下一次计划的维护时段中重新运行部署。  

## <a name="using-multiple-maintenance-windows"></a>使用多个维护时段  
 如果客户端计算机是配置了维护时段的多个设备集合的成员，则以下规则适用：  

-   如果维护时段未重叠，则将它们视为两个独立的维护时段。  

-   如果维护时段重叠，则将它们视为包含两个维护时段所涵盖的时间段的单一维护时段。 例如，如果有两个维护时段，每个维护时段的持续时间为 1 小时，其中 30 分钟重叠，则维护时段的有效持续时间将为 90 分钟。  

 当用户从软件中心中启动应用程序安装时，应用程序将立即安装，而无论维护时段如何配置。  

 如果目的为“必需”  的应用程序部署在非营业时间（由用户在软件中心中配置）内达到其安装期限，将安装应用程序。  

### <a name="how-to-configure-maintenance-windows"></a>如何配置维护时段  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

2.  在“资产和符合性”  工作区中，单击“设备集合” 。  

3.  在“设备集合”  列表中，选择要为其配置维护时段的集合。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  在“&lt;集合名称\>属性”对话框的“维护时段”选项卡中，单击“新建”图标。  

    > [!NOTE]  
    >  你不能为“所有系统”  集合创建维护时段。  

6.  在“&lt;新\>计划”对话框中，为维护时段指定名称、计划和定期模式。 此外可以启用此选项，将计算只应用于任务序列。  

7.  从“将此计划应用到”  下拉列表中，选择将此维护时段应用于所有部署、仅软件更新还是仅任务序列。  

8.  单击“确定”关闭“&lt;新\>计划”对话框，并创建新维护时段。  

9. 关闭“&lt;集合名称\>属性”对话框。  



<!--HONumber=Nov16_HO1-->


