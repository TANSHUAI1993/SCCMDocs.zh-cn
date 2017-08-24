---
title: "用户如何向本地 MDM 注册设备 - Configuration Manager | Microsoft Docs"
description: "了解用户如何在 System Center Configuration Manager 中向本地移动设备管理注册设备。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 8c7438c2cc0bc66654eb3e74de10553df53181d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>用户如何在 System Center Configuration Manager 中向本地移动设备管理注册设备

*适用范围：System Center Configuration Manager (Current Branch)*

借助 System Center Configuration Manager 本地移动设备管理，如果用户已获得注册权限（通过更新客户端设置的方式）并且设备已安装所需的根证书以与承载所需站点系统角色的服务器进行受信任的通信，则可以注册设备。 有关如何设置注册的详细信息，请参阅 [Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)（在 System Center Configuration Manager 中为本地移动设备管理设置设备注册）。  

> [!NOTE]  
>  Configuration Manager 的 Current Branch 支持针对运行以下操作系统的设备的本地移动设备管理中的注册：  
>   
> -  Windows 10 企业版  
> -   Windows 10 专业版  
> -   Windows 10 协同版\(自 Configuration Manager 版本 1602 起\)  
> -   Windows 10 移动版  
> -   Windows 10 移动企业版
> -   Windows 10 IoT 企业版   

以下任务说明了如何注册和验证本地移动设备管理的计算机和设备的注册：  

-   [注册 Windows 10 计算机](#bkmk_enrollDesk)  

-   [注册 Windows 10 移动版设备](#bkmk_enrollMob)  

-   [验证设备注册](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> 注册 Windows 10 计算机  

1.  在 Windows 10 计算机上，转到“设置” 。  

2.  单击“帐户” ，然后单击“工作单位访问” 。  

3.  在“工作单位访问”下的“连接到工作单位或学校” 中，单击“连接” ，输入工作电子邮件地址，然后单击“继续” 。  

4.  输入承载注册代理点站点系统角色的服务器的 FQDN，然后单击“继续”。  

5.  在“连接到服务”中，输入你的工作电子邮件密码，然后单击“登录” 。  

6.  单击“跳过”  以记住登录信息，不久过后将连接设备。  

##  <a name="bkmk_enrollMob"></a> 注册 Windows 10 移动版设备  

1.  在 Windows 10 移动版设备上，转到“设置” 。  

2.  单击“帐户” ，然后单击“工作单位访问” 。  

3.  单击“连接” 。  

4.  输入你的工作电子邮件地址以及承载注册代理点站点系统角色的服务器的 FQDN。 单击“连接” 。  

5.  在下一个屏幕上，输入你的工作电子邮件地址和密码，然后单击“登录” 。 不久过后，设备将完成注册。 单击“Done”（完成） 。  

##  <a name="bkmk_verify"></a> 验证设备注册  
 可以在 Configuration Manager 控制台中验证是否已成功注册设备。  

1.  启动 Configuration Manager 控制台。  

2.  单击“关闭”  >  > 所需的站点系统角色之间进行受信任的通信需要此根证书。 列表中将显示已注册的设备。  
