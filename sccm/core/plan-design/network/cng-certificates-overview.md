---
title: "CNG 证书概述"
titleSuffix: Configuration Manager
description: "Configuration Manager 中的 CNG 证书概述"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>CNG 证书概述
<!-- 1356191 --> 

Configuration Manager 对下一代加密技术 (CNG) 证书提供有限支持。 Configuration Manager 客户端可以通过 CNG 密钥存储提供者 (KSP) 中的私钥使用 PKI 客户端身份验证证书。 通过 KSP 支持，Configuration Manager 客户端可支持基于硬件的私钥，如用于 PKI 客户端身份验证证书的 TPM KSP。

## <a name="supported-scenarios"></a>支持的方案
可以将[下一代加密技术 (CNG) API](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) 证书模板用于以下方案：

- 客户端注册和与 HTTPS 管理点的通信。   
- 使用 HTTPS 分发点的软件分发和应用程序部署。   
- 操作系统部署。  
- 客户端消息 SDK（具有最新更新）和 ISV 代理。   
- 云管理网关配置。  

> [!NOTE]
> CNG 后向兼容 crypto API (CAPI)。 即使 CNG 支持已在客户端启用，CAPI 证书仍继续得到支持。

## <a name="unsupported-scenarios"></a>不支持的方案

当前不支持以下方案：

- 当以 HTTPS 模式安装且 CNG 证书绑定到 Internet Information Services (IIS) 的网站时，应用程序目录 Web 服务、应用程序目录网站、注册点和注册代理点角色均无法运行。 在应用程序和包部署到用户或用户组集合时，软件中心不会将其显示为可用。

- 当以 HTTPS 模式安装且 CNG 证书绑定到 IIS 中的网站时，状态迁移点无法运行。

- 使用 CNG 证书创建云分发点。

- 如果 NDES 策略模块正在将 CNG 证书用作客户端身份验证证书，则 NDES 策略模块与证书注册点 (CRP) 通信失败。

- 如果已指定 CNG 证书，任务序列媒体创建将无法创建可启动媒体。

## <a name="to-use-cng-certificates"></a>使用 CNG 证书

若要使用 CNG 证书，证书颁发机构 (CA) 需要为目标计算机提供 CNG 证书模板。 模板详细信息因场景而异；但是，还需要提供以下属性：

- “兼容性”选项卡

    - “证书颁发机构”必须是 Windows Server 2008 或更高版本。 （建议使用 Windows Server 2012）。

    - “证书接收者”必须是 Windows Vista/Server 2008 或更高版本。 （建议使用 Windows 8/Windows Server 2012）。

- “加密”选项卡

    - “提供程序类别”必须是“密钥存储提供者”。 （必需）

> [!NOTE]
> 对环境或组织的需求可能有所不同。 请联系 PKI 专家。 证书模板必须使用密钥存储提供者来利用 CNG，这一点要着重考虑。

为获得最佳结果，我们建议从 Active Directory 信息中生成“使用者名称”。 使用“使用者名称格式”的 DNS 名称，并在另一个使用者名称中包含 DNS 名称。 否则，必须在设备注册到证书配置文件时提供此信息。