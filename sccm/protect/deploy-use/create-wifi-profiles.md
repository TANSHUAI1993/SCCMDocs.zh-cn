---
title: "如何创建 Wi-Fi 配置文件 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中使用 Wi-Fi 配置文件为组织中的用户部署无线网络设置。"
ms.custom: na
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f1ae976899de1fd3efcbde0c7268f071a5d0218b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-wi-fi-profiles"></a>创建 Wi-Fi 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*


在 System Center Configuration Manager 中使用 Wi-Fi 配置文件将无线网络设置部署到组织中的用户。 通过部署这些设置，可以让用户很方便地连接到 Wi-Fi。  

 例如，你有一个 Wi-Fi 网络并想让所有 iOS 设备都能够连接到该网络。 创建 Wi-Fi 配置文件，其中包含连接到无线网络所必需的设置。 然后，将该配置文件部署到在层次结构中拥有 iOS 设备的所有用户。 IOS 设备的用户可以在无线网络列表中看到公司网络，并且可以容易地连接到此网络。  

 你可以使用 Wi-fi 配置文件配置下列设备类型：  

-   运行 Windows 8.1 (32 位) 的设备  

-   运行 Windows 8.1 (64 位) 的设备  

-   运行 Windows RT 8.1 的设备  

-   运行 Windows 10 桌面或移动版的设备  

如需深入了解如何在 System Center Configuration Manager 中使用 Wi-Fi 配置文件将无线网络设置部署到移动设备用户，请参阅[针对移动设备创建 Wi-Fi 配置文件](../../mdm/deploy-use/create-wifi-profiles.md)。

> [!IMPORTANT]  
>  若要将配置文件部署到 Android、iOS、Windows Phone 和注册的 Windows 8.1 或更高版本设备，这些设备必须在 Microsoft Intune 中注册。 有关如何注册设备的信息，请参阅[在 Intune 中注册设备以进行管理](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。  

 在创建 Wi-Fi 配置文件时，你可以纳入各种各样的安全设置。 其中包括已通过使用 Configuration Manager 证书配置文件推送的服务器验证和客户端身份验证证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](introduction-to-certificate-profiles.md)。  

## <a name="create-a-wi-fi-profile"></a>创建 Wi-Fi 配置文件  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” > “符合性设置” >  “公司资源访问” > “Wi-Fi 配置文件”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建 Wi-Fi 配置文件”。  

1.  在“常规”页中，为 Wi-Fi 配置文件输入唯一名称和说明。  如果想要使用另一个 Wi-fi 配置文件中的设置，请选择“从文件中导入现有的 Wi-fi 配置文件项”。  

    > [!IMPORTANT]  
    >  确保导入的 Wi-fi 配置文件包含 Wi-fi 配置文件的有效 XML。 导入文件时，Configuration Manager 不会验证该配置文件。  

3.  在**报表的不符合性严重程度**中，指定在客户端设备上发现 Wi-Fi 配置文件不符合（例如，配置文件安装失败）时报告的严重性级别。 可用的严重性级别如下：  

    -   **无**：对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  

    -   **信息**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**信息**。  

    -   **警告**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**警告**。  

    -   **严重**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。  

    -   **事件严重**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。 应用程序事件日志中也会以 Windows 事件的形式记录此严重性级别。  

1.  在“Wi-Fi 配置文件”页，提供设备会将其显示为网络名称的名称。  

    > [!IMPORTANT]  
    >  Configuration Manager 不支持在网络名称中使用单引号 (**â€˜**) 或逗号 (**,**) 字符。  

2.  指定区分大小写的 **SSID**
3.  选择其他适当的连接选项，包括：   如果有可能隐藏了 SSID，则**在网络未广播其名称 (SSID) 时连接**  

