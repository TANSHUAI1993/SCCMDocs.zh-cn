---
title: "Windows Hello 企业版设置 | Microsoft Docs"
description: "了解如何将 Windows Hello 企业版与 System Center Configuration Manager 集成。"
ms.custom: na
ms.date: 03/28/2017
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: c9a6842958e6fa3f740caabbaf20aabb9df4e8a8
ms.lasthandoff: 03/27/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Windows Hello 企业版设置

*适用范围：System Center Configuration Manager (Current Branch)*

通过 System Center Configuration Manager，可与 Windows Hello 企业版（以前为 Microsoft Passport for Windows）集成，其为 Windows 10 设备的替代登录方法。 Hello 企业版使用 Active Directory 或 Azure Active Directory 帐户来替代密码、智能卡或虚拟智能卡。  

在 Hello 企业版中，可以使用“用户手势”取代密码进行登录。 用户手势可以是简单的 PIN、生物识别身份验证或指纹读取器等外部设备。  

 Configuration Manager 通过两种方式与 Windows Hello 企业版集成：  

-   可以使用 Configuration Manager 来控制用户能够和不能用于登录的手势。  

-   可在 Windows Hello 企业版密钥存储提供程序 (KSP) 中存储身份验证证书。 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

- 可将 Windows Hello 企业版策略部署到运行 Configuration Manager 客户端的已加入域的 Windows 10 设备。 在下面的[在已加入域的 Windows 10 设备上配置 Windows Hello 企业版](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)中介绍了此配置。 搭配使用 Configuration Manager 和 Intune（混合）时，可在 Windows 10 和 Windows 10 移动设备上配置这些设置，但不能在运行 Configuration Manager 客户端的已加入域的设备上进行配置。 有关详细信息，请参阅[配置 Windows Hello 商业版设置（混合）](../../mdm/deploy-use/windows-hello-for-business-settings.md)。

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>在已加入域的 Windows 10 设备上配置 Windows Hello 企业版
可以三种方式控制已加入域的 Windows 10 设备上的 Windows Hello 企业版设置：

- 可创建和部署 Windows Hello 企业版配置文件。 此为推荐方法。
- 可使用组策略。  
- 可使用 PowerShell 脚本。

请注意，除此配置外，还必须部署证书配置文件，如[配置证书配置文件](#configure-a-certificate-profile)中所述。

## <a name="recommended-approach----configure-a-windows-hello-for-business-profile"></a>推荐方法 - 配置 Windows Hello 企业版配置文件  

在 Configuration Manager 控制台的“公司资源访问”下，右键单击“Windows Hello 企业版配置文件”，然后选择“新建”以启动配置文件向导。 提供向导请求的设置，在最终页上查看并确认设置，然后单击“关闭”。 设置的示例可能如下所示：  

![Windows Hello 企业版设置](../media/Hello-for-Business-settings.png)

## <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>通过 Active Directory 中的组策略配置 Windows Hello 企业版  

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

## <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>通过使用 Configuration Manager 部署 PowerShell 脚本来配置 Windows Hello 企业版    
可使用 Configuration Manager 应用程序管理来创建和部署以下 PowerShell 脚本。    

**powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"** 

有关 Configuration Manager 应用程序管理的详细信息，请参阅 [System Center Configuration Manager 中的应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>配置证书配置文件以便在 Configuration Manager 中注册 Windows Hello 企业版注册证书  
 如果你想使用基于 Windows Hello 企业版证书的登录（或 Microsoft Hello），请进行以下配置：  

-   Configuration Manager 证书配置文件。  

-   在证书配置文件中，选择使用智能卡登录 EKU 的模板。  

-    如果想要在 Windows Hello 企业版密钥容器中存储证书配置文件，而证书配置文件使用智能卡登录 EKU，则必须配置以下密钥注册的权限，以确保证书验证正确。
必须首先创建了**密钥管理**组，并将所有 Configuration Manager 管理点计算机添加为此组的成员。

    1.    以域管理员身份或使用等效的凭据登录到域控制器或管理工作站。
    2.    打开“Active Directory 用户和计算机”。
    3.    从导航窗格中，右键单击你的域名，然后单击“属性”。
    4.    在“*<domain name>* 属性”对话框的“安全”选项卡上，单击“高级”。 如果未显示“安全”选项卡，则从“Active Directory 用户和计算机”的“视图”菜单中打开“高级功能”。
    5.    单击“添加” 。
    6.    在“*<domain name>* 的权限条目”对话框中，单击“选择主体”。
    7.    在“选择用户、计算机、服务帐户或组”对话框中，在“输入要选择的对象名称”文本框中键入“密钥管理”。  单击" **确定**"。
    8.    从“适用于”列表中，选择“后代用户对象”。
    9.    滚动到页面底部并单击“全部清除”。
    10.    在“属性”部分中，选择“读取 msDS-KeyCredentialLink”。
    11.    单击“确定”三次以完成任务。


 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

## <a name="see-also"></a>另请参阅  
 [使用 System Center Configuration Manager 保护数据和站点基础结构](../../protect/understand/protect-data-and-site-infrastructure.md)

 [使用 Windows Hello 企业版管理身份验证](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)。  

