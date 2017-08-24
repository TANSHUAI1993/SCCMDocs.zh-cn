---
title: "使用 System Center Configuration Manager 创建任务序列媒体 | Microsoft Docs"
description: "创建任务序列媒体（如 CD）以将操作系统部署到 Configuration Manager 环境中的目标计算机。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: bd5448d70c2d465347de840cb197d4c33075c90a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建任务序列媒体

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用媒体从引用计算机中捕获操作系统映像，或者将操作系统部署到 System Center Configuration Manager 环境中的目标计算机。 你创建的媒体可以是 CD、DVD 集或者 USB 闪存驱动器。  

 媒体的主要用途是，在没有网络连接或者使用低带宽连接来连接到 Configuration Manager 站点的目标计算机上部署操作系统。 但是，部署媒体也用于在现有 Windows 操作系统之外启动操作系统部署。 部署媒体的这个第二用途在以下情况下很重要：目标计算机上没有操作系统，操作系统处于不工作的状态，或者管理用户想将目标计算机上的硬盘重新分区。  

 部署媒体包括可启动媒体、独立媒体和预留媒体。 部署媒体的内容因你使用的媒体类型而异。 例如，独立媒体包含用于部署操作系统的任务序列，而其他类型的媒体从管理点检索任务序列。  

> [!IMPORTANT]  
>  若要创建任务序列媒体，必须是从中运行 Configuration Manager 控制台的计算机上的管理员。 如果你不是管理员，则系统会在你启动创建任务序列媒体向导时提示提供管理员凭据。  

##  <a name="BKMK_PlanCaptureMedia"></a>操作系统映像的捕获媒体  
 捕获媒体可让你从引用计算机中捕获操作系统映像。 捕获媒体包含用于启动引用计算机的启动映像，以及用于捕获操作系统映像的任务序列。 有关如何创建捕获媒体的信息，请参阅[使用 System Center Configuration Manager 创建捕获媒体](create-capture-media.md)。  

##  <a name="BKMK_PlanBootableMedia"></a>可启动媒体操作系统部署  
 可启动媒体仅包含启动映像、可选的 [预启动命令](../understand/prestart-commands-for-task-sequence-media.md) 及其必需的文件和 Configuration Manager 二进制文件。 在目标计算机启动时，它连接到网络，并从网络中检索任务序列、操作系统映像和任何其他必需的内容。 由于任务序列不在媒体上，因此，你无需重新创建媒体就能更改任务序列或内容。  

> [!IMPORTANT]  
>  可启动媒体上的包并未加密。 管理用户必须采取适当的安全措施（例如向媒体添加密码），以确保未经授权的用户不能访问包内容。  

 有关如何创建可启动媒体的信息，请参阅[创建可启动媒体](create-bootable-media.md)。  

##  <a name="BKMK_PlanPrestagedMedia"></a>预留媒体操作系统部署  
 利用预留媒体，你可以在执行设置过程之前将可启动媒体和操作系统映像预留到硬盘上。 预留媒体是 Windows 映像格式 (WIM) 文件，可以由制造商安装在裸机上，也可以安装在未连接到 Configuration Manager 环境的企业暂存中心。  

 预留媒体包含用于启动目标计算机的启动映像，以及应用到目标计算机的操作系统映像。 你还可以指定要作为预留媒体的一部分包含的应用程序、包和驱动程序包。 此媒体不包含用于部署操作系统的任务序列。 在部署使用预留媒体的任务序列时，客户端会首先检查本地任务序列缓存以查找有效的内容，如果无法找到内容或内容已被修改，则客户端会从分发点下载内容。  

 在将新计算机发送给最终用户之前，预留媒体将应用到此计算机的硬盘驱动器。 在应用预留媒体后第一次启动计算机时，计算机会启动 Windows PE 并连接到管理点，以查找将完成操作系统部署过程的任务序列。  

> [!IMPORTANT]  
>  预留媒体上的包并未加密。 管理用户必须采取适当的安全措施（例如向媒体添加密码），以确保未经授权的用户不能访问包内容。  

 有关如何创建预留媒体的信息，请参阅[创建预留媒体](create-prestaged-media.md)。  

##  <a name="BKMK_PlanStandaloneMedia"></a>独立媒体操作系统部署  
 独立媒体包含部署操作系统所需的所有内容。 这包括任务序列和所需的任何其他内容。 由于部署操作系统所需的所有内容均存储在独立媒体上，因此，独立媒体所需的磁盘空间将显著大于其他类型的媒体所需的磁盘空间。  

 有关如何创建独立媒体的信息，请参阅[创建独立媒体](create-stand-alone-media.md)。  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>在使用为 HTTPS 配置的站点系统时的媒体注意事项  
 在将管理点和分发点均配置为使用 HTTPS 通信时，必须在主站点而不是管理中心站点上创建启动媒体和预留媒体。 此外，还要考虑下列两点，以帮助你确定是将媒体配置为动态还是配置为基于站点：  

-   若要将媒体配置为动态媒体，则所有主站点均必须具有你从中创建了媒体的站点的根 CA。 可以将根 CA 导入到层次结构中的所有主站点。  

-   在 Configuration Manager 层次结构中的主站点使用不同的根 CA 时，必须在每个站点使用基于站点的媒体。  
