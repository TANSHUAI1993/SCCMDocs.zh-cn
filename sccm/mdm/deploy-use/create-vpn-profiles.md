---
title: VPN 配置文件
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中移动设备上的 VPN 配置文件。
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9409b6cc71ea238755f40baf75e6211c447b547f
ms.sourcegitcommit: 826e9ec385d6a1c1f3aa86ac202883154e0c1285
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2018
ms.locfileid: "37116491"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>System Center Configuration Manager 中移动设备上的 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

使用 Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的移动设备用户。 如果部署这些设置，可以最大限度地减少最终用户在连接公司网络上的资源时需要完成的工作。  

例如，你希望设置所有 iOS 设备来连接到公司网络上的文件共享。 创建具有必需的连接设置的 VPN 配置文件。 然后将此配置文件部署到所有拥有 iOS 设备的用户。 用户能在可用网络的列表中看到 VPN 连接，并可以轻松连接到此网络。  

创建 VPN 配置文件时，可以纳入各种安全设置。 例如，可以为已使用 Configuration Manager 证书配置文件设置的服务器验证和客户端身份验证指定证书。 有关详细信息，请参阅[证书配置文件](../../protect/deploy-use/introduction-to-certificate-profiles.md)。  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>配合使用 Configuration Manager 和 Intune 时的 VPN 配置文件

若要将配置文件部署到 iOS、Android、Windows Phone 和 Windows 8.1 设备，必须在 Microsoft Intune 中注册这些设备。 其他平台上的设备也可以注册到 Intune。 有关如何注册的信息，请参阅[在 Microsoft Intune 中注册设备](/intune/device-enrollment)。 

下表展示了每个设备平台支持的连接类型：  

 |连接类型|iOS 和 macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 桌面和移动版|  
 |---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
 |Cisco AnyConnect|是<sup>1</sup>|是|否|否|否|否|否|
 |Cisco (IPSec)|仅限 iOS|否|否|否|否|否|否|  
 |脉冲安全|是|是|是|否|是|是|是|  
 |F5 Edge Client|是|是|是|否|是|是|是|  
 |Dell SonicWALL Mobile Connect|是|是|是|否|是|是|是|  
 |Check Point Mobile VPN|是|是|是|否|是|是|是|  
 |Microsoft SSL (SSTP)|否|否|是|是|是|否|否|  
 |Microsoft Automatic|否|否|是|是|是|否|是|  
 |IKEv2|是（自定义策略，iOS 9 及更高版本）|否|是|是|是|是|是|  
 |PPTP|是|否|是|是|是|否|是|  
 |L2TP|是|否|是|是|是|否|是 (OMA-URI)|  

