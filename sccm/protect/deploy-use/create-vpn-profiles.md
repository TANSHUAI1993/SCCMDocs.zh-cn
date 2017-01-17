---
title: "如何在 System Center Configuration Manager 中创建 VPN 配置文件 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中创建 VPN 配置文件。"
ms.custom: 
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
author: nbigman
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: f674aa5502e4b3b45d0eda119419863892d72cff


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中创建 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>
> - 有关针对不同设备可用的连接类型，请参阅 [System Center Configuration Manager 中的 VPN 配置文件](../../protect/deploy-use/vpn-profiles.md)。  
> - 对于第三方 VPN 连接，在部署 VPN 配置文件之前分发 VPN 应用。 如果不部署应用，则将在用户尝试连接到 VPN 时提示他们部署应用。 若要了解如何部署应用，请参阅[使用 System Center Configuration Manager 部署应用程序](../../apps/deploy-use/deploy-applications.md)。

### <a name="start-the-create-vpn-profile-wizard"></a>启动“创建 VPN 配置文件向导”  

1.  在 System Center Configuration Manager 控制台中，单击“资产和符合性”。  

2.  在 System Center Configuration Manager 控制台的“资产和符合性”工作区中，依次展开“符合性设置”和“公司资源访问”，然后单击“VPN 配置文件”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建 VPN 配置文件” 。  

### <a name="provide-general-information-about-the-vpn-profile"></a>提供有关 VPN 配置文件的一般信息  

1.  在“创建 VPN 配置文件向导”  的“常规” 页上，指定下列信息：  

    -   “名称” - 输入 VPN 配置文件的唯一名称（最多 256 个字符）。  

        > [!IMPORTANT]  
        >  不要在 VPN 配置文件名称中使用字符 \\/:*?<> | 或空格字符，因为 Windows Server VPN 配置文件不支持这些字符。  

    -   **说明** - 输入说明以帮助查找 System Center Configuration Manager 控制台中的配置文件（最多 256 个字符）。  

    -   **从文件导入现有的 VPN 配置文件项** - 选择此选项以显示“导入 VPN 配置文件”页。 在此页上，你可以导入以前导出到 XML 文件的 VPN 配置文件信息（仅限 Windows 8.1 和 Windows RT 操作系统）。  

### <a name="provide-connection-information-for-the-vpn-profile"></a>提供 VPN 配置文件的连接信息  

1.  在向导的“连接”  页上，指定以下信息：  

    -   **连接类型：** 从下拉列表中选择 VPN 连接的连接类型。 可以从显示支持平台的下表中的连接类型中进行选择。  

        > [!IMPORTANT]  
        >  在可以使用部署到设备的 VPN 配置文件之前，应安装所需的第三方 VPN 应用。 可以使用[如何使用 System Center Configuration Manager 创建应用程序](../../apps/deploy-use/create-applications.md)主题中的信息来帮助你使用 System Center Configuration Manager 部署应用。  

    -   **服务器列表：** 单击“添加”  以添加用于 VPN 连接的新服务器。 根据连接类型，你可以添加一个或多个 VPN 服务器，还可以指定哪个服务器将作为默认服务器。  

        > [!NOTE]  
        >  运行 iOS 的设备不支持使用多个 VPN 服务器。 如果配置多个 VPN 服务器并随后将 VPN 配置文件部署到 iOS 设备，则只会使用默认服务器。  

     下表中的其他选项可能会显示，具体情况视所选的连接类型而定。 请参阅 VPN 服务器文档以了解更多信息。  

    |选项|更多信息|连接类型|  
    |------------|----------------------|---------------------|  
    |**领域**|指定你想要使用的身份验证领域的名称。 身份验证领域是“脉冲安全”连接类型使用的身份验证资源的分组。|脉冲安全|  
    |**角色**|指定有权访问此连接的用户角色的名称。|脉冲安全|  
    |**登录组或域**|指定你想要连接到的登录组或域的名称。|Dell SonicWALL Mobile Connect|  
    |**指纹**|指定一个将用于验证 VPN 服务器是否可以信任的字符串（例如“Contoso Fingerprint Code”）。<br /><br /> 指纹可以：<br /><br /> - 发送到客户端，使其知道在连接时可信任所有提供相同指纹的服务器。<br /><br /> - 如果设备还没有指纹，其将在显示指纹时提示用户信任正连接到的 VPN 服务器（用户手动验证指纹并单击“信任”以连接）。|Check Point Mobile VPN|  
    |**通过 VPN 连接发送所有网络流量**|如果未选择此选项，则可以为连接（针对 **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 和 **L2TP** 连接类型）指定其他路由，这被称为拆分或 VPN 隧道。<br /><br /> 仅将通过 VPN 隧道发送与公司网络的连接。 你连接到 Internet 上的资源时，不会使用 VPN 隧道。|All|  
    |**特定于连接的 DNS 后缀**|（可选）为连接指定特定于连接的域名系统 (DNS) 后缀。|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**连接到公司 Wi-Fi 网络时不使用 VPN**|指定当设备连接到公司 Wi-Fi 网络时将不使用 VPN 连接。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**连接到家庭 Wi-Fi 网络时绕过 VPN**|指定当设备连接到家庭 Wi-Fi 网络时将不使用 VPN 连接。|All|  
    |**每个应用 VPN （iOS 7 及更高版本，Mac OS X 10.9 及更高版本）**|如果你想要将此 VPN 连接与 iOS 应用相关联，以便在运行该应用时打开连接，请选择此选项。 可在部署它时将 VPN 配置文件与应用关联。|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
    |**自定义 XML（可选）**|使你可以指定配置 VPN 连接的自定义 XML 命令。<br /><br /> 例如：<br /><br /> 对于“Pulse Secure”：<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> 对于“CheckPoint Mobile VPN”：<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> 对于“Dell SonicWALL Mobile Connect”：<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> 对于“F5 Edge Client”：<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> 有关如何编写自定义 XML 命令的详细信息，请参阅每个制造商 VPN 文档。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Windows 10 VPN 功能（将 Configuration Manager 与 Intune 配合使用时可用）  


