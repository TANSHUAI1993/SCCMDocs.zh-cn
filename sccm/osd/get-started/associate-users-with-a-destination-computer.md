---
title: "将用户与目标计算机相关联 | Microsoft Docs"
description: "配置 System Center Configuration Manager 以在部署操作系统时将用户与目标计算机关联。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0331567b94a99b29cc73c16de17a9f3bc6b9e43
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>将用户与 System Center Configuration Manager 中的目标计算机关联

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 部署操作系统时，可以将用户与在其中部署操作系统的目标计算机关联。 此配置操作包括以下各项：  

-   单一用户是目标计算机的主要用户。  

-   多个用户是目标计算机的主要用户。  

 当你部署应用程序时，用户设备相关性支持以用户为中心的管理。 当你将用户与要在其上安装操作系统的目标计算机关联时，你可以稍后将应用程序部署到该用户，并且应用程序将自动安装在目标计算机上。 但是，尽管你能够在部署操作系统时配置对用户设备相关性的支持，但你无法使用用户设备相关性来部署操作系统。  

 有关用户设备相关性的详细信息，请参阅[将用户和设备同用户设备相关性相链接](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>如何在部署操作系统时指定用户  
 下表列出了一些操作，你可以执行这些操作以将用户设备相关性集成到操作系统部署中。 你可以将用户设备相关性集成到 PXE 部署、可启动媒体部署以及预留媒体部署中。  

|操作|更多信息|  
|------------|----------------------|  
|创建包括 **SMSTSAssignUsersMode** 变量的任务序列|遵循 **Set Task Sequence Variable** 任务序列步骤将  [SMSTSAssignUsersMode](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) 变量添加到任务序列的开头。 此变量指定任务序列处理用户信息的方式。<br /><br /> 将该变量设置为以下值之一：<br /><br /> <br /><br /> **自动**：任务序列在用户和目标计算机之间自动创建关系，并部署操作系统。<br /><br /> **挂起**：任务序列在用户和目标计算机之间创建关系，但在部署操作系统之前等待管理用户的批准。<br /><br /> **已禁用**：任务序列不将用户与目标计算机关联，并继续部署操作系统。<br /><br /> <br /><br /> 也可以对计算机或集合设置此变量。 有关内置变量的详细信息，请参阅[任务序列内置变量](../../osd/understand/task-sequence-built-in-variables.md)。|  
|创建用于收集用户信息的预启动命令|预启动命令可以是具有输入框的 Visual Basic (VB) 脚本，或者可以是对所输入的用户数据进行验证的 HTML 应用程序 (HTA)。<br /><br /> 预启动命令必须设置在运行任务序列时使用的 **SMSTSUdaUsers** 变量。 可以对计算机、集合或任务序列变量设置此变量。 添加多个用户时请使用以下格式： *domain\user1, domain\user2, domain\user3*。|  
|配置分发点和媒体将用户与目标计算机关联的方式|当你 [将分发点配置为接受 PXE 启动请求](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) ，并通过使用创建任务序列媒体向导创建 [可启动媒体](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) 或 [预留媒体](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) 时，你可以指定分发点或媒体如何支持将用户与在其中部署操作系统的目标计算机关联。<br /><br /> 配置用户设备相关性支持没有用于验证用户标识的内置方法。 当设置计算机的技术人员代表用户输入信息时，这一点可能很重要。 除了设置任务序列处理用户信息的方式外，在分发点和媒体上配置这些选项还能够限制从 PXE 启动或特定媒体类型中启动的部署。|  
