---
title: "部署 Windows 客户端 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机。"
ms.custom: na
ms.date: 10/06/2016
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
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5a52386c6327ded3c5a400c7a046a6a12af96bae


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中部署客户端到 Windows 计算机

*适用范围：System Center Configuration Manager (Current Branch)*

你可以使用不同的客户端部署方法在计算机上安装 System Center Configuration Manager 客户端软件。 要帮助决定要使用的部署方法，请参阅[System Center Configuration Manager 中的客户端安装方法](../../../core/clients/deploy/plan/client-installation-methods.md)。  

 安装 Configuration Manager 客户端之前，请确保准备好所有必备组件，并且已经完成了所有必需的部署配置。 有关详细信息，请参阅[在 System Center Configuration Manager 中将客户端部署到 Windows 计算机的先决条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)。  


##  <a name="a-namebkmkclientpusha-how-to-install-configuration-manager-clients-by-using-client-push"></a><a name="BKMK_ClientPush"></a> 如何使用客户端请求安装 Configuration Manager 客户端  

 使用客户端请求安装在 Configuration Manager 发现的计算机上安装 Configuration Manager 客户端软件。 你可以为站点配置客户端请求安装，客户端安装将在站点的配置边界（如果这些边界被配置为边界组）内发现的计算机上自动运行。 或者，你可以运行特定集合或集合内的资源的“客户端请求安装向导”来启动客户端请求安装。  

 你也可以使用客户端请求安装向导来将 Configuration Manager 客户端安装到运行查询获取的结果。 为了在此情况下使安装成功，所选查询返回的其中一个项目必须为属性类“系统资源”  中的属性“资源 ID” 。 有关查询的详细信息，请参阅 [System Center Configuration Manager 的查询技术参考](../../../core/servers/manage/queries-technical-reference.md)。  

 如果站点服务器无法与客户端计算机联系或者无法启动安装过程，则它每小时都会尝试进行一次安装，一直尝试 7 天，直到安装成功为止。  

 为了帮助跟踪客户端安装过程，请在安装客户端之前安装回退状态点站点系统。 安装回退状态点后，在使用客户端请求安装方法安装客户端时，会自动将该回退状态点分配给客户端。 查看客户端部署和分配报表以跟踪客户端安装进度。 此外，客户端日志文件提供了用于疑难解答的更加详细的信息，并且不需要安装回退状态点。 例如，站点服务器上的 CCM.log 文件记录了站点服务器连接到计算机时出现的任何问题，客户端上的 CCMSetup.log 文件记录了安装过程。  

> [!IMPORTANT]  
>  为了继续执行客户端请求，请确保所有先决条件已经准备就绪。 这些条件列于[在 System Center Configuration Manager 中将客户端部署到 Windows 计算机的先决条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)中的“安装方法依赖关系”部分。  

#### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>将站点配置为对发现的计算机自动使用客户端请求  

1.  在 Configuration Manager 控制台中，单击“管理”   

2.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。  

3.  在“站点”  列表中，选择要为其配置自动站点范围客户端请求安装的站点。  

4.  在“主页”  选项卡上的“设置”  组中，单击“客户端安装设置” ，然后单击“客户端请求安装” 。  

5.  在“客户端请求安装属性”  对话框的“常规”  选项卡上，选择“启用自动站点范围客户端请求安装” 。 通过选择“服务器”、“工作站”或“Configuration Manager 站点系统服务器”来选择 Configuration Manager 应该将客户端软件请求到的系统类型。 默认选择是 **“服务器”** 或 **“工作站”**。  

6.  选择是否想让自动站点范围客户端请求安装在域控制器上安装 Configuration Manager 客户端软件。  

7.  在“帐户”选项卡上，指定 Configuration Manager 连接到要安装客户端软件的计算机时要使用的一个或多个帐户。 单击“创建”  图标，输入“用户名”  和“密码” ，确认密码，然后单击“确定” 。 必须指定至少一个客户端推送安装帐户，此帐户在你想要安装客户端的每台计算机上必须具有本地管理员权限。 如果未指定客户端推送安装帐户，则 Configuration Manager 会尝试使用站点系统计算机帐户，这将导致跨域客户端推送失败。  

    > [!IMPORTANT]  
    >  客户端请求安装帐户的密码限制为不超过 38 个字符。  

    > [!NOTE]  
    >  如果你打算使用辅助站点中的客户端请求安装方法，则必须在启动客户端请求的辅助站点中指定帐户。  
    >   
    >  有关客户端请求安装帐户的详细信息，请参阅下一个过程，即“使用客户端请求安装向导”。  

