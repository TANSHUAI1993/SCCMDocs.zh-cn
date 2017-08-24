---
title: "Technical Preview 1611 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1611 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: d2ad00e8-9f10-41b6-816a-d8542c23a22e
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5e77ebbfd3f3d573d903fe58024a22feb9884e4a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1611-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1611 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*



本文介绍了 System Center Configuration Manager Technical Preview 1611 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    

**此 Technical Preview 中的已知问题：**   
- ***先决条件状态***：安装版本 1611 时，先决条件的整体状态可能显示为已通过并出现警告，但不会列出导致警告的先决条件。 这可能是由以下两个先决条件引起的：
  - SQL 索引创建内存选项
  - 检查受支持的 SQL Server 版本  

 由于这些只是警告，因此可以忽略。

- ***PowerShell***：从 Configuration Manager 控制台连接到 Windows PowerShell 时，可能会收到以下错误： **Microsoft.ConfigurationManagement.PowerShell.Types.ps1xml 未进行数字签名**。  

   可通过使用版本 1610 中的已签名版本替换某些文件来解决此问题。 从版本 1610 安装中的“&lt;安装目录>\AdminConsole\bin”**\**文件夹复制所有具有以下扩展名的文件：**.psd1**、**.ps1xml** 和 **.psm1**。 将这些文件粘贴到 Technical Preview 1611 安装中的“&lt;安装目录>\AdminConsole\bin”**\**文件夹，覆盖 1611 版本的文件。


**以下是可以试用的此版本的新功能。**  

## <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>为可用部署和任务序列预先缓存内容
在此技术预览中，对于可用的部署和任务序列，可选择使用预先缓存功能，让客户端在用户安装内容之前仅下载相关内容。

例如，假设要部署 Windows 10 就地升级任务序列，只想为所有用户提供单个任务序列，并且具有多个体系结构和/或语言。 在 Current Branch 中，如果创建可用部署，然后用户在软件中心中单击“安装”，则将在此时下载内容。 这在安装准备启动之前增加了额外时间。 或者，如果在 Current Branch 中创建可用的任务序列部署，则将下载任务序列中引用的所有内容。 这包括所有语言和体系结构的操作系统升级包。 如果每个包大小都约为 3 GB，则下载包可能会很大。

借助预先缓存内容功能，用户可选择允许客户端在收到部署后立即下载适用的内容。 因此，当用户在软件中心中单击“安装”时，内容便已就绪，并且安装可以快速启动，因为内容位于本地硬盘上。

### <a name="to-configure-the-pre-cache-feature"></a>配置预先缓存功能

1. 为特定体系结构和语言创建操作系统升级包。 在包的“数据源”选项卡上指定体系结构和语言。 对于语言，使用十进制转换（例如，英语的十进制为 1033，其十六进制等效项是 0x0409）。 有关详细信息，请参阅[创建用于升级操作系统的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)。

    体系结构和语言值用于匹配将在下一步中创建的任务序列步骤条件，以确定是否应预先缓存操作系统升级包。
2. 为不同的语言和体系结构创建具有条件步骤的任务序列。 例如，对于英语版本，可创建如下所示的步骤：

    ![预先缓存属性](media/precacheproperties2.png)

    ![预先缓存选项](media/precacheoptions2.png)  

3. 部署任务序列。 对于预先缓存功能，请配置以下各项：
    - 在“常规”选项卡上，选择“此任务序列的预下载内容”。
    - 在“部署设置”选项卡上，配置任务序列，将“目的”配置为“可用”。 如果创建**所需**部署，预先缓存功能将不起作用。
    - 在“计划”选项卡上，对于“当此部署可用时进行计划”设置，选择将来的某一时间，以便在部署对用户可用之前为客户端提供足够的时间来预先缓存内容。 例如，可将可用时间设置为未来 3 小时，以便有足够的时间来预先缓存内容。  
    - 在“分发点”选项卡上，配置“部署选项”设置。 如果用户开始安装之前，该内容未预先缓存到客户端，则使用这些设置。


### <a name="user-experience"></a>用户体验
- 客户端收到部署策略时，将开始预先缓存内容。 这包括所有引用的内容（任何其他包类型），并且仅包括基于任务序列中设置的条件匹配客户端的操作系统升级包。
- 部署对用户可用时（部署的“计划”选项卡上的设置），将显示一条通知，告知用户有关新部署的信息以及该部署在软件中心中可见。 用户可转到软件中心并单击“安装”以开始安装。
- 如果内容未完全预先缓存，则它将使用部署的“部署选项”选项卡上指定的设置。 建议在创建部署和用户可使用部署之间保留足够的时间，以允许客户端预先缓存内容。


## <a name="see-also"></a>另请参阅
[System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)
