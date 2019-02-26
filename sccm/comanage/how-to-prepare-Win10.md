---
title: 共同管理基于 internet 的设备
titleSuffix: Configuration Manager
description: 了解如何准备 Windows 10 的基于 internet 的设备进行共同管理。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbe26eee8b01c581776b1c134e1fe59cf4293e1a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754656"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>基于 internet 的设备进行共同管理的准备工作

本文重点介绍共同管理，为新的基于 internet 的设备的第二个路径。 这种情况下是具有新的 Windows 10 设备加入 Azure AD 并自动注册到 Intune。 安装 Configuration Manager 客户端，以达到共同管理状态。  



## <a name="windows-autopilot"></a>Windows Autopilot

对于新的 Windows 10 设备，可以使用 Autopilot 服务来配置全新体验 (OOBE)。 此过程包括将设备加入到 Azure AD 并在 Intune 中的设备注册。  

有关详细信息，请参阅[Windows Autopilot 概述](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot)。    

若要配置你的设备时他们加入 Azure AD 自动注册到 Intune，请参阅 [Microsoft intune 注册 Windows 设备](https://docs.microsoft.com/intune/windows-enroll)。  


### <a name="gather-information-from-configuration-manager"></a>收集从 Configuration Manager 的信息

从 1802 版开始，使用 Configuration Manager 可收集和报告 Microsoft Store 商业版和教育版所需的设备信息。 此信息包括设备序列号、Windows 产品标识符和硬件标识符。 它用于在 Microsoft Store 以支持 Windows Autopilot 注册设备。 

1. 在 Configuration Manager 控制台中，转到**监视**工作区中，展开**报表**节点，展开**报表**，然后选择**硬件-常规**节点。  

2. 运行报表时， **Windows Autopilot 设备信息**，并查看结果。  

3. 在报表查看器中，选择**导出**图标，然后选择**CSV （逗号分隔）** 选项。  

4. 在保存该文件后，将数据上传到 Microsoft Store 商业版和教育版。  

有关详细信息，请参阅[企业和教育的 Microsoft Store 中添加设备](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)。


### <a name="autopilot-for-existing-devices"></a>适用于现有设备的 autopilot
<!--1358333-->

[现有的设备的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430)是可用的 Windows 10，1809年或更高版本。 此功能，可重置映像和预配为 Windows 7 设备[Windows Autopilot 用户驱动模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)使用一个单一的本机 Configuration Manager 任务序列。 



## <a name="install-the-configuration-manager-client"></a>安装 Configuration Manager 客户端

对于第二个路径中的基于 internet 的设备，需要在 Intune 中创建应用程序。 将此应用程序部署到不存在 Configuration Manager 客户端的 Windows 10 设备。 

### <a name="get-the-command-line-from-configuration-manager"></a>获取从 Configuration Manager 的命令行

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。  

2. 选择共同管理对象，然后选择**属性**功能区中。  

3. 上**启用**选项卡上，复制命令行。 将其粘贴到记事本，以保存以供下一步的过程。  

下面的命令行是一个示例： `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215--> 从版本 1806 开始，现需要更少的命令行属性。  

- 在所有方案中都需要以下命令行属性：  
    - CCMHOSTNAME  
    - SMSSITECODE  

- 在使用 Azure AD 进行客户端身份验证而不是使用基于 PKI 的客户端身份验证证书时，需要以下属性：  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- 如果客户端漫游回到 intranet，则需要以下属性：  
    - SMSMP  

- 如果使用自己的 PKI SSL 证书和 CRL 不发布到 internet，则需要以下参数：  
    - /noCRLCheck  
    
     有关详细信息，请参阅[规划 Crl](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

下面的示例包括所有这些属性：   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

有关详细信息，请参阅[客户端安装属性](/sccm/core/clients/deploy/about-client-installation-properties)。


### <a name="create-the-app-in-intune"></a>在 Intune 中创建应用程序

1. 转到[Azure 门户](https://portal.azure.com)，然后打开 Intune 页。  

2. 选择**客户端应用** > **应用** > **添加**。  

3. 在“其他”下，选择“业务线应用”。  

4. 上传**ccmsetup.msi**应用包文件。 站点服务器上的 Configuration Manager 在以下文件夹中找到此文件： `<ConfigMgr installation directory>\bin\i386`。  

5. 更新应用程序后，使用命令行复制从 Configuration Manager 中配置应用信息。  

> [!IMPORTANT]    
> 如果自定义此命令行，请确保它不超过 1024年个字符。 命令行长度超过 1024年个字符时，客户端安装将失败。


