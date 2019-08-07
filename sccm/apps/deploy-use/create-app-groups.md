---
title: 创建应用程序组
titleSuffix: Configuration Manager
description: 创建一组可以在 Configuration Manager 中作为单个部署发送到用户或设备集合的应用程序。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2698105d125abbbf1354cb045753586899e003ba
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537655"
---
# <a name="create-application-groups"></a>创建应用程序组

<!--3555907-->

从版本 1906 开始，创建一组可以作为单个部署发送到用户或设备集合的应用程序。 指定的有关应用组的元数据在软件中心中显示为单个实体。 可以在组中对应用排序，以便客户端将其以特定顺序安装。

> [!Note]  
> 在该 Configuration Manager 版本中，应用组是预发形功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区  。 展开“应用程序管理”，然后选择“应用程序组”节点   。  

1. 在功能区中的 "创建" 组中, 选择 "**创建应用程序组**"。

1. 在“常规信息”页上，指定有关应用组的信息  。  

1. 在“软件中心”页上，包含软件中心中显示的信息  。  

1. 在“应用程序组”页上，选择“添加”   。 为此组选择一个或多个应用。 使用“上移”和“下移”操作对其重新排序   。  

1. 完成向导。  

使用与部署应用程序相同的过程部署应用组。 有关详细信息，请参阅[部署应用程序](/sccm/apps/deploy-use/deploy-applications)。

如果在部署组后将新应用添加到组, 则必须将新应用内容单独分发到分发点。

若要对应用组部署进行故障排除, 请在客户端上使用以下日志文件:

- **AppGroupHandler**
- **AppEnforce.log**
- **SettingsAgent**

> [!Important]  
> 在将整个层次结构和目标客户端更新为至少1906版之前, 请勿创建或部署应用组。

### <a name="known-issues"></a>已知问题

- 组中的应用只能包含**Windows Installer**或**脚本**部署类型。 将 "部署类型" 安装行为设置为 "**针对系统安装**"。
- 只能将应用组部署到设备集合。
