---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: 了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1709 中的可用功能。
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79d7488e0554a36eb274bf4ef76cff92b48a71ba
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418435"
---
# <a name="capabilities-in-technical-preview-1709-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1709 中的功能

适用范围：*System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview（版本 1709）中的可用功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 中的已知问题：**
- 如果站点服务器处于被动模式，则无法更新到预览版本 1709。 如果运行的是预览版本 1706、1707 或 1708，且[主站点服务器处于被动模式](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)，则必须先卸载被动模式站点服务器，然后才能将预览站点成功更新到版本 1709。 可以在站点运行版本 1709 后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。


**以下是此版本可以试用的新功能。**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Configuration Manager 控制台中改进了 VPN 配置文件体验
<!-- 1313282 --> 在此版本中，我们更新了 VPN 配置文件向导和属性页，以显示选定平台相应的设置。 具体而言：

- 每个平台均有其自己的工作流，这意味着新的 VPN 配置文件仅包含平台支持的设置。
- 如今，“支持的平台”页在“常规”页后显示。  现在于设置属性值之前选择平台。
- 如果将平台设置为“Android”、“Android for Work”或“Windows Phone 8.1”，则不需要“支持的平台”页，该页也不会显示。
- 基于 Configuration Manager 客户端的工作流已与基于混合移动设备 (MDM) 客户端的 Windows 10 工作流相结合，它们支持相同的设置。
- 每个平台工作流仅包含适用于该工作流的设置。  例如，Android 工作流包含适用于 Android 的设置；Android 工作流中将不再显示适用于 iOS 或 Windows 10 移动版的设置。
- 对于 Windows 8.1 设备，清楚标记了 Configuration Manager 管理的设置。
- “自动 VPN”页已过时且已删除。

这些更改适用于新的 VPN 配置文件。  

为把兼容性风险降至最低，现有的 VPN 配置文件保持不变。  编辑现有的配置文件时，设置将以创建该配置文件时的形式显示。  

### <a name="try-it-out"></a>试试看！

使用常用流程创建新的 VPN。 请注意，VPN 配置文件向导选项的首页已更改。

1.  请转到“资产和符合性” > “概述” > “符合性设置” > “公司资源访问权限” > “VPN 配置文件”，然后选择“创建 VPN 配置文件”。
2.  在“常规”页中输入名称，然后选择“指定要创建的 VPN 配置文件类型”下的以下选项之一：

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS 和 macOS  
    - Android  
    - Android for Work  

3.  如果选择“Windows 8.1”，则也可选择“创建新的配置文件”或“从文件导入”。
4.  完成向导，结束配置文件创建。

请注意，选择不同的平台时，只显示与选定平台相关的设置。

## <a name="co-management-for-windows-10-devices"></a>适用于 Windows 10 设备的共同管理    
<!-- 1350871 --> 许多客户想要使用一种基于云的简单低成本解决方案通过管理移动设备的相同方式来管理 Windows 10 设备。 然而，实现从传统管理到现代管理的转换可能具有挑战性。 从 Windows 10 版本 1607（也称为周年更新）开始，可以将 Windows 10 设备同时联接到本地 Active Directory (AD) 和基于云的 Azure AD（混合 Azure AD）。 共同管理将利用此项改进，并使你能够同时使用 Configuration Manager 和 Intune 来管理 Windows 10 设备。 它是一种解决方案，在传统管理与现代管理之间架起一座桥梁，为你提供利用分阶段的方法实现转换的途径。 

### <a name="prerequisites"></a>先决条件
必须具备以下先决条件才能实现共同管理。 存在一般先决条件，以及针对现有 Configuration Manager 客户端和不属于该客户端的设备的不同先决条件。

### <a name="known-issues"></a>已知问题
创建共同管理策略后，无法编辑该策略。 若要更改策略，需将其删除，然后使用所需设置重新创建它。 

#### <a name="general-prerequisites"></a>一般先决条件
以下是实现共同管理的一般先决条件：  

