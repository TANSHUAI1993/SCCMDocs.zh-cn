---
title: "设置 System Center Configuration Manager 实验室 | Microsoft Docs"
description: "设置实验室以便使用模拟现实活动评估 Configuration Manager。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
caps.latest.revision: "11"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 11f5d0c3c61d675a8182e985f82e6af363b34592
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-your-system-center-configuration-manager-lab"></a>设置你的 System Center Configuration Manager 实验室

*适用范围：System Center Configuration Manager (Current Branch)*

遵循本主题中的指导原则将使你能够设置实验室以使用模拟现实活动评估 Configuration Manager。  

##  <a name="BKMK_LabCore"></a> 核心组件  
 为 System Center Configuration Manager 中设置环境需要一些核心组件支持安装 Configuration Manager。    

-   **该实验室环境使用 Windows Server 2012 R2**，我们将在其中安装 System Center Configuration Manager。  

     可以从 [TechNet 评估中心](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012)下载 Windows Server 2012 R2 的评估版。  

     请考虑修改或禁用 Internet Explorer 增强的安全配置以便更轻松地访问在整个练习过程中引用的某些下载文件。 请查看 [Internet Explorer：增强的安全配置](https://technet.microsoft.com/en-us/library/dd883248\(v=ws.10\).aspx) 以获取其他信息。  

-   **实验室环境中将 SQL Server 2012 SP2** 用于站点数据库。  

     可以从 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=29066)下载 SQL Server 2012 的评估版。  

     SQL Server 具有[支持的 SQL Server 版本](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)，必须满足这些版本才能用于 System Center Configuration Manager。  

    -   Configuration Manager 需要 64 位版本的 SQL Server 以托管站点数据库。  

    -   **SQL_Latin1_General_CP1_CI_AS** 作为“SQL 排序规则”  类。  

    -   **Windows 身份验证**， [而不是 SQL 身份验证](https://technet.microsoft.com/en-us/library/ms144284.aspx)， is required.  

    -   需要专用的 **SQL Server 实例**。  

    -   不限制用于 SQL Server 的**系统可寻址内存**。  

    -   将 **SQL Server 服务帐户**配置为使用**域本地用户**帐户运行。  

    -   必须安装 **SQL Server reporting services**。  

    -   **站点间通信** 对默认端口 TCP 4022 使用 SQL Server Service Broker。  

    -   SQL Server 数据库引擎与所选 Configuration Manager 站点系统角色之间的**站点内通信**使用默认端口 TCP 1433。  

-   **域控制器使用 Windows Server 2008 R2**（安装了 Active Directory 域服务）。 域控制器还充当 DHCP 的主机和 DNS 服务器以便用于完全限定的域名。  

     有关其他信息，请查看此 [Active Directory 域服务概述](https://technet.microsoft.com/en-us/library/hh831484)。  

-   **Hyper-V 与几个虚拟机一起使用**，以验证在这些练习中执行的管理步骤是否按预期正常工作。 建议最少三个虚拟机，并已安装 Windows 7（或更高版本）。  

     有关其他信息，请查看此 [Hyper-V 概述](https://technet.microsoft.com/en-us/library/hh831531.aspx)。  

-   **管理员权限** 。  

    -   Configuration Manager 需要管理员在 Windows Server 环境中具有本地权限  

    -   Active Directory 需要具有架构修改权限的管理员  

    -   虚拟机需要计算机本身的本地权限  

虽然此实验室不需要，不过可以查看 [System Center Configuration Manager 支持的配置](../../core/plan-design/configs/supported-configurations.md)以了解有关实现 System Center Configuration Manager 的要求的其他信息。 请参阅此处所引用软件版本之外的版本的文档。  

安装所有这些组件后，还必须执行其他步骤以为 Configuration Manager 配置 Windows 环境：  

###  <a name="BKMK_LabADPrep"></a> 为实验室准备 Active Directory 内容  
 你将为此实验室创建一个安全组，然后向其添加一个域用户。  

-   安全组： **Evaluation**  

    -   组作用域： **Universal**  

    -   组类型： **Security**  

-   域用户： **ConfigUser**  

     正常情况下，你不会将向环境内的所有用户授予通用访问权限。 你与此用户一起进行此操作的目的是为了简化你的实验室联机。  

使 Configuration Manager 客户端能够查询 Active Directory 域服务以找到站点资源所需的后续步骤列于后续程序上。  

###  <a name="BKMK_CreateSysMgmtLab"></a> 创建系统管理容器  
 扩展架构时，Configuration Manager 不会在 Active Directory 域服务中自动创建所需的系统管理容器。 因此，你会为你的实验室创建此系统管理容器。 此步骤将要求你 [安装 ADSI 编辑器。](https://technet.microsoft.com/en-us/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit)  

 确保你以对 Active Directory 域服务中的“系统”  容器具有“创建所有子对象”  权限的帐户身份登录。  

##### <a name="to-create-the-system-management-container"></a>若要创建系统管理容器：  

1.  运行“ADSI 编辑器” ，并连接到站点服务器所在的域。  

2.  展开“域&lt;计算机完全限定的域名\>”，展开“<可分辨名称\>”，右键单击“CN=System”，再单击“新建”，然后单击“对象”。  

3.  在  “创建对象”对话框中，选择“容器” ，然后单击“下一步” 。  

4.  在“值”  框中，键入 **System Management**，然后单击“下一步” 。  

5.  单击“完成”  以完成该过程。  

###  <a name="BKMK_SetSecPermLab"></a> 为系统管理容器设置安全权限  
 授予站点服务器计算机帐户将站点信息发布到容器所需的权限。 你也会针对此任务使用 ADSI 编辑器。  

> [!IMPORTANT]  
>  确认你在开始下列过程之前已连接到站点服务器的域。  

##### <a name="to-set-security-permissions-for-the-system-management-container"></a>若要为系统管理容器设置安全权限：  

1.  在控制台窗格中，依次展开“站点服务器的域”、“DC=&lt;服务器可分辨名称\>”，然后展开“CN=System”。 右键单击“CN=System Management” ，然后单击“属性” 。  

2.  在“CN=System Management 属性”  对话框中，单击“安全”  选项卡，然后单击“添加”  以添加该站点服务器计算机帐户。 为该帐户授予“完全控制”  权限。  

3.  单击“高级”，选择站点服务器的计算机帐户，然后单击“编辑”。  

4.  在“应用到”  列表中，选择“这个对象及全部后代” 。  

5.  单击“确定”  关闭“ADSI 编辑器”  控制台并完成该过程。  

     有关此过程的其他见解，请查看[扩展 System Center Configuration Manager 的 Active Directory 架构](../../core/plan-design/network/extend-the-active-directory-schema.md)  

###  <a name="BKMK_ExtADSchLab"></a> 使用 extadsch.exe 来扩展 Active Directory 架构  
 你将扩展此实验室中的 Active Directory 架构，因为这会使你能够以最小的管理开销使用所有 Configuration Manager 功能。 扩展 Active Directory 架构是林范围的配置，每个林执行一次该配置。 扩展架构永久修改基本 Active Directory 配置中的类和属性的集。 此操作不可逆。 扩展架构允许 Configuration Manager 访问组件，这可以使其可在实验室环境中最有效地工作。  

> [!IMPORTANT]  
>  确保你使用作为“架构管理员”  安全组成员的帐户登录到架构主机域控制器。 尝试使用备用凭据都将失败。  

##### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>若要使用 extadsch.exe 来扩展 Active Directory 架构：  

1.  创建架构主机域控制器的系统状态的备份。 有关备份主机域控制器的详细信息，请查看 [Windows Server Backup](https://technet.microsoft.com/en-us/library/cc770757.aspx)  

2.  导航至安装介质中的 **\SMSSETUP\BIN\X64** 。  

3.  运行 **extadsch.exe**。  

4.  通过查看位于系统驱动器根目录中的 **extadsch.log** ，验证架构扩展是否成功。  

     有关此过程的其他见解，请查看[扩展 System Center Configuration Manager 的 Active Directory 架构](../../core/plan-design/network/extend-the-active-directory-schema.md)。  

###  <a name="BKMK_OtherTasksLab"></a> 其他必需的任务  
 你在安装前还需要完成以下任务。  

 **创建文件夹存储所有下载内容**  

 在本次练习期间，安装媒介的组件将需要多个下载文件。 开始任何安装过程前，请先确定一个在你取消配置实验室之前不会要求你移动这些文件的位置。 建议使用一个具有很多子文件夹的文件夹来存储这些下载文件。  

 **安装 .NET 并且 激活 Windows Communication Foundation**  

 你需要安装这两种.NET 框架：首先安装 .NET 3.5.1，然后安装 .NET 4.5.2+。 你还需要激活 Windows Communication Foundation (WCF)。 WCF 通过面向服务的编程模型专为实现分布式计算、广泛的互操作性和直接支持服务方向提供可管理的方法，并简化了连接应用程序开发。 请查看 [什么是 Windows Communication Foundation？](https://technet.microsoft.com/en-us/subscriptions/ms731082\(v=vs.90\).aspx) ，了解关于 WCF 的其他见解。  

##### <a name="to-install-net-and-activate-windows-communication-foundation"></a>若要安装 .NET 并且激活 Windows Communication Foundation：  

1.  打开 **Server Manager**，然后导航到“管理” 。 单击“添加角色和功能”  以打开“添加角色和功能向导”  **Wizard.**。  

2.  查看“开始前”  面板提供的信息，然后单击“下一步” 。  

3.  选择“基于角色或基于功能的安装” ，然后单击“下一步” 。  

4.  从“服务器池” 选择你的服务器，然后单击“下一步” 。  

5.  查看“服务器角色”  面板，然后单击“下一步” 。  

6.  通过从列表中选择，添加以下“功能”  ：  

    -   **.NET Framework 3.5 功能**  

        -   **.NET framework 3.5（包括 .NET 2.0 和 3.0）**  

    -   **.NET Framework 4.5 功能**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **WCF 服务**  

            -   **HTTP 激活**  

            -   **TCP 端口共享**  

7.  查看“Web 服务器角色 (IIS)”  以及“角色服务”  屏幕，然后单击“下一步” 。  

8.  查看“确认”  屏幕，然后单击“下一步” 。  

9. 单击“安装”  并在“服务器管理器”  的“通知” 窗格验证安装是否正确完成。  

10. .NET 的基本安装完成后，导航到 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/details.aspx?id=42643) 以获取 .NET Framework 4.5.2 的 Web 安装程序。 单击“下载”  按钮，然后单击“运行”以运行  安装程序。 它将自动检测并安装你选择的语言版本的所需组件。  

有关其他信息，请查看以下文章以了解为什么需要这些 .NET 框架：  

-   [.NET Framework 版本和依赖关系](https://technet.microsoft.com/en-us/library/bb822049.aspx)  

-   [.NET Framework 4 RTM 应用程序兼容性演练](https://technet.microsoft.com/en-us/library/dd889541.aspx)  

-   [如何：将 ASP.NET Web 应用程序更新到 ASP.NET 4](https://technet.microsoft.com/en-us/library/dd483478\(VS.100\).aspx)  

-   [Microsoft .NET Framework 支持生命周期策略常见问题](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [CLR 全面透彻解析 - 进程内并行](https://msdn.microsoft.com/en-us/magazine/ee819091.aspx)  

**启用 BITS、IIS 和 RDC**  

[后台智能传输服务 (BITS)](https://technet.microsoft.com/en-us/library/dn282296.aspx) 用于需要在客户端和服务器之间异步传输文件的应用程序。 通过计数前台和后台传输的流，BITS 保留了其他网络应用程序的响应能力。 如果传输会话中断，则它还会自动恢复文件传输。  

因为此站点服务器也将用作管理点，所以你需要为此实验室安装 BITS。  

Internet 信息服务 (IIS) 是可用来承载 Web 上找到的任何内容的灵活、可扩展的 Web 服务器。 由 Configuration Manager 将其用于大量站点系统角色。 有关 IIS 的其他信息，请查看 [System Center Configuration Manager 中的站点系统服务器网站](../../core/plan-design/network/websites-for-site-system-servers.md)。  

[远程差分压缩 (RDC)](https://technet.microsoft.com/en-us/library/cc754372.aspx) 是应用程序可用于确定是否已对一组文件进行过任何更改的 API 集。 RDC 使应用程序能够仅复制文件已更改的部分，将网络流量保持在最低限度。  

##### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>若要启用 BITS、IIS 和 RDC 站点服务器角色：  

1.  在你的站点服务器上，打开 **Server Manager**。 导航到“管理” 。 单击“添加角色和功能”  以打开“添加角色和功能向导” 。  

2.  查看“开始前”  面板提供的信息，然后单击“下一步” 。  

3.  选择“基于角色或基于功能的安装” ，然后单击“下一步” 。  

4.  从“服务器池” 选择你的服务器，然后单击“下一步” 。  

5.  通过从列表中选择，添加以下“服务器角色”  ：  

    -   **Web 服务器 (IIS)**  

        -   **常见 HTTP 功能**  

            -   **默认文档**  

            -   **目录浏览**  

            -   **HTTP 错误**  

            -   **静态内容**  

            -   **HTTP 重定向**  

        -   **运行状况和诊断**  

            -   **HTTP 日志记录**  

            -   **日志记录工具**  

            -   **请求监视器**  

            -   **跟踪**  

    -   **性能**  

        -   **静态内容压缩**  

        -   **动态内容压缩**  

    -   **Security**  

        -   **请求筛选**  

        -   **基本身份验证**  

        -   **客户端证书映射身份验证**  

        -   **IP 和域限制**  

        -   **URL 授权**  

        -   **Windows 授权**  

    -   **应用程序开发**  

        -   **.NET Extensibility 3.5**  

        -   **.NET Extensibility 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **ISAPI 扩展**  

        -   **ISAPI 筛选器**  

        -   **服务器端包括**  

    -   **FTP 服务器**  

        -   **FTP 服务**  

    -   **管理工具**  

        -   **IIS 管理控制台**  

        -   **IIS 6 管理兼容性**  

            -   **IIS 6 元数据库兼容性**  

            -   **IIS 6 管理控制台**  

            -   **IIS 6 脚本工具**  

            -   **IIS 6 WMI 兼容性**  

        -   **IIS 6 管理脚本和工具**  

        -   **管理服务**  

6.  通过从列表中选择，添加以下“功能”  ：  

    -   -   **后台智能传输服务 (BITS)**  

            -   **IIS 服务器扩展**  

        -   **远程服务器管理工具**  

            -   **功能管理工具**  

                -   **BITS 服务器扩展工具**  

7.  单击“安装”  并在“服务器管理器”  的“通知” 窗格验证安装是否正确完成。  

默认情况下，IIS 阻止多种文件拓展名和位置通过 HTTP 或 HTTPS 通信进行访问。 若要使这些文件分发到客户端系统，你需要为分发点上的 IIS 配置请求筛选。 有关详细信息，请参阅[分发点的 IIS 请求筛选](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering)。  

##### <a name="to-configure-iis-filtering-on-distribution-points"></a>若要在分发点上配置 IIS 筛选：  

1.  打开 **IIS Manager** 并在侧栏中选择你的服务器名。 这将使你转到“主页”  屏幕。  

2.  验证已选择“主页”  屏幕底部的“功能视图”  。 导航到 **IIS** 并打开“请求筛选” 。  

3.  在“操作”  窗格中，单击“允许文件拓展名...”   

4.  键入 **.msi** 到对话框中，然后单击“确定” 。  

###  <a name="BKMK_InstallCMLab"></a> 安装配置管理器  
你将创建[确定何时使用主站点](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary)以直接管理客户端。 这将允许你的实验室环境支持可能设备的[站点系统扩展](/sccm/core/plan-design/configs/size-and-scale-numbers)管理。  
在此过程中，你也可以安装 Configuration Manager 控制台，它将用于管理你今后的评估设备。  

在开始安装之前，使用 Windows Server 2012 启动服务器上的[必备组件检查程序](/sccm/core/servers/deploy/install/prerequisite-checker)以确认已正确启用所有设置。  

##### <a name="to-download-and-install-configuration-manager"></a>若要下载和安装 Configuration Manager：  

1.  导航到[系统中心评估](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection)页以下载 System Center Configuration Manager 的最新评估版本。  

2.  将下载媒体解压缩到预定义位置。  

3.  请按照[使用 System Center Configuration Manager 安装向导安装站点](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)中列出的安装过程操作。 在该过程中，你将输入以下各项：  

    |站点安装过程的步骤|选择|  
    |-----------------------------------------|---------------|  
    |步骤 4：“产品密钥”  页|选择“评估” 。|  
    |步骤 7：“必备下载”  |选择“下载所需文件”  并指定预定义的位置。|  
    |步骤 10：“站点和安装设置” |-   **站点代码：LAB**<br />-   **站点名称：Evaluation**<br />-    指定预定义的位置。|  
    |步骤 11：“主站点安装” |选择“将主站点安装为独立站点” ，然后单击“下一步” 。|  
    |步骤 12：“数据库安装” |-    在此处输入你的 FQDN。<br />-    将其留空，因为你将使用以前安装的 SQL 的默认实例。<br />-    保留为默认端口 4022。|  
    |步骤 13：“数据库安装” |将这些设置保留为默认值。|  
    |步骤 14：“SMS 提供程序”|将这些设置保留为默认值。|  
    |步骤 15：“客户端通信设置” |确认未选择“所有站点系统角色仅接受来自客户端的 HTTPS 通信” |  
    |步骤 16：“站点系统角色” |输入你的 FQDN，并确认仍未选择“所有站点系统角色仅接受来自客户端的 HTTPS 通信”  。|  

###  <a name="BKMK_EnablePubLab"></a>为 Configuration Manager 站点启用发布  
每个 Configuration Manager 站点将其自己的特定于站点的信息发布到 Active Directory 架构中其域分区内的系统管理容器中。 必须打开 Active Directory 和 Configuration Manager 之间的双向通道以处理此流量。 此外，还将启用林发现以确定 Active Directory 和网络基础结构的某些组件。  

##### <a name="to-configure-active-directory-forests-for-publishing"></a>针对发布配置 Active Directory 林：  

1.  在 Configuration Manager 控制台的左下角，单击“管理”。  

2.  在“管理”  工作区中，展开“层次结构配置” ，然后单击“发现方法” 。  

3.  选择“Active Directory 林发现”  ，然后单击“属性” 。  

4.  在“属性”  对话框中，选择“启用 Active Directory 林发现” 。 此功能激活后，选择“当发现 Active Directory 站点边界时自动进行创建” 。 将出现一个对话框，显示“你想尽快运行完整的发现吗？”  单击“完成” 。  

5.  在屏幕顶部的“发现方法”  组中，单击“立即运行林发现” ，然后导航至侧栏中的“Active Directory 林”  。 Active Directory 林应显示在发现的林列表中。  

6.  导航到该屏幕顶部的“常规”  选项卡。  

7.  在“管理”  工作区中，展开“层次结构配置” ，然后单击“Active Directory 林” 。  

##### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>使 Configuration Manager 站点能够将站点信息发布到 Active Directory 林：  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  你将配置尚未发现的新林。  

3.  在“管理”  工作区中，单击“Active Directory 林” 。  

4.  在该站点属性的“发布”  选项卡上，选择你连接的林，然后单击“确定”  保存配置。
