---
title: 管理来自适用于企业的 Microsoft Store 的应用
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager 管理并部署来自适用于企业的 Microsoft Store 的应用。
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4999784140ece9df49a28063e8660566f7206df0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336113"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理来自适用于企业的 Microsoft Store 的应用
在[适用于企业的 Microsoft Store](https://www.microsoft.com/business-store) 中可以为组织查找和购买 Windows 应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可以使用 Configuration Manager 同步已购买的应用列表。 然后，可以在 Configuration Manager 控制台中查看这些应用，并按照部署任何其他应用的方式进行部署。


## <a name="online-and-offline-apps"></a>联机和脱机应用

适用于企业的 Microsoft Store 支持两种类型的应用：

- **联机** - 此许可类型要求用户和设备连接到应用商店，以获取应用及其许可。 Windows 10 设备必须已加入 Azure Active Directory 域。
- **脱机** - 能够缓存应用和许可证，直接在本地网络内部署。 设备不需要连接到 Microsoft Store 或 Internet。

[了解更多](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview)适用于企业的 Microsoft Store 的相关信息。

Configuration Manager 支持在具有 Configuration Manager 客户端的 Windows 10 设备上管理适用于企业的 Microsoft Store 应用，也支持使用 Microsoft Intune 注册的 Windows 10 设备。 Configuration Manager 对联机和脱机应用提供以下功能。

> [!IMPORTANT]
> 若要使用适用于企业的 Microsoft Store，Windows 10 设备必须运行 2015 年 11 月（即 1511）版本或更高版本。


|功能|脱机应用|联机应用|
|------------|------------|------------|
|将应用数据同步到 Configuration Manager<br>（每 24 小时同步一次）|是|是|
|从应用商店应用创建 Configuration Manager 应用程序|是|是|
|对应用商店中免费应用的支持|是|是|
|对应用商店中收费应用的支持|否|是<sup>1</sup>|
|支持针对用户或设备集合必需的部署|是|是|
|支持对用户或设备集合可用的部署|是|是|
|来自应用商店的业务线应用的支持|是|是|

<sup>1</sup>若要使用 Configuration Manager 客户端将联机许可的应用部署到 Windows 10 电脑上，这些应用必须在 Windows 10 创意者更新或更高版本上运行。

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>在运行 Configuration Manager 客户端的 PC 上使用适用于企业的 Microsoft Store 部署在线应用程序
在将适用于企业的 Microsoft Store 应用部署到运行完整 Configuration Manager 客户端的 PC 前，请考虑以下方面：

- 若要使用完整功能，PC 必须运行 Windows 10 创意者更新或更高版本。
- 必须将电脑添加到将适用于企业的 Microsoft Store 注册为管理工具的同一个租户的 Azure Active Directory 中。
- 使用内置管理员帐户登录 PC 时，它们无法访问适用于企业的 Microsoft Store 应用。
- PC 必须具有适用于企业的 Microsoft Store 的实时 Internet 连接。

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>有关运行较早版本的 Windows 10 的 PC 的说明
在运行创意者更新（与 Configuration Manager 客户端一起使用）之前的 Windows 10 版本的 PC 上，适用以下功能：


- 通过用户安装应用程序强制执行安装时，应用程序达到其安装截止日期，或者通过对所需部署进行安装后重新评估：
    - 通过启动适用于企业的 Microsoft Store 应用，“强制执行”应用程序。 
    - 在安装应用前，最终用户必须从应用商店完成安装
    - 在 Configuration Manager 控制台中，应用程序状态会报告失败，并显示以下错误：“Microsoft Store 应用在客户端电脑上打开并等待用户完成安装。”
- 在下一步的应用程序评估周期中：
    - 如果最终用户从应用商店安装了应用程序，则应用程序会报告状态成功。 
    - 如果最终用户未尝试从应用商店安装应用：
        - 所需的部署会尝试启动应用商店并再次强制执行应用程序安装。
        - 不会重新强制执行可用的部署。

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>有关运行较早版本的 Windows 10 的 PC 的进一步说明：

- 不能部署来自适用于企业的 Microsoft Store 的业务线应用
- 部署来自应用商店的付费应用时，最终用户必须登录到应用商店并自己购买应用。
- 如果部署组策略来禁用 Microsoft Store 的使用者版本的访问权限，则适用于企业的 Microsoft Store 中的部署无法运行，即使已启用适用于企业的 Microsoft Store。


## <a name="set-up-microsoft-store-for-business-synchronization"></a>设置适用于企业的 Microsoft Store 同步
同步组织购买的应用列表，可在 Configuration Manager 控制台中查看这些应用。

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>对于 1706 之前的 Configuration Manager 版本

在 Azure Active Directory 中，将 Configuration Manager 注册为“Web 应用和/或 Web API”管理工具。**此操作会提供客户端 ID，稍后需要使用它。**
1. 在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 Active Directory 节点中，选择“Azure Active Directory”，然后单击“应用程序” > “添加”。
2.  单击“添加我的组织正在开发的应用程序”。
3.  为应用程序输入名称，选择“Web 应用程序”和/或“Web API”，然后单击“下一步”箭头。
4.  为**登录 URL**和**应用 ID URI** 输入相同 URL。 该 URL 可以是任何内容，无需解析为实际地址。 例如，可以输入 https://yourdomain/sccm。
5.  完成向导。

**在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥**
1.  突出显示已创建的应用程序，然后单击“配置”。
2.  在“密钥”下，从列表中选择持续时间，然后单击“保存”。 此操作会创建一个新的客户端密钥。 成功将适用于企业的 Microsoft Store 载入到 Configuration Manager 之前，请勿导航离开此页面。

在适用于企业的 Microsoft Store 中，将 Configuration Manager 配置为存储管理工具
1.  打开[https://businessstore.microsoft.com/managementtools](https://businessstore.microsoft.com/managementtools) 并按提示登录。
2.  接受使用条款（如果需要）。
3.  在“管理工具”下，单击“添加管理工具”。
4.  在“按名称搜索工具”中，键入以前在 AAD 中创建的应用程序的名称，然后单击“添加”。
5.  在已导入的应用程序旁单击“激活”。
6.  如果要允许购买脱机许可的应用程序，则在“管理”>“帐户信息”页面，选择“显示脱机许可的应用”。

**将应用商店帐户添加到 Configuration Manager**

1. 请确保已从适用于企业的 Microsoft Store 购买至少一个应用。 在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后单击“适用于企业的 Microsoft Store”。
2.  在“主页”选项卡上的“适用于企业的 Microsoft Store”组中，单击“添加适用于企业的 Microsoft Store 帐户”。 
3.  从 Azure Active Directory 添加租户 ID、客户端 ID 和客户端密钥，然后完成向导。
4. 完成之后，Configuration Manager 控制台中的“适用于企业的 Microsoft Store”下会出现帐户。

### <a name="for-configuration-manager-version-1706-and-later"></a>对于 Configuration Manager 版本 1706 及更高版本
<!-- ...remove above after 1802 -->

1. 在控制台中，转到“管理” > “云服务” > “Azure 服务”，然后选择“配置 Azure 服务”以启动“Azure 服务向导”。
2. 在“Azure 服务”页上，选择要配置的服务，然后单击“下一步”。
3. 在“常规”页上，提供“Azure 服务名称”的友好名称和可选说明，然后单击“下一步”。
4. 在“应用”页上，指定 Azure 环境，然后单击“浏览”打开“服务器应用”窗口。
5. 在“服务器应用”窗口中，选择要使用的服务器应用，然后单击“确定”。 服务器应用是包含 Azure 帐户配置的 Azure Web 应用，包括客户端的租户 ID、客户端 ID 和客户端的密钥。 如果没有可用的服务器应用，请使用以下操作之一：
    - 创建：若要创建新的服务器应用，请单击“创建”。 为应用和租户提供友好名称。 然后，登录到 Azure 后，Configuration Manager 在 Azure 中为用户创建 Web 应用，包括用于 Web 应用的客户端 ID 和密钥。 之后，可在 Azure 门户中查看这些内容。
    - 导入：若要使用 Azure 订阅中已存在的 Web 应用，请单击“导入”。 为应用和租户提供友好名称。 然后为 Configuration Manager 要使用的 Azure Web 应用指定租户 ID、客户端 ID 和密钥。 “验证”信息后，单击“确定”以继续。 
6. 查看“信息”页，并根据指示完成所有额外步骤和配置。 这些配置是通过 Configuration Manager 使用服务所必需的。 例如，配置适用于企业的 Microsoft Store：
    - 在 Azure 中，必须将 Configuration Manager 注册为 Web 应用或 Web API 并记录客户端 ID。 还可以指定用于管理工具 (Configuration Manager) 的客户端密钥。
    - 在适用于企业的 Microsoft Store 门户中，必须将 Configuration Manager 配置为应用商店管理工具，启用对脱机许可应用的支持，然后购买至少一个应用。 
7. 准备好继续后，单击“下一步”。
8. 在“应用配置”页上，完成此服务的应用目录和语言配置，然后单击“下一步”。
9. 完成向导后，Configuration Manager 控制台显示已将“适用于企业的 Microsoft Store”配置为“云服务类型”。




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>从适用于企业的 Microsoft Store 应用创建并部署 Configuration Manager 应用程序
同步后，像其他应用一样，创建并部署 Microsoft Store 应用。

1.  在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。
2.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，单击“创建应用程序”。
将创建包含适用于企业的 Microsoft Store 应用的 Configuration Manager 应用程序。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。

> [!IMPORTANT]
> 对于使用 Microsoft Intune 注册的设备，已部署的应用仅适用于最初注册该设备的用户。 其他任何用户都无法访问该应用。

## <a name="next-steps"></a>后续步骤

在“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。

对于管理的每个 Microsoft Store 应用，都可以查看有关该应用的信息。 此信息包括应用名称、平台、所拥有的应用许可证数量以及可以用的许可证数量。

部署在线应用后，该应用的任何更新将直接来自 Microsoft Store。 此外，Configuration Manager 不会检查在线应用的版本符合性，只是 Windows 报告应用为已安装。  

使用 Configuration Manager 客户端将脱机应用部署到 Windows 10 设备时，用户不能更新 Configuration Manager 部署外部的应用程序。 控制脱机应用的更新在多用户环境（如教室）中尤为重要。 用户可以选择使用[组策略](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy)来禁用 Microsoft Store。 

适用于企业的 Microsoft Store 管理员购买了一个脱机应用后，不要通过 Microsoft Store 将应用发布给用户。 此配置可确保用户无法安装或联机更新。 用户将仅通过 Configuration Manager 接收脱机应用更新。 
