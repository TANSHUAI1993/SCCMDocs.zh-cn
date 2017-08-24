---
title: "安全基础知识 | Microsoft Docs"
description: "了解有关 System Center Configuration Manager 的安全性层的信息。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: df3198885259b1db4a1aadee0db6512a1a2d4911
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>System Center Configuration Manager 安全性的基础知识

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 的安全性包括若干层。 第一层是由 Windows 安全功能为操作系统和网络提供的，它包括以下内容：  

-   用于在 Configuration Manager 组件之间传输文件的文件共享。  

-   帮助保护文件和注册表项的访问控制列表 (ACL)。  

-   帮助保护通信的 Internet 协议安全性 (IPsec)。  

-   用于设置安全策略的组策略。  

-   用于分布式应用程序的分布式组件对象模型 (DCOM) 权限，例如 Configuration Manager 控制台。  

-   用于存储安全主体的 Active Directory 域服务。  

-   Windows 帐户安全，包括在 Configuration Manager 安装过程中创建的一些组。  

而附加的安全组件（如防火墙和入侵检测）帮助为整个环境提供防御。 由行业标准的公钥基础结构 (PKI) 实现所颁发的证书帮助提供身份验证、签名和加密。  

除了 Windows 服务器和网络基础设施提供的安全性之外，Configuration Manager 以几种方式控制对 Configuration Manager 控制台及其资源的访问权限。 默认情况下，只有本地管理员才有权访问在安装了 Configuration Manager 控制台的计算机上运行此控制台所需的文件和注册表项。  

下一个安全层建立在通过 Windows Management Instrumentation (WMI)（具体指 SMS 提供程序）进行的访问的基础上。 SMS 提供程序是一种 Configuration Manager 组件，它授予用户访问权限以查询站点数据库中的信息。 默认情况下，只有本地 SMS 管理员组的成员才能访问该提供程序。 此组最初仅包含安装了 Configuration Manager 的用户。 若要向其他帐户授予对通用信息模型 (CIM) 存储库和 SMS 提供程序的权限，请将这些帐户添加到 SMS 管理员组中。  

最后一个安全层基于与站点数据库中的对象有关的权限。 默认情况下，本地系统帐户和用于安装 Configuration Manager 的用户帐户可以管理站点数据库中的所有对象。 可以在 Configuration Manager 控制台中使用基于角色的管理向其他管理用户授予权限和限制其权限。  



## <a name="role-based-administration"></a>基于角色的管理  
 Configuration Manager 使用基于角色的管理来帮助保护对象（如集合、部署和站点）。 此管理模式为所有站点和站点设置集中定义及管理层次结构范围的安全访问设置。 安全角色将分配给管理用户和组权限。 权限将连接到不同的 Configuration Manager 对象类型，如用于创建或更改客户端设置的权限。 管理用户负责管理且特定于安全作用域组的实例对象，如安装 Microsoft Office 的应用程序。 安全角色、安全作用域和集合的组合定义管理用户可以查看和管理的对象。 Configuration Manager 为典型的管理任务安装某些默认安全角色。 但是，可以创建自己的安全角色来满足特定业务需求。  

 有关详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。  

## <a name="securing-client-endpoints"></a>保护客户端终结点  
 通过使用自签名证书或者 PKI 证书，可以保护客户端与站点系统角色的通信。 对于 Configuration Manager 检测到在 Internet 上的客户端计算机和移动设备客户端，将需要使用 PKI 证书。 PKI 证书使用 HTTPS 保护客户端终结点。 可以将客户端连接到的站点系统角色配置为进行 HTTPS 或 HTTP 客户端通信。 客户端计算机始终使用可用的最安全方法进行通信。 客户端计算机仅在具有允许 HTTP 通信的站点系统角色时才会回退到在 Intranet 上使用最不安全的 HTTP 通信方法。  

 有关详细信息，请参阅 [System Center Configuration Manager 的加密控件技术参考](../../protect/deploy-use/cryptographic-controls-technical-reference.md)。  

## <a name="configuration-manager-accounts-and-groups"></a>Configuration Manager 帐户和组  
 Configuration Manager 使用本地系统帐户来执行大部分站点操作。 某些管理任务可能需要创建和维护其他帐户。 在安装过程中，会创建几个默认的组和 SQL Server 角色。 可能要手动将计算机或用户帐户添加到默认的组和 SQL Server 角色中。  

 有关详细信息，请参阅 [System Center Configuration Manager 中使用的帐户](../../core/plan-design/hierarchy/accounts.md)。  

## <a name="privacy"></a>隐私  
 尽管企业管理产品因其可以有效地管理大量客户端而提供了许多优点，你仍必须注意此软件将可能如何影响组织中用户的隐私。 System Center Configuration Manager 包括很多用于收集数据和监视设备的工具。 一些工具可能存在隐私方面的隐患。  

 例如，在安装 Configuration Manager 客户端时，默认情况下会启用许多管理设置。 这会导致客户端软件向 Configuration Manager 站点发送信息。 客户端信息存储在 Configuration Manager 数据库中，不会将该信息发送给 Microsoft。 实施 System Center Configuration Manager 前，请考虑隐私要求。  