4.  在“安全配置”选择无线网络使用的安全协议；如果网络无安全保护，则选择“无身份验证(开放式)”。
    > [!IMPORTANT]  
    >  如果你正在为本地移动设备管理创建 Wi-Fi 配置文件，Configuration Manager 的 Current Branch 仅支持以下 Wi-Fi 安全性配置：  
    >   
    >  安全类型：“WPA2 企业”  或“WPA2 个人”   
    > 加密类型：“AES”  或“TKIP”   
    > EAP 类型：“智能卡或其他证书”  或“PEAP”   

    > 仅限 Android 设备，不支持安全类型“WPA – 个人”、“WPA2 – 个人”和“WEP”。  

2.  选择无线网络使用的加密方法。  

3.  选择用于向无线网络进行验证的 EAP 类型。  

     仅限 Windows Phone 设备：不支持 EAP 类型“LEAP”  和“EAP-FAST”  。  

4.  单击“配置”  ，为所选的 EAP 类型指定属性。 对于某些所选的 EAP 类型，此选项可能不可用。  

    > [!IMPORTANT]  
    >  单击“配置” 时，打开的对话框是 Windows 对话框。 因此，必须确保运行 Configuration Manager 控制台的计算机的操作系统支持配置所选的 EAP 类型。  
    >   
    >  对于 iOS 设备，如果你选择非 EAP 方法用于身份验证，那么无论你选择何种方法，都将使用 MS-CHAP v2 进行连接。  

5.  如果你想要存储用户凭据，以便用户无需在每次登录时输入凭据，请选择“在每次登录时记住用户凭据” 。  

6. **仅适用于 iOS 设备：**  
 配置 Wi-Fi 连接所需的任何证书的信息。 必须配置客户端证书以及受信任的服务器证书名称或根证书，如下所示：  

    -   **受信任的服务器证书名称**：如果设备连接到的服务器使用服务器身份验证证书来识别服务器并帮助保护信道的安全，请在该证书的使用者名称或使用者备用名称中输入一个或多个名称。 名称通常为服务器完全限制的域名。 例如，服务器证书在证书使用者中具有公用名 srv1.contoso.com，则输入“srv1.contoso.com” 。 如果服务器证书具有多个在使用者可选名称中指定的名称，请输入每个名称，以分号分隔。  

    > [!TIP]  
    >  如果将使用你为 iOS 设备 EAP 或客户端身份验证选择的客户端证书来向远程身份验证拨入用户服务 (RADIUS) 服务器（例如正在运行网络策略服务器的服务器）进行验证，则你必须将使用者可选名称设置为用户主体名称。  

    -   “选择用于服务器验证的根证书”：如果设备连接到的服务器使用设备不信任的服务器身份验证证书，请选择包含服务器证书的根证书的证书配置文件，以在设备上创建证书信任链。  

    -   **选择用于客户端身份验证的客户端证书**：如果服务器或网络设备需要客户端证书来验证连接设备，请选择包含客户端身份验证证书的证书配置文件。  

    > [!NOTE]  
    >  必须首先以证书配置文件的形式配置和部署根证书和客户端证书，然后你才能选择这些证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](introduction-to-certificate-profiles.md)。  

7.  在“高级设置”页上，指定 Wi-Fi 配置文件的高级设置，例如身份验证模式、单一登录选项以及（美国）联邦信息处理标准符合性。 有关这些选项的详细信息，请参阅 Windows 文档。 高级设置可能不可用或可能会有所不同，具体情况视你在向导的“安全性配置”  页上所选的选项而定。  

1.  在“代理设置”页上，如果无线网络使用代理服务器，请选择“配置此 Wi-Fi 配置文件的代理设置”，然后提供配置信息。  

2. 在“支持的平台”页上，选择将在其中安装 Wi-Fi 配置文件的操作系统。 或者单击“全选”  以将 Wi-Fi 配置文件安装到所有可用的操作系统。  

### <a name="next-steps"></a>后续步骤
 有关如何部署 Wi-Fi 配置文件的信息，请参阅[如何在 System Center Configuration Manager 中部署 Wi-Fi 配置文件](deploy-wifi-vpn-email-cert-profiles.md)。  
