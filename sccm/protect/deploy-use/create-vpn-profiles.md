---
title: "如何在 System Center Configuration Manager 中创建 VPN 配置文件 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中创建 VPN 配置文件。"
ms.custom: 
ms.date: 4/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: "15"
author: lleonard-msft
caps.handback.revision: "0"
ms.author: alleonar
ms.manager: angrobe
ms.openlocfilehash: 359fcfd9754fb5c81763bc44cac45376ea3ab0b8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

[System Center Configuration Manager 中的 VPN 配置文件](../../protect/deploy-use/vpn-profiles.md) 中介绍了不同设备平台可用的连接类型。  

对于第三方 VPN 连接，在部署 VPN 配置文件之前分发 VPN 应用。 如果不部署应用，则将在用户尝试连接到 VPN 时提示他们部署应用。 若要了解如何部署应用，请参阅[使用 System Center Configuration Manager 部署应用程序](../../apps/deploy-use/deploy-applications.md)。

### <a name="create-a-vpn-profile"></a>创建 VPN 配置文件   

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “符合性设置” > “公司资源访问” > “VPN 配置文件”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建 VPN 配置文件”。  


1.  完成“常规”页。 ，并注意以下事项：  

    - VPN 配置文件名称中不要使用字符 \\/:*?&lt;>&#124; 或空格。 Windows Server VPN 配置文件不支持这些字符。  

     -   选择“从文件中导入现有 VPN 配置文件项”，将已导出到 XML 文件的 VPN 配置文件信息导入（仅适用于 Windows 8.1 和 Windows RT）。  

1.  在“连接”页面上，指定以下内容：  

    -   **连接类型**：选择 VPN 连接类型。 可从下表的连接类型中进行选择。  

    -   **服务器列表**：添加用于 VPN 连接的新服务器。 根据连接类型，可以添加一个或多个 VPN 服务器，并指定默认服务器。  

        > [!NOTE]  
        >  运行 iOS 的设备不支持使用多个 VPN 服务器。 如果配置多个 VPN 服务器并随后将 VPN 配置文件部署到 iOS 设备，则只会使用默认服务器。  

     此表提供了可供选择的连接类型。 请参阅 VPN 服务器文档以了解更多信息。

| &nbsp;&nbsp;选项&nbsp;&nbsp; | 更多信息 | &nbsp;&nbsp;连接&nbsp;类型&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**领域**     |想要使用的身份验证领域。 身份验证领域是“脉冲安全”连接类型使用的身份验证资源的分组。|脉冲安全|    
|**角色**        |有权访问此连接的用户角色。 |脉冲安全|  
|**登录组或域** |想要连接到的登录组或域的名称。|Dell SonicWALL Mobile Connect|  
|**指纹**  |将用于验证 VPN 服务器是否可以信任的字符串（例如“Contoso Fingerprint Code”）。<br /><br /> 指纹可以：<br /><br /> - 发送到客户端，使其知道在连接时可信任所有提供相同指纹的服务器。<br /><br /> - 如果设备还没有指纹，其将在显示指纹时提示用户信任正连接到的 VPN 服务器（用户手动验证指纹并选择“信任”以连接）。|Check Point Mobile VPN|  
|**通过 VPN 连接发送所有网络流量** |如果未选择此选项，则可以为连接（针对 **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 和 **L2TP** 连接类型）指定其他路由，这被称为拆分或 VPN 隧道。<br /><br /> 仅将通过 VPN 隧道发送与公司网络的连接。 你连接到 Internet 上的资源时，不会使用 VPN 隧道。 |All|  
|**特定于连接的 DNS 后缀** |用于连接的特定于连接的域名系统 (DNS) 后缀。|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**连接到公司 Wi-Fi 网络时不使用 VPN**  |设备连接到公司 Wi-Fi 网络时，将不使用 VPN 连接。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**连接到家庭 Wi-Fi 网络时绕过 VPN**  |设备连接到家庭 Wi-Fi 网络时，将不使用 VPN 连接。|All|  
|**每个应用 VPN （iOS 7 及更高版本，Mac OS X 10.9 及更高版本）** |将此 VPN 连接与 iOS 应用相关联，以便在运行该应用时打开连接。 可在部署它时将 VPN 配置文件与应用关联。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
|**自定义 XML（可选）** |指定配置 VPN 连接的自定义 XML 命令。<br /><br /> 例如：<br /><br /> 对于“Pulse Secure”：<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> 对于“CheckPoint Mobile VPN”：<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> 对于“Dell SonicWALL Mobile Connect”：<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> 对于“F5 Edge Client”：<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> 有关如何编写自定义 XML 命令的详细信息，请参阅每个制造商 VPN 文档。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

> [!NOTE]  
>  有关特定于针对移动设备创建 VPN 配置文件的信息，请参阅[创建 VPN 配置文件](../../mdm/deploy-use/create-vpn-profiles.md)  

完成向导。 新的 VPN 配置文件将显示在“资产和符合性”  工作区的“VPN 配置文件”  节点中。

### <a name="next-steps"></a>后续步骤

- 对于第三方 VPN 连接，在部署 VPN 配置文件之前分发 VPN 应用。 如果不部署应用，则将在用户尝试连接到 VPN 时提示他们部署应用。 若要了解如何部署应用，请参阅[使用 System Center Configuration Manager 部署应用程序](../../apps/deploy-use/deploy-applications.md)。

- 部署 VPN 配置文件，如[如何在 System Center Configuration Manager 中部署配置文件](deploy-wifi-vpn-email-cert-profiles.md)中所述。  
