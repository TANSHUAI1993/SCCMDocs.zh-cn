---
title: VPN 配置文件
titleSuffix: Configuration Manager
description: 了解如何使用 System Center Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的用户。
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d30e7cc834f1693f2cbcf2db840d650421062a19
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1283610-->
使用 Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的用户。 通过部署这些设置，你可以最大限度减少最终用户连接到公司网络资源需要进行的工作。  

 例如，你希望用连接到公司网络上的文件共享所需的设置来配置所有 Windows 10 设备。 可以用连接到公司网络所需的设置创建 VPN 配置文件。 然后将此配置文件部署至拥有运行 Windows 10 的设备的所有用户。 用户能在可用网络的列表中看到 VPN 连接，并可以轻松连接。  

 创建 VPN 配置文件时，可以纳入各种安全设置。 这些设置包括服务器验证和客户端身份验证（使用 Configuration Manager 证书配置文件预配）的证书。 有关详细信息，请参阅[证书配置文件](introduction-to-certificate-profiles.md)。  

> [!Note]  
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此选项。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  


 若要查看通过 Microsoft Intune 使用 Configuration Manager 时可配置的设备，请参阅[移动设备上的 VPN 配置文件](/sccm/mdm/deploy-use/create-vpn-profiles)。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>使用 Configuration Manager 时的 VPN 配置文件  
 下表介绍了可为各种设备平台配置的 VPN 配置文件。  

|连接类型|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|否|否|否|否|  
|**Pulse Secure**|是|否|是|是|  
| **F5 Edge Client**|是|否|是|是|  
|**Dell SonicWALL Mobile Connect**|是|否|是|是|  
|**Check Point Mobile VPN**|是|否|是|是|  
|**Microsoft SSL (SSTP)**|是|是|是|否|  
|**Microsoft Automatic**|是|是|是|否|  
|**IKEv2**|是|是|是|否|  
|**PPTP**|是|是|是|否|  
|**L2TP**|是|是|是|否|  

### <a name="next-steps"></a>后续步骤  
 可以使用下列主题来规划、配置、操作和维护 Configuration Manager 中的 VPN 配置文件。  

-   [System Center Configuration Manager 中 VPN 配置文件的先决条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中 VPN 配置文件的安全和隐私](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
