---
title: "远程控制 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中的远程控制简介。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29350919-6a25-446b-a0da-05e8914fbb26
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 00c9e6bff02d534af2be975e0d5d41bcf0e7cb1c


---
# <a name="introduction-to-remote-control-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的远程控制简介

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的远程控制可远程管理、提供协助或查看层次结构中的任何客户端计算机。 可以使用远程控制来解决客户端计算机上的硬件和软件配置问题，并在需要访问用户计算机时提供支持人员支持。 Configuration Manager 支持对工作组计算机以及加入 Active Directory 域的计算机的远程控制。  

 此外，Configuration Manager 允许用户通过配置客户端设置，从 Configuration Manager 控制台运行 Windows 远程桌面和远程协助。  

> [!NOTE]  
>  在以下情况下，无法建立从 Configuration Manager 控制台到客户端计算机的远程协助会话：  
>   
>  -   客户端计算机处于工作组中。  
> -   运行 Configuration Manager 控制台的计算机在运行 Windows XP Service Pack 3，但主计算机未运行 Windows XP Service Pack 3。 有关详细信息，请参阅 Windows 远程协助文档。  

 可以从 Windows 命令提示符窗口或从 Windows“开始”菜单，从 Configuration Manager 控制台中的任何设备集合启动远程控制会话。  



<!--HONumber=Dec16_HO3-->


