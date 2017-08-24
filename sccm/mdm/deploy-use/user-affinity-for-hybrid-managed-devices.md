---
title: "Configuration Manager 中混合托管设备的用户关联 | Microsoft Docs"
description: "配置 Configuration Manager 中托管设备的用户关联。"
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: "6"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: d039792a88b9e7704f37718a88f841dd9216d1b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Configuration Manager 中混合托管设备的用户关联

*适用范围：System Center Configuration Manager (Current Branch)*

配置公司拥有的设备的配置文件时，管理员可以指定托管设备是否可以具有“用户关联”（用于标识设备的特定用户）。  

##  <a name="BKMK_iOSCP"></a>具有用户关联的托管设备  
 配置了“用户关联”的设备可以安装和运行公司门户应用，以下载应用和管理设备。 用户收到设备后，必须完成一些其他步骤，以便完成设置助理并安装公司门户应用。  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>如何注册具有用户关联的 iOS 设备  

1.  用户首次打开新设备时，系统会提示其完成设置助理。 注册配置文件可以指定在安装过程中提示输入凭据。 用户必须使用与其在 Intune 中的订阅相关联的凭据（即唯一的个人名称或 UPN）。  

2.  安装过程中，系统还可能提示用户输入 Apple ID。 必须提供 Apple ID 设备才能安装公司门户。 用户也可以在安装完成后在 iOS“设置”菜单中提供 Apple ID。  

3.  安装完成后，iOS 设备必须从应用商店安装公司门户应用，例如[公司门户应用](https://itunes.apple.com/us/app/id719171358)。  

4.  现在用户可以使用在设置设备时使用的 UPN 登录公司门户。  

5.  登录后，系统会提示用户注册其设备。 第一步是“识别其设备”。 应用会提供一份已向企业注册并已分配到最终用户的 Intune 帐户的 iOS 设备列表。 选择匹配的设备。  

     如果该设备还不是企业拥有的设备，选择“新设备”以继续标准注册流程。  

6.  在下一个屏幕上，用户必须确认新设备的序列。 用户可以点击“确认序列号”链接以启动设置应用程序来验证序列号。 然后用户必须将序列号的最后 4 个字符输入到公司门户应用中。  

     此步骤验证该设备是否是在 Intune 中注册的企业设备。 如果设备上的序列号不匹配，则选择了错误的设备。 返回到上一屏幕并选择其他设备。  

7.  验证序列号后，公司门户应用将重定向到公司门户网站以完成注册，然后会提示用户返回到应用。  

8.  注册现已完成。 现在你可以使用此设备的完整功能集。  

##  <a name="BKMK_noUA"></a>不具有用户关联的托管设备  
 配置为“无用户关联”的设备不支持公司门户，因此不能安装该应用。 公司门户适用于具有企业凭据的用户，并且需要访问个性化企业资源（例如邮件）的权限。 注册为“无用户关联”的设备并不具有专用的用户登录。 展台、销售点 (POS) 或共享实用程序设备是注册为“无用户关联”的设备的典型用例。 如果需要用户关联，注册设备前请确保设备的注册配置文件选中“用户关联”。 若要更改设备的关联状态，必须停用并重新注册设备。
