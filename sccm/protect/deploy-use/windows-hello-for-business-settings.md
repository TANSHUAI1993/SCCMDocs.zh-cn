---
title: "Windows Hello 企业版设置 | Microsoft Docs"
description: "了解如何将 Windows Hello 企业版与 System Center Configuration Manager 集成。"
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 1f254ee31bae1c3d7b1506e68c40baf78793bf66


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Windows Hello 企业版设置

*适用范围：System Center Configuration Manager (Current Branch)*

通过 System Center Configuration Manager，可与 Windows Hello 企业版（以前为 Microsoft Passport for Windows）集成，其为 Windows 10 设备的替代登录方法。 Hello 企业版使用 Active Directory 或 Azure Active Directory 帐户来替代密码、智能卡或虚拟智能卡。  

在 Hello 企业版中，可以使用“用户手势”取代密码进行登录。 用户手势可以是简单的 PIN、生物识别身份验证或指纹读取器等外部设备。  

 Configuration Manager 通过两种方式与 Windows Hello 企业版集成：  

-   可以使用 Configuration Manager 来控制用户能够和不能用于登录的手势。  

-   可在 Windows Hello 企业版密钥存储提供程序 (KSP) 中存储身份验证证书。 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

- 可将 Windows Hello 企业版策略部署到运行 Configuration Manager 客户端的已加入域的 Windows 10 设备。 在下面的[在已加入域的 Windows 10 设备上配置 Windows Hello 企业版](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)中介绍了此配置。 搭配使用 Configuration Manager 和 Intune（混合）时，可在 Windows 10 和 Windows 10 移动设备上配置这些设置，但不能在运行 Configuration Manager 客户端的已加入域的设备上进行配置。   

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>配置 Windows Hello 企业版设置（混合）  

1.  在 Configuration Manager 控制台中，单击“管理” > “云服务” > “Microsoft Intune 订阅”。  

3.  从列表中选择你的 Microsoft Intune 订阅，然后在“主页”选项卡的“订阅”组中，单击“配置平台” > “Windows (MDM)”。  

4.  在“Microsoft Intune 订阅属性”对话框的“Windows Hello 企业版”选项卡上，从以下值中选择将影响所有已注册的 Windows 10 和 Windows 10 移动版设备的项：  

    -   **禁用已注册设备上的 Windows Hello 企业版**或**启用已注册设备上的 Windows Hello 企业版** - 启用或禁用所有已注册的 Windows 10 和 Windows 10 移动版设备上的 Windows Hello 企业版。  

    -   **使用受信任的平台模块 (TPM)** - 受信任的平台模块 (TPM) 芯片提供了一层额外的数据安全保障。 选择下列值之一：  

        -   **必须** （默认）- 仅具有可访问 TPM 的设备可预配 Windows Hello 企业版。  

        -   **首选** - 首次尝试使用 TPM 的设备。 如果这不可用，他们可以使用软件加密  

    -   **要求的最小 PIN 长度** - 指定 Windows Hello 企业版 PIN 所需的最小字符数。 必须使用至少 4 个字符（默认值为 6 个字符）。  

    -   **要求的最大 PIN 长度** - 指定 Windows Hello 企业版 PIN 允许的最大字符数。 最多可以使用 127 个字符。  

    -   **要求在 PIN 中使用小写字母** - 指定是否必须在 Windows Hello 企业版 PIN 中使用小写字母。 选择：  

        -   **允许** - 用户可以在其 PIN 中使用小写字母。  

        -   **必须** - 用户必须在其 PIN 中包含至少一个小写字母。  

        -   **不允许** （默认）- 用户不得在其 PIN 中使用小写字母。  

    -   **要求在 PIN 中使用大写字母** - 指定是否必须在 Windows Hello 企业版 PIN 中使用大写字母。 选择：  

        -   **允许** - 用户可以在其 PIN 中使用大写字母。  

        -   **必须** - 用户必须在其 PIN 中包含至少一个大写字母。  

        -   **不允许** （默认）- 用户不得在其 PIN 中使用大写字母。  

    -   **要求含有特殊字符** - 指定 PIN 中使用特殊字符。 选择：  

        -   **允许** - 用户可以在其 PIN 中使用特殊字符。  

        -   **必须** - 用户必须在其 PIN 中包含至少一个特殊字符。  

        -   **不允许** （默认）- 用户必须在其 PIN 中使用特殊字符（这也是不配置此设置时的行为）。  

         特殊字符包括：**! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**。  

    -   **需要 PIN 有效期（天）** - 指定必须更改设备 PIN 前的天数。 默认值为 41 天。  

    -   **防止重用以前的 PIN** - 使用此设置来限制重用以前使用过的 PIN。 默认设置为不能重用最近使用的 5 个 PIN。  

    -   **启用生物识别手势** - 启用如面部识别或指纹等生物识别身份验证作为 Windows Hello 企业版的 PIN 的替代方法。 如果生物识别身份验证失败，则用户仍必须配置工作 PIN。  

         如果设置为“启用”，Windows Hello 企业版则允许生物识别身份验证。  如果设置为“禁用”，Windows Hello 企业版将阻止生物识别身份验证（对于所有帐户类型）。  

    -   **在可用时，使用增强型反欺骗程序** - 配置是否在支持增强型反欺骗程序的设备上使用该程序。  

         如果设置为“已启用” ，则 Windows 将在支持反电子欺骗技术时要求所有用户对面部识别功能使用此技术。  

    -   **使用远程 Passport** - 如果此选项设置为“启用”，则用户可以使用远程 Hello 企业版充当台式计算机身份验证的便携伴侣设备。 台式计算机必须加入 Azure Active Directory，并且伴侣设备必须配置 Windows Hello 企业版 PIN。  

