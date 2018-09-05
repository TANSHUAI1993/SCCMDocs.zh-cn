---
title: 准备 Windows 10 进行共同管理
titleSuffix: Configuration Manager
description: 了解如何准备 Windows 10 设备进行共同管理。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: a34a50d4c7b917666316f9a4651aaebc2c001287
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384257"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>准备 Windows 10 设备进行共同管理
可对已加入 AD 和 Azure AD 并在 Microsoft Intune 中注册的 Windows 10 设备和 Configuration Manager 中的客户端启用共同管理。 对于新的 Windows 10 设备和已在 Intune 中注册的设备，请在可以进行共同管理前先安装 Configuration Manager 客户端。 对于已属于 Configuration Manager 客户端的 Windows 10 设备，可向 Intune 注册设备并在 Configuration Manager 控制台中启用共同管理。

> [!IMPORTANT]
> Windows 10 移动设备不支持共同管理。


## <a name="prerequisites"></a>先决条件
必须具备以下先决条件才能实现共同管理。 存在一般先决条件，而对于安装和未安装 Configuration Manager 客户端的设备，存在不同的先决条件。
### <a name="general-prerequisites"></a>一般先决条件
以下是实现共同管理的一般先决条件：  

- Configuration Manager 版本 1710 或更高版本
    - 自 Configuration Manager 版本 1806 起，可将多个 Configuration Manager 实例连接到单个 Intune 租户。 <!--1357944-->
- [将站点载入 Azure AD 以实现云管理](/sccm/core/servers/deploy/configure/azure-services-wizard)
- 适用于所有用户的 EMS 或 Intune 许可证
- [Azure AD 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)已启用
- Intune 订阅（Intune 中的 MDM 机构设置为 Intune）


   > [!Note]  
   > 如果具有混合 MDM 环境（Intune 与 Configuration Manager 集成），则无法实现共同管理。 但是，你可以开始将用户迁移到 Intune 独立版本，然后对其关联的 Windows 10 设备启用共同管理。 有关迁移到 Intune 独立版本的详细信息，请参阅[开始从混合 MDM 迁移到 Intune 独立版本](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)。

### <a name="prerequisite-azure-resource-manager-roles"></a>必备的 Azure 资源管理器角色
要详细了解 Azure 角色，请参阅[了解不同角色](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)。
|操作|所需角色|
|----|----|
|设置云管理网关|Azure 订阅管理者|
|设置云分发点|Azure 订阅管理者|
|通过 Configuration Manager 控制台创建 Azure Active Directory 应用|Azure Active Directory 全局管理员|
|将 Azure 客户端和服务器应用导入 Configuration Manager 控制台| Configuration Manager 管理员，无需其他 Azure 角色。|
|通过共同管理向导设置共同管理| Azure Active Directory 用户权限，以及具有所有作用域权限的 Configuration Manager 管理员。 
 
### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>针对安装了 Configuration Manager 客户端的设备的其他先决条件
- Windows 10 版本 1709 或更高版本
- [已联接混合 Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)（联接到 AD 和 Azure AD）

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>针对未安装 Configuration Manager 客户端的设备的其他先决条件
- Windows 10 版本 1709 或更高版本
- Configuration Manager 中的[云管理网关](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway)（当你使用 Intune 安装 Configuration Manager 客户端时）

> [!IMPORTANT]
> Windows 10 移动设备不支持共同管理。


## <a name="command-line-to-install-configuration-manager-client"></a>安装 Configuration Manager 客户端的命令行
在适用于 Windows 10 设备（尚不是 Configuration Manager 客户端）的 Intune 中创建应用。 在下一节中创建应用时，请使用以下命令行：

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

例如，如果具有以下值：

- **云管理网关相互身份验证终结点 URL**：https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    

   >[!Note]    
   >对于云管理网关相互身份验证终结点 URL 值，使用 vProxy_Roles SQL 视图中的 MutualAuthPath 值。