- Configuration Manager Technical Preview 1709 版本
- Azure AD 
- 适用于所有用户的 EMS 或 Intune 许可证
- Intune 订阅（Intune 中的 MDM 机构设置为 Intune）

   > [!Note]  
   > 如果具有混合 MDM 环境（Intune 与 Configuration Manager 集成），则无法实现共同管理。 如果有兴趣迁移到 Intune 独立版本，请参阅[从混合 MDM 迁移到 Intune 独立版本](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>针对现有 Configuration Manager 客户端的其他先决条件
- Windows 10，版本 1709 (Fall Creators Update) 及更高版本
- 已联接混合 Azure AD（联接到 AD 和 Azure AD）

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>针对新 Windows 10 设备的其他先决条件
- Windows 10，版本 1709 (Fall Creators Update) 及更高版本
- Configuration Manager 中的[云管理网关](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)

### <a name="workloads-you-can-switch-to-intune"></a>可以切换到 Intune 的工作负荷
启用共同管理后，Configuration Manager 将继续管理所有工作负荷。 如果决定已准备就绪，即可使 Intune 开始管理可用的工作负荷。 在此版本中，可以使 Intune 管理以下工作负荷。   

#### <a name="compliance-policies"></a>相容性策略
符合性策略定义设备必须遵从的规则和设置，以便将设备视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。 有关详细信息，请参阅[设备符合性策略](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/device-compliance-policies)。  

#### <a name="windows-update-for-business-policies"></a>适用于企业的 Windows 更新策略
通过适用于企业的 Windows 更新策略，可以针对 Windows 10 功能更新或直接由适用于企业的 Windows 更新托管的 Windows 10 设备的质量更新，配置延迟策略。 有关详细信息，请参阅[配置适用于企业的 Windows 更新延迟策略](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)。  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Azure 上 Intune 中适用于共同管理设备的可用远程操作
如果为 Windows 10 设备启用了共同管理，在 Azure 上的 Intune 中可以执行以下远程操作：  
- [恢复出厂设置](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [选择性擦除](https://docs.microsoft.com/intune/apps-selective-wipe)
- [删除设备](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [重启设备](https://docs.microsoft.com/intune/device-restart)
- [全新启动](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>准备 Intune 进行共同管理
将工作负荷从 Configuration Manager 切换到 Intune 之前，在 Intune 中创建所需的配置文件和策略，以确保设备继续受保护。
可以根据 Configuration Manager 中包含的对象在 Intune 中创建对象。 或者，如果当前策略基于旧式或传统管理，可能需要退后一步，重新思考现代管理需要哪些策略和配置文件。 使用以下资源创建策略和配置文件。    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [适用于企业的 Windows 更新策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [设备配置文件](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>共同管理体系结构概述
下图提供共同管理的体系结构概述，以及它如何适用于现有的配置和 Intune 基础结构。

![共同管理体系结构关系图](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>启用共同管理的方案  
可以对在 Microsoft Intune 和现有 Windows 10 Configuration Manager 客户端中注册的 Windows 10 设备启用共同管理。 这两种方案都将导致 Windows 10 设备由 Configuration Manager 和 Intune 同时管理，并联接到 AD 和 Azure AD。  

#### <a name="devices-enrolled-in-intune"></a>在 Intune 中注册的设备  
如果在 Intune 中注册 Windows 10 设备，可在设备上安装 Configuration Manager 客户端（使用特定的命令行参数），使客户端准备好进行共同管理。 然后，从 Configuration Manager 控制台中启用共同管理，开始针对特定 Windows 10 设备将特定的工作负荷移动到 Intune。  

对于尚未在 Intune 中注册的 Windows 10 设备，可以在 Azure 中使用自动注册来注册设备。 对于新的 Windows 10 设备，可以使用 Windows AutoPilot 配置全新体验 (OOBE)，其中包括在 Intune 中注册设备的自动注册。  

#### <a name="configuration-manager-clients"></a>Configuration Manager 客户端
如果具有属于 Configuration Manager 客户端的 Windows 10 设备，可注册设备并从 Configuration Manager 控制台启用共同管理。 Configuration Manager 根据 Azure AD 租户信息将自动注册触发到 Intune。  

### <a name="prepare-windows-10-devices-for-co-management"></a>准备 Windows 10 设备进行共同管理
可对已联接 AD 和 Azure AD 并在 Intune 中注册的 Windows 10 设备和 Configuration Manager 中的客户端启用共同管理。 对于新的 Windows 10 设备和已在 Intune 中注册的设备，请在可以进行共同管理前先安装 Configuration Manager 客户端。 对于已属于 Configuration Manager 客户端的 Windows 10 设备，可向 Intune 注册设备并在 Configuration Manager 控制台中启用共同管理。

#### <a name="command-line-to-install-configuration-manager-client"></a>安装 Configuration Manager 客户端的命令行
在适用于 Windows 10 设备（还不是 Configuration Manager 客户端）的 Intune 中创建应用。 在下一节中创建应用时，请使用以下命令行：

ccmsetup.msi CCMSETUPCMD="/mp:<云管理网关相互身份验证终结点 URL>/ CCMHOSTNAME=<云管理网关相互身份验证终结点 URL> SMSSiteCode=<站点代码> SMSMP=https://<MP 的 FQDN> AADTENANTID=<AAD 租户 ID> AADTENANTNAME=<租户名> AADCLIENTAPPID=<AAD 集成的 Server AppID> AADRESOURCEURI=https://<资源 ID>”

例如，如果具有以下值：

- 云管理网关相互身份验证终结点 URL： https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >对于云管理网关相互身份验证终结点 URL 值，使用 vProxy_Roles SQL 视图中的 MutualAuthPath 值。

- 管理点 (MP) 的 FQDN：sccmmp.corp.contoso.com    
- **站点代码**：PS1    
- **Azure AD 租户 ID**：72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- Azure AD 租户名称：contoso    
- Azure AD 客户端应用 ID：bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **AAD 资源 ID URI**：ConfigMgrServer    

  > [!Note]    
  > 对于 AAD 资源 ID URI 值，使用在 vSMS_AAD_Application_Ex SQL 视图中找到的 IdentifierUri 值。

将使用以下命令行：

ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https://sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https://ConfigMgrServer”

> [!Tip]
>可通过使用以下步骤查找站点的命令行参数：     
> 1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。  
> 2. 在“主页”选项卡的“管理”组中，选择“配置共同管理”以打开“共同管理载入”向导。 ****    
> 3. 在“订阅”页中，单击“登录”并登录到 Intune 租户，然后单击“下一步”。    
> 4. 在“启用”页面的“在 Intune 中注册的设备”部分中单击“复制”，将命令行复制到剪贴板，然后将其保存，用在创建应用的过程中。  
> 5. 单击“取消”退出向导。

#### <a name="new-windows-10-devices"></a>新的 Windows 10 设备
对于新的 Windows 10 设备，可以使用 Autopilot 服务来配置全新体验，这包括将设备联接到 AD 和 Azure AD，以及在 Intune 中注册设备。 然后，在 Intune 中创建应用，部署 Configuration Manager 客户端。  
1. 对新的 Windows 10 设备启用 AutoPilot。 有关详细信息，请参阅 [Windows AutoPilot 概述](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)。  
2. 为设备在 Azure AD 中配置自动注册，以自动向 Intune 注册设备。 有关详细信息，请参阅 [针对 Microsoft Intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。
3. 使用 Configuration Manager 客户端程序包在 Intune 中创建应用，并将应用部署到要共同管理的 Windows 10 设备中。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>未在 Intune 中注册或不是 Configuration Manager 客户端的 Windows 10 设备
对于未在 Intune 中注册或不是 Configuration Manager 客户端的 Windows 10 设备，可以使用自动注册在 Intune 中注册设备。 然后，在 Intune 中创建应用，部署 Configuration Manager 客户端。
1. 为设备在 Azure AD 中配置自动注册，以自动向 Intune 注册设备。 有关详细信息，请参阅 [针对 Microsoft Intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。  
2. 使用 Configuration Manager 客户端程序包在 Intune 中创建应用，并将应用部署到要共同管理的 Windows 10 设备中。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。

#### <a name="windows-10-devices-enrolled-in-intune"></a>在 Intune 中注册的 Windows 10 设备
对于已在 Intune 中注册的 Windows 10 设备，在 Intune 中创建应用，以部署 Configuration Manager 客户端。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。  

### <a name="switch-configuration-manager-workloads-to-intune"></a>将 Configuration Manager 工作负荷切换到 Intune
在上一节中，你准备了 Windows 10 设备进行共同管理。 这些设备现已联接到 AD 和 Azure AD，并且它们已在 Intune 中注册，具有 Configuration Manager 客户端。 你可能仍然具有已联接到 AD 且具有 Configuration Manager 客户端的 Windows 10 设备，但该设备未联接到 Azure AD 或在 Intune 中注册。 以下步骤介绍如何启用共同管理，准备其余的 Windows 10 设备（没有进行 Intune 注册的 Configuration Manager 客户端）进行共同管理，并允许开始将特定的 Configuration Manager 工作负荷切换到 Intune。

1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。    
2. 在“主页”选项卡的“管理”组中，选择“配置共同管理”以打开“共同管理载入”向导。 ****    
3. 在“订阅”页中，单击“登录”并登录到 Intune 租户，然后单击“下一步”。   
4. 在“暂存”页中，配置以下设置并单击“下一步”：
    - **试点组**：试点组包含选定的一个或多个集合。 在分阶段推出共同管理过程中使用此组。 可从小型测试集合开始，然后随着向更多用户和设备推出共同管理，向试点组添加更多集合。 可随时在共同管理属性中更改试点组中的集合。
    - **生产**：如果选择此设置，将对所有支持的 Windows 10 设备启用共同管理。 使用一个或多个集合配置排除组。 将不对属于此组中任意集合的成员的设备使用共同管理。 
5. 在“启用”页中，选择“试点”或“全部”（具体取决于“暂存”页中所配置的设置），在 Intune 中启用自动注册，然后单击“下一步”。 如果选择“试点”，仅属于试点组成员的 Configuration Manager 客户端可在 Intune 中自动注册。 这使你能够对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。 
6. 在“工作负荷”页中选择是否将 Configuration Manager 工作负荷切换为由 Intune 托管，然后单击“下一步”。 使用滑块来选择是否将工作负荷切换到试点组或所有 Windows 10 设备（具体取决于在“暂存”页中所配置的设置）。 
7. 要启用共同管理，请完成向导。  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>另请参阅
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。 
