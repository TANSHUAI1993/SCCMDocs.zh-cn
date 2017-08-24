---
title: "Technical Preview 1606 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 中的可用功能，1606 版。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
caps.latest.revision: "31"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 08747ca981f6697e2bd621afe5df0e3bd06b332d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1606-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 版本 1606 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview 版本 1606 中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    

**此 Technical Preview 中的已知问题：**  
*  当从技术预览版 1604 更新到 1605 ，然后再更新到 1606 时，更新可能会失败，并且会在 **cmupdate.log** 中记录一个类似于以下的错误：

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    如果发生这种情况，请在“更新与维护服务”节点中单击“检查更新”，然后单击“重试”，以重试更新安装。
    ***

**以下是可以试用的此版本的新功能。**  

## <a name="dmp_category"></a>自动将设备分类到集合
可创建设备类别，可将其用于配合使用 Microsoft Intune 和 Configuration Manager 时自动在设备集合中放置设备。 然后要求用户在 Intune 中注册设备时选择某个设备类别。 此外，还可以从 Configuration Manager 控制台中更改设备的类别。

**重要提示：**此功能适用于 **2016 年 6** 月版本的 Microsoft Intune。 试用这些过程前，请确保已更新到此版本。

### <a name="try-it-out"></a>试试看！

### <a name="create-a-set-of-device-categories"></a>创建一组设备类别
1.  在 Configuration Manager 控制台的“资产和符合性”工作区中，展开“概述”，然后单击“设备集合”。
2.  在“主页”选项卡上的“类别” 组中，单击“管理设备类别”。
3.  在“管理设备类别”对话框中，可以创建、编辑或删除类别。 尝试创建新类别。

### <a name="associate-a-collection-with-a-device-category"></a>将集合与设备类别相关联
将集合与设备类别关联后，指定的分类中的所有设备都会添加到该集合。
1.  在设备集合的“属性”对话框中，单击“添加规则” > “设备类别规则”。
2.  在“创建设备类别成员身份规则”对话框中，选择将应用到集合中所有设备的类别。
3.  关闭“创建设备类别成员身份规则”对话框和集合属性对话框。

### <a name="change-the-category-of-a-device"></a>更改设备的类别
1.  在 Configuration Manager 控制台的“资产和符合性”工作区中，展开“概述”，然后单击“设备”。
2.  从“设备”列表选择一个设备，然后在“主页”选项卡上的“设备”组中，单击“更改类别”。
3.  在“编辑设备类别”对话框框中，选择将应用于此设备的类别，然后单击“确定”。

## <a name="dmp_grace"></a>所需的应用程序和软件更新部署的强制宽限期

在某些情况下，可能会希望为用户提供更多时间（超出所配置的任何截止时间）来安装所需的应用程序部署或软件更新。 通常，当一台计算机关闭的时间过长和计算机需要安装大量应用程序或更新部署时，会需要执行这种操作。
例如，如果最终用户刚从假期返回，则他们可能需要等待很长时间，因为安装的应用程序部署已过期。
为了帮助解决此问题，现在可通过将 Configuration Manager 客户端设置部署到集合来定义强制的宽限期。

### <a name="try-it-out"></a>试试看！

若要配置宽限期，请执行以下操作：

1.  在客户端设置的“计算机代理”页上，将“部署截止时间后强制的宽限期(小时)”这一新属性的值配置为介于 **1** 和 **120** 小时之间。
2.  在新的所需应用程序部署中，或在现有部署属性中，在“计划”页上，选中复选框“根据用户首选项延迟此部署的强制执行”，延迟时间以客户端设置中定义的宽限期为依据。
选中了此复选框的所有部署，以及针对其中部署了客户端设置的设备的所有部署，都将使用此强制的宽限期。

如果配置强制宽限期，并选中该复选框，则当到达应用程序安装截止时间后，将在用户按照宽限期配置的第一个非业务窗口中安装该应用程序。 但是，用户仍可打开软件中心并在任何所需时间安装该应用程序。 一旦过了宽限期，对于未完成的部署，强制将恢复为正常行为。
已将类似的选项添加到软件更新部署向导、自动部署规则向导和属性页中。

##  <a name="dmp_devg"></a>通过 Device Guard 将 Configuration Manager 用作托管的安装程序

“设备保护”是 Windows 10 的一种功能，它使用硬件和软件功能严格控制什么可以在设备上运行。

有关“设备保护”的功能和工作方式的详细概述请参阅[此 Technet 文章](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview)。

