---
title: CNG 证书概述
titleSuffix: Configuration Manager
description: 了解对适用于 Configuration Manager 客户端和服务器的下一代加密技术证书的支持。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fb57705079072e6a656464f5b7252b2ce05ad9d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123240"
---
# <a name="cng-certificates-overview"></a>CNG 证书概述
<!-- 1356191 --> 

Configuration Manager 提供一定程度的加密支持：下一代 (CNG) 证书. Configuration Manager 客户端可以通过 CNG 密钥存储提供者 (KSP) 中的私钥使用 PKI 客户端身份验证证书。 通过 KSP 支持，Configuration Manager 客户端可支持基于硬件的私钥，如用于 PKI 客户端身份验证证书的 TPM KSP。

## <a name="supported-scenarios"></a>支持的方案
可以使用[加密 API：下一代加密技术 (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) 证书模板用于以下方案：

- 客户端注册和与 HTTPS 管理点的通信   
- 使用 HTTPS 分发点的软件分发和应用程序部署   
- 操作系统部署  
- 客户端消息 SDK（具有最新更新）和 ISV 代理   
- 云管理网关配置  

从版本 1802 开始，CNG 证书将用于以下已启用 HTTPS 的服务器角色：<!-- 1357314 -->   
- 管理点
- 分发点
- 软件更新点
- 状态迁移点     

自版本 1806 起，CNG 证书将用于下述已启用 HTTPS 的服务器角色：

- 证书注册点，包括具有 Configuration Manager 策略模块的 NDES 服务器<!--1357314-->

> [!NOTE]
> CNG 后向兼容 crypto API (CAPI)。 即使 CNG 支持已在客户端启用，CAPI 证书仍继续得到支持。

## <a name="unsupported-scenarios"></a>不支持的方案

当前不支持以下方案：

- 当以 HTTPS 模式安装且 CNG 证书绑定到 Internet Information Services (IIS) 中的网站时，以下服务器角色无法运行： 
    - 应用程序目录 Web 服务
    - 应用程序目录网站
    - 注册点  
    - 注册代理点  

- 在应用程序和包部署到用户或用户组集合时，软件中心不会将其显示为可用。

- 使用 CNG 证书创建云分发点。

- 如果 NDES 策略模块使用 CNG 证书进行客户端身份验证，则其与证书注册点的通信会失败。 
    - 自 Configuration Manager 1806 起支持此方案。

- 如果在创建任务序列媒体时指定 CNG 证书，则该向导无法创建可启动的媒体。
    - 自 Configuration Manager 1806 起支持此方案。

## <a name="to-use-cng-certificates"></a>使用 CNG 证书

若要使用 CNG 证书，证书颁发机构 (CA) 需要为目标计算机提供 CNG 证书模板。 模板详细信息因场景而异；但是，还需要提供以下属性：

- “兼容性”选项卡

    - “证书颁发机构”必须是 Windows Server 2008 或更高版本。 （建议使用 Windows Server 2012）。

    - “证书接收者”必须是 Windows Vista/Server 2008 或更高版本。 （建议使用 Windows 8/Windows Server 2012）。

- “加密”选项卡

    - “提供程序类别”必须是“密钥存储提供者”。 （必需）
    - **请求必须使用以下提供程序之一：** 必须要是 Microsoft 软件密钥存储提供程序。 

> [!NOTE]
> 对环境或组织的需求可能有所不同。 请联系 PKI 专家。 证书模板必须使用密钥存储提供者来利用 CNG，这一点要着重考虑。

为获得最佳结果，我们建议从 Active Directory 信息中生成“使用者名称”。 使用“使用者名称格式”的 DNS 名称，并在另一个使用者名称中包含 DNS 名称。 否则，必须在设备注册到证书配置文件时提供此信息。
