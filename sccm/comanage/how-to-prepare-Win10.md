---
title: 共同管理基于 Internet 的设备
titleSuffix: Configuration Manager
description: 了解如何准备 Windows 10 基于 Internet 的设备进行共同管理。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31779b3588617816df4309461ed7715b20b0abd4
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "57558025"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>如何准备基于 Internet 的设备进行共同管理

本文重点介绍了对基于 Internet 的新设备进行共同管理的第二种方式。 具体场景：具备联接 Azure AD 并自动注册到 Intune 的新 Windows 10 设备。 安装 Configuration Manager 客户端以实现共同管理。  



## <a name="windows-autopilot"></a>Windows Autopilot

对于新的 Windows 10 设备，可以使用 Autopilot 服务来配置全新体验 (OOBE)。 此过程包括将设备联接 Azure AD 并在 Intune 中注册设备。  

有关详细信息，请参阅 [Windows Autopilot 概述](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot)。    

若要将设备配置为在其联接 Azure AD 时自动注册到 Intune，请参阅 [将 Windows 设备注册到 Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll)。  


### <a name="gather-information-from-configuration-manager"></a>收集来自 Configuration Manager 的信息

从 1802 版开始，使用 Configuration Manager 可收集和报告 Microsoft Store 商业版和教育版所需的设备信息。 此信息包括设备序列号、Windows 产品标识符和硬件标识符。 它用于在 Microsoft Store 中注册设备以支持 Windows Autopilot。 

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报告”节点，展开“报表”，然后选择“硬件 - 常规”节点。  

2. 运行“Windows Autopilot 设备信息”报表并查看结果。  

3. 在报表查看器中，选择“导出”图标，并选择“CSV (逗号分隔)”选项。  

4. 在保存该文件后，将数据上传到 Microsoft Store 商业版和教育版。  

有关详细信息，请参阅[在适用于企业的 Microsoft Store 和适用于教育的 Microsoft Store 中添加设备](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)。


### <a name="autopilot-for-existing-devices"></a>面向现有设备的 Autopilot
<!--1358333-->

Windows 10 版本 1809 或更高版本中提供了[面向现有设备的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430)。 此功能可重置映像并使用单个本机 Configuration Manager 任务序列为 [Windows Autopilot 用户驱动模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)预配 Windows 7 设备。 

有关详细信息，请参阅[面向现有设备任务序列的 Windows Autopilot](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices)。



## <a name="install-the-configuration-manager-client"></a>安装 Configuration Manager 客户端

对于第二种方式中基于 Internet 的设备，需要在 Intune 中创建一个应用。 将此应用部署到尚不是 Configuration Manager 客户端的 Windows 10 设备。 

### <a name="get-the-command-line-from-configuration-manager"></a>从 Configuration Manager 获取命令行

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。  

2. 选择共同管理对象，然后选择功能区中的“属性”。  

3. 在“启用”选项卡上，复制命令行。 将其粘贴到记事本，保存以供下一过程使用。  

命令行示例：`CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215-->
从 1806 版开始，现在需要的命令行属性有所减少。  

- 在所有方案中都需要以下命令行属性：  
    - CCMHOSTNAME  
    - SMSSITECODE  

- 在使用 Azure AD 进行客户端身份验证而不是使用基于 PKI 的客户端身份验证证书时，需要以下属性：  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- 如果客户端漫游回 Intranet，则需要以下属性：  
    - SMSMP  

- 如果使用自己的 PKI SSL 证书且 CRL 未发布到 Internet，则需要以下参数：  
    - /noCRLCheck  
    
     有关详细信息，请参阅[规划 CRL](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

从 1810 版开始，该站点将其他 Azure AD 信息发布到云管理网关 (CMG)。 Azure AD 联接的客户端使用其联接的同一租户在 ccmsetup 进程中从 CMG 获取此信息。 这种行为进一步简化了注册设备，使其在有多个 Azure AD 租户的环境中进行共同管理。 现在，只有两个必需的 ccmsetup 属性：CCMHOSTNAME 和 SMSSiteCode。<!--3607731-->

> [!Note]
> 如果已从 Intune 部署 Configuration Manager 客户端，请使用新命令行和新 MSI 更新 Intune 应用。 <!-- SCCMDocs-pr issue 3084 -->

下面的示例包含所有这些属性：   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

有关详细信息，请参阅[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。


### <a name="create-the-app-in-intune"></a>在 Intune 中创建应用

1. 转到 [Azure 门户](https://portal.azure.com)，然后打开 Intune 页。  

2. 选择“客户端应用” > “应用” > “添加”。  

3. 在“其他”下，选择“业务线应用”。  

4. 上传 ccmsetup.msi 应用包文件。 此文件位于 Configuration Manager 站点服务器上的以下文件夹中：`<ConfigMgr installation directory>\bin\i386`。  

    > [!Tip]  
    > 更新站点时，请确保同时在 Intune 中更新此应用。  

5. 更新应用后，使用从 Configuration Manager 复制的命令行配置应用信息。  

> [!IMPORTANT]    
> 如果自定义此命令行，请确保其长度不超过 1024 个字符。 如果命令行字符长度大于 1024，客户端安装会失败。


