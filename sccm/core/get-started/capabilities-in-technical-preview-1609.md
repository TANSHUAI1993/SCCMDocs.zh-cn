---
title: "Technical Preview 1609 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 版本 1609 中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: article
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
caps.latest.revision: "2"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 89a41c8a3137d0e54011ddf9a1d9b4894ecb7df8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1609 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*



本文介绍了 System Center Configuration Manager Technical Preview 版本 1609 中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    

**此 Technical Preview 中的已知问题：**  
*  升级到 Configuration Manager 1609 Technical Preview 时，将删除已部署的任何版本升级策略。 若要继续使用这些策略，则必须重新创建并部署它们。


**以下是可以试用的此版本的新功能。**  

## <a name="improvements-to-endpoint-protection"></a>Endpoint Protection 的改进
Endpoint Protection 反恶意软件策略设置的改进 - 现在可以指定 Endpoint Protection 云保护服务在其中阻止可疑文件的级别。 一个新的设置，可以使管理员根据计算机遇到的大量恶意软件指定“危险的”计算机。

## <a name="increased-number-of-enrolled-devices"></a>增加了“注册的设备”的数量
管理员现在可以让用户在使用 Intune 管理的混合移动设备中注册多达 15 个设备。 以前此限制为每个用户 5 个设备。

## <a name="additional-apple-dep-settings"></a>其他 Apple DEP 设置

管理员现在可以在适用于 iOS 和 Mac 设备的 DEP 配置文件中配置下列 Apple 设备注册计划 (DEP) 设置：
- **Touch ID**
- **缩放**
- **Siri**

如果启用，在设备激活过程中 Apple 的设置助理会提示此服务。

## <a name="integration-with-upgrade-analytics"></a>与 Upgrade Analytics 的集成

Upgrade Analytics 使你能够评估和分析设备的准备情况以及与 Windows 10 的兼容性，从而实现更轻松、更流畅的升级。 通过将 Upgrade Analytics 与 Configuration Manager 集成，你可以访问 Configuration Manager 管理控制台中的升级兼容性数据，然后从设备列表中设置目标设备以进行升级或更新。

有关 Upgrade Analytics 的详细信息，请参阅 [Upgrade Analytics 入门](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started)。

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Windows 10 VPN 混合配置文件的本机连接类型

结合使用 Configuration Manager 和 Intune 时，现在可在 Configuration Manager 控制台中创建具有 Microsoft Automatic、IKEv2、PPTP 和 L2TP 连接类型的 Windows 10 VPN 配置文件，而无需使用 OMA-URI。

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>适用于企业的 Windows 应用商店与 Configuration Manager 集成的增强功能

在此版本中，我们已更新[适用于企业的 Windows 应用商店集成](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)的以下新增功能：

**更新：**当前的技术预览版不支持即时同步功能。

- 以前，你仅可以从适用于企业的 Windows 应用商店部署免费的应用程序。 Configuration Manager 现在还支持部署在线支付许可应用（仅适用于注册了 Intune 的设备）。
- 现在你可启动适用于企业的 Windows 应用商店和 Configuration Manager 之间的即时同步。
- 现在可修改从 Azure Active Directory 获取的客户端密钥

### <a name="try-it-out"></a>试试看！

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>购买并同步在线支付许可应用

1. 从适用于企业的 Windows 应用商店购买在线支付许可应用。
2. 在 Configuration Manager 控制台的“管理”工作区中，单击“云服务” > “更新与维护服务” > “适用于企业的 Windows 应用商店”。
3. 在“主页”选项卡上的“同步”组中，单击“立即同步”。
4. 不久之后，你购买的应用将出现在“应用程序管理”工作区的“应用商店应用的许可证信息”节点中。

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>创建和部署来自同步应用数据的 Configuration Manager 应用程序

从付费的应用商店应用中创建和部署 Configuration Manager 应用程序的过程与从免费的应用中创建应用程序的过程相同。 请参阅[使用 System Center Configuration Manager 管理来自适用于企业的 Windows 应用商店的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)中的**创建和部署来自适用于企业的 Windows 应用商店应用的 Configuration Manager 应用程序**部分。


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>修改 Azure Active Directory 中的客户端密钥

