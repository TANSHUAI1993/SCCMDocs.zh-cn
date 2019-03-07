---
title: 设置 Intune 订阅
titleSuffix: Configuration Manager
description: 设置 Intune 订阅，以便跟踪授权在本地移动设备管理在 Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff4fcc67325645387aea1e57354321769a515ca
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558059"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>为本地 MDM 配置管理器中设置 Microsoft Intune 订阅

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 本地移动设备管理 (MDM) 需要 Microsoft Intune 订阅，以便跟踪授权。 Intune 服务不用于管理的设备或存储管理信息。 本地 MDM，为所有设备管理由 Configuration Manager 基础结构进行都处理。  

为本地 MDM 安装所需的站点系统角色之前，设置 Intune 订阅。 此操作最小化新安装的站点系统角色开始正常运行所需的时间。  

> [!Note]  
> 从版本 1810年，Intune 连接不再新的本地 MDM 部署所必需的。<!--3607730, fka 1359124--> 组织仍需要 Intune 许可证才能使用此功能。 当前不能从现有的本地 MDM 部署中删除 Intune 连接。 有关详细信息，请参阅 [Intune 支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。  



##  <a name="sign-up-for-microsoft-intune"></a>注册 Microsoft Intune  

Intune 需要以使本地 MDM 功能。 [注册](https://docs.microsoft.com/intune/free-trial-sign-up)试用或付费订阅。 然后转到下一步，将订阅添加到 Configuration Manager。  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>将 Intune 订阅添加到 Configuration Manager  

若要将订阅添加到 Configuration Manager，请根据需要添加的混合 MDM 与 Intune 订阅时执行的相同基本步骤。 阅读以下有关特定差异的说明，然后使用[配置 Microsoft Intune 订阅](/sccm/mdm/deploy-use/configure-intune-subscription)中的指示。  

> [!NOTE]
>  添加 Intune 订阅，请记住以下说明：  
> 
> - 添加 Microsoft Intune 订阅向导中指定的集合不用于在本地 MDM 用户权限委派。 它仅用于使用 Intune 管理移动设备。 但是，必须先指定一个集合，若要继续执行向导。  
> 
> - 在向导中指定的站点代码将忽略为本地 MDM 它使用在注册中指定的站点代码向用户授予权限以注册设备的配置文件。  
> 
> - 不要启用多重身份验证。 本地 MDM 中不支持  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>配置本地 MDM 的 Intune 订阅  

1. 在 Configuration Manager 控制台中，转到**Administration**工作区中，展开**云服务**，然后选择**Microsoft Intune 订阅**节点。 选择你的订阅，然后选择**属性**功能区中。   

    1. 在底部的本地移动设备管理部分**常规**页上，选择以下选项之一：

        - 如果您计划为只包含设备托管在本地，选择选项**只能管理本地设备**。  

            > [!NOTE]  
            > 如果启用此选项，你将配置 Intune 订阅以保留所有管理信息的本地。 没有设备管理数据复制到云。  

        - 如果你打算通过 Intune 和 Configuration Manager 本地管理的设备，不配置此选项。  

    选择**确定**关闭订阅属性。

2. 如果你打算管理 Windows 10 移动版设备，选择你的订阅在列表中，选择**配置平台**在功能区中，，然后选择**Windows Phone**。  

    1. 选择的选项**Windows Phone 8.1 和 Windows 10 移动版**，然后选择**确定**。  

3. 如果你打算管理 Windows 10 桌面计算机，选择你的订阅在列表中，选择**配置平台**在功能区中，，然后选择**Windows**。  

    1. 选择选项**启用 Windows 注册**，然后选择**确定**。  

