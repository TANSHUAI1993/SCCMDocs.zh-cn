---
title: 教程&#58;共同管理路径 1
titleSuffix: Configuration Manager
description: 已在管理 Windows 10 设备使用 Configuration Manager 时，请使用 Microsoft Intune 中配置共同管理。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aecb2c33c874717f1da979f1316d1b46b785071
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754667"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>教程：启用共同管理现有 Configuration Manager 客户端
通过共同管理，可以保留您使用 Configuration Manager 来管理你的组织中的 Pc 的现成过程。 在同一时间投资通过 Intune 使用的安全和最新预配在云中。  

在本教程中，你将在 Configuration Manager 已注册的 Windows 10 设备的共同管理设置。 本教程开始使用已使用 Configuration Manager 来管理 Windows 10 设备的前提。

使用本教程时：  

- 混合 Azure AD 配置中具有可以连接到 Azure Active Directory (Azure AD) 的本地 Active Directory
- 具有你想要将云附加的现有 Configuration Manager 客户端


**在本教程中，你将：**  
> [!div class="checklist"]  
> * 查看适用于 Azure 和本地环境的先决条件  
> * 设置混合 Azure AD  
> * 配置 Configuration Manager 客户端代理注册到 Azure AD  
> * 配置 Intune 自动注册设备  
> * 向用户分配 Intune 许可证  
> * 启用共同管理配置管理器中  


## <a name="prerequisites"></a>先决条件  

