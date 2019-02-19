---
title: 选择设备管理解决方案
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 提供的用于管理电脑、服务器和设备的解决方案。
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2b396ad5955227494511355f6efdb88ecd901110
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120825"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>选择 Configuration Manager 的设备管理解决方案

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 提供了用于管理 PC、服务器和设备的多种解决方案。 请选择适合你组织的解决方案。 可以根据进行管理所需的设备平台和所需的管理功能来决定选择哪种解决方案。  


> [!Important]  
> 自 2018 年 8 月 14 日起，混合移动设备管理[功能停用](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)。 有关详细信息，请参阅[什么是混合 MDM](/sccm/mdm/understand/hybrid-mobile-device-management)。<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>概述

本文介绍以下四种设备管理解决方案： 
- [Configuration Manager 客户端](#bkmk_sccm)
- [通过 Configuration Manager 实现本地移动设备管理 (MDM)](#bkmk_opmdm)
- [使用 Microsoft Intune 进行共同管理](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

可以使用这些设备管理解决方案本身或彼此之间相互结合使用。 例如，你可以使用基于客户端的管理方法来管理组织中的计算机和服务器，同时使用共同管理来管理基于 Internet 的笔记本电脑。 通过这样的组合方法，可以满足所有设备管理需求。  

本文还包含两个表，根据以下因素对管理解决方案进行比较： 
- [根据支持的平台进行比较](#bkmk_comp1)
- [根据管理功能进行比较](#bkmk_comp2)


### <a name="bkmk_sccm"></a> Configuration Manager 客户端  

此选项要求在设备上安装 Configuration Manager 客户端。 它提供管理你环境中的电脑、服务器和其他设备的大多数功能。 

有关详细信息，请参阅[客户端安装方法](/sccm/core/clients/deploy/plan/client-installation-methods)。  


### <a name="bkmk_opmdm"></a> 本地 MDM  

此选项使用内置于 Windows 10 的设备管理功能。 尽管没有基于客户端管理的功能全面，但本地移动设备管理可提供更轻松的触点方法来进行管理。 它使用本地 Configuration Manager 资源来管理设备。  

有关详细信息，请参阅[使用本地基础结构管理移动设备](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)。  


### <a name="bkmk_comanage"></a>使用 Microsoft Intune 进行共同管理

共同管理是将现有 Configuration Manager 部署附加到 Microsoft 365 云的主要方式之一。 它使你能够使用 Configuration Manager 和 Microsoft Intune 同时管理 Windows 10 设备。 借助共同管理，可以通过添加新功能在 Configuration Manager 中云附加现有投资。 

有关详细信息，请参阅[什么是共同管理？](/sccm/comanage/overview)  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

此选项使用 Exchange Server 连接器将多个 Exchange 服务器连接到 Configuration Manager。 以便集中管理连接到 Exchange ActiveSync 的设备。 你可以在 Configuration Manager 控制台中配置 Exchange 移动设备管理功能。 示例功能包括针对多个 Exchange 服务器的远程设备擦除和设置控制。

有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)。  



## <a name="bkmk_comp1"></a> 按支持的平台比较解决方案  

|平台|Configuration Manager 客户端|本地 MDM|带 Exchange 的 Configuration Manager|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |是|  
|iOS| | |是|  
|Mac OS X|是| |是|  
|UNIX/Linux|是| |是|  
|Windows 10|是|是|是|  
|Windows 10 移动版| |是|是|  
|Windows（以前版本）|是| |是|  
|Windows Server|是| |是|  
|Windows CE|是（具有移动设备旧客户端）| |是|  
|Windows Embedded|是| | |  
|Windows Mobile| | |是|  

有关支持的平台的完整列表，请参阅 [System Center Configuration Manager 客户端和设备支持的操作系统](configs/supported-operating-systems-for-clients-and-devices.md)。

Microsoft 建议使用 Intune 来管理 Android、iOS 和 Windows 10 移动设备。 有关更多信息，请参阅[什么是 Microsoft Intune？](https://docs.microsoft.com/intune/what-is-intune)



##  <a name="bkmk_comp2"></a>根据管理功能比较解决方案  

|管理功能|Configuration Manager 客户端|本地 MDM|带 Exchange 的 Configuration Manager|  
|--------|----------------------------|---------------|-----------------------------------|  
|移动设备和 Configuration Manager 之间的公钥基础结构 (PKI) 安全性（使用相互身份验证和 SSL 加密数据传输）|是|是| |  
|客户端安装|是| | |  
|通过 Internet 提供的支持|是| | |  
|发现|是| |是|  
|硬件清单|是|是|是|  
|软件清单|是| |是|  
|设置|是|是|是|  
|软件部署|是|是| |  
|利用回退状态点进行监视|是| | |  
|连接到管理点|是|是| |  
|连接到分发点|是|是| |  
|通过 Configuration Manager 进行阻止|是|是| |  
|通过 Exchange Server 和 Configuration Manager 进行隔离和阻止| | |是|  
|远程擦除| |是|是|  


