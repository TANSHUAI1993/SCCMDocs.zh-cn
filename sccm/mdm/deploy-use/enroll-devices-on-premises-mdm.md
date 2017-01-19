---

title: "注册设备 | Microsoft Docs | MDM 系统中心"
description: "了解在 System Center Configuration Manager 中为本地移动设备管理注册设备的方法。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: 6
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d6479bcc134103e6005159a8ea295a5f359a436
ms.openlocfilehash: 9ecfef871b9082aad4c8f0cf933f963efd57c292


---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中为本地移动设备管理注册设备

*适用范围：System Center Configuration Manager (Current Branch)*

若要使用 System Center Configuration Manager 本地移动设备管理来管理计算机，需要注册设备，以便 Configuration Manager 能够与设备通信进行任务管理。 Configuration Manager 提供了两种注册设备的方法：  

-   “用户注册” - 在这种方法中，用户启动其设备上的注册过程。 为了使用户注册成功，必须在设备上安装受信任的根证书且用户必须设置为由 Configuration Manager 进行注册。  若要注册设备，用户只需提供工作凭据，设备就被注册为可管理状态。  

     有关详细信息，请参阅[用户如何在 System Center Configuration Manager 中向本地移动设备管理注册设备](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

-   “批量注册” - 这种方法中，设备用户不需要启动注册。 而是在 Configuration Manager 内创建批量注册程序包，然后将其放置到设备上并打开。 打开时，此包提供注册设备所需的信息。  

     有关详细信息，请参阅[如何在 System Center Configuration Manager 中向本地移动设备管理批量注册设备](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

 > [!NOTE]  
>  Configuration Manager 的 Current Branch 支持针对运行以下操作系统的设备的本地移动设备管理中的注册：  
>   
>  -   Windows 10 企业版  
> -   Windows 10 专业版  
> -   Windows 10 协同版（自 Configuration Manager 版本 1602 起）  
> -   Windows 10 移动版  
> -   Windows 10 移动企业版   



<!--HONumber=Dec16_HO3-->


