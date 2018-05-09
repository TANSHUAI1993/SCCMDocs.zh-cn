---
title: 服务时段
titleSuffix: Configuration Manager
description: 使用服务时段控制 System Center Configuration Manager 站点安装更新的时间。
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 8b81efc7f31339bd7b19530ef603855f0ee8fad6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
#  <a name="service-windows-for-site-servers"></a>站点服务器的服务时段

*适用范围：System Center Configuration Manager (Current Branch)*

可以在中心管理站点和主站点配置服务时段，控制控制台中更新可以安装的时间。  可配置多个时段，时段允许用于安装更新，更新由该站点服务器的所有服务时段的组合决定。

如果未配置任何服务时段：
- **在顶层站点**（中心管理站点或独立主站点）上，选择启动更新安装的时间。
- 中心管理站点的更新完成安装后，**子主站点上**的更新将自动安装。
- **在辅助站点上**，永远不会自动启动更新。 但是，在父主站点完成更新安装后，必须从控制台中手动启动更新安装。

如果已配置服务时段：
- **在顶层站点上**，将无法从 Configuration Manager 控制台中启动任何新更新的安装。 即使配置了服务时段，站点也会自动下载更新，以便准备安装。  
- **在子主站点上**，已在中心管理站点安装的更新将下载到主站点，但不会自动启动。 在使用服务时段阻止期间，不能手动启动更新安装。 服务时段不再阻止更新安装时，更新安装将自动启动。
- **辅助站点**不支持服务时段，并且不会自动安装更新。 辅助站点的主父站点安装更新后，可从控制台中启动辅助站点的更新。

## <a name="to-configure-a-service-window"></a>配置服务时段

1.  在 Configuration Manager 控制台中，打开“管理” > “站点配置” > “站点”，然后选择要在其中配置服务时段的站点服务器。  

2.  接下来，编辑站点服务器“属性”，然后选择“服务时段”选项卡，此时你可以在其中为该站点服务器设置一个或多个服务时段。  
