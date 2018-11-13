---
title: 增强型 HTTP
titleSuffix: Configuration Manager
description: 使用新式身份验证来保护客户端通信，而无需 PKI 证书。
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3a49fd8e171b053a5cc89d316fce3651e2a2f567
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411556"
---
# <a name="enhanced-http"></a>增强型 HTTP

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Note]  
> 在该 Configuration Manager 版本中，增强型 HTTP 是预发行功能。 若要启用此功能，请参阅[预发行功能](/sccm/core/servers/manage/pre-release-features)。  

Microsoft 建议对于所有 Configuration Manager 通信路径使用 HTTPS 通信，但由于管理 PKI 证书的开销，对一些客户来说可能是一个挑战。 Azure Active Directory (Azure AD) 集成的引入可以减少某些证书要求但不是所有证书要求。 

Configuration Manager 版本 1806 包括对客户端与站点系统之间的通信方式的改进。 这些改进有两个主要目标：  

- 可保护敏感客户端通信，而无需提供 PKI 服务器身份验证证书。  

- 客户端可安全地从分发点访问内容，而无需网络访问帐户、客户端 PKI 证书和 Windows 身份验证。  

> [!Note]  
> 对于具有以下要求的客户，PKI 证书仍然是有效选项：   
> - 所有客户端通信均通过 HTTPS 进行  
> - 对签名基础架构的高级控制  


## <a name="bkmk_scenario"></a> 方案

以下方案受益于这些改进：  


### <a name="bkmk_scenario1"></a> 方案 1：客户端到管理点
<!--1356889-->

[已加入 Azure AD 的设备](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices)能够与为 HTTP 配置的管理点进行通信。 站点服务器为管理点生成证书，使其能够通过安全通道进行通信。   

> [!Note]  
> 此行为在 Configuration Manager 当前分支版本 1802 中有所不同，在这种情况下，它需要一个已启用 HTTPS 的管理点，用于通过云管理网关进行通信的已加入 Azure AD 的客户端。 有关详细信息，请参阅[为管理点启用 HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps)。  


### <a name="bkmk_scenario2"></a> 方案 2： 客户端到分发点
<!--1358228-->

工作组或已加入 Azure AD 的客户端可通过安全通道从为 HTTP 配置的分发点进行身份验证及下载内容。 这些类型的设备还可从为 HTTPS 配置的分发点进行身份验证和下载内容，而无需在客户端上使用 PKI 证书。 将客户端身份验证证书添加到工作组或已加入 Azure AD 的客户端，这颇具挑战性。

此行为包括 OS 部署方案，其中任务序列从启动媒体、PXE 或软件中心运行。 有关详细信息，请参阅[网络访问帐户](/sccm/core/plan-design/hierarchy/accounts#network-access-account)。<!--1358278-->


### <a name="bkmk_scenario3"></a> 方案 3：Azure AD 设备标识 
<!--1358460-->

没有 Azure AD 用户登录的已加入 Azure AD 的设备或[混合 Azure AD 设备](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices)可安全地与其分配的站点进行通信。 现在，对于以设备为中心的方案，基于云的设备标识足以通过 CMG 和管理点进行身份验证。 （以用户为中心的方案仍然需要用户令牌。）  


## <a name="prerequisites"></a>先决条件  

- 针对 HTTP 客户端连接配置的管理点。 在站点系统角色属性的“常规”选项卡上设置此选项。  

- 针对 HTTP 客户端连接配置的分发点。 在站点系统角色属性的“常规”选项卡上设置此选项。 请勿启用选项“允许客户端进行匿名连接”。  

- 将站点载入 Azure AD 以便进行云管理。  

    - 如果你的站点已满足此先决条件，则需更新 Azure AD 应用程序。 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure Active Directory 租户”。 选择 Azure AD 租户，再选择“应用程序”窗格中 Web 应用程序，然后选择功能区中的“更新应用程序设置”。  

- 仅限[方案 3](#bkmk_scenario3)：运行 Windows 10 版本 1803 且已加入 Azure AD 的客户端。 



## <a name="configure-the-site"></a>配置站点

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择一个站点，然后选择功能区中的“属性”。  

2. 切换到“客户端计算机通信”选项卡。选择选项“HTTPS 或 HTTP”，然后启用选项“将 Configuration Manager 生成的证书用于 HTTP 站点系统”。  

> [!Tip]
> 请等待 30 分钟以便管理点从站点接收并配置新证书。

可以在 Configuration Manager 控制台中查看这些证书。 转到“管理”工作区，展开“安全”，然后选择“证书”节点。 查找“SMS 发证”根证书，以及由 SMS 发证根颁发的站点服务器角色证书。

有关客户端如何使用此配置与管理点和分发点进行通信的详细信息，请参阅[从客户端到站点系统和服务的通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System)。



## <a name="see-also"></a>另请参阅
- [规划安全性](/sccm/core/plan-design/security/plan-for-security)  

- [Configuration Manager 客户端的安全和隐私](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [配置安全性](/sccm/core/plan-design/security/configure-security)  

- [终结点之间的通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

