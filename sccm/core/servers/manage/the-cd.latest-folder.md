---
title: CD.Latest 文件夹
titleSuffix: Configuration Manager
description: 了解有关从 Configuration Manager 控制台内部将更新传递到产品的过程。
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4f69d686a48af3c6e710c6aff592d71de1dbff1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496988"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Configuration Manager 的 CD.Latest 文件夹

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 具有从 Configuration Manager 控制台内部将更新传递到产品的过程。 为了支持更新 Configuration Manager 这一新方法，创建了一个名为 CD.Latest 的新文件夹。 此文件夹包含适用于站点更新版本的 Configuration Manager 安装文件的副本。  

CD.Latest 文件夹包含一个名为 Redist 的文件夹，该文件夹包含安装程序下载和使用的可再发行文件。 这些文件与在该 CD.Latest 文件夹中找到的 Configuration Manager 文件的版本相匹配。 当从 CD.Latest 文件夹运行安装程序时，必须使用与该安装程序的版本相匹配的文件。 可以指示安装程序从 Microsoft 下载新文件和当前文件，或指示安装程序使用包含在 CD.Latest 文件夹中的 Redist 文件夹中的文件。

基线媒体不包括 Redist 文件夹。 只有在安装控制台中更新后，站点才会创建 Redist 文件夹。 同时，从基线媒体安装站点时，请使用所用 Redist 文件夹。  

> [!TIP]  
> 请确保使用最新的可再发行文件。 如果最近没有下载可再发行文件，请计划允许安装程序从 Microsoft 执行该操作。   

下面是在管理中心站点或主站点服务器上创建或更新 CD.Latest 文件夹的方案：  

- 从 Configuration Manager 控制台安装更新或修补程序时，站点在 Configuration Manager 安装文件夹中创建或更新该文件夹。  

- 在运行内置 Configuration Manager 备份任务时，站点在指定备份文件夹位置下创建或更新该文件夹。  

- 使用基线媒体安装新站点时，站点将会创建 CD.Latest 文件夹。


## <a name="supported-scenarios"></a>支持的方案

以下场景支持 CD.Latest 文件夹中的源文件：  

### <a name="backup-and-recovery"></a>备份和恢复
若要恢复站点，请使用 CD.Latest 文件夹中与站点匹配的源文件。 使用内置站点备份任务运行站点备份时，CD.Latest 文件夹作为备份的一部分包括在内。

- 当你在站点恢复中重新安装站点时，会从包含在你的备份中的 CD.Latest 文件夹安装站点。 此操作会使用与你的站点备份和站点数据库匹配的文件版本安装站点。  

    - 如果没有访问正确 CD.Latest 文件夹版本的权限，请通过在实验室环境中安装一个站点来获取具有正确文件版本的 CD.Latest 文件夹。 然后，更新该站点，以匹配想要恢复的版本。  

    - 如果没有正确的 CD.Latest 文件夹及其内容，则无法恢复站点。 在这种情况下，需要重新安装站点。  

- 当没有 CD.Latest 文件夹，但是具有正常运行的子主站点或管理中心站点时，可以将该站点用作站点恢复的引用站点。  

### <a name="install-a-child-primary-site"></a>安装子级主站点
要在安装了一个或多个控制台中更新的管理中心站点下安装新的子主站点时，使用来自管理中心站点的 CD.Latest 文件夹中的安装程序和源文件。 此过程使用与管理中心站点的版本匹配的安装源文件。 有关详细信息，请参阅[使用安装向导来安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)。  

### <a name="expand-a-stand-alone-primary-site"></a>扩展独立主站点
要通过安装新的管理中心站点来扩展独立主站点时，使用来自主站点的 CD.Latest 文件夹中的安装程序和源文件。 此过程使用与主站点的版本匹配的安装源文件。 有关详细信息，请参阅[扩展独立主站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand)。

### <a name="install-a-secondary-site"></a>安装辅助站点
<!-- SCCMDocs-pr issue #3164 -->
若要在安装了一个或多个控制台中更新的主站点下安装新的辅助站点，请使用主站点中 CD.Latest 文件夹内的源文件。 

有关详细信息，请参阅[安装辅助站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary)。 


## <a name="unsupported-scenarios"></a>不支持的方案

对于以下各项不支持更新后的 CD.Latest 源文件：  
   
- 为新层次结构安装新站点  
- 将 Microsoft System Center 2012 Configuration Manager 站点升级到 System Center Configuration Manager Current Branch
- 安装 Configuration Manager 客户端
- 安装 Configuration Manager 控制台

