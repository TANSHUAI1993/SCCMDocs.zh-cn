---
title: 创建任务序列媒体
titleSuffix: Configuration Manager
description: 创建任务序列媒体并将 OS 部署到 Configuration Manager 环境中的目标计算机。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 101cee8ed63cacfc41481b2df69b42e1760d8837
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082817"
---
# <a name="create-task-sequence-media"></a>创建任务序列媒体

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用媒体从引用计算机中捕获 OS 映像，或者将 OS 部署到 Configuration Manager 环境中的目标计算机。 你创建的媒体可以是 CD、DVD 集或者 USB 闪存驱动器。  

媒体的主要用途是，在没有网络连接或者使用低带宽连接来连接到 Configuration Manager 站点的目标计算机上部署操作系统。 不过，还可以使用媒体启动现有 Windows OS 之外的 OS 部署。 在没有现有 OS、OS 未正常工作，或者需要重新分区硬盘的情况下，此方法很有用。  

部署媒体包括可启动媒体、独立媒体和预留媒体。 媒体的内容因你使用的媒体类型而异。 例如，独立媒体包含用于部署 OS 的任务序列。 其他类型的媒体从管理点检索任务序列。  

> [!IMPORTANT]  
> 若要创建任务序列媒体，必须是从中运行 Configuration Manager 控制台的计算机上的管理员。 如果你不是管理员，在你启动创建任务序列媒体向导时，系统会提示你提供管理员凭据。  


## <a name="BKMK_PlanCaptureMedia"></a>捕获媒体

使用捕获媒体可以从引用计算机捕获 OS 映像。 捕获媒体包含用于启动引用计算机的启动映像，以及用于捕获 OS 映像的任务序列。

有关如何创建捕获媒体的详细信息，请参阅[创建捕获媒体](/sccm/osd/deploy-use/create-capture-media)。  


## <a name="BKMK_PlanBootableMedia"></a>可启动媒体

可启动媒体包含以下组件：

- 启动映像
- 可选的[预启动命令](/sccm/osd/understand/prestart-commands-for-task-sequence-media)及其所需的文件
- Configuration Manager 二进制文件

在目标计算机启动时，它连接到网络，并从网络中检索任务序列、OS 映像和任何其他必需的内容。 由于任务序列不在媒体上，因此，无需重新创建媒体就能更改任务序列或内容。  

> [!IMPORTANT]  
> 可启动媒体上的包并未加密。 采取适当的安全措施（例如向媒体添加密码），确保阻止未经授权的用户访问包内容。  

有关如何创建可启动媒体的详细信息，请参阅[创建可启动媒体](/sccm/osd/deploy-use/create-bootable-media)。  


## <a name="BKMK_PlanPrestagedMedia"></a>预留媒体

使用预留媒体，可以在执行预配过程之前将可启动媒体和 OS 映像应用到硬盘。 预留媒体是 Windows 映像 (WIM) 文件。 它可以由制造商安装在裸机上，也可以安装在未连接到生产 Configuration Manager 环境的暂存中心。  

预留媒体包含用于启动目标计算机的启动映像，以及应用到目标计算机的 OS 映像。 你还可以指定要作为预留媒体的一部分包含的应用程序、包和驱动程序包。 用于部署 OS 的任务序列不包含在该媒体中。 部署使用预留媒体的任务序列时，客户端会先检查本地任务序列缓存是否存在有效的内容。 如果找不到内容或内容已被修改，客户端会从分发点或对等机中下载内容。  

在将新计算机发送给最终用户之前，预留媒体将应用到此计算机的硬盘驱动器。 在应用预留媒体后首次启动计算机时，计算机将在 Windows PE 中启动。 它会连接到管理点以查找将完成 OS 部署过程的任务序列。  

> [!IMPORTANT]  
> 预留媒体上的包并未加密。 采取适当的安全措施（例如向媒体添加密码），确保阻止未经授权的用户访问包内容。  

有关如何创建预留媒体的详细信息，请参阅[创建预留媒体](/sccm/osd/deploy-use/create-prestaged-media)。  


## <a name="BKMK_PlanStandaloneMedia"></a>独立媒体

独立媒体包含部署 OS 所需的所有内容。 此内容包括任务序列和所需的任何其他内容。 由于部署 OS 所需的所有内容均存储在独立媒体上，因此，独立媒体所需的磁盘空间将大于其他类型的媒体所需的磁盘空间。  

有关如何创建独立媒体的详细信息，请参阅[创建独立媒体](/sccm/osd/deploy-use/create-stand-alone-media)。  


## <a name="considerations-when-using-https"></a>使用 HTTPS 时的注意事项

在将管理点和分发点均配置为使用 HTTPS 时，在主站点而不是管理中心站点上创建启动媒体和预留媒体。 此外，还要考虑以下两点，帮助确定是将媒体配置为动态媒体还是基于站点的媒体：  

- 若要将媒体配置为动态媒体，所有主站点均必须具有你从中创建了媒体的站点的根证书颁发机构 (CA)。 可以将根 CA 导入到层次结构中的所有主站点。  

- 在 Configuration Manager 层次结构中的主站点使用不同的根 CA 时，必须在每个站点使用基于站点的媒体。  
