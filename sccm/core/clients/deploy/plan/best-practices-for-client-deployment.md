---
title: "客户端部署最佳实践 | Microsoft Docs"
description: "获取在 System Center Configuration Manager 中部署客户端的最佳方案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 49b2520a82614bedc7bcc077604e0b89885119c2


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中部署客户端的最佳方案

*适用范围：System Center Configuration Manager (Current Branch)*

以下信息介绍了使用 System Center Configuration Manager 在计算机上部署客户端的最佳方案。  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>为 Active Directory 计算机使用基于软件更新的客户端安装  
 此客户端部署方法具有使用现有 Windows 技术的优势，与 Active Directory 基础结构集成，在 Configuration Manager 中需要进行的配置最少，对于防火墙而言最容易配置，并且最为安全。 通过为组策略配置使用安全性组和 WMI 筛选，你还可以非常灵活地控制哪些计算机安装 Configuration Manager 客户端。  

 有关详细信息，请参阅 [如何使用基于软件更新的安装来安装 Configuration Manager 客户端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)。  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>扩展 Active Directory 架构并发布站点，以便能够不带命令行选项运行 CCMSetup  
 在扩展 Configuration Manager 的 Active Directory 架构并将站点发布到 Active Directory 域服务时，会将许多客户端安装属性发布到 Active Directory 域服务。 如果计算机可以找到这些客户端安装属性，则它可以在 Configuration Manager 客户端的部署过程中使用这些属性。 由于此信息自动生成，消除了与手动输入安装属性关联的人为错误风险。  

 有关详细信息，请参阅[关于 System Center Configuration Manager 中的发布到 Active Directory 域服务的客户端安装属性](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>如果有许多要部署的客户端，请计划工作时间外的分阶段转出  
 通过计划在一段时间内分阶段转出客户端，从而最大程度地降低对站点服务器上的 CPU 处理要求的影响。 在一天当中的工作时间之外部署客户端，以使关键业务服务有更多的可用带宽，并且，在用户计算机的速度变慢或者需要重启来完成安装的情况下，将不会中断用户的工作。  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>在主客户端部署完成后启用自动升级  
 如果想要升级可能被主要客户端安装方法遗漏的少数客户端计算机，则自动客户端升级很有用。 例如，你已经完成了初始客户端升级，但在升级部署过程中有些客户端处于脱机状态。 则可以使用此方法在这些计算机下次处于活动状态时升级其上的客户端。  

> [!NOTE]  
>  Configuration Manager 中的性能改进可允许你使用自动升级作为主要客户端升级方法。 但是，性能将取决于层次结构基础架构，例如客户端数量。  

 有关客户端自动升级方法的详细信息，请参阅[如何在 System Center Configuration Manager 中升级 Windows 计算机的客户端](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)。  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>如果使用 client.msi 属性安装客户端，请使用 SMSMP 和 FSP  
 SMSMP 属性指定初始管理点以使客户端与之通信，并删除服务位置解决方案上的依赖关系，例如 Active Directory 域服务、DNS 和 WINS。  

 使用 FSP 属性并安装回退状态点，以便你能够监视客户端安装和分配，并确定任何通信问题。  

 有关这些选项的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../../core/clients/deploy/about-client-installation-properties.md)。  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>如果需要使用除英语外的其他客户端语言，请在安装客户端之前安装客户端语言包  
 如果你在安装客户端之后在站点上安装客户端语言包，则必须重新安装客户端，然后才能使用其他语言。 对于移动设备客户端，这意味着你必须擦除并再次注册移动设备。  

 有关如何添加对其他客户端语言的支持的详细信息，请参阅 [System Center Configuration Manager 中的语言包](../../../../core/servers/deploy/install/language-packs.md)。  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>提前规划和准备任何所需的 PKI 证书  
 要管理 Internet 上的设备、注册的移动设备和 Mac 计算机，你在站点系统（管理点和分发点）以及客户端设备上必须有 PKI 证书。 对于许多客户，这需要提前计划和准备，特别是在你有管理 PKI 的单独团队的情况下尤为如此。 在生产网络上，你可能需要变更管理批准以使用新证书，重启站点系统服务器，或者用户可能必须为新组成员身份注销和登录。 此外，你必须为安全权限的复制和任何新证书模板留出足够的时间。  

 有关需要的 PKI 证书的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>在安装客户端之前，请配置任何必需的客户端设置和维护时段  
 尽管你可以在安装客户端之前或之后配置客户端设置和维护时段，但请在安装客户端之前配置任何必需的设置，以便在安装客户端之后立即使用这些设置。 有关详细信息，请参阅 [如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

 为服务器和 Windows Embedded 设备配置维护时段，以确保这些通常对于业务很关键的计算机的业务连续性。 例如，维护时段将确保所需的软件更新和反恶意软件不会在工作时间内重启计算机。  

> [!IMPORTANT]  
>  对于计划使用统一写入筛选器 (UWF) 进行保护的 Windows 10 计算机，必须在安装客户端之前为 UWF 配置设备。 这使 Configuration Manager 可以使用自定义凭据提供程序安装客户端，该提供程序可在维护模式期间阻止低权限用户登录设备。  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>对于通过 Configuration Manager 注册的 Mac 计算机和移动设备，请计划你的用户注册体验  
 如果用户将通过使用 Configuration Manager 注册他们自己的 Mac 计算机和移动设备，请计划和准备用户体验。 例如，你可以通过网页使用脚本完成安装和注册过程以便用户输入最少量的必要信息，并通过电子邮件向用户发送包含链接的说明。  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>当你管理 Windows Embedded 设备时，请使用基于文件的写入筛选器 (FBWF)（而不是增强写入筛选器 (EWF)）来提高可伸缩性  
 使用增强写入筛选器 (EWF) 的嵌入式设备可能会遇到状态消息重新同步。 如果只有少数使用增强写入筛选器的嵌入式设备，你可能不会注意到这一点。 但是，如果你有很多同步其信息（例如发送完整清单而不是增量清单）的嵌入式设备，这可能会明显增加网络数据包，并增加站点服务器上的 CPU 处理需求。  

 如果可以选择要启用的写入筛选器类型，请选择基于文件的写入筛选器，并配置例外以在设备下次重启之前保持客户端状态和清单数据，以在 Configuration Manager 客户端上提高网络和 CPU 效率。 有关写入筛选器的详细信息，请参阅   [在 System Center Configuration Manager 中计划 Windows Embedded 设备的客户端部署](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

 有关主站点可支持的最大 Windows Embedded 客户端数量的详细信息，请参阅[客户端和设备支持的操作系统](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。  



<!--HONumber=Dec16_HO3-->


