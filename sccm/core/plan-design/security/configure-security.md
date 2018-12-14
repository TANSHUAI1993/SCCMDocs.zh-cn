---
title: 配置安全性
titleSuffix: Configuration Manager
description: 配置 Configuration Manager 的安全相关选项。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1aaf6db583d9749dda3be14cfd06acbff19b093
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456084"
---
# <a name="configure-security-in-configuration-manager"></a>配置 Configuration Manager 中的安全性

*适用范围：System Center Configuration Manager (Current Branch)*

使用本主题中的信息来帮助为 Configuration Manager 配置以下安全相关选项。 它涵盖以下安全选项：
- [客户端计算机通信](#BKMK_ConfigureClientPKI)，用于客户端 PKI 证书  
- [签名和加密](#BKMK_ConfigureSigningEncryption)  
- [基于角色的管理](#BKMK_ConfigureRBA)  
- [管理帐户](#BKMK_ManageAccounts)  
- [配置 Azure Active Directory](#bkmk_azuread)  
- [配置 SMS 提供程序的身份验证](#bkmk_auth)  



##  <a name="BKMK_ConfigureClientPKI"></a> 为客户端 PKI 证书配置设置  

如果要为与使用 Internet Information Services (IIS) 的站点系统的客户端连接使用公钥基础架构 (PKI) 证书，请使用下列过程来为这些证书配置设置。  

#### <a name="to-configure-client-pki-certificate-settings"></a>配置客户端 PKI 证书设置  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择要配置的主站点。  

2.  在功能区中，选择“属性”。 然后，切换到“客户端计算机通信”选项卡。  

    此选项卡仅在主站点上可用。 如果看不到“客户端计算机通信”选项卡，请确保你未连接到管理中心站点或辅助站点。  

3.  选择使用 IIS 的站点系统的设置。  

    - **仅 HTTPS**：分配给站点的客户端在连接到使用 IIS 的站点系统时始终使用客户端 PKI 证书。  

    - **HTTPS 或 HTTP**：不要求客户端使用 PKI 证书。  

    - **为 HTTP 站点系统使用 Configuration Manager 生成的证书**：有关此设置的详细信息，请参阅[增强的 HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)。  

4.  选择客户端计算机的设置。  

    - **使用客户端 PKI 证书(客户端身份验证功能)(如果可用)**：如果选择了“HTTPS 或 HTTP”站点服务器设置，请选择此选项以使用客户端 PKI 证书进行 HTTP 连接。 客户端使用此证书（而不是自签名证书）来向站点系统验证自身。 如果选择“仅 HTTPS”，则会自动选择此选项。  

    当一个客户端上有多个有效 PKI 客户端证书，选择“修改”以配置客户端证书选择方法。  

    有关客户端证书选择方法的详细信息，请参阅[规划 PKI 客户端证书选择](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForClientCertificateSelection)。  

    - **客户端检查站点系统的证书吊销列表(CRL)**：为客户端启用此设置以检查组织的 CRL 是否已吊销证书。  

    有关客户端 CRL 检查的详细信息，请参阅[规划 PKI 证书吊销](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs)。  

5.  若要导入、查看和删除受信任的根证书颁发机构的证书，请选择“设置”。  

    有关详细信息，请参阅[规划 PKI 受信任的根证书和证书颁发者列表](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRootCAs)。  


为层次结构中的所有主站点重复此过程。  



##  <a name="BKMK_ConfigureSigningEncryption"></a> 配置签名和加密  

为站点系统配置站点中的所有客户端可支持的最安全签名和加密设置。 当你让客户端通过使用 HTTP 上的自签名证书与站点系统通信时，这些设置特别重要。  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>为站点配置签名和加密  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”节点。 选择要配置的主站点。  

2.  在功能区中，选择“属性”，然后切换到“签名和加密”选项卡。  

    此选项卡仅在主站点上可用。 如果看不到“签名和加密”选项卡，请确保你未连接到管理中心站点或辅助站点。  

3.  配置客户端的签名和加密选项以与站点通信。  

    - **需要签名**：客户端在发送到管理点之前签署数据。  

    - **需要 SHA-256**：客户端在签名数据时使用 SHA-256 算法。  

    > [!WARNING]  
    >  如果没有首先确认所有客户端都支持此哈希算法，请不要“需要 SHA-256”。 这些客户端包括将来可能分配给该站点的客户端。  
    >   
    >  如果选择此选项，并且具有自签名证书的客户端不支持 SHA-256，则 Configuration Manager 将会拒绝这些客户端。 SMS_MP_CONTROL_MANAGER 组件记录消息 ID 5443。  

    - **使用加密**：客户端在发送到管理点之前加密客户端清单数据和状态消息。 它们使用 3DES 算法。  

为层次结构中的所有主站点重复此过程。  



##  <a name="BKMK_ConfigureRBA"></a> 配置基于角色的管理  

基于角色的管理结合了安全角色、安全作用域和分配的集合来定义每个管理用户的管理作用域。 范围包括用户可在控制台中查看的对象，以及与他们有权执行的与对象相关的任务。 基于角色的管理配置应用于层次结构中的每个站点。  

有关详细信息，请参阅[配置基于角色的管理](/sccm/core/servers/deploy/configure/configure-role-based-administration)。 本文详细介绍以下操作：  

- 创建自定义安全角色  

- 配置安全角色  

- 配置对象的安全作用域  

- 配置集合来管理安全性  

- 创建新管理用户  

- 修改管理用户的管理作用域  

> [!IMPORTANT]  
>  你自己的管理作用域定义你在为另一个管理用户配置基于角色的管理时可分配的对象和设置。 有关基于角色的管理规划的信息，请参阅[基于角色的管理的基础](/sccm/core/understand/fundamentals-of-role-based-administration)。  



##  <a name="BKMK_ManageAccounts"></a>管理 Configuration Manager 使用的帐户  

Configuration Manager 支持为许多不同任务和用途使用 Windows 帐户。 若要为不同任务配置的帐户并管理 Configuration Manager 用于每个帐户的密码，请使用以下过程：  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>管理 Configuration Manager 使用的帐户  

1.  在 Configuration Manager 控制台中，转到“管理”工作区，展开“安全性”，然后选择“帐户”节点。  

2.  要更改帐户的密码，请在列表中选择该帐户。 选择功能区中的“属性”。  

3.  选择“设置”以打开“Windows 用户帐户”对话框。 指定 Configuration Manager 用于此帐户的新密码。  

    > [!NOTE]  
    >  指定的密码必须与 Active Directory 中此帐户的密码匹配。  

有关详细信息，请参阅 [Configuration Manager 中使用的帐户](/sccm/core/plan-design/hierarchy/accounts)。



##  <a name="bkmk_azuread"></a>配置 Azure Active Directory

将 Configuration Manager 与 Azure Active Directory (Azure AD) 集成，以简化和支持云环境。 使用 Azure AD 使站点和客户端能够进行身份验证。 有关详细信息，请参阅[配置 Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)中的“云管理”服务。



## <a name="bkmk_auth"></a>配置 SMS 提供程序的身份验证

从版本 1810 开始，可以为管理员指定访问 Configuration Manager 站点的最低身份验证级别。 此功能强制管理员以要求的级别登录到 Windows。 有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth)。 <!--1357013-->  



## <a name="see-also"></a>另请参阅

- [规划安全性](/sccm/core/plan-design/security/plan-for-security)  

- [Configuration Manager 客户端的安全和隐私](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [终结点之间的通信](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [加密控制技术参考](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)  
