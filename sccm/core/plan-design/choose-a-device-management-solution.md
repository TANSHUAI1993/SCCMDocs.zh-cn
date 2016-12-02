---
title: "选择 System Center Configuration Manager 的设备管理解决方案"
description: "了解 System Center Configuration Manager 提供的用于管理电脑、服务器和设备的解决方案。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>选择 System Center Configuration Manager 的设备管理解决方案

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 提供用于管理 PC、服务器和设备的不同解决方案。 可以根据进行管理所需的设备平台和所需的管理功能来选择最适合的解决方案。  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> 设备管理解决方案概述  
 提供了以下使用 Configuration Manager 管理计算机和设备的选项：  

-   **使用 Configuration Manager 客户端管理设备**  

     此选项（要求在每台要管理的设备上安装 Configuration Manager 客户端应用程序）提供用于管理电脑、服务器和环境中的其他设备的最全面的功能。 此选项是 Configuration Manager 提供设备管理的传统方法，在过去的产品版本中便已存在。  

     有关此解决方案的详细信息，请参阅 [System Center Configuration Manager 中的客户端安装方法](/sccm/core/client/deploy/plan/client-installation-methods)。  

-   **使用本地 Configuration Manager 基础结构管理移动设备**  

     此选项使用内置于特定设备平台的操作系统的设备管理功能。 尽管没有基于客户端的管理的功能全面，本地移动设备管理为使用本地 Configuration Manager 资源访问和管理设备的管理提供更轻巧的触点方法。 本地移动设备管理目前仅支持 Windows 10 电脑和 Windows 10 移动设备。  

     有关此解决方案的详细信息，请参阅[在 System Center Configuration Manager 中使用本地基础结构管理移动设备](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

-   **使用 Microsoft Intune（混合）管理移动设备**  

     此选项称为混合移动设备管理。  它使用 Microsoft Intune 注册和管理设备，而不是使用 Configuration Manager 本地资源。 尽管由 Intune 管理设备，但你需要在 Configuration Manager 控制台中控制管理任务。 此选项支持所有主要移动设备操作系统，包括 Windows 10 Mobile、Windows Phone、iOS 以及 Android。 它还为组织中的 Windows 8.1 和 Windows 10 计算机提供管理。  

     有关此解决方案的详细信息，请参阅[使用 System Center Configuration Manager 和 Microsoft Intune 的混合移动设备管理 (MDM)](../../mdm/plan-design/hybrid-mobile-device-management.md)。  

-   **使用 Exchange 管理移动设备**  

     此选项（使用 Exchange Server 连接器将多个 Exchange 服务器连接到 Configuration Manager）集中管理可连接到 Exchange ActiveSync 的设备。 可从 Configuration Manager 控制台配置 Exchange 移动设备管理功能，例如远程设备擦除和针对多个 Exchange 服务器的设置控制。  

     有关此解决方案的详细信息，请参阅[使用 System Center Configuration Manager 和 Exchange 管理移动设备](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

 可以使用这些本身相互结合的设备管理解决方案。 例如，可以使用基于客户端的管理方法来介绍管理组织中的计算机和服务器，也可以使用基于 Intune 的管理来管理移动设备。 通过这样组合方法，你可以满足所有设备管理需求并可以完全从 Configuration Manager 控制台对它进行控制。  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> 根据支持的移动设备平台比较设备管理解决方案  

|平台|带 Configuration Manager 客户端|带 Microsoft Intune 的 Configuration Manager（混合）|本地移动设备管理|带 Exchange 的 Configuration Manager|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||是||是|  
|iOS||是||是|  
|Mac OS X|是|||是|  
|UNIX/Linux|是|||是|  
|Windows 10|是|是|是|是|  
|Windows 10 移动版||是|是|是|  
|Windows（以前的版本）|是|是||是|  
|Windows CE|是（具有移动设备旧客户端）|||是|  
|Windows Embedded|是||||  
|Windows Phone||是||是|  
|Windows Server|是|||是|  

 有关支持的平台的完整列表，请参阅 [System Center Configuration Manager 客户端和设备支持的操作系统](configs\supported-operating-systems-for-clients-and-devices.md)。

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> 根据管理功能比较移动设备管理解决方案  

|管理功能|带 Configuration Manager 客户端|带 Microsoft Intune 的 Configuration Manager（混合）|本地移动设备管理|带 Exchange 的 Configuration Manager|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|移动设备和 Configuration Manager 之间的公钥基础结构 (PKI) 安全性通过使用相互身份验证和 SSL 来加密数据传输|是|是|是||  
|客户端安装|是||||  
|通过 Internet 提供的支持|是||||  
|发现|是|||是|  
|硬件清单|是|是|是|是|  
|软件清单|是|||是|  
|设置|是|是|是|是|  
|软件部署|是|是|是||  
|利用回退状态点进行监视|是||||  
|连接到管理点|是||是||  
|连接到分发点|是|是|是||  
|通过 Configuration Manager 进行阻止|是|是|是||  
|通过 Exchange Server 和 Configuration Manager 进行隔离和阻止||||是|  
|远程擦除|是|是|是|是|  



<!--HONumber=Nov16_HO1-->


