---
title: "代理服务器支持 | Microsoft Docs"
description: "了解 System Center Configuration Manager 支持的站点系统服务器和客户端使用的代理服务器。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dc36be47310d2c2178c974a2b503d0b5f9f6e2ec
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的代理服务器支持

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 站点系统服务器和客户端都可使用代理服务器。  

## <a name="site-system-servers"></a>站点系统服务器  
当站点系统角色需要连接到 Internet 时，可对其进行配置，以使用代理服务器。  

-   托管站点系统服务器的计算机支持由同一计算机上的所有站点系统角色共享的单一代理服务器配置。 如果需要不同角色或角色实例的单独的代理服务器，必须将这些角色放在单独的站点系统服务器上。  

-   在为已有代理服务器配置的站点系统服务器配置新的代理服务器设置时，将覆盖原始配置。  

-   使用托管站点系统角色的计算机的**系统**帐户连接到代理。  

以下站点系统角色均可连接到 Internet，并且可能需要代理服务器。  有一个例外，站点系统角色可以使用代理进行此操作而无需进行其他配置。 此例外是软件更新点。 以下列表包含有关软件更新点需要的其他配置信息：  

**资产智能同步点**：此站点系统角色连接到 Microsoft，并在托管资产智能同步点的计算机上使用代理服务器配置。  

**基于云的分发点**：若要为基于云的分发点设置代理服务器，可以在管理基于云的分发点的主站点上设置代理。  

对于此配置，主站点服务器：  

-   必须能够连接到 Microsoft Azure 以设置、监视并将内容分发到分发点。  

-   使用该计算机系统帐户来建立连接。  

-   使用该计算机默认 Web 浏览器。  

无法在 Microsoft Azure 中基于云的分发点上设置代理服务器。  

**云连接点**：此站点系统角色连接到 Configuration Manager 云服务以下载 Configuration Manager 的版本更新，并且使用在托管服务连接点的计算机上配置的代理服务器。  

**Exchange Server 连接器**：此站点系统角色连接到 Exchange Server，并在托管 Exchange Server 连接器的计算机上使用代理服务器配置。  

**服务连接点**：此站点系统角色连接到 Microsoft Intune，并使用在托管服务连接点的计算机上配置的代理服务器。  

**软件更新点** - 此站点系统角色在连接到 Microsoft 更新来下载修补程序和同步有关更新的信息时可以使用代理。 在设置软件更新点过程中，如果启用该选项，软件更新点仅针对以下选项使用代理：  

-   **同步软件更新时使用代理服务器**  

-   **通过使用自动部署规则在下载内容时使用代理服务器**（当此设置可用时，软件更新点不在辅助站点上使用它。）  

在“添加站点系统角色”向导的“活动软件更新点”页上或在“软件更新点组件属性”中的“常规”选项卡上配置代理服务器。  

-   代理服务器设置都仅与该站点上的软件更新点相关联。  

-   只有已为托管软件更新点的站点系统服务器设置代理服务器时，代理服务器选项才可用。  

> [!NOTE]  
>  默认情况下，当自动部署规则运行时，将使用在其上创建自动部署规则的服务器的**系统**帐户连接到 Internet 并下载软件更新。  
>   
>  此帐户无法访问 Internet 时，将无法下载软件更新并且 ruleengine.log 会记录以下条目：**无法从 Internet 下载更新。错误 = 12007。**  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>设置站点系统服务器的代理服务器  

1.  在 Configuration Manager 控制台中，选择“管理”，展开“站点配置”，然后选择“服务器和站点系统角色”。  

2.  选择要编辑的站点系统服务器，然后在“详细信息”窗格中，右键单击“站点系统”，然后选择“属性”。  

3.  在“站点系统属性”中，选择“代理”选项卡，然后设置此主站点服务器的代理设置。  

4.  选择“确定”以保存新的代理服务器配置。  
