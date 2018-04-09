---
title: 安装客户端（使用 Azure AD）
titleSuffix: Configuration Manager
description: 在 Windows 10 设备上安装并分配 Configuration Manager 客户端（使用 Azure Active Directory 进行身份验证）
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a8ca1a60a249756065ee2af6cb9c37f3fe2a1e0
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）

要在 Windows 10 设备上安装 Configuration Manager 客户端（使用 Azure AD 身份验证），请将 Configuration Manager 与 Azure Active Directory (Azure AD) 集成。 客户端可采用 Intranet，与启用 HTTPS 的管理点直接通信。 它们也可以通过 CMG 或基于 Internet 的管理点进行基于 Internet 的通信。 此过程使用 Azure AD 对访问 Configuration Manager 站点的客户端进行身份验证。 Azure AD 使你不再需要配置和使用客户端身份验证证书。



## <a name="before-you-begin"></a>在开始之前

- Azure AD 租户是先决条件  

- 设备要求：  

    - Windows 10  

    - 已加入 Azure AD（已加入纯云域或混合 Azure AD）  

- 用户要求：  

    - 已登录用户必须是 Azure AD 标识。   

    - 如果用户是联合标识或同步标识，则必须使用 Configuration Manager [Active Directory 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser)和 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)。 有关混合标识的详细信息，请参阅[定义混合标识采用策略](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)<!--497750-->  

- 除了管理点站点系统角色的[现有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq)，还需在此服务器上启用“ASP.NET 4.5”。 包括启用 ASP.NET 4.5 时自动选择的任何其他选项。  

- 针对 HTTPS 模式配置所有管理点。 有关详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)和[为运行 IIS 的站点系统部署 Web 服务器证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)。  

- （可选）要部署基于 Internet 的客户端，请设置[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG)。 使用 Azure AD 进行身份验证的本地客户端不需要 CMG。  


## <a name="configure-azure-services-for-cloud-management"></a>配置 Azure 服务以进行云管理

首先，将 Configuration Manager 站点连接到 Azure AD。 有关此流程的详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。 创建到“云管理”服务的连接。

在加入“云管理”期间启用 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)。 

完成以上操作后，Configuration Manager 站点将连接到 Azure AD。 



## <a name="configure-client-settings"></a>配置客户端设置

这些客户端设置有助于 Windows 10 加入 Azure AD。 它们还可使基于 Internet 的客户端使用 CMG 和云分发点。

1.  按照[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)中的信息，在“云服务”部分配置以下客户端设置。  

    - **允许访问云分发点**：启用此设置可帮助基于 Internet 的设备获取安装 Configuration Manager 客户端所需的内容。 如果内容在云分发点上不可用，设备可以从 CMG 检索该内容。 客户端安装启动会在 4 小时内重试云分发点，之后将回退到 CMG。<!--495533-->  

    - **在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备**：设置为“是”或“否”。 默认设置为“是”。 这也是 Windows 10 1709 版中的默认行为。

    - 允许客户端使用云管理网关 – 设置为“是”（默认值），或“否”。  

2.  将客户端设置部署到所需的设备集合。 不要将这些设置部署到用户集合。

要确认设备已加入 Azure AD，请在命令提示符中运行 `dsregcmd.exe /status`。 如果设备已加入 Azure AD，结果中的“AzureAdjoined”字段会显示“YES”。



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>使用 Azure AD 标识安装并注册客户端

要使用 Azure AD 标识手动安装客户端，请首先查看[如何手动安装客户端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)了解常规流程。 

 > [!Note]  
 > 设备需要访问 Internet 与 Azure AD 通信，但不需要基于 Internet。 

以下示例显示命令行的一般结构：`ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADTENANTNAME=<Azure AD tenant name> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

有关详细信息，请参阅[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。

/mp 和 CCMHOSTNAME 属性指定以下项之一，具体取决于应用场景：
- 本地管理点。 仅指定 /mp 属性。 不需要 CCMHOSTNAME。
- 云管理网关
- 基于 Internet 的管理点 SMSMP 属性指定本地或基于 Internet 的管理点。

本示例使用云管理网关。 它将替代每个属性的示例值：`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADTENANTNAME=contoso AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

要使用 Azure AD 标识通过 Microsoft Intune 自动执行客户端安装，请参阅[准备 Windows 10 设备进行共同管理](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)流程。



## <a name="next-steps"></a>后续步骤

完成后，可以继续[监视和管理客户端](/sccm/core/clients/manage/monitor-clients)。
