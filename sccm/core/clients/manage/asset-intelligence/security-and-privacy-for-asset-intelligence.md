---
title: "资产智能安全和隐私 | Microsoft Docs"
description: "获取 System Center Configuration Manager 中资产智能的安全和隐私信息。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b12054cce52e2b83715a083d78a62e06b5127a2f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 中资产智能的安全和隐私

*适用范围：System Center Configuration Manager (Current Branch)*

本主题包括有关 System Center Configuration Manager 中资产智能的安全和隐私的信息。  

##  <a name="BKMK_Security_AI"></a> 资产智能安全最佳方案  
 在使用资产智能时，请使用以下安全最佳方案。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|导入许可证文件（Microsoft 批量许可文件或常规许可声明文件）时，请确保文件和通信通道的安全。|在导入过程中，使用 NTFS 文件系统权限来确保只有经授权的用户可以访问许可证文件，并在将数据传输到站点服务器时使用服务器消息块 (SMB) 签名来确保其完整性。|  
|使用最低权限的原则导入许可证文件。|使用基于角色的管理来向导入许可证文件的管理用户授予管理资产智能权限。 资产管理员的内置角色包括此权限。|  

##  <a name="BKMK_Privacy_HardwareInventory"></a> 资产智能的隐私信息  
 资产智能扩展 Configuration Manager 的清单功能，帮助提供更高级别的企业资产可见性。 不会自动启用资产智能信息收集。 你可以通过启用硬件清单报表类来修改所收集信息的类型。 有关详细信息，请参阅[配置 System Center Configuration Manager 中的资产智能](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md)。  

 资产智能信息按照与清单信息相同的方式存储在 Configuration Manager 数据库中。 当客户端使用 HTTPS 连接到管理点时，在传输到管理点的过程中始终加密数据。 当客户端使用 HTTP 连接时，可以配置对清单数据传输进行签名和加密。 清单数据不会以加密格式存储在数据库中。 信息将保留在数据库中，直到被每 90 天一次的站点维护任务“删除过期的清单历史记录”  删除。 可以配置删除间隔。  

 资产智能不会向 Microsoft 发送关于用户和计算机或许可证使用的信息。 你可以选择发送 System Center Online 分类请求，这意味着你可以标记一个或多个未分类的软件标题，将它们发送给 System Center Online 进行研究和分类。 在上载软件标题后，Microsoft 研究人员会进行识别、分类，然后将此信息提供给使用在线服务的所有客户。 您应该注意下列有关向 System Center Online 提交信息的隐私隐患：  

-   上载只适用于您可以选择向 System Center Online 发送的一般软件标题信息（名称、发布者等）。 清单信息不通过上载发送。  

-   上载决不会自动发生，系统并不打算自动进行此任务。 你必须手动选择并批准上载每个软件标题。  

-   在上载过程开始之前，将会出现一个对话框，向你显示将上载的确切数据。  

-   许可证信息不会发送到 Microsoft。 许可证信息存储在 Configuration Manager 数据库的一个独立区域，不能将其发送给 Microsoft。  

-   上载的任何软件标题都会变为公用，表现为指定的应用程序及其分类的信息将成为 System Center Online 资产智能目录的一部分，之后会下载到该目录的其他用户。  

-   软件标题的来源不会记录在资产智能目录中，也不会提供给其他客户。 但是，你仍必须验证以确保没有加载包含任何隐私信息的任何应用程序标题。  

-   无法取消上载的数据。  

 在配置资产智能数据收集以及确定是否将信息提交给 System Center Online 之前，请考虑组织的隐私要求。  
