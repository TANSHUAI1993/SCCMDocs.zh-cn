---
title: "管理来自适用于企业的 Windows 应用商店的应用 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 管理并部署来自适用于企业的 Windows 应用商店的应用"
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理来自适用于企业的 Windows 应用商店的应用

*适用范围：System Center Configuration Manager (Current Branch)*

[适用于企业的 Windows 应用商店](https://www.microsoft.com/business-store)中可以为组织查找并采购 Windows 应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可以同步已使用 Configuration Manager 购买的应用列表，在 Configuration Manager 控制台中查看这些应用，并像部署任何其他应用一样部署它们。


## <a name="online-and-offline-apps"></a>联机和脱机应用

适用于企业的 Windows 应用商店支持两种类型的应用：

- **联机** - 此许可类型要求用户和设备连接到应用商店，以获取应用及其许可。 Windows 10 设备必须已加入 Azure Active Directory 域。
- **脱机** - 组织可以缓存应用和许可，以直接在本地网络部署，而无需连接应用商店或连接 Internet。

[了解更多](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview)适用于企业的 Windows 应用商店的相关信息。

Configuration Manager 支持在运行 Configuration Manager 客户端的 Windows 10 设备上管理适用于企业的 Windows 应用商店的应用，也支持在向 Microsoft Intune 注册的 Windows 10 设备上（称之为混合配置）管理这些应用。 Configuration Manager 对联机和脱机应用提供以下功能。

> [!IMPORTANT]
> 若要使用此功能，Windows 10 设备必须运行 2015 年 11 月（即 1511）版本或更高版本。

|功能|脱机应用|联机应用|
|------------|------------|------------|
|将应用数据同步到 Configuration Manager<br>（每 24 小时同步一次）|是|是|
|从应用商店应用创建 Configuration Manager 应用程序|是|是|
|对应用商店中免费应用的支持|是|是|
|对应用商店中收费应用的支持|否|否|
|支持针对用户或设备集合必需的部署|是|是<sup>1</sup>|
|支持对用户或设备集合可用的部署|是<sup>3</sup>|否<sup>2</sup>|

<sup>1</sup>仅支持由 Intune 管理的设备。 虽然不会阻止你在 Configuration Manager 控制台中创建联机应用程序，并将其部署到 Configuration Manager 客户端管理的设备，但这不会起作用。 会将最终用户定向到应用商店中的相关页，他们必须在其中手动安装应用。

<sup>2</sup>联机应用可部署为只针对 Configuration Manager 客户端管理的设备的用户或设备集合可用，但当最终用户在软件中心选择该应用时，他们将转到适用于企业的 Windows 应用商店，必须在其中手动安装该应用。 不支持对向 Microsoft Intune 注册的设备可用的部署。

<sup>3</sup>对于由 Intune 管理的设备不受支持。

> [!IMPORTANT]
> 在此版本中，如果有一个 Configuration Manager 层次结构包含管理中心站点和至少一个主站点，则将适用于企业的 Windows 应用商店应用部署到 Intune 管理的设备将失败。


## <a name="activate-the-windows-store-for-business-capability"></a>激活适用于企业的 Windows 应用商店功能
由于这是一个预发行功能，因此在能将 Configuration Manager 连接到适用于企业的 Windows 应用商店前，必须执行以下步骤：

**同意使用预发行功能**
1. 在 Configuration Manager 控制台的“管理”工作区中，单击“站点配置” > “站点”。
2. 在层次结构中选择顶层站点，然后打开“层次结构设置”。
3. 在“层次结构设置属性”对话框中，勾选“同意使用预发行功能”。
4. 单击" **确定**"。

**激活适用于企业的 Windows 应用商店功能**
1. 在 Configuration Manager 控制台的“管理”工作区中，单击“云服务” > “更新与服务” > “功能”。
2. 选择“适用于企业的 Windows 应用商店集成”，然后在“主页”选项卡的“功能”组中，单击“开启”。
3. 关闭，然后重新打开 Configuration Manager 控制台。
4. 现在，就可以在“云服务”下的“管理”工作区中看到**适用于企业的 Windows 应用商店**节点。

## <a name="set-up-windows-store-for-business-synchronization"></a>设置适用于企业的 Windows 应用商店同步

**在 Azure Active Directory 中，将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具。这会为你提供以后将需要的客户端 ID。**
1. 在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 Active Directory 节点中，选择 Azure Active Directory，然后单击“应用程序” > “添加”。
2.  单击“添加我的组织正在开发的应用程序”。
3.  为应用程序输入名称，选择“Web 应用程序”和/或“Web API”，然后单击“下一步”箭头。
4.  为**登录 URL**和**应用 ID URI** 输入相同 URL。 该 URL 可以是任何内容，无需解析为实际地址。 例如，可以输入 *https://yourdomain/sccm*。
5.  完成向导。

**在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥**
1.  突出显示刚创建的应用程序，然后单击“配置”。
2.  在“密钥”下，从列表中选择持续时间，然后单击“保存”。 这创建新客户端密钥。 成功将适用于企业的 Windows 应用商店载入到 Configuration Manager 之前，请勿导航离开此页面。

**在适用于企业的 Windows 应用商店中，将 Configuration Manager 配置为存储管理工具**
1.  打开 [https://businessstore.microsoft.com/zh-cn/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，在出现提示时进行登录。
2.  接受使用条款（如果需要）。
3.  在“管理工具”下，单击“添加管理工具”。
4.  在“按名称搜索工具”中，键入以前在 AAD 中创建的应用程序的名称，然后单击“添加”。
5.  在刚导入的应用程序旁单击“激活”。
6.  如果要允许购买脱机许可的应用程序，则在“管理”>“帐户信息”页面，选择“显示脱机许可的应用”。

**将应用商店帐户添加到 Configuration Manager**

1. 确保至少已从适用于企业的 Windows 应用商店购买了一个应用。在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后单击“适用于企业的 Windows 应用商店”。
2.  在“主页”选项卡上的“适用于企业的 Windows 应用商店”组中，单击“添加适用于企业的 Windows 应用商店帐户”。
3.  从 Azure Active Directory 添加租户 ID、客户端 ID 和客户端密钥，然后完成向导。
4. 完成之后，会在 Configuration Manager 控制台中“适用于企业的 Windows 应用商店”列表中看到配置的帐户。


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>从适用于企业的 Windows 应用商店应用创建和部署 Configuration Manager 应用程序。
1.  在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。
2.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，单击“创建应用程序”。
将创建包含适用于企业的 Windows 应用商店应用的 Configuration Manager 应用程序。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。

> [!IMPORTANT]
> 对于向 Intune 注册的设备，已部署的应用仅适用于最初注册该设备的用户。 其他任何用户都无法访问该应用。

## <a name="monitor-windows-store-for-business-apps"></a>监视适用于企业的 Windows 应用商店应用

在“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。

对于所管理的每个应用商店应用，可以查看关于应用的以下信息：名称、平台、拥有的应用许可数量和可用的许可数量。



<!--HONumber=Nov16_HO1-->