8.  在“安装属性”选项卡上，指定安装 Configuration Manager 客户端时要使用的任何安装属性。 你可以指定 Windows Installer 包 (Client.msi) 的安装属性，并且可以指定以下 CCMSetup.exe 属性：  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     如果已为 Configuration Manager 扩展架构，此选项卡中指定的客户端安装属性将发布到 Active Directory 域服务，并由不使用安装属性运行 CCMSetup 的客户端安装读取。 有关客户端安装属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

    > [!NOTE]  
    >  如果在辅助站点上启用客户端请求安装，请确保将 SMSSITECODE 属性设置为其父主站点的 Configuration Manager 站点名称。 如果已为 Configuration Manager 扩展了 Active Directory 架构，你也可以将此属性设置为“自动”以自动查找正确的站点分配。  

#### <a name="to-use-the-client-push-installation-wizard"></a>使用客户端请求安装向导  

1.  在 Configuration Manager 控制台中，单击“管理”   

2.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。  

3.  在“站点”  列表中，选择要为其配置自动站点范围客户端请求安装的站点。  

4.  在“主页”  选项卡上的“设置”  组中，单击“客户端安装设置” ，然后单击“客户端请求安装” 。  

5.  在“安装属性”选项卡上，指定安装 Configuration Manager 客户端时要使用的任何安装属性。 你可以指定 Windows Installer 包 (Client.msi) 的安装属性，并且可以指定以下 CCMSetup.exe 属性：  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     如果已为 Configuration Manager 扩展架构，此选项卡中指定的客户端安装属性将发布到 Active Directory 域服务，并由不使用安装属性运行 CCMSetup 的客户端安装读取。 有关客户端安装属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

6.  在 Configuration Manager 控制台中，单击“资产和符合性” 。  

7.  在“资产和符合性”  工作区中，选择一个或多个计算机，或选择计算机集合。  

8.  在“主页”  选项卡上，选择下列其中一项：  

    -   如果想要将客户端安装到一台或多台计算机上，请在“设备”  组中单击“安装客户端” 。  

    -   如果想要将客户端安装到计算机集合中，请在“集合”  组中单击“安装客户端” 。  

9. 在“安装客户端向导”  的“开始之前” 页上，查看信息，然后单击“下一步” 。  

10. 在“安装选项”  页上，配置是否可以在域控制器上安装客户端、是将在具有现有客户端的计算机上重新安装、升级还是修复客户端，以及将安装客户端软件的站点的名称。 单击“下一步” 。  

11. 查看安装设置，然后关闭向导。  

> [!NOTE]  
>  即使站点没有配置客户端请求，你也可以使用向导来安装客户端。  

##  <a name="a-namebkmkclientsupa-how-to-install-configuration-manager-clients-by-using-software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> 如何使用基于软件更新的安装来安装 Configuration Manager 客户端  
 基于软件更新的客户端安装将 Configuration Manager 客户端作为其他软件更新发布到软件更新点。 此客户端安装方法可用于在还没有安装 Configuration Manager 客户端的计算机上安装此客户端，或者升级现有 Configuration Manager 客户端。  

 如果计算机安装了 Configuration Manager 客户端，则 Configuration Manager 会向此客户端提供用于从中获取软件更新的软件更新点服务器名称和端口。 此信息包含在客户端策略中。  

