---
title: "发布和 Active Directory 架构 | Microsoft Docs"
description: "为 System Center Configuration Manager 扩展 Active Directory 架构，以简化部署和配置客户端的过程。"
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: "17"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 58beef440db8e019a06ce7c4c8eaabc8e85ce954
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-active-directory-for-site-publishing"></a>为站点发布准备 Active Directory

*适用范围：System Center Configuration Manager (Current Branch)*

为 System Center Configuration Manager 扩展 Active Directory 架构时，向 Configuration Manager 站点所使用的 Active Directory 引入新结构，以便将关键信息发布在客户端可以轻松访问的安全位置。  

建议使用具有扩展的 Active Directory 架构的 Configuration Manager 来管理本地客户端。 扩展架构可以简化部署和设置客户端的过程。 扩展架构还可让客户端高效查找资源，如不同 Configuration Manager 站点系统角色提供的内容服务器和其他服务。  

-   如果不熟悉提供 Configuration Manager 部署的扩展架构，可参阅 [System Center Configuration Manager 的架构扩展](../../../core/plan-design/network/schema-extensions.md)帮助你做出这一决定。  

-   不使用扩展的架构时，可以设置其他方法（例如 DNS 和 WINS）来查找服务和站点系统服务器。 这些服务定位方法需要附加配置，不是客户端进行服务定位的首选方法。 若要了解详细信息，请阅读[了解客户端如何查找 System Center Configuration Manager 的站点资源和服务](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)。  

-   如果已为 Configuration Manager 2007 或 System Center 2012 Configuration Manager 扩展了 Active Directory 架构，则不需要执行其他操作。 架构扩展不变，并已就位。  

扩展架构是用于任何林的一次性操作。 若要进行扩展并使用扩展的 Active Directory 架构，请遵循以下步骤：  

## <a name="step-1-extend-the-schema"></a>步骤 1。 扩展架构  
为 Configuration Manager 扩展架构：  

-   使用属于“架构管理员”安全组成员的帐户。  

-   登录架构主域控制器。  

-   运行 **Extadsch.exe** 工具，或将 LDIFDE 命令行实用程序用于 **ConfigMgr_ad_schema.ldf** 文件。 工具和文件均位于 Configuration Manager 安装媒体上的 **SMSSETUP\BIN\X64** 文件夹中。  

#### <a name="option-a-use-extadschexe"></a>选项 A：使用 Extadsch.exe  

1.  运行 **extadsch.exe** ，将新类和属性添加到 Active Directory 架构。  

    > [!TIP]  
    >  从命令行运行此工具，以便在它运行时查看反馈。  

2.  通过查看系统驱动器根目录中的 extadsch.log，验证架构扩展是否成功。  

#### <a name="option-b-use-the-ldif-file"></a>选项 B：使用 LDIF 文件  

1.  编辑 **ConfigMgr_ad_schema.ldf** 文件以定义你希望扩展的 Active Directory 根域：  

    -   将该文件中文本“DC=x”的所有实例替换为要扩展的域的完整名称。  

    -   例如，如果要扩展的域的完整名称为 widgets.microsoft.com，则将文件中 DC=x 的所有实例更改为 **DC=widgets, DC=microsoft, DC=com**。  

2.  使用 LDIFDE 命令行实用工具将“ConfigMgr_ad_schema.ldf”文件的内容导入 Active Directory 域服务：  

    -   例如，下列命令行会将架构扩展导入 Active Directory 域服务，启用详细日志记录，并在导入过程中创建一个日志文件：**ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;location to store log file\>**。  

3.  通过查看上一步中使用的命令行所创建的日志文件，可以验证架构扩展是否成功。  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>步骤 2。  创建系统管理容器，并向该容器授予站点权限  
 扩展架构之后，必须在 Active Directory 域服务 (AD DS) 中创建名为“系统管理”的容器：  

-   在具有将向 Active Directory 发布数据的主站点或辅助站点的每个域中创建一次此容器。  

-   对于每个容器，向发布数据到域的每个主站点和辅助站点服务器的计算机帐户授予权限。 每个帐户都需要对容器具有“完全控制”权限，并且高级权限“应用到”等于“这个对象及全部后代”。  

#### <a name="to-add-the-container"></a>若要添加容器  

1.  使用对 Active Directory 域服务中“系统”容器具有“创建所有子对象”权限的帐户。  

2.  运行“ADSI 编辑器”(adsiedit.msc)，并连接到站点服务器的域。  

3.  创建容器：  

    -   展开“域”&lt;计算机完全限定的域名\>，展开&lt;可分辨名称\>，右键单击“CN=System”，选择“新建”，然后选择“对象”。  

    -   在“创建对象”对话框中，选择“容器”，然后选择“下一步”。  

    -   在“值”框中，输入“系统管理”，然后选择“下一步”。  

4.  分配权限：  

    > [!NOTE]  
    >  如果有需要，可以使用 Active Directory 用户和计算机管理工具 (dsa.msc) 等其他工具向容器添加权限。  

    -   右键单击“CN=System Management”，然后选择“属性”。  

    -   选择“安全”选项卡，选择“添加”，然后添加具有“完全控制”权限的站点服务器计算机帐户。  

    -   选择“高级”，选择站点服务器的计算机帐户，然后选择“编辑”。  

    -   在“应用到”列表中，选择“这个对象及全部后代”。  

5.  选择“确定”关闭控制台并保存配置。  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>步骤 3。 设置站点以发布到 Active Directory 域服务  
 设置容器并授予权限，并且安装 Configuration Manager 主站点后，可以设置该站点以将数据发布到 Active Directory。  

 有关发布的详细信息，请参阅[发布 System Center Configuration Manager 的站点数据](../../../core/servers/deploy/configure/publish-site-data.md)。  
