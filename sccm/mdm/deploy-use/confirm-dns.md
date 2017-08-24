---
title: "使用 System Center Configuration Manager 确认域名要求 | Microsoft Docs"
description: "使用 System Center Configuration Manager 确认域名要求。"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: "18"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 35b24294073956a6bdb14cae07705f56d31e00a9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 确认域名要求

*适用范围：System Center Configuration Manager (Current Branch)*

如有必要，请执行以下步骤以满足 Configuration Manager 外部的任何依赖关系：

1. 每个用户必须分配有 Intune 许可证才能注册设备。 若要将 Intune 许可证关联到用户，每个用户必须具有可公开解析的用户主体名称 (UPN)（例如，johndoe@contoso.com）或是在 Azure Active Directory 中配置的备用登录 ID。 配置备用登录 ID 使用户可以使用电子邮件地址登录，即使其 UPN 是 NetBIOS 格式（例如 CONTOSO\johndoe）。

  - 如果公司使用公开解析的 UPN（例如 johndoe@contoso.com），则无需进一步配置。
  - 如果公司使用不可解析的 UPN（例如 CONTOSO\johndoe），则你必须[在 Azure Active Directory 中配置备用 ID](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)。

2.  部署并配置 Active Directory 联合身份验证服务 (AD FS)。 （可选）

     在设置单一登录时，用户可以使用其公司凭据登录，以访问 Intune 中的服务。

     有关详细信息，请参阅下列主题：
    -   [为单一登录做准备](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [规划和部署 AD FS 2.0 以用于单一登录](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  部署并配置目录同步。

     目录同步可让你利用同步的用户帐户来填充 Intune。 同步的用户帐户和安全组被添加到 Intune 中。 未能启用目录同步是在使用 Microsoft Intune 设置 Configuration Manager MDM 时，设备无法注册的一个常见原因。

     有关详细信息，请参阅 Active Directory 文档库中的 [目录集成](http://go.microsoft.com/fwlink/?LinkID=271120) 。

4.  可选但不建议：如果没有使用 Active Directory 联合身份验证服务，则重置用户的 Microsoft Online 密码。

     如果没有使用 AD FS，则必须为每个用户设置 Microsoft Online 密码。

> [!div class="button"]
[< 上一步](create-mdm-collection.md)  [下一步 >](configure-intune-subscription.md)
