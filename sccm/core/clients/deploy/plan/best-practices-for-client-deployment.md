---
title: "客户端部署最佳实践 | Microsoft Docs"
description: "获取在 System Center Configuration Manager 中部署客户端的最佳方案。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 979c21c436429cad03a61671b707a99817146d95
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中部署客户端的最佳方案

*适用范围：System Center Configuration Manager (Current Branch)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>为 Active Directory 计算机使用基于软件更新的客户端安装  
 此客户端部署方法使用现有 Windows 技术，与 Active Directory 基础结构集成，在 Configuration Manager 中需要进行的配置最少，对于防火墙而言最容易配置，并且最为安全。 通过为组策略配置使用安全性组和 WMI 筛选，你还可以非常灵活地控制哪些计算机安装 Configuration Manager 客户端。  

 有关详细信息，请参阅 [如何使用基于软件更新的安装来安装 Configuration Manager 客户端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)。  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>扩展 Active Directory 架构并发布站点，以便能够不带命令行选项运行 CCMSetup  
 在扩展 Configuration Manager 的 Active Directory 架构并将站点发布到 Active Directory 域服务时，会将许多客户端安装属性发布到 Active Directory 域服务。 如果计算机可以找到这些客户端安装属性，则它可以在 Configuration Manager 客户端的部署过程中使用这些属性。 由于此信息自动生成，消除了与手动输入安装属性关联的人为错误风险。  

 有关详细信息，请参阅[关于 System Center Configuration Manager 中的发布到 Active Directory 域服务的客户端安装属性](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>使用分阶段推出管理 CPU 使用率  
 通过使用分阶段推出的客户端，最大程度降低 CPU 处理要求对站点服务器的影响。 在一天中的非工作时间部署客户端，以便其他服务有更多的可用带宽，并且在计算机速度较慢或者需要重启时，确保不会中断用户的工作。  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>在主客户端部署完成后启用自动升级  
 如果想要升级主要客户端安装方法遗漏的少数客户端计算机（可能因为脱机），则[自动客户端升级](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)很有用。 

> [!NOTE]  
>  Configuration Manager 中的性能改进可允许你使用自动升级作为主要客户端升级方法。 但是，性能将取决于层次结构基础架构，例如客户端数量。  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>如果使用 client.msi 属性安装客户端，请使用 SMSMP 和 FSP  
 SMSMP 属性指定初始管理点以使客户端与之通信，并删除服务位置解决方案上的依赖关系，例如 Active Directory 域服务、DNS 和 WINS。  

 使用 FSP 属性并安装回退状态点，以便你能够监视客户端安装和分配，并确定任何通信问题。  

 有关这些选项的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../../core/clients/deploy/about-client-installation-properties.md)。  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>在安装客户端之前安装客户端语言包。  
建议在部署客户端之前安装客户端语言包。 如果在安装客户端之后在站点上安装[客户端语言包](../../../../core/servers/deploy/install/language-packs.md)，则必须重新安装客户端，然后才能使用这些语言。 对于移动设备客户端，必须擦除并再次注册移动设备。  

## <a name="prepare-required-pki-certificates-in-advance"></a>提前准备所需的 PKI 证书  
 要管理 Internet 上的设备、注册的移动设备和 Mac 计算机，你在站点系统（管理点和分发点）以及客户端设备上必须有 PKI 证书。 在生产网络上，你可能需要变更管理批准以使用新证书，重启站点系统服务器，或者用户可能必须为新组成员身份注销和登录。 此外，你必须为安全权限的复制和任何新证书模板留出足够的时间。  

 有关所需 PKI 证书的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>在安装客户端之前，请配置任何必需的客户端设置和维护时段  
 尽管可以在安装客户端之前或之后[配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)和维护时段，但最好在安装客户端之前配置所需设置，以便在安装客户端之后即可使用这些设置。 

 为服务器和 Windows Embedded 设备配置维护时段，以确保关键设备的业务连续性。 维护时段将确保所需的软件更新和反恶意软件不会在工作时间内重启计算机。  

> [!IMPORTANT]  
>  对于计划使用统一写入筛选器 (UWF) 进行保护的 Windows 10 计算机，必须在安装客户端之前为 UWF 配置设备。 这使 Configuration Manager 可以使用自定义凭据提供程序安装客户端，该提供程序可在维护模式期间阻止低权限用户登录设备。  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>计划对于 Mac 计算机和移动设备的用户注册体验   
 如果用户将使用 Configuration Manager 注册他们自己的 Mac 计算机和移动设备，请计划用户体验。 例如，可以通过网页使用脚本完成安装和注册过程，以便用户输入最少量的必要信息，并通过电子邮件向用户发送包含链接的说明。  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>对 Windows Embedded 设备使用基于文件的写入筛选器 
 使用增强写入筛选器 (EWF) 的嵌入式设备可能会遇到状态消息重新同步。 如果只有少数使用增强写入筛选器的嵌入式设备，你可能不会注意到这一点。 但是，如果你有很多同步其信息（例如发送完整清单而不是增量清单）的嵌入式设备，这可能会明显增加网络数据包，并增加站点服务器上的 CPU 处理需求。  

 如果可以选择要启用的写入筛选器类型，请选择基于文件的写入筛选器，并配置例外以在设备下次重启之前保持客户端状态和清单数据，以在 Configuration Manager 客户端上提高网络和 CPU 效率。 有关写入筛选器的详细信息，请参阅   [在 System Center Configuration Manager 中计划 Windows Embedded 设备的客户端部署](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

 有关主站点可支持的最大 Windows Embedded 客户端数量的详细信息，请参阅[客户端和设备支持的操作系统](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。  
