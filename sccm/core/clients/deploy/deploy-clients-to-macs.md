---
title: "部署 Mac 客户端 | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中将客户端部署到 Mac 计算机。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: eae9e76085a95cb09fe01a32fd4b57294bc1cc20


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

在 System Center Configuration Manager 中为 Mac 计算机安装和管理客户端需要公钥基础结构 (PKI) 证书。 Configuration Manager 可通过将 Microsoft 证书服务与企业证书颁发机构 (CA)、Configuration Manager 注册点和注册代理点站点系统角色一起使用，从而请求和安装用户客户端证书。 或者，如果证书满足 Configuration Manager 的要求，你可以独立于 Configuration Manager 请求和安装计算机证书。 PKI 证书通过使用手动身份验证和加密的数据传输来保护 Mac 计算机和 Configuration Manager 站点之间的通信的安全。  

> [!IMPORTANT]  
>  Configuration Manager Mac 客户端始终执行证书吊销检查；与 Windows 上运行的 Configuration Manager 客户端不同，你无法禁用此证书吊销列表 (CRL) 检查功能。  
>   
>  如果 Mac 客户端由于无法找到 CRL 而无法确认服务器证书的证书吊销状态，它们将无法成功连接到 Configuration Manager 站点系统，例如管理点和分发点。 特别是，对于所在的林与证书颁发机构不同的 Mac 客户端，请检查你的 CRL 设计以确保 Mac 客户端可找到并连接到 CRL 分发点 (CDP) 以便连接站点系统服务器。  

 在 Mac 计算机上安装 Configuration Manager 客户端之前，请决定安装客户端证书的方式：  

-   通过 CMEnroll 工具使用 Configuration Manager 注册，并按照本主题的下一部分中的步骤进行操作。 注册过程不支持自动证书续订，因此你必须在安装的证书过期之前重新注册 Mac 计算机。  

-   使用与 Configuration Manager 无关的证书请求和安装方法。 有关安装方法，请参见此主题中的 [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation) 部分。  

> [!NOTE]  
>  有关 Mac 客户端证书要求和支持 Mac 计算机所需的其他 PKI 证书的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

 会自动将 Mac 客户端分配给对其进行管理的 Configuration Manager 站点。 即使仅与 Intranet 通信，Mac 客户端也将安装为仅 Internet 的客户端。 这种客户端配置意味着，当你将为客户端分配的站点中的站点系统角色（管理点和分发点）配置为允许来自 Internet 的客户端连接时，它们只会与这些站点系统角色通信。 Mac 计算机不会与为其分配的站点范围外的站点系统角色通信。  

> [!IMPORTANT]  
>  Configuration Manager Mac 客户端不能用于连接至配置为使用数据库副本的管理点。 有关数据库副本的信息，请参阅 [System Center Configuration Manager 管理点的数据库副本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)。  

 使用下列部分来为 Configuration Manager 安装、配置和管理 Mac 计算机：  

