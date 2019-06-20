---
title: 教程：为现有 Configuration Manager 客户端启用共同管理
titleSuffix: Configuration Manager
description: 在已使用 Configuration Manager 管理 Windows 10 设备时，在 Microsoft Intune 中配置共同管理。
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b19f54d60ed0594be4a51b5abcef69304a27ece
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834765"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>教程：为现有 Configuration Manager 客户端启用共同管理
通过共同管理，可以保持完善的流程，以便使用 Configuration Manager 管理组织中的电脑。 同时，通过使用 Intune 在云上投入，实现安全性和新式预配。  

在本教程中，你对已在 Configuration Manager 中注册的 Windows 10 设备设置共同管理。 开始学习此教程的前提是，你已使用 Configuration Manager 来管理 Windows 10 设备。

若要使用本教程，需要具备以下条件：  

- 具有可以连接到混合 Azure AD 配置中的 Azure Active Directory (Azure AD) 的本地 Active Directory。 

  如果无法部署联接本地 AD 与 Azure AD 联接的混合 Azure Active Directory (AD)，建议学习我们的配套教程：[为基于 Internet 的新 Windows 10 设备启用共同管理](/sccm/comanage/tutorial-co-manage-new-devices)。 
- 具有想要进行云附加的 Configuration Manager 客户端。


**在本教程中，你将：**  
> [!div class="checklist"]  
> * 检查 Azure 和本地环境的先决条件  
> * 设置混合 Azure AD  
> * 配置 Configuration Manager 客户端代理以注册 Azure AD  
> * 将 Intune 配置为自动注册设备  
> * 将 Intune 许可证分配给用户  
> * 在 Configuration Manager 中启用共同管理  


## <a name="prerequisites"></a>先决条件  

### <a name="azure-services-and-environment"></a>Azure 服务和环境
- Azure 订阅（[免费试用版](https://azure.microsoft.com/free)）
- Azure Active Directory Premium
- Microsoft Intune 订阅
  > [!TIP]  
  > 企业移动性 + 安全性 (EMS) 订阅包括 Azure Active Directory Premium 和 Microsoft Intune。 EMS 订阅（[免费试用版](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)）。  

如果环境中尚不存在，在学习本教程期间，你将：
- 为用户分配 Intune 和 Azure Active Directory Premium 许可证
- 在本地 Active Directory 和 Azure Active Directory (AD) 租户之间配置 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation)


### <a name="on-premises-infrastructure"></a>本地基础结构
- [受支持的](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) System Center Configuration Manager Current Branch 版本
- 必须将 [MDM 机构](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority)设置为 Intune  


### <a name="permissions"></a>权限
在本教程中，请使用以下权限来完成各项任务：  
- Azure 中的全局管理员帐户  
- 本地基础结构上的域管理员帐户  
- Configuration Manager 中所有范围的完全权限管理员帐户   

## <a name="set-up-hybrid-azure-ad"></a>设置混合 Azure AD
设置混合 Azure AD 时，实际上是使用 Azure AD Connect 和 Active Directory 联合身份验证服务 (ADFS) 来设置本地 AD 与 Azure AD 的集成。 成功配置后，工作人员可以使用其本地 AD 凭据无缝登录到外部系统。

