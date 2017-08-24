---
title: "安装站点系统角色 | Microsoft Docs"
description: "向导帮助用户将站点系统角色添加到站点中的现有站点系统服务器或新的站点系统服务器。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76b070f8e203cc0c751f35e5a4b4904504786c04
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>安装 System Center Configuration Manager 的站点系统角色

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 控制台具有可用于安装站点系统角色的两个向导：  

-   **添加站点系统角色向导**：使用此向导将站点系统角色添加到站点中的现有站点系统服务器。  

-   **创建站点系统服务器向导**：使用此向导将新服务器指定为站点系统服务器，然后在该服务器上安装一个或多个站点系统角色。 此向导与“添加站点系统角色向导” 相同，只是你必须在第一页上指定要使用的服务器的名称以及你要在其进行安装的站点。  

当你将站点系统角色安装到远程计算机（包括 SMS 提供程序的实例）上时，会将远程计算机的计算机帐户添加到站点服务器上的本地组。 在域控制器上安装站点后，站点服务器上的组是域组而不是本地组。 在这种情况下，站点系统角色计算机重启或远程计算机帐户的 Kerberos 票证刷新前，远程站点系统角色不会运行。 有关详细信息，请参阅 [System Center Configuration Manager 中使用的帐户](../../../../core/plan-design/hierarchy/accounts.md)。  

在即将安装站点系统角色之前，Configuration Manager 会检查目标计算机，以确保其满足所选站点系统角色的先决条件。 了解有关安装站点系统角色的以下各项：  

-   默认情况下，当 Configuration Manager 安装站点系统角色时，安装文件将安装在具有最多可用磁盘空间的第一个 NTFS 格式的磁盘驱动器上。 若要防止 Configuration Manager 在特定驱动器上安装，可创建名为 **no_sms_on_drive.sms** 的空文件。 安装站点系统服务器之前，将其复制到驱动器的根文件夹。  

-   Configuration Manager 使用**站点系统安装帐户**来安装站点系统角色。 你在运行适用的向导来创建新站点系统服务器或向现有站点系统服务器中添加站点系统角色时指定此帐户。 默认情况下，此帐户是站点服务器计算机的本地系统帐户，但你可以指定域用户帐户以供用作站点系统安装帐户。 有关详细信息，请参阅 [System Center Configuration Manager 中使用的帐户](../../../../core/plan-design/hierarchy/accounts.md)。  

##  <a name="bkmk_Install"></a>在现有站点系统服务器上安装站点系统角色  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，并单击“服务器和站点系统角色” 。 然后选择要用于新站点系统角色的服务器。  

3.  在“主页”  选项卡上的“服务器”  组中，单击“添加站点系统角色” 。  

4.  在“常规”  页上查看设置，然后单击“下一步” 。  

    > [!TIP]  
    >  要从 Internet 访问站点系统角色，请确保指定 Internet 完全限定的域名 (FQDN)。  

5.  在“代理”页上，如果此站点系统服务器上运行的站点系统角色需要代理服务器来连接到 Internet 上的位置，请指定代理服务器的设置。 然后单击 **“下一步”**。  

6.  在“系统角色选择”  页上，选择要添加的站点系统角色，然后单击“下一步” 。  

7.  完成向导。  

> [!TIP]  
>  Windows PowerShell cmdlet New-CMSiteSystemServer 执行与此过程相同的功能。 有关详细信息，请参阅 Microsoft System Center 2012 Configuration Manager SP1 Cmdlet 参考文档中的 [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414)。  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>在新的站点系统服务器上安装站点系统角色  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，并单击“服务器和站点系统角色” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建站点系统服务器” 。  

4.  在“常规”  页上，指定站点系统的常规设置，然后单击“下一步” 。  

    > [!TIP]  
    >  要从 Internet 中访问新的站点系统角色，请确保指定 Internet FQDN。  

5.  在“代理”页上，如果此站点系统服务器上运行的站点系统角色需要代理服务器来连接到 Internet 上的位置，请指定代理服务器的设置。 然后单击 **“下一步”**。  

6.  在“系统角色选择”  页上，选择要添加的站点系统角色，然后单击“下一步” 。  

7.  完成向导。  

> [!TIP]  
>  Windows PowerShell cmdlet New-CMSiteSystemServer 执行与此过程相同的功能。 有关详细信息，请参阅 Microsoft System Center 2012 Configuration Manager SP1 Cmdlet 参考文档中的 [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414)。  
