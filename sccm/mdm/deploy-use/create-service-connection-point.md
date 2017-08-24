---
title: "使用 System Center Configuration Manager 创建服务连接点 | Microsoft Docs"
description: "使用 System Center Configuration Manager 创建服务连接点。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 9a21d02cb2a50162e5de50481f0f27f2dd7a616c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 创建服务连接点

*适用范围：System Center Configuration Manager (Current Branch)*

创建了订阅后，你可以随后安装服务连接点站点系统角色，该角色使你能够连接到 Intune 服务。 此站点系统角色会将设置和应用程序推送到 Intune 服务。

 服务连接点将设置和软件部署信息发送到 Configuration Manager，并从移动设备中检索状态和清单消息。 Configuration Manager 服务充当与移动设备通信的网关并存储设置。

> [!NOTE]
>  服务连接点系统角色只能安装在管理中心站点或独立主站点上。 服务连接点必须具有 Internet 访问权限。


## <a name="configure-the-service-connection-point-role"></a>配置服务连接点角色

1.  在 Configuration Manager 控制台中，单击“管理” 。

2.  在“管理”工作区中，展开“站点”，然后单击“服务器和站点系统角色”。

3.  使用关联的步骤将“服务连接点”  角色添加到新的或现有的站点系统服务器：

    -   新站点系统服务器：在“主页”  选项卡上的“创建”  组中，单击“创建站点系统服务器”  以启动创建站点系统服务器向导。

    -   现有站点系统服务器：单击你要在其上安装服务连接点角色的服务器。 然后，在“主页”  选项卡上的“服务器”  组中，单击“添加站点系统角色”  以启动添加站点系统角色向导。

4.  在“系统角色选择”  页面上，选择“服务连接点” ，然后单击“下一步” 。
![创建服务连接点](../media/mdm-service-connection-point.png)

* 完成向导。

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>服务连接点如何通过 Microsoft Intune 服务进行身份验证？
 服务连接点通过与基于云的 Intune 服务建立连接扩展了 Configuration Manager，从而可通过 Internet 管理移动设备。 服务连接点按照以下方式通过 Intune 服务进行身份验证：

1.  在 Configuration Manager 控制台中创建 Intune 订阅时，通过连接到 Azure Active Directory 对 Configuration Manager 管理员进行身份验证，Azure Active Directory 将重定向到相应的 ADFS 服务器，提示输入用户名和密码。 然后，Intune 向租户颁发证书。

2.  步骤 1 中的证书安装在服务连接点站点角色上，用于对与 Microsoft Intune 服务的所有进一步通信进行身份验证和授权。

> [!div class="button"]
[< 上一步](terms-and-conditions.md)  [下一步 >](enable-platform-enrollment.md)
