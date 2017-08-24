---
title: "System Center Configuration Manager 中的 VPN 配置文件 | Microsoft Docs"
description: "System Center Configuration Manager 中移动设备上的 VPN 配置文件。"
ms.custom: na
ms.date: 07/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: "18"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: e4a53caab7d76b604a3fee7dcfc4dc48f22b0fb0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>System Center Configuration Manager 中移动设备上的 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的移动设备用户。 如果部署这些设置，可以最大限度地减少最终用户在连接公司网络上的资源时需要完成的工作。  

 例如，你希望使用连接公司网络上的文件共享所需的设置，设置所有运行 iOS 操作系统的设备。 可以创建一个含有连接公司网络所需的设置的 VPN 配置文件，然后将此配置文件部署到在你的层次结构中使用运行 iOS 的设备的所有用户。 IOS 设备用户可在可用网络列表中看到 VPN 连接，并可通过最少量的工作连接到此网络。  

 创建 VPN 配置文件时，可以纳入各种安全设置。 例如，可以为已使用 System Center Configuration Manager 证书配置文件设置的服务器验证和客户端身份验证指定证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)。  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>配合使用 Configuration Manager 和 Intune 时的 VPN 配置文件

 若要将配置文件部署到 iOS、Android、Windows Phone 和 Windows 8.1 设备，必须在 Microsoft Intune 中注册这些设备。 其他平台上的设备也可以注册到 Intune。 有关如何注册的信息，请参阅[使用 Microsoft Intune 管理移动设备](https://technet.microsoft.com/en-us/library/dn646962.aspx)。 下表展示了每个设备平台支持的连接类型：  

 |连接类型|iOS 和 macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 桌面和移动版|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|是|是|否|否|否|否|是 (OMA-URI)|
 |Cisco (IPSec)|仅限 iOS|否|否|否|否|否|否|  
 |脉冲安全|是|是|是|否|是|是|是|  
 |F5 Edge Client|是|是|是|否|是|是|是|  
 |Dell SonicWALL Mobile Connect|是|是|是|否|是|是|是|  
 |Check Point Mobile VPN|是|是|是|否|是|是|是|  
 |Microsoft SSL (SSTP)|否|否|是|是|是|否|否|  
 |Microsoft Automatic|否|否|是|是|是|否|是 (OMA-URI)|  
 |IKEv2|是（自定义策略）|否|是|是|是|是|是 (OMA-URI)|  
 |PPTP|是|否|是|是|是|否|是 (OMA-URI)|  
 |L2TP|是|否|是|是|是|否|是 (OMA-URI)|  

## <a name="create-vpn-profiles"></a>创建 VPN 配置文件
[如何在 System Center Configuration Manager 中创建 VPN 配置文件](../../protect/deploy-use/create-vpn-profiles.md)介绍了有关如何创建 VPN 配置文件的一般信息。

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>将 Configuration Manager 与 Intune 结合使用时可用的 Windows 10 VPN 功能  


> [!NOTE]  
> 使用 Windows 10 VPN 功能的 VPN 配置文件的名称既不能采用 Unicode 格式，也不能包含特殊字符。


|选项|更多信息|连接类型|  
    |------------|----------------------|---------------------|  
    |**连接到公司 Wi-Fi 网络时不使用 VPN**|设备连接到公司 Wi-Fi 网络时，将不使用 VPN 连接。 输入用于确定设备是否已连接公司网络的受信任网络名称。|All|  
    |**网络通信规则**|设置将为 VPN 连接启用的协议、本地端口、远程端口和地址范围。<br /><br /> **注意：**如果没有创建网络流量规则，将启用所有协议、端口和地址范围。 创建流量规则后，VPN 连接只会使用此规则或其他规则中指定的协议、端口和地址范围。|All|  
    |**路由**|将使用 VPN 连接的路由。 请注意，创建超过 60 个路由可能会导致策略失败。 |All|  
    |**DNS 服务器**|在建立 VPN 连接后连接所使用的 DNS 服务器。|All|  
    |**自动连接到 VPN 的应用**|可以添加自动使用 VPN 连接的应用或导入这些应用的列表。 应用的类型决定应用标识符。 对于桌面应用，请提供应用的文件路径。 对于通用的应用，请提供包系列名称 (PFN)。 若要了解如何查找应用的 PFN，请参阅[查找每个应用 VPN 的包系列名称](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。 |All|

> [!IMPORTANT]
> 我们建议你保护编译来用于每个应用 VPN 配置的关联应用的所有列表。 如果未经授权的用户更改你的列表，且你将此表导入每应用 VPN 应用列表中，则可能会向不应拥有访问权限的应用授予 VPN 访问权限。 保护应用列表的一种方法是使用访问控制列表 (ACL)。


1.  在向导的“身份验证方法”页上，指定下列信息：  

    -   **身份验证方法**：选择 VPN 连接将使用的身份验证方法。 可用的方法视连接类型而定，如此表中所示。  

        |身份验证方法|支持的&nbsp;连接&nbsp;类型|  
        |---------------------------|--------------------------------|  
        |**证书**<br /><br /> **注意：**<ul><li>如果客户端证书对 RADIUS 服务器（如网络策略服务器）进行身份验证，那么必须将证书中的使用者可选名称设置为用户主体名称。</li><li>对于 Android 部署，请选择 EKU 标识符和证书颁发者指纹哈希值。  否则，用户必须手动选择相应的证书。</li></ul>  |<ul><li>Cisco AnyConnect</li><li>脉冲安全</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
        |**用户名和密码**|<ul><li>脉冲安全</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**Microsoft 受保护的 EAP (PEAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Microsoft 受保护的密码 (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**智能卡或其他证书**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** （仅限 iOS）|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**使用计算机证书**|<ul><li>IKEv2</li></ul>|  

         可能需要指定更多信息，具体视选择的选项而定，比如：  

        -   **每次登录时记住用户凭据**：记住用户凭据，这样用户就不必在每次连接时都输入凭据。  

        -   **选择用于客户端身份验证的客户端证书**：选择之前创建的客户端 [SCEP 证书](create-pfx-certificate-profiles.md)，它将用于对 VPN 连接进行身份验证。   

            > [!NOTE]  
            >  对于 iOS 设备，选择的 SCEP 配置文件将嵌入 VPN 配置文件中。 对于其他平台，将添加适用性规则，以确保只有在证书存在或符合要求时才安装 VPN 配置文件。  
            >   
            >  如果你指定的 SCEP 证书不符合要求或尚未部署，那么将不会在设备上安装 VPN 配置文件。
            >  
            >  连接类型为“PPTP”时，运行 iOS 的设备对身份验证方法仅支持“RSA SecurID”和“MSCHAP v2”。 若要避免报告错误，请将单独的 PPTP VPN 配置文件部署到运行 iOS 的设备中。  

        - **条件性访问**
            - 选择“启用此 VPN 连接的条件性访问”可以确保连接到 VPN 的设备在连接前进行了条件性访问合规性测试。 [System Center Configuration Manager 中的设备符合性策略](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)中介绍了符合性策略。
            - 选中“启用使用替代证书进行单一登录(SSO)”可以选择除 VPN 身份验证证书以外的其他证书来验证设备符合性。 如果选中此选项，请输入 VPN 客户端应查找的正确证书的“EKU”（以逗号分隔的列表）和“颁发者哈希”。

         - 对于 **Windows 信息保护**，请输入企业管理的公司标识（通常是组织的主域，例如 *contoso.com*）。 可以指定组织拥有的多个域，只需用“|”字符来分隔域即可。 例如，*contoso.com|newcontoso.com*。   
            有关 Windows 信息保护的详细信息，请参阅[使用 Microsoft Intune 创建 Windows 信息保护 (WIP) 策略](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune)。   

         ![为 VPN 配置条件性访问](media/vpn-conditional-access.png)

         如果受运行 Configuration Manager 的 Windows 版本_和_选定授权方法支持，可以选择“配置”，打开“Windows 属性”对话框，并配置身份验证方法属性。  如果“配置”遭禁用，请使用其他方法来配置身份验证方法属性。

2.  在“创建 VPN 配置文件向导”的“代理设置”页上，如果 VPN 连接使用的是代理服务器，请选中“配置此 VPN 配置文件的代理设置”框。 然后提供代理服务器信息。 有关详细信息，请参阅 Windows Server 文档。  

    > [!NOTE]  
    >  在 Windows 8.1 计算机上，只有在使用此计算机连接 VPN 之后，VPN 配置文件才会显示代理信息。  


3. 根据需要，配置其他 DNS 设置。  
 在“配置自动 VPN 连接”页上，可以配置以下设置：  

    -   **按需启用 VPN**：如果要为 Windows Phone 8.1 设备配置更多 DNS 设置，请使用此选项。 此设置仅适用于 Windows Phone 8.1 设备，并且只能在将要部署到 Windows Phone 8.1 设备的 VPN 配置文件上启用。

    -   **DNS 后缀列表**（仅适用于 Windows Phone 8.1 设备）：配置将建立 VPN 连接的域。 对于指定的每个域，请添加 DNS 后缀、DNS 服务器地址和下面的一项按需操作：  

        -   **从不建立**：从不建立 VPN 连接。  

        -   **需要时建立**：仅在设备需要连接资源时建立 VPN 连接。  

        -   **始终建立**：始终建立 VPN 连接。  

    -   **合并**：将配置的所有 DNS 后缀复制到“受信任的网络列表”。  

    -   **受信任的网络列表**（仅适用于 Windows Phone 8.1 设备）：每行指定一个 DNS 后缀。 如果该设备处于受信任的网络中，将不会打开 VPN 连接。  

    -   **后缀搜索列表**（仅适用于 Windows Phone 8.1 设备）：每行指定一个 DNS 后缀。 使用短名称连接网站时，将搜索每个 DNS 后缀。  

     例如，假设指定了 DNS 后缀“domain1.contoso.com”和“domain2.contoso.com”，然后转到 URL **http://mywebsite**。 将搜索以下地址：  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  仅适用于 Windows Phone 8.1 设备  
    >   
    >  如果选择了“通过 VPN 连接发送所有网络流量”选项，*且* VPN 连接使用的是完整隧道，那么 VPN 连接会使用第一个设备配置文件自动建立。 若要使用其他配置文件建立连接，请将相应配置文件设置为默认值。  
    >   
    >  如果*未*选择“通过 VPN 连接发送所有网络流量”选项，*且* VPN 连接使用的是隧道分离，那么 VPN 连接会自动针对已配置的路由或连接专用 DNS 后缀进行建立。  


4. 在“创建 VPN 配置文件向导”的“支持的平台”页上，选择将在其中安装 VPN 配置文件的操作系统。也可以选择“全选”，将 VPN 配置文件安装在所有可用的操作系统中。  

5. 完成该向导。 此时，“资产和符合性”工作区中的“VPN 配置文件”节点会显示新建的 VPN 配置文件。  


**部署**：若要详细了解如何部署 VPN 配置文件，请参阅[部署 Wi-Fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

### <a name="next-steps"></a>后续步骤  
 下面的主题可帮助你在 Configuration Manager 中规划、设置、操作和维护 VPN 配置文件。  

-   [System Center Configuration Manager 中 VPN 配置文件的先决条件](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中 VPN 配置文件的安全和隐私](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