> [!NOTE]  
> 使用 Windows 10 VPN 功能的 VPN 配置文件的名称不能是 Unicode 格式或包含特殊字符。


|选项|更多信息|连接类型|  
|------------|----------------------|---------------------|  
|**连接到公司 Wi-Fi 网络时不使用 VPN**|指定当设备连接到公司 Wi-Fi 网络时将不使用 VPN 连接。 输入将用于确定是否要将设备连接到公司网络的受信任网络名称。|All|  
|**网络通信规则**|设置将为 VPN 连接启用的协议、本地和远程端口及地址范围。<br /><br /> **注意：** 如果你没有创建网络流量规则，则所有协议、端口和地址范围都将启用。 创建规则后，VPN 连接将仅使用该规则或其他规则中指定的协议、端口和地址范围。|All|  
|**路由**|将使用 VPN 连接的路由。 请注意，创建超过 60 个路由可能会导致策略失败。 |All|  
|**DNS 服务器**|建立 VPN 连接后该连接将使用的 DNS 服务器。|All|  
|**自动连接到 VPN 的应用**|可以添加自动使用 VPN 连接的应用或导入这些应用的列表。 应用的类型决定应用标识符。 对于桌面应用，请提供应用的文件路径。 对于通用的应用，请提供包系列名称 (PFN)。 若要了解如何查找应用的 PFN，请参阅[查找每个应用 VPN 的包系列名称](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。 |All|

> [!IMPORTANT]
> 我们建议你保护编译来用于每个应用 VPN 配置的关联应用的所有列表。 如果未经授权的用户修改你的列表，而你将此表导入每个应用 VPN 的应用列表中，则可能会向不应具有访问权限的应用授予 VPN 访问权限。 保护应用列表的一种方法是使用访问控制列表 (ACL)。


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>配置 VPN 配置文件的身份验证方法  

1.  在向导的“身份验证方法”  页上，指定下列信息：  

    -   **身份验证方法：** 从下拉列表中选择 VPN 连接将使用的身份验证方法。 下拉列表中的项可能会有所不同，这些项视你之前选择的连接类型而定。 下表中列出了可用的身份验证方法和支持的连接类型。  

        |身份验证方法|支持的连接类型|  
        |---------------------------|--------------------------------|  
        |**证书**<br /><br /> **注意：** 如果使用客户端证书对 RADIUS 服务器（例如网络策略服务器）进行验证，则证书中的“使用者可选名称”必须设置为“用户主体名称”。|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**用户名和密码**|- <br />                            脉冲安全<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft 受保护的 EAP (PEAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Microsoft 受保护的密码 (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**智能卡或其他证书**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|-  Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** （仅限 iOS）|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**使用计算机证书**|IKEv2|  

         根据你选择的选项，可能需要你指定进一步的信息，如：  

        -   **每次登录时记住用户凭据**：选择此选项以确保记住用户凭据，使用户不必在每次建立连接时输入凭据。  

        -   “选择用于客户端身份验证的客户端证书” - 选择之前创建的客户端 SCEP 证书，它将用于对 VPN 连接进行身份验证。 有关如何在 System Center Configuration Manager 中使用证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](introduction-to-certificate-profiles.md)。  

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

         ![为 VPN 配置条件性访问](../media/vpn-conditional-access.png)


        > [!NOTE]  
        >
        >对于某些身份验证方法，可以单击“配置”来打开 Windows 属性对话框（如果正在运行 System Center Configuration Manager 控制台的 Windows 版本支持此身份验证方法），然后在其中配置身份验证方法的属性。  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>配置 VPN 配置文件的代理设置  

1.  在“创建 VPN 配置文件向导”  的“代理设置” 页上，如果 VPN 连接使用代理服务器，请选中“配置此 VPN 配置文件的代理设置”  复选框。  

2.  指定有关代理服务器及其设置的详细信息。 有关详细信息，请参阅 Windows Server 文档。  

> [!NOTE]  
>  在 Windows 8.1 计算机上，VPN 配置文件将不会显示代理服务器信息，直至使用该计算机连接到 VPN。  


### <a name="configure-further-dns-settings-if-required"></a>进一步配置 DNS 设置（如果需要）  
 在向导的“配置自动 VPN 连接”  页上，可以配置以下设置：  

-   “按需启用 VPN”– 如果想要在 Windows Phone 8.1 设备的此向导页上进一步配置 DNS 设置，请选择此选项。

> [!Note]  
> 此设置仅适用于 Windows Phone 8.1 设备，并且应仅在将要部署到 Windows Phone 8.1 设备的 VPN 配置文件上启用。


-   DNS 后缀列表（仅适用于 Windows Phone 8.1 设备）– 配置将建立 VPN 连接的域。 对于每个你所指定域，添加 DNS 后缀、DNS 服务器地址和以下按需操作之一：  

    -   “从不建立”– 从不会打开 VPN 连接  

    -   “需要时建立”– 仅在设备需要连接到资源时打开 VPN 连接  

    -   “始终建立”– 始终打开 VPN 连接  

-   “合并”– 复制任何配置到“受信任的网络列表”中的 DNS 后缀。  

-   “受信任的网络列表” （仅适用于 Windows Phone 8.1 设备）- 在每一行上指定一个 DNS 后缀。 如果该设备处于受信任的网络中，将不会打开 VPN 连接。  

-   “后缀搜索列表” （仅适用于 Windows Phone 8.1 设备）- 在每一行上指定一个 DNS 后缀。 使用短名称连接到网站时，将搜索你指定的每个 DNS 后缀。  

     例如，你指定了 DNS 后缀“domain1.contoso.com”  和“domain2.contoso.com”  ，然后访问 URL“http://mywebsite” 。 将搜索以下地址：  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  仅适用于 Windows Phone 8.1 设备  
>   
>  如果选择了“通过 VPN 连接发送所有网络流量”  选项，并且 VPN 连接使用完整隧道，则对于设备上配置的第一个配置文件，将自动打开 VPN 连接。 如果希望另一个配置文件自动打开连接，则必须使其成为设备上的默认配置文件。  
>   
>  如果未选择“通过 VPN 连接发送所有网络流量”  选项并且 VPN 连接使用拆分隧道，则在配置路由或连接特定的 DNS 后缀时可以自动打开 VPN 连接。  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>为 VPN 配置文件配置支持的平台  
 支持的平台是指将在其中安装 VPN 配置文件的操作系统。  

在“创建 VPN 配置文件向导”  的“支持的平台” 页上，选择将在其中安装 VPN 配置文件的操作系统，或单击“全选”  以将 VPN 配置文件安装在所有可用的操作系统。  

### <a name="complete-the-wizard"></a>完成向导  
 在向导的“摘要”页面上，查看要执行的操作，然后单击“完成”。 新的 VPN 配置文件将显示在“资产和符合性”  工作区的“VPN 配置文件”  节点中。  

### <a name="next-steps"></a>后续步骤

- 对于第三方 VPN 连接，在部署 VPN 配置文件之前分发 VPN 应用。 如果不部署应用，则将在用户尝试连接到 VPN 时提示他们部署应用。 若要了解如何部署应用，请参阅[使用 System Center Configuration Manager 部署应用程序](../../apps/deploy-use/deploy-applications.md)。

- 部署 VPN 配置文件，如[如何在 System Center Configuration Manager 中部署配置文件](deploy-wifi-vpn-email-cert-profiles.md)中所述。  



<!--HONumber=Dec16_HO3-->


