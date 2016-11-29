---
title: "Wi-Fi 配置文件简介 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中使用 Wi-Fi 配置文件为组织中的用户部署无线网络设置。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的 Wi-Fi 配置文件简介

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中使用 Wi-Fi 配置文件将无线网络设置部署到组织中的用户。 通过部署这些设置，你可最大程度减少最终用户连接到无线网络所需的工作。  

 例如，安装了名为“Contoso Wi-Fi” 的新 Wi-Fi 网络。 你现在想向所有运行 iOS 操作系统的设备提供连接到此网络所需的设置。 你可以创建一个 Wi-Fi 配置文件，其中包含连接到“Contoso Wi-Fi”  无线网络所必需的设置。 然后，你可以向其设备在你的层次结构中运行 iOS 的所有用户部署此配置文件。 IOS 设备的用户可以在无线网络列表中看到公司网络，并且可以容易地连接到此网络。  

 你可以使用 Wi-fi 配置文件配置下列设备类型：  

-   运行 Windows 8.1 (32 位) 的设备  

-   运行 Windows 8.1 (64 位) 的设备  

-   运行 Windows RT 8.1 的设备  

-   运行 Windows Phone 8.1 的设备  

-   运行 Windows 10 桌面或移动版的设备  

-   运行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 IPhone 设备  

-   运行 iOS 5、iOS 6、iOS 7 和 iOS 8 的 IPad 设备  

-   运行版本 4 的 Android 设备  

> [!IMPORTANT]  
>  若要将配置文件部署到 Android、iOS、Windows Phone 和注册的 Windows 8.1 或更高版本设备，这些设备必须在 Microsoft Intune 中注册。 有关如何注册设备的信息，请参阅 [使用 Microsoft Intune 管理移动设备](https://technet.microsoft.com/library/dn646962.aspx)。  

 在创建 Wi-Fi 配置文件时，你可以纳入各种各样的安全设置。 其中包括已通过使用 Configuration Manager 证书配置文件预配的服务器验证和客户端身份验证证书。 有关证书配置文件的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件](introduction-to-certificate-profiles.md)。  



<!--HONumber=Nov16_HO1-->


