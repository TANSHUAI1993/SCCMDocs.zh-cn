---
title: Power Viewer 工具
titleSuffix: Configuration Manager
description: 使用 Power Viewer 工具在 Configuration Manager 客户端上查看电源管理功能的状态。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f9695decaf7af8d947d57443bd4b14032545b7d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133310"
---
# <a name="power-viewer-tool"></a>Power Viewer 工具

适用范围：System Center Configuration Manager (Current Branch)

Power Viewer 工具是一个 [Configuration Manager 工具](/sccm/core/support/tools)。 可用来在 Configuration Manager 客户端上查看电源管理功能的状态。

以管理员身份运行 PowerVwr.exe。 工具启动时，会在“电源配置”选项卡上显示本地计算机的电源功能和电源设置。 

查看远程计算机的电源管理数据：  

1. 转到“文件”菜单，然后单击“连接”。 

2. 输入“计算机”名称、“用户名”和“密码”（如有必要）。 

Power Viewer 中有三个选项卡：  

- **电源配置**：查看目标计算机的电源功能和电源设置。  

- **每日活动**：查看客户端的每日活动图表，其中包含以下信息：  

    - **计算机状态**：一天当中计算机的电源状态。 睡眠模式视为关机状态。  

    - **监视器状态**：一天当中监视器的打开或关闭状态。  

    - **用户活动**：一天当中用户活动的信息。  

- **电源事件**：查看每日所有电源事件。 客户端在零晨 12 点总结这些事件。 此摘要会生成每日活动图表的数据。  