> [!IMPORTANT]  
> 本教程详细介绍了为托管域设置混合 Azure AD 的基本过程。 建议你熟悉此过程，而不依赖于本教程引导你了解和部署混合 Azure AD。
>
> 有关混合 Azure AD 的详细信息，请先参阅 Azure Active Directory 文档中的以下文章：
> - [规划 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [规划混合 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [控制设备的混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [为联盟域配置混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>设置 Azure AD Connect  
混合 Azure AD 需要配置 Azure AD Connect，以使本地 Active Directory (AD) 中的计算机帐户和 Azure AD 中的设备对象保持同步。

从版本 1.1.819.0 开始，Azure AD Connect 提供了配置混合 Azure AD 联接的向导。 使用该向导可简化配置过程。  

若要配置 Azure AD Connect，需要 Azure AD 租户的全局管理员凭据。  

> [!TIP]  
> 以下过程不应被视为是设置 Azure AD Connect 的权威方法，但在这里提供此方法旨在帮助简化在 Intune 和 Configuration Manager 之间配置共同管理的过程。 有关此过程的权威内容和与设置 Azure AD 相关的过程，请参阅 Azure AD 文档中的[为托管域配置混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)。  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>使用 Azure AD Connect 配置混合 Azure AD 联接

1. 获取和安装[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594)（1.1.819.0 或更高版本）。  
2. 启动 Azure AD Connect，然后选择“配置”。
3. 在“其他任务”页上，选择“配置设备选项”，然后选择“下一步”。
4. 在“概述”页上，选择“下一步”。
5. 在“连接到 Azure AD”页上，输入 Azure AD 租户的全局管理员凭据。
6. 在“设备选项”页上，选择“配置混合 Azure AD 联接”，然后选择“下一步”。
7. 在“设备操作系统”页上，选择 Active Directory 环境中的设备所使用的操作系统，然后选择“下一步”。  

   可以选择支持 Windows 下层加入域的设备的选项，但请记住，仅 Windows 10 支持设备的共同管理。
8. 在“SCP’页上，对于想要 Azure AD Connect 配置服务连接点 (SCP) 的每个本地林，执行以下步骤，然后选择“下一步”：  
   1. 选择林。  
   2. 选择身份验证服务。  如果具有联盟域，选择 AD FS 服务器，除非贵组织具有专门的 Windows 10 客户端且已配置计算机/设备同步或组织正在使用 [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)。  
   3. 单击“添加”以输入企业管理员凭据。  
9. 如果有托管域，则跳过此步骤。  

   在“联合身份验证配置”页上，输入 AD FS 管理员的凭据，然后选择“下一步”。
10. 在“已准备好进行配置”页上，选择“配置”。
11. 在“配置完成”页上，选择“退出”。

如果在完成已加入域的 Windows 设备的混合 Azure AD 联接时遇到问题，请参阅[针对 Windows 当前设备混合 Azure AD 联接的故障排除](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)。


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>配置客户端设置，以引导客户端注册 Azure AD  
使用客户端设置将 Configuration Manager 客户端配置自动注册 Azure AD。  

1. 打开“Configuration Manager 控制台” > “管理” > “概述” > “客户端设置”，然后编辑“默认客户端设置”。  

2. 选择“云服务”。  

3. 在“默认设置”页上，将“在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备”设置为 =“是”。  

4. 选择“确定”以保存此配置。  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>配置设备自动注册到 Intune   
接下来，我们将在 Intune 中设置设备的自动注册。 借助自动注册，使用 Configuration Manager 管理的设备将在 Intune 中自动注册。

自动注册还允许用户将其 Windows 10 设备注册到 Intune。 在以下情况中注册设备：用户将其工作帐户添加到其个人拥有的设备，或将企业拥有的设备加入到 Azure Active Directory。  

1. 登录到 [Azure 门户](https://portal.azure.com/)，然后选择“Azure Active Directory” > “移动性(MDM 和 MAM)” > “Microsoft Intune”。  

2. 配置“MDM 用户范围”。 指定以下任一设置以配置由 Microsoft Intune 管理的用户设备并接受 URL 值的默认值。  

   - “部分”- 选择可自动注册其 Windows 10 设备的“组”  

   - “全部”- 当设置为“无”时，所有用户都可以自动注册其 Windows 10 设备，移动设备管理 (MDM) 自动注册将遭禁用

   > [!IMPORTANT]  
   > 如果为某个组同时启用了“MAM 用户范围”和自动 MDM 注册（MDM 用户范围），则仅启用 MAM。 当该组中用户的工作区加入个人设备时，仅为这些用户添加移动应用程序管理 (MAM)。 设备不会自动注册 MDM。  

3. 选择“保存”以完成自动注册的配置。  

4. 返回到“移动性(MDM 和 MAM)”，然选择“Microsoft Intune 注册”。  

5. 对于 MDM 用户范围，选择“全部”，然后选择“保存”。  


## <a name="assign-intune-licenses-to-users"></a>将 Intune 许可证分配给用户   
有一个关键操作（但这个操作通常被忽略）是向将要使用共同管理的设备的每个用户分配 Intune 许可证。  

若要将许可证分配给用户组，请使用 Azure Active Directory。  

1. 使用管理员帐户登录到 [Azure 门户](https://portal.azure.com/)。 若要管理许可证，该帐户必须是全局管理员角色或用户帐户管理员。  

2. 选择左侧导航窗格中的“所有服务”，然后选择“Azure Active Directory”。  

3. 在“Azure Active Directory”窗格上，选择“许可证”以打开窗格，可以在此处查看和管理租户中的所有可许可的产品。  

4. 在“所有产品”下，选择包含 Intune 许可证的产品选项，然后选择窗格顶部的“分配”。  

   例如，如果是要获取 Intune，可以选择“企业移动性 + 安全性 E5”。  

5. 在“分配许可证”窗格上，单击“用户和组”打开“用户和组”窗格。 选择要为其分配许可证的组和单个用户。  然后，单击窗格底部的“选择”以确认所选内容。  

6. 在“分配许可证”窗格上，单击“分配选项”以显示之前选择的产品中包含的所有服务计划。 如果选中某个产品（如 Intune），则仅显示该产品。  
   - 将“Microsoft Intune”设置为“启用”。  
   - 为每个用户分配 Azure Active Directory Premium 许可证。  

   分配适用的许可证后，选择“确定”。  

7. 若要完成分配，在“分配许可证”窗格上，单击窗格底部的“分配”。

8. 右上角随即出现一条通知，显示过程的状态和结果。 如果无法完成组的分配（例如，由于组中预先存在的许可证），单击该通知以查看失败的详细信息。

有关向用户分配 Intune 许可证的详细信息，请参阅[分配许可证](https://docs.microsoft.com/intune/licenses-assign)。


## <a name="enable-co-management-in-configuration-manager"></a>在 Configuration Manager 中启用共同管理
混合 Azure AD 设置后，Configuration Manager 客户端配置就绪，并向用户分配了产品许可证，现在你可以切换开关并启用 Windows 10 设备的共同管理。  

> [!TIP]  
>  在以下过程的第六步中，你将指定一个集合作为共同管理的试点组。 此组包含少量客户端，用于测试共同管理配置。 建议在开始此过程前先创建合适的集合。 然后，可以选择此集合，而无需退出该过程来执行此操作。  

1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。

2. 在“主页”选项卡的“管理”组中，选择“配置共同管理”以打开“共同管理配置向导”。

3. 在“订阅”页上，选择“登录”并登录到 Intune 租户，然后选择“下一步”。

4. 在“启用”页的“在 Intune 中自动注册”下拉列表中，选择以下选项之一：  

   - **试点**  - （建议）指定的集合成员将被自动注册到 Intune，然后可以对其进行共同管理。 可以在此向导的“暂存”页上指定试点集合。 通过此选项可以测试客户端子集上的共同管理。 然后，可以分阶段逐步向其他客户端推出共同管理。  

   - **全部** - 为所有客户端启用共同管理。  

5. 在“工作负荷”页上，可以将工作负荷从“Configuration Manager”切换为以下负荷之一，然后准备好继续后，选择“下一步”。  

   - **试点 Intune** - 仅为试点组中的设备切换工作负荷。 将在向导的下一页上将集合指定为试点组。  

   - **Intune** - 切换所有共同管理的 Windows 10 设备的关联的工作负荷。  

   在启用共同管理时，无需切换任何工作负荷。 在配置共同管理后，可以稍后从 Configuration Manager 控制台重新访问此配置。  

   切换工作负荷之前，请确保已在 Intune 中配置和部署相应的工作负荷。 这样做可以管理工作负荷。  

6. 在“暂存”页上，指定供“试点集合”使用的集合，然后单击“下一步”。 在分阶段启用共同管理的过程中将用到你指定的集合。 可随时在共同管理属性中更改试点组中的集合。  

7. 在“摘要”页上，选择“下一步”，然后选择“关闭”以完成向导。  


## <a name="next-steps"></a>后续步骤
- 使用[共同管理仪表板](/sccm/comanage/how-to-monitor)查看共同管理的设备的状态
- 开始从共同管理中获取[即时值](quickstarts.md#immediate-value)
- 使用[条件访问](quickstart-conditional-access.md)和 Intune 符合性规则来管理用户对企业资源的访问权限
