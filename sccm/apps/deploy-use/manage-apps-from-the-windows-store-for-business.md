---
title: "管理来自适用于企业的 Windows 应用商店的应用 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理并部署来自适用于企业的 Windows 应用商店的应用"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f955b5aadfc617e08d5d933dee8e42de838f83c0
ms.openlocfilehash: bf2937f5ba86db19d9cb40e2c98cbb8ba365f7eb

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理来自适用于企业的 Windows 应用商店的应用

*适用范围：System Center Configuration Manager (Current Branch)*

在[适用于企业的 Windows 应用商店](https://www.microsoft.com/business-store)中可以为组织查找并采购 Windows 应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可以同步使用 Configuration Manager 购买的应用列表，在 Configuration Manager 控制台中查看这些应用，并像部署任何其他应用一样部署它们。


## <a name="online-and-offline-apps"></a>联机和脱机应用

适用于企业的 Windows 应用商店支持两种类型的应用：

- **联机** - 此许可类型要求用户和设备连接到应用商店，以获取应用及其许可证。 Windows 10 设备必须已加入 Azure Active Directory 域。
- **脱机** - 组织可以缓存应用和许可证，以直接在本地网络部署而无需连接到应用商店或 Internet。

阅读更多有关[适用于企业的 Windows 应用商店](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview)的信息。

Configuration Manager 支持在运行 Configuration Manager 客户端的 Windows 10 设备和已注册 Microsoft Intune（混合配置）的 Windows 10 设备上管理适用于企业的 Windows 应用商店的应用。 Configuration Manager 对联机和脱机应用提供以下功能。

> [!IMPORTANT]
> 若要使用这些功能，Windows 10 设备必须运行 2015 年 11 月（即 1511）版本或更高版本。

|功能|脱机应用|联机应用|
|------------|------------|------------|
|将应用数据同步到 Configuration Manager<br>（每隔 24 小时同步一次或启动即时同步）|是|是|
|从应用商店应用创建 Configuration Manager 应用程序|是|是|
|对应用商店中免费应用的支持|是|是<sup>1</sup>|
|对应用商店中收费应用的支持|否|是<sup>1</sup>|
|支持针对用户或设备集合必需的部署|是|是<sup>1</sup>|
|支持对用户或设备集合可用的部署|是<sup>2</sup>|否|

<sup>1</sup>仅支持由 Intune 管理的设备。 虽然不会阻止你在 Configuration Manager 控制台中创建联机应用程序和将其部署到 Configuration Manager 客户端管理的设备，但部署不会起作用。 会将用户定向到应用商店中的相关页以便手动安装应用。

<sup>2</sup>仅支持由 Configuration Manager 客户端管理的设备。

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>设置适用于企业的 Windows 应用商店同步

> [!IMPORTANT]
> 在 Configuration Manager和适用于企业的 Windows 应用商店之间设置连接时，必须提供保存从应用商店同步的应用内容的文件夹。
若要确保此文件夹是安全的且可将其内容部署到设备，请确保以下权限就位：
-    安装服务连接点站点系统角色（层次结构中的顶级站点）的计算机必须具有使用 **Computer$** 帐户时指定的文件夹的读取和写入权限。
-    应用作者必须具有所指定文件夹的读取权限。
-    托管 SMS 提供程序实例的每台计算机的 **Computer$** 帐户必须能够使用所指定的文件夹。


在 Azure Active Directory 中，将 Configuration Manager 注册为 Web 应用程序或 Web API 管理工具。 这会为你提供以后将需要的客户端 ID。
1. 在 Active Directory 节点 [https://manage.windowsazure.com](https://manage.windowsazure.com) 中，选择“应用程序”“添加” > 。
2.  选择“添加我的组织正在开发的应用程序”。
3.  为应用程序输入名称，选择“Web 应用程序”和/或“Web API”，然后选择“下一步”。
4.  为**登录 URL**和**应用 ID URI** 输入相同 URL。 该 URL 可以是任何内容，无需解析为实际地址。 例如，可以输入 *https://yourdomain/sccm*。
5.  完成该向导。

在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。
1.  突出显示刚创建的应用程序，然后选择“配置”。
2.  在“密钥”下，从列表中选择持续时间，然后选择“保存”。 这创建新客户端密钥。 成功将适用于企业的 Windows 应用商店载入到 Configuration Manager 之前，请勿离开此页面。

在适用于企业的 Windows 应用商店中，将 Configuration Manager 设置为应用商店管理工具。
1.  打开 [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，在出现提示时进行登录。
2.  接受使用条款（如果需要）。
3.  在“管理工具”下，选择“添加管理工具”。
4.  在“按名称搜索工具”中，键入以前在 Azure Active Directory 中创建的应用程序的名称，然后选择“添加”。
5.  选择刚导入的应用程序旁边的“激活”。
6.  如果要允许购买脱机许可的应用程序，则在“管理”>“帐户信息”页面上选择“显示脱机许可的应用”。

> [!Note]
> 在以前，如果使用多个管理工具部署 Windows 商业应用商店的应用，只能将其中一种工具关联到 Windows 商业应用商店。 现在可将多种管理工具与该应用商店关联，例如 Intune 和 Configuration Manager。

将应用商店帐户添加到 Configuration Manager。

1. 请确保已从适用于企业的 Windows 应用商店购买至少一个应用。 在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后选择“适用于企业的 Windows 应用商店”。
2.  在“主页”选项卡的“适用于企业的 Windows 应用商店”组中，选择“添加适用于企业的 Windows 应用商店帐户”。
3.  从 Azure Active Directory 添加租户 ID、客户端 ID 和客户端密钥，然后完成向导。
4. 完成之后，会在 Configuration Manager 控制台的“适用于企业的 Windows 应用商店”列表中看到设置的帐户。

更改将在供用户下载的应用程序目录中显示的应用语言。

1.    在 Configuration Manager 控制台的“管理”工作区中，选择“云服务” > “更新和维护服务” > “适用于企业的 Windows 应用商店”。
2.    选择适用于企业的 Windows 应用商店的帐户，然后选择“属性”。
3.    选择“语言”选项卡。
4.    添加或删除应用程序目录中将显示的语言。 选择可供用户使用的默认应用程序目录语言。

>[!IMPORTANT]
>在此版本中，如果要更改将进行同步的语言，必须先重启站点服务器上的 SMS Executive 服务，语言设置才会生效。


修改 Azure Active Directory 中的客户端密钥。

1.    在 Configuration Manager 控制台的“管理”工作区中，选择“云服务” > “更新和维护服务” > “适用于企业的 Windows 应用商店”。
2.    选择适用于企业的 Windows 应用商店的帐户，然后选择“属性”。
3.    在“适用于企业的 Windows 应用商店的帐户属性”对话框中的“客户端密钥”字段中输入新的密钥，然后选择“验证”。 验证后，选择“应用”，然后关闭此对话框。

## <a name="sync-apps-from-the-store-with-configuration-manager"></a>使用 Configuration Manager 同步应用商店中的应用

每隔 24 小时同步一次，或使用以下过程启动即时同步：

1. 在 Configuration Manager 控制台的“管理”工作区中，选择“云服务” > “更新和维护服务” > “适用于企业的 Windows 应用商店”。
3.    在“主页”选项卡的“同步”组中，选择“立即同步”。
4.    购买的应用将出现在“应用程序管理”工作区的“应用商店应用的许可证信息”节点中。


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>从适用于企业的 Windows 应用商店应用创建和部署 Configuration Manager 应用程序

此过程假定至少已获得一个免费的应用，或从适用于企业的 Windows 应用商店购买了一个在线支付的许可应用。

1.  在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后选择“应用商店应用的许可证信息”。
2.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，选择“创建应用程序”。
将创建包含适用于企业的 Windows 应用商店应用的 Configuration Manager 应用程序。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。

> [!IMPORTANT]
> 对于向 Intune 注册的设备，已部署的应用仅适用于最初注册该设备的用户。 其他用户不能使用该应用。

## <a name="monitor-windows-store-for-business-apps"></a>监视适用于企业的 Windows 应用商店应用

在“软件库”工作区中，展开“应用程序管理”，然后选择“应用商店应用的许可证信息”。

对于所管理的每个应用商店应用，可以查看关于应用的以下信息：名称、平台、所拥有应用的许可证数量和可用的许可证数量。



<!--HONumber=Feb17_HO3-->


