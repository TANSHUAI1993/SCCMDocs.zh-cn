---
title: "管理分发点 | Microsoft Docs"
description: "使用分发点以承载部署到设备和用户的内容（文件和软件）。 此处介绍如何安装和配置这些分发点。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4c94e4de5bbfe621492e8682c9424a48eb38196d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>为 System Center Configuration Manager 安装和配置分发点

*适用范围：System Center Configuration Manager (Current Branch)*
 
安装 System Center Configuration Manager 分发点以承载部署到设备和用户的内容（文件和软件）。 还可以创建分发点组，该组可简化管理分发点以及将内容分发到分发点的方式。  

 安装新的分发点（使用安装向导）或管理现有分发点属性（通过编辑分发点属性）时，可配置大多数分发点设置。 有几个设置仅安装或编辑时才可用，但无法同时可用：  

-   仅在安装分发点时可用的设置：  

    -   **允许 Configuration Manager 在分发点计算机上安装 IIS**

    -   **为分发点配置驱动器空间设置**  

-   仅在编辑分发点属性时可用的设置：  

    -   **管理分发点组关系**  

    -   **查看部署到分发点的内容**  

    -   **为分发点的数据传输配置速率限制**  

    -   **为分发点的数据传输配置计划**  

##  <a name="bkmk_install"></a>安装分发点  
 你必须将站点系统服务器指定为分发点，然后才能将内容提供给客户端计算机使用。 你可以将分发点站点角色添加到新站点系统服务器，或将站点角色添加到现有站点系统服务器。  

 安装新的分发点时，可使用安装向导来帮助完成可用设置的配置。 开始之前，请注意以下问题：  

-   你必须拥有下列安全权限才能创建和配置分发点：  

    -   “分发点” 对象的“读取”  权限  

    -   “分发点” 对象的“复制到分发点”  权限  

    -   “站点” 对象的“修改”  权限  

    -   “站点” 对象的“管理操作系统部署证书”  权限  

-   承载分发点的服务器上必须安装 Internet Information Services (IIS)。 安装站点系统角色时，Configuration Manager 会为用户安装并配置 IIS。  

