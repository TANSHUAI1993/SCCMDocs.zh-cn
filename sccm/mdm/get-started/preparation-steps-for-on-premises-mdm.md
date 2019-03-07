---
title: 准备本地 MDM
titleSuffix: Configuration Manager
description: 准备使用 Configuration Manager 中的本地移动设备管理来管理设备
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fad5ce96b84b5a6edfafdead64cff0223009ebf8
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558042"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>用于本地 MDM Configuration Manager 中的准备步骤

适用范围：System Center Configuration Manager (Current Branch)

若要使用 Configuration Manager 本地移动设备管理 (MDM) 管理设备，先设置必要的基础结构。 所需的站点系统角色需要跨整个受信任通道与移动设备通信。 这些角色包括注册代理点、 注册点、 设备管理点和分发点。

为本地 MDM 准备 Configuration Manager 所需的以下高级任务：  

- [为本地 MDM 设置 Microsoft Intune 订阅](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    注册 Microsoft Intune，然后将订阅添加到 Configuration Manager 通过 Configuration Manager 控制台。 此步骤仅需用于许可授权的目的。 Intune 不用于管理设备或存储管理信息。 设备的所有协调和管理均由你组织的企业通过使用本地 Configuration Manager 基础结构实施。  

    > [!Note]  
    > 从版本 1810年，Intune 连接不再新的本地 MDM 部署所必需的。<!--3607730, fka 1359124--> 组织仍需要 Intune 许可证才能使用此功能。 当前不能从现有的本地 MDM 部署中删除 Intune 连接。 有关详细信息，请参阅 [Intune 支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。  

- [为本地 MDM 安装站点系统角色](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    安装和配置使用本地 Configuration Manager 基础结构管理设备所需的站点系统。 最小值，此功能需要注册代理点、 注册点、 设备管理点和分发点角色。  

- [设置本地 MDM 的受信任通信的证书](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    配置本地配置管理器基础结构，允许被管理的设备和承载所需的站点系统角色的服务器之间的受信任的通信 (HTTPS)。  

- [设置本地 MDM 的设备注册](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    权限授予用户注册的计算机和设备。 设备要允许 HTTPS 连接到的站点系统服务器上安装受信任的根证书。 这些设备通常不是已加入域的。  

