---
title: "PKI 证书要求 | Microsoft Docs"
description: "查找 System Center Configuration Manager 可能需要的 PKI 证书的要求。"
ms.custom: na
ms.date: 04/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6a73e68-57d8-4786-842b-36669541d8ff
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a99b58acef7448af2c9576bfa0ec2635f5a4f86f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="pki-certificate-requirements-for-system-center-configuration-manager"></a>System Center Configuration Manager 的 PKI 证书要求

*适用范围：System Center Configuration Manager (Current Branch)*

以下各个表列出了 System Center Configuration Manager 可能需要的公钥基础结构 (PKI) 证书。 此信息假定用户对 PKI 证书有着基本了解。 如需逐步部署指南，请参阅 [System Center Configuration Manager PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)。 有关 Active Directory 证书服务的详细信息，请参阅下列文档：  

-   对于 Windows Server 2012： [Active Directory 证书服务概述](http://go.microsoft.com/fwlink/p/?LinkId=286744)  

-   对于 Windows Server 2008： [Windows Server 2008 中的 Active Directory 证书服务](http://go.microsoft.com/fwlink/p/?LinkId=115018)  

> [!IMPORTANT]  
> System Center Configuration Manager 支持安全哈希算法 2 (SHA-2) 证书。 SHA-2 证书引入了重大的安全改进功能。 因此，建议执行以下操作：
> - 颁发使用 SHA-2（包括 SHA-256 和 SHA-512 等）签名的新服务器和客户端身份验证证书。
> - 所有面向 Internet 的服务均应使用 SHA-2 证书。 例如，如果购买用于云管理网关的公用证书，请确保购买 SHA-2 证书。  
>
>自 2017 年 2 月 14 日起生效， Windows 不再信任使用 SHA-1 签名的某些证书。 通常，建议颁发使用 SHA-2（包括 SHA-256 和 SHA-512 等）签名的新服务器和客户端身份验证证书。 此外，建议所有面向 Internet 的服务均使用 SHA-2 证书。 例如，如果购买用于云管理网关的公用证书，请确保购买 SHA-2 证书。
>
> 在大多数情况下，对 SHA-2 证书的更改不会影响操作。 有关详细信息，请参阅 [Windows Enforcement of SHA1 certificates](http://social.technet.microsoft.com/wiki/contents/articles/32288.windows-enforcement-of-sha1-certificates.aspx)（Windows 针对 SHA1 证书的强制措施）。

 除了 System Center Configuration Manager 在移动设备和 Mac 计算机上注册的客户端证书、Microsoft Intune 为管理移动设备自动创建的证书以及 System Center Configuration Manager 在基于 AMT 的计算机上安装的证书以外，可以使用任何 PKI 来创建、部署和管理以下证书。 但是，当你使用 Active Directory 证书服务和证书模板时，可以使用此 Microsoft PKI 解决方案轻松地管理证书。 使用以下各表中的“要使用的 Microsoft 证书模板”  列来确定最符合证书要求的证书模板。 仅运行于服务器操作系统的企业版或数据中心版（例如 Windows Server 2008 Enterprise 和 Windows Server 2008 Datacenter）上的企业证书颁发机构可以使用基于模板的证书。  

> [!IMPORTANT]  
>  当使用企业证书颁发机构和证书模板时，请不要使用版本 3 模板。 这些证书模板会创建与 System Center Configuration Manager 不兼容的证书。 请按照下列说明改为使用版本 2 模板：  
>   
>  -   对于 Windows Server 2012 上的 CA：在证书模板属性的“兼容性”  选项卡上，为“证书颁发机构”  选项指定“Windows Server 2003”  ，并为“证书接收者”  选项指定“Windows XP/Server 2003”  。  
> -   对于 Windows Server 2008 上的 CA：在复制证书模板时，请在“复制模板”对话框提示你时保留默认选择“Windows Server 2003 Enterprise”。 不要选择“Windows Server 2008，Enterprise Edition” 。  

 使用下列部分来查看证书要求。  

##  <a name="BKMK_PKIcertificates_for_servers"></a> 服务器的 PKI 证书  

|System Center Configuration Manager 组件|证书用途|要使用的 Microsoft 证书模板|证书中的特定信息|如何在 System Center Configuration Manager 中使用证书|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|运行 Internet Information Services (IIS) 并针对 HTTPS 客户端连接进行设置的站点系统：<br /><br /> <ul><li>管理点</li><li>分发点</li><li>软件更新点</li><li>状态迁移点</li><li>注册点</li><li>注册代理点</li><li>应用程序目录 Web 服务点</li><li>应用程序目录网站点</li><li>证书注册点</li></ul>|服务器身份验证|**Web 服务器**|“增强型密钥用法” 值必须包含“服务器身份验证 (1.3.6.1.5.5.7.3.1)” 。<br /><br /> 如果站点系统接受来自 Internet 连接，则“使用者名称”或“使用者备用名称”必须包含 Internet 完全限定的域名 (FQDN)。<br /><br /> 如果站点系统接受来自 Intranet 的连接，则“使用者名称”或“使用者备用名称”必须包含 Intranet FQDN（建议）或计算机的名称，视站点系统的设置方式而定。<br /><br /> 如果站点系统接受来自 Internet 和 Intranet 的连接，则必须在 Internet FQDN 和 Intranet FQDN（或计算机名）之间使用和号 (&) 分隔符来指定这两个名称。<br /><br /> **注意：**当软件更新点仅接受来自 Internet 的客户端连接时，该证书必须包含 Internet FQDN 和 Intranet FQDN。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> System Center Configuration Manager 不指定此证书支持的最大密钥长度。 任何有关此证书密钥大小的相关问题，请参阅 PKI 和 IIS 文档。|此证书必须位于计算机证书存储的个人存储中。<br /><br /> 此 Web 服务器证书用于向客户端对这些服务器进行身份验证，并通过使用安全套接字层 (SSL) 对它们之间传输的所有数据进行加密。|  
|基于云的分发点|服务器身份验证|**Web 服务器**|“增强型密钥用法” 值必须包含“服务器身份验证 (1.3.6.1.5.5.7.3.1)” 。<br /><br /> “使用者名称”必须包含客户定义的服务名称和 FQDN 格式的域名作为基于云的分发点的特定实例的公用名。<br /><br /> 私钥必须是可导出的。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的密钥长度：2,048 位。|此服务证书用于向 Configuration Manager 客户端验证基于云的分发点服务，并通过使用安全套接字层 (SSL) 对它们之间传输的所有数据进行加密。 必须采用公钥证书标准 (PKCS #12) 格式导出此证书，并且密码必须已知，以便在创建基于云的分发点时可以导入该证书。<br /><br /> **注意：** 该证书与 Windows Azure 管理证书结合使用。 |  
|运行 Microsoft SQL Server 的站点系统服务器|服务器身份验证|**Web server**|“增强型密钥用法” 值必须包含“服务器身份验证 (1.3.6.1.5.5.7.3.1)” 。<br /><br /> “使用者名称”必须包含 Intranet 完全限定的域名 (FQDN)。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|此证书必须位于“计算机”证书存储的“个人”存储中。 System Center Configuration Manager 会将其自动复制到 System Center Configuration Manager 层次结构中可能必须与服务器建立信任的服务器的“受信任人”存储。<br /><br /> 这些证书用于服务器间身份验证。|  
|SQL Server 群集：运行 Microsoft SQL Server 的站点系统服务器|服务器身份验证|**Web server**|“增强型密钥用法” 值必须包含“服务器身份验证 (1.3.6.1.5.5.7.3.1)” 。<br /><br /> “使用者名称”必须包含群集的 Intranet 完全限定的域名 (FQDN)。<br /><br /> 私钥必须是可导出的。<br /><br /> 配置 System Center Configuration Manager 来使用 SQL Server 群集时，证书必须包含至少两年的有效期。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|在群集中的一个节点上请求并安装了此证书后，请导出证书并将其导入到 SQL Server 群集中的每个其他节点。<br /><br /> 此证书必须位于“计算机”证书存储的“个人”存储中。 System Center Configuration Manager 会将其自动复制到 System Center Configuration Manager 层次结构中可能必须与服务器建立信任的服务器的“受信任人”存储。<br /><br /> 这些证书用于服务器间身份验证。|  
|下列站点系统角色的站点系统监视：<br /><br /><ul><li>管理点</li><li>状态迁移点</li></ul>|客户端身份验证|**工作站身份验证**|“增强型密钥用法”值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 计算机必须在“使用者名称”字段或“使用者备用名称”字段中有唯一的值。<br /><br /> **注意：**如果将多个值用于“使用者可选名称”，则只会使用第一个值。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|此证书在列出的站点系统服务器上是必需的（即使未安装 System Center Configuration Manager 客户端）。 可以通过此设置监视这些站点系统角色的运行状况并向站点报告。<br /><br /> 这些站点系统的证书必须位于“计算机”证书存储的“个人”存储中。|  
|将 System Center Configuration Manager 策略模块与网络设备注册服务角色服务一起运行的服务器|客户端身份验证|**工作站身份验证**|“增强型密钥用法” 值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 对证书“使用者”或“使用者可选名称 (SAN)”没有特定要求。 可以将同一个证书用于多个运行“网络设备注册服务”的服务器。<br /><br /> 支持 SHA-2 和 SHA-3 哈希算法。<br /><br /> 支持的密钥长度：1,024 位和 2,048 位。||  
|安装了分发点的站点系统|客户端身份验证|**工作站身份验证**|“增强型密钥用法” 值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 对证书“使用者”或“使用者可选名称 (SAN)”没有特定要求。 可以将同一个证书用于多个分发点。 但是，最好为每个分发点使用不同的证书。<br /><br /> 私钥必须是可导出的。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|此证书有两个用途：<br /><br /><ul><li>在分发点发送状态消息之前，此证书向启用 HTTPS 的管理点验证分发点。</li><li>如果选择了“为客户端启用 PXE 支持”分发点选项，则将证书发送到计算机。 在操作系统部署过程中的任务序列包括客户端操作（例如，客户端策略检索或发送清单信息）的情况下，客户端计算机可在操作系统部署过程中连接到启用 HTTPS 的管理点。</li></ul> 此证书仅在操作系统部署过程中使用，不会安装在客户端上。 由于这种暂时使用，如果您不想使用多个客户端证书，则可将同一个证书用于每个操作系统部署。<br /><br /> 此证书必须使用公钥证书标准 (PKCS #12) 格式导出。 必须知道密码，以便将其导入分发点属性。<br /><br /> **注意：**此证书的要求与部署操作系统的启动映像的客户端证书相同。 由于要求相同，因此你可以使用同一证书文件。|  
|带外服务点|AMT 设置|**Web 服务器** （已修改）|“增强型密钥用法” 值必须包含“服务器身份验证 (1.3.6.1.5.5.7.3.1)”  和以下对象标识符： **2.16.840.1.113741.1.2.3**。<br /><br /> 使用者名称字段必须包含承载带外服务点的服务器的 FQDN。<br /><br /> **注意：**从外部 CA 而非自己的内部 CA 请求的 AMT 设置证书可能不支持 AMT 设置对象标识符 2.16.840.1.113741.1.2.3。 或者可以选择将以下文本字符串指定为证书使用者名称中的组织单位 (OU) 属性：**Intel(R) Client Setup Certificate**。 必须完全按原样使用这一英文文本字符串（大小写相同，不带后面的句号），另外再加上承载带外服务点的服务器的 FQDN。<br /><br /> 支持的密钥长度：1,024 和 2,048。 对于 AMT 6.0 及更高版本，还支持 4,096 位的密钥长度。|此证书位于带外服务点站点系统服务器的“计算机”证书存储的“个人”存储中。<br /><br /> 此 AMT 设置证书用于为带外管理准备计算机。<br /><br /> 你必须从提供 AMT 设置证书的 CA 请求此证书。 必须设置基于 Intel AMT 的计算机的 BIOS 扩展以便为此设置证书使用根证书指纹（也称为证书哈希）。<br /><br /> VeriSign 是提供 AMT 设置证书的外部 CA 的典型示例，但你也可以使用自己的内部 CA。<br /><br /> 将证书安装在承载带外服务点的服务器上，该服务器必须能够成功地链接到证书的根 CA。 （默认情况下，在 Windows 安装时会安装 VeriSign 的根 CA 证书和中间 CA 证书。）|  
|运行 Microsoft Intune 连接器的站点系统服务器|客户端身份验证|不适用：Intune 会自动创建此证书。|“增强型密钥用法”值包含“客户端身份验证 (1.3.6.1.5.5.7.3.2)”。<br /><br /> 3 个自定义扩展唯一地标识客户的 Intune 订阅。<br /><br /> 密钥大小为 2,048 位，并且使用 SHA-1 哈希算法。<br /><br /> **注意：**无法更改这些设置。 此信息仅供参考。|订阅 Microsoft Intune 时，会自动请求此证书并将其安装到 Configuration Manager 数据库。 安装 Microsoft Intune 连接器时，此证书会随后安装到运行 Microsoft Intune 连接器的站点系统服务器上。 它将安装到“计算机”证书存储中。<br /><br /> 此证书用于通过 Microsoft Intune 连接器向 Microsoft Intune 验证 Configuration Manager 层次结构。 在它们之间传输的所有数据都使用安全套接字层 (SSL)。|  

###  <a name="BKMK_PKIcertificates_for_proxyservers"></a>用于基于 Internet 的客户端管理的代理 Web 服务器  
 如果站点支持基于 Internet 的客户端管理，并且通过为传入 Internet 连接使用 SSL 终端（桥接）来使用代理 Web 服务器，则代理 Web 服务器具有下表所列的证书要求。  

> [!NOTE]  
>  如果你使用代理 Web 服务器但不使用 SSL 终端（隧道），则代理 Web 服务器不需要其他证书。  

|网络基础结构组件|证书用途|要使用的 Microsoft 证书模板|证书中的特定信息|如何在 System Center Configuration Manager 中使用证书|  
|--------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|接受通过 Internet 的客户端连接的代理 Web 服务器|服务器身份验证和客户端身份验证|1. <br />                        **Web 服务器**<br /><br /> 2. <br />                        **工作站身份验证**|“使用者名称”字段或“使用者备用名称”字段中 的 Internet FQDN。 如果使用的是 Microsoft 证书模板，“使用者备用名称”只能与工作站模板配合使用。<br /><br /> 支持 SHA-2 哈希算法。|此证书用于向 Internet 客户端对以下服务器进行验证，以及通过使用 SSL 对客户端和此服务器之间传输的所有数据进行加密：<br /><br /><ul><li>基于 Internet 的管理点</li><li>基于 Internet 的分发点</li><li>基于 Internet 的软件更新点</li></ul> 客户端身份验证用于在 System Center Configuration Manager 客户端与基于 Internet 的站点系统之间桥接客户端连接。|  

##  <a name="BKMK_PKIcertificates_for_clients"></a> 客户端的 PKI 证书  

|System Center Configuration Manager 组件|证书用途|要使用的 Microsoft 证书模板|证书中的特定信息|如何在 System Center Configuration Manager 中使用证书|  
|-------------------------------------|-------------------------|-------------------------------------------|---------------------------------------------|----------------------------------------------------------|  
|Windows 客户端计算机|客户端身份验证|**工作站身份验证**|“增强型密钥用法”值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)** 。<br /><br /> 客户端计算机必须在“使用者名称”字段或“使用者备用名称”字段中有唯一的值。<br /><br /> **注意：**如果将多个值用于“使用者可选名称”，则只会使用第一个值。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|在默认情况下，System Center Configuration Manager 将在计算机证书存储的个人存储中查找计算机证书。<br /><br /> 除了软件更新点和应用程序目录网站点以外，此证书向运行 IIS 并且设置为使用 HTTPS 的站点系统服务器验证客户端。|  
|移动设备客户端|客户端身份验证|**经过验证的会话**|“增强型密钥用法”值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> SHA-1<br /><br /> 支持的最大密钥长度为 2,048 位。<br /><br /> **注意：**<br /><br /><ul><li>这些证书必须采用可分辨编码规则 (DER) 编码的二进制 X.509 格式。</li><li>不支持 Base64 编码的 X.509 格式。</li></ul>|此证书向它与之通信的站点系统服务器（例如管理点和分发点）验证移动设备客户端。|  
|用于部署操作系统的启动映像|客户端身份验证|**工作站身份验证**|“增强型密钥用法”值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 没有针对证书“使用者名称”字段或“使用者备用名称” (SAN) 的特定要求，并且你可以为所有启动映像使用同一证书。<br /><br /> 私钥必须是可导出的。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|如果操作系统部署过程中的任务序列包括客户端操作（例如客户端策略检索或发送清单信息），则会使用该证书。<br /><br /> 此证书仅在操作系统部署过程中使用，不会安装在客户端上。 由于这种暂时使用，如果您不想使用多个客户端证书，则可将同一个证书用于每个操作系统部署。<br /><br /> 必须采用公钥证书标准 (PKCS #12) 格式导出此证书，并且密码必须已知，以便可将其导入 System Center Configuration Manager 启动映像中。<br /><br /> 此证书临时用于任务序列，不可用于安装客户端。 如果你的环境中仅包含 HTTPS，则客户端必须具有有效证书才能与站点通信并继续部署。 客户端加入 Active Directory 时会自动生成证书，或者你也可以通过其他方法安装客户端证书。<br /><br /> **注意：** 此证书的要求与安装了分发点的站点系统的服务器证书的要求相同。 由于要求相同，因此你可以使用同一证书文件。|  
|Mac 客户端计算机|客户端身份验证|对于 System Center Configuration Manager 注册：**经过验证的会话**<br /><br /> 对于独立于 System Center Configuration Manager 的证书安装：**工作站身份验证**|“增强型密钥用法” 值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 对于创建用户证书的 System Center Configuration Manager，会使用注册 Mac 计算机的人员的用户名自动填充证书使用者值。<br /><br /> 安装证书时，如果不使用 System Center Configuration Manager 注册，但独立于 System Center Configuration Manager 部署计算机证书，则证书使用者值必须唯一。 例如，指定计算机的 FQDN。<br /><br /> 不支持“使用者可选名称”字段。<br /><br /> 支持 SHA-2 哈希算法。<br /><br /> 支持的最大密钥长度为 2,048 位。|此证书向它与之通信的站点系统服务器（例如管理点和分发点）验证 Mac 客户端计算机。|  
|Linux 和 UNIX 客户端计算机|客户端身份验证|**工作站身份验证**|“增强型密钥用法” 值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 不支持“使用者可选名称”字段。<br /><br /> 私钥必须是可导出的。<br /><br /> 如果客户端操作系统支持 SHA-2，则支持 SHA-2 哈希算法。 有关详细信息，请参阅[在 System Center Configuration Manager 中规划对 Linux 和 UNIX 计算机的客户端部署](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)中的[关于不支持 SHA-256 的 Linux 和 UNIX 操作系统](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)部分。<br /><br /> 支持的密钥长度：2,048 位。<br /><br /> **注意：** 这些证书必须采用可分辨编码规则 (DER) 编码的二进制 X.509 格式。 不支持 Base64 编码的 X.509 格式。|此证书向它与之通信的站点系统服务器（例如管理点和分发点）验证 Linus 或 UNIX 客户端计算机。 必须采用公钥证书标准 (PKCS #12) 格式导出此证书，并且密码必须已知，以便可以在指定 PKI 证书时将它指定到客户端。<br /><br /> 有关详细信息，请参阅[在 System Center Configuration Manager 中规划对 Linux 和 UNIX 计算机的客户端部署](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md)中的[为 Linux 和 UNIX 服务器规划安全性和证书](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_SecurityforLnU)部分。|  
|下列情况下的根证书颁发机构 (CA) 证书：<br /><br /><ul><li>操作系统部署</li><li>移动设备注册</li><li>基于 Intel AMT 的计算机的 RADIUS 服务器身份验证</li><li> 客户端证书身份验证</li></ul>|到受信任来源的证书链|不适用。|标准的根 CA 证书。|在客户端必须将通信服务器的证书链接到受信任的来源时，必须提供根 CA 证书。 这适用于下列情况：<br /><br /><ul><li>部署操作系统，而且运行该操作系统的任务序列将客户端计算机连接到设置为使用 HTTPS 的管理点时。</li><li>注册由 System Center Configuration Manager 托管的移动设备时。</li><li>使用 802.1X 对基于 AMT 的计算机进行身份验证，而且想为 RADIUS 服务器的根证书指定文件时。</li></ul> 此外，如果颁发客户端证书的 CA 层次结构与颁发管理点证书的 CA 层次结构不同，则必须提供客户端的根 CA 证书。|  
|基于 Intel AMT 的计算机|服务器身份验证。|**Web 服务器** （已修改）<br /><br /> 必须为“用 Active Directory 中的信息生成” 配置使用者名称，然后为“使用者名称格式”  选择“公用名” 。<br /><br /> 对于你在带外管理组件属性中指定的通用安全组，必须向其授予“读取”和“注册”权限。|“增强型密钥用法” 值必须包含“服务器身份验证 (1.3.6.1.5.5.7.3.1)” 。<br /><br /> 使用者名称必须包含基于 AMT 的计算机的 FQDN，它是自动通过 Active Directory 域服务提供的。|此证书驻留在计算机中的管理控制器的永久性随机存取内存中，而且在 Windows 用户界面中不可见。<br /><br /> 每台基于 Intel AMT 的计算机都会在 AMT 设置期间以及后续更新时请求此证书。 如果从这些计算机中删除 AMT 设置信息，则它们会吊销此证书。<br /><br /> 在基于 Intel AMT 的计算机上安装此证书时，也会安装到根 CA 的证书链。 基于 AMT 的计算机不能支持密钥长度大于 2,048 位的 CA 证书。<br /><br /> 在基于 Intel AMT 的计算机上安装此证书之后，此证书将向带外服务点站点系统服务器和运行带外管理控制台的计算机验证基于 AMT 的计算机，并使用传输层安全性 (TLS) 对在它们之间传输的所有数据进行加密。|  
|Intel AMT 802.1X 客户端证书|客户端身份验证|**工作站身份验证**<br /><br /> 必须为“用 Active Directory 中的信息生成”设置使用者名称，为“使用者名称格式”选择“公用名”，清除 DNS 名称，并为使用者可选名称选择用户主体名称 (UPN)。<br /><br /> 对于你在带外管理组件属性中指定的通用安全组，必须向其授予此证书模板的“读取”和“注册”权限。|“增强型密钥用法” 值必须包含**客户端身份验证 (1.3.6.1.5.5.7.3.2)**。<br /><br /> 使用者名称字段必须包含基于 AMT 的计算机的 FQDN，而使用者可选名称必须包含 UPN。<br /><br /> 支持的最大密钥长度：2,048 位。|此证书驻留在计算机中的管理控制器的永久性随机存取内存中，而且在 Windows 用户界面中不可见。<br /><br /> 每台基于 Intel AMT 的计算机都可以在 AMT 设置期间请求此证书，但是，在删除计算机的 AMT 设置信息时，其不会吊销此证书。<br /><br /> 在基于 AMT 的计算机上安装此证书之后，此证书将向 RADIUS 服务器验证基于 AMT 的计算机，以便它之后能获得网络访问的授权。|  
|Microsoft Intune 注册的移动设备|客户端身份验证|不适用：Intune 会自动创建此证书。|“增强型密钥用法”值包含“客户端身份验证 (1.3.6.1.5.5.7.3.2)”。<br /><br /> 三个自定义扩展唯一地标识客户 Intune 订阅。<br /><br /> 用户可以在注册过程中提供证书使用者值。 但是，Intune 不使用此值标识设备。<br /><br /> 密钥大小为 2,048 位，并且使用 SHA-1 哈希算法。<br /><br /> **注意：**无法更改这些设置。 此信息仅供参考。|经过身份验证的用户使用 Microsoft Intune 注册他们的移动设备时，会自动请求和安装此证书。 设备上的最终证书驻留在计算机存储中，并且向 Intune 验证已注册的移动设备，以便之后可以管理它。<br /><br /> 由于证书中包含自定义扩展，因此，只能向已经为组织建立的 Intune 订阅进行验证。|
