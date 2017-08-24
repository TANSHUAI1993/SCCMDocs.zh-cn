---
title: "Technical Preview 1605 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1605 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
caps.latest.revision: "36"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8b3d472c586e704ee48e9825138c72f655d89492
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1605-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1605 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview 1605 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

 **此 Technical Preview 中的已知问题：**  

-   使用 Technical Preview 1605，如果在安装管理点后更新其属性，可能会出现一个错误，该错误将强制关闭控制台。  如果发生此情况，可以卸载管理点，然后再使用所需的设置重新安装它。 也可以在安装 Technical Preview 1605 前修改管理点。  

-   使用 Technical Preview 1604 的适用于企业的 Windows 应用商店功能，然后升级到 Technical Preview 1605 时，你将无法再查看载入的数据。 所有其他功能继续正常运行。 如果使用 Technical Preview 1604 进行载入，在安装 Technical Preview 1605 后仍可继续载入，并且无需采取进一步操作。  

 **以下是可以试用的此版本的新功能。**  

##  <a name="BKMK_PerAppVPN"></a> Windows 10 设备的每应用 VPN  
 对于配合使用 Configuration Manager 和 Intune 管理的 Windows 10 设备，可添加一个应用列表，此列表可自动打开通过 Configuration Manager 管理控制台配置的 VPN 连接。 可以选择对这些应用限制 VPN 通信，也可以继续允许通过 VPN 连接进行所有通信。  

 **要求**：  

-   带 Intune 的 Configuration Manager  

-   Windows 10 VPN 配置文件至少已部署到一台设备  

##  <a name="BKMK_InstallSU"></a>安装软件更新任务序列的改进  
 已对“安装软件更新”任务序列进行以下改进：  

-   提供了一个新的任务序列变量 SMSTSSoftwareUpdateScanTimeout，用于控制“安装软件更新”任务序列步骤中软件更新扫描的超时时间。 默认值为 30 分钟。  

-   已对日志记录进行改进。 Smsts.log 日志文件包含引用其他日志文件的新日志条目，有助于在软件更新安装过程中解决问题。  

##  <a name="BKMK_PrepareConfigMgrClient"></a>准备 ConfigMgr 客户端以便捕获任务序列步骤的改进  
 “准备 ConfigMgr 客户端”一步现在将完全删除 Configuration Manager 客户端，而不是仅删除密钥信息。 任务序列每次部署捕获的操作系统映像时，都将安装新的 Configuration Manager 客户端。  

##  <a name="BKMK_Grace"></a>应用程序部署所需的宽限期  
 在某些情况下，可能会希望为用户提供更多时间（超出所配置的任何截止时间）来安装所需的应用程序部署。 例如，如果最终用户刚从假期返回，则他们可能需要等待很长时间，因为安装的应用程序部署已过期。 但是，他们仍可以在任何想要的时候立即安装应用程序。  

 为了帮助解决此问题，现在可通过将 Configuration Manager 客户端设置部署到集合来定义**宽限期**。  

 若要配置宽限期，请执行以下操作：  

1.  在客户端设置的“计算机代理”页上，将“部署截止时间后强制的宽限期(小时)”这一新属性的值配置为介于 **1** 和 **120** 小时之间。  

2.  在新的应用程序部署中，或在现有部署属性中，在“计划”页上，选中复选框“根据用户首选项延迟此部署的强制”，直到在客户端设置中定义的宽限期。  

     选中了此复选框的所有部署，以及针对其中部署了客户端设置的设备的所有部署，都将使用此宽限期。  

 在此版本中，客户端设备不使用所配置的宽限期。 如果配置宽限期，并选中该复选框，则将在截止时间后在用户配置的第一个非业务窗口中安装该应用程序。  

 已将类似的选项添加到软件更新部署向导、自动部署规则向导和属性页中。 但是，这些选项当前都未在此技术预览中实现。  

##  <a name="BKMK_Remote"></a>远程设备操作的新体验  
 已改进从 Configuration Manager 控制台执行远程设备操作的体验。  
现在，常见操作（如“停用/擦除”、“重置密码”、“远程锁定”和“不使用激活锁”）可在从“资产和合规性”工作区访问的“远程设备操作”菜单中找到。  

 ![新的远程设备操作屏幕截图](media/New-Remote-Device-Actions.png)  

 这些操作的状态位于以下位置：  

-   从“设备”节点选择设备时，可查看详细内容窗格。  

