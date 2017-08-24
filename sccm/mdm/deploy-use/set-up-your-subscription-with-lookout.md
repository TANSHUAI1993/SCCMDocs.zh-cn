---
title: "使用 Lookout 设置订阅 |System Center Configuration Manager"
description: "本主题提供有关如何配置 Lookout 设备威胁保护的详细信息。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: b777140c753e709f4048a30e63d8ae730d3e8723
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>设置订阅以使用 Lookout 设备威胁保护

*适用范围：System Center Configuration Manager (Current Branch)*

为了为 Lookout 设备威胁防护服务准备好订阅，Lookout 支持人员 enterprisesupport@lookout.com 需要有关 Azure Active Directory (Azure AD) 订阅的以下信息。 Lookout 移动端点安全租户将与 Azure AD 订阅关联以便让 Lookout 与 Intune 集成。 

* **Azure AD 租户 ID**
* Lookout 控制台**完全**访问权限的**Azure AD 组对象 ID**
* Lookout 控制台**受限**访问权限的**Azure AD 组对象 ID**（可选）

> [!IMPORTANT]
> 没有与 Azure AD 租户相关联的现有 Lookout 移动端点安全租户不能用于与 Azure AD 和 Intune 集成。 请联系 Lookout 支持人员以创建新的 Lookout 移动端点安全租户。 使用新的租户以加入 Azure AD 用户。

使用下列部分来收集需要向 Lookout 支持团队提供的信息。  