> [!IMPORTANT]  
>  要使用基于软件更新的安装，你必须对客户端安装和软件更新使用相同的 Windows Server Update Services (WSUS) 服务器。 此服务器必须是主站点中的活动软件更新点。 有关详细信息，请参阅[安装软件更新点](../../../sum/get-started/install-a-software-update-point.md)。  

 如果计算机未安装 Configuration Manager 客户端，则必须在 Active Directory 域服务中配置和分配组策略对象 (GPO)，以指定计算机将从中获取软件更新的软件更新点服务器名称。  

 不能将命令行属性添加到基于软件更新的客户端安装中。 如果已为 Configuration Manager 扩展 Active Directory 架构，则客户端计算机在安装时会在 Active Directory 域服务中自动查询安装属性。  

 如果没有扩展 Active Directory 架构，则可以使用组策略向站点中的计算机提供客户端安装设置。 这些设置将自动应用于任何基于软件更新的客户端安装。 有关详细信息，请参阅[如何设置客户端安装属性（基于组策略和软件更新的客户端安装）](#BKMK_Provision)以及[如何在 System Center Configuration Manager 中将客户端分配到一个站点](../../../core/clients/deploy/assign-clients-to-a-site.md)。  

 使用以下过程将无 Configuration Manager 客户端的计算机配置为使用软件更新点进行客户端安装和软件更新，以及将 Configuration Manager 客户端软件发布到软件更新点。  

> [!NOTE]  
>  如果计算机在安装软件后处于等待重新启动状态，则基于软件更新的客户端安装可能会导致计算机重新启动。  

#### <a name="to-configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>将 Active Directory 域服务中的组策略对象配置为指定软件更新点以进行客户端安装和软件更新  

1.  使用组策略管理控制台打开新的或现有的组策略对象。  

2.  在控制台中依次展开“计算机配置” 、“管理模板” 和“Windows 组件” ，然后单击“Windows 更新” 。  

3.  打开“指定 Intranet Microsoft 更新服务位置” 设置的属性，然后单击“已启用” 。  

4.  在“设置检测更新的 Intranet 更新服务” 框中，指定想要使用的软件更新点服务器的名称以及端口。 这些内容必须与软件更新点正在使用的服务器名称格式和端口完全匹配：  

    -   如果将 Configuration Manager 站点系统配置为使用完全限定的域名 (FQDN)，请使用 FQDN 格式指定服务器名称。  

    -   如果未将 Configuration Manager 站点系统配置为使用完全限定的域名 (FQDN)，请使用短名称格式指定服务器名称。  

    > [!NOTE]  
    >  若要确定软件更新点正在使用的端口号，请参阅[如何确定 WSUS System Center Configuration Manager 中 WSUS 使用的端口设置](../../../sum/plan-design/plan-for-software-updates.md)。  

     示例： **http://server1.contoso.com:8530**  

5.  在“设置 Intranet 统计服务器” 框中，指定想要使用的 Intranet 统计服务器的名称。 没有关于指定该服务器的特定要求。 它不必与软件更新点服务器是同一台计算机，如果是同一台服务器，则格式不必匹配。  

6.  将组策略对象分配到想要在其中安装 Configuration Manager 客户端以及接收软件更新的计算机。  

#### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>将 Configuration Manager 客户端发布到软件更新点  

1.  在 Configuration Manager 控制台中，单击“管理”   

2.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。  

3.  在“站点”  列表中，选择要为其配置基于软件更新的客户端安装的站点。  

4.  在“主页”  选项卡上的“设置”  组中，单击“客户端安装设置” ，然后单击“基于软件更新的客户端安装” 。  

5.  在“软件更新点客户端安装属性”  对话框中，选择“启用基于软件更新的客户端安装”  以启用此客户端安装方法。  

6.  如果 Configuration Manager 站点服务器上的客户端软件版本高于存储在软件更新点上的客户端版本，则会打开“检测到客户端包的较高版本”对话框。 单击“是”  以将客户端软件的最新版本发布到软件更新点。  

    > [!NOTE]  
    >  如果以前尚未将此客户端软件发布到软件更新点，则此框将为空白。  

7.  要配置完软件更新点客户端安装，请单击“确定” 。  

> [!NOTE]  
>  当有新版本时不会自动更新 Configuration Manager 客户端的软件更新。 如果升级包括新客户端版本的站点，则必须重复此过程并在步骤 6 中单击“是”  。  

##  <a name="a-namebkmkclientgpa-how-to-install-configuration-manager-clients-by-using-group-policy"></a><a name="BKMK_ClientGP"></a> 如何使用组策略安装 Configuration Manager 客户端  
 你可以使用 Active Directory 域服务中的组策略发布或分配要在企业中的计算机上安装的 Configuration Manager 客户端。 使用组策略将 Configuration Manager 客户端分配到计算机时，会在首次启动计算机时安装客户端。 使用组策略发布 Configuration Manager 客户端时，客户端会显示在计算机控制面板的“添加或删除程序”中供用户安装。  

 使用 Windows Installer 包 (CCMSetup.msi) 进行基于组策略的安装。 此文件位于 Configuration Manager 站点服务器上的 **&lt;ConfigMgr installation directory\>\bin\i386**文件夹中。 你无法将属性添加到此文件中以修改安装行为：  

> [!IMPORTANT]  
>  你必须对此文件夹具有管理员权限才能访问客户端安装文件。  

-   如果为 Configuration Manager 扩展了 Active Directory 架构，并且在“站点属性”对话框的“高级”选项卡中选择了“在 Active Directory 域服务中发布此站点”，则客户端计算机会在 Active Directory 域服务中自动搜索安装属性。 有关发布的安装属性的详细信息，请参阅[关于 System Center Configuration Manager 中的发布到 Active Directory 域服务的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

-   如果未扩展 Active Directory 架构，则可以按照本主题中的以下过程将安装属性存储在计算机的注册表中： [如何设置客户端安装属性（基于组策略和软件更新的客户端安装）](#BKMK_Provision)。 然后在安装 Configuration Manager 客户端时使用这些安装属性。  

 关于如何使用 Active Directory 域服务中的组策略安装软件的信息，请参阅 Windows Server 文档。  

##  <a name="a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually"></a><a name="BKMK_Manual"></a> 如何手动安装 Configuration Manager 客户端  
 你可以使用 CCMSetup.exe 程序在企业计算机上手动安装 Configuration Manager 客户端软件。 可以在站点服务器上或站点中的管理点上 Configuration Manager 安装文件夹的 **Client** 文件夹中找到此程序及其支持文件。 该文件夹以  

 \\\\&lt;Site Server Name\>\SMS_&lt;Site Code\>\Client\  

 其中，&lt;Site Server Name\> 是托管管理点的其中一个服务器的名称，&lt;Site Code\> 是客户端所属的主站点的代码。  若要在客户端上从命令行运行 CCMSetup.exe，必须将网络驱动器映射到此位置，然后再运行命令。  

> [!IMPORTANT]  
>  你必须对此文件夹具有管理员权限才能访问客户端安装文件。  

 CCMSetup.exe 会将所有必需安装先决条件复制到客户端计算机，并调用 Windows Installer 包 (Client.msi) 以执行客户端安装。  

> [!IMPORTANT]  
>  你不能直接运行 Client.msi。  

 你可以指定 CCMSetup.exe 和 Client.msi 的命令行属性，以修改客户端安装的行为。 在指定 Client.msi 属性之前，请确保指定 CCMSetup 属性（以 **/** 开头的属性）。  

 例如，你可以指定下面的命令：  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  

 以及使用以下属性安装的客户端：  

|属性|描述|  
|--------------|-----------------|  
|**/mp:SMSMP01**|此 CCMSetup 属性指定管理点 SMSMP01 以下载所需的客户端安装文件。|  
|**/logon**|此 CCMSetup 属性指定在计算机上发现已有 Configuration Manager 客户端时应停止安装。|  
|**SMSSITECODE=AUTO**|此 Client.msi 属性指定客户端尝试查找要使用的 Configuration Manager 站点代码，例如通过使用 Active Directory 域服务来查找。|  
|**FSP=SMSFP01**|此 Client.msi 属性指定将使用名为 SMSFP01 的回退状态点接收从客户端计算机发送的状态消息。|  

 有关所有 CCMSetup.exe 属性的详细信息，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)  

### <a name="examples-for-installing-configuration-manager-clients-manually"></a>手动安装 Configuration Manager 客户端的示例  
 这些示例适用于 Intranet 上的 Active Directory 客户端，使用以下值来表示站点的其他方面：  

 **MPSERVER** = 托管管理点的服务器   
**FSPSERVER** = 托管回退状态点的服务器  
**ABC** = 站点代码  
**contoso.com** = 域名  

 所有站点系统服务器均配置有 Intranet FQDN，且此站点被发布到客户端的 Active Directory 林。  

 在客户端计算机上，你以本地管理员身份登录，将驱动器 (z:) 映射到 \\\MPSERVER\SMS_ABC\Client，将命令提示符切换到 z 盘，然后运行以下命令之一。  

 **示例 1：**  

```  
CCMSetup.exe  
```  

> [!NOTE]  
>  此示例安装客户端时未使用其他属性，以便使用发布到 Active Directory 域服务的客户端安装属性自动配置客户端。 例如，针对站点代码（要求将客户端的网络位置包括在为客户端分配配置的边界组中）、管理点、回退状态点以及客户端是否只能使用 HTTPS 进行通信，系统将自动配置客户端。 有关可以为 Active Directory 客户端自动配置的客户端安装属性的详细信息，请参阅[关于 System Center Configuration Manager 中的发布到 Active Directory 域服务的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

 **示例 2：**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  

> [!NOTE]  
>  此示例替代 Active Directory 域服务可以提供的自动配置，不要求将客户端的网络位置包括在为客户端分配配置的边界组中。 而安装会指定站点、Intranet 管理点和基于 Internet 的管理点、一个接受来自 Internet 的连接的回退状态点，并使用具有最长有效期的客户端 PKI 证书（如果可用）。  

##  <a name="a-namebkmkclientlogonscripta-how-to-install-configuration-manager-clients-by-using-logon-scripts"></a><a name="BKMK_ClientLogonScript"></a> 如何使用登录脚本安装 Configuration Manager 客户端  
 Configuration Manager 支持登录脚本来安装 Configuration Manager 客户端软件。 你可以在登录脚本中使用“CCMSetup.exe”  程序文件来触发客户端安装。  

 登录脚本安装使用的方法与手动客户端安装使用的方法相同。 你可以为 CCMSsetup.exe 指定“/logon”  安装属性，如果计算机上已经存在任何版本的客户端，则此属性会阻止安装客户端。 每次运行登录脚本时，此属性会阻止发生客户端重新安装。  

 如果未指定使用 **/Source** 属性的安装源，未使用 **/MP** 属性指定要从中获取安装的管理点，并且为 Configuration Manager 扩展了架构并将站点发布到 Active Directory 域服务，则 CCMSetup.exe 可以通过搜索 Active Directory 域服务来查找管理点。 或者，客户端可能会使用 DNS 或 WINS 来查找管理点。  

##  <a name="a-namebkmkclientappa-how-to-install-configuration-manager-clients-by-using-a-package-and-program"></a><a name="BKMK_ClientApp"></a> 如何通过使用包和程序来安装 Configuration Manager 客户端  
 你可以使用 Configuration Manager 来创建和部署包和程序，以为层次结构中所选择的计算机升级客户端软件。 随 Configuration Manager 一起提供了一个包定义文件，此文件使用常用值填充包属性。 你可以通过指定其他命令行属性来自定义客户端安装的行为。  

> [!NOTE]  
>  使用此方法无法升级 Configuration Manager 2007 客户端。 请改用自动客户端升级，它能自动创建并部署包含客户端最新版本的包。 有关详细信息，请参阅[在 System Center Configuration Manager 中升级客户端](../../../core/clients/manage/upgrade/upgrade-clients.md)。  
>   
>  有关如何从旧版 Configuration Manager 客户端迁移的详细信息，请参阅[在 System Center Configuration Manager 中规划客户端迁移策略](../../../core/migration/planning-a-client-migration-strategy.md)。  

 使用以下过程创建 Configuration Manager 包和程序，你可以将此包和程序部署到 Configuration Manager 客户端计算机以升级客户端软件。  

#### <a name="to-create-a-package-and-program-for-the-client-software"></a>创建客户端软件的包和程序  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“应用程序管理” ，然后单击“包” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“从定义创建包” 。  

4.  在“从定义创建包向导”  的“包定义” 页上，从“发布者”  下拉列表中选择“Microsoft”  ，从“包定义”  列表中选择“Configuration Manager 客户端升级”  ，然后单击“下一步” 。  

5.  在向导的“源文件”  页上，选择“始终从源文件夹获取文件” ，然后单击“下一步” 。  

6.  在“通过定义向导创建包”的“源文件夹”页上，选择“网络路径(UNC 名称)”并将网络路径输入到 Configuration Manager 客户端安装文件所在的计算机和文件夹。  

    > [!NOTE]  
    >  运行 Configuration Manager 部署的计算机必须能够访问你指定的网络文件夹。 如果计算机无访问权限，则安装将失败。  

7.  单击“下一步”  并完成向导。  

8.  如果想要更改任何客户端安装属性，则可以在“Configuration Manager 代理无提示升级属性”  程序对话框的“常规”  选项卡上修改 CCMSetup.exe 命令行参数。 默认安装属性为“/noservice SMSSITECODE=AUTO” 。  

9. 将包分发给你想要承载客户端升级包的所有分发点。 然后，你可以将此包部署到包含想要升级的 Configuration Manager 客户端的计算机集合。  

##  <a name="a-namebkmkclientimagea-how-to-install-configuration-manager-clients-by-using-computer-imaging"></a><a name="BKMK_ClientImage"></a> 如何使用计算机映像来安装 Configuration Manager 客户端  
 你可以在将用于构建企业计算机的主映像计算机上预安装 Configuration Manager 客户端软件。 要在主计算机上安装客户端，请不要指定客户端的站点代码。 从此主映像中对计算机进行映像时，这些计算机将包含 Configuration Manager 客户端，并且在安装完成时必须完成站点分配。  

> [!IMPORTANT]  
>  将 Configuration Manager 客户端分配到 Configuration Manager 站点之前，进行镜像的计算机不能充当 Configuration Manager 客户端。  

 你必须删除在主映像计算机上安装的任何特定于计算机的证书。 例如，你使用公钥基础结构 (PKI) 证书，则在映像计算机之前，必须在“计算机”  和“用户”  的“个人”  存储中删除证书。  

 如果客户端无法查询 Active Directory 域服务来查找管理点，则它们会使用受信任的根密钥来确定受信任的管理点。 如果所有映像的客户端将与主计算机部署在同一层次结构中，请保留受信任的根密钥。 如果客户端将部署在不同层次结构中，请删除受信任的根密钥，作为最佳方案，请用新的受信任的根密钥预先设置这些客户端。 有关详细信息，请参阅  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

#### <a name="to-prepare-the-client-computer-for-imaging"></a>准备要映像的客户端计算机  

1.  在主映像计算机上手动安装 Configuration Manager 客户端软件。 有关详细信息，请参阅 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual)。  

    > [!IMPORTANT]  
    >  请不要在 CCMSetup.exe 命令行属性中为客户端指定 Configuration Manager 站点代码。  

2.  在命令提示符下，键入 **net stop ccmexec** 以确保“SMS 代理主机”  服务 (Ccmexec.exe) 不在主映像计算机上运行。  

3.  删除存储在主映像计算机上的本地计算机存储中的任何证书。  

4.  如果客户端将与主映像计算机安装在不同的 Configuration Manager 层次结构中，请从主映像计算机中删除受信任的根密钥。  

5.  使用映像软件捕获主计算机的映像。  

6.  将映像部署到目标计算机。  

##  <a name="a-namebkmkclientworkgroupa-how-to-install-configuration-manager-clients-on-workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> 如何在工作组计算机上安装 Configuration Manager 客户端  
 Configuration Manager 支持为工作组中的计算机安装客户端。 通过使用 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual)中指定的方法在工作组计算机上安装客户端。  

 必须满足以下先决条件才能在工作组计算机上安装 Configuration Manager 客户端：  

-   必须在每台工作组计算机上手动安装客户端。 在安装过程中，已登录用户必须具有工作组计算机上的本地管理员权限。  

-   为了访问 Configuration Manager 站点服务器域中的资源，必须为该站点配置网络访问帐户。 你以软件分发组件属性的形式指定此帐户。 有关详细信息，请参阅 [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md)。  

 有许多针对支持工作组计算机的限制：  

-   工作组客户端无法从 Active Directory 域服务中查找管理点，而是必须使用 DNS、WINS 或其他管理点。  

-   不支持全局漫游，因为客户端无法查询 Active Directory 域服务来查找站点信息。  

-   Active Directory 发现方法无法发现工作组中的计算机。  

-   你无法向工作组计算机的用户部署软件。  

-   你无法使用客户端请求安装方法在工作组计算机上安装客户端。  

-   工作组客户端无法使用 Kerberos 进行身份验证，因此可能需要手动批准。  

-   不能将工作组客户端配置为分发点。 Configuration Manager 要求分发点计算机是某个域的成员。  

#### <a name="to-install-the-client-on-workgroup-computers"></a>在工作组计算机上安装客户端  

1.  确保你要在其上安装客户端的计算机满足上述先决条件。  

2.  按照 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual)部分中的说明操作。  

     示例 1： **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**  

    > [!NOTE]  
    >  此示例针对 Intranet 客户端管理安装客户端，并指定站点代码和 DNS 后缀以查找管理点。  

     示例 2： **CCMSetup.exe FSP=fspserver.constoso.com**  

    > [!NOTE]  
    >  此示例要求客户端位于在边界组中配置的网络位置上，以便自动站点分配可成功进行。 命令包括一个位于服务器 FSPSERVER 上的回退状态点，以帮助跟踪客户端部署并确定任何客户端通信问题。  