<sup>1</sup> 从版本 1802 开始，Cisco AnyConnect 连接类型的使用情况各不相同。<!--1357393-->  
   - 对于以下版本的 VPN 配置文件，请使用“Cisco 旧式 AnyConnect”选项：
       - 带有 Cisco AnyConnect 4.0.5 或更低版本的 iOS
       - 带有 Cisco AnyConnect 任何版本的 macOS
   - 对于以下版本的 VPN 配置文件，请使用“Cisco AnyConnect”选项：
       - 带有 Cisco AnyConnect 4.0.7 或更高版本的 iOS

     > [!Tip]  
     > 适用于 iOS 的 Cisco AnyConnect 4.0.07x 和更高版本作为[预发行功能](/sccm/core/servers/manage/pre-release-features)首次被引入版本 1802。 从[更新 4163547](https://support.microsoft.com/help/4163547) 开始到版本 1802，此功能不再属于预发行功能。  
  
  
> [!Note]  
> 混合 MDM 中的 VPN 配置文件不支持 F5 Access 2018。  


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>将 Configuration Manager 与 Intune 结合使用时可用的 Windows 10 VPN 功能  

以下选项适用于 Windows 10 上的所有连接类型：

- **连接到公司 Wi-Fi 网络时不使用 VPN**：当设备连接到公司 Wi-Fi 网络时，不使用 VPN 连接。 输入用于确定设备是否已连接公司网络的受信任网络名称。  

- **网络流量规则**：设置针对 VPN 连接 要启用的协议、本地端口、远程端口和地址范围。  

     > [!Note]  
     > 如果未创建网络流量规则，则会启用所有协议、端口和地址范围。 创建流量规则后，VPN 连接只会使用此规则或其他规则中指定的协议、端口和地址范围。  
  
- **路由**：使用 VPN 连接的路由。 创建超过 60 个路由可能会导致策略失败。  

- **DNS 服务器**：建立连接后由 VPN 连接使用的 DNS 服务器。  

- **自动连接到 VPN 的应用**：可添加应用或导入自动使用 VPN 连接的应用列表。 应用的类型决定应用标识符。 对于桌面应用，请提供应用的文件路径。 对于通用的应用，请提供包系列名称 (PFN)。 若要了解如何查找应用的 PFN，请参阅[查找每个应用 VPN 的包系列名称](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md)。  

     > [!IMPORTANT]  
     > 保护编译用于每应用 VPN 配置的关联应用的所有列表。 如果未经授权的用户更改你的列表，且你将此表导入每应用 VPN 应用列表中，则可能向不应拥有访问权限的应用授予 VPN 访问权限。 保护应用列表的一种方法是使用访问控制列表 (ACL)。  



## <a name="create-vpn-profiles"></a>创建 VPN 配置文件


1. 在 Configuration Manager 控制台的“资产和符合性”工作区中，依次展开“符合性设置”和“公司资源访问”，然后选择“VPN 配置文件”。 

2. 在功能区中单击“创建 VPN 配置文件”。  

3. 在“常规”页上，指定“名称”，然后选择“VPN 配置文件类型”。   
     > [!NOTE]  
     > 使用 Windows 10 VPN 功能的 VPN 配置文件的名称既不能采用 Unicode 格式，也不能包含特殊字符。


4. 如果“支持的平台”页可用，请为先前指定的 VPN 配置文件类型选择操作系统版本。 选择“全选”以在所有可用的操作系统版本上安装 VPN 配置文件。  

5. 在“连接”页上配置 VPN 连接。 有关这些选项的详细信息，请参阅[创建 VPN 配置文件](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile)中“连接”页上的步骤。  

6.  在“身份验证方法”页上，请指定以下设置：  

    -   **身份验证方法**：选择 VPN 连接使用的身份验证方法。 可用的方法视连接类型而定，如此表中所示。  

        |身份验证方法|支持的&nbsp;连接&nbsp;类型|  
        |---------------------------|--------------------------------|  
        |**证书**<br /><br /> **注意：**<ul><li>如果客户端证书对 RADIUS 服务器（如网络策略服务器）进行身份验证，请将证书中的使用者可选名称设置为用户主体名称。</li><li>对于 Android 部署，请选择 EKU 标识符和证书颁发者指纹哈希值。 否则，用户必须手动选择相应的证书。</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco 旧式 AnyConnect</li><li>脉冲安全</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
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

        -   **选择用于客户端身份验证的客户端证书**：选择之前创建用于对 VPN 连接进行身份验证的客户端 [SCEP 证书](create-pfx-certificate-profiles.md)。   

            > [!NOTE]  
            >  对于 iOS 设备，选择的 SCEP 配置文件在 VPN 配置文件中嵌入。 对于其他平台，可添加适用性规则确保仅在该证书存在或符合要求时才安装 VPN 配置文件。  
            >   
            >  如果指定的 SCEP 证书不符合要求或尚未部署，则不会在设备上安装 VPN 配置文件。
            >  
            >  连接类型为“PPTP”时，运行 iOS 的设备对身份验证方法仅支持“RSA SecurID”和“MSCHAP v2”。 若要避免报告错误，请将单独的 PPTP VPN 配置文件部署到运行 iOS 的设备中。   

        - **条件性访问**  
            - 选择“启用此 VPN 连接的条件性访问”可以确保连接到 VPN 的设备在连接前进行了条件性访问合规性测试。 有关详细信息，请参阅[设备符合性策略](/sccm/protect/deploy-use/device-compliance-policies)。  

            - 选中“启用使用替代证书进行单一登录(SSO)”可以选择除 VPN 身份验证证书以外的其他证书来验证设备符合性。 如果选中此选项，请输入 VPN 客户端应查找的正确证书的“EKU”（以逗号分隔的列表）和“颁发者哈希”。  

         - 对于 **Windows 信息保护**，请输入企业管理的公司标识（通常是组织的主域，例如 *contoso.com*）。 可指定组织拥有的多个域，只需用“|”字符来分隔域即可。 例如，*contoso.com|newcontoso.com*。 有关详细信息，请参阅[通过 Intune 创建和部署 Windows 信息保护应用保护策略](/intune/windows-information-protection-policy-create)。   

         ![创建 VPN 配置文件向导，“身份验证方法”页](media/vpn-conditional-access.png)

         当 Windows 客户端版本支持时，“配置”身份验证方法的选项可用。 此选项将打开 Windows 属性对话框以配置身份验证方法。 如果“配置”遭禁用，请使用其他方法来配置身份验证方法属性。  

3.  在“创建 VPN 配置文件向导”的“代理设置”页上，如果 VPN 连接使用的是代理服务器，请选中“配置此 VPN 配置文件的代理设置”框。 然后提供代理服务器信息。 有关详细信息，请参阅 Windows Server 文档。  

    > [!NOTE]  
    >  在 Windows 8.1 计算机上，只有在使用此计算机连接 VPN 之后，VPN 配置文件才会显示代理信息。  


4. 如有必要，请进一步配置 DNS 设置。  

5. 完成该向导。 此时，“资产和符合性”工作区中的“VPN 配置文件”节点会显示新建的 VPN 配置文件。  



## <a name="next-steps"></a>后续步骤  
有关如何部署 VPN 配置文件的详细信息，请参阅[配置 Wi-Fi、VPN、电子邮件和证书配置文件](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)。

 使用以下文章来帮助你规划、设置、操作和维护 VPN 配置文件：  

-   [VPN 配置文件的先决条件](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [VPN 配置文件的安全和隐私](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