5.  完成后单击“确定” 。  


## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>在已加入域的 Windows 10 设备上配置 Windows Hello 企业版
可以三种方式控制已加入域的 Windows 10 设备上的 Windows Hello 企业版设置：

- 可创建和部署 Windows Hello 企业版配置文件。 此为推荐方法。
- 可使用组策略。  
- 可使用 PowerShell 脚本。

请注意，除此配置外，还必须部署证书配置文件，如[配置证书配置文件](#configure-a-certificate-profile)中所述。

### <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>推荐方法 - 配置 Windows Hello 企业版配置文件  

在管理员控制台的“公司资源访问”下，右键单击“Windows Hello 企业版配置文件”，然后选择“新建”以启动配置文件向导。 提供向导请求的设置，在最终页上查看并确认设置，然后单击“关闭”。 设置的示例可能如下所示：  

![Windows Hello 企业版设置](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>通过 Active Directory 中的组策略配置 Windows Hello 企业版  

可使用 Active Directory 组策略配置已加入域的 Windows 10 设备，以便在用户登录到 Windows 时为其设置 Hello 企业版凭据：

1.  在 Windows Server 计算机上，打开服务器管理器并导航到“工具” > “组策略管理”。    

2.  在“组策略管理”  对话框中，展开你希望在其中启用“自动加入工作区”的域。    

3.  右键单击“组策略对象”，然后单击“新建”。  

4.  在“新建 GPO”对话框中，为新的组策略对象输入名称，例如“启用 Windows Hello 企业版”，然后单击“确定”。  

5.  在“组策略对象”  节点中，右键单击刚创建的对象，然后单击“编辑” 。  

6.  在“组策略管理编辑器”对话框中，导航到“计算机配置” > “策略” > “管理模板” > “Windows 组件” > “Windows Hello 企业版”。  

7.  右键单击“启用 Windows Hello 企业版”，然后单击“编辑”。   

8.  选择“启用” ，单击“应用” ，然后单击“确定” 。

现在即可将刚创建的组策略对象链接到所选位置。 例如：    

   AD 中的特定组织单位 (OU)，其中将放置加入域的 Windows 10 计算机。    

   包含将自动注册到 Azure AD 的加入域的 Windows 10 计算机的特定安全组。    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>通过使用 Configuration Manager 部署 PowerShell 脚本来配置 Windows Hello 企业版    
可使用 Configuration Manager 应用程序管理来创建和部署以下 PowerShell 脚本。    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

有关 Configuration Manager 应用程序管理的详细信息，请参阅 [System Center Configuration Manager 中的应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>配置证书配置文件以便在 Configuration Manager 中注册 Windows Hello 企业版注册证书  
 如果你想使用基于 Windows Hello 企业版证书的登录（或 Microsoft Hello），请进行以下配置：  

-   Configuration Manager 证书配置文件。  

-   在证书配置文件中，选择使用智能卡登录 EKU 的模板。  

 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

### <a name="see-also"></a>另请参阅  
 [使用 System Center Configuration Manager 保护数据和站点基础结构](../../protect/understand/protect-data-and-site-infrastructure.md)

 [使用 Windows Hello 企业版管理身份验证](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)。  



<!--HONumber=Dec16_HO3-->


