---
title: "配置 Endpoint Protection | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中管理客户端计算机上的安全和恶意软件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 3678fd1e2ba70ad1cc03a3e0ca294901fae96255


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中配置 Endpoint Protection

*适用范围：System Center Configuration Manager (Current Branch)*

使用 Endpoint Protection 管理 Configuration Manager 客户端计算机上的安全和恶意软件之前，请先使用本主题进行设置。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>如何在 Configuration Manager 中配置 Endpoint Protection  
 Configuration Manager 中的 Endpoint Protection 具有产品内部和外部依赖关系。  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中配置 Endpoint Protection  
配置 Endpoint Protection 需要五个步骤

|步骤|详细信息|
|---|----|
|步骤 1|[创建 Endpoint Protection 点站点系统角色](endpoint-protection-site-role.md) - 安装 Endpoint Protection 点站点系统角色 |
|步骤 2|[为 Endpoint Protection 配置警报](endpoint-configure-alerts.md) - 配置 Endpoint Protection 警报以便在层次结构中发生特定安全事件时通知管理员|
|步骤 3 | [为 Endpoint Protection 客户端配置定义更新源](endpoint-definition-updates.md) - 从可用的方法中进行选择，以使客户端计算机上的反恶意软件定义保持最新|
|步骤 4|[配置默认反恶意软件政策并创建自定义反恶意软件政策](endpoint-antimalware-policies.md) - 安装 Endpoint Protection 客户端时会应用默认反恶意软件政策；在部署客户端 60 分钟内会应用自定义策略|
|步骤 5|[为 Endpoint Protection 配置自定义客户端设置](endpoint-protection-configure-client.md) - 为 Endpoint Protection 配置自定义客户端设置以便部署到计算机集合|

> [!IMPORTANT]  
>  如果管理 Windows 10 计算机的 Endpoint Protection，则必须配置 Configuration Manager 以更新和分发 Windows Defender 的恶意软件定义。 虽然 Windows 10 中包含了 Windows Defender，但仍然必须安装 SCEPInstall，并且仍然需要 Endpoint Protection 的自定义客户端设置（步骤 5）。  



<!--HONumber=Dec16_HO3-->