##  <a name="a-namebkmkclientinterneta-how-to-install-configuration-manager-clients-for-internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> 如何针对基于 Internet 的客户端管理安装 Configuration Manager 客户端  
 如果 Configuration Manager 站点支持对有时位于 Intranet 有时位于 Internet 上的客户端进行基于 Internet 的客户端管理，则在 Intranet 上安装客户端时，你有两个选择：  

-   你可以在安装客户端（例如，通过使用手动安装或客户端请求进行安装）时包括 Client.msi 属性 CCMHOSTNAME=&lt;基于 Internet 的管理点的 Internet FQDN\>。 在使用此方法时，你还必须将客户端直接分配到站点，并且无法使用自动站点分配。 本主题 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual) 部分中提供了此配置方法的示例。  

-   你可以针对 Intranet 客户端管理安装客户端，然后通过使用控制面板中的 Configuration Manager 客户端属性或通过使用脚本将基于 Internet 的客户端管理点分配到客户端。 在使用此方法时，你可以使用自动客户端分配。 有关详细信息，请参阅本主题中的 [如何在客户端安装后针对基于 Internet 的客户端管理配置客户端](#BKMK_ConfigureIBCM_MP) 部分。  

 如果你因为客户端是仅限 Internet 的客户端或者必须在客户端回到 Intranet 中之前安装客户端的原因而必须安装 Internet 上的客户端，请选择下列支持的方法之一：  

-   提供一个机制，使这些客户端使用虚拟专用网 (VPN) 临时连接到 Intranet，然后通过使用任何相应的客户端安装方法安装这些客户端。  

-   使用独立于 Configuration Manager 的安装方法，例如将客户端安装源文件打包到可移动媒体上，你可以将该媒体随说明一起发送给用户进行安装。 客户端安装源文件位于 Configuration Manager 站点服务器和管理点上的 &lt;安装路径\>\Client 文件夹中。 在媒体上包括一个脚本以手动复制客户端文件夹或从此文件夹中进行复制，使用 CCMSetup.exe 以及所有适合的 CCMSetup 命令行属性安装客户端。  

> [!NOTE]  
>  Configuration Manager 不支持直接通过基于 Internet 的管理点或基于 Internet 的软件更新点安装客户端。  

 由于通过 Internet 管理的客户端必须与基于 Internet 的站点系统通信，因此在安装这些客户端之前，请确保它们也安装了公钥基础结构 (PKI) 证书。 你必须独立于 Configuration Manager 安装这些证书。 有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

#### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>通过指定 CCMSetup 命令行属性在 Internet 上安装客户端  

1.  按照 [如何手动安装 Configuration Manager 客户端](#BKMK_Manual) 部分中的说明操作并始终包括以下内容：  

    -   CCMSetup 命令行属性 **/source:**&lt;复制的 Client 文件夹的本地路径\>  

    -   CCMSetup 命令行属性 **/UsePKICert**  

    -   Client.msi 属性 **CCMHOSTNAME=**&lt;基于 Internet 的管理点的 FQDN\>  

    -   Client.msi 属性 **SMSSIGNCERT=**&lt;导入的站点服务器签名证书的本地路径\>  

    -   Client.msi 属性 **SMSSITECODE=**&lt;基于 Internet 的管理点的本地路径\>  

    > [!NOTE]  
    >  如果站点有多个基于 Internet 的管理点，你为 CCMHOSTNAME 属性指定哪个基于 Internet 的管理点并不重要。 当 Configuration Manager 客户端连接到基于 Internet 的指定管理点时，管理点会向客户端发送一个站点中基于 Internet 的可用管理点的列表，客户端将从该列表中进行选择。 选择是不确定的。  

2.  如果不希望客户端检查证书吊销列表 (CRL)，请指定 CCMSetup 命令行属性 **/NoCRLCheck**。  

3.  如果你使用基于 Internet 的回退状态点，请指定 Client.msi 属性 **FSP=**&lt;Internet 回退状态点的 Internet FQDN\>。  

4.  如果要针对仅限 Internet 的客户端管理安装客户端，请指定 Client.msi 属性 **CCMALWAYSINF=1**。  

5.  验证是否必须指定任何其他 CCMSetup 命令行属性。 例如，在客户端有多个有效 PKI 证书的情况下，你可能必须指定证书选择条件。 有关可用属性的列表，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

     例如： **CCMSetup.exe /source:D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**  

    > [!NOTE]  
    >  此示例从 D 驱动器上的一个文件夹中安装客户端源文件（包含使用客户端 PKI 证书以及针对仅限 Internet 的客户端管理使用有效期最长的证书的设置），分配客户端以使用 contoso.com 域中基于 Internet 的管理点（名为 SERVER1）和基于 Internet 的回退状态点，并将客户端分配到 ABC 站点。  

###  <a name="a-namebkmkconfigureibcmmpa-how-to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> 如何在客户端安装后针对基于 Internet 的客户端管理配置客户端  
 要在安装客户端之后分配基于 Internet 的管理点，请使用下列过程之一。 第一个过程需要手动配置，因此它适合于少数客户端，而如果你有很多要配置的客户端，则第二个过程更为适合。  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>在客户端安装之后通过在 Configuration Manager 属性中分配基于 Internet 的管理点来针对基于 Internet 的客户端管理配置客户端  

1.  在客户端计算机上的控制面板中，导航到“Configuration Manager”  ，然后双击以打开其属性。  

2.  在“Internet”  选项卡上的“Internet FQDN”文本框中输入基于 Internet 的管理点的完全限定的域名。  

    > [!NOTE]  
    >  只有当客户端具有客户端 PKI 证书时，“Internet”  选项卡才可用。  

3.  如果客户端将通过使用代理服务器访问 Internet，请输入代理服务器设置。  

4.  单击" **确定**"。  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>在客户端安装后通过使用脚本来针对基于 Internet 的客户端管理配置客户端  

1.  打开文本编辑器，例如记事本。  

2.  将以下内容复制并粘贴到文件中：  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

3.  将 *mp.contoso.com* 替换为你的基于 Internet 的管理点的 Internet FQDN。  

    > [!NOTE]  
    >  如果必须删除基于 Internet 的指定管理点以便不将客户端配置为使用基于 Internet 的管理点，请删除引号内的值，使此行变为 **newInternetBasedManagementPointFQDN = ""**。  

4.  以 .vbs 扩展名保存文件。  

5.  通过以下方法之一使用 cscript 在客户端计算机上运行脚本：  

    -   通过使用包和程序将文件部署到现有 Configuration Manager 客户端。  

    -   通过在 Windows 资源管理器中双击脚本文件，以本地方式在现有 Configuration Manager 客户端上运行文件。  

 你可能必须重启客户端以使此脚本中的新设置生效。  

##  <a name="a-namebkmkprovisiona-how-to-provision-client-installation-properties-group-policy-and-software-update-based-client-installation"></a><a name="BKMK_Provision"></a> 如何设置客户端安装属性（基于组策略和软件更新的客户端安装）  
 你可以使用 Windows 组策略，通过 Configuration Manager 客户端安装属性来设置企业中的计算机。 这些属性存储在计算机的注册表中，在安装客户端软件时将读取这些属性。 Configuration Manager 通常不需要此过程。 但是，对于诸如以下一些客户端安装方案，此过程可能是必需的：  

-   你在使用基于组策略设置或软件更新的客户端安装方法，并且尚未为 Configuration Manager 扩展 Active Directory 架构。  

-   你希望覆盖特定计算机上的客户端安装属性。  

> [!NOTE]  
>  如果在 CCMSetup.exe 命令行上提供了任何安装属性，则不使用计算机上设置的安装属性。  

 Configuration Manager 安装媒体上提供了名为 ConfigMgrInstallation.adm 的组策略管理模板，可以使用该模板通过安装属性来设置客户端计算机。 使用以下过程来配置此模板并将其分配给组织中的计算机。  

#### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>使用组策略对象来配置和分配客户端安装属性  

1.  通过使用编辑器（例如 Windows 组策略对象编辑器）将管理模板 ConfigMgrInstallation.adm 导入到新的或现有的组策略对象中。  

    > [!NOTE]  
    >  此文件可在 Configuration Manager 安装媒体上的 **TOOLS\ConfigMgrADMTemplates** 文件夹中找到。  

2.  打开导入的设置“配置客户端部署设置” 的属性。  

3.  单击“已启用” 。  

4.  在“CCMSetup”  框中，输入必需的 CCMSetup 命令行属性。 有关所有 CCMSetup 命令行属性的列表及其用法示例，请参阅[关于 System Center Configuration Manager 中的客户端安装属性](../../../core/clients/deploy/about-client-installation-properties.md)。  

5.  将组策略对象分配给要通过 Configuration Manager 客户端安装属性设置的计算机。  

 有关 Windows 组策略的信息，请参阅 Windows Server 文档。  



<!--HONumber=Nov16_HO1-->


