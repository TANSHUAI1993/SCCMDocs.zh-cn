---
title: "确保设备合规性 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理组织中设备的配置和合规性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ecfe550d2e28579ea873442b2a68dc1c7c5483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="ensure-device-compliance-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 确保设备的合规性

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的符合性设置提供了管理组织中设备的配置和符合性所需的工具与资源。 这可以帮助你支持以下业务要求：  

-   将你所管理的 Windows PC、Mac 计算机、服务器和移动设备的配置与你创建的或从其他供应商处获取的最佳方案配置进行比较  

-   确定未经授权的设备配置  

-   报告与法规策略和内部安全策略的符合性  

-   确定安全漏洞  

-   提供帮助桌面，帮助桌面中具有通过确定不符合配置来检测所报告事件和问题的可能原因的信息。  

-   自动修正移动设备上的某些非符合性设置  

-   通过将应用程序、包、程序或脚本部署到由报告其在符合性范围外的设备自动进行填充的集合，以修正符合性的问题  


## <a name="get-started"></a>入门  
 了解有关符合性设置的基本信息，以及你可以使用这些设置完成的任务。  

 [符合性设置入门](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>规划和设计  
 在开始使用符合性设置之前，请确保你已实现本主题中包含的必要先决条件。  

 [规划和配置符合性设置](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

## <a name="common-tasks"></a>常见任务  
 本部分中会列出一些常见方案，有助于用户了解如何在 Configuration Manager 中使用符合性设置。  

 [管理符合性的常见任务](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>远程连接配置文件  
 此配置项目类型允许将用户的 PC 配置为在未连接到域或者其个人计算机通过 Internet 连接时以远程方式连接到工作计算机。  

 [创建远程连接配置文件](/sccm/compliance/deploy-use/create-remote-connection-profiles)  

## <a name="user-data-and-profiles"></a>用户数据和配置文件  
 配置项目类型包含的设置可为层次结构中的用户管理运行 Windows 8 和更高版本的计算机上的文件夹重定向、脱机文件和漫游配置文件。  

 [创建用户数据和配置文件配置项目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)  

## <a name="windows-edition-upgrade-policy"></a>Windows 版本升级策略  
 版本升级策略允许你将 Windows 10 设备自动升级到新版本。 你可以指定升级 Windows 10 桌面版的产品密钥或可用于升级运行 Windows 10 移动版和 Windows 10 全息版的设备的许可证文件。  

 [使用版本升级策略升级 Windows 设备](/sccm/compliance/deploy-use/upgrade-windows-version)  
