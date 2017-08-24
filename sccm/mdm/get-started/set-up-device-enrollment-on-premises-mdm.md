---
title: "设置设备注册 | Microsoft Docs"
description: "对用户授予在 System Center Configuration Manager 中向本地移动设备管理注册设备的权限。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
caps.latest.revision: "10"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 16d4106d486d821b7ce92a1de65ebb04469d18de
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>为 System Center Configuration Manager 中的本地移动设备管理设置设备注册

*适用范围：System Center Configuration Manager (Current Branch)*

要使用户可向 System Center Configuration Manager 本地移动设备管理注册设备，需要授予其执行此操作的权限。 若要向用户授予注册设备的权限，请执行以下任务。

-   [创建允许用户注册新式设备的注册配置文件](#bkmk_createProf)  

-   [为注册的设备设置其他客户端设置](#bkmk_addClient)  

-   [使用户能够接收新式设备注册配置文件](#bkmk_enableUsers)  

-   [在要注册的设备上存储根证书](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> 创建允许用户注册新式设备的注册配置文件  
 为了推送允许用户注册新式设备所需的设置，可以向默认客户端设置添加新的注册配置文件，该配置文件适用于 Configuration Manager 站点中发现的所有用户。  

1.  在 Configuration Manager 控制台中，单击“管理” > “概述” > “客户端设置”，打开“默认客户端设置”并选择“注册”。  

2.  在“设备设置”下，为新式设备指定轮询间隔。  

3.  在“用户设置”下，为“允许用户注册新式设备”  选择“是” 。  

4.  在“新式设备注册配置文件”旁，单击“设置配置文件…”，然后单击“创建…”  

5.  在“创建注册配置文件”中，键入注册配置文件的名称，然后选择你希望具有该注册配置文件的用户使用的管理站点代码。 单击“确定”  数次以退出“默认设置”页。  

> [!NOTE]  
>  如果你希望将注册配置文件部署到的已发现用户的子集，则可以使用用户集合，并创建要部署到该集合的自定义客户端设置。 有关创建自定义客户端设置的信息，请参阅 [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="bkmk_addClient"></a> 为注册的设备设置其他客户端设置  
 除了为新式设备设置注册配置文件之外，还可以设置其他客户端设置以便在注册设备时配置它们。  有关设置客户端设置的信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

 并非所有客户端设置都对本地移动设备管理可用。 Configuration Manager 的 current branch 支持以下用于本地移动设备管理的客户端设置：  

-   注册 - 这些设置为托管设备设置注册配置文件。 有关如何设置注册配置文件的详细信息，请参阅 [创建允许用户注册新式设备的注册配置文件](#bkmk_createProf)。  

-   客户端策略 - 这些设置指定将客户端策略下载到设备的频率。 还可以启用设置以便使用策略轮询确定目标用户。 有关客户端策略设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../core/clients/deploy/about-client-settings.md)中的“客户端策略”部分。  

-   软件部署 - 此设置可设置为软件部署评估客户端设备的间隔。 有关软件部署设置的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../core/clients/deploy/about-client-settings.md)中的“软件部署”部分  

    > [!NOTE]  
    >  对于本地移动设备管理，软件部署设置只能用作默认客户端设置。 在 Configuration Manager 的 current branch 中，软件部署设置不能与自定义客户端设置一起使用。  

##  <a name="bkmk_enableUsers"></a> 使用户能够接收新式设备注册配置文件  
 为使用户接收具有本地移动设备管理的注册配置文件的已修改客户端设置，必须通过 Active Directory 发现方法发现它们。 为了确保需要注册配置文件的每个人能够获得它，请运行对 Active Directory 用户运行发现。 有关如何发现用户的说明，请参阅 [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md)。  

##  <a name="bkmk_storeCert"></a> 在要注册的设备上存储根证书  
 由于根是作为域加入过程的一部分与 Active Directory 一起颁发的，所以使用已加入域的设备的用户将很可能已具有所需根证书，能够与站点系统角色的宿主服务器进行受信任的通信。 未加入域的计算机和移动设备将需要在设备上手动安装的根证书才能进行注册。 这些设备将不自动具有所需根证书。  

 必须向设备提供导出的证书文件才能进行手动安装。 可使用电子邮件、OneDrive、SD 卡、USB 拇指驱动器或最能满足你的需求的任何方法完成此操作。  

 你想要在设备上使用的根证书是在[导出根与 Web 服务器证书的根相同的证书](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)中导出的。  

1.  在要注册的设备上，找到并双击该根证书文件。  

2.  在“证书”窗口中，单击“安装证书...”  

3.  在“证书导入向导”中，选择“本地计算机” 并单击“下一步” 。  

4.  在“用户帐户控制”窗口中，选择“是” 。  

5.  选择“将所有的证书放入下列存储” ，然后单击“浏览” 。  

6.  依次单击“受信任的根证书颁发机构” 和“确定” ，然后单击“下一步” 。  

7.  单击 **“完成”**。  
