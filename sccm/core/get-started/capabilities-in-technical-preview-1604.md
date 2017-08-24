---
title: "Technical Preview 1604 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1604 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 26b0d8ea7b3e841c48945df55f8860394a98a29f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1604 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍 System Center Configuration Manager Technical Preview 1604 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

 以下是可以试用的此版本的新功能。  

##  <a name="BKMK_WindowsVPP"></a>管理从适用于企业的 Windows 应用商店批量采购的应用  
 在[适用于企业的 Windows 应用商店](https://www.microsoft.com/en-us/business-store)中可以为组织查找并采购应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可从 Configuration Manager 控制台管理批量采购的应用，例如：  

-   可以将采购的应用列表与 Configuration Manager 同步  

-   同步的应用会出现在 Configuration Manager 控制台中，可以如同任何其他应用一样部署这些应用  

-   可以跟踪可用的许可证数，以及在 Configuration Manager 控制台中使用的许可证数  

### <a name="try-it-out"></a>试试看！  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>方案 1：设置适用于企业的 Windows 应用商店同步  

1.  在 Azure Active Directory 中，将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具。 这会为你提供以后将需要的客户端 ID。  

    1.  在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 **Active Directory** 节点中，选择“Azure Active Directory”，然后单击“应用程序” > “添加”。  

    2.  单击“添加我的组织正在开发的应用程序”。  

    3.  为应用程序输入名称，选择“Web 应用程序”和/或“Web API”，然后单击“下一步”箭头。  

    4.  为**登录 URL**和**应用 ID URI** 输入相同 URL。  该 URL 可以是任何内容，无需解析为实际地址。 例如，可以输入 **https://&lt;yourdomain\>/sccm**。  

    5.  完成向导。  

2.  在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。  

    1.  突出显示刚创建的应用程序，然后单击“配置”。  

    2.  在“密钥”下，从列表中选择持续时间，然后单击“保存”。  这创建新客户端密钥。  成功将适用于企业的 Windows 应用商店载入到 Configuration Manager 之前，请勿导航离开此页面。  

3.  在适用于企业的 Windows 应用商店中，将 Configuration Manager 配置为存储管理工具。  

    1.  打开 [https://businessstore.microsoft.com/zh-cn/managementtools](https://businessstore.microsoft.com/en-us/managementtools)，在出现提示时进行登录。  

    2.  接受使用条款（如果需要）。  

    3.  在“管理工具”下，单击“添加管理工具”。  

    4.  在“按名称搜索工具”中，键入以前在 AAD 中创建的应用程序的名称，然后单击“添加”。  

    5.  在刚导入的应用程序旁单击“激活”。  

    6.  在“显示脱机许可的应用”向导中，如果要允许采购脱机许可的应用程序，则单击“是”。  

4.  从适用于企业的 Windows 应用商店采购至少一个应用。  

5.  在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后单击“适用于企业的 Windows 应用商店”。  

6.  在“主页”选项卡上的“创建”组中，单击“添加适用于企业的 Windows 应用商店帐户”。  

7.  从 Azure Active Directory 添加租户 ID、客户端 ID 和客户端密钥，然后完成向导。  

8.  完成之后，会在 Configuration Manager 控制台中“适用于企业的 Windows 应用商店帐户”列表中看到配置的帐户。  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>方案 2：从适用于企业的 Windows 应用商店离线授权的应用创建和部署 Configuration Manager 应用程序  

1.  在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。  

2.  **从适用于企业的 Windows 应用商店购买的应用**列表显示了从存储区同步的应用列表。 选择要部署的应用，然后在“主页”选项卡的“创建”组中，单击“创建应用程序”。  

3.  将创建包含适用于企业的 Windows 应用商店应用的 Configuration Manager 应用程序。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。  

##  <a name="BKMK_PFW"></a> 对 Microsoft Passport for Work 管理的改进  
 现在可以将 Passport for Work 策略部署到由 Configuration Manager客户端管理的已加入域的 Windows 10 设备。  

##  <a name="bkmk_switchsup"></a>供客户端切换到新软件更新点的选项  
 在 1604 Technical Preview 中，可以启用 Configuration Manager 供客户端在活动软件更新点出现问题时切换到新软件更新点的选项。 对于此选项，必须在主站点上有多个软件更新点可用。 在设备集合上启用此选项，在启用之后，当集合中的客户端未能成功连接到活动的软件更新点时，将在下一次扫描时查找另一个软件更新点。 根据 WSUS 配置设置（更新分类、产品等），切换到新的软件更新点将会产生额外的网络流量。 因此，应仅当需要时才使用此选项。  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>启用切换软件更新点的选项  

1.  在 Configuration Manager 控制台中，转到“资产和符合性”>“概览”>“设备集合”。  

2.  在“主页”选项卡上的“集合”组中，单击“客户端通知”，然后单击“切换到下一个软件更新点”。  

> [!NOTE]  
>  此选项只在具有多个软件更新点的站点上可用。  

##  <a name="bkmk_peercache"></a>用于管理客户端缓存设置和客户端对等缓存的客户端设置  
 技术预览版 1604 引入了影响客户端缓存使用的两个新设备客户端设置。 这两个设置可以单独使用，但是在用于客户端设置的同一个属性表中配置，可结合使用以帮助管理将内容部署到远程位置的客户端。  

-   第一个设置是**客户端对等缓存**，这是内置 Configuration Manager 解决方案，供客户端用于直接从本地缓存将内容与其他客户端共享。 若要使对等缓存客户端可以共享内容，它们必须是相同边界组的成员。 对等缓存不会代替其他解决方案（如 BranchCache）的使用，而是并行工作以便提供更多选项，用于扩展传统内容部署解决方案（如分发点）。  

     将启用对等缓存的客户端设置部署到集合后，该集合的成员可以充当其边界组中其他客户端的对等内容源。  充当对等内容源的客户端将提交一份可用内容列表，即缓存到其管理点的内容的列表。 然后，当该边界组中的下一个客户端请求该内容时，该对等缓存源将作为潜在内容源提供，同时提供所有配置为快速的分发点。 客户端从此内容源的组合池中选择一个随机内容源。 当边界组中没有快速分发点或对等缓存源时，客户端将只能从配置为慢速的分发点查找内容。  

-   第二个新设置使用户能够在客户端上**管理缓存的大小**。 可以将缓存设置为具有以兆字节 (MB) 表示时的最大大小，以及以客户端驱动器空间的百分比表示时的最大大小。  客户端会强制执行先达到的设置值。  

为了帮助了解客户端对等缓存的使用，可以查看“客户端数据源”仪表板。 在控制台中，转到“监视”>“客户端状态”>“客户端数据源”。 在此处可以选择要应用于仪表板的时间段。 然后在显示中，可以选择要查看其信息的边界组或包。 查看信息时，可以将鼠标悬停在表面上方，以查看有关不同内容或策略源的更多详细信息。  

 还可以使用新报表“客户端数据源 - 摘要”查看每个边界组的客户端数据源摘要。   
**有关使用对等缓存的要求：**  

-   必须使用对每个客户端上的缓存文件夹具有**完全控制**的**网络访问帐户**来配置站点。 默认情况下，这是 **%windir%\ccmcache**  

-   仅当是相同边界组的成员时，客户端才能使用对等缓存传输内容。  

#### <a name="to-configure-client-peer-cache-client-settings"></a>配置客户端对等缓存客户端设置  

1.  两种设置均在同一客户端设置页上进行配置。 在 Configuration Manager 控制台中，转到“管理”>“客户端设置”，然后打开要使用的设备客户端设置对象。 还可以修改默认客户端设置对象。  

2.  从可用设置的列表中，选择“客户端缓存设置”。  

3.  若要管理缓存的大小，请将“配置客户端缓存大小”设置为“是”。 然后可同时以兆字节和客户端驱动器空间的百分比这两种形式配置最大缓存大小。  

4.  要使客户端能够参与客户端对等缓存，请将“在完整操作系统中启用 Configuration Manager 客户端以共享内容”设置为“是”。 然后可以配置客户端使用的端口，包括将采用 HTTP 还是 HTTPS。  

### <a name="try-it-out"></a>试试看！  
 尝试完成下面的任务，然后使用本主题顶部附近的反馈信息，让我们知道它的工作方式：  

1.  修改客户端设置以指定客户端缓存的新大小，然后在客户端上确认此设置。  

2.  使用客户端设置来配置多个使用对等缓存的客户端  

3.  将内容部署到客户端，以便一些或大部分客户端通过使用对等缓存从其他客户端获取该内容。  可以通过查看新仪表板确认使用的内容源。  

    > [!NOTE]  
    >  若要使用技术预览版和单个分发点完成此任务，请将该分发点配置为对所有客户端的网络位置是慢速的。 然后将内容分发给单个客户端。  该客户端获取内容之后，可以将内容分发给其他客户端，这些客户端应首先查找本地对等方以用作内容源，然后再从客户端位置被视为慢速的分发点。  

##  <a name="bkmk_passport"></a>支持将 Passport for Work 作为 KSP  
 System Center Configuration Manager 允许集成 Microsoft Passport for Work，它是使用 Active Directory 或 Azure Active Directory 帐户取代密码、智能卡或虚拟智能卡进行登录的一种替代方法。  
通过 Passport，你可以使用“用户手势”取代密码进行登录。 用户手势可以是简单 PIN、Windows Hello 等生物识别身份验证或指纹读取器等外部设备。  

-   可以使用 Configuration Manager 控制用户可以用于以及不能用于登录的手势，并配置 PIN 复杂性要求。  

-   可在 Passport for Work 密钥存储提供程序 (KSP) 中存储身份验证证书。  

当用户创建 Passport PIN 时，Windows 会发送通知，Configuration Manager 会侦听该通知。  这使 Configuration Manager 可以快速了解哪些用户创建了 Passport PIN。 如果 Passport 在证书配置文件中用作密钥存储提供程序，则 Configuration Manager 随后还可以向这些用户颁发新证书。  

##  <a name="bkmk_onpremdha"></a>本地设备运行状况证明  
 Windows 10 设备的运行状况证明现在可以配置为使用本地基础结构进行通信。  管理员可以指定是通过云还是本地资源进行报告。  如果为运行状况证明报告选择“本地”，则可以为服务指定 URI。 这使无法进行 Internet 访问的客户端电脑可以启用和管理使用运行状况证明的设备。  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>为本地设备启用运行状况证明  

1.  在 Configuration Manager 控制台中，导航到“管理” > “概述” > “客户端设置”，然后将“使用本地运行状况证明服务”设置为“是”。  

2.  指定**本地运行状况证明服务 URL**，然后单击“确定”。  

若要进行尝试，请使用客户端代理设置配置本地运行状况证明服务。  

##  <a name="BKMK_Smart"></a>适用于 Android 设备的 SmartLock 设置  
 一个新设置“允许 SmartLock 和其他信任代理”已添加到“Android 和 Samsung KNOX”配置项目，这使用户可以在兼容的 Android 设备上控制 SmartLock 功能。 如果设备处于可信位置（例如当它连接到特定蓝牙设备时，或者在 NFC 标记附近时），则此手机功能（有时称为信任代理）使你可以禁用或绕过设备锁屏界面密码。 可以使用此设置防止最终用户配置 SmartLock。  