### <a name="azure-services-and-environment"></a>Azure 服务和环境
- Azure 订阅 ([免费试用版](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune 订阅
  > [!TIP]  
  > 企业移动性 + 安全性 (EMS) 订阅包括 Azure Active Directory Premium 和 Microsoft Intune。 EMS 订阅 ([免费试用版](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))。  

如果你的环境中尚不存在将在本教程期间：
- 将用户分配的许可证*Intune*以及*Azure Active Directory Premium*
- 配置[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation)之间在本地 Active Directory 和 Azure Active Directory (AD) 租户


### <a name="on-premises-infrastructure"></a>在本地基础结构
- 一个[受支持的版本](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions)System Center Configuration Manager current branch
- [MDM 机构](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority)必须设置为 Intune  


### <a name="permissions"></a>权限
在本教程中，使用以下权限来完成的任务：  
- 该帐户是*全局管理员*在 Azure 中  
- 该帐户是*域管理员*上的本地基础结构  
- 该帐户是*完全权限管理员*有关*所有*作用域在配置管理器   

## <a name="set-up-hybrid-azure-ad"></a>设置混合 Azure AD
如果设置了混合 Azure AD 时，要真正设置集成的本地 AD 与 Azure AD 使用 Azure AD Connect 和 Active Directory 联合服务 (ADFS)。 成功配置，与您的工作人员可以无缝登录到外部系统使用其本地 AD 凭据。

> [!IMPORTANT]  
> 本教程详细介绍了一个基本的过程设置混合 Azure AD 托管域。 我们建议您应该熟悉过程而不依赖本教程引导您了解和部署混合 Azure AD。
>
> 有关混合 Azure AD 的详细信息，开始使用 Azure Active Directory 文档中的以下文章：
> - [计划你的 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [规划混合 Azure AD 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [控制你的设备的混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [配置为联合域的混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>设置 Azure AD Connect  
混合 Azure AD 需要配置的 Azure AD Connect，以使计算机帐户在你的本地 Active Directory (AD) 和设备对象在 Azure AD 中保持同步。

从版本 1.1.819.0 开始，Azure AD Connect 提供向导，配置混合 Azure AD 联接。 使用该向导可简化配置过程。  

若要配置 Azure AD Connect，需要在 Azure AD 租户的全局管理员凭据。  

> [!TIP]  
> 下面的过程应不被视为具有权威的 Azure AD Connect 设置，但这里提供了用于帮助简化配置 Intune 和 Configuration Manager 之间的共同管理。 对此的权威内容和相关的过程的设置的 Azure AD 中，请参阅[托管域配置混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)Azure AD 文档中。  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>配置使用 Azure AD Connect 的混合 Azure AD 联接

1. 获取并安装[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 或更高版本)。  
2. 启动 Azure AD Connect，并选择**配置**。
3. 上**其他任务**页上，选择**配置设备选项**，然后选择**下一步**。
4. 上**概述**页上，选择**下一步**。
5. 上**连接到 Azure AD**页上，输入你的 Azure AD 租户的全局管理员凭据。
6. 上**设备选项**页上，选择**配置混合 Azure AD 联接**，然后选择**下一步**。
7. 上**SCP**页上，对于每个本地林所需 Azure AD Connect 配置服务连接点 (SCP)，执行以下步骤，然后选择**下一步**:  
   1. 选择该林。  
   2. 选择身份验证服务。  如果联合的域，请选择 AD FS 服务器，除非你的组织有专门的 Windows 10 客户端和配置计算机/设备同步，或使用你的组织[SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)。  
   3. 单击**添加**输入企业管理员凭据。  
8. 上**设备的操作系统**页上，选择在 Active Directory 环境中，设备使用的操作系统，然后选择**下一步**。  

   您可以选择选项以支持 Windows 下层已加入域的设备，但请记住该共同管理的设备仅支持适用于 Windows 10。

9. 如果必须在托管的域，请跳过此步骤。  

   上**联合身份验证配置**页上，输入你的 AD FS 管理员凭据，然后选择**下一步**。
10. 上**已准备好配置**页上，选择**配置**。
11. 上**完成配置**页上，选择**退出**。

如果遇到问题与完成混合 Azure AD 域联接已加入的 Windows 设备，请参阅[适用于 Windows 当前设备的故障排除混合 Azure AD 联接](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)。


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>配置客户端设置以直接向 Azure AD 注册客户端  
使用客户端设置来配置 Configuration Manager 客户端自动注册到 Azure AD。  

1. 打开**Configuration Manager 控制台** > **管理** > **概述** > **客户端设置**，然后编辑**默认客户端设置**。  

2. 选择**云服务**。  

3. 上**默认设置**页上，将**与 Azure Active Directory 自动注册 Windows 10 已加入域的新设备**为 =**是**。  

4. 选择“确定”以保存此配置。  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>配置自动注册到 Intune 的设备   
接下来，我们将设置具有 Intune 的设备自动注册。 使用自动注册，使用 Configuration Manager 自动管理的设备注册 Intune。

自动注册还允许用户注册到 Intune Windows 10 设备。 当用户将其工作帐户添加到其个人拥有的设备，或者当公司拥有的设备加入 Azure Active Directory 注册设备。  

1. 登录到[Azure 门户](https://portal.azure.com/)，然后选择**Azure Active Directory** > **移动性 （MDM 和 MAM）** > **Microsoft Intune**.  

2. 配置**MDM 用户作用域**。 指定一个以下操作来配置由 Microsoft Intune 管理的用户设备，然后接受 URL 值的默认值。  

   - **某些**-选择**组**可以自动注册其 Windows 10 设备  

   - **所有**-所有用户可以自动都注册 Windows 10 设备如果设置为**None**，移动设备管理 (MDM) 自动注册已禁用

   > [!IMPORTANT]  
   > 如果这两个**MAM 用户作用域**和自动 MDM 注册 (**MDM 用户作用域**) 之外的所有组，只会启用 MAM。 仅移动应用管理 (MAM) 添加为该组中的用户时这些工作区加入个人设备。 设备不会自动注册 MDM。  

3. 选择**保存**完成自动注册的配置。  

4. 返回到**移动性 （MDM 和 MAM）** ，然后选择**Microsoft Intune 注册**。  

5. MDM 用户范围，请选择**所有**，然后**保存**。  


## <a name="assign-intune-licenses-to-users"></a>向用户分配 Intune 许可证   
通常被忽略，但关键操作是将 Intune 许可证分配给每个用户都将使用共同管理的设备。  

若要将许可证分配到用户组，请使用 Azure Active Directory。  

1. 登录到[Azure 门户](https://portal.azure.com/)使用管理员帐户。 若要管理许可证，该帐户必须是全局管理员角色或用户帐户管理员。  

2. 选择**所有服务**在左侧的导航窗格中，然后选择**Azure Active Directory**。  

3. 上**Azure Active Directory**窗格中，选择**许可证**以打开的窗格，可以在其中查看和管理租户中所有可许可的产品。  

4. 下**所有产品**，选择你的产品选项，包括 Intune 许可证，并选择**分配**窗格的顶部。  

   例如，可以选择**企业移动性 + 安全性 E5**如果这是如何获取 Intune。  

5. 上**分配许可证**窗格中，单击**用户和组**以打开**用户和组**窗格。 选择的组和你要向其分配许可证的单个用户。  然后，单击**选择**底部的以确认所选内容窗格。  

6. 上**分配许可证**窗格中，单击**分配选项**以显示包含在前面选择的产品中的所有服务计划。 如果选择了一个 Intune 等产品，则会显示仅该产品。  
   - 设置**Microsoft Intune**到**上**。  
   - 每个用户分配的许可证**Azure Active Directory Premium**。  

   在适用的许可证分配，选择**确定**。  

7. 若要完成分配，在**分配许可证**窗格中，单击**分配**窗格的底部。

8. 在右上角显示的状态和过程的结果显示一个通知。 如果 （例如，由于组中的已有许可证），无法完成向组分配，请单击该通知查看失败的详细信息。

有关将 intune 许可证分配给用户的详细信息，请参阅[将许可证分配](https://docs.microsoft.com/intune/licenses-assign)。


## <a name="enable-co-management-in-configuration-manager"></a>启用共同管理配置管理器中
使用混合 Azure AD 设置，Configuration Manager 中的位置，并向用户分配的产品许可证的客户端配置，现在即可将开关和启用共同管理的 Windows 10 设备。  

> [!TIP]  
>  在步骤 6 个以下的过程中，将分配集合作为*试点组*进行共同管理。 这是包含少量的客户端来测试共同管理配置的组。 我们建议在开始该过程之前创建合适的集合。 然后您可以选择该集合而不退出过程来执行此操作。  

1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。

2. 在主页选项卡上，在管理组中，选择**配置共同管理**打开共同管理配置向导。

3. 在订阅页上，选择**Sign In**并登录到你的 Intune 租户，然后选择**下一步**。

4. 在启用页中，从*在 Intune 中的自动注册*下拉列表中，选择以下选项之一：  

   - **试点**  - *（推荐）* 指定的集合的成员自动注册到 Intune，随后可共同管理。 在指定试点集合*过渡*此向导页。 此选项可以测试共同管理的客户端的一个子集。 您然后可以向其他客户端使用分阶段的方式推出共同管理。  

   - **所有**-为所有客户端启用共同管理。  

5. 工作负荷页上，您可以切换工作负荷**Configuration Manager**为以下内容，并准备好继续后，选择**下一步**。  

   - **试验 Intune** -试点组中切换仅适用于设备的工作负荷。 将分配为向导的下一页上的试验组的集合。  

   - **Intune** -切换为所有共同托管的 Windows 10 设备相关联的工作负荷。  

   您无需启用共同管理次切换任何工作负荷。 配置共同管理后，可以重新访问 Configuration Manager 控制台中的此配置更高版本。  

   切换工作负荷之前，请确保配置和部署在 Intune 中的相应工作负荷。 执行操作，使工作负荷管理。  

6. 在暂存页上，指定要用于集合**试点集合**，然后单击**下一步**。 指定的集合用作的分阶段推出共同管理的一部分。 可随时在共同管理属性中更改试点组中的集合。  

7. 在摘要页上选择**下一步**，然后**关闭**以完成向导。  


## <a name="next-steps"></a>后续步骤
- 查看与共同托管的设备状态[共同管理仪表板](/sccm/comanage/how-to-monitor)
- 开始获取[即时值](quickstarts.md#immediate-value)从共同管理
- 使用[条件性访问](quickstart-conditional-access.md)和 Intune 符合性规则，用于管理用户对公司资源的访问权限
