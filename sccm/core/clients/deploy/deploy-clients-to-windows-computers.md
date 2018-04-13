---
title: 将客户端部署到 Windows
titleSuffix: Configuration Manager
description: 了解如何将 Configuration Manager 客户端部署到 Windows 计算机。
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3d7c3e9c9f2af8d612ef158897c281d422692268
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中部署客户端到 Windows 计算机

*适用范围：System Center Configuration Manager (Current Branch)*

安装 Configuration Manager 客户端之前，请确保准备好所有[先决条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)，并且已经完成了所有必需的部署配置。   



##  <a name="BKMK_ClientPush"></a> 如何使用客户端请求来安装客户端  

可以为站点配置客户端请求安装。 客户端安装将在站点的配置边界（如果这些边界被配置为边界组）内发现的计算机上自动运行。 或者，你可以运行特定集合或集合内的资源的“客户端请求安装向导”来启动客户端请求安装。  

你也可以使用客户端请求安装向导来将 Configuration Manager 客户端安装到[查询](../../../core/servers/manage/queries-technical-reference.md)结果。 为了使安装成功，查询返回的其中一个项目必须为“系统资源”类中的“资源 ID”属性。   

如果站点服务器无法与客户端计算机联系或者无法启动安装过程，则它每小时都会自动重试安装。 服务器不断重试长达七天。  

为了帮助跟踪客户端安装过程，请在安装客户端之前安装回退状态点。 安装回退状态点后，在使用客户端请求安装方法安装客户端时，会自动将该回退状态点分配给客户端。 若要跟踪客户端安装进度，请查看客户端部署和分配报表。 

客户端日志文件提供了用于疑难解答的更加详细的信息。 日志文件不需要回退状态点。 例如，连接到计算机时站点服务器上的 CCM.log 文件记录来自站点服务器的任何问题。 客户端上的 CCMSetup.log 文件记录安装过程。  

> [!IMPORTANT]  
>  为了继续执行客户端请求，请确保所有先决条件已经准备就绪。 有关详细信息，请参阅[安装方法依赖项](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies)。  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>将站点配置为对发现的计算机自动使用客户端请求

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”。  

3.  选择要为其配置自动站点范围客户端请求安装的站点。  

4.  在“主页”选项卡上的“设置”组中，选择“客户端安装设置” > “客户端请求安装”。  

5.  在“客户端请求安装属性”对话框的“常规”选项卡上，选择“启用自动站点范围客户端请求安装”。 选择 Configuration Manager 应向其推送客户端软件的系统类型。  

6.  选择是否要在域控制器上安装客户端。  

