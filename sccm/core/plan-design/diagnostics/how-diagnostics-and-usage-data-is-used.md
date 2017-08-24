---
title: "诊断数据的使用 | Microsoft Docs"
description: "了解 Microsoft 如何使用 System Center Configuration Manager 收集的诊断和使用情况数据。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9864f6ba7b9a2211c99b1a5d9ebd582e01ccfeb6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>如何将诊断和使用情况数据用于 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 收集的诊断和使用数据为 Microsoft 提供有关产品使用情况的近乎即时的反馈，并可用于调整将来的更新。 我们也能查看配置数据，这些数据可帮助我们设计并测试生产中的配置。 例如：  

-   站点服务器使用的 Windows Server 版本  

-   已安装的语言包  

-   SQL 架构针对产品默认值的增量  

此数据帮助工程团队计划将来的测试，以确保在最常见的配置下获得最佳体验。 由于将以更快频率发布 Configuration Manager 更新（以便更好地支持 Windows 10 和 Microsoft Intune 等快速发展的技术），因此，此数据对于快速调整和适应至关重要。  

同样重要的一点是，了解诊断和使用数据不适用于哪些方面。 Microsoft 不会将此数据用于以下方面：  

-   许可审核，例如按照许可协议比较客户使用情况  

-   不支持的产品的审核  

-   基于功能使用情况或地理位置（时区）等可用数据进行广告宣传  

##  <a name="bkmk_improve"></a> 诊断和使用数据如何改进产品的示例  
Microsoft 使用可用数据来改进产品。 以下是几个示例：  

-   **修订了对较旧服务器操作系统的支持：**  

     System Center Configuration Manager Current Branch 提供的初始支持对 Windows Server 2008 R2 的支持时间线加以限制。 检查已升级到 Configuration Manager Current Branch 的客户的使用数据之后，我们发现需要修订和扩展此时间线，以支持仍使用此服务器操作系统托管站点服务器和站点系统角色的客户。  

-   **改进了先决条件检查：**  

     基于使用数据，我们改进了先决条件检查以便安装更新，从而删除过时的规则、负责处理其他情况以及在某些情况下自动修正某些问题。  