-   设备的“属性”页。  

-   “设备”节点的主页（默认情况下，可能不会显示所有列）。  

 有关 iOS 绕过激活锁的详细信息，请参阅[通过 Configuration Manager 的绕过激活锁帮助保护 iOS 设备](/sccm/mdm/deploy-use/manage-ios-activation-lock)，特别是 **Configuration Manager Technical Preview 中绕过激活锁的当前已知问题**部分。  

##  <a name="BKMK_WSFB"></a>适用于企业的 Windows 应用商店应用  
 在[适用于企业的 Windows 应用商店](https://www.microsoft.com/business-store)中可以为组织查找并采购应用（单个或批量）。 通过将应用商店连接到 Configuration Manager，可从 Configuration Manager 控制台管理批量采购的应用，例如：  

-   可以将采购的应用列表与 Configuration Manager 同步  

-   同步的应用会出现在 Configuration Manager 控制台中，可以如同任何其他应用一样部署这些应用  

-   Configuration Manager 每 24 小时就会从应用商店中下载应用许可信息，你可在 Configuration Manager 控制台中进行查看  

 在 1604 技术预览版中，你可以从 Configuration Manager 控制台中的适用于企业的 Windows 应用商店进行同步并查看应用。 在此版本中，我们已添加从同步的应用商店应用创建和部署 Configuration Manager 应用程序的功能。  

### <a name="set-up-windows-store-for-business-synchronization"></a>设置适用于企业的 Windows 应用商店同步  

1.  在 Azure Active Directory 中，将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具。 这会为你提供以后将需要的客户端 ID。  

    1.  在 [https://manage.windowsazure.com](https://manage.windowsazure.com) 的 Active Directory 节点中，选择“Azure Active Directory”，然后单击“应用程序” > “添加”。  

    2.  单击“添加我的组织正在开发的应用程序”。  

    3.  为应用程序输入名称，选择“Web 应用程序”和/或“Web API”，然后单击“下一步”箭头。  

    4.  为**登录 URL**和**应用 ID URI** 输入相同 URL。 该 URL 可以是任何内容，无需解析为实际地址。 例如，可以输入 **https://&lt;yourdomain>/sccm**。  

    5.  完成向导。  

2.  在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。  

    1.  突出显示刚创建的应用程序，然后单击“配置”。  

    2.  在“密钥”下，从列表中选择持续时间，然后单击“保存”。 这创建新客户端密钥。 成功将适用于企业的 Windows 应用商店载入到 Configuration Manager 之前，请勿导航离开此页面。  

3.  在适用于企业的 Windows 应用商店中，将 Configuration Manager 配置为存储管理工具。  

    1.  打开 [https://businessstore.microsoft.com/zh-cn/managementtools](https://businessstore.microsoft.com/managementtools)，在出现提示时进行登录。  

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

### <a name="try-it-out"></a>试试看！  
 尝试完成以下任务，然后通过使用 Microsoft Connect 站点上 [Configuration Manager 反馈计划](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)页上的反馈表告知我们它的工作原理：  

 从适用于企业的 Windows 应用商店脱机许可应用创建和部署 Configuration Manager 应用程序。  

1.  在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。  

2.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，单击“创建应用程序”。  

 将创建包含适用于企业的 Windows 应用商店应用的 Configuration Manager 应用程序。 然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。  

> [!IMPORTANT]  
>  从脱机许可应用创建具有单一部署类型的 Configuration Manager 应用程序时，可将其部署到 MDM 托管并使用 Configuration Manager 客户端进行管理的设备。 如果尝试使用多种部署类型来部署一个应用，安装将失败。  
>   
>  当前无法使用 Configuration Manager 部署联机许可应用。  

##  <a name="BKMK_VPP2"></a>批量采购应用的一般改进  

-   在此版本中，来自适用于企业的 Windows 应用商店和 iOS 应用商店的批量采购应用已合并为同一个视图，即**应用商店应用的许可证信息**。  

-   对于 iOS 批量采购的应用，已从“创建应用程序”向导的“适用于 iOS 浏览器的应用包”对话框删除“Apple 批量采购计划”选项卡。 若要创建适用于 iOS 的批量采购应用，请使用以下步骤：  

    1.  1.  在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”。  

    2.  2.  选择要部署的应用，然后在“主页”选项卡的“创建”组中，单击“创建应用程序”。  

-   在 Configuration Manager 控制台中，用于获取和上传批量采购的应用的 Apple VPP 令牌的位置已更改。 你现在可以在“云服务” > “Apple 批量采购计划令牌”节点下的“管理”工作区中执行此操作。  

##  <a name="BKMK_VPP"></a>企业数据保护 (EDP)  
 你可创建配置项目来部署企业数据保护 (EDP) 策略，包括选择受保护的应用、EDP 保护级别和在网络上查找企业数据的方法。 有关 EDP 的详细信息，请参阅下列主题：  

-   [使用企业数据保护 (EDP) 保护公司数据](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp)  

-   [使用 System Center Configuration Manager 创建和部署企业数据保护 (EDP) 策略](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm)  

##  <a name="BKMK_End"></a>最终用户可从公司门户安装应用  
 System Center Configuration Manager 版本 1511 中引入了本地 MDM。 在以前的版本中，你可以将应用程序部署到 MDM 托管的 Windows 10 设备，部署目的在于为本地 MDM 托管设备提供**必需**的安装。  

 在此版本中，你现在可以部署应用，部署目的在于使这些应用对本地 MDM 托管的 Windows 10 计算机用户**可用**，并且用户现在可以从公司门户自行安装这些应用。
在此技术预览中，如果公司门户打开超过 15 分钟，则最终用户将看到一条错误消息。 重启公司门户可解决此问题。  

### <a name="before-you-start"></a>开始之前  

#### <a name="server-prerequisites"></a>服务器先决条件  

-   .NET 4.5 或更高版本（需要重启）  

-   用于配置脚本的 PowerShell 3.0（需要重启）  

#### <a name="client-prerequisites"></a>客户端先决条件  

-   Windows 10 桌面版 1511（OS 内部版本 10586.218）或更高版本  

#### <a name="general-prerequisites"></a>一般先决条件  

-   确保已完成[用于本地移动设备管理的准备步骤](https://technet.microsoft.com/library/mt613153.aspx)并[已注册设备](https://technet.microsoft.com/library/mt627870.aspx)。  

-   为了获得使用公司门户时的最佳应用程序安装体验，请确保 Configuration Manager 与 Microsoft Intune 之间已建立连接。  

-   如果选择批量注册选项，请在尝试此方案之前，为已注册设备配置用户服务相关性。  

### <a name="configuration-steps"></a>配置步骤  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>安装应用程序目录角色并启用移动设备管理支持  

1.  添加应用程序目录 Web 服务和网站角色  

    1.  选择“HTTPS 模式”和“允许移动设备使用此应用程序目录 Web 服务点”选项。  

    2.  此 Technical Preview 中的限制：  

        -   必须先卸载任何现有的应用程序目录角色，然后才能选择允许移动设备连接的选项。  

        -   确保仅有一组应用程序目录角色，并且这些角色与注册点和注册代理点角色位于同一站点系统上。  

2.  在 Configuration Manager 控制台中的“组件状态”节点验证以下组件是否可操作：  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>配置边界  
 为 Intranet 分发点配置所需的边界。  

> [!NOTE]  
>  目前移动设备管理仅支持 IPv4 范围边界。  

### <a name="deploy-the-company-portal-application-and-configuration"></a>部署公司门户应用程序和配置  

1.  使用此技术预览版随附的配置脚本准备公司门户部署和配置：  

    1.  打开已升级的 PowerShell 命令窗口。  

    2.  运行 **set-executionPolicy RemoteSigned**  

    3.  从文件夹 **&lt;SCCM 安装目录 \>\cd.latest\SMSSETUP\TOOLS\MDM** 运行 **.\ConfigurationScript.ps1**  

     此配置脚本可执行以下操作：  

    1.  使用同一文件夹中的 **CompanyPortalOnPremisesMDM.appx** 创建包含 Windows 应用包部署类型的 Configuration Manager 应用程序。  

    2.  创建配置公司门户的配置项目和配置基线。  

    3.  部署配置基线和应用程序，并将应用程序添加到所有分发点。  

    > [!NOTE]  
    >  如果应用程序目录角色不与主站点位于同一处，请执行以下操作：  
    >   
    >  -   在“资产和符合性”工作区中，找到“OnPremMDM 门户配置 CI - 服务器 URL”配置项目  
    > -   将“符合性规则”值更改为其中包含应用程序目录角色的站点系统的完全限定的域名。  

2.  部署公司门户应用程序及其配置后，使用 Configuration Manager 控制台的“部署”部分验证给定设备的应用程序和配置基线是否符合。 在设备上的“开始”菜单中，公司门户将显示为“公司门户 (Technical Preview)”。  

### <a name="try-it-out"></a>试试看！  
 尝试完成以下任务，然后通过使用 Microsoft Connect 站点上 [Configuration Manager 反馈计划](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)页上的反馈表告知我们它的工作原理：  

1.  使用支持的部署类型为用户集合部署多个应用程序，部署目的为**可用**。 对于此技术预览版，未经管理员批准的应用程序将不受支持，并且不会显示在公司门户中。  

2.  然后用户可以从公司门户浏览并安装应用。  

     打开公司门户后，将看到名为 **System Center Configuration Manager** 的身份验证对话框，指定用户用以登录的 Active Directory 凭据（以 user@domain 或域\用户的形式）。  

##  <a name="BKMK_SW1"></a>软件中心中的更新和操作系统的新选项卡  
 在此版本中，已进行以下更改以改进软件中心应用程序的布局：  

-   “应用程序”选项卡已被拆分为三个单独的“更新”、“操作系统”（这两者之前位于“筛选器”列表中）和“应用程序”选项卡。  

##  <a name="BKMK_ServerGroups"></a>维护服务器组  
 System Center Configuration Manager Technical Preview 版本 1511 中有一个创建集合的功能，其中集合中的所有设备组成了一个服务器组。 而且，在将软件更新部署到服务器组中时，可以部署要使用的服务器组设置、控制在任何给定时间内更新的计算机百分比，以及配置要运行自定义操作的前期部署和后期部署 PowerShell 脚本。  

 System Center Configuration Manager Technical Preview 1605 版中新增了在服务器组中按定义的指定顺序更新计算机的功能，添加了增强型监视，以便在服务器组中查看计算机的状态，并提供了清除部署锁定的功能，当在客户端无法安装软件更新并阻止其他客户端安装其软件更新时，此功能会非常有用。  

### <a name="try-it-out"></a>试试看！  
 尝试完成以下任务，然后通过使用 Microsoft Connect 站点上 [Configuration Manager 反馈计划](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)页上的反馈表告知我们它的工作原理：  

-   我可以创建表示服务器组的集合。 对于此测试，可以将收集成员身份规则配置为在此集合中具有 2 台计算机。   

-   我可以根据此集合的服务器组设置指定服务器组中的计算机按特定的顺序安装软件更新。 使用过程中的示例脚本来指定预先部署脚本和后期部署脚本。  

-   我可以将软件更新部署到此集合。 查看 C:\temp 中的 start.txt 和 end.txt 文件（从示例脚本创建），并验证服务器组中计算机上的部署开始和结束时间。 有关详细信息，请查看 UpdatesDeployment.log 文件。  

#### <a name="to-create-a-collection-for-a-server-group"></a>创建服务器组的集合  

1.  [创建一个设备集合](https://technet.microsoft.com/library/gg712295.aspx)，使其包含服务器组中的计算机。  

2.  在“资产和符合性”工作区中，单击“设备集合”，右键单击包含服务器组中的计算机的集合，然后单击“属性”。  

3.  在“常规”选项卡上，选择“所有设备均为相同服务器组的一部分”，然后单击“设置”。  

4.  在“服务器组设置”页上指定下列设置之一：  

    -   **允许同时更新一定比例的计算机**：指定仅特定比例的客户端可在任意某个时间进行更新。 例如，如果集合中有 10 个客户端，并且配置该集合为可同时更新 30% 的客户端，则在任何给定时间只有 3 个客户端可安装软件更新。  

    -   **允许同时更新一定数量的计算机**：指定仅特定数量的客户端可在任意某个时间进行更新。  

    -   **指定维护顺序**：指定集合中的客户端将按配置的顺序一次更新一个。 列表中位于某客户端前面的客户端完成安装其软件更新后，该客户端才能安装软件更新。  

5.  指定是否使用部署前（节点排出）脚本或部署后（节点恢复）脚本。  

    > [!TIP]  
    >  以下是可用于测试当前时间写入文本文件的部署前和部署后脚本的示例：  
    >   
    >  **前期部署**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **后期部署**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>将软件更新部署到服务器组并监视状态  

1.  将[软件更新部署](https://technet.microsoft.com/library/gg712304.aspx)到服务器组集合。  

2.  [监视软件更新部署](https://technet.microsoft.com/library/gg712304.aspx)。 除了软件更新部署的标准监视视图之外，客户端在等待安装软件更新时，还将显示新的状态说明。 这一新状态显示为**等待锁定**。  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>清除服务器组中计算机的部署锁定  

1.  在“资产和符合性”工作区中，单击“设备集合”，然后单击要清除部署锁定的集合。  

2.  在“主页”选项卡的“部署”组中，单击“清除服务器组部署锁定”。 当客户端未能安装软件更新并阻止其他客户端安装其软件更新时，可以手动清除部署锁定。  

##  <a name="BKMK_ATP"></a>支持 Windows Defender 高级威胁防护服务  
 Windows Defender 高级威胁防护 (ATP) 是一种新服务，可帮助企业检测、调查其网络上的高级攻击并对此做出响应。 了解有关 [Windows Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection) 的详细信息。 Configuration Manager 有助于你载入和监视托管的 Windows 10 周年纪念版客户端设备。  

### <a name="try-it-now"></a>立即试试看！  
 尝试完成以下任务，然后通过使用 Microsoft Connect 站点上 [Configuration Manager 反馈计划](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)页上的反馈表告知我们它的工作原理：  

-   Windows Defender 高级威胁防护 (ATP) 联机服务的机载设备  

-   监视托管设备的 Windows Defender ATP 部署  

 **先决条件**  

-   Windows Defender 高级威胁防护联机服务的订阅  

-   运行 Windows 10 周年纪念版（内部版本 14328 及更高版本）的客户端  

-   创建客户端载入配置文件  

    ##### <a name="how-to-create-an-onboarding-configuration-file"></a>如何创建载入配置文件  

    1.  登录到 Windows Defender ATP 联机服务  

    2.  单击“客户端载入”菜单项  

    3.  选择“System Center Configuration Manager”，然后单击“下载包”。  

    4.  下载压缩的存档 (.zip) 文件并将内容解压缩。  


##### <a name="onboard-devices-for-windows-defender-atp"></a>Windows Defender ATP 的机载设备  

1.  在 Configuration Manager 控制台中，导航到“资产和符合性” > “概述” > “Endpoint Protection” > “Windows Defender ATP 策略”，然后单击“创建 Windows Defender ATP 策略”。 将打开 Windows Defender ATP 策略向导。  

2.  键入 Windows Defender ATP 策略的**名称**和**说明**，然后选择“载入”。 单击“下一步”。  

3.  **浏览**到组织的 Windows Defender ATP 云服务租户提供的配置文件。 单击“下一步”。  

4.  指定从托管设备收集和共享的文件示例以进行分析。  

    -   **无** - 没有收集示例文件进行分析  

    -   **可移植可执行文件** - 收集并共享可在网络攻击中利用的文件（例如程序文件 (.exe)、动态库链接 (.dll) 文件、字体文件，以及类似文件），以进行分析  

     单击“下一步” 。  

5.  查看摘要，然后完成该向导。  

6.  通过单击“部署”，现在可以将 Windows Defender ATP 策略部署到托管客户端计算机。  

##### <a name="monitor-windows-defender-atp"></a>监视 Windows Defender ATP  

1.  在 Configuration Manager 控制台中，导航到“监视” > 概述” > “安全”，然后单击“Windows Defender ATP”。  

2.  查看 Windows Defender 高级威胁防护仪表板。  

    -   **Windows Defender 代理部署状态** - 合格托管客户端计算机（已载入活动 Windows Defender ATP 策略）的数量和百分比  

    -   **Windows Defender ATP 代理运行状况** - 报告其 Windows Defender ATP 代理状态的计算机客户端的百分比  

        -   **运行状况** - 运行正常  

        -   **非活动** - 在时间段内没有数据发送到服务  

        -   **代理状态** - Windows 中代理的系统服务未运行  

        -   **未载入** - 策略已应用，但代理尚未报告载入策略  

##  <a name="BKMK_DHA"></a>本地设备运行状况证明  
 Windows 10 设备的运行状况证明现在可以配置为使用本地基础结构进行通信。 管理员可以指定是通过云还是本地资源进行报告。 如果为运行状况证明报告选择“本地”，则可以为服务指定 URL。 这使无法进行 Internet 访问的客户端电脑可以启用和管理使用运行状况证明的设备。  

### <a name="enable-health-attestation-for-on-premises-devices"></a>为本地设备启用运行状况证明  
 在 1605 中，我们修复了几个在 1604 Technical Preview 中发现的 bug。  若要进行尝试，请使用客户端代理设置配置本地运行状况证明服务。  

1.  在 Configuration Manager 控制台中，导航到“管理” > “概述” > “客户端设置”，然后将“使用本地运行状况证明服务”设置为“是”。  

2.  指定**本地运行状况证明服务 URL**，然后单击“确定”。  

##  <a name="BKMK_RestartOptions"></a>在软件更新安装之后重启 Windows 10 客户端的新选项  
 当需要重启的软件更新已使用 Configuration Manager 进行部署并且已安装在一台计算机上时，将计划挂起的重启并显示重启对话框。 当前，对于 Windows 8 和更高版本，如果使用 Windows 电源选项（而不是从重启对话框）关闭或重启计算机，计算机重启后“重启”对话框仍然保留并且计算机在配置的截止时间仍将需要重启。 在此技术预览中，只要 Configuration Manager 软件更新存在挂起的重启，Windows 10 计算机上的 Windows 电源选项中就将出现“更新并重启”和“更新并关闭”选项。 使用这些选项中的某一个后，计算机重启后将不再显示重启对话框。  

##  <a name="BKMK_IMEI"></a>预声明具有 IMEI 或 iOS 序列号的公司拥有的设备  
 现在，可通过导入公司拥有的设备的国际移动设备识别 (IMEI) 码对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。  还可以导入 iOS 设备的序列号。  导入的信息将用于设置注册为“公司”的设备的所有权。  访问该服务的每位用户仍需要 Intune 许可证。  

### <a name="try-it-out"></a>试试看！  
 尝试完成以下任务，然后通过使用 Microsoft Connect 站点上 [Configuration Manager 反馈计划](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback)页上的反馈表告知我们它的工作原理：  

-   将一组 IMEI 号码导入到 .csv 文件中。 每一行均包含 IMEI 号码，后跟详细信息字段。  

-   从 Configuration Manager 控制台手动导入 IMEI 号码。  

-   将一组 iOS 序列号导入到 .csv 文件中。 同样，每一行均包含一个号码，后跟有关设备的任何详细信息。  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>预声明具有 IMEI 或 iOS 序列号的公司拥有的设备  

1.  在 Configuration Manager 控制台中，转到“资产和符合性” > “概述” > “公司拥有的所有设备” > “预声明设备”，然后单击“创建预声明设备”。 将打开“预声明设备”向导。  

2.  指定添加设备信息的方式：  

    -   **上传包含 IMEI 号码和详细信息的 .csv 文件** - 若要上传号码列表，请参阅步骤 #3。  

    -   **手动添加 IMEI 号码和详细信息** - 若要手动输入信息，请键入 IMEI 号码或 iOS 序列号和设备的详细信息，然后继续执行步骤 #4。  

3.  对于已上传的文件，浏览到包含信息的 .csv 文件，以预声明公司拥有的设备。 该文件必须具有以下格式，顶行（仅提供指导）除外：  

    |**IMEI 号码**|**iOS 序列**|**OS**|**详细信息**|
    |---|---|---|---|
    |123456789012345||WINDOWS|公司拥有的 Windows 设备|
    |123456789012|A0BCD0EFGH0J|IOS|公司拥有的 iOS 设备|
    |123456789012346||ANDROID|公司拥有的 Android 设备|

     **列：**  

    -   第 1 列：IMEI 号码 - 每行都必须提供 IMEI 号码或 iOS 序列号  

    -   第 2 列：iOS 序列号 - 仅可预声明 iOS 序列号。 将 IMEI 号码用于其他设备平台  

    -   第 3 列：设备的操作系统（需要大写）：  

        -   IOS - 所有 iOS 设备  

        -   WINDOWS - 包括 Windows Phone、Windows 10 Mobile 和 Windows 电脑  

        -   ANDROID - 所有 Android 设备  

    -   第 4 列：详细信息 - Configuration Manager 控制台中显示的其他设备信息  

     单击“下一步” 。  

4.  查看文件导入的结果。 以前导入的 IMEI 或序列号会将其详细信息更新为新的详细信息。  单击“下一步”继续，或单击“返回”保存更新后的详细信息，然后完成向导。  