-   [为 Mac 安装和配置客户端的步骤](#InstallSteps)  

-   [Uninstalling the Mac client](#uninstallMacClient)  

-   [Renewing the Mac client certificate](#BKMK_Renew)  

-   [Use a certificate request and installation method that is independent from Configuration Manager](#BKMK_ManualCertifcateInstallation)  

##  <a name="a-nameinstallstepsa-steps-to-install-and-configure-the-client-for-macs"></a><a name="InstallSteps"></a> 为 Mac 安装和配置客户端的步骤  

> [!IMPORTANT]  
>  在执行这些步骤之前，请确保 Mac 计算机满足先决条件。 有关详细信息，请参阅 [Mac 支持的操作系统](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)。  

### <a name="step-1-deploy-a-web-server-certificate-to-site-system-servers"></a>步骤 1：将 Web 服务器证书部署到站点系统服务器  
 这些站点系统对于其他 Configuration Manager 客户端可能已经有此证书。 如果没有，请将 Web 服务器证书部署到容纳下列站点系统角色的计算机：  

-   管理点  

-   分发点  

-   注册点  

-   注册代理点  

> [!IMPORTANT]  
>  Web 服务器证书必须包含在站点系统属性中指定的 Internet FQDN。  
>   
>  这并不意味着服务器必须可从 Internet 中访问才能支持 Mac 计算机。 如果不需要基于 Internet 的客户端管理，你可以为 Internet FQDN 指定 Intranet FQDN 值。  

 有关创建和安装此 Web 服务器证书的部署示例，请参阅[为运行 IIS 的站点系统部署 Web 服务器证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  

> [!IMPORTANT]  
>  确保在管理点、分发点和注册代理点的 Web 服务器证书中指定站点系统的 Internet FQDN 值。  

### <a name="step-2-deploy-a-client-authentication-certificate-to-site-system-servers"></a>步骤 2：将客户端身份验证证书部署到站点系统服务器  
 这些站点系统对于 Configuration Manager 功能可能已经有此证书。 如果没有，请将客户端身份验证证书部署到容纳下列站点系统角色的计算机：  

-   管理点  

-   分发点  

 有关创建和安装管理点的客户端证书的示例部署，请参阅[为 Windows 计算机部署客户端证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)  

 有关创建和安装分发点的客户端证书的示例部署，请参阅[为分发点部署客户端证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)。  

### <a name="step-3-prepare-the-client-certificate-template-for-macs"></a>步骤 3：为 Mac 准备客户端证书模板  

> [!NOTE]  
>  要运行 Configuration Manager 注册工具，你必须有 Active Directory 用户帐户。  

 对于将在 Mac 计算机上注册证书的用户帐户，证书模板必须具有“读取”  和“注册”  权限。  

 请参阅[部署 Mac 计算机的客户端证书](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)。  

### <a name="step-4-configure-the-management-point-and-distribution-point"></a>步骤 4：配置管理点和分发点  
 为下列选项配置管理点：  

-   HTTPS  

-   允许来自 Internet 的客户端连接  

    > [!NOTE]  
    >  管理 Mac 计算机需要该配置值。 但是，它并不意味着站点系统服务器必须可从 Internet 中访问。  

-   允许移动设备和 Mac 计算机使用此管理点  

 尽管在 Mac 计算机上安装客户端无需分发点，但是，如果要在安装 Configuration Manager 客户端之后将软件部署到这些 Mac 计算机，你必须配置分发点以允许来自 Internet 的客户端连接。  

 此过程配置现有管理点和分发点以支持 Mac 计算机。 在开始此过程之前，请确保运行管理点和分发点的站点系统服务器配置为包含 Internet FQDN。 如果这些站点系统服务器将不支持基于 Internet 的客户端管理，你可以指定 Intranet FQDN 作为 Internet FQDN 值。 此外，这些站点系统角色必须位于主站点中。  

##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>配置管理点和分发点以支持 Mac  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，选择“服务器和站点系统角色” ，然后选择容纳要配置的站点系统角色的服务器。  

3.  在详细信息窗格中，右键单击“管理点” ，单击“角色属性” ，并在“管理点属性”  对话框中配置下列选项，然后单击“确定” ：  

    1.  选择“HTTPS” 。  

    2.  选择“仅允许 Internet 客户端连接”  或“允许 Intranet 和 Internet 客户端连接” 。 这些选项要求在站点系统属性中指定 Internet FQDN（即使站点系统服务器将不可从 Internet 中访问）。  

    3.  选择“允许移动设备和 Mac 计算机使用此管理点” 。  

4.  在详细信息窗格中，右键单击“分发点” ，单击“角色属性” ，并在“分发点属性”  对话框中配置下列选项，然后单击“确定” ：  

    -   选择“HTTPS” 。  

    -   选择“仅允许 Internet 客户端连接”  或“允许 Intranet 和 Internet 客户端连接” 。 这些选项要求在站点系统属性中指定 Internet FQDN（即使站点系统服务器将不可从 Internet 中访问）。  

    -   单击“导入证书” ，浏览到导出的客户端分发点证书文件，然后指定密码。  

5.  为将用于 Mac 计算机的主站点中的所有管理点和分发点重复此过程中的步骤 2 至 4。  

### <a name="step-5-configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>步骤 5：配置注册代理点和注册点  
 你必须在同一站点中安装这两个站点系统角色，但不必将它们安装在同一站点系统服务器上或同一 Active Directory 林中。  

 有关站点系统角色布局和注意事项的详细信息，请参阅[为 System Center Configuration Manager 规划站点系统服务器和站点系统角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)中的[站点系统角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)。  

 这些过程配置站点系统角色以支持 Mac 计算机。 根据你是将安装新站点系统服务器来支持 Mac 计算机还是使用现有站点系统服务器，选择这些过程之一：  

-   [安装和配置注册站点系统：新的站点系统服务器](#BKMK_HowtoInstallEnrollmentSiteSystems_new)  

-   [安装和配置注册站点系统：现有站点系统服务器](#BKMK_HowtoInstallEnrollmentSiteSystems_existing)  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsnewa-to-install-and-configure-the-enrollment-site-systems-new-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_new"></a> 安装和配置注册站点系统：新的站点系统服务器  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，并单击“服务器和站点系统角色”   

3.  在“主页”  选项卡上的“创建”  组中，单击“创建站点系统服务器” 。  

4.  在“常规”  页上，指定站点系统的常规设置，然后单击“下一步” 。  

    > [!IMPORTANT]  
    >  即使站点系统服务器将不可从 Internet 中访问，也要确保为 Internet FQDN 指定值。 如果由于站点系统服务器将不可从 Internet 中访问而没有 Internet FQDN，你可以指定 Intranet FQDN 值作为 Internet FQDN。 Mac 计算机始终连接到 Internet FQDN，即便当它们位于 Intranet 上时也是如此。  

5.  在“系统角色选择”  页上，从可用角色列表中选择“注册代理点”  和“注册点”  ，然后单击“下一步” 。  

6.  在“注册代理点”  页上，查看设置并进行任何所需更改，然后单击“下一步” 。  

7.  在“注册点设置”  页上，查看设置并进行任何所需更改，然后单击“下一步” 。  

8.  完成向导。  

####  <a name="a-namebkmkhowtoinstallenrollmentsitesystemsexistinga-to-install-and-configure-the-enrollment-site-systems-existing-site-system-server"></a><a name="BKMK_HowtoInstallEnrollmentSiteSystems_existing"></a> 安装和配置注册站点系统：现有站点系统服务器  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，展开“站点配置” ，选择“服务器和站点系统角色” ，然后选择要用于支持 Mac 计算机的服务器。  

3.  在“主页”  选项卡上的“创建”  组中，单击“添加站点系统角色” 。  

4.  在“常规”  页上，指定站点系统的常规设置，然后单击“下一步” 。  

    > [!IMPORTANT]  
    >  即使站点系统服务器将不可从 Internet 中访问，也要确保为 Internet FQDN 指定值。 如果由于站点系统服务器将不可从 Internet 中访问而没有 Internet FQDN，你可以指定 Intranet FQDN 值作为 Internet FQDN。 Mac 计算机始终连接到 Internet FQDN，即便当它们位于 Intranet 上时也是如此。  

5.  在“系统角色选择”  页上，从可用角色列表中选择“注册代理点”  和“注册点”  ，然后单击“下一步” 。  

6.  在“注册代理点”  页上，查看设置并进行任何所需更改，然后单击“下一步” 。  

7.  在“注册点设置”  页上，查看设置并进行任何所需更改，然后单击“下一步” 。  

8.  完成向导。  

### <a name="step-6-optional-install-the-reporting-services-point"></a>步骤 6：可选：安装 Reporting Services 点  
 如果要为 Mac 计算机运行报表，请安装 Reporting Services 点。  

 有关如何安装和配置 Reporting Services 点的详细信息，请参阅[在 Configuration Manager 中配置报表](../../../core/servers/manage/configuring-reporting.md)。  

### <a name="step-7-configure-client-settings-for-enrollment"></a>步骤 7：为注册配置客户端设置  
 你必须使用默认客户端设置来为 Mac 计算机配置注册；你无法使用自定义客户端设置。  

 有关客户端设置的详细信息，请参阅 [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md)。  

 Configuration Manager 需要此步骤以便在 Mac 计算机上请求和安装证书。  

##### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>为 Configuration Manager 配置默认客户端设置以便为 Mac 注册证书  

1.  在 Configuration Manager 控制台中，单击“管理” 。  

2.  在“管理”  工作区中，单击“客户端设置” 。  

3.  单击“默认客户端设置” 。  

    > [!IMPORTANT]  
    >  你无法为注册配置使用自定义客户端设置；你必须使用默认客户端设置。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  选择“注册”  部分，然后配置下列用户设置：  

    1.  **允许用户注册移动设备和 Mac 计算机：是**  

    2.  “注册配置文件：” 单击“设置配置文件” 。  

6.  在“移动设备注册配置文件”  对话框中，单击“创建” 。  

7.  在“创建注册配置文件”  对话框中，输入此注册配置文件的名称，然后配置“管理站点代码” 。 选择包含将管理 Mac 计算机的管理点的 Configuration Manager 主站点。  

    > [!NOTE]  
    >  如果无法选择站点，则检查是否将站点中的至少一个管理点配置为支持移动设备。  

8.  单击“添加” 。  

9. 在“添加移动设备证书颁发机构”  对话框中，选择将向 Mac 计算机颁发证书的证书颁发机构 (CA) 服务器，然后单击“确定” 。  

10. 在“创建注册配置文件”  对话框中，选择在步骤 3 中创建的 Mac 计算机证书模板，然后单击“确定” 。  

11. 单击“确定”  关闭“注册配置文件”  对话框，然后单击“确定”  关闭“默认客户端设置”  对话框。  

    > [!TIP]  
    >  如果想要更改客户端策略间隔，请使用“客户端策略”  客户端设置组中的“客户端策略轮询间隔”  客户端设置。  

 当所有用户下一次下载客户端策略时，将使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅[为 Configuration Manager 客户端启动策略检索](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)。  

 除了注册客户端设置之外，请确保配置了以下 Configuration Manager 客户端设备设置：  

-   “硬件清单”：如果想要从 Mac 和 Windows 客户端计算机中收集硬件清单，请启用和配置此客户端设置。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中扩展硬件清单](../../../core/clients/manage/inventory/extend-hardware-inventory.md)。  

-   “符合性设置”：如果想要评估和修正 Mac 和 Windows 客户端计算机上的设置，请启用和配置此客户端设置。 有关详细信息，请参阅[规划和配置符合性设置](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)。  

> [!NOTE]  
>  有关 Configuration Manager 客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../core/clients/deploy/configure-client-settings.md)。  

### <a name="step-8-download-the-client-source-files-for-macs"></a>步骤 8：为 Mac 下载客户端源文件  
 在 Mac 上安装和管理 Configuration Manager 客户端之前，必须下载和安装以下程序：  

-   **Ccmsetup**：使用此应用程序在组织中的 Mac 计算机上安装 Configuration Manager 客户端。  

-   **CMDiagnostics**：使用此工具在组织中的 Mac 计算机上收集与 Configuration Manager 客户端相关的诊断信息。  

-   **CMUninstall**：使用此工具从组织中的 Mac 计算机中卸载 Configuration Manager 客户端。  

-   **CMAppUtil**：使用此工具将 Apple 应用程序包转换为可部署为 Configuration Manager 应用程序的格式。  

-   **CMEnroll**：使用此工具请求和安装 Mac 计算机的客户端证书，以便以后可以安装 Configuration Manager 客户端。  

> [!IMPORTANT]  
>  当你为 Mac 计算机安装新客户端时，你可能还需要安装 Configuration Manager 更新以反映 Configuration Manager 控制台中的新客户端信息。  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>下载并安装 Mac OS X 客户端文件  

1.  下载 Mac OS X 客户端文件包“ConfigmgrMacClient.msi” 并将其保存在运行 Windows 的计算机上。  

     Configuration Manager 安装媒体上不提供此文件。 可以从 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/?LinkID=525184)下载此文件。  

2.  在 Windows 计算机上运行刚下载的 **ConfigmgrMacClient.msi** 文件，以将 Mac 客户端包 Macclient.dmg 提取到本地磁盘上的文件夹（默认位置为 **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**）。  

3.  将 Macclient.dmg 文件复制到 Mac 计算机上的文件夹中。  

4.  在 Mac 计算机上，运行刚才下载的 Macclient.dmg 文件以将文件提取到本地磁盘上的文件夹中。  

5.  在此文件夹中，请确保提取 Ccmsetup 和 CMClient.pkg 文件，并且创建一个包含 CMDiagnostics、CMUninstall、CMAppUtil 和 CMEnroll 工具的名称为“工具”的文件夹。  

### <a name="step-9-install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>步骤 9：在 Mac 上安装客户端，然后注册客户端证书  
 此过程安装客户端，然后使用 CMEnroll 工具为 Mac 计算机请求和安装客户端证书，以便你以后可以使用 Configuration Manager 管理此计算机。  

 你可以使用“Mac 计算机注册向导”来注册客户端，而不必使用 CMEnroll 工具。 有关详细信息，请参阅下面的过程。  

##### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>安装客户端并使用 CMEnroll 工具注册证书  

1.  在 Mac 计算机上，导航到文件夹，你在该文件夹中已经提取了从 Microsoft 下载中心下载的 Macclient.dmg 文件的内容。  

2.  输入以下命令行： **sudo ./ccmsetup**  

3.  请一直等到看到“已完成安装”  消息。 虽然安装程序显示一条表明现在必须重启的消息，但现在请不要重启，而是继续进行下一步。  

4.  从 Mac 计算机上的工具文件夹中，键入以下内容：**sudo ./CMEnroll -s &lt;注册代理服务器名称> -ignorecertchainvalidation -u &lt;用户名'>**  

    > [!NOTE]  
    >  客户端安装后，Mac 计算机注册向导将在客户端安装后打开，以帮助你注册 Mac 计算机。 要用此方法注册客户端，请参见此主题中的 [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) 。  

     随后将提示你键入 Active Directory 用户帐户的密码。  

    > [!IMPORTANT]  
    >  输入此命令时，实际上会提示你输入两个密码：第一个提示用于运行命令的超级用户帐户。 第二个提示用于 Active Directory 用户帐户。 提示看起来相同，因此请确保按正确的顺序指定它们。  

     用户名可以是以下格式：  

    -   “域\名称”。 例如：“contoso\mnorth”  

    -   'user@domain'. 例如： 'mnorth@contoso.com'  

     用户名和对应的密码必须与被授予 Mac 客户端证书模板的“读取”和“注册”权限的 Active Directory 用户帐户匹配。  

     示例：如果注册代理点服务器名为 **server02.contoso.com**，并且向 **contoso\mnorth** 用户名授予了对 Mac 客户端证书模板的权限，请键入以下内容： **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!IMPORTANT]  
    >  如果用户名包含以下任一字符：**&lt;>"+=,**，则注册将失败。  
    >   
    >  若要解决此问题，获取带有不包含这些字符的用户名的带外证书。  

    > [!NOTE]  
    >  为了获得更加完美的用户体验，你可以对安装步骤和命令编写脚本，以便用户只须提供其用户名和密码。  

5.  请一直等到看到“已成功注册”  消息。  

6.  若要将注册的证书限制在 Configuration Manager 范围内，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    1.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  在“密钥链访问”  对话框中的“密钥链”  部分中，单击“系统” ，然后在“类别”  部分中，单击“密钥” 。  

    3.  展开密钥以查看客户端证书。 标识了具有刚才安装的私钥的证书后，双击密钥。  

    4.  在“访问控制”  选项卡上，选择“在允许访问前确认” 。  

    5.  浏览到“/Library/Application Support/Microsoft/CCM” ，选择“CCMClient” ，然后单击“添加” 。  

    6.  单击“保存更改”  并关闭“密钥链访问”  对话框。  

7.  重新启动 Mac 计算机。  

 在 Mac 计算机上的“系统首选项”  中打开“Configuration Manager”  项以验证客户端安装是否成功。 也可以更新和查看“所有系统”  集合，以确认现在 Mac 计算机在此集合中显示为托管客户端。  

> [!TIP]  
>  为了帮助排查 Mac 客户端的任何问题，你可以使用 Mac OS X 客户端包附带的 CMDiagnostics 程序收集以下诊断信息：  
>   
>  -   运行的进程的列表  
> -   Mac OS X 操作系统版本  
> -   与 Configuration Manager 客户端相关的 Mac OS X 故障报告包括 **CCM\*.crash** 和 **System Preference.crash**。  
> -   Configuration Manager 客户端安装创建的物料清单 (BOM) 文件和属性列表 (.plist) 文件。  
> -   /Library/Application Support/Microsoft/CCM/Logs 文件夹的内容。  
>   
>  CmDiagnostics 收集的信息会添加到一个 zip 文件中，该文件将保存到计算机的桌面上并且名为 cmdiag-<主机名\>**-**<日期和时间\>.zip。  

####  <a name="a-namebkmkenrollr2a-to-enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a><a name="BKMK_EnrollR2"></a> 使用“Mac 计算机注册向导”注册客户端  

1.  安装完客户端后，“计算机注册向导”将打开。 单击“下一步”  继续通过欢迎页。  

    > [!NOTE]  
    >  如果向导未打开或者你无意中关闭了向导，请单击“Configuration Manager”  首选项页中的“注册”  以打开向导。  

2.  在向导的下一页上，指定下列信息：  

    -   **用户名** - 用户名可以是以下格式：  

        -   “域\名称”。 例如：“contoso\mnorth”  

        -   'user@domain'. 例如： 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  使用电子邮件地址填充“用户名”字段时，Configuration Manager 将自动使用该电子邮件地址的域名和注册代理点服务器的默认名称填充“服务器名称”字段。 如果此域名和服务器名称与注册代理点服务器的名称不匹配，你必须告知用户要使用的正确名称，使他们能够在注册其 Mac 计算机时输入此项。  

         用户名和对应的密码必须与被授予 Mac 客户端证书模板的“读取”和“注册”权限的 Active Directory 用户帐户匹配。  

    -   **密码** - 为指定的用户名输入对应的密码。  

    -   **服务器名称** - 输入注册代理点服务器的名称。  

3.  单击“下一步”  继续，然后完成向导。  

##  <a name="a-nameuninstallmacclienta-uninstalling-the-mac-client"></a><a name="uninstallMacClient"></a> 卸载 Mac 客户端  
 如果要卸载 Mac 客户端，请使用与你从 Web 中下载的 Mac 客户端文件一起提供的 CMUninstall 脚本。 使用以下过程帮助你从 Mac 计算机中卸载 Configuration Manager 客户端。  

#### <a name="to-uninstall-the-mac-client"></a>要卸载 Mac 客户端  

1.  在 Mac 计算机上，打开终端窗口并导航到文件夹，你在该文件夹中已经提取了从 Microsoft 下载中心下载的 macclient.dmg 文件的内容。  

2.  导航到“工具”文件夹并输入以下命令行：  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  **-c** 属性指示客户端卸载也会删除客户端崩溃日志和日志文件。 这是可选项，但如果你以后重新安装客户端，那么这是帮助避免混淆的最佳方案。  

3.  如果需要，手动删除 Configuration Manager 所使用的客户端身份验证证书，或将其吊销。 CMUnistall 不会删除或吊销此证书。  

##  <a name="a-namebkmkrenewa-renewing-the-mac-client-certificate"></a><a name="BKMK_Renew"></a> 续订 Mac 客户端证书  
 使用下列方法之一续订 Mac 客户端证书：  

-   [Renewing the Mac client certificate by using the Renew Certificate Wizard](#BKMK_UI)  

-   [Renewing the Mac client certificate manually](#BKMK_Man)  

###  <a name="a-namebkmkuia-renewing-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a><a name="BKMK_UI"></a> 使用续订证书向导续订 Mac 客户端证书  
 使用下列过程在 Configuration Manager 中配置和使用续订证书向导。  

##### <a name="to-renew-the-mac-client-certificate-by-using-the-renew-certificate-wizard"></a>要使用续订证书向导续订 Mac 客户端证书  

1.  在 ccmclient.plist 文件中配置以下值以控制续订证书向导的打开时间：  

    > [!IMPORTANT]  
    >  你必须以字符串形式配置这些值。 如果将值配置为整数数据类型（通过使用 **-int** 属性），则将不会读取这些值。  

    -   **RenewalPeriod1** - 指定用户可以在其中续订证书的第一个续订期间（以秒为单位）。 默认值为 3,888,000 秒（45 天）。  

        > [!NOTE]  
        >  如果将“RenewalPeriod1”  配置为大于或等于 300 秒，则将使用配置的值。  如果配置的值大于 0 而小于 300 秒，则将使用默认值 45 天。  

    -   **RenewalPeriod2** - 指定用户可以在其中续订证书的第二个续订期间（以秒为单位）。 默认值为 259,200 秒（3 天）。  

        > [!NOTE]  
        >  如果将“RenewalPeriod2”  配置为大于或等于 300 秒且小于或等于“RenewalPeriod1” ，则将使用配置的值。 如果“RenewalPeriod1”  大于 3 天，则“RenewalPeriod2” 将使用的值为 3 天。  如果“RenewalPeriod1”  小于 3 天，则“RenewalPeriod2”  设置为与“RenewalPeriod1” 相同的值。  

    -   **RenewalReminderInterval1** - 指定在第一个续订期间将向用户显示续订证书向导的频率（以秒为单位）。 默认值为 86,400 秒（1 天）。  

        > [!NOTE]  
        >  如果“RenewalReminderInterval1”  大于 300 秒且小于为“RenewalPeriod1” 配置的值，则将使用配置的值。 否则，将使用默认值，即 1 天。  

    -   **RenewalReminderInterval2** - 指定在第二个续订期间将向用户显示续订证书向导的频率（以秒为单位）。 默认值为 28,800 秒（8 小时）。  

        > [!NOTE]  
        >  如果“RenewalReminderInterval2”  大于 300 秒、小于等于“RenewalReminderInterval1”  且小于等于“RenewalPeriod2” ，则将使用配置的值。 否则，将使用的值为 8 小时。  

     **示例：** 如果将各值保留为其默认值，则在证书到期前 45 天，将每 24 小时打开该向导。  在证书到期前 3 天内，将每隔 8 小时打开该向导。  

     **示例：** 使用以下命令行或脚本将第一个续订期间设置为 20 天。  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  当预订证书向导打开时，通常将预先填充“用户名”  和“服务器名称”  字段，用户只需输入密码即可续订证书。  

    > [!NOTE]  
    >  如果向导未打开或者你无意中关闭了向导，请单击“Configuration Manager”  首选项页中的“续订”  以打开向导。  

###  <a name="a-namebkmkmana-renewing-the-mac-client-certificate-manually"></a><a name="BKMK_Man"></a> 手动续订 Mac 客户端证书  
 Mac 客户端证书的有效期通常为 1 年。 Configuration Manager 不自动续订其在注册过程中请求的用户证书，因此你必须使用以下程序来手动续订证书。  

> [!IMPORTANT]  
>  如果证书过期，你必须卸载、重新安装并随后重新注册 Mac 客户端。  

 此过程会删除为相同 Mac 计算机请求新证书所需的 SMSID。 请求新证书后，Configuration Manager 会自动使用该证书。  

> [!IMPORTANT]  
>  如果删除和替换客户端 SMSID，则从 Configuration Manager 控制台中删除客户端之后会删除诸如清单之类的任何存储的客户端历史记录。  

##### <a name="to-renew-the-mac-client-certificate-manually"></a>要手动续订 Mac 客户端证书  

1.  为必须续订用户证书的 Mac 计算机创建设备集合，然后将 Mac 计算机添加到该集合中。  

    > [!WARNING]  
    >  Configuration Manager 不监视它为 Mac 计算机注册的证书的有效期。 你必须独立于 Configuration Manager 监视此有效期，以标识要添加到此集合中的 Mac 计算机。  

2.  在“资产和符合性”  工作区中，启动“创建配置项目向导” 。  

3.  在向导的“常规”  页上，指定下列信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **类型：Mac OS X**  

4.  在向导的“支持的平台”  页上，确保选择所有的 Mac OS X 版本。  

5.  在向导的“设置”  页上，单击“新建”  ，然后在“创建设置”  对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **设置类型：脚本**  

    -   **数据类型：字符串**  

6.  在“创建设置”  对话框中，对于“发现脚本” ，请单击“添加脚本”  以指定发现配置有 SMSID 的 Mac 计算机的脚本。  

7.  在“编辑发现脚本”  对话框中，输入以下外壳脚本：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  单击“确定”  以关闭“编辑发现脚本”  对话框。  

9. 在“创建设置”  对话框中，对于“修正脚本(可选)” ，请单击“添加脚本”  以指定在 Mac 计算机上发现 SMSID 时将其删除的脚本。  

10. 在“创建修正脚本”  对话框中，输入以下外壳脚本：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 单击“确定”  以关闭“创建修正脚本”  对话框。  

12. 在向导的“符合性规则”  页上，单击“新建” ，然后在“创建规则”  对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   “选择设置：” 单击“浏览”  ，然后选择你先前指定的发现脚本。  

    -   在“以下值”  字段中，输入 **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**。  

    -   启用“当此设置不符合时运行指定的修正脚本” 选项。  

13. 完成“创建配置项目向导”。  

14. 创建一个包含你刚刚创建的配置项目的配置基线，然后将它部署到你在步骤 1 中创建的设备集合。  

     有关如何创建和部署配置基线的详细信息，请参阅[如何在 System Center Configuration Manager 中创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)和[如何在 System Center Configuration Manager 中部署配置基线](../../../compliance/deploy-use/deploy-configuration-baselines.md)。  

15. 在删除了 SMSID 的 Mac 计算机上，运行以下命令以安装新证书：  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     出现提示时，提供超级用户帐户的密码以运行命令，然后提供 Active Directory 用户帐户的密码。  

16. 若要将注册的证书限制在 Configuration Manager 范围内，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    1.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  在“密钥链访问”  对话框中的“密钥链”  部分中，单击“系统” ，然后在“类别”  部分中，单击“密钥” 。  

    3.  展开密钥以查看客户端证书。 标识了具有刚才安装的私钥的证书后，双击密钥。  

    4.  在“访问控制”  选项卡上，选择“在允许访问前确认” 。  

    5.  浏览到“/Library/Application Support/Microsoft/CCM” ，选择“CCMClient” ，然后单击“添加” 。  

    6.  单击“保存更改”  并关闭“密钥链访问”  对话框。  

17. 重新启动 Mac 计算机。  

##  <a name="a-namebkmkmanualcertifcateinstallationa-use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a><a name="BKMK_ManualCertifcateInstallation"></a> 使用与 Configuration Manager 无关的证书请求和安装方法  
 但如果不使用 Configuration Manager 注册，请独立于 Configuration Manager 请求和安装客户端证书，配置步骤略微不同：  

1.  执行步骤 1、2、4、6（可选）和 8。  

2.  不执行步骤 3、5、7 和 9。  

3.  按照以下说明安装客户端。  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>独立于 Configuration Manager 安装客户端证书并安装客户端  

1.  要独立于 Configuration Manager 安装客户端证书，请使用所选证书部署方法附带的说明在 Mac 计算机上请求和安装客户端证书。  

2.  导航到文件夹，你在该文件夹中已经提取了从 Microsoft 下载中心下载的 macclient.dmg 文件的内容。  

3.  输入以下命令行：**sudo ./ccmsetup -MP <管理点 Internet FQDN\> -SubjectName <证书使用者值\>**  

    > [!IMPORTANT]  
    >  证书使用者值区分大小写，因此请键入与证书详细信息中显示的值完全相同的值。  

     示例：如果站点系统属性中的 Internet FQDN 为 **server03.contoso.com**，并且 Mac 客户端证书以 **mac12.contoso.com** 的 FQDN 作为证书使用者中的公用名，请键入：**sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  请一直等到看到“已完成安装”  消息，然后重启 Mac 计算机。  

5.  要确保 Configuration Manager 可以访问此证书，请在 Mac 计算机上打开终端窗口并进行以下更改：  

    1.  输入命令 **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    2.  在“密钥链访问”  对话框中的“密钥链”  部分中，单击“系统” ，然后在“类别”  部分中，单击“密钥” 。  

    3.  展开密钥以查看客户端证书。 标识了具有刚才安装的私钥的证书后，双击密钥。  

    4.  在“访问控制”  选项卡上，选择“在允许访问前确认” 。  

    5.  浏览到“/Library/Application Support/Microsoft/CCM” ，选择“CCMClient” ，然后单击“添加” 。  

    6.  单击“保存更改”  并关闭“密钥链访问”  对话框。  

6.  如果有多个包含同一使用者值的证书，你必须指定证书序列号以标识要用于 Configuration Manager 客户端的证书。 若要执行此操作，请使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序列号\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 在 Mac 计算机上的“系统首选项”  中打开“Configuration Manager”  项以验证客户端安装是否成功。 也可以更新和查看“所有系统”  集合，以确认现在 Mac 计算机在此集合中显示为托管客户端。  

### <a name="renewing-the-mac-client-certificate"></a>续订 Mac 客户端证书  
 在 Mac 计算机上续订计算机证书之前，请使用以下过程。  

 此过程会删除客户端在 Mac 计算机上使用新证书或续订的证书所需的 SMSID。  

> [!IMPORTANT]  
>  如果删除和替换客户端 SMSID，则从 Configuration Manager 控制台中删除客户端之后会删除诸如清单之类的任何存储的客户端历史记录。  

##### <a name="to-renew-the-mac-client-certificate"></a>要续订 Mac 客户端证书  

1.  为必须续订计算机证书的 Mac 计算机创建设备集合，然后将 Mac 计算机添加到该集合中。  

2.  在“资产和符合性”  工作区中，启动“创建配置项目向导” 。  

3.  在向导的“常规”  页上，指定下列信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **类型：Mac OS X**  

4.  在向导的“支持的平台”  页上，确保选择所有的 Mac OS X 版本。  

5.  在向导的“设置”  页上，单击“新建”  ，然后在“创建设置”  对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   **设置类型：脚本**  

    -   **数据类型：字符串**  

6.  在“创建设置”  对话框中，对于“发现脚本” ，请单击“添加脚本”  以指定发现配置有 SMSID 的 Mac 计算机的脚本。  

7.  在“编辑发现脚本”  对话框中，输入以下外壳脚本：  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  单击“确定”  以关闭“编辑发现脚本”  对话框。  

9. 在“创建设置”  对话框中，对于“修正脚本(可选)” ，请单击“添加脚本”  以指定在 Mac 计算机上发现 SMSID 时将其删除的脚本。  

10. 在“创建修正脚本”  对话框中，输入以下外壳脚本：  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. 单击“确定”  以关闭“创建修正脚本”  对话框。  

12. 在向导的“符合性规则”  页上，单击“新建” ，然后在“创建规则”  对话框中指定以下信息：  

    -   **名称：删除 Mac 的 SMSID**  

    -   “选择设置：” 单击“浏览”  ，然后选择你先前指定的发现脚本。  

    -   在“以下值”  字段中，输入 **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**。  

    -   启用“当此设置不符合时运行指定的修正脚本” 选项。  

13. 完成“创建配置项目向导”。  

14. 创建一个包含你刚刚创建的配置项目的配置基线，然后将它部署到你在步骤 1 中创建的设备集合。  

     有关如何创建和部署配置基线的详细信息，请参阅[如何在 System Center Configuration Manager 中创建配置基线](../../../compliance/deploy-use/create-configuration-baselines.md)。  

15. 在删除了 SMSID 的 Mac 计算机上安装了新的证书后，运行以下命令，以便将客户端配置为使用此新证书：  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. 如果有多个包含同一使用者值的证书，你必须指定证书序列号以标识要用于 Configuration Manager 客户端的证书。 若要执行此操作，请使用下列命令：**sudo defaults write com.microsoft.ccmclient SerialNumber -data "<序列号\>"**。  

     例如： **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. 重新启动 Mac 计算机。  



<!--HONumber=Nov16_HO1-->


