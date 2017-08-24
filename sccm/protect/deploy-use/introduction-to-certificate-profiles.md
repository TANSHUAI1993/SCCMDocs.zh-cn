---
title: "证书配置文件简介 | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的证书配置文件如何与 Active Directory 证书服务一起使用。"
ms.custom: na
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: "7"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7b1c0e449f3d1ef42e279e8707df6bf1df163b3f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的证书配置文件简介

*适用范围：System Center Configuration Manager (Current Branch)*


证书配置文件使用 Active Directory 证书服务和网络设备注册服务角色设置托管设备的身份验证证书，以便用户能够无缝地访问公司资源。 例如，可以创建和部署证书配置文件来为用户提供必要的证书，从而启动 VPN 和无线连接。 

证书配置文件可自动配置用户设备，以便能够访问诸如 Wi-Fi 网络和 VPN 服务器等公司资源，而不必手动安装证书或使用带外进程。 证书配置文件还有助于保持公司资源的安全，因为你可使用受企业公钥基础结构 (PKI) 支持的更安全的设置。 例如，你可以要求对所有 Wi-fi 和 VPN 连接进行服务器身份验证，因为你已经在托管设备上设置了所需证书。   

证书配置文件提供以下管理功能：  

-   通过企业证书颁发机构 (CA) 为运行 iOS、Windows 8.1、Windows RT 8.1、Windows 10 桌面和移动版以及 Android 的设备注册和续订证书。 这些证书随后可用于 Wi-Fi 和 VPN 连接。  

-   部署受信任的根 CA 证书和中间 CA 证书，以在需要服务器身份验证时针对 VPN 和 Wi-Fi 连接在设备上配置一个信任链。  

-   监视并报告已安装的证书。  

**例如：** 所有员工都必须能够连接到多个公司位置的 Wi-fi 热点。 部署连接 Wi-Fi 所需的证书并部署引用该证书以实现无缝用户连接的 Wi-Fi 配置文件。  

**例如：** 你有 PKI 并且想迁移到更灵活、更安全的证书设置方法，可使用户在不影响安全性的情况下从个人设备访问公司资源。 使用特定设备平台支持的设置和协议配置证书配置文件。 随后设备可从面向 Internet 的注册服务器自动请求这些证书。 然后，配置 VPN 配置文件以使用这些证书，以便设备能够访问公司资源。  

## <a name="types-of-certificate-profiles"></a>证书配置文件的类型  
 有 3 种类型的证书配置文件：  

-   **可信 CA 证书** - 可部署受信任的根 CA 或中间 CA 证书，以便在设备必须验证服务器时形成证书信任链。  

-   **简单证书注册协议 (SCEP)** - 可通过在运行 Windows Server 2012 R2 的服务器上使用 SCEP 协议和网络设备注册服务，为设备或用户请求一个证书。

    首先创建“受信任的 CA 证书”证书配置文件，然后才能创建“简单证书注册协议(SCEP)”证书配置文件。

-   **个人信息交换 (.pfx)** - 可为设备或用户请求一个 .pfx（又称 PKCS #12）证书。

    可以通过从现有证书[导入凭据](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md)或[定义证书](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md)颁发机构来处理请求的方式创建 PFX 证书配置文件。

    从版本 1706 开始，可以将 Microsoft 或 Entrust 用作“个人信息交换 (.pfx)”证书的证书颁发机构。


## <a name="requirements-and-supported-platforms"></a>要求和支持的平台  
若要部署使用 SCEP 的证书配置文件，必须在管理中心站点或主站点中的站点系统服务器上安装证书注册点。 还必须在运行 Windows Server 2012 R2（包含 Active Directory 证书服务角色和有效的 NDES）的服务器上安装 NDES 策略模块，即 Configuration Manager 策略模块，在需要证书的设备中可以访问该模块。 对于通过 Microsoft Intunee 注册的设备，则要求 NDES 可从 Internet 中访问，例如，位于外围子网（也称为 DMZ）中。  

PFX 证书还要求在管理中心站点或主站点中的站点系统服务器上具有证书注册点。  此外，还必须为证书指定证书颁发机构 (CA) 和相关访问凭据。  从版本 1706 开始，可以将 Microsoft 或 Entrust 指定为证书颁发机构。  

有关网络设备注册服务如何支持策略模块以便 Configuration Manager 可以部署证书的详细信息，请参阅[结合使用策略模块和网络设备注册服务](http://go.microsoft.com/fwlink/p/?LinkId=328657)。  

Configuration Manager 支持将证书部署到不同的证书存储，具体情况视要求、设备类型和操作系统而定。 支持下列设备和操作系统：  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 桌面和移动版  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  若要将配置文件部署到 Android、iOS、Windows Phone 和注册的 Windows 8.1 或更高版本设备，这些设备必须[在 Microsoft Intune 中注册](https://technet.microsoft.com/en-us/library/dn646962.aspx)。   

System Center Configuration Manager 的一个典型方案是，在连接使用 EAP-TLS、EAP-TTLS 和 PEAP 身份验证协议以及 IKEv2、L2TP/IPsec 和 Cisco IPsec VPN 隧道协议时，安装受信任的根 CA 证书以验证 Wi-Fi 和 VPN 服务器。  

你必须确保在设备上安装企业根 CA 证书，然后设备才能使用 SCEP 证书配置文件请求证书。  

你可以在 SCEP 证书配置文件中指定各种设置，以便针对不同的环境或连接要求请求自定义证书。 “创建证书配置文件向导”  包含两个注册参数页面。 首先，“SCEP 注册” 包含有关注册请求以及在何处安装证书的设置。 其次，“证书属性” 本身描述了请求的证书。  

## <a name="deploying-certificate-profiles"></a>部署证书配置文件  
 在部署证书配置文件时，配置文件内的证书文件安装在客户端设备上。 还将部署任何 SCEP 参数，并且将在客户端设备上处理 SCEP 请求。 可将证书配置文件部署到用户或设备集合，并为每个证书指定目标存储。 适用性规则确定证书是否可安装在设备上。 将证书配置文件部署到用户集合时，用户设备相关性确定用户的哪台设备将安装证书。 将包含用户证书的证书配置文件部署到设备集合时，默认情况下证书将安装在用户的每台主设备上。 可在“创建证书配置文件向导” 的“SCEP 注册”页上修改此行为，以将证书安装在用户的任何设备上。 此外，如果设备是工作组计算机，则不会将用户证书部署到这些设备。  

## <a name="monitoring-certificate-profiles"></a>监视证书配置文件  

可通过查看符合性结果或报表来监视证书配置文件部署。 [如何监视证书配置文件](/sccm/protect/deploy-use/monitor-certificate-profiles)中介绍了这些方法。


## <a name="automatic-revocation-of-certificates"></a>自动吊销证书  
 System Center Configuration Manager 在以下情况下会自动撤销使用证书配置文件部署的用户和计算机证书：  

-   设备已从 System Center Configuration Manager 管理停用。  

-   有选择地擦除了设备。  

-   设备在 System Center Configuration Manager 层次结构中受阻止。  

 为了吊销证书，站点服务器会将吊销命令发送至证书颁发机构。 吊销原因是“停止操作” 。  