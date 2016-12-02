---
title: "安全基础知识 | System Center Configuration Manager"
description: "了解有关 System Center Configuration Manager 的安全性层的信息。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb84efcaac281aa8c9338cd69ce32054ea775de3


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>System Center Configuration Manager 安全性的基础知识

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 的安全性包括若干层。 第一层是由 Windows 安全功能为操作系统和网络提供的，它包括以下内容：  

-   用于在 Configuration Manager 组件之间传输文件的文件共享  

-   帮助保护文件和注册表项的访问控制列表 (ACL)  

-   用于保护通信的 IPsec  

-   用于设置安全策略的组策略  

-   用于分布式应用程序的 DCOM 权限，例如 Configuration Manager 控制台  

-   用于存储安全主体的 Active Directory 域服务  

-   Windows 帐户安全，包括在 Configuration Manager 安装过程中创建的一些组  

而附加的安全组件（例如防火墙和入侵检测）帮助为整个环境提供深层防御。 由行业标准的 PKI 实现所颁发的证书帮助提供身份验证、签名和加密。  

除了 Windows 服务器和网络基础设施提供的安全性之外，Configuration Manager 以几种方式控制对 Configuration Manager 控制台及其资源的访问权限。 默认情况下，只有本地管理员才有权访问在安装了 Configuration Manager 控制台的计算机上运行此控制台所需的文件和注册表项。  

下一个安全层建立在通过 Windows Management Instrumentation (WMI)（具体指 **SMS 提供程序**）进行的访问的基础上。 SMS 提供程序是一种 Configuration Manager 组件，它授予用户访问权限以查询站点数据库中的信息。 默认情况下，只有本地 **SMS 管理员** 组的成员才能访问该提供程序。 此组最初仅包含安装了 Configuration Manager 的用户。 若要向其他帐户授予对通用信息模型 (CIM) 存储库和 SMS 提供程序的权限，请将这些帐户添加到 SMS 管理员组中。  

最后一个安全层基于与站点数据库中的对象有关的权限。 默认情况下，本地系统帐户和用于安装 Configuration Manager 的用户帐户可以管理站点数据库中的所有对象。 可以在 Configuration Manager 控制台中使用**基于角色的管理**向其他管理用户授予权限和限制其权限。  

本主题的其余部分讨论与 Configuration Manager 相关的安全性方面的内容。  

## <a name="role-based-administration"></a>基于角色的管理  
 Configuration Manager 使用基于角色的管理来帮助保护对象（例如集合、部署和站点）。 此管理模式为所有站点和站点设置集中定义及管理层次结构范围的安全访问设置。 会向管理用户分配安全角色，并向不同的 Configuration Manager 对象类型分配组权限，例如创建或更改客户端设置的权限。 管理用户负责管理且特定于安全作用域组的实例对象，例如安装 Microsoft Office 的应用程序。 安全角色、安全作用域和集合的组合定义管理用户可以查看和管理的对象。 Configuration Manager 为典型的管理任务安装某些默认安全角色。 但是，可以创建自己的安全角色，以满足你的特定业务需求。  

 有关详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)  

## <a name="securing-client-endpoints"></a>保护客户端终结点  
 通过使用自签名证书或者公钥基础结构 (PKI) 证书，可以保护客户端与站点系统角色的通信。 Configuration Manager 检测到位于 Internet 上的计算机客户端和移动设备客户端必须使用 PKI 证书，以便可以使用 HTTPS 来保护客户端终结点。 可以将客户端连接到的站点系统角色配置为进行 HTTPS 或 HTTP 客户端通信。 客户端计算机始终会使用可用的最安全方法进行通信，而且仅在具有允许 HTTP 通信的站点系统角色时才会回退到在 Intranet 上使用最不安全的 HTTP 通信方法。  

 有关详细信息，请参阅 [System Center Configuration Manager 的加密控件技术参考](../../protect/deploy-use/cryptographic-controls-technical-reference.md)  

## <a name="configuration-manager-accounts-and-groups"></a>Configuration Manager 帐户和组  
 Configuration Manager 使用**本地系统**帐户来执行大部分站点操作。 但是，某些管理任务可能需要创建和维护其他帐户。 在安装过程中，会创建几个默认的组和 SQL Server 角色。 但是，你可能要手动将计算机或用户帐户添加到这些默认的组和角色中。  

 有关详细信息，请参阅 [System Center Configuration Manager 中使用的帐户](../../core/plan-design/hierarchy/accounts.md)。  

## <a name="privacy"></a>隐私  
 尽管企业管理产品因其可以有效地管理大量客户端而提供了许多优点，你仍必须注意此软件将可能如何影响组织中用户的隐私。 System Center Configuration Manager 包括很多用于收集数据和监视设备的工具，其中一些工具可能存在隐私方面的隐患。  

 例如，在安装 Configuration Manager 客户端时，默认情况下会启用许多管理设置。 这会导致客户端软件向 Configuration Manager 站点发送信息。 客户端信息存储在 Configuration Manager 数据库中，不会将该信息发送给 Microsoft。 实施 System Center Configuration Manager 前，请考虑隐私要求。  



<!--HONumber=Nov16_HO1-->