1. 在 Configuration Manager 控制台的“管理”工作区中，单击“云服务” > “更新与维护服务” > “适用于企业的 Windows 应用商店”。
2. 选择适用于企业的 Windows 应用商店的帐户，然后单击“属性”。
3. 在“适用于企业的 Windows 应用商店的帐户属性”对话框中的“客户端密钥”字段中输入新的密钥，然后单击“验证”。 验证后，单击“应用”，然后关闭此对话框。


## <a name="new-compliance-settings-for-configuration-items"></a>配置项目的新符合性设置

我们添加了许多新设置，你可以在配置项目中将这些设置用于各种设备平台。
这些设置之前存在于 Microsoft Intune 的独立配置中，现在结合使用 Intune 和 Configuration Manager 时可以使用这些设置。
如果需要有关任何这些设置的帮助，请打开[使用 Microsoft Intune 策略管理设备上的设置和功能](https://docs.microsoft.com/en-us/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies)，然后选择所需的平台设置副标题。


### <a name="new-settings-for-android-devices"></a>适用于 Android 设备的新设置

#### <a name="password-settings"></a>密码设置

- **记住密码历史**
- **允许指纹解锁**

#### <a name="security-settings"></a>安全设置

- **需要对存储卡进行加密**
- **允许屏幕捕获**
- **允许提交诊断数据**

#### <a name="browser-settings"></a>浏览器设置

- **允许使用 Web 浏览器**
- **允许自动填充**
- **允许使用弹出窗口阻止程序**
- **允许使用 Cookie**
- **允许使用活动脚本**

#### <a name="app-settings"></a>应用设置

- **允许使用 Google Play 商店**

#### <a name="device-capability-settings"></a>设备功能设置

- **允许使用可移动存储**
- **允许使用 Wi-Fi tethering**
- **允许使用地理位置**
- **允许使用 NFC**
- **允许使用蓝牙**
- **允许语音漫游**
- **允许数据漫游**
- **允许 SMS/MMS 消息传送**
- **允许使用语音助手**
- **允许语音拨号**
- **允许复制和粘贴**


### <a name="new-settings-for-ios-devices"></a>适用于 iOS 设备的新设置

#### <a name="password-settings"></a>密码设置

- **密码中所需的复杂字符数**
- **允许简单密码**
- **需要提供密码之前处于非活动状态的分钟数**
- **记住密码历史**

### <a name="new-settings-for-mac-os-x-devices"></a>适用于 Mac OS X 设备的新设置

#### <a name="password-settings"></a>密码设置

- **密码中所需的复杂字符数**
- **允许简单密码**
- **记住密码历史**
- **屏幕保护程序激活前处于非活动状态的分钟数**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>适用于 Windows 10 桌面和移动版设备的新设置

#### <a name="password-settings"></a>密码设置

- **最小字符集数**
- **记住密码历史**
- **当设备从空闲状态返回时需要密码**

#### <a name="security-settings"></a>安全设置

- **需要对移动设备加密**
- **允许手动取消注册**

#### <a name="device-capability-settings"></a>设备功能设置

- **允许通过移动电话网络使用 VPN**
- **允许在通过移动电话网络漫游时使用 VPN**
- **允许重置手机**
- **允许使用 USB 连接**
- **允许使用 Cortana**
- **允许操作中心通知**

### <a name="new-settings-for-windows-10-team-devices"></a>适用于 Windows 10 协同版设备的新设置

#### <a name="device-settings"></a>设备设置

- **启用 Azure Operational Insights**
- **启用 Miracast 无线投影**
- **选择“欢迎”屏幕上显示的会议信息**
- **锁屏背景图像 URL**


### <a name="new-settings-for-windows-81-devices"></a>适用于 Windows 8.1 设备的新设置

#### <a name="applicability-settings"></a>适用性设置

- **将所有配置应用到 Windows 10**

#### <a name="password-settings"></a>密码设置

- **所需的密码类型**
- **最小字符集数**
- **最短密码长度**
- **擦除设备前允许的重复登录失败次数**
- **屏幕关闭前处于不活动状态的分钟数**
- **密码过期（天数）**
- **记住密码历史**
- **防止重用以前的密码**
- **允许图片密码和 PIN**

#### <a name="browser-settings"></a>浏览器设置

- **允许自动检测 Intranet 网络**


### <a name="new-settings-for-windows-phone-81-devices"></a>适用于 Windows Phone 8.1 设备的新设置

#### <a name="applicability-settings"></a>适用性设置

- **将所有配置应用到 Windows 10**

#### <a name="password-settings"></a>密码设置

- **最小字符集数**
- **允许简单密码**
- **记住密码历史**

#### <a name="device-capability-settings"></a>设备功能设置

- **允许自动连接到免费 Wi-Fi 热点**


## <a name="improvements-for-boundary-groups"></a>边界组的改进
此预览版介绍了对边界组的重要更改以及它们如何与分发点配合使用。 这些更改将有助于简化内容基础结构的设计，同时使你更好地控制客户端如何以及何时回退以搜索更多分发点作为内容源位置。 这包括位于本地和基于云的分发点。

这些改进将替换你现如今可能已熟悉的概念和行为（类似于将分发点配置为快速或慢速），将它们替换为一个新的模型，该模型将更易于设置和维护。 这些更改也是未来更改的基础，以后还将改进与边界组相关联的其他站点系统角色。  

在升级到 1609 期间，升级将转换你的当前边界组配置，以适应新的模型，以便这些更改不会妨碍内容分发配置（请参阅[将现有边界组更新到新模型](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update)。

以下部分将详细说明此预览版引入的更改、新模型的工作原理，以及在升级已配置边界组的站点时可以期望的内容。



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>边界组和内容位置的用户界面和行为的更改
以下是对边界组以及客户端查找内容的方式的关键更改。 这些更改许多都和概念协同工作。
-   **已删除对于快速或慢速的配置：**不再将单独的分发点配置为快速或慢速。  相反，每个与边界组相关联的站点系统都将视为相同的系统。 由于有此更改，边界组属性的“引用”选项卡不再支持快速或慢速的配置。
-   **每个站点的新默认边界组：**每个主站点都具有一个名为 ***Default-Site-Boundary-Group\<sitecode>*** 的新默认边界组。  当客户端不在分配给边界组的网络位置时，该客户端将从其指定的站点使用与默认组相关联的站点系统。 计划使用此边界组作为回退内容位置概念的替换。    
 -  已删除**“允许使用内容的回退源位置”**：无法再将分发点显式配置为用于回退，并且已从用户界面中删除设置此操作的选项。

    此外，已更改应用程序部署类型上的**允许客户端使用内容的回退源位置**的设置结果。 部署类型上的此设置现在允许客户端使用默认站点边界组作为内容源位置。

 -  **边界组关系：**每个边界组都可链接到一个或多个其他的边界组。 这些链接就会形成关系，并在名为“关系”的新边界组属性选项卡上进行配置：
    -   客户端直接与之关联的每个边界组都称为**当前**边界组。  
    -   由于客户端的“当前”边界组和另一个组之间存在关联，客户端可以使用的任何边界组都称为**邻居**边界组。
    -  它位于添加可用作“邻居”边界组的边界组“关系”选项卡中。 还可以配置时间（分钟），用于确定在当前组中无法从分发点找到内容的客户端开始从这些邻居边界组搜索内容位置的时间。

        添加或更改边界组配置时，可以选择阻止从当前正在配置的组中回退到该特定的边界组。

    若要使用新配置，可定义从一个边界组到另一个边界组的显式关联（链接），并在相同的时间（分钟）内配置该关联组中的所有分发点。 配置的时间可确定未能从其当前边界组找到内容源的客户端可以开始从该邻居边界组搜索内容源的时间。

    除了显式配置的边界组外，每个边界组都具有指向默认站点边界组的隐式链接。 此链接在 120 分钟后变为活动状态，在这段时间，默认站点边界组成为一个邻居边界组，它允许客户端使用与该边界组相关联的分发点作为内容源位置。

    此行为替换以前称为内容回退的行为。  可以通过将默认站点边界组显式关联到当前组，并设置特定的时间（分钟），或完全阻止回退以防使用，来替代此 120 分钟的默认行为。


-   **客户端尝试从每个分发点获取高达 2 分钟的内容：**客户端搜索内容源位置时，它将尝试对每个分发点进行 2 分钟的访问，然后再尝试访问另一个分发点。 这是对以前版本的一个更改，在以前版本中，客户端尝试连接到分发点的时间高达 2 小时。

    - 客户端尝试使用的第一个分发点是从客户端的当前边界组（或组）中的可用分发点池中随机选择的。

    - 两分钟后，如果客户端找不到内容，它将切换到新的分发点并尝试从该服务器获取内容。 每隔两分钟重复此过程，直到客户端找到内容或到达其池中的最后一个服务器。

    - 如果在回退到达邻居边界组期间前，客户端无法从其当前池找到有效的内容源位置，则客户端将向其当前列表的末尾添加邻居组中的分发点，然后搜索包括来自两个边界组的分发点的扩展组的源位置。

        > [!TIP]  
        > 创建从当前边界组到默认站点边界组的显式链接，并定义比链接到邻居边界组的回退时间更少的回退时间时，客户端将在包括邻居组之前从默认站点边界组开始搜索源位置。

    - 客户端无法从池中的最后一个服务器获取内容时，它将再次开始该过程。


### <a name="how-the-new-model-works"></a>新模型的工作原理
配置边界组时，可以将边界（网络位置）和站点系统角色（如分发点）关联到边界组。 这样做有助于将客户端链接到站点系统服务器，如位于网络上的客户端附近的分布点。   
-   可以将相同的边界分配给多个边界组
-   站点系统服务器（如分发点）可与多个边界组相关联，从而使它们可用于更广泛的网络位置
-   如果分发点不与边界组关联，则客户端不能使用该分发点作为内容源位置。

从本技术预览开始，可以定义边界组关系，以配置内容源位置的回退行为。 可以在边界组属性的新“关系”选项卡配置这一新行为，该行为替换了将站点系统配置为慢速或快速，并配置一个边界组以允许内容的回退源位置行为。

在“关系”选项卡上，添加其他边界组，以配置与这些组之间的关系。 每个关系都是一个单向链接（从**当前**边界组指向添加的边界组），这称为**邻居**。 对于创建的每个链接，都可以为分发点配置一个回退时间（分钟）。 如果当前边界组中的客户端无法从其当前边界组找到有效的内容源位置，则可以使用此时间来确定开始使用邻居边界组中的分发点的时间间隔。

如果客户端无法找到内容，并开始从邻居边界组搜索位置，则它将以一种可控的方式增加该客户端的可用分发点池。  

-   一个边界组可具有多个关系。 这使你可以为不同的邻居配置回退，以在不同的时间段后发生。
-   客户端仅回退到是其当前边界组的直接邻居的边界组。
-   当某个客户端是多个边界组的成员时，此当前边界组即被定义为所有客户端的边界组的联合。  然后该客户端可以回退到任何这些原始边界组的一个邻居边界组。

除了定义的链接外，还有一个隐式链接，此链接是在你创建的边界组和为每个站点自动创建的默认边界组之间自动创建的。 此自动链接：
-   由不在边界上的客户端使用，边界与层次结构中的任何边界组都相关联，层次结构自动使用分配的站点中的默认边界组来确定有效的内容源位置。   
-   是一个默认回退选项，即从当前边界组回退到站点默认边界组，120 分钟后使用。

**使用新模型的示例：**     
创建三个边界组，使其不共享边界或站点系统服务器：
-   组 BG_A，包含与该组关联的 DP_A1 和 DP_A2 分发点
-   组 BG_B，包含与该组关联的 DP_B1 和 DP_B2 分发点
-   组 BG_C，包含与该组关联的 DP_C1 和 DP_C2 分发点

将客户端网络位置作为边界添加到仅 BG_A 边界组中，然后配置从该边界组到其他两个边界组的关系：
-   配置第一个邻居组 (BG_B) 的分发点，使其 10 分钟后使用。 此组包含分发点 DP_B1 和 DP_B2。 这两个分发点都很好地连接到第一组边界位置。
-   配置第二个邻居组 (BG_C)，使其 20 分钟后使用。 此组包含分发点 DP_C1 和 DP_C2。 这两个分发点都从其他两个边界组跨越 WAN。
-   此外，还需将位于站点服务器上的其他分发点添加到站点的默认站点边界组。 这是你最不希望的内容源位置，但它位于所有边界组的中心位置。

    边界组和回退时间的示例：

     ![BG_Fallack](media/BG_Fallback.png)


使用该配置：
-   客户端开始从其当前边界组 (BG_A) 中的分发点搜索内容，对每个分发点进行为时两分钟的搜索，然后再切换到边界组中的下一个分发点。 有效的内容源位置的客户端池包括 DP_A1 和 DP_A2。
-   如果在搜索 10 分钟之后客户端无法从其当前边界组找到内容，然后，它将向它的搜索添加 BG_B 边界组中的分发点。 然后它将继续从其组合的分发点池中的分发点搜索内容，该池现在包含来自 BG_A 和 BG_B 边界组的分发点。 客户端继续对每个分发点进行为时两分钟的联系，然后再从其池切换到下一个分发点。 有效的内容源位置的客户端池包括 DP_A1、DP_A2、DP_B1 和 DP_B2。
-   再过 10 分钟（20 分钟）后，如果客户端仍未找到分发点的内容，它将扩展其可用分发点池，以便包含来自第二个邻居组（边界组 BG_C）的分发点。 现在，客户端具有 6 个要搜索的分发点（DP_A1、DP_A2、DP_B2、DP_B2、DP_C1 和 DP_C2），并继续每隔两分钟切换到新的分发点直到找到内容。
-   如果客户端在总共 120 分钟后还未找到内容，则它将回退，以将默认站点边界组纳入其继续搜索的一部分。 现在，分发点池包括来自这三个已配置的边界组的所有分发点，并且最后一个分发点位于站点服务器计算机上。  然后，客户端继续执行对内容的搜索，并每隔两分钟对分发点进行更改直到找到内容。

通过将不同的邻居组配置为在不同的时间可用，可以控制将特定分发点添加为内容源位置的时间，以及客户端将默认站点边界组的回退用作从任何其他位置不可用的内容的安全网络的时间或设想。


### <a name="bkmk_update"></a>将现有边界组更新到新模型
安装版本 1609 并更新网站时，将自动进行以下配置。 这些配置旨在确保当前的回退行为保持可用，直到配置了新边界组和关系。  
-   站点中不受保护的分发点将添加到该站点的默认站点边界组 \<sitecode> 边界组。
-   副本由每个现有的边界组组成，这些边界组包含配置为慢速连接的站点服务器。 新组的名称为 ***\<original boundary group name>-Slow-Tmp***：  
    -   包含快速连接的站点系统会保留在原始边界组中。
    -   包含慢速连接的站点系统副本将添加到边界组副本中。 配置为慢速的原始站点系统仍处于原始边界组中，以便保持向后兼容性，但不从该边界组使用它。
    -   此边界组副本不具有与之相关联的边界。 但是，已在原始组和将回退时间设置为 0 的新边界组副本之间创建回退链接。

 下表列出了可从原始部署设置和分发点配置组合期望的新回退行为：

慢速网络中“不运行程序”的原始部署配置  |“允许客户端使用内容的回退源位置”的原始分发点配置  |新的回退行为  
---------|---------|---------
选定     |  选定    |  **没有回退** - 仅使用当前边界组中的分发点       
选定     |  未选定|  **没有回退** - 仅使用当前边界组中的分发点       
未选定 |  未选定|  **回退到邻居** - 使用当前边界组中的分发点，然后添加邻居边界组中的分发点。 除非已配置到默认站点边界组的显式链接，否则客户端将不会回退到该组。    
未选定 | 选定     |   **正常回退** - 使用当前边界组中的分发点，然后使用来自邻居和站点默认边界组的分发点

 所有其他的部署配置会导致**正常回退**。  



## <a name="office-365-client-management-dashboard"></a>Office 365 客户端管理仪表板  
Configuration Manager 1609 Technical Preview 引入了一个新的仪表板。 若要查看该仪表板，可在 Configuration Manager 控制台中转到“软件库” > “概述” > “Office 365 客户端管理”。
>[!NOTE]
>在 Configuration Manager 控制台中的“新增功能”工作区中，新仪表板被错误地命名为“Office 365 服务仪表板”。

仪表板显示以下内容的图表：

- Office 365 客户端数
- Office 365 客户端版本
- Office 365 客户端语言
- Office 365 客户端通道     
有关详细信息，请参阅 [Office 365 专业增强版的更新频道概述](https://technet.microsoft.com/library/mt455210.aspx)。
- 已在可用产品集中选择 Office 365 客户端的自动部署规则。

你可以对仪表板执行以下操作：
- 在仪表板顶部，使用“集合”下拉列表设置按特定集合的成员筛选仪表板数据。
- 在仪表板的右上方，单击“Office 365 安装程序”以启动 Office 365 客户端安装向导，将 Office 365 应用部署到客户端。 有关详细信息，请参阅[将 Office 365 应用部署到客户端](#deploy-office-365-apps-to-clients)。
- 在仪表板的中右侧，单击“创建 ADR”以打开“自动部署规则向导”，创建新的自动部署规则 (ADR)。 若要创建适用于 Office 365 应用的 ADR，请在选择该产品时选择“Office 365 客户端”。 有关详细信息，请参阅[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。
- 在仪表板的右下方，单击“创建客户端代理设置”以打开客户端代理设置。 有关详细信息，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings)。



有关 Office 365 专业增强版更新的详细信息，请参阅[使用 Configuration Manager 管理 Office 365 专业增强版更新](/sccm/sum/deploy-use/manage-office-365-proplus-updates)。

## <a name="deploy-office-365-apps-to-clients"></a>将 Office 365 应用部署到客户端
在此版本中，可以从 Office 365 客户端管理仪表板启动 Office 365 安装程序，此程序可用于配置 Office 365 安装设置、从 Office 内容传送网络 (CDN) 下载文件，以及将文件部署为 Configuration Manager 中的应用程序。

### <a name="limitations-of-office-365-deployment"></a>Office 365 部署的限制
- 尝试导入 Office 365 应用安装向导中的现有客户端设置 (XML) 时，可能会遇到问题。 你可以手动配置客户端设置，而不会出现问题。

#### <a name="to-deploy-office-365-apps-to-clients"></a>将 Office 365 应用部署到客户端
1. 在 Configuration Manager 控制台中，导航到“软件库” > “概述” > “Office 365 客户端管理”。
2. 单击右上方窗格中的“Office 365 安装程序”。 将打开 Office 365 客户端安装向导。
3. 在“应用程序设置”页上，提供应用的名称和说明，输入文件的下载位置，然后单击“下一步”。 请注意，必须采用 &#92;&#92;*server*&#92;*share* 形式指定位置。
4. 在“导入客户端设置”页上，选择是从现有的 XML 配置文件导入 Office 365 客户端设置还是手动指定设置，然后单击“下一步”。
如果具有现有的配置文件，请输入文件的位置并跳到步骤 7。 请注意，必须采用 &#92;&#92;*server*&#92;*share*&#92;*filename*.XML 形式指定位置。

    > [!IMPORTANT]
    >尝试导入此技术预览中的现有客户端设置 (XML) 时，可能会遇到问题。

5. 在“客户端产品”页上，依次选择使用的 Office 365 套件、想要包括的应用程序、应包括的任何其他 Office 产品，然后单击“下一步”。
6. 在“客户端设置”页上，选择要包括的设置，然后单击“下一步”。
7. 在“部署”页上，选择是否部署该应用程序，然后单击“下一步”。
如果选择不部署向导中的包，请跳到步骤 9。
8. 像配置典型应用程序那样，配置该向导页的其余部分。 有关详细信息，请参阅[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)。
9. 完成向导。
10. 可以在 Configuration Manager 中从“软件库” > “概述” > “应用程序管理” > “应用程序”部署或编辑应用程序，就像部署或编辑任何其他应用程序一样。

>[!NOTE]
>部署 Office 365 应用后，可以创建自动部署规则以维护该应用。 若要创建适用于 Office 365 应用的 ADR，请单击“创建 ADR”，然后在选择该产品时选择“Office 365 客户端”。 有关详细信息，请参阅[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。

## <a name="BKMK_UEFIConversion"></a>对于 BIOS 到 UEFI 转换的改进
现在可以使用新的变量 TSUEFIDrive 自定义操作系统部署任务的序列，以便“重启计算机”步骤为到 UEFI 的转换在硬盘驱动器上准备 FAT32 分区。 以下过程提供了有关如何创建任务序列步骤以便为 BIOS 到 UEFI 的转换准备硬盘驱动器的示例。

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>为到 UEFI 的转换准备 FAT32 分区：
在现有的用于安装操作系统的任务序列中，添加一个新组，并包含将 BIOS 转换为 UEFI 的步骤。

1. 在捕获文件和设置之后，并在安装操作系统之前，创建新的任务序列组。 例如，在“捕获文件和设置”组之后创建名为“BIOS-to-UEFI”的组。
2. 在新组的“选项”选项卡中，添加一个新的任务序列变量作为条件，其中 **_SMSTSBootUEFI**  **不等于** **true**。 这样可以在计算机已处于 UEFI 模式时，防止运行组中的步骤。
![BIOS 转 UEFI 组](media/BIOS-to-UEFI-group.png)
3. 在新组中，添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。  
4. 在“选项”选项卡中，添加一个任务序列变量作为条件，其中 **_SMSTSInWinPE 等于 false**。 这样在计算机已处于 Windows PE 时，防止运行此步骤。

    ![“重启计算机”步骤](media/Restart-in-Windows-PE.png)
5. 添加一个步骤以启动 OEM 工具，该工具可将固件从 BIOS 转换到 UEFI。 这通常是**运行命令行**任务序列步骤，其中有一个命令行可以启动 OEM 工具。
5.  添加“格式化磁盘并分区”任务序列步骤，用于对硬盘进行分区和格式化。 在该步骤中，执行以下操作：
    1.  创建 FAT32 分区，该分区在安装操作系统之前将转换为 UEFI。 为“磁盘类型”选择“GPT”。
    ![格式化磁盘并分区步骤](media/Format-and-partition-disk.png)
    2.  转到 FAT32 分区的属性。 在“变量”字段中输入“TSUEFIDrive”。 当任务序列检测到此变量时，它将为 UEFI 转换做准备，准备就绪后会重启计算机。
    ![分区属性](media/Partition-properties.png)
    3. 创建 NTFS 分区，任务序列引擎使用此分区保存其状态和存储日志文件。
6.  添加“重启计算机”任务序列步骤。 在“指定重启后要运行的内容”中，选择“已选择分配给此任务序列的启动映像”以在 Windows PE 中启动计算机。  




## <a name="intune-compliance-charts"></a>Intune 合规性图表
在此版本中，可以通过使用 Configuration Manager 控制台中“监视工作区”下的新图表快速查看设备的总体合规性以及不合规的主要原因。

#### <a name="to-view-the-intune-compliance-charts"></a>查看 Intune 合规性图表
1. 在 Configuration Manager 控制台中，转到“监视” > “概述” > “符合性设置”。
2. 将显示“设备的总体合规性”图表。
3. 单击“合规性策略”节点以查看“设备的总体合规性”和“不合规的主要原因”图表。

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>TP 1609 中的 Intune 合规性图表的限制
- “设备的总体合规性”图表的向下钻取当前生成错误。
- “不合规的主要原因”图表列出了策略名称，而没有逐条列出不合规的原因。 可以单击该策略向下钻取，查看不符合该策略的设备。

### <a name="try-it-out"></a>试试看
按顺序完成下列部分：

#### <a name="check-overall-compliance-chart"></a>检查“总体合规性”图表
1. 在 Configuration Manager 中添加两个 iOS 合规性策略。 一个策略应具有设备的一组设置（例如，设置 PIN 长度为 6）。 另一个策略应具有另一组设置（例如，PIN 复杂性）。 策略设置不应重叠或冲突。
2. 将这两个策略部署到一组用户。
3. 使用相同的用户帐户（即收到上一步中的策略的帐户）在 Intune 中注册两个 iOS 设备。 设备不应满足合规性策略的条件。
4. 在 Configuration Manager 中，查看“设备的总体合规性”图表。 这两个设备都应报告为不符合。
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>查看“不合规的主要原因”图表
5. 查看“不合规的主要原因”图表。 此图表列出了不符合的 5 个主要原因，但当仅跨策略设置两个符合性设置时，将仅显示前 2 个不符合的原因。
6. 单击图表中的一个部分。 这两种设备都应显示在筛选视图中的“资产和符合性” > “概述” > “设备”下。

#### <a name="make-devices-compliant-and-check-the-charts"></a>使设备合规，然后查看图表
7. 使其中一个设备符合其中一个策略。 再次查看“设备的总体合规性”图表。 该图表将显示一个合规的设备和一个不合规的设备。
8. 使另一个设备符合相同的策略。 这将使一个设备符合这两个策略以及一个设备仅符合其中一个策略。
9. 查看“不合规的主要原因”图表。 应仅列出一个不符合的原因。
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>另请参阅
[System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)
