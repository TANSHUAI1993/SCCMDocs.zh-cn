---
title: 安装客户端（使用 Azure AD）
titleSuffix: Configuration Manager
description: 在 Windows 10 设备上安装并分配 Configuration Manager 客户端（使用 Azure Active Directory 进行身份验证）
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6af2f179a540c4a532173eacf265ec11bf292209
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677876"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）

要在 Windows 10 设备上安装 Configuration Manager 客户端（使用 Azure AD 身份验证），请将 Configuration Manager 与 Azure Active Directory (Azure AD) 集成。 客户端可以在 Intranet 上直接与启用 HTTPS 的管理点或启用增强型 HTTP 的站点中的任何管理点通信。 它们也可以通过 CMG 或基于 Internet 的管理点进行基于 Internet 的通信。 此过程使用 Azure AD 对访问 Configuration Manager 站点的客户端进行身份验证。 Azure AD 使你不再需要配置和使用客户端身份验证证书。

对于某些客户而言，设置 Azure AD 可能比为基于证书的身份验证设置公钥基础结构更容易。 有些功能要求将站点载入 Azure AD，但不一定要求客户端已加入 Azure AD。<!-- SCCMDocs issue 1259 --> 有关详细信息，请参阅下列文章：
- [规划 Azure Active Directory](/sccm/core/plan-design/security/plan-for-security#bkmk_planazuread)
- [使用 Azure AD 进行共同管理](/sccm/comanage/quickstart-hybrid-aad)



## <a name="before-you-begin"></a>在开始之前

- Azure AD 租户是先决条件  

- 设备要求：  

    - Windows 10  

    - 已加入 Azure AD（已加入纯云域或混合 Azure AD）  

- 用户要求：  

    - 已登录用户必须是 Azure AD 标识。   

    - 如果用户是联合标识或同步标识，则必须使用 Configuration Manager [Active Directory 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)和 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)。 若要详细了解混合标识，请参阅[定义混合标识采用策略](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)。<!--497750-->  

- 除了管理点站点系统角色的[现有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq)，还需在此服务器上启用“ASP.NET 4.5”  。 包括启用 ASP.NET 4.5 时自动选择的任何其他选项。  

- 确定管理点是否需要 HTTPS。 有关详细信息，请参阅[为管理点启用 HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps)。  

- （可选）要部署基于 Internet 的客户端，请设置[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG)。 使用 Azure AD 进行身份验证的本地客户端不需要 CMG。  


## <a name="configure-azure-services-for-cloud-management"></a>配置 Azure 服务以进行云管理

首先，将 Configuration Manager 站点连接到 Azure AD。 有关此流程的详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。 创建到“云管理”服务的连接  。

在加入“云管理”期间启用 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  。 

完成以上操作后，Configuration Manager 站点将连接到 Azure AD。 



## <a name="configure-client-settings"></a>配置客户端设置

这些客户端设置有助于 Windows 10 加入 Azure AD。 它们还可使基于 Internet 的客户端使用 CMG 和云分发点。

1. 按照[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)中的信息，在“云服务”部分配置以下客户端设置  。  

    - **允许访问云分发点**：启用此设置可帮助基于 Internet 的设备获取安装 Configuration Manager 客户端所需的内容。 如果内容在云分发点上不可用，设备可以从 CMG 检索该内容。 客户端安装启动会在 4 小时内重试云分发点，之后将回退到 CMG。<!--495533-->  

    - **在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备**：设置为“是”或“否”   。 默认设置为“是”  。 这也是 Windows 10 1709 版中的默认行为。

    -  允许客户端使用云管理网关 – 设置为“是”  （默认值），或“否”  。  

2. 将客户端设置部署到所需的设备集合。 不要将这些设置部署到用户集合。

要确认设备已加入 Azure AD，请在命令提示符中运行 `dsregcmd.exe /status`。 如果设备已加入 Azure AD，结果中的“AzureAdjoined”字段会显示“YES”   。



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>使用 Azure AD 标识安装并注册客户端

要使用 Azure AD 标识手动安装客户端，请首先查看[如何手动安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)了解常规流程。 

 > [!Note]  
 > 设备需要访问 Internet 与 Azure AD 通信，但不需要基于 Internet。 

以下示例显示命令行的一般结构：`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

有关详细信息，请参阅[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。

/mp 和 CCMHOSTNAME 属性指定以下项之一，具体取决于应用场景：
- 本地管理点。 仅指定 /mp 属性。 不需要 CCMHOSTNAME。
- 云管理网关
- 基于 Internet 的管理点 SMSMP 属性指定本地或基于 Internet 的管理点。

本示例使用云管理网关。 它将替代每个属性的示例值：`ccmsetup.exe /mp: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

从 1810 版开始，该站点将其他 Azure AD 信息发布到云管理网关 (CMG)。 Azure AD 联接的客户端使用其联接的同一租户在 ccmsetup 进程中从 CMG 获取此信息。 此行为进一步简化了在具有多个 Azure AD 租户的环境中安装客户端的过程。 现在，只有两个必需的 ccmsetup 属性：CCMHOSTNAME  和 SMSSiteCode  。<!--3607731-->

若要使用 Azure AD 标识通过 Microsoft Intune 自动执行客户端安装，请参阅[如何准备基于 Internet 的设备以进行共同管理](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client)。



## <a name="next-steps"></a>后续步骤

完成后，可以继续[监视和管理客户端](/sccm/core/clients/manage/monitor-clients)。
