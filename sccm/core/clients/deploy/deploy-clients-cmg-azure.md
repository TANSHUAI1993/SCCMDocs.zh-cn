---
title: "从 Internet 安装并分配客户端"
titleSuffix: Configuration Manager
description: "从 Internet 安装并分配 System Center Configuration Manager 客户端。"
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 2ef7580f94864094e9420eb0f5a5c5b4dc9d6d24
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）

可以将 Configuration Manager 云服务与 Azure AD 配合使用以支持以下方案：

- 在 Windows 10 设备上从 Internet 手动安装 Configuration Manager 客户端，并将它分配到 Configuration Manager 站点（需要云管理网关站点系统角色）。
- 使用 Azure AD 验证客户端，以访问 Configuration Manager 站点。 Azure AD 使你不再需要配置和使用客户端身份验证证书。
- 在站点中发现 Azure AD 用户，从而在集合和其他 Configuration Manager 操作中使用。

使用下列步骤来帮助你实现这一点：

- **第 1 步：在 Configuration Manager 云服务中设置 Azure 服务应用，并配置 Azure AD 用户发现**
- **第 2 步：设置云管理网关**（对于本地客户端，此为可选步骤）
- **第 3 步：将客户端设置配置为将 Windows 10 设备加入 Azure AD，并为客户端启用云管理网关**
- 步骤 4：使用 Azure Active Directory 标识安装并注册 Configuration Manager 客户端


## <a name="before-you-start"></a>开始之前

- 必须具有 Azure AD 租户。
- 设备必须运行 Windows 10、加入 Azure AD 且使用 Azure AD 身份登录。 除加入 Azure AD 外，客户端还可以加入域。
- 除了管理点站点系统角色的[现有先决条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)外，还必须确保 ASP.NET 4.5（和自动选择的任何其他选项）在托管此站点系统角色的计算机上启用。
- 若要使用 Configuration Manager 部署客户端，请按照以下步骤操作：
    - 若要使用 Azure AD（而不是客户端证书）进行身份验证，请至少配置一个 HTTPS 模式管理点。
        若要使用客户端证书（而不是云管理网关），可以根据需要配置 HTTPS 管理点，但建议这样做。 若要使用 Azure AD 进行身份验证，无论是本地客户端，还是 Internet 客户端，都必须配置 HTTPS 管理点。
    - 若要部署 Internet 客户端，请设置云管理网关。 对于要使用 Azure AD 进行身份验证的本地客户端，不需要配置云管理网关。


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>第 1 步：在 Configuration Manager 云服务中设置 Azure 服务应用

这会将 Configuration Manager 站点连接到 Azure AD，这也是本节中所有其他操作的先决条件。 

将 Azure AD 用户发现配置为云管理的一部分。 执行此操作的过程在主题“配置 Azure 服务以用于 Configuration Manager”中[创建 Azure Web 应用以用于 Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) 过程的步骤 6 中进行了详细介绍。
    
完成此过程后，就已经将 Configuration Manager 站点连接到 Azure AD 了。 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>第 2 步：设置云管理网关

设置云管理网关有助于实现本主题中所述的云管理方案。 在以下主题中找到帮助： 

- [在 Configuration Manager 中规划云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)。
- [为 Configuration Manager 设置云管理网关](/sccm/core/clients/manage/setup-cloud-management-gateway)。
- [在 Configuration Manager 中监视云管理网关](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)。

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>第 3 步：将客户端设置配置为将 Windows 10 设备加入 Azure AD，并为客户端启用云管理网关

1.  使用[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)中的信息，配置以下客户端设置部分（位于“云服务”中）。
    - **允许访问云分发点** - 如果启用此设置，可帮助基于 Internet 的设备获取安装 Configuration Manager 客户端所需的内容。 如果云分发点上没有内容，设备可以从连接到云管理网关的管理点检索内容。
    - 在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备 – 设置为“是”（默认值），或“否”。
    - 允许客户端使用云管理网关 – 设置为“是”（默认值），或“否”。
2.  将客户端设置部署到所需的设备集合。 不要将这些设置部署到用户集合。

要确认设备是否已加入 Azure AD，请在命令提示符窗口运行命令“dsregcmd.exe /status”。 如果设备已加入 Azure AD，结果中的“AzureAdjoined”字段会显示“YES”。


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>步骤 4：使用 Azure Active Directory 标识安装并注册 Configuration Manager 客户端

若要安装客户端，请使用以下安装命令行，按照[如何将 System Center Configuration Manager 客户端部署到 Windows 计算机](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually)中的说明操作： 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP** - 下载源。 如果从 Internet 启动，可以设置为 CMG。
- **CCMHOSTNAME：**Internet 管理点的名称。 可以通过从托管客户端的命令提示符处运行 gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate 找到此名称。
- **SMSSiteCode：**Configuration Manager 站点的站点代码。
- **SMSMP：**查找管理点的名称，管理点可以位于 Intranet 上。
- **AADTENANTID**、**AADTENANTNAME：**关联到 Configuration Manager 的 Azure AD 租户的 ID 和名称。 可以通过从加入 Azure AD 的设备上的命令提示符处运行 dsregcmd.exe /status 找到上述内容。
- **AADCLIENTAPPID：**Azure AD 客户端应用 ID。 有关查找此内容的帮助，请参阅[使用门户创建可访问资源的 Azure Active Directory 应用程序和服务主体](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key)。
- **AADResourceUri：**载入的 Azure AD 服务器应用的标识符 URI。 有关详细信息，请参阅[配置用于 Configuration Manager 的 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)。




## <a name="next-steps"></a>后续步骤

完成后，可以继续[监视和管理客户端](/sccm/core/clients/manage/monitor-clients)。