7.  在“帐户”选项卡上，指定当连接到目标计算机时 Configuration Manager 要使用的一个或多个帐户。 单击“创建”图标，输入“用户名”和“密码”（不超过 38 个字符），确认密码，然后单击“确定”。 指定至少一个客户端请求安装帐户。 此帐户在目标计算机上必须具有本地管理员权限以安装客户端。 如果未指定客户端请求安装帐户，则 Configuration Manager 会尝试使用站点系统计算机帐户。 使用站点系统计算机帐户时，跨域客户端请求失败。  
    > [!NOTE]  
    >  若要从辅助站点使用客户端请求，请指定用于启动客户端请求的辅助站点上的帐户。  
    >   
    >  有关客户端请求安装帐户的详细信息，请参阅下一个过程，即[使用客户端请求安装向导](#use-the-client-push-installation-wizard)。  

8.  完成“安装属性”选项卡。

     如果为 Configuration Manager 扩展了架构，站点将在此选项卡中指定的[客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)发布到 Active Directory 域服务。通过运行不带安装属性的 CCMSetup 来进行的客户端安装将读取这些属性。  

    > [!NOTE]  
    >  如果在辅助站点上启用客户端请求安装，请确保将 SMSSITECODE 属性设置为其父主站点的 Configuration Manager 站点名称。 如果已为 Configuration Manager 扩展了 Active Directory 架构，也可以将此属性设置为“自动”以自动查找正确的站点分配。  

### <a name="use-the-client-push-installation-wizard"></a>使用“客户端请求安装向导”

1.  在 Configuration Manager 控制台中，单击“管理” >  “站点配置” > “站点”。  

3.  选择要为其配置自动站点范围客户端请求安装的站点。  

4.  在“主页”选项卡 > “设置”组中，选择“客户端安装设置” > “客户端请求安装”。  

5.  完成“安装属性”选项卡。  

     如果为 Configuration Manager 扩展了架构，站点将在此选项卡中指定的[客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)发布到 Active Directory 域服务。通过运行不带安装属性的 CCMSetup 来进行的客户端安装将读取这些属性。   

6.  在 Configuration Manager 控制台中，选择“资产和符合性”。  

7.  在“资产和符合性”  工作区中，选择一个或多个计算机，或选择计算机集合。  

8.  在“开始”选项卡上，选择以下任一选项：  

    -   如果想要将客户端安装到一台或多台计算机上，请在“设备”组中选择“安装客户端”。  

    -   如果想要将客户端安装到计算机集合中，请在“集合”组中选择“安装客户端”。  

9. 在“安装客户端向导”的“开始之前”页上，查看信息，然后选择“下一步”。  

10. 完成“安装选项”页。  

11. 查看安装设置，然后关闭向导。  

> [!NOTE]  
>  即使站点没有配置客户端请求，也可以使用向导来安装客户端。  



##  <a name="BKMK_ClientSUP"></a> 如何使用基于软件更新点的安装来安装客户端  
 基于软件更新的客户端安装将客户端作为软件更新发布到软件更新点。 首次安装或升级时使用此方法。  

 如果计算机安装了 Configuration Manager 客户端，将从站点接收客户端策略。 此策略包括软件更新点服务器名称和获取软件更新的端口。   

> [!IMPORTANT]  
>  要使用基于软件更新的安装，你必须对客户端安装和软件更新使用相同的 Windows Server Update Services (WSUS) 服务器。 此服务器必须是主站点中的活动软件更新点。 有关详细信息，请参阅[安装软件更新点](../../../sum/get-started/install-a-software-update-point.md)。  

如果计算机未安装 Configuration Manager 客户端，请在 Active Directory 域服务中配置和分配组策略对象以指定软件更新点的服务器名称。  

不能将命令行属性添加到基于软件更新的客户端安装中。 如果已为 Configuration Manager 扩展 Active Directory 架构，则客户端计算机在安装时会在 Active Directory 域服务中自动查询安装属性。  

如果没有扩展 Active Directory 架构，则可以使用组策略向站点中的计算机提供客户端安装设置。 这些设置将自动应用于任何基于软件更新的客户端安装。 有关详细信息，请参阅[如何设置客户端安装属性（基于组策略和软件更新的客户端安装）](#BKMK_Provision)以及[如何将客户端分配到一个站点](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

使用以下过程将无 Configuration Manager 客户端的计算机配置为使用软件更新点进行客户端安装和软件更新，以及将客户端软件发布到软件更新点。  

> [!NOTE]  
>  如果计算机在安装软件后处于等待重新启动状态，则基于软件更新的客户端安装可能会导致计算机重新启动。  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>将 Active Directory 域服务中的组策略对象配置为指定软件更新点以进行客户端安装和软件更新：  

1.  使用组策略管理控制台打开新的或现有的组策略对象。  

2.  在控制台中依次展开“计算机配置”、“管理模板”和“Windows 组件”，然后选择“Windows 更新”。  

3.  打开“指定 Intranet Microsoft 更新服务位置”设置的属性，然后选择“已启用”。  

4.  在“设置检测更新的 Intranet 更新服务”框中，指定软件更新点服务器的名称以及端口：  

    -   如果 Configuration Manager 站点系统配置为使用完全限定的域名 (FQDN)，则使用 FQDN 格式。  

    -   如果 Configuration Manager 站点系统未配置为使用 FQDN，则使用短名称格式。  

    > [!NOTE]  
    >  若要确定端口号，请参阅[如何确定 WSUS 使用的端口设置](../../../sum/plan-design/plan-for-software-updates.md)。  

     例如：http://server1.contoso.com:8530  

5.  在“设置 Intranet 统计服务器”框中，指定 Intranet 统计服务器的名称。 它不必与软件更新点服务器相同。 如果它是相同的服务器，则格式不必匹配。  

6.  将组策略对象分配到想要在其中安装客户端以及接收软件更新的计算机。  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>将 Configuration Manager 客户端发布到软件更新点  

1.  在 Configuration Manager 控制台中，单击“管理” > “站点配置” > “站点”。  

3.  选择要为其配置基于软件更新的客户端安装的站点。  

4.  在“主页”选项卡上的“设置”组中，选择“客户端安装设置”，然后选择“基于软件更新的客户端安装”。  

5.  选择“启用基于软件更新的客户端安装”。  

6.  如果 Configuration Manager 站点服务器上的客户端软件版本高于软件更新点上的客户端软件版本，则会打开“检测到客户端包的较高版本”对话框。 单击“是”以发布最新的版本。  

    > [!NOTE]  
    >  如果以前未将此客户端软件发布到软件更新点，则此框为空白。  

当有新版本时不会自动更新 Configuration Manager 客户端的软件更新。 如果升级包括新客户端版本的站点，请重复此过程并在步骤 6 中单击“是”。  



##  <a name="BKMK_ClientGP"></a> 如何使用组策略安装客户端  
 可以使用 Active Directory 域服务中的组策略发布或分配要在企业中的计算机上安装的 Configuration Manager 客户端。 客户端在计算机启动时安装。 使用组策略时，客户端会显示在控制面板的“添加或删除程序”中供用户安装。  

 使用 Windows Installer 包 (CCMSetup.msi) 进行基于组策略的安装。 此文件位于 Configuration Manager 站点服务器上的 **&lt;ConfigMgr installation directory\>\bin\i386**文件夹中。 不能通过向此文件添加属性来修改安装行为。  

> [!IMPORTANT]  
>  必须具有管理员权限才能访问客户端安装文件。  

-   如果为 Configuration Manager 扩展了 Active Directory 架构，并且在“站点属性”对话框的“高级”选项卡中选择了“在 Active Directory 域服务中发布此站点”，则客户端计算机会在 Active Directory 域服务中自动搜索安装属性。 有关发布的安装属性的详细信息，请参阅[关于发布到 Active Directory 域服务的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

-   如果未扩展 Active Directory 架构，则可以按照本主题中的过程将安装属性存储在计算机的注册表中：[如何设置客户端安装属性（基于组策略和软件更新的客户端安装）](#BKMK_Provision)。 在安装客户端时使用这些安装属性。  

有关如何使用 Active Directory 域服务中的组策略安装软件的信息，请参阅 Windows Server 文档。  



##  <a name="BKMK_Manual"></a> 如何手动安装客户端  
 你可以使用 CCMSetup.exe 程序在企业计算机上手动安装客户端软件。 可以在站点服务器上或站点中的管理点上 Configuration Manager 安装文件夹的 **Client** 文件夹中找到此程序及其支持文件。 该文件夹以  

 \\\\&lt;Site Server Name\>\SMS_&lt;Site Code\>\Client\  

 其中，&lt;Site Server Name\> 是托管管理点的其中一个服务器的名称，&lt;Site Code\> 是客户端所分配的主站点代码。 若要在客户端上从命令行运行 CCMSetup.exe，必须将网络驱动器映射到此位置，然后再运行命令。  

> [!IMPORTANT]  
>  必须具有管理员权限才能访问客户端安装文件。  

 CCMSetup.exe 会将所有必需的先决条件复制到客户端计算机，并调用 Windows Installer 包 (Client.msi)，以安装客户端。 不能直接运行 Client.msi。  

 你可以指定 CCMSetup.exe 和 Client.msi 的命令行属性，以修改客户端安装的行为。 在指定 Client.msi 属性之前，请确保指定 CCMSetup 属性（以 **/** 开头的属性）。 例如：  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

以及使用以下属性安装的客户端：  

|属性|说明|  
|--------------|-----------------|  
|**/mp:SMSMP01**|此 CCMSetup 属性指定管理点 SMSMP01 以下载所需的客户端安装文件。|  
|**/logon**|此 CCMSetup 属性指定在计算机上发现已有 Configuration Manager 客户端时应停止安装。|  
|**SMSSITECODE=AUTO**|此 Client.msi 属性指定客户端尝试查找要使用的 Configuration Manager 站点代码，例如通过使用 Active Directory 域服务来查找。|  
|**FSP=SMSFP01**|此 Client.msi 属性指定使用名为 SMSFP01 的回退状态点接收从客户端计算机发送的状态消息。|  

 有关所有 CCMSetup.exe 属性的详细信息，请参阅[关于客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)  

> [!Tip]  
> 有关使用 Azure AD 标识在现代 Windows 10 设备上安装 Configuration Manager 客户端的过程，请参阅[安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。 该过程适用于 Intranet 或 Internet 上的客户端。  


### <a name="examples"></a>示例
 这些示例适用于 Intranet 上的 Active Directory 客户端。 它们使用以下值来表示站点的不同方面：  

 **MPSERVER** = 托管管理点的服务器   
**FSPSERVER** = 托管回退状态点的服务器  
**ABC** = 站点代码  
**contoso.com** = 域名  

 使用 Intranet FQDN 配置所有站点系统服务器。 站点发布到客户端的 Active Directory 林。  

 在客户端计算机上，以本地管理员身份登录，将驱动器 (z:) 映射到 \\\MPSERVER\SMS_ABC\Client，将命令提示符切换到 z 盘，然后运行以下命令之一：  

 **示例 1：**  

`CCMSetup.exe`  

此示例不使用其他属性安装客户端。 使用发布到 Active Directory 域服务的客户端安装属性自动配置客户端。 它为以下设置自动配置： 
- 站点代码。 此设置要求客户端的网络位置包括在为客户端分配配置的边界组中。 
- 管理点
- 回退状态点
- 仅使用 HTTPS 进行通信  
  
有关详细信息，请参阅[关于发布到 Active Directory 域服务的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

 **示例 2：**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
此示例替代 Active Directory 域服务提供的自动配置。 它不要求客户端的网络位置包括在为客户端分配配置的边界组中。 相反，安装会指定以下设置：
- 站点代码
- Intranet 管理点 
- 基于 Internet 的管理点
- 接受来自 Internet 的连接的回退状态点
- 使用具有最长有效期的客户端 PKI 证书（如果可用）  



##  <a name="BKMK_ClientLogonScript"></a> 如何使用登录脚本安装客户端  
 Configuration Manager 支持登录脚本来安装 Configuration Manager 客户端软件。 你可以在登录脚本中使用“CCMSetup.exe”  程序文件来触发客户端安装。  

 登录脚本安装使用的方法与手动客户端安装使用的方法相同。 可以为 CCMSsetup.exe 指定 /logon 安装属性。 如果计算机上已存在任何版本的客户端，则此属性将阻止客户端安装。 每次运行登录脚本时，此行为会阻止发生客户端重新安装。  

 如果未使用 /Source 属性指定安装源，未使用 /MP 属性指定可从中获取安装的管理点，则 CCMSetup.exe 通过搜索 Active Directory 域服务找到管理点。 只有为 Configuration Manager 扩展了架构并将站点发布到 Active Directory 域服务时，才会发生此行为。 或者，客户端可能会使用 DNS 或 WINS 来查找管理点。  



##  <a name="BKMK_ClientApp"></a> 如何使用包和程序安装客户端  
 你可以使用 Configuration Manager 来创建和部署包和程序，以为层次结构中所选择的计算机升级客户端软件。 随 Configuration Manager 一起提供了一个包定义文件，此文件使用常用值填充包属性。 可以通过指定其他命令行属性来自定义客户端安装的行为。  

> [!NOTE]  
>  无法使用此方法升级 Configuration Manager 2007 客户端。 请改用自动客户端升级，它能自动创建并部署包含客户端最新版本的包。 有关详细信息，请参阅[升级客户端](../../../core/clients/manage/upgrade/upgrade-clients.md)。  
>   
>  有关如何从旧版 Configuration Manager 客户端迁移的详细信息，请参阅[规划客户端迁移策略](../../../core/migration/planning-a-client-migration-strategy.md)。  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>创建客户端软件的包和程序  

使用以下过程创建 Configuration Manager 包和程序，你可以将此包和程序部署到 Configuration Manager 客户端计算机以升级客户端软件。  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “包”。  

3.  在“主页”选项卡的“创建”组中，选择“从定义创建包”。  

4.  在向导的“包定义”页上，从“发布者”下拉列表中选择“Microsoft”，然后从“包定义”列表中选择“Configuration Manager 客户端升级”。  

5.  在“源文件”页上，选择“始终从源文件夹获取文件”。  

6.  在“源文件夹”页上，选择“网络路径(UNC 名称)”。 然后将网络路径输入到客户端安装文件所在的计算机和文件夹。  

    > [!NOTE]  
    >  运行 Configuration Manager 部署的计算机必须能够访问指定的网络文件夹，否则安装失败。  

    若要更改任何客户端安装属性，请在“Configuration Manager 代理无提示升级属性”程序对话框的“常规”选项卡上修改 CCMSetup.exe 命令行参数。 默认安装属性为“/noservice SMSSITECODE=AUTO” 。  

9. 将包分发给你想要承载客户端升级包的所有分发点。 然后，可以将此包部署到包含想要升级的客户端的计算机集合。  



## <a name="bkmk_mdm"></a>如何将客户端安装到 Intune MDM 托管的 Windows 设备

可以将客户端安装文件部署到使用 Microsoft Intune 注册的计算机。 

此过程适用于连接到 Intranet 的传统客户端。 它使用传统的客户端身份验证方法。 若要确保客户端软件安装后，设备仍保持托管状态，设备必须在 Intranet 上，并且位于 Configuration Manager 站点边界内。  

有关使用 Azure AD 标识在现代 Windows 10 设备上安装 Configuration Manager 客户端的过程，请参阅[安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。

> [!NOTE]
> 客户端软件安装后，从 Intune 取消注册该设备。
> 
> 从版本 1710 开始，客户端不从 Intune 取消注册。 它们可以同时具有 Configuration Manager 客户端和 MDM 注册。 有关详细信息，请参阅[共同管理](/sccm/core/clients/manage/co-management-overview)。

###  <a name="install-clients-with-intune"></a>使用 Intune 安装客户端：

1. 在 Intune 中，[创建应用](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune)，该应用包含 Configuration Manager 客户端安装文件 **ccmsetup.msi**。 此文件位于 Configuration Manager 站点服务器上的 **&lt;ConfigMgr installation directory\>\bin\i386**文件夹中。

2. 在 Intune 软件发行者中，输入命令行参数。 例如，在 Intranet 上通过传统客户端使用以下命令行：

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > 有关使用现代 Windows 10 客户端（使用 Azure AD 进行身份验证）的示例命令行，请参阅[准备 Windows 10 设备进行共同管理](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)。

3. 向已注册的 Windows 计算机[部署应用](/intune/deploy-use/deploy-apps-in-microsoft-intune)。



##  <a name="BKMK_ClientImage"></a> 如何使用计算机映像安装客户端  
可以在用于创建 OS 映像的引用计算机上预装 Configuration Manager 客户端软件。   

> [!Important]
> 使用 Configuration Manager 任务序列部署 OS 映像时，[准备 ConfigMgr 客户端](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)任务序列步骤将 Configuration Manager 客户端完全删除。 

### <a name="prepare-the-client-computer-for-imaging"></a>准备要映像的客户端计算机  

1.  在引用计算机上手动安装 Configuration Manager 客户端软件。 有关详细信息，请参阅 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual)。  

    > [!IMPORTANT]  
    >  请不要在 CCMSetup.exe 命令行属性中为客户端指定 Configuration Manager 站点代码。  

2.  在命令提示符下，键入 `net stop ccmexec` 以确保引用计算机上未运行“SMS 代理主机”服务 (Ccmexec.exe)。
3.  从引用计算机上的“Windows”文件夹中删除文件“SMSCFG.INI”。  
3.  删除存储在引用计算机上的本地计算机存储中的任何证书。 例如，你使用公钥基础结构 (PKI) 证书，则在映像计算机之前，必须在“计算机”  和“用户”  的“个人”  存储中删除证书。

4.  如果客户端与引用计算机安装在不同的 Configuration Manager 层次结构中，请从引用计算机中删除受信任的根密钥。  
    > [!NOTE]  
    >  如果客户端无法查询 Active Directory 域服务来查找管理点，则它们会使用受信任的根密钥来确定受信任的管理点。 如果所有映像的客户端与主计算机部署在同一层次结构中，请保留受信任的根密钥。 如果客户端部署在不同层次结构中，请删除受信任的根密钥。 还为这些客户端设置新的受信任的根密钥。 有关详细信息，请参阅[规划受信任的根密钥](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。 

5.  使用映像软件捕获主计算机的映像。  

6.  将映像部署到目标计算机。  



##  <a name="BKMK_ClientWorkgroup"></a> 如何在工作组计算机上安装客户端  
 Configuration Manager 支持为工作组中的计算机安装客户端。 通过使用 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual)中指定的方法在工作组计算机上安装客户端。  

 先决条件：  

-   必须在每台工作组计算机上手动安装客户端。 在安装过程中，已登录用户必须具有本地管理员权限。  

-   为了访问 Configuration Manager 站点服务器域中的资源，必须为该站点配置网络访问帐户。 将此帐户指定为软件分发组件属性。 有关详细信息，请参阅 [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)。  

 限制：  

-   工作组客户端无法从 Active Directory 域服务中查找管理点，而是必须使用 DNS、WINS 或其他管理点。  

-   不支持全局漫游，因为客户端无法查询 Active Directory 域服务来查找站点信息。  

-   Active Directory 发现方法无法发现工作组中的计算机。  

-   你无法向工作组计算机的用户部署软件。  

-   你无法使用客户端请求安装方法在工作组计算机上安装客户端。  

-   工作组客户端无法使用 Kerberos 进行身份验证，可能需要手动批准。  

-   不能将工作组客户端配置为分发点。 Configuration Manager 要求分发点计算机是某个域的成员。  

### <a name="install-the-client-on-workgroup-computers"></a>在工作组计算机上安装客户端  

查看先决条件，然后按照[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分中的说明操作。  

   此示例针对 Intranet 客户端管理安装客户端，并指定站点代码和 DNS 后缀以查找管理点。 `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   此示例要求客户端位于在边界组中配置的网络位置上。 此要求是为了让自动站点分配成功。 该命令包含位于服务器 FSPSERVER 上的回退状态点。 此属性有助于跟踪客户端部署，并识别任何客户端通信问题。 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a>如何针对基于 Internet 的客户端管理安装客户端  
 
> [!Note]
> 本部分不适用于使用[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)的客户端。 若要使用云管理网关安装基于 Internet 的客户端，请参阅[安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](/sccm/core/clients/deploy/deploy-clients-cmg-azure)。

如果 Configuration Manager 站点支持对有时位于 Intranet 有时位于 Internet 上的客户端进行[基于 Internet 的客户端管理](/sccm/core/clients/manage/plan-internet-based-client-management)，则在 Intranet 上安装客户端时有两个选择：  

-   可以在安装客户端（例如，通过使用手动安装或客户端请求进行安装）时包括 Client.msi 属性 CCMHOSTNAME=&lt;基于 Internet 的管理点的 Internet FQDN\>。 在使用此方法时，你还必须将客户端直接分配到站点，并且无法使用自动站点分配。 本主题[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分中提供了此配置方法的示例。  

-   可以针对 Intranet 客户端管理安装客户端，然后将基于 Internet 的客户端管理点分配到客户端。 通过使用 Configuration Manager 客户端属性或通过使用脚本更改管理点。 在使用此方法时，你可以使用自动客户端分配。 有关详细信息，请参阅本主题中的[如何在客户端安装后针对基于 Internet 的客户端管理配置客户端](#BKMK_ConfigureIBCM_MP)部分。  

 如果必须安装 internet 上的客户端，选择下列支持方法之一：  

-   为这些客户端提供机制以使用 VPN 临时连接到 Intranet。 然后使用任何合适的客户端安装方法安装客户端。  

-   使用与 Configuration Manager 无关的安装方法。 例如将客户端安装源文件打包到可移动媒体上，可以将该媒体随说明一起发送给用户进行安装。 客户端安装源文件位于 Configuration Manager 站点服务器和管理点上的 &lt;安装路径\>\Client 文件夹中。 在媒体上包括一个脚本以手动复制客户端文件夹或从此文件夹中进行复制，使用 CCMSetup.exe 以及所有适合的 CCMSetup 命令行属性安装客户端。  

> [!NOTE]  
>  Configuration Manager 不支持直接通过基于 Internet 的管理点或基于 Internet 的软件更新点安装客户端。  

 通过 Internet 管理的客户端必须与基于 Internet 的站点系统进行通信。 在安装客户端之前，确保这些客户端还具有公钥基础结构 (PKI) 证书。 独立于 Configuration Manager 安装这些证书。 有关证书要求的详细信息，请参阅 [PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>通过指定 CCMSetup 命令行属性在 Internet 上安装客户端  

1.  按照[如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分中的说明操作并始终包括以下内容：  

    -   CCMSetup 命令行属性 /source:&lt;复制的 Client 文件夹的本地路径\>  

    -   CCMSetup 命令行属性 **/UsePKICert**  

    -   Client.msi 属性 CCMHOSTNAME=&lt;基于 Internet 的管理点的 FQDN\>  

    -   Client.msi 属性 SMSSIGNCERT=&lt;导入的站点服务器签名证书的本地路径\>  

    -   Client.msi 属性 SMSSITECODE=&lt;基于 Internet 的管理点的本地路径\>  

    > [!NOTE]  
    >  如果站点有多个基于 Internet 的管理点，则为 CCMHOSTNAME 属性指定哪个基于 Internet 的管理点并不重要。 当 Configuration Manager 客户端连接到基于 Internet 的指定管理点时，管理点会向客户端发送一个站点中基于 Internet 的可用管理点的列表。 客户端从该列表中随机选择一个。  

2.  如果不希望客户端检查证书吊销列表 (CRL)，请指定 CCMSetup 命令行属性 **/NoCRLCheck**。  

3.  如果使用基于 Internet 的回退状态点，请指定 Client.msi 属性 FSP=&lt;基于 Internet 的回退状态点的 Internet FQDN\>。  

4.  如果要针对仅限 Internet 的客户端管理安装客户端，请指定 Client.msi 属性 CCMALWAYSINF=1。  

5.  验证是否必须指定其他 CCMSetup 命令行属性。 例如，在客户端有多个有效 PKI 证书的情况下，你可能必须指定证书选择条件。 有关可用属性的列表，请参阅[关于客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

   例如：  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   此示例使用以下行为安装客户端：
   - 使用 D 驱动器上文件夹中的源文件
   - 使用客户端 PKI 证书 
   - 选择有效期最长的证书 
   - 仅限 Internet 的客户端管理
   - 分配客户端以使用名为 SERVER1 的基于 Internet 的管理点
   - 分配 contoso.com 域中基于 Internet 的回退状态点
   - 将客户端分配到 ABC 站点  

###  <a name="BKMK_ConfigureIBCM_MP"></a> 在客户端安装后针对基于 Internet 的客户端管理配置客户端  
 若要在安装客户端之后分配基于 Internet 的管理点，请使用这些过程之一。 第一个过程需手动进行配置，并且仅适用于某些客户端。 第二个过程更适用于配置大部分客户端。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>在客户端安装之后通过在 Configuration Manager 属性中分配基于 Internet 的管理点来针对基于 Internet 的客户端管理配置客户端  

1.  在客户端计算机上的控制面板中，导航到“Configuration Manager”  ，然后双击以打开其属性。  

2.  在“Internet”选项卡上的“Internet FQDN”文本框中输入基于 Internet 的管理点的完全限定的域名。  

    > [!NOTE]  
    >  只有当客户端具有客户端 PKI 证书时，“Internet”  选项卡才可用。  

3.  如果客户端通过使用代理服务器访问 Internet，请输入代理服务器设置。  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>在客户端安装后通过使用脚本来针对基于 Internet 的客户端管理配置客户端  

1.  打开文本编辑器，例如记事本。  

2.  将以下 VBScript 示例复制并粘贴到文件中。 将 mp.contoso.com 替换为基于 Internet 的管理点的 Internet FQDN。  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  如果必须删除基于 Internet 的指定管理点以便不将客户端配置为使用基于 Internet 的管理点，请删除引号内的值，使此行变为：`newInternetBasedManagementPointFQDN = ""`  

4.  以 .vbs 扩展名保存文件。  

5.  通过以下方法之一使用 cscript.exe 在客户端计算机上运行脚本：  

    -   通过使用包和程序将文件部署到现有 Configuration Manager 客户端。  

    -   通过在 Windows 资源管理器中双击脚本文件，以本地方式在现有 Configuration Manager 客户端上运行文件。  

 可能必须重启客户端以使更改生效。  



##  <a name="BKMK_Provision"></a> 如何设置客户端安装属性（基于组策略和软件更新的客户端安装）  
 可以使用 Windows 组策略，通过 Configuration Manager 客户端安装属性来设置计算机。 这些属性存储在计算机的注册表中，安装客户端软件时将读取这些属性。 通常不需要此过程，但在某些客户端安装方案中可能需要，例如：  

-   正在使用组策略设置或基于软件更新的客户端安装方法。 没有为 Configuration Manager 扩展 Active Directory 架构。  

-   你希望覆盖特定计算机上的客户端安装属性。  

> [!NOTE]  
>  如果在 CCMSetup.exe 命令行上提供了任何安装属性，则不使用计算机上设置的安装属性。  

 Configuration Manager 安装介质上提供了名为 ConfigMgrInstallation.adm 的组策略管理模板。 可以使用该模板通过安装属性来设置客户端计算机。   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>使用组策略对象来配置和分配客户端安装属性  

1.  通过使用编辑器（例如 Windows 组策略对象编辑器）将管理模板 ConfigMgrInstallation.adm 导入到新的或现有的组策略对象中。 此文件可在 Configuration Manager 安装媒体上的 **TOOLS\ConfigMgrADMTemplates** 文件夹中找到。  

2.  打开导入的设置“配置客户端部署设置” 的属性。  

3.  选择“启用”。  

4.  在“CCMSetup”  框中，输入必需的 CCMSetup 命令行属性。 有关所有 CCMSetup 命令行属性的列表及其用法示例，请参阅[关于客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

5.  将组策略对象分配给要通过 Configuration Manager 客户端安装属性设置的计算机。  

有关 Windows 组策略的信息，请参阅 Windows Server 文档。  



## <a name="next-steps"></a>后续步骤
如需安装 Configuration Manager 客户端方面的更多帮助，请参阅[客户端安装方法](../../../core/clients/deploy/plan/client-installation-methods.md)。