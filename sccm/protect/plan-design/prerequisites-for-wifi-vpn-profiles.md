---
title: Wi-Fi 和 VPN 配置文件先决条件
titleSuffix: Configuration Manager
description: 了解管理 System Center Configuration Manager 中的证书配置文件、Wi-Fi 配置文件和 VPN 配置文件所需的安全权限。
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 894717df4b5acb7142aa7d171a8b8b63a28f8dc0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中 Wi-Fi 和 VPN 配置文件的先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的 Wi-Fi 和 VPN 配置文件仅在产品内有依赖关系。  

 你必须具有下列安全权限才能管理公司资源访问设置，例如证书配置文件、Wi-Fi 配置文件和 VPN 配置文件：  

-   若要查看和管理 Wi-Fi 配置文件的警报和报表：需要对“警报”对象的“创建”、“删除”、“修改”、“修改报表”、“读取”和“运行报表”权限。  

-   若要创建和管理证书配置文件：需要“证书配置文件” 对象的“创作策略” 、“修改报表” 、“读取”  和“运行报表”  权限。  

-   若要管理 Wi-Fi、证书和 VPN 配置文件部署：需要对“集合” 对象的“部署配置策略” 、“修改客户端状态警报” 、“读取”  和“读取资源”  。  

-   若要管理所有配置策略：需要对“配置策略” 对象的“创建” 、“删除” 、“修改” 、“读取”  和“设置安全作用域”  权限。  

-   若要运行与 Wi-Fi 和 VPN 配置文件相关的查询：需要对“查询”对象的“读取”权限。  

-   若要在 System Center Configuration Manager 控制台中查看 Wi-Fi 和 VPN 配置文件信息：需要对“站点”对象的“读取”权限。  

-   若要查看 Wi-Fi 和 VPN 配置文件的状态消息：需要对“状态消息”对象的“读取”权限。  

-   若要创建和修改受信任的 CA 证书配置文件：需要对“受信任的 CA 证书配置文件” 对象的“创作策略” 、“修改报表” 、“读取”  和“运行报表”  权限。  

-   若要创建和管理 VPN 配置文件：需要对“VPN 配置文件” 对象的“创作策略” 、“修改报表” 、“读取”  和“运行报表”  权限。  

-   若要创建和管理 Wi-Fi 配置文件：需要对“Wi-Fi 配置文件” 对象的“创作策略” 、“修改报表” 、“读取”  和“运行报表”  权限。  

 **公司资源访问管理器**安全角色包括在 System Center Configuration Manager 中管理 Wi-Fi 配置文件所需的这些权限。 有关详细信息，请参阅[在 System Center Configuration Manager 中配置安全性](../../core/plan-design/security/configure-security.md)。
