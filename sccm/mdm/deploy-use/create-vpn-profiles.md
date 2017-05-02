---
title: "System Center Configuration Manager 中的 VPN 配置文件 | Microsoft Docs"
description: "System Center Configuration Manager 中移动设备上的 VPN 配置文件。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 699b79b68440b61904a9053e5004318a2a248bfd
ms.openlocfilehash: 8adc41a30bf12a91a272029db49e50ba003d3e9c
ms.lasthandoff: 04/25/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>System Center Configuration Manager 中移动设备上的 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

使用 System Center Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的移动设备用户。 通过部署这些设置，你可以最大限度减少最终用户连接到公司网络资源需要进行的工作。  

 例如，你想要用连接到公司网络上的文件共享所需的设置来设置所有运行 IOS 操作系统的设备。 你可以创建一个 VPN 配置文件，在其中包含连接到公司网络所需的设置，然后将此配置文件部署到你的层次结构中使用运行 IOS 的设备的所有用户。 IOS 设备用户可在可用网络列表中看到 VPN 连接，并可通过最少量的工作连接到此网络。  

 在创建 VPN 配置文件时，你可以纳入各种各样的安全设置，其中包括已通过使用 System Center Configuration Manager 证书配置文件预配的服务器验证和客户端身份验证证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)。  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>配合使用 Configuration Manager 和 Intune 时的 VPN 配置文件

 若要将配置文件部署到 iOS、Android、Windows Phone 和 Windows 8.1 设备，必须将这些设备注册到 Microsoft Intune。 其他平台上的设备也可以注册到 Intune。 有关如何注册的信息，请参阅[使用 Microsoft Intune 管理移动设备](https://technet.microsoft.com/en-us/library/dn646962.aspx)。 下表显示了每个设备平台支持的连接类型：  

 |连接类型|iOS 和 Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 桌面和移动版|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|是|是|否|否|否|否|是 (OMA-URI)|  
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
有关创建 VPN 配置文件的一般信息，请参阅[如何在 System Center Configuration Manager 中创建 VPN 配置文件](../../protect/deploy-use/create-vpn-profiles.md)。

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Windows 10 VPN 功能（将 Configuration Manager 与 Intune 配合使用时可用）  


> [!NOTE]  
> 使用 Windows 10 VPN 功能的 VPN 配置文件的名称不能是 Unicode 格式或包含特殊字符。


|选项|更多信息|连接类型|  
    |------------|----------------------|---------------------|  
    |**连接到公司 Wi-Fi 网络时不使用 VPN**|设备连接到公司 Wi-Fi 网络时，将不使用 VPN 连接。 输入受信任的网络名称，用于确定是否要将设备连接到公司网络。|All|  
    |**网络通信规则**|设置将为 VPN 连接启用的协议、本地和远程端口及地址范围。<br /><br /> **注意：** 如果你没有创建网络流量规则，则所有协议、端口和地址范围都将启用。 创建规则后，VPN 连接将仅使用该规则或其他规则中指定的协议、端口和地址范围。|All|  
    |**路由**|将使用 VPN 连接的路由。 请注意，创建超过 60 个路由可能会导致策略失败。 |All|  
    |**DNS 服务器**|建立 VPN 连接后该连接将使用的 DNS 服务器。|All|  
    |**自动连接到 VPN 的应用**|可以添加自动使用 VPN 连接的应用或导入这些应用的列表。 应用的类型决定应用标识符。 对于桌面应用，请提供应用的文件路径。 对于通用的应用，请提供包系列名称 (PFN)。 若要了解如何查找应用的 PFN，请参阅[查找每个应用 VPN 的包系列名称](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。 |All|

> [!IMPORTANT]
> 我们建议你保护编译来用于每个应用 VPN 配置的关联应用的所有列表。 如果未经授权的用户修改你的列表，而你将此表导入每个应用 VPN 的应用列表中，则可能会向不应具有访问权限的应用授予 VPN 访问权限。 保护应用列表的一种方法是使用访问控制列表 (ACL)。


1.  在向导的“身份验证方法”页上，指定下列信息：  

    -   **身份验证方法**：选择 VPN 连接将使用的身份验证方法。 可用的方法视连接类型而定，如此表中所示。  

        |身份验证方法|支持的&nbsp;连接&nbsp;类型|  
        |---------------------------|--------------------------------|  
        |**证书**<br /><br /> **注意：**<br />- 如果客户端证书对 RADIUS 服务器（例如网络策略服务器）进行身份验证，则证书中的使用者可选名称必须设置为用户主体名称。<br/><br />- 对于 Android 部署，选择 EKU 标识符和证书颁发者指纹哈希值。  否则，用户必须手动选择相应的证书。  |- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**用户名和密码**|- Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft 受保护的 EAP (PEAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Microsoft 受保护的密码 (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**智能卡或其他证书**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|-  Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** （仅限 iOS）|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**使用计算机证书**|IKEv2|  

         根据你选择的选项，可能需要你指定进一步的信息，如：  

        -   **每次登录时记住用户凭据**：记住用户凭据，这样用户不必在每次连接时都输入凭据。  

        -   **选择用于客户端身份验证的客户端证书** - 选择之前创建的客户端 [SCEP 证书](create-pfx-certificate-profiles.md)，它将用于对 VPN 连接进行身份验证。   

            > [!NOTE]  
            >  对于 iOS 设备，所选择的 SCEP 配置文件将嵌入 VPN 配置文件中。 对于其他平台，将添加适用性规则以确保如果该证书不存在或不符合要求，不会安装 VPN 配置文件。  
            >   
            >  如果所指定的 SCEP 证书不符合或尚未进行部署，则 VPN 配置文件将不会安装到设备上。
            >  
            >  连接类型为“PPTP”时，运行 iOS 的设备对身份验证方法仅支持“RSA SecurID”和“MSCHAP v2”。 若要避免报告错误，请将单独的 PPTP VPN 配置文件部署到运行 iOS 的设备中。  

        - **条件性访问**
            - 选择“启用此 VPN 连接的条件性访问”可以确保连接到 VPN 的设备在连接前进行了条件性访问合规性测试。 [System Center Configuration Manager 中的设备合规性策略](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)中介绍了合规性策略
            - 选择“启用使用替代证书进行单一登录(SSO)”可以选择除设备合规性 VPN 身份验证证书以外的证书。 如果选择此选项，对于 VPN 客户端应查找的正确证书，请提供 **EKU**（以逗号分隔的列表）和**颁发者哈希**。

         - **Windows 信息保护** - 提供企业管理的公司标识，该标识通常是组织的主域，例如 *contoso.com*。 采用“|”字符将域分隔可以指定组织拥有的多个域。 例如，*contoso.com|newcontoso.com*。   
              有关 Windows 信息保护的信息，请参阅[使用 Microsoft Intune 创建 Windows 信息保护 (WIP) 策略](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune)。   

         ![为 VPN 配置条件性访问](media/vpn-conditional-access.png)

         受运行 Configuration Manager 的 Windows 版本和所选的授权方法支持时，可以单击“配置”打开“Windows 属性”对话框并配置身份验证方法属性。  如果禁用“配置”，请使用备选方法配置身份验证方法属性。

2.  在“创建 VPN 配置文件向导”  的“代理设置” 页上，如果 VPN 连接使用代理服务器，请选中“配置此 VPN 配置文件的代理设置”  复选框。 然后提供代理服务器信息。 有关详细信息，请参阅 Windows Server 文档。  

    > [!NOTE]  
    >  在 Windows 8.1 计算机上，VPN 配置文件将不会显示代理服务器信息，直至使用该计算机连接到 VPN。  


3. 进一步配置 DNS 设置（如果需要）  
 在“配置自动 VPN 连接”页上，可以配置以下内容：  

    -   **按需启用 VPN**：如果想要进一步配置 Windows Phone 8.1 设备的 DNS 设置，请使用此选项。 此设置仅适用于 Windows Phone 8.1 设备，并且只能在将要部署到 Windows Phone 8.1 设备的 VPN 配置文件上启用。

    -   DNS 后缀列表（仅适用于 Windows Phone 8.1 设备）- 配置将建立 VPN 连接的域。 对于每个你所指定域，添加 DNS 后缀、DNS 服务器地址和以下按需操作之一：  

        -   “从不建立”– 从不会打开 VPN 连接  

        -   “需要时建立”– 仅在设备需要连接到资源时打开 VPN 连接  

        -   “始终建立”– 始终打开 VPN 连接  

    -   “合并”– 复制任何配置到“受信任的网络列表”中的 DNS 后缀。  

    -   **受信任的网络列表**（仅适用于 Windows Phone 8.1 设备）- 在每一行上指定一个 DNS 后缀。 如果该设备处于受信任的网络中，将不会打开 VPN 连接。  

    -   **后缀搜索列表**（仅适用于 Windows Phone 8.1 设备）- 在每一行上指定一个 DNS 后缀。 使用短名称连接到网站时，将搜索每个 DNS 后缀。  

     例如，你指定了 DNS 后缀“domain1.contoso.com”  和“domain2.contoso.com”  ，然后访问 URL“http://mywebsite” 。 将搜索以下地址：  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  仅适用于 Windows Phone 8.1 设备  
    >   
    >  如果选择了“通过 VPN 连接发送所有网络流量”  选项，并且 VPN 连接使用完整隧道，则对于设备上配置的第一个配置文件，将自动打开 VPN 连接。 如果希望另一个配置文件自动打开连接，则必须使其成为设备上的默认配置文件。  
    >   
    >  如果未选择“通过 VPN 连接发送所有网络流量”  选项并且 VPN 连接使用拆分隧道，则在配置路由或连接特定的 DNS 后缀时可以自动打开 VPN 连接。  


4. 在“创建 VPN 配置文件向导”  的“支持的平台” 页上，选择将在其中安装 VPN 配置文件的操作系统，或单击“全选”  以将 VPN 配置文件安装在所有可用的操作系统。  

5. 完成向导。 新的 VPN 配置文件将显示在“资产和符合性”  工作区的“VPN 配置文件”  节点中。  


**部署：**有关部署 VPN 配置文件的信息，请参阅[部署 Wi-Fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

### <a name="next-steps"></a>后续步骤  
 可以使用下列主题来规划、配置、操作和维护 Configuration Manager 中的 VPN 配置文件。  

-   [System Center Configuration Manager 中 VPN 配置文件的先决条件](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中 VPN 配置文件的安全和隐私](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

