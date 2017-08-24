---
title: "虚拟桌面基础结构 (VDI) 客户端管理 | Microsoft Docs "
description: "在虚拟桌面基础结构 (VDI) 中管理 System Center Configuration Manager 客户端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d73daf6427b8c58d21d579f3b41df513cc3e3b0b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>关于在虚拟桌面基础结构 (VDI) 中管理 System Center Configuration Manager 客户端的注意事项

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 支持在以下虚拟桌面基础结构 (VDI) 方案中安装 Configuration Manager 客户端：  

-   **个人虚拟机** - 若要确保在会话之间在虚拟机上维护用户数据和设置时，通常使用个人虚拟机。  

-   **远程桌面服务会话** - 远程桌面服务使服务器能够承载多个并发客户端会话。 用户可以连接到会话，然后在该服务器上运行应用程序。  

-   **共用的虚拟机** - 在会话之间不保留共用的虚拟机。 当关闭会话时，将丢弃所有数据和设置。 当无法使用远程桌面服务时（因为所需的业务应用程序无法在承载客户端会话的 Windows Server 上运行），共用的虚拟机很有用。  

 下表列出了关于在虚拟桌面基础结构中管理 Configuration Manager 客户端的考虑事项。  

|虚拟机类型|注意事项|  
|--------------------------|--------------------|  
|个人虚拟机|Configuration Manager 将个人虚拟机同等地视为物理计算机。 可以在虚拟机映像上预先安装 Configuration Manager 客户端，或者在预配虚拟机之后部署该客户端。|  
|远程桌面服务|不会为单个远程桌面会话安装 Configuration Manager 客户端。 而是在远程桌面服务服务器上仅一次性地安装客户端。 在远程桌面服务服务器上可以使用所有的 Configuration Manager 功能。|  
|共用的虚拟机|当共用的虚拟机被解除授权时，使用 Configuration Manager 所做的任何更改都会丢失。<br /><br /> Configuration Manager 功能（如硬件清单、软件清单和软件计数）返回的数据可能与用户的需求无关，因为虚拟机可能仅运行很短一段时间。 请考虑从清单任务中排除共用的虚拟机。|  

 因为虚拟化支持在同一物理计算机上运行多个 Configuration Manager 客户端，所以对于计划操作（如硬件和软件清单、反恶意软件扫描、软件安装和软件更新扫描），许多客户端操作都具有内置的随机化延迟。 对于具有运行 Configuration Manager 客户端的多个虚拟机的计算机，此延迟有助于分发 CPU 处理以及数据传输。  

> [!NOTE]  
>  除了处于维护模式的 Windows Embedded 客户端之外，未在虚拟化环境中运行的 Configuration Manager 客户端也使用此随机化延迟。 如果具有许多部署的客户端，则此行为有助于避免网络带宽高峰，并且可以在 Configuration Manager 站点系统（如管理点和站点服务器）上减少 CPU 处理要求。 延迟间隔因 Configuration Manager 功能而异。  
>   
>  默认情况下，使用以下客户端设置为所需软件更新和所需应用程序部署禁用了随机延迟：“计算机代理” ：“禁用截止时间随机性” 
