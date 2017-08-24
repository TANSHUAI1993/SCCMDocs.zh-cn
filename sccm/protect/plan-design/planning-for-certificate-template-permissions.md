---
title: "规划证书模板权限 | Microsoft Docs"
description: "了解如何规划配置 System Center Configuration Manager 使用的证书模板所需的权限。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 832be8c9fda727804f57e83768cd8799db722c67
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中规划证书配置文件的证书模板权限

*适用范围：System Center Configuration Manager (Current Branch)*


下列信息可帮助规划如何为 System Center Configuration Manager 在你部署证书配置文件时使用的证书模板配置权限。  

## <a name="default-security-permissions-and-considerations"></a>默认安全权限和注意事项  
 System Center Configuration Manager 将用于为用户和设备请求证书的证书模板所需的默认安全权限如下：  

-   “读取”和“注册”（针对网络设备注册服务应用程序池使用的帐户）  

-   “读取”（针对运行 System Center Configuration Manager 控制台的帐户）  

 有关这些安全权限的详细信息，请参阅[配置证书基础结构](../deploy-use/certificate-infrastructure.md)。  

 当你使用此默认配置时，用户和设备无法通过证书模板直接请求证书，所有请求必须由网络设备注册服务发起。 此限制非常重要，因为对于证书使用者，这些证书模板必须配置为包含“在请求中提供”  ，这意味着，如果恶意用户或泄露的设备请求了证书，则存在假冒的风险。 在默认配置中，网络设备注册服务必须发起此类请求。 但是，如果运行网络设备注册服务的服务已泄露，则这种假冒风险仍然存在。 为了帮助避免这种风险，请为网络设备注册服务和运行此角色服务的计算机遵循所有最佳安全方案。  

 如果默认安全权限无法满足你的业务要求，你可以选择使用其他方法配置证书模板的安全权限：你可以为用户和计算机添加读取和注册权限。  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>为用户和计算机添加“读取”和“注册”权限  
 如果一个独立团队管理你的证书颁发机构 (CA) 基础结构团队，并且该独立团队希望 System Center Configuration Manager 在向用户发送证书配置文件来请求用户证书之前验证用户是否具有有效的 Active Directory 域服务帐户，则可能适合为用户和计算机添加“读取”和“注册”权限。 对于此配置，你必须指定包含用户的一个或多个安全组，然后向那些组授予对证书模板的“读取”和“注册”权限。 在这种情况下，CA 管理员将管理安全控制。  

 你可以同样指定包含计算机帐户的一个或多个安全组，并授予这些组对证书模板的“读取”和“注册”权限。 如果将计算机证书配置文件部署到是域成员的计算机，则必须为该计算机的计算机帐户授予“读取”和“注册”权限。 如果计算机不是域成员（例如，它是工作组计算机或个人移动设备），则无需这些权限。  

 尽管此配置使用额外的安全控制，但这不是推荐的最佳做法。 因为指定的用户或设备的所有者可独立于 System Center Configuration Manager 请求证书，并为证书“使用者”提供可能用于假冒另一个用户或设备的值。  

 此外，如果你指定无法在进行证书请求时进行验证的帐户，则默认情况下证书请求将失败。 例如，运行网络设备注册服务的服务器位于包含证书注册点站点系统服务器的林不信任的 Active Directory 林中，则证书请求将失败。 你可以将证书注册点配置为在帐户由于域控制器无响应而无法进行验证的情况下继续。 但是，这不是一种最佳安全做法。  

 请注意，如果证书注册点配置为检查是否有帐户权限以及域控制器是否可用，并且拒绝身份验证请求（例如，帐户被锁定或已删除），则证书注册请求将失败。  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>检查用户和域成员计算机的“读取”和“注册”权限  

1.  在承载证书注册点的站点系统服务器上，创建下列 DWORD 注册表项以具有值 0：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  如果帐户由于域控制器无响应而无法进行验证，并且你要绕过权限检查：  

    -   在承载证书注册点的站点系统服务器上，创建下列 DWORD 注册表项以具有值 1：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  在颁发 CA 的证书模板属性内的“安全”  选项卡上，添加一个或多个安全组以向用户或设备帐户授予“读取”和“注册”权限。  
