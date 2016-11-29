---
title: "System Center Configuration Manager 中的 VPN 配置文件 | System Center Configuration Manager"
description: "了解如何使用 System Center Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的用户。"
ms.custom: na
ms.date: 10/10/2016
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
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: dda572392884c54b63af09a9fae79c1e73eb3d95


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 VPN 配置文件

*适用范围：System Center Configuration Manager (Current Branch)*


使用 System Center Configuration Manager 中的 VPN 配置文件将 VPN 设置部署到组织中的用户。 通过部署这些设置，你可以最大限度减少最终用户连接到公司网络资源需要进行的工作。  

 例如，你想要用连接到公司网络上的文件共享所需的设置来设置所有运行 IOS 操作系统的设备。 你可以创建一个 VPN 配置文件，在其中包含连接到公司网络所需的设置，然后将此配置文件部署到你的层次结构中使用运行 IOS 的设备的所有用户。 IOS 设备用户可在可用网络列表中看到 VPN 连接，并可通过最少量的工作连接到此网络。  

 在创建 VPN 配置文件时，你可以纳入各种各样的安全设置，其中包括已通过使用 System Center Configuration Manager 证书配置文件预配的服务器验证和客户端身份验证证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](introduction-to-certificate-profiles.md)。  

 以下各部分介绍了在使用 Configuration Manager 或带 Microsoft Intune 的 Configuration Manager 时，可向哪些设备配置 VPN 配置文件。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>使用 Configuration Manager 时的 VPN 配置文件  
 下表介绍了可为各种设备平台配置的 VPN 配置文件。  

|连接类型|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|否|否|否|否|  
|**Pulse Secure**|是|否|是|是|  
|** F5 Edge Client**|是|否|是|是|  
|**Dell SonicWALL Mobile Connect**|是|否|是|是|  
|**Check Point Mobile VPN**|是|否|是|是|  
|**Microsoft SSL (SSTP)**|是|是|是|否|  
|**Microsoft Automatic**|是|是|是|否|  
|**IKEv2**|是|是|是|否|  
|**PPTP**|是|是|是|否|  
|**L2TP**|是|是|是|否|  

## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>配合使用 Configuration Manager 和 Intune 时的 VPN 配置文件  
 若要将配置文件部署到 iOS、Android、Windows Phone 和 Windows 8.1 设备，必须将这些设备注册到 Microsoft Intune。 其他平台上的设备也可以注册到 Intune。 有关如何注册的信息，请参阅[使用 Microsoft Intune 管理移动设备](https://technet.microsoft.com/en-us/library/dn646962.aspx)。 下表显示了每个设备平台支持的连接类型：  

|连接类型|iOS 和 Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 桌面和移动版|  
|---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
|Cisco AnyConnect|是|是|否|否|否|否|是 (OMA-URI)|  
|脉冲安全|是|是|是|否|是|是|是|  
|F5 Edge Client|是|是|是|否|是|是|是|  
|Dell SonicWALL Mobile Connect|是|是|是|否|是|是|是|  
|Check Point Mobile VPN|是|是|是|否|是|是|是|  
|Microsoft SSL (SSTP)|否|否|是|是|是|否|否|  
|Microsoft Automatic|否|否|是|是|是|否|是 (OMA-URI)|  
|IKEv2|是（自定义策略）|否|是|是|是|是|是 (OMA-URI)|  
|PPTP|是|否|是|是|是|否|是 (OMA-URI)|  
|L2TP|是|否|是|是|是|否|是 (OMA-URI)|  

### <a name="next-steps"></a>后续步骤  
 可以使用下列主题来规划、配置、操作和维护 Configuration Manager 中的 VPN 配置文件。  

-   [System Center Configuration Manager 中 VPN 配置文件的先决条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager 中 VPN 配置文件的安全和隐私](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Nov16_HO1-->


