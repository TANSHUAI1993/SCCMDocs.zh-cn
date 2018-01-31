---
title: "准备 Windows 10 设备进行共同管理"
description: "了解如何准备 Windows 10 设备进行共同管理。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: d605dd4770be6878b08f4ac61da6ab27e3b6d61f
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>准备 Windows 10 设备进行共同管理
可对已联接 AD 和 Azure AD 并在 Intune 中注册的 Windows 10 设备和 Configuration Manager 中的客户端启用共同管理。 对于新的 Windows 10 设备和已在 Intune 中注册的设备，请在可以进行共同管理前先安装 Configuration Manager 客户端。 对于已属于 Configuration Manager 客户端的 Windows 10 设备，可向 Intune 注册设备并在 Configuration Manager 控制台中启用共同管理。

## <a name="command-line-to-install-configuration-manager-client"></a>安装 Configuration Manager 客户端的命令行
须在适用于 Windows 10 设备（还不是 Configuration Manager 客户端）的 Intune 中创建应用。 在下一节中创建应用时，请使用以下命令行：

ccmsetup.msi CCMSETUPCMD="/mp:<云管理网关相互身份验证终结点 URL>/ CCMHOSTNAME=<云管理网关相互身份验证终结点 URL> SMSSiteCode=<站点代码> SMSMP=https://<MP 的 FQDN> AADTENANTID=<AAD 租户 ID> AADTENANTNAME=<租户名> AADCLIENTAPPID=<AAD 集成的 Server AppID> AADRESOURCEURI=https://<资源 ID>”

例如，如果具有以下值：

- 云管理网关相互身份验证终结点 URL：https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >对于云管理网关相互身份验证终结点 URL 值，使用 vProxy_Roles SQL 视图中的 MutualAuthPath 值。

- 管理点 (MP) 的 FQDN：sccmmp.corp.contoso.com    
- 站点代码：PS1    
- Azure AD 租户 ID：72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- Azure AD 租户名称：contoso    
- Azure AD 客户端应用 ID：bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- AAD 资源 ID URI：ConfigMgrServer    

  > [!Note]    
  > 对于 AAD 资源 ID URI 值，使用在 vSMS_AAD_Application_Ex SQL 视图中找到的 IdentifierUri 值。

将使用以下命令行：

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
> 可通过使用以下步骤查找站点的命令行参数：     
> 1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。  
> 2. 在“主页”选项卡的“管理”组中，选择“配置共同管理”以打开“共同管理载入”向导 ****。    
> 3. 在“订阅”页中，单击“登录”并登录到 Intune 租户，然后单击“下一步”。    
> 4. 在“启用”页面的“在 Intune 中注册的设备”部分中单击“复制”，将命令行复制到剪贴板，然后将其保存，用在创建应用的过程中。  
> 5. 单击“取消”退出向导。

> [!Important]    
> 如果要自定义安装 Configuration Manager 客户端的命令行，请确保命令行的字符数不超过 1024。 如果命令行的字符数大于 1024，客户端安装会失败。


## <a name="new-windows-10-devices"></a>新的 Windows 10 设备
对于新的 Windows 10 设备，可以使用 Autopilot 服务来配置全新体验，这包括将设备联接到 AD 和 Azure AD，以及在 Intune 中注册设备。 然后，在 Intune 中创建应用，部署 Configuration Manager 客户端。  
1. 对新的 Windows 10 设备启用 AutoPilot。 有关详细信息，请参阅 [Windows AutoPilot 概述](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)。  
2. 为设备在 Azure AD 中配置自动注册，以自动向 Intune 注册设备。 有关详细信息，请参阅 [针对 Microsoft Intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。
3. 使用 Configuration Manager 客户端程序包在 Intune 中创建应用，并将应用部署到要共同管理的 Windows 10 设备中。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>未在 Intune 中注册或不是 Configuration Manager 客户端的 Windows 10 设备
对于未在 Intune 中注册或不是 Configuration Manager 客户端的 Windows 10 设备，可以使用自动注册在 Intune 中注册设备。 然后，在 Intune 中创建应用，部署 Configuration Manager 客户端。
1. 为设备在 Azure AD 中配置自动注册，以自动向 Intune 注册设备。 有关详细信息，请参阅 [针对 Microsoft Intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。  
2. 使用 Configuration Manager 客户端程序包在 Intune 中创建应用，并将应用部署到要共同管理的 Windows 10 设备中。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。

## <a name="windows-10-devices-enrolled-in-intune"></a>在 Intune 中注册的 Windows 10 设备
对于已在 Intune 中注册的 Windows 10 设备，在 Intune 中创建应用，以部署 Configuration Manager 客户端。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。  

## <a name="next-steps"></a>后续步骤
[将 Configuration Manager 工作负荷切换到 Intune](co-management-switch-workloads.md)