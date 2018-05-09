---
title: Windows Hello 企业版设置
titleSuffix: Configuration Manager
description: 了解如何将 Windows Hello 企业版与 System Center Configuration Manager 集成。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60dcf98b83fb4650a10e5503d42b9f49d3aba359
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Windows Hello 企业版设置

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1245704-->
通过 System Center Configuration Manager，可与 Windows Hello 企业版（以前为 Microsoft Passport for Windows）集成，其为 Windows 10 设备的替代登录方法。 Hello 企业版使用 Active Directory 或 Azure Active Directory 帐户来替代密码、智能卡或虚拟智能卡。  

在 Hello 企业版中，可以使用“用户手势”取代密码进行登录。 用户手势可以是简单的 PIN、生物识别身份验证或指纹读取器等外部设备。

有关详细信息，请参阅 [Windows Hello 企业版](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)。


> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


 Configuration Manager 通过两种方式与 Windows Hello 企业版集成：  

-   可以使用 Configuration Manager 来控制用户能够和不能用于登录的手势。  

-   可在 Windows Hello 企业版密钥存储提供程序 (KSP) 中存储身份验证证书。 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

- 可将 Windows Hello 企业版策略部署到运行 Configuration Manager 客户端的已加入域的 Windows 10 设备。 [在已加入域的 Windows 10 设备上配置 Windows Hello 企业版](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)部分介绍了此配置。 结合使用 Configuration Manager 与 Microsoft Intune（混合）时，可以在 Windows 10 设备和 Windows 10 移动版设备上配置这些设置。 有关详细信息，请参阅[配置 Windows Hello 企业版设置（混合）](../../mdm/deploy-use/windows-hello-for-business-settings.md)。

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>在已加入域的 Windows 10 设备上配置 Windows Hello 企业版
可以创建和部署 Windows Hello 企业版配置文件，控制域加入 Windows 10 设备上的 Windows Hello 企业版设置。 建议使用此方法。


如果使用的是基于证书的身份验证，还必须部署证书配置文件，如[配置证书配置文件](#configure-a-certificate-profile)中所述。 如果使用的是基于密钥的身份验证，无需部署证书配置文件。

## <a name="configure-a-windows-hello-for-business-profile"></a>配置 Windows Hello for Business 配置文件  

在 Configuration Manager 控制台的“公司资源访问”下，右键单击“Windows Hello 企业版配置文件”，然后选择“新建”以启动配置文件向导。 提供向导请求的设置，在最终页上查看并确认设置，然后单击“关闭”。 设置的示例可能如下所示：  

![Windows Hello 企业版策略向导，显示可用设置列表](../media/Hello-for-Business-settings.png)

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>配置证书配置文件以便在 Configuration Manager 中注册 Windows Hello 企业版注册证书  
 若要使用基于 Windows Hello 企业版证书的登录，请配置下列组件：  

-   Configuration Manager 证书配置文件。  

-   在证书配置文件中，选择使用智能卡登录 EKU 的模板。  

-   如果想要在 Windows Hello 企业版密钥容器中存储证书配置文件，而证书配置文件使用智能卡登录 EKU，则必须配置以下密钥注册的权限，以确保证书验证正确。
必须首先创建了**密钥管理**组，并将所有 Configuration Manager 管理点计算机添加为此组的成员。

一些配置可能不需要配置权限，或可能需要进一步配置。 请参阅下表，获取更多帮助：

|Windows 客户端版本|Configuration Manager 1602 或 1606|Configuration Manager 1610|Configuration Manager 1702 或更高版本|
|-|-|-|-|
|Windows 10 周年更新|无需修补程序<br><br>无需权限<br><br>无需 Windows 架构更新|无需修补程序（见“警告”）<br><br>无需权限<br><br>无需 Windows 架构更新|配置权限<br><br>将 Windows Server 2016 架构应用于 Active Directory|
|Windows 10 创意者更新或更高版本|不支持|安装[此修补程序](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>配置权限<br><br>将 Windows Server 2016 架构应用于 Active Directory|配置权限<br><br>将 Windows Server 2016 架构应用于 Active Directory|

> [!WARNING]
> 虽然 Configuration Manager 1610 和 Windows 10 周年更新并不需要[修补程序](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)，但仍可以安装。  如果安装了修补程序，需要配置权限，并将 Windows Server 2016 架构应用于 Active Directory。

## <a name="to-configure-permissions"></a>配置权限的具体步骤

1.  以域管理员身份或使用等效的凭据登录到域控制器或管理工作站。
2.  打开“Active Directory 用户和计算机”。
3.  从导航窗格中，右键单击你的域名，然后单击“属性”。
4.  在“*<domain name>* 属性”对话框的“安全”选项卡上，单击“高级”。 如果未显示“安全”选项卡，则从“Active Directory 用户和计算机”的“视图”菜单中打开“高级功能”。
5.  单击“添加” 。
6.  在“*<domain name>* 的权限条目”对话框中，单击“选择主体”。
7.  在“选择用户、计算机、服务帐户或组”对话框中，在“输入要选择的对象名称”文本框中键入“密钥管理”。 单击" **确定**"。
8.  从“适用于”列表中，选择“后代用户对象”。
9.  滚动到页面底部并单击“全部清除”。
10. 在“属性”部分中，选择“读取 msDS-KeyCredentialLink”。
11. 单击“确定”三次以完成任务。


## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  




