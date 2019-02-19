---
title: 站点失败影响
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站点中各种失败的影响。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eebd1aaf72cbd7932a919c0a8ffdef6d6af8389f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132010"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Configuration Manager 中站点失败的影响

适用范围：System Center Configuration Manager (Current Branch)

站点服务器和任何其他站点系统都可能失败，并导致丢失其通常提供的服务。 如果在同一个站点上安装了多个站点系统，而该计算机失败，则那些站点系统通常提供的所有服务不再可用。

部分规划过程应包括了解为组织提供的服务所受到的影响。 因为站点中的每个站点系统提供不同的功能，站点失败的影响也不尽相同，视失败站点系统的角色而定。 

使用[高可用性选项](/sccm/core/servers/deploy/configure/high-availability-options)可帮助缓解任何单一系统的故障。 此外，规划并实施[备份和恢复](/sccm/core/servers/manage/backup-and-recovery)策略，以减少服务不可用的时间。

以下部分描述了指定的站点系统不可操作时的影响：


### <a name="site-server"></a>站点服务器

- 无法进行站点管理。 无法将控制台连接到站点。  

- 在站点服务器恢复联机之前，管理点会收集并缓存客户端信息。  

- 用户可以运行现有部署，客户端可以从分发点下载内容。  


### <a name="site-database"></a>站点数据库

- 无法进行站点管理。  

- 如果 Configuration Manager 客户端已经有使用新策略的策略分配，并且管理点缓存了策略正文，则客户端可以发出策略正文请求并接收策略正文回复。 但是，该站点无法服务任何新的策略分配请求。  

- 客户端只有在已经收到策略并且关联的源文件已在客户端本地缓存的情况下才能运行部署。  


### <a name="management-point"></a>管理点

- 虽然可以创建新部署，但在管理点联机之前，客户端不会接受它们。  

- 客户端仍然收集清单、软件计数和状态信息。 它们在管理点可用之前，会在本地存储此数据。  

- 客户端只有在已经收到策略并且关联的源文件已在客户端本地缓存的情况下才能运行部署。  


### <a name="distribution-point"></a>分发点

- 仅当关联的源文件已在本地下载或在对等源上可用时，Configuration Manager 客户端才能运行部署。

