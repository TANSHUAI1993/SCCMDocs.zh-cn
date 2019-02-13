---
title: 设置 Lookout 订阅
titleSuffix: Configuration Manager
description: 了解如何配置 Lookout 移动威胁防护。
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f914cba7eee44f340bf5b696aca1854128aeb8b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141300"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>设置 Lookout 移动威胁防护订阅

适用范围：System Center Configuration Manager (Current Branch)

Lookout 移动威胁防御订阅的设置步骤如下：

| #        |步骤  |
| ------------- |-------------|
| 1 | [收集 Azure AD 信息](#collect-azure-ad-information) |
| 2 | [配置订阅](#configure-your-subscription) |
| 3 | [配置注册组](#configure-enrollment-groups) |
| 4 | [配置状态同步](#configure-state-sync) |
| 5 | [配置错误报告电子邮件收件人信息](#configure-error-report-email-recipient-information) |
| 6 | [配置注册设置](#configure-enrollment-settings) |
| 7 | [配置电子邮件通知](#configure-email-notifications) |
| 8 | [配置威胁分类](#configure-threat-classification) |
| 9 | [监视注册](#watching-enrollment) |


> [!IMPORTANT]  
> 未与 Azure AD 租户关联的现有 Lookout 移动端点安全租户不能用于与 Azure AD 和 Intune 进行集成。 请联系 Lookout 支持人员以创建新的 Lookout 移动端点安全租户。 使用新的租户以加入 Azure AD 用户。




## <a name="collect-azure-ad-information"></a>收集 Azure AD 信息
Lookout 移动端点安全租户将与 Azure AD 订阅关联以便让 Lookout 与 Intune 集成。 若要启用 Lookout 移动威胁防御服务订阅，请向 Lookout 支持人员 (enterprisesupport@lookout.com) 提供以下信息：

- **Azure AD 租户 ID**
- Lookout 控制台*完全*访问权限的**Azure AD 组对象 ID**
- Lookout 控制台*受限*访问权限的**Azure AD 组对象 ID**（可选）

以下步骤介绍了如何收集需要提供给 Lookout 支持团队的信息。

1. 登录到 [Azure 门户](https://portal.azure.com)并选择自己的订阅。 

2. 选择订阅名称时，所生成的 URL 包括订阅 ID。 如果查找订阅 ID 时遇到任何问题，请参阅此 [Microsoft 支持文章](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b)获取查找订阅 ID 的技巧。

3. 查找 Azure AD 组 ID。  
     > [!NOTE]   
     > “组对象 ID”位于 Azure 门户的 Azure AD 边栏选项卡中组的“属性”页。  

   Lookout 控制台支持两种级别的访问权限：  

   - **完全访问权限：** Azure AD 管理员可以创建具有完全访问权限的用户的组和 （可选） 创建将具有受限访问权限的用户的组。 只有这些组中的用户才能登录到 Lookout 控制台。
   - **受限访问权限：** 此组中的用户将没有任何访问某些配置和注册相关模块的 Lookout 控制台中，且有只读访问**安全策略**Lookout 控制台的模块。  

     > [!TIP]  
     > 有关权限的详细信息，请参阅 [Lookout 支持文章](https://personal.support.lookout.com/hc/articles/114094105653)。


4. 收集此信息后，请联系 Lookout 支持人员（电子邮件：enterprisesupport@lookout.com）。 Lookout 支持人员将使用主要联系人载入订阅，并使用收集的信息创建 Lookout 企业帐户。



## <a name="configure-your-subscription"></a>配置订阅

1. Lookout 支持人员创建 Lookout 企业帐户后，将向公司的主要联系人发送电子邮件，其中附带[登录 url](https://aad.lookout.com/les?action=consent) 的链接。

2. 首次登录到 Lookout 控制台时必须使用具有 Azure AD 全局管理员角色的用户帐户，以便注册 Azure AD 租户。 后续登录无需此级别的 Azure AD 特权。 此时显示同意页。 选择“接受”完成注册。 接受并同意后，系统将重定向到 Lookout 控制台。

   ![第一次登录到 Lookout 控制台时的登录页面屏幕截图](media/lookout-initial-login.png)

3. 在 [Lookout 控制台](https://aad.lookout.com)的“系统”模块中选择“连接器”选项卡，然后选择“Intune”。

   ![打开了连接器选项卡的 Lookout 控制台屏幕截图，其中突出显示了 Intune 选项](media/lookout-setup-intune-connector.png)

4. 转到“连接器” > “连接设置”，然后指定“检测信号频率”（按分钟计）。

   ![连接设置选项卡的屏幕截图，其中显示配置了检测信号频率](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>配置注册组
1. 最佳做法是在 [Azure 门户](https://portal.azure.com)中创建一个 Azure AD 安全组，并纳入一些用户用于测试 Lookout 集成。

    > [!NOTE]  
    > 对于在 Azure AD 注册组中标识和受到支持的用户，其所有支持 Lookout 并已注册 Intune 设备都已在 Lookout MTD 控制台中注册且可在此处激活。

2. 在 [Lookout 控制台](https://aad.lookout.com)的“系统”模块中，选择“连接器”选项卡，然后选择“注册管理”，以定义一组其设备应注册 Lookout 的用户。 添加用于注册的 Azure AD 安全组“显示名称”。

    ![Intune 连接器注册页面的屏幕截图](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > 正如 Azure 门户安全组的“属性”中所示，“显示名称”区分大小写。 如下图所示，安全组的“显示名称”为大小写混用，而标题全为小写。 在 Lookout 控制台中，请匹配安全组的“显示名称”的大小写。
    >![Azure 门户的屏幕截图、Azure Active Directory 服务、属性页](media/aad-group-display-name.png)

    >[!NOTE]  
    >最佳做法是使用时间增量的默认值（即五分钟）来检查新设备。 当前限制， **Lookout 无法验证组显示名称：** 请确保**显示名称**在 Azure 门户中的字段与 Azure AD 安全组完全匹配。 **不支持创建嵌套组：** Azure AD 安全 Lookout 中使用的组必须包含仅限于用户。 不能包含其他组。

3.  添加组后，用户下次在受支持的设备上打开 Lookout for Work 应用时，设备将在 Lookout 中激活。

4.  如果对结果满意，则继续注册其他用户组。



## <a name="configure-state-sync"></a>配置状态同步
在“状态同步”选项中，指定应发送到 Intune 的数据类型。 需同时启用设备状态和威胁状态，Lookout Intune 集成才能正常工作。 这些设置默认启用。



## <a name="configure-error-report-email-recipient-information"></a>配置错误报告电子邮件收件人信息
在“错误管理”选项中输入接收错误报告的电子邮件地址。

![Intune 连接器错误管理页面的屏幕截图](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>配置注册设置
在“系统”模块的“连接器”页上，指定将设备视为已断开连接之前的天数。 将断开连接的设备视为不符合，并根据 SCCM 条件性访问策略阻止其访问公司应用程序。 可以指定介于 1 到 90 天之间的值。

![Lookout 注册设置](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>配置电子邮件通知
若要接收与威胁相关的电子邮件警报，请使用应接收该通知的用户帐户登录到 [Lookout 控制台](https://aad.lookout.com)。 在“系统”模块的“首选项”选项卡上，选择应接收通知的威胁级别，然后将其设置为“开”。 保存所做更改。

![显示用户帐户的首选项页面屏幕截图](media/lookout-email-notifications.png) 如果不再需要接收电子邮件通知，可将通知设置为“关”并保存所作更改。



## <a name="configure-threat-classification"></a>配置威胁分类
Lookout 移动威胁防御将移动威胁分为多种类型。 [Lookout 威胁分类](http://personal.support.lookout.com/hc/articles/114094130693)具有与之相关联的默认风险级别。 可随时更改这些设置以满足公司需求。

![显示威胁和分类的策略页屏幕截图](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> 风险级别是移动威胁防御的一个重要方面。 Intune 集成在运行时根据这些风险级别计算设备是否符合要求。 Intune 管理员在策略中设置规则，在设备中存在最低等级为高级、中级或低级的活跃威胁时将设备标识为不符合。 Lookout 移动威胁防御中的威胁分类策略直接引导着 Intune 中的设备符合性计算。



## <a name="watching-enrollment"></a>观看注册
设置完成后，Lookout 移动威胁防御将开始轮询 Azure AD，查找与指定注册组相对应的设备。 可在设备模块上找到已注册设备的相关信息。 设备的初始状态显示为待定。 安装、打开并激活 Lookout for Work 应用后，设备状态将发生更改。 若要详细了解如何将 Lookout for Work 应用推送到设备，请参阅[配置并部署 Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)。


## <a name="next-steps"></a>后续步骤
[启用 Lookout MTP 连接 Intune](enable-lookout-connection-in-intune.md)