在此版本中，Configuration Manager 可与“设备保护”和 [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) 进行互操作，以便当通过 Configuration Manager 部署的可执行文件和 DLL 文件从托管安装程序到来时自动变为受信任，这意味着将允许它们在目标设备上运行，而其他软件将不允许运行，除非由其他 AppLocker 规则明确允许运行。  

目前，无法从 Configuration Manager 控制台中配置此功能。 若要配置该策略，需要在每个客户端上配置注册表项并在客户端上配置 Windows 服务。
完成此操作后，请配置 AppLocker 策略文件。 配置策略文件后，可以将其部署到任何兼容的客户端设备。


与所有 AppLocker 策略一样，托管安装程序规则的策略可以两种模式运行：

- 审核模式 - 不会阻止应用程序运行，如果有阻止的应用程序，会在日志文件中报告（以后的一个更高版本的 Configuration Manager 将支持此功能）。
- 启用强制 – 阻止应用程序运行。

有关如何结合使用 Configuration Manager 和设备保护的详细信息，请参阅[企业移动性和安全性博客](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10)。

延伸阅读：

- [设备保护简介](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [设备保护认证和符合性](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [设备保护部署指南](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

 ##  <a name="dmp_onprem"></a>本地移动设备管理的多个设备管理点  
 借助 Technical Preview 1606，本地移动设备管理 (MDM) 可支持Windows 10 周年更新中的新功能，该功能会自动将已注册设备配置为具有多个可供使用的设备管理点。 此功能允许设备在其正常使用的设备管理点不可用时回退到另一个设备管理点。 此功能仅适用于安装了 Windows 10 周年更新的电脑。  

### <a name="try-it-out"></a>试试看！  

1.  在层次结构中安装多个设备管理点。  

2.  注册 Windows 10 周年更新设备以实现本地移动设备管理。  

有关如何准备站点和注册设备以实现本地移动设备管理，请参阅[使用 System Center Configuration Manager 中的本地基础结构管理移动设备](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

## <a name="cloud_proxy"></a>用于管理 Internet 上客户端的云代理服务

云代理服务提供一种简单方法来管理 Internet 上的 Configuration Manager 客户端。 该服务部署到 Microsoft Azure 且需要 Azure 订阅，它使用名为云代理连接点的新角色连接到本地 Configuration Manager 基础结构。 服务完全部署并配置好后，客户端可以访问本地 Configuration Manager 站点系统角色，而不管它们是连接到内部专用网络还是 Internet 上。

使用 Configuration Manager 控制台将服务部署到 Azure，添加云代理连接器点角色，并配置站点系统角色以允许云代理通信。 云代理服务目前只支持管理点、分发点和软件更新点角色。

需要用客户端证书和安全套接字层 (SSL) 证书来进行计算机身份验证和加密不同服务层之间的通信。 通常，客户端计算机通过组策略实施接收客户端证书。 若要加密客户端和托管角色的站点系统服务器之间的通信，需要从 CA 创建自定义 SSL 证书。 除了这两种证书类型，还需要对 Azure 设置管理证书以允许 Configuration Manager 部署云代理服务。  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>TP 1606 中云代理服务的要求
- 运行云代理连接器点的客户端计算机和站点系统服务器。
- 内部 CA 自定义 SSL 证书 - 用来加密来自客户端计算机的通信和对云代理服务器的标识进行身份验证。
- 云服务的 Azure 订阅。
- Azure 管理证书 - 用于通过 Azure 对 Configuration Manager 进行身份验证。

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>TP 1606 中云代理服务的限制

- 只支持管理点、分发点和软件更新点角色。
- 不支持用户策略。
- 不能用于 Configuration Manager 中的[本地移动设备管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) 。
- 仅通过 Azure 公有云平台进行支持。


### <a name="try-it-out"></a>试试看！

云代理服务部署过程包括以下步骤：

1. 创建和颁发云代理服务的自定义 SSL 证书。
1. 导出客户端证书的根。
2. 将管理证书上传到 Azure。
3. 在 Configuration Manager 控制台中设置云代理服务。
4. 配置主站点以使用客户端证书身份验证。
5. 将云代理连接点添加到网站。
6. 配置站点系统角色，以接受云代理通信。

以下部分会介绍有关完成这些步骤的详细信息。

#### <a name="create-a-custom-ssl-certificate"></a>创建自定义 SSL 证书

采用针对基于云的分发点的同一方法，为云代理服务创建自定义 SSL 证书。 按照[为基于云的分发点部署服务证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012)中的说明，但以不同方式执行以下操作：

* 在设置新证书模板时，向为 Configuration Manager 服务器设置的安全组提供**读取**和**注册**权限。

#### <a name="export-the-client-certificates-root"></a>导出客户端证书的根

导出网络上所用的客户端证书根的最简捷的方法就是打开已加入域且有客户端证书的一台计算机上的客户端证书并进行复制。

>[!NOTE]
>希望通过云代理服务管理的计算机以及托管云代理连接点的站点系统服务器都需要客户端证书。 如果需要将客户端证书添加到任何这类计算机上，请参阅[为 Windows 计算机部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012)。

1. 在“运行”窗口中，键入 **mmc**，然后按“Return”。
2. 在管理控制台中的“文件”菜单上，单击“添加/删除管理单元...”。
3. 在“添加或删除管理单元”对话框中，单击“证书”，单击“添加”>，单击“计算机帐户”，单击“下一步”，单击“本地计算机”，然后单击“完成”。 单击“确定”  关闭对话框。
4. 转到“证书”>“个人”>“证书”。
5. 双击计算机上用于客户端身份验证的证书，单击“证书路径”选项卡，然后双击根颁发机构（位于路径顶部）。
6.  单击“详细信息”选项卡，然后单击“复制到文件...”。
7. 使用默认证书格式完成证书导出向导。 记下创建的根证书的名称和位置。 将需要在后面的一个步骤中使用它来配置云代理服务。

#### <a name="upload-the-management-certificate-to-azure"></a>将管理证书上传到 Azure

Configuration Manager 需要 Azure 管理证书来访问 Azure API 和配置云代理服务。 有关如何上传管理证书的详细信息和说明，请参阅 Azure 文档中的以下文章：
- [Azure 云服务证书概述](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [上传 Azure Management API 管理证书](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)。

请确保复制与管理证书关联的订阅 ID。 需要使用此 ID 在 Configuration Manager 控制台中配置云代理服务。

#### <a name="set-up-cloud-proxy-service"></a>设置云代理服务

1. 在 Configuration Manager 控制台中转到“管理”>“云服务”>“云代理服务”。
2. 单击“创建云代理服务”。
3. 在“创建云代理服务”向导中，输入 Azure 订阅 ID（从 Azure 管理门户复制），单击“浏览”，并选择要上传为 Azure 管理证书的证书文件。 单击“下一步” 。 请花费少许时间，等待控制台连接 Azure。
4. 在向导中填写其他详细信息：
    - 指定从自定义 SSL 证书中导出的私钥（.pfx 文件）。
    - 指定从客户端证书导出的根证书。
    - 指定创建新证书模板时使用的同一服务名称 FQDN。
    - 清除“验证客户端证书吊销”旁边的复选框（除非要公开发布 CRL 信息）。
    - 完成后单击“下一步”。
5. 检查设置，然后单击“下一步”。 Configuration Manager 开始设置服务。 向导完成后，可单击“关闭”，但需花费 5 到 15 分钟时间在 Azure 中完整配置该服务。 检查新设置的云代理服务的“状态”，以确定服务是否已设置完毕。

#### <a name="configure-primary-site-for-client-certification-authentication"></a>配置客户端证书身份验证的主站点

1. 在 Configuration Manager 控制台中，转到“管理”>“站点配置”>“站点”。
2. 选择希望通过云代理服务管理的客户端的主站点，并单击“属性”。
3. 在主站点属性表的“客户端计算机通信”选项卡上，选中“在可用时使用 PKI 客户端证书（客户端身份验证）”旁边的复选框。
4. 请确保清除“客户端检查站点系统的证书吊销列表 (CRL)”旁边的复选框。 仅当公开发布 CRL 时才需选择此选项。
5. 单击" **确定**"。

#### <a name="add-the-cloud-proxy-connector-point"></a>添加云代理连接点

云代理连接点是一种新站点系统角色，用于与云代理服务进行通信。 若要添加云代理连接点，请按照[添加 System Center Configuration Manager 的站点系统角色](../../core/servers/deploy/configure/add-site-system-roles.md)中的说明操作。

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>配置用于云代理通信的角色

设置云代理服务的最后一步是配置站点系统角色以接受云代理通信。 对于 Tech Preview 1606，云代理服务只支持管理点、分发点和软件更新点角色。 必须分别配置每个角色。

1. 在 Configuration Manager 控制台中，转到“管理”>“站点配置”>“服务器和站点系统角色”。
2. 单击要配置的云代理通信的角色的站点系统服务器。
3. 单击“角色”，然后单击“属性” 。
4. 在角色属性表中的“客户端连接”下，选择“HTTPS”，选中“允许 Configuration Manager 云代理通信”旁边的复选框，然后单击“确定”。 为其余角色重复这些步骤。

#### <a name="check-status-on-a-client-on-the-internet"></a>检查 Internet 上客户端的状态

对服务和角色进行完全配置后，内部客户端会在下一次位置请求时获取云代理服务的位置。 然后，带有已更新的位置信息的客户端便可在 Internet 上与 Configuration Manager 进行通信。 位置请求的轮询周期为 24 小时。 如果不想等待按正常计划执行的位置请求，可以通过重新启动计算机上的 SMS 代理主机服务 (ccmexec.exe) 强制执行该请求。

客户端拥有云代理服务的新位置信息后，请尝试检查已不在内部专用网络上但具有 Internet 访问权限的客户端的状态。 还可以通过后列方式监视云代理服务通信：转到“管理”>“云服务”>“云代理服务”，在列表窗格中选择服务，然后查看详细信息窗格中的通信信息。   

## <a name="manage_o365"></a>在 Configuration Manager 中管理 Office 365 客户端代理  

从 Technical Preview 1606 开始，可以使用 Configuration Manager 客户端代理设置而非组策略，来使 Office 365 客户端接收来自 Configuration Manager 的更新。 配置此设置和部署 Office 365 更新后，Configuration Manager 客户端代理将与 Office 365 客户端代理通信，从分发点下载 Office 365 更新并进行安装。 Configuration Manager 还会获取客户端代理设置的清单。

有关详细信息，请参阅[管理 Office 365 ProPlus 更新](https://technet.microsoft.com/library/mt741983.aspx)。

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>设置 Configuration Manager 客户端设置以管理 Office 365 客户端代理
1.  在 Configuration Manager 控制台中，单击“管理” > “概述” > “客户端设置”。
2. 打开相应的设备设置以启用客户端代理。 有关默认客户端设置和自定义客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。
3. 单击“软件更新”，并针对“启用 Office 365 客户端代理的管理”设置选择“是”。  


## <a name="osdpreservedriveletter"></a>已弃用 OSDPreserveDriveLetter 任务序列变量
OSDPreserveDriveLetter 任务序列变量决定当将此图像应用到目标计算机时，任务序列是否使用在操作系统映像 WIM 文件中捕获的驱动器号。
- Technical Preview 1606 中已弃用此任务序列变量。

现在，在操作系统部署期间，默认情况下，Windows 安装程序会确定要使用的最佳驱动器号（通常为 C:）。 如果想要指定使用另一个驱动器，可以在“应用操作系统”任务序列步骤中更改位置。 转到“选择要应用此操作系统的位置”设置，选择“特定逻辑驱动器号”，然后选择要使用的驱动器。 目标计算机上必须存在分配有该号的驱动器。 

## <a name="updatesandservicing"></a>更新和服务节点的更改
Technical Preview 1606 版中做了几处更改，适用于 Configuration Manager 控制台中的更新与服务：
- **节点名称更改：**

    在“监视”工作区中，已将“站点服务状态”节点重命名为“更新和服务状态”。
- **更多安装状态：**

    查看站点的更新安装状态时，控制台现在会显示以下操作的单独详细信息：
    - **下载**（这仅适用于在其中安装服务连接点站点系统角色的顶层站点）
    - **复制**
    - **先决条件检查**
    - **安装**

  此外，现在对于每个步骤有更详细的信息，包括可以在哪个日志文件查看更多信息。  
-   **用于重试先决条件失败的新选项：**

    在“管理”和“监视”这两个工作区中，“更新和服务”节点都在功能区上包含了一个名为“忽略先决条件警告”的新按钮。

    如果安装更新时不使用“忽略先决条件警告”选项（从更新向导中），更新安装会中止并出现“先决条件警告”状态，那么之后可以在功能区选择“忽略先决条件警告”来触发更新的自动继续安装，而忽略先决条件警告。  



- **更清楚的更新视图：**

    查看“更新和服务”节点时，现在仅能看到最近安装的更新以及任何可供安装的新更新。 若要查看以前安装的更新，请单击功能区中新的“历史记录”按钮。  

-   **重命名的预生产选项：**

    在“更新和服务”节点中，名为“客户端选项”的按钮现重命名为“提升预生产客户端”。
