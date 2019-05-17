---
title: 电子邮件配置文件的先决条件
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager 中的电子邮件配置文件及其在产品外部和内部的依赖关系。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0e682d96b772dfb1bfd6be8947781fc0a002018
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493877"
---
# <a name="email-profile-prerequisites"></a>电子邮件配置文件先决条件

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的电子邮件配置文件在产品外部与内部均有依赖关系。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|必须授予特定的安全权限来管理电子邮件配置文件|你必须具有以下安全权限才能管理公司资源访问设置，例如电子邮件配置文件：<br /><br /> - 若要查看和管理电子邮件配置文件的警报和报表：需要对“警报”对象的“创建”、“删除”、“修改”、“修改报表”、“读取”和“运行报表”权限。<br /><br /> - 若要创建和管理证书配置文件：需要对“证书配置文件”对象的“创作策略”、“修改报表”、“读取”和“运行报表”权限。<br /><br /> - 若要管理电子邮件配置文件部署：需要对“集合”对象的“部署配置策略”、“修改客户端状态警报”、“读取”和“读取资源”权限。<br /><br /> - 若要管理所有配置策略：需要对“配置策略”对象的“创建”、“删除”、“修改”、“读取”和“设置安全作用域”权限。<br /><br /> - 若要运行与电子邮件配置文件相关的查询：需要对“查询”对象的“读取”权限。<br /><br /> - 若要在 System Center Configuration Manager 控制台中查看电子邮件配置文件信息：需要对“站点”对象的“读取”权限。<br /><br /> - 若要查看电子邮件配置文件的状态消息：需要对“状态消息”对象的“读取”权限 。<br /><br /> - 若要创建和管理电子邮件配置文件：需要对“通信设置配置文件”对象的“创作策略”、“修改报表”、“读取”和“运行报表”权限。<br /><br /> **公司资源访问管理器**安全角色包括在 System Center Configuration Manager 中管理电子邮件配置文件所需的这些权限。 有关详细信息，请参阅[在 System Center Configuration Manager 中配置安全性](../../core/plan-design/security/configure-security.md)。|  
|Active directory 中的邮件属性|如果要使用用户的主 SMTP 地址生成电子邮件配置文件中的用户电子邮件地址，则必须配置 System Center Configuration Manager 用户发现以从 Active Directory 中发现“邮件”属性（此为默认配置）。|  

## <a name="external-dependencies"></a>外部依赖关系  

|依赖关系|更多信息|  
|----------------|----------------------|  
|Active directory 中的邮件属性|如果想要通过使用用户的主 SMTP 地址生成电子邮件配置文件中的用户电子邮件地址，则此地址必须存在于 Active Directory 的“邮件”属性中。<br /><br /> 有关详细信息，请参阅 Windows Server 文档。|