## <a name="get-your-azure-ad-information"></a>获取 Azure AD 信息
### <a name="azure-ad-tenant-id"></a>Azure AD 租户 ID
登录到[Azure AD 管理门户](https://manage.windowsazure.com)，然后选择订阅。 

![显示租户名称的 Azure AD 页面的屏幕截图](media/aad_tenant_name.png)选择订阅名称时，生成的 URL 包含订阅 ID。  如果查找订阅 ID 时遇到任何问题，请参阅此 [Microsoft 支持文章](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US)获取查找订阅 ID 的技巧。   
### <a name="azure-ad-group-id"></a>Azure AD 组 ID
Lookout 控制台支持 2 种级别的访问权限:  
* **完全访问：** Azure AD 管理员可以为用户创建一个具有完全访问权限的组，并根据需要创建具有受限访问权限的组。  只有这些组中的用户才能登录到 **Lookout 控制台**。
* **受限的访问权限：**此组中的用户不能访问某些配置以及与 Lookout 控制台注册相关的模块，并且对控制台模块的**安全策略**仅具有只读访问权限。  

有关权限的详细信息，请参阅 Lookout 网站上的[此文](https://personal.support.lookout.com/hc/en-us/articles/114094105653)。

**组对象 ID**位于“Azure AD 管理控制台”中的组的“属性”页上。

![突出显示 GroupID 字段的属性页屏幕截图](media/aad_group_object_id.png)

收集此信息后，请联系 Lookout 支持人员（电子邮件：enterprisesupport@lookout.com）。

Lookout 支持人员将使用主要联系人载入订阅，并使用收集的信息创建 Lookout 企业帐户。


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>使用 Lookout 设备威胁保护配置订阅
### <a name="step-1-set-up-your-device-threat-protection"></a>步骤 1：设置设备威胁防护
Lookout 支持人员创建企业帐户后，你可以登录到 Lookout 控制台。   Lookout 会向公司的主要联系人发送一封电子邮件，并附带登录链接(url:https://aad.lookout.com/les?action=consent)

首次登录到 Lookout 控制台时，必须使用全局管理员 Azure AD 角色的用户帐户，因为 Lookout 需要此信息来注册 Azure AD 租户。   后续登录不需要用户具有此级别的 Azure AD 特权。  第一次登录时将显示同意页。 选择“接受”完成注册。

![第一次登录到 Lookout 控制台时的登录页面屏幕截图](media/lookout-initial-login.png)

接受并同意后，系统将重定向到 Lookout 控制台。 初始注册后，可使用 URL (https://aad.lookout.com) 进行后续登录

如果遇到登录问题，请参阅[疑难解答文章]()。

接下来的步骤概述了在 [Lookout 控制台](https://aad.lookout.com) 内完成 Lookout 设置必须执行的任务。

### <a name="step-2-configure-the-intune-connector"></a>步骤 2：配置 Intune 连接器

1.  在 Lookout 控制台中，从“系统”模块中选择“连接器”选项卡，然后选择“Intune”。

  ![打开了连接器选项卡的 Lookout 控制台屏幕截图，其中突出显示了 Intune 选项](media/lookout-setup-intune-connector.png)

2.  在连接设置选项中，以分钟为单位配置检测信号频率。  Intune 连接器现已准备就绪。  

  ![连接设置选项卡的屏幕截图，其中显示配置了检测信号频率](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>步骤 3：配置注册组
在“注册管理”选项中，定义一组其设备已向 Lookout 注册的用户。 最佳做法是使用一小组用户进行测试，熟悉集成的工作原理。  若测试结果令人满意，可以将注册扩展到其他组的用户。

若要开始使用注册组，首先请定义一个 Azure AD 安全组，它将成为在 Lookout 设备威胁保护中注册的第一组优良用户。 在 Azure、AD 和 Lookout 控制台中创建组后，请转到“注册管理”选项，然后添加 Azure AD 安全组“显示名称”以进行注册。

如果用户在注册组中，任何在 Azure AD 中经过识别并获得支持的设备都可以在 Lookout 设备威胁保护中注册并激活。  首次在支持的设备上打开 Lookout for Work 应用时，设备就已在 Lookout 中激活。

![Intune 连接器注册页面的屏幕截图](media/lookout-enrollment.png)

最佳做法是使用时间增量的默认值（即 5 分钟）来检查新设备。

>[!IMPORTANT]
> 显示名称区分大小写。  请使用“显示名称”，如 Azure 门户安全组的“属性”页所示。 注意在下面的图片中，安全组的“属性”页上的显示名称区分大小写。  标题全部显示为小写，不应将其用于进入 Lookout 控制台。
>![Azure 门户的屏幕截图、Azure Active Directory 服务、属性页](media/aad-group-display-name.png)

当前版本具有以下局限性：  
* 组显示名称没有任何验证。  请确保在 Azure AD 安全组的 Azure 门户中显示的“显示名称”字段中使用值。
* 当前不支持在组内创建组。  指定的 Azure AD 安全组可能仅包含用户，而不包含嵌套组。


### <a name="step-4-configure-state-sync"></a>步骤 4：配置状态同步
在“状态同步”选项中，指定应发送到 Intune 的数据类型。  目前，必须启用设备状态和威胁状态以便使 Lookout Intune 集成能正常工作。  默认情况下已启用以上状态。
### <a name="step-5-configure-error-report-email-recipient-information"></a>步骤 5：配置错误报告电子邮件收件人的信息
在“错误管理”选项中输入接收错误报告的电子邮件地址。

![Intune 连接器错误管理页面的屏幕截图](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>步骤 6： 配置注册设置
在“系统”模块的“连接器”页上，指定将设备视为已断开连接之前的天数。  将断开连接的设备视为不合规，并根据 SCCM 条件性访问策略阻止其访问公司应用程序。 可以指定介于 1 到 90 天之间的值。

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>步骤 7：配置电子邮件通知
若要接收与威胁相关的电子邮件警报，请使用应接收该通知的用户帐户登录到 [Lookout 控制台](https://aad.lookout.com)。 在“系统”模块的“首选项”选项卡上，选择所需的通知并将它们设置为“打开”。 保存所做更改。

![显示用户帐户的首选项页屏幕截图](media/lookout-email-notifications.png)如果不再需要接收电子邮件通知，可将通知设置为“关闭”并保存所做的更改。
### <a name="step-8-configure-threat-classification"></a>第 8 步：配置威胁分类
Lookout 设备威胁保护会对各种移动威胁进行分类。 [Lookout 威胁分类](http://personal.support.lookout.com/hc/en-us/articles/114094130693)具有与之相关联的默认风险级别。 可以随时更改这些级别以满足公司的需要。

![显示威胁和分类的策略页屏幕截图](media/lookout-threat-classification.png)

>[!IMPORTANT]
> 此处指定的风险级别是设备威胁保护的一个重要方面，因为 Intune 集成会在运行时根据这些风险级别计算设备的合规性。 换而言之，如果设备的活动威胁级别为：高、中或低，Intune 管理员会在策略中设置规则来标识不合规的设备。 Lookout 设备威胁保护中的威胁分类策略直接影响 Intune 中设备的合规性计算。

## <a name="watching-enrollment"></a>观看注册
设置完成后，Lookout 设备威胁保护会轮询对应于指定注册组的 Azure AD 设备。  可在设备模块上找到已注册设备的相关信息。  设备的初始状态显示为待定。  安装、打开并激活 Lookout for Work 应用后，设备状态将发生更改。  有关如何将 Lookout for Work 应用推送到设备的详细信息，请参阅[配置并部署 Lookout for Work 应用](configure-and-deploy-lookout-for-work-apps.md)主题。
## <a name="next-steps"></a>后续步骤
[启用 Lookout MTP 连接 Intune](enable-lookout-connection-in-intune.md)
