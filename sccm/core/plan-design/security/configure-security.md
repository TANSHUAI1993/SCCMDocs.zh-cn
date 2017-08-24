---
title: "配置 System Center Configuration Manager 中的安全性 | Microsoft Docs"
description: "配置 System Center Configuration Manager 的安全相关选项。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0034381a7a388ddc3eda5e774f3c63d741336301
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-security-in-system-center-configuration-manager"></a>配置 System Center Configuration Manager 中的安全性

*适用范围：System Center Configuration Manager (Current Branch)*

使用本主题中的信息来帮助为 System Center Configuration Manager 配置以下安全相关选项。  

##  <a name="BKMK_ConfigureClientPKI"></a> 为客户端 PKI 证书配置设置  
如果要为与使用 Internet Information Services (IIS) 的站点系统的客户端连接使用公钥基础架构 (PKI) 证书，请使用下列过程来为这些证书配置设置。  

#### <a name="to-configure-client-pki-certificate-settings"></a>配置客户端 PKI 证书设置  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“站点配置” ，选择“站点”，然后选择要配置的主站点。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”，然后选择“客户端计算机通信”选项卡。  

    此选项卡仅在主站点上可用。 如果看不到“客户端计算机通信”  选项卡，请检查你是否未连接到管理中心站点或辅助站点。  

4.  如果希望分配给站点的客户端在连接到使用 IIS 的站点系统时始终使用客户端 PKI 证书，请选择“仅 HTTPS”。 或者，如果不需要客户端使用 PKI 证书，请选择“HTTPS 或 HTTP”。  

5.  如果选择了“HTTPS 或 HTTP”，请在希望为 HTTP 连接使用客户端 PKI 证书时选择“使用客户端 PKI 证书(客户端身份验证功能)(如果可用)”。 客户端使用此证书（而不是自签名证书）来向站点系统验证自身。 如果选择“仅 HTTPS”，则会自动选择此选项。  

    如果检测到客户端位于 Internet 上，或者针对仅限 Internet 的客户端管理配置了客户端，则客户端始终使用客户端 PKI 证书。  

6.  选择“修改”，为一个客户端上有多个有效 PKI 客户端证书的情况配置所选客户端选择方法，然后选择“确定”。  

    有关客户端证书选择方法的详细信息，请参阅[规划 PKI 客户端证书选择](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)。  

7.  选中或清除客户端的复选框以检查证书吊销列表 (CRL)。  

    有关客户端 CRL 检查的详细信息，请参阅[规划 PKI 证书吊销](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。  

8.  如果必须为客户端指定受信任根证书颁发机构 (CA)，请选择“设置”，导入根 CA 证书文件，然后选择“确定”。  

    有关此设置的详细信息，请参阅[规划 PKI 受信任的根证书和证书颁发者列表](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs)。  

9. 单击“确定”以关闭站点的属性对话框。  

为层次结构中的所有主站点重复此过程。  

##  <a name="BKMK_ConfigureSigningEncryption"></a> 配置签名和加密  
为站点系统配置站点中的所有客户端可支持的最安全签名和加密设置。 当你让客户端通过使用 HTTP 上的自签名证书与站点系统通信时，这些设置特别重要。  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>为站点配置签名和加密  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“站点配置” ，选择“站点”，然后选择要配置的主站点。  

3.  在“主页”选项卡上的“属性”组中，选择“属性”，然后选择“签名和加密”选项卡。  

    此选项卡仅在主站点上可用。 如果看不到“签名和加密”  选项卡，请检查你是否未连接到管理中心站点或辅助站点。  

4.  配置所需的签名和加密选项，然后选择“确定”。  

    > [!WARNING]  
    >  在未先检查可能分配给站点的所有客户端是否可支持此哈希算法并且它们具有有效的 PKI 客户端认证证书的情况下，请不要选择“需要 SHA-256” 。 你可能必须在客户端上安装更新或修补程序来支持 SHA-256。 例如，运行 Windows Server 2003 SP2 的计算机必须安装 [知识库文章 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666)中引用的修补程序。  
    >   
    >  如果选择此选项，而客户端无法支持 SHA-256 和使用自签名证书，则 Configuration Manager 将拒绝这些客户端。 在此方案中，SMS_MP_CONTROL_MANAGER 组件记录消息 ID 5443。  

5.  单击“确定”以关闭站点的“属性”对话框。  

为层次结构中的所有主站点重复此过程。  

##  <a name="BKMK_ConfigureRBA"></a> 配置基于角色的管理  
基于角色的管理结合了安全角色、安全作用域和分配的集合来定义每个管理用户的管理作用域。 管理作用域包括管理用户可在 Configuration Manager 控制台中查看的对象，以及管理用户有权执行的与这些对象相关的任务。 基于角色的管理配置应用于层次结构中的每个站点。  

以下链接指向[为 System Center Configuration Manager 配置基于角色的管理](../../../core/servers/deploy/configure/configure-role-based-administration.md)一文中的相关章节：  

-   [创建自定义安全角色](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [配置安全角色](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [配置对象的安全作用域](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [配置集合来管理安全性](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [创建新管理用户](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [修改管理用户的管理作用域](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  你自己的管理作用域定义你在为另一个管理用户配置基于角色的管理时可分配的对象和设置。 有关规划基于角色的管理的信息，请参阅 [System Center Configuration Manager 的基于角色的管理基础](../../../core/understand/fundamentals-of-role-based-administration.md)。  

##  <a name="BKMK_ManageAccounts"></a> 管理 Configuration Manager 使用的帐户  
Configuration Manager 支持为许多不同任务和用途使用 Windows 帐户。  

使用以下过程来查看为不同任务配置的帐户，以及管理 Configuration Manager 用于每个帐户的密码。  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>若要管理 Configuration Manager 使用的帐户  

1.  在 Configuration Manager 控制台中，选择“管理”。  

2.  在“管理”工作区中，展开“安全”，然后选择“帐户”以查看为 Configuration Manager 配置的帐户。  

3.  要更改为 Configuration Manager 配置的帐户的密码，请选择该帐户。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  选择“设置”打开“Windows 用户帐户”对话框，并指定 Configuration Manager 用于该帐户的新密码。  

    > [!NOTE]  
    >  你指定的密码必须与在 Active Directory 用户和计算机中为帐户指定的密码匹配。  

6.  选择“确定”完成该过程。  
