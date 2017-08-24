---
title: "创建捕获介质 - Configuration Manager | Microsoft Docs"
description: "使用“创建任务序列媒体向导”在 Configuration Manager 中创建捕获媒体，以从引用计算机中捕获操作系统映像。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5acf800ff5aebd849e294393337755145a60cca5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建捕获媒体

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中捕获媒体使用户可以从引用计算机中捕获操作系统映像。 在以下情况下使用捕获媒体：  

-   [创建用于捕获操作系统的任务序列](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> 如何创建捕获媒体  
 使用捕获媒体从引用计算机中捕获操作系统映像。 捕获媒体包含用于启动引用计算机的启动映像，以及用于捕获操作系统映像的任务序列。

通过使用创建任务序列媒体向导来创建捕获媒体。 在运行向导之前，请确保满足下列所有条件：  

|任务|描述|  
|----------|-----------------|  
|启动映像|请考虑以下关于将在任务序列中用于捕获操作系统的启动映像信息：<br /><br /> -   启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。<br />-   确保启动映像包含预配目标计算机所需的网络和大容量存储驱动程序。|  
|分发与任务序列关联的所有内容|必须将任务序列所需的所有内容至少分发到一个分发点。 这包括启动映像、操作系统映像和其他相关联的文件。 向导在创建独立媒体时从分发点中收集信息。 必须具有对该分发点上的内容库的 **读取** 访问权限。  有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。|  
|准备可移动的 USB 驱动器|对于可移动的 USB 驱动器：<br /><br /> 如果你要使用可移动的 USB 驱动器，该 USB 驱动器必须连接到运行向导的计算机，并且 USB 驱动器必须可被 Windows 检测为可移动设备。 向导将在创建媒体时直接写入 USB 驱动器。|  
|创建一个输出文件夹|对于 CD/DVD 集：<br /><br /> 在运行创建任务序列媒体向导以便为 CD 或 DVD 集创建媒体之前，你必须为向导创建的输出文件创建一个文件夹。 为 CD 或 DVD 集创建的媒体将以 .iso 文件形式直接写入该文件夹。|  

 使用以下过程来创建捕获媒体。  

#### <a name="to-create-capture-media"></a>创建捕获媒体  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”工作区中，展开“操作系统”，然后单击“任务序列”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列媒体”  以启动创建任务序列媒体向导。  

4.  在“选择媒体类型”  页上，选择“捕获媒体” ，然后单击“下一步” 。  

5.  在“媒体类型”  页上，指定媒体是闪存驱动器还是 CD/DVD 集，然后单击进行以下配置：  

    -   如果选择“USB 闪存驱动器” ，则指定要在其中存储内容的驱动器。  

    -   如果选择“CD/DVD 集”，请指定媒体的容量以及输出文件的名称和路径。 向导会将输出文件写入到此位置。 例如：**\\\servername\folder\outputfile.iso**  

         如果媒体的容量太小，无法存储整个内容，则会创建多个文件，从而必须将内容存储在多张 CD 或 DVD 上。 当需要多个媒体时，Configuration Manager 会在创建的每个输出文件的名称中添加序号。 此外，如果将应用程序与操作系统一起部署，而单个媒体无法容纳应用程序，则 Configuration Manager 会将应用程序存储到多个媒体中。 在运行独立媒体时，Configuration Manager 会提示用户提供下一个存储了应用程序的媒体。  

        > [!IMPORTANT]  
        >  如果选择现有的 .iso 映像，任务序列媒体向导将在你进入向导的下一页后立即从驱动器或共享中删除该映像。 即使随后取消该向导，也会删除这个现有的映像。  

     单击“下一步” 。  

6.  在“启动映像包”  页上，指定以下信息，然后单击“下一步” 。  

    > [!IMPORTANT]  
    >  指定的启动映像的体系结构必须适合于引用计算机的体系结构。 例如，x64 引用计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 引用计算机只能启动和运行 x86 启动映像。  

    -   在“启动映像包”  框中，指定用于启动引用计算机的启动映像。  

    -   在“分发点”  框中，指定启动映像所在的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        >  你必须对分发点上的内容库具有“读取”访问权限。  

7.  完成向导。  