使用以下基本步骤安装或更改分发点。 有关可用配置选项的详细信息，请参阅本主题的[配置分发点](#bkmk_configs)部分。  

#### <a name="to-install-a-distribution-point"></a>若要安装分发点  

1.  在 Configuration Manager 控制台中，选择“管理” >  “站点配置” > “服务器和站点系统角色”。  

2.  将分发点站点系统角色添加到新的或现有的站点系统服务器：  

    -   **新建站点系统服务器**：在“主页”选项卡上的“创建”组中，选择“创建站点系统服务器”。 创建站点系统服务器向导将会打开。  

    -   **现有站点系统服务器**：选择要在其中安装分发点站点系统角色的服务器。 选择服务器时，会在结果窗格中显示服务器上已经安装的站点系统角色的列表。  

         在“主页”选项卡上的“服务器”组中，选择“添加站点系统角色”。 添加站点系统角色向导将会打开。  

3.  在“常规”  页上，指定站点系统服务器的一般设置。 向现有站点系统服务器添加分发点时，请验证以前配置的值。  

4.  在“系统角色选择”页上，从可用角色列表中选择“分发点”，然后选择“下一步”。  

5.  有关该向导的后续页，请参阅[配置分发点](#bkmk_configs)部分中的信息。  

     例如，如果希望将分发点安装为请求分发点，请选择“允许此分发点请求来自其他分发点的内容”，然后配置请求分发点所需的其他配置。  

6.  完成向导后，会将分发点站点角色添加到站点系统服务器。  

#### <a name="to-change-a-distribution-point"></a>更改分发点  

1.  在 Configuration Manager 控制台中，选择“管理” >  “分发点”，然后选择要配置的分发点。  

2.  在“主页”选项卡上的“属性”组中，选择“属性”。  

3.  编辑分发点的属性时，请参考[配置分发点](#bkmk_configs)中的相关信息。  

4.  进行所需更改后，请保存设置并关闭分发点属性。  

##  <a name="bkmk_manage"></a>管理分发点组  
 分发点组为内容分发提供分发点的逻辑分组。 使用这些组，可以从中央位置管理和监视跨多个站点的分发点的内容。 请记住以下几点：

-   可以将层次结构内的任何站点中的一个或多个分发点添加到分发点组。  

-   可以将分发点添加到多个分发点组。  

-   将内容分发到分发点组时，Configuration Manager 会将内容分发到属于分发点组成员的所有分发点。  

-   在进行初始的内容分发之后，如果将某个分发点添加到分发点组，则 Configuration Manager 会将内容自动分发到新的分发点成员。  

-   可以将集合与分发点组关联。 将内容分发到该集合时，Configuration Manager 将决定哪个分发点组与集合关联。 之后，内容会分发到这些分发点组的所有分发点成员。  

    > [!NOTE]  
    >  将内容分发到某集合后，如果将此集合关联到新的分发点组，则必须将内容重新分发到此集合，然后才能将内容分发到新的分发点组。  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>创建和配置新的分发点组  

1.  在 Configuration Manager 控制台中，选择“管理” > “分发点组”。  

2.  在“主页”选项卡的“创建”组中，选择“创建组”。  

3.  输入分发点组的名称和描述。  

4.  在“集合”选项卡上，选择“添加”，选择要与分发点组关联的集合，然后选择“确定”。  

5.  在“成员”选项卡上，选择“添加”，选择要添加为分发点组的成员的分发点，然后选择“确定”。  

6.  选择“确定”以创建分发点组。  

#### <a name="to-add-distribution-points-and-associate-collections-with-an-existing-distribution-point-group"></a>添加分发点并将集合与现有的分发点组关联  

1.  在 Configuration Manager 控制台中，选择“管理” > “分发点组”。  

2.  在“主页”选项卡上的“属性”组中，选择“属性”。  

3.  在“集合”选项卡上，选择“添加”以选择要与分发点组关联的集合，然后选择“确定”。  

4.  在“成员”选项卡上，选择“添加”以选择要添加为分发点组的成员的分发点，然后选择“确定”。  

5.  选择“确定”以保存对分发点组所做的更改。  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>将所选分发点添加到新分发点组中  

1.  在 Configuration Manager 控制台中，选择“管理” > “分发点”，然后选择要添加到新分发点组中的分发点。  

2.  在“主页”选项卡上的“分发点”组中，展开“添加所选项目”，然后选择“将所选项目添加到新分发点组中”。  

3.  输入分发点组的名称和描述。  

4.  在“集合”选项卡上，选择“添加”以选择要与分发点组关联的集合，然后选择“确定”。  

5.  在“成员”选项卡上，确认想要 Configuration Manager 将列出的分发点添加为分发点组的成员。 选择“添加”以添加分发点，然后选择“确定”。  

6.  选择“确定”以创建分发点组。  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>将所选分发点添加到现有分发点组中  

1.  在 Configuration Manager 控制台中，选择“管理” > “分发点”，然后选择要添加到新分发点组中的分发点。  

2.  在“主页”选项卡上的“分发点”组中，展开“添加所选项目”，然后选择“将所选项目添加到现有分发点组中”。  

3.  在“可用分发点组”中，选择要将所选分发点添加为其成员的分发点组，然后选择“确定”。  

##  <a name="bkmk_configs"></a>配置分发点  
 各分发点支持各种不同的配置。 但是，并非所有分发点类型都支持所有配置。 例如，基于云的分发点不支持为 PXE 或多播启用的内容部署。 可在以下主题中找到有关特定限制的信息：  

-   [结合使用基于云的分发点与 System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [结合使用请求分发点与 System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

下面的部分描述安装新分发点或编辑现有分发点的属性时可以选择的配置。  

### <a name="general"></a>常规  
 配置常规分发点设置：  

-   **在 Configuration Manager 要求的情况下安装和配置 IIS：**选择此设置以让 Configuration Manager 在服务器上安装和配置 IIS（如果尚未安装）。 必须在所有分发点上安装 IIS。 如果服务器上未安装 IIS，并且未选择此设置，则必须安装 IIS，然后才能成功安装分发点。  

    > [!NOTE]  
    >  此选项仅在安装新分发点时可用。  

- **对此分发点启用和配置 BranchCache：**选择此设置以允许 Configuration Manager 在分发点服务器上配置 Windows BranchCache。 有关配合使用 Windows BranchCache 与 System Center Configuration Manager 的详细信息，请参阅*对 System Center Configuration Manager 中 Windows 功能和网络的支持*中的 [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache)。

-   **配置客户端设备与分发点的通信方式：**无论是使用 HTTP 还是 HTTPS，都有一些优点和缺点。 有关详细信息，请参阅 [System Center Configuration Manager 中内容管理的基本概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)中的“安全最佳实践”。  

-   **允许客户端进行匿名连接**：此设置指定分发点是否允许从 Configuration Manager 客户端到内容库的匿名连接。  

    > [!IMPORTANT]  
    >  若不使用此设置，则客户端上的 Windows Installer 应用程序修复可能失败。  
    >   
    >  在 Configuration Manager 客户端上部署 Windows Installer 应用程序时，Configuration Manager 会将文件下载到客户端上的本地缓存。 安装完成后，最后会删除这些文件。
    >  
    >  Configuration Manager 客户端使用所关联分发点上的内容库的内容路径，以更新安装了 Windows Installer 应用程序的 Windows Installer 源列表。 稍后，如果在 Configuration Manager 客户端上通过“添加或删除程序”启动修复操作，MSIExec 将尝试通过使用匿名用户访问内容路径。  
    >   
    >  但是，可以安装 Microsoft 知识库文章 [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) 中所述的更新，然后修改注册表项以更改此行为。  
    >   
    >  在客户端上安装更新之后，MSIExec 将使用已登录的用户帐户（未选择“允许客户端进行匿名连接”设置时所用的账户）来访问内容路径。  

-   **为分发点创建自签名证书或导入公钥基础结构 (PKI) 客户端证书**：证书具有下列用途：  

    -   在分发点发送状态消息之前，该证书向管理点验证分发点。  

    -   如果在“PXE 设置”页上选中“为客户端启用 PXE 支持”复选框，则会将证书发送到执行 PXE 启动的计算机，以便这些计算机能够在操作系统部署过程中连接到管理点。  

    如果针对 HTTP 配置了站点中的所有管理点，请创建自签名证书。 如果针对 HTTPS 配置了管理点，请导入 PKI 客户端证书。  

    若要导入证书，请浏览到包含 PKI 证书的公钥加密标准 (PKCS #12) 文件，对于 Configuration Manager 有以下要求：  

    -   计划的使用必须包括客户端身份验证。  

    -   必须能够导出私钥。  

    > [!TIP]  
    >  没有针对证书使用者或使用者备用名称 (SAN) 的特定要求，并且你可以为多个分发点使用同一证书。  

     有关证书要求的详细信息，请参阅 [System Center Configuration Manager 的 PKI 证书要求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

     有关此证书的示例部署，请参阅 [System Center Configuration Manager 的 PKI 证书的分步部署示例：Windows Server 2008 证书颁发机构](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)主题中的“为分发点部署客户端证书”部分。  

-   **为预安排内容启用此分发点**：选择此设置为预安排内容启用分发点。 如果选择此设置，你可以在分发内容时配置分发行为。 可以选择始终执行以下操作之一：

 - 在分发点上预留内容。
 - 预留包的初始内容，但在有内容更新时使用普通内容分发流程。
 - 对包中的内容使用普通内容分发流程。  

### <a name="drive-settings"></a>驱动器设置  

> [!NOTE]  
>  这些选项仅在安装新分发点时可用。  

指定分发点的驱动器设置。 可以为内容库和包共享分别配置最多两个磁盘驱动器。 前两个驱动器达到配置的驱动器空间预留量时，Configuration Manager 可以使用其他驱动器。 “驱动器设置”  页配置磁盘驱动器的优先级以及每个磁盘驱动器上剩余的可用磁盘空间量。  

-   **保留的驱动器空间 (MB)**：在 Configuration Manager 选择其他驱动器并对其继续执行复制过程之前，为此设置配置的值会确定驱动器上的可用空间量。 内容文件可以跨多个驱动器。  

-   **内容位置**：指定内容库和包共享的内容位置。 Configuration Manager 将内容复制到主内容位置，直至可用空间量达到指定的“保留的驱动器空间 (MB)”值。 默认情况下，内容位置设置为“自动” 。 主内容位置设置为在安装时具有最多磁盘空间的磁盘驱动器，辅助位置将分配给具有第二多可用磁盘空间的磁盘驱动器。 当主驱动器和辅助驱动器达到保留的驱动器空间时，Configuration Manager 将选择另一个具有最多可用磁盘空间的可用驱动器，并继续执行复制过程。  

> [!NOTE]  
>  若要阻止 Configuration Manager 安装在特定驱动器上，请在安装分发点之前创建一个名为 **no_sms_on_drive.sms** 的空文件，并将该文件复制到驱动器的根文件夹。  

### <a name="pull-distribution-point"></a>请求分发点  
选择“允许此分发点从其他分发点请求内容”时，将更改计算机获取分发到该分发点的内容的行为方式。 它将成为请求分发点。  

对于所配置的每个请求分发点，必须指定该请求分发点从中获取内容的一个或多个源分发：  

-   选择“添加”，然后选择一个或多个可用分发点作为源分发点。  

-   选择“删除”将作为源分发点的所选分发点删除。  

-   使用箭头按钮调整请求分发点在尝试传输内容时与源分发点联系的顺序。 将首先联系具有最低值的分发点。  

### <a name="pxe"></a>PXE  
指定是否在分发点上启用 PXE。 启用 PXE 时，Configuration Manager 将在服务器上安装 Windows 部署服务（如果需要）。 Windows 部署服务是执行 PXE 启动以安装操作系统的服务。 完成创建分发点向导后，Configuration Manager 将在 Windows 部署服务中安装使用 PXE 启动功能的提供程序。  

在选择“为客户端启用 PXE 支持”时，请配置下列设置：  

-   **允许此分发点响应传入的 PXE 请求**：指定是否启用 Windows 部署服务以使其响应 PXE 服务请求。 使用此复选框来启用和禁用服务，而不从分发点中删除 PXE 功能。  

-   **启用未知计算机支持**：指定是否启用对 Configuration Manager 不管理的计算机的支持。  

-   **当计算机使用 PXE 时要求密码**：为了提高 PXE 部署的安全性，请指定强密码。  

-   **用户设备相关性**：指定你希望分发点如何将用户与 PXE 部署的目标计算机关联。 选择下列选项之一：  

    -   **通过自动批准允许用户设备相关性**：选择此设置以自动将用户与目标计算机关联，而无需等待批准。  

    -   **允许用户设备相关性挂起管理员批准**：选择此设置以在将用户与目标计算机关联之前等待管理用户批准。  

    -   **不允许用户设备相关性**：选择此设置以指定不将用户与目标计算机关联。  

     有关用户设备相关性的详细信息，请参阅[在 System Center Configuration Manager 中将用户和设备同用户设备相关性相链接](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。  

-   **网络接口**：指定分发点响应来自所有网络接口或来自特定网络接口的 PXE 请求。 如果分发点响应特定网络接口，必须提供每个网络接口的 MAC 地址。  

-   **指定 PXE 服务器响应延迟(秒)**：指定在使用了多个启用 PXE 的分发点时分发点在响应计算机请求之前延迟的时间长度（以秒为单位）。 默认情况下，Configuration Manager PXE 服务点首先响应网络 PXE 请求。  

> [!NOTE]  
>  可以使用 PXE 协议对 Configuration Manager 客户端计算机启动操作系统部署。 Configuration Manager 使用启用了 PXE 的分发点站点角色来启动操作系统部署过程。 启用 PXE 的分发点必须配置为：
>
> 1. 响应 Configuration Manager 客户端在网络上发出的 PXE 启动请求。
> 2. 与 Configuration Manager 基础结构交互，以确定要采取的适当部署操作。  

### <a name="multicast"></a>多播  
指定是否在分发点上启用多播。 启用多播时，Configuration Manager 会在服务器上安装 Windows 部署服务（如有需要）。  

如果选中“启用多播以将数据同时发送到多个客户端”复选框，请配置下列设置：  

-   **多播连接帐户**：指定在为多播配置 Configuration Manager 数据库连接时使用的帐户。  

-   **多播地址设置**：指定 IP 地址，用于将数据发送到目标计算机。 默认情况下，IP 地址是从为分发多播地址启用的 DHCP 服务器中获得的。 根据网络环境，可以指定从 239.0.0.0 到 239.255.255.255 的 IP 地址范围。  

    > [!IMPORTANT]  
    >  请求操作系统映像的目标计算机必须可访问你配置的 IP 地址。 验证路由器和防火墙是否允许目标计算机和站点服务器之间的多播流量。  

-   **用于多播的 UDP 端口范围**：指定用于将数据发送到目标计算机的用户数据报协议 (UDP) 端口的范围。  

    > [!IMPORTANT]  
    >  请求操作系统映像的目标计算机必须可访问 UDP 端口。 验证路由器和防火墙是否允许目标计算机和站点服务器之间的多播流量。  

-   **客户端传输速率**：选择用于将数据下载到目标计算机的传输速率。  

-   **最大客户端数**：指定可从此分发点下载操作系统的目标计算机的最大数量。  

-   **启用计划的多播**：指定 Configuration Manager 如何控制何时开始将操作系统部署到目标计算机。 配置以下选项：  

    -   **会话启动延迟(分钟)**：指定 Configuration Manager 在响应第一个部署请求之前等待的分钟数。  

    -   **最小会话大小(客户端)**：指定在 Configuration Manager 开始部署操作系统之前必须收到多少请求。  

> [!NOTE]  
>  多播部署将数据同时发送到多个 Configuration Manager 客户端，而不是通过单独连接向每个客户端发送数据副本，从而节省网络带宽。 有关使用操作系统多播的详细信息，请参阅[使用多播与 System Center Configuration Manager 一起通过网络部署 Windows](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)。  

### <a name="group-relationships"></a>组关系  

> [!NOTE]  
>  这些选项仅在编辑以前安装的分发点的属性时可用。  

管理此分发点所属的分发点组。  

要将此分发点作为成员添加到现有分发点组，请选择“添加”。 在“添加分发点组”对话框内的列表中选择现有分发点组，然后选择“确定”。  

要从分发点组中删除此分发点，请在列表中选择分发点组，然后选择“删除”。  

### <a name="content"></a>Content  

> [!NOTE]  
>  这些选项仅在编辑以前安装的分发点的属性时可用。  

管理已分发到分发点的内容。 **部署包**部分提供分发到此分发点的包的列表。 你可以从列表中选择包并执行下列操作：  

-   **验证**：启动对包中内容文件的完整性进行验证的过程。 若要查看内容验证过程的结果，请在“监视”工作区中展开“分发状态”，然后选择“内容状态”节点。  

-   **重新分发**：将包中的所有内容文件复制到分发点，并覆盖现有文件。 通常使用此操作来修复包中的内容文件。  

-   **删除**：为包从分发点中删除内容文件。  

### <a name="content-validation"></a>内容验证  
指定是否设置一个计划来验证分发点上的内容文件的完整性。 如果按计划启用内容验证，Configuration Manager 将在计划的时间启动进程，并且会验证分发点上的所有内容。 你还可以配置内容验证优先级。 默认情况下，优先级设置为“最低” 。  

若要查看内容验证过程的结果，请在“监视”工作区中展开“分发状态”，然后选择“内容状态”节点。 会显示每种包类型（例如，应用程序、软件更新包以及启动映像）的内容。  

> [!WARNING]  
>  虽然使用计算机的本地时间来指定内容验证计划，但 Configuration Manager 控制台仍会在 UTC 中显示该计划。  

### <a name="boundary-group"></a>边界组  
管理为其分配此分发点的边界组。 可以将边界组与分发点关联。 在内容部署过程中，客户端必须位于与分发点关联的边界组中，才能将其用作内容的源位置。

此外：

- 对于 1610 前的版本，可选中“允许客户端使用此站点系统作为内容的回退源位置”复选框，以便在没有其他分发点可用时让这些边界组外部的客户端回退并使用分发点作为内容的源位置。 有关边界组的详细信息，请参阅 [1511、1602 和 1606 版的边界组](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606)。 有关首选分发点的信息，请参阅 [System Center Configuration Manager 中内容管理的基本概念](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)。

- 借助 1610 或更高版本，可配置边界组关系，定义客户端为查找内容而回退的时间以及可回退到的边界组。 有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups)。


### <a name="schedule"></a>计划  

> [!NOTE]  
>  这些选项仅在编辑以前安装的分发点的属性时可用。  

> [!TIP]  
>  仅当编辑站点服务器计算机的远程分发点的属性时，此选项卡才可用。  

 指定是否配置一个计划，该计划限制 Configuration Manager 何时可将数据传输到分发点。  

> [!IMPORTANT]  
>  计划基于发送站点的时区，而不是分发点的时区。  

要限制数据，请选择时间段，并选择下列“可用性”设置之一：  

-   **为所有优先级打开**：指定 Configuration Manager 不受限制地将数据发送到分发点。  

-   **允许中和高优先级**：指定 Configuration Manager 仅向分发点发送中等优先级和高优先级数据。  

-   **仅允许高优先级**：指定 Configuration Manager 仅向分发点发送高优先级数据。  

-   **已关闭**：指定 Configuration Manager 不向分发点发送任何数据。  

你可以按优先级来限制数据或为所选时间段关闭连接。  

### <a name="rate-limits"></a>速率限制  

> [!NOTE]  
>  这些选项仅在编辑以前安装的分发点的属性时可用。  

> [!TIP]  
>  仅当编辑站点服务器计算机的远程分发点的属性时，此选项卡才可用。  

指定是否配置速率限制来控制在 Configuration Manager 将内容传输到分发点时使用的网络带宽。 可从以下选项中进行选择：  

-   **发送到此目标时无限制**：此选项指定 Configuration Manager 在不受速率限制约束的情况下将内容发送到分发点。  

-   **脉冲模式**：此选项指定发送到分发点的数据块的大小。 你也可以指定在两次发送各个数据块之间的时间延迟。 如果必须在连接到分发点的极低带宽网络上发送数据，请使用此选项。 例如，你可能有每五秒发送 1 KB 数据的约束，而不管某个给定时间的链接速度或其使用率如何。  

-   **限制为按小时指定的最大传输速率**：指定此设置以让站点仅使用你配置的时间百分比将数据发送到分发点。 如果使用此选项，Configuration Manager 将不会确定网络可用带宽，而是划分可发送数据的时间。 然后在一个短时间段内发送数据，之后的几个时间段则不发送数据。 例如，如果最大速率设置为 **50%**，Configuration Manager 传输数据一段时间后，在相同的时间内不发送任何数据。 不会管理实际数据量大小或数据块大小， 而只会管理发送数据期间的时间量。  
