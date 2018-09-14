---
title: 将用户与计算机关联
titleSuffix: Configuration Manager
description: 配置 Configuration Manager 以在部署操作系统时将用户与目标计算机关联。
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 325b571adbcb2750eaa0b3a856dda753c43634f0
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755894"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>在 Configuration Manager 中将用户与目标计算机关联

*适用范围：System Center Configuration Manager (Current Branch)*

 使用 Configuration Manager 部署操作系统时，可以将用户与目标计算机关联。 如果单个用户或多个用户是目标计算机的主要用户，则此选项有效。  

 当你部署应用程序时，用户设备相关性支持以用户为中心的管理。 将用户与要在其上安装操作系统的目标计算机关联时，可以稍后将应用程序部署到该用户，应用程序将自动安装在目标计算机上。 尽管可以在操作系统部署过程中配置用户设备相关性的支持，但无法使用用户设备相关性来部署操作系统。  

 有关用户设备相关性的详细信息，请参阅[将用户和设备同用户设备相关性相链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。  

 可以使用几种方法将用户设备相关性集成到操作系统部署。 你可以将用户设备相关性集成到 PXE 部署、可启动媒体部署以及预留媒体部署中。  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>创建包括 **SMSTSAssignUsersMode** 变量的任务序列

 通过使用[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤将 SMSTSAssignUsersMode 变量添加到任务序列的开头。 此变量指定任务序列处理用户信息的方式。

 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSAssignUsersMode)。


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>创建用于收集用户信息的预启动命令

 预启动命令可以是带输入框的 VBScript。 它还可以是验证所输入用户数据的 HTML 应用程序 (HTA)。 

 预启动命令必须设置在运行任务序列时使用的 SMSTSUDAUsers 变量。 可以对计算机、集合或任务序列变量设置此变量。

 有关详细信息，请参阅[任务序列变量](/sccm/osd/understand/task-sequence-variables#SMSTSUDAUsers)。


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>配置分发点和媒体将用户与目标计算机关联的方式

 分发点或媒体支持将用户与部署操作系统的目标计算机相关联。 使用以下方法之一： 

 - [配置分发点以接受 PXE 启动请求](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)  
 - [创建可启动媒体](/sccm/osd/deploy-use/create-bootable-media)  
 - [创建预留媒体](/sccm/osd/deploy-use/create-prestaged-media)  


 配置用户设备相关性支持没有用于验证用户标识的内置方法。 当设置计算机的技术人员代表用户输入信息时，此行为很重要。 除了设置任务序列处理用户信息的方式外，在分发点和媒体上配置这些选项还能够限制从 PXE 启动或特定媒体类型中启动的部署。