- **管理点 (MP) 的 FQDN**：mp1.contoso.com    
- 站点代码：PS1    
- Azure AD 租户 ID：60a413f4-c606-4744-8adb-9476ae3XXXXX    
- Azure AD 客户端应用 ID：9fb9315f-4c42-405f-8664-ae63283XXXXX     
- AAD 资源 ID URI：ConfigMgrServer    

  > [!Note]    
  > 对于 AAD 资源 ID URI 值，使用在 vSMS_AAD_Application_Ex SQL 视图中找到的 IdentifierUri 值。

将使用以下命令行：

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=60a413f4-c606-4744-8adb-9476ae3XXXXX AADCLIENTAPPID=9fb9315f-4c42-405f-8664-ae63283XXXXX AADRESOURCEURI=https://ConfigMgrServer"`

> [!Tip]
> 可通过使用以下步骤查找站点的命令行参数：     
> 1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。  
> 2. 在“主页”选项卡的“管理”组中，选择“配置共同管理”以打开“共同管理载入”向导。 ****    
> 3. 在“订阅”页中，单击“登录”并登录到 Intune 租户，然后单击“下一步”。    
> 4. 在“启用”页面的“在 Intune 中注册的设备”部分中单击“复制”，将命令行复制到剪贴板，然后将其保存，用在创建应用的过程中。  
> 5. 单击“取消”退出向导。

> [!Important]    
> 如果要自定义安装 Configuration Manager 客户端的命令行，请确保命令行的字符数不超过 1024。 如果命令行的字符数大于 1024，客户端安装会失败。


## <a name="new-windows-10-devices"></a>新的 Windows 10 设备
对于新的 Windows 10 设备，可以使用 Autopilot 服务来配置全新体验，这包括将设备联接到 AD 和 Azure AD，以及在 Intune 中注册设备。 然后，在 Intune 中创建应用，部署 Configuration Manager 客户端。  
1. 对新的 Windows 10 设备启用 AutoPilot。 有关详细信息，请参阅 [Windows AutoPilot 概述](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot)。    

   > [!NOTE]   
   > 从 1802 版开始，使用 Configuration Manager 可收集和报告 Microsoft Store 商业版和教育版所需的设备信息。 此信息包括设备序列号、Windows 产品标识符和硬件标识符。 在 Configuration Manager 控制台中的“监视”工作区中，展开“报告”节点，展开“报表”，然后选择“硬件 - 常规”节点。 运行新的报表“Windows AutoPilot 设备信息”并查看结果。 在报表查看器中，单击“导出”图标，并选择“CSV (逗号分隔)”选项。 在保存该文件后，将数据上传到 Microsoft Store 商业版和教育版。 有关详细信息，请参阅[在 Microsoft Store 商业版和教育版中添加设备](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)。

2. 为设备在 Azure AD 中配置自动注册，以自动向 Intune 注册设备。 有关详细信息，请参阅 [针对 Microsoft Intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。
3. 使用 Configuration Manager 客户端程序包在 Intune 中创建应用，并将应用部署到要共同管理的 Windows 10 设备中。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>未在 Intune 中注册或不是 Configuration Manager 客户端的 Windows 10 设备
对于未在 Intune 中注册或不具备 Configuration Manager 客户端的 Windows 10 设备，可使用自动注册功能在 Intune 中注册设备。 然后，在 Intune 中创建应用，部署 Configuration Manager 客户端。
1. 为设备在 Azure AD 中配置自动注册，以自动向 Intune 注册设备。 有关详细信息，请参阅 [针对 Microsoft Intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。  
2. 使用 Configuration Manager 客户端程序包在 Intune 中创建应用，并将应用部署到要共同管理的 Windows 10 设备中。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。

## <a name="windows-10-devices-enrolled-in-intune"></a>在 Intune 中注册的 Windows 10 设备
对于已在 Intune 中注册的 Windows 10 设备，在 Intune 中创建应用，以部署 Configuration Manager 客户端。 执行[使用 Azure AD 安装来自 Internet 的应用](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure)的步骤时，请使用[安装 Configuration Manager 客户端的命令行](#command-line-to-install-configuration-manager-client)。  

## <a name="next-steps"></a>后续步骤
[将 Configuration Manager 工作负荷切换到 Intune](co-management-switch-workloads.md)