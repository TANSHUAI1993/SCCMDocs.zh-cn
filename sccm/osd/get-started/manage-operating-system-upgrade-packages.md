---
title: 管理 OS 升级包
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理 OS 升级包。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7b8b18cbec5a3b5972a448e8a70339533dc11fb
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456000"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>使用 Configuration Manager 管理 OS 升级包

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的 OS 升级包包含用于在计算机上升级现有 OS 的 Windows 安装程序源文件。 本文介绍如何添加、分发和维护 OS 升级包。



##  <a name="BKMK_AddOSUpgradePkgs"></a> 添加 OS 升级包  

在使用 OS 升级包之前，请先将其添加到 Configuration Manager 站点。 

1.  在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统升级包”节点。  

2.  在功能区的“主页”选项卡上的“创建”组中，选择“添加操作系统升级包”。 此操作将启动“添加操作系统升级向导”。  

3.  在“数据源”页面上，指定以下设置： 

    - OS 升级包的安装源文件的网络**路径**。 例如，`\\server\share\path`。  

        > [!NOTE]  
        >  安装源文件包含 setup.exe 和其他文件以及用于安装 OS 的文件夹。  

        > [!IMPORTANT]  
        >  限制对这些安装源文件的访问，以防受到恶意篡改。  

    - 如果要在客户端上预缓存内容，请指定映像的**体系结构**和**语言**。 有关详细信息，请参阅[配置预缓存内容](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)。  

4.  在“常规”页面上，指定以下信息。 当你有多个 OS 升级包时，可利用这些信息对其进行识别。  

    -   **名称**：OS 升级包的唯一名称。  

    -   **版本**：可选的版本标识符。 此属性无需为该升级包的 OS 版本。 它通常为组织的包的版本。  

    -   **注释**：可选的简要说明。  

5.  完成向导。  


接下来，将 OS 升级包分发到分发点。  



##  <a name="BKMK_Distribute"></a> 将内容分发到分发点  

将 OS 升级包分发到与其他内容相同的分发点。 在部署任务序列之前，请将 OS 升级包分发到至少一个分发点。 有关详细信息，请参阅[分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)。  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## <a name="next-steps"></a>后续步骤

[创建用于升级 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)