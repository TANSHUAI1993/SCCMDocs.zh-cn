---
title: 管理分发点
titleSuffix: Configuration Manager
description: 使用分发点托管部署到设备和用户的内容。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21ed29204a5ed41e54a12a1294bc9582d3e6eaa1
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67252328"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>在 Configuration Manager 中安装和配置分发点

适用范围：  System Center Configuration Manager (Current Branch)

安装 Configuration Manager 分发点以托骨干部署到设备和用户的内容文件。 创建分发点组以简化管理分发点和将内容分发到分发点的方式。  

使用安装向导安装新的分发点  。 有关详细信息，请参阅[安装分发点](#bkmk_install)。 要管理现有分发点的属性，请编辑分发点的属性  。 有关详细信息，请参阅[配置分发点](#bkmk_configs)。

使用任一方法配置大多数分发点设置。 有几个设置仅安装或编辑时才可用，但无法同时可用：  

- 仅在安装分发点时可用的设置：  

    - **允许 Configuration Manager 在分发点计算机上安装 IIS**

    - **为分发点配置驱动器空间设置**  

- 仅在编辑分发点属性时可用的设置：  

    - **管理分发点组关系**  

    - **查看部署到分发点的内容**  

    - **为分发点的数据传输配置速率限制**  

    - **为分发点的数据传输配置计划**  


## <a name="bkmk_install"></a>安装分发点  

选择站点系统服务器作为分发点，然后才能将内容提供给客户端计算机使用。 必须将分发点分配给至少一个[边界组](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points)，然后本地客户端计算机才能将此分发点用作内容源位置。 将分发点角色添加到新站点系统服务器，或将其添加到现有站点系统服务器。

### <a name="bkmk_install-prereq"></a> 先决条件

安装新的分发点时，可使用安装向导来帮助完成可用设置的配置。 开始之前，请注意以下先决条件：  

- 你必须拥有下列安全权限才能创建和配置分发点：  

    - “分发点”  对象的“读取”  权限  

    - “分发点”  对象的“复制到分发点”  权限  

    - “站点”  对象的“修改”  权限  

    - “站点”  对象的“管理操作系统部署证书”  权限  

- 在托管分发点的 Windows 服务器上安装 Internet Information Services (IIS)。 或者，安装站点系统角色时，Configuration Manager 会为用户安装并配置 IIS。  

### <a name="bkmk_install-procedure"></a>安装分发点的过程  

使用此过程添加新的分发点。 要更改现有分发点的配置，请参阅[配置分发点](#bkmk_configs)部分。  

从[安装站点系统角色](/sccm/core/servers/deploy/configure/install-site-system-roles)的常规过程开始。 在“创建站点系统服务器”向导的“系统角色选择”页上选择“分发点”角色   。 此操作将以下页面添加到向导：  

- [分发点](#bkmk_config-general)
- [驱动器设置](#bkmk_config-drive)
- [拉取分发点](#bkmk_config-pull)
- [PXE 设置](#bkmk_config-pxe)
- [多播](#bkmk_config-multicast)
- [内容验证](#bkmk_config-valid)
- [边界组](#bkmk_config-boundary)

> [!Important]  
> 仅在安装分发点时，以下设置才可用：  
>
> - **允许 Configuration Manager 在分发点计算机上安装 IIS**  
>
> - **为分发点配置驱动器空间设置**  

有关特定于分发点角色向导页的详细信息，请参阅[配置分发点](#bkmk_configs)部分。 例如，如果要将分发点安装为[拉取分发点](#bkmk_config-pull)，请选择“启用此分发点以从其他分发点拉取内容”选项  。 然后进行拉取分发点所需的其他配置。  

完成“创建站点系统服务器”向导后，该站点会将分发点角色添加到站点系统服务器。  


## <a name="bkmk_manage"></a>管理分发点组  

分发点组为内容分发提供分发点的逻辑分组。 使用这些组，可以从中央位置管理和监视跨多个站点的分发点的内容。 请记住以下几点：

- 将层次结构内的任何站点中的一个或多个分发点添加到分发点组。  

- 将分发点添加到多个分发点组。  

- 将内容分发到分发点组时，Configuration Manager 会将内容分发到属于组成员的所有分发点。  

- 在进行初始的内容分发之后，如果将某个分发点添加到组，则 Configuration Manager 会将内容自动分发到新的分发点成员。  

- 将集合与分发点组关联。 将内容分发到该集合时，Configuration Manager 将决定哪个组与集合关联。 之后，它将内容分发到作为这些组成员的所有分发点。  

    > [!NOTE]  
    > 将内容分发到某集合后，如果将此集合关联到新的分发点组，则必须将内容重新分发到此集合，然后才能将内容分发到新的分发点组。  

下一节将列出管理分发点组的以下操作的过程：  

- [创建和配置新的分发点组](#bkmk_dpgroup-create)
- [修改现有分发点组](#bkmk_dpgroup-modify)
- [将所选分发点添加到现有分发点组中](#bkmk_dpgroup-addexist)

### <a name="bkmk_dpgroup-create"></a>创建和配置新分发点组的过程  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点组”节点   。  

2. 在功能区上，选择“创建组”  。  

3. 在“创建新分发点组”窗口中，输入组的名称  和描述  （可选）。  

4. 在“成员”  选项卡上，选择“添加”  。  

5. 在“添加分发点”窗口中，选择一个或多个分发点，将其添加为组成员。 然后选择“确定”  。  

6. 如有必要，切换到“创建新分发点组”窗口的“集合”  选项卡，然后选择“添加”  。  

7. 在“选择集合”窗口中，选择要与分发点组关联的集合，再选择“确定”  。  

8. 在“创建新分发点组”窗口中，选择“确定”  以创建组。  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>从现有分发点创建新组

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点”节点   。 选择一个或多个分发点以添加到新分发点组中。  

2. 在功能区中，选择“添加所选项”  ，然后选择“将所选项添加到新分发点组中”  。  

此过程会自动使用所选服务器填充“创建新分发点组”窗口的“成员”选项卡  。

### <a name="bkmk_dpgroup-modify"></a>修改现有分发点组的过程  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点组”节点   。  

2. 选择要修改的现有分发点组。 在功能区中，选择“属性”  。  

3. 要将新集合与此组关联，请切换到“集合”  选项卡，然后选择“添加”  。 选择该集合，然后选择“确定”  。  

4. 要将新分发点添加到此组，请切换到“成员”  选项卡，然后选择“添加”  。 选择分发点，然后选择“确定”  。  

5. 选择“确定”  以保存对分发点组所做的更改。  

### <a name="bkmk_dpgroup-addexist"></a>将所选分发点添加到现有分发点组的过程  

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点”节点   。 选择一个或多个分发点以添加到现有组中。  

2. 在功能区中，选择“添加所选项”  ，然后选择“将所选项添加到现有分发点组中”  。  

3. 在“可用分发点组”中，选择要将所选分发点添加为其成员的组  。 然后选择“确定”  。  


## <a name="bkmk_reassign"></a>重新分配分发点

<!-- 1306937 -->

许多客户都有大型的 Configuration Manager 基础结构，并且正在减少主站点或辅助站点来简化其环境。 他们仍需要在分支机构位置保留分发点，以向托管客户提供内容。 这些分发点通常包含多个 TB 或更多的内容。 将此内容分发到这些远程服务器所需的时间和网络带宽成本高昂。

从 1802 版开始，此功能允许向其他主站点重新分配分发点，而无需重新分发内容。 此操作可更新站点系统分配，同时在服务器上保留所有内容。 如果需要重新分配多个分发点，请首先对一个分发点执行此操作。 然后继续对其他服务器执行操作（一次一个）。

> [!IMPORTANT]  
> 目标服务器只能托管分发点角色。 如果站点系统服务器承载其他 Configuration Manager 服务器角色，例如状态迁移点，则无法重新分配分发点。 无法重新分配云分发点。

在重新分配分发点之前，将目标站点服务器的计算机帐户添加到目标分发点服务器上的本地管理员组。

请按照下列步骤操作以重新分配分发点：

1. 在 Configuration Manager 控制台中，连接到管理中心站点。  

2. 转到“管理”工作区，并选择“分发点”节点   。  

3. 右键单击目标分发点，然后选择“重新分配分发点”  。  

4. 选择想要向其重新分配分发点的目标站点服务器和站点代码。  

像添加新角色时那样监视重新分配。 最简单的方法是在几分钟后刷新控制台视图。 将站点代码列添加到视图中。 Configuration Manager 重新分配服务器时会更改此值。 如果尝试在刷新控制台视图之前在目标服务器上执行另一项操作，会出现“找不到对象”错误。 在服务器上开始任何其他操作之前，请确保此过程完成并刷新控制台视图。

重新分配分发点后，请刷新服务器的证书。 新的站点服务器需要使用其公钥重新加密此证书，并将其存储在站点数据库中。 有关详细信息，请参阅分发点属性的“[常规](#bkmk_config-general)”选项卡上的“创建自签名证书或导入分发点的公钥基础结构 (PKI) 客户端证书”设置  。

- 对于 PKI 证书，无需创建新证书。 导入相同的 .PFX，并输入密码。  

- 对于自签名证书，请调整到期日期或时间以更新。  

- 如果不刷新证书，分发点仍提供内容，但以下功能会失败：  

    - 内容验证消息（distmgr.log 显示它无法解密该证书）  

    - 适用于客户端的 PXE 支持  

### <a name="tips"></a>提示

- 从管理中心站点执行此操作。 此操作有助于复制到主站点。  

- 请勿在将内容分发到目标服务器后，再尝试重新分配它。 在重新分配过程中，正在进行的分发内容任务可能会失败，但它会按正常重试。  

- 如果服务器也是 Configuration Manager 客户端，请确保也将该客户端重新分配到新的主站点。 此步骤对于使用客户端组件下载内容的拉取分发点尤为重要。  

- 此过程从旧站点的默认边界组中删除分发点。 如有必要，则需要手动将其添加到新站点的默认边界组。 所有其他边界组分配保持不变。  


## <a name="bkmk_maint"></a> 维护模式

<!--3555754-->

从版本 1902 开始，可在维护模式下设置分发点。 如果要安装软件更新，或对服务器进行硬件更改，请启用维护模式。

当分发点处于维护模式下时，其行为如下：

- 站点不会向该分发点分发任何内容。  

- 管理点不会向客户端返回此分发点的位置。

- 更新站点时，维护模式下的分发点仍会更新。

- 分发点属性为只读。 例如，不能更改证书或添加边界组。  

- 任何计划的任务（例如，内容验证）仍按相同的日程安排运行。

请谨慎对多个分发点启用维护模式。 此操作可能导致对其他分发点产生性能影响。 根据边界组配置，客户端可能增加下载次数或无法下载内容。

### <a name="enable-maintenance-mode"></a>启用维护模式

若要将分发点置于维护模式，用户帐户需要“站点”  类上的“修改”  权限。 例如，基础结构管理员  和完全权限管理员  内置角色具有此权限。<!-- SCCMDocs-pr issue #3407 -->

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。  

2. 选择“分发点”  节点。  

3. 选择目标分发点，并从功能区中选择“启用维护模式”  。  

若要查看分发点的当前状态，请向控制台中的“分发点”节点添加“分发模式”列  。

有关使用 Configuration Manager SDK 自动执行此过程的详细信息，请参阅[类 SMS_DistributionPointInfo 中的 SetDPMaintenanceMode 方法](/sccm/develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo)。


## <a name="bkmk_configs"></a>配置分发点  

各分发点支持各种不同的配置。 但是，并非所有分发点类型都支持所有配置。 例如，云分发点不支持启用了 PXE 或多播的部署。 有关特定限制的详细信息，请参阅以下文章：  

- [使用云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- [使用请求分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

当[安装新分发点](#bkmk_install-procedure)或[编辑现有分发点](#bkmk_change-procedure)时，以下各节介绍了分发点配置：  

- [常规设置](#bkmk_config-general)
- [驱动器设置](#bkmk_config-drive)
- [拉取分发点](#bkmk_config-pull)
- [PXE 设置](#bkmk_config-pxe)
- [多播](#bkmk_config-multicast)
- [内容验证](#bkmk_config-valid)
- [边界组](#bkmk_config-boundary)

#### <a name="bkmk_change-procedure"></a>更改分发点的过程

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点”节点   。  

2. 选择要配置的分发点。 在功能区中，选择“属性”  。  

3. 编辑分发点的属性时，请使用以下部分中的信息。  

4. 进行所需更改后，请选择“确定”  以保存设置并关闭分发点属性。  

### <a name="bkmk_config-general"></a>常规  

以下设置位于“创建站点系统服务器”向导的“分发点”页和分发点属性窗口的“常规”选项卡上   ：  

- **在 Configuration Manager 要求的情况下安装和配置 IIS**：如果服务器上尚未安装 IIS，Configuration Manager 将安装并配置它。 Configuration Manager 在所有分发点上都需要 IIS。 如果未选择此设置，并且服务器上未安装 IIS，需要先安装 IIS，Configuration Manager 才能成功安装分发点。  

    > [!NOTE]  
    > 此选项仅在“创建站点系统服务器”向导的“分发点”页上  。 它仅在[安装新分发点](#bkmk_install-procedure)时可用。  

- **启用和配置此分发点的 BranchCache**：选择此设置以允许 Configuration Manager 在分发点服务器上配置 Windows BranchCache。 有关详细信息，请参阅 [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache)。  

- **调整下载速度以使用未用网络带宽(Windows LEDBAT)**<!--1358112-->：自版本 1806 开始，启用分发点可使用网络拥塞控制。 有关详细信息，请参阅 [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat)。 获取 LEDBAT 支持要满足的最低要求：<!-- SCCMDocs issue 883 -->  

    - Configuration Manager 版本 1806（常规版本）  

        - Windows Server 版本 1709 或更高版本  

    - 包含更新汇总 (4462978) 的 Configuration Manager 版本 1806 或更高版本  

        - Windows Server 版本 1709 或更高版本
        - 包含更新 KB4132216 和 KB4284833 的 Windows Server 2016

    - Configuration Manager 版本 1810 或更高版本：

        - Windows Server 版本 1709 或更高版本
        - 包含更新 KB4132216 和 KB4284833 的 Windows Server 2016
        - Windows Server 2019  

- **描述**：此分发点角色的可选描述。  

- **配置客户端设备与分发点通信的方式**：使用 HTTP 或 HTTPS 有一些优点和缺点   。 有关详细信息，请参阅[内容管理的最佳安全做法](/sccm/core/plan-design/hierarchy/security-and-privacy-for-content-management#BKMK_Security_ContentManagement)。  

- **允许客户端进行匿名连接**：此设置指定分发点是否允许从 Configuration Manager 客户端到内容库的匿名连接。  

    > [!Important]  
    > 如果不使用此设置，请在 Windows 7 客户端上应用 Microsoft 知识库文章 [2619572](https://support.microsoft.com/help/2619572/) 中描述的更改。 否则，Windows Installer 应用程序的修复可能会失败。  
    >
    > 部署 Windows Installer 应用程序时，Configuration Manager 客户端会将文件下载到其本地缓存。 安装完成后，客户端最终会删除这些文件。 Configuration Manager 客户端更新应用程序的 Windows Installer 源列表。 它设置关联分发点上内容库的内容路径。 稍后，如果尝试修复设备上的应用程序，MSIExec 将尝试使用匿名用户访问内容路径。  
    >
    > 在客户端上安装更新并修改记录的注册表项后，MSIExec 将使用已登录的用户帐户访问内容路径。  

- **创建自签名证书或导入 PKI 客户端证书**：Configuration Manager 将此证书用于以下目的：  

    - 在分发点发送状态消息之前，该证书向管理点验证分发点。  

    - 当在“PXE 设置”页上“为客户端启用 PXE 支持”时，分发点会将其发送到 PXE 启动的计算机   。 然后，这些计算机使用它在 OS 部署过程中连接到管理点。  

    在站点中为 HTTP 配置所有管理点时，请选择“创建自签名证书”选项  。 配置 HTTPS 的管理点时，请使用从 PKI“导入证书”选项  。  

    要导入证书，请浏览到有效的公钥加密标准 (PKCS #12) 文件。 此 PFX 或 CER 文件具有 PKI 证书，其中包含对 Configuration Manager 的以下要求：  

    - 预期用途包括客户端身份验证  

    - 启用要导出的私钥  

    > [!TIP]  
    > 对证书“使用者”或“使用者可选名称 (SAN)”没有特定要求。 如有必要，将同一个证书用于多个分发点。  

    有关证书要求的详细信息，请参阅 [PKI 证书要求](/sccm/core/plan-design/network/pki-certificate-requirements)。  

    有关此证书的部署示例，请参阅[为分发点部署客户端证书](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012)。  

- **为预留内容启用此分发点**：使用此设置可在分发软件之前向服务器添加内容。 由于内容文件已在内容库中，因此，当分发软件时，不会通过网络传输内容文件。 有关详细信息，请参阅[预留内容](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent)。  

### <a name="bkmk_config-drive"></a>驱动器设置  

> [!NOTE]  
> 这些选项仅在安装新分发点时可用。  

指定分发点的驱动器设置。 为内容库和包共享分别配置最多两个磁盘驱动器。 前两个驱动器达到配置的驱动器空间预留量时，Configuration Manager 可以使用其他驱动器。 “驱动器设置”  页配置磁盘驱动器的优先级以及每个磁盘驱动器上剩余的可用磁盘空间量。  

- **保留的驱动器空间 (MB)** ：在 Configuration Manager 选择其他驱动器并对其继续执行复制过程之前，此值会确定驱动器上的可用空间量。 内容文件可以跨多个驱动器。  

- **内容位置**：在此分发点上指定内容库和包共享的位置。 默认情况下，所有内容位置设置为“自动”  。 Configuration Manager 将内容复制到主内容位置，直至可用空间量达到指定的“保留的驱动器空间 (MB)”  值。 选择“自动”时，Configuration Manager 会将主要内容位置设置为安装时磁盘空间最大的磁盘驱动器  。 它将辅助位置设置为具有第二大可用磁盘空间的磁盘驱动器。 当主位置和辅助位置达到保留的驱动器空间时，Configuration Manager 将选择另一个具有最多可用磁盘空间的可用驱动器，以继续执行复制过程。  

> [!Tip]  
> 若要阻止 Configuration Manager 安装在特定驱动器上，请在安装分发点之前创建一个名为 **no_sms_on_drive.sms** 的空文件，并将该文件复制到驱动器的根文件夹。  

有关详细信息，请参阅[内容库](/sccm/core/plan-design/hierarchy/the-content-library)。

### <a name="bkmk_config-pull"></a>拉取分发点  

当你“启用此分发点以从其他分发点拉取内容”时，它将成为拉取分发点  。 可更改分发点获取分发内容的方式。 有关详细信息，请参阅[使用拉取分发点](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)。

对于所配置的每个拉取分发点，指定从中获取内容的一个或多个源分发点：  

- 选择“添加”  ，然后选择一个或多个可用分发点作为源。  

- 使用箭头按钮调整优先级。 当拉取分发点尝试传输内容时，优先级是它与源分发点联系的顺序。 它首先联系具有最低值的分发点。  

### <a name="bkmk_config-pxe"></a>PXE  

指定是否在分发点上启用 PXE。 使用 PXE 在客户端上启动 OS 部署。 有关如何在 Configuration Manager 中使用 PXE 的详细信息，请参阅[使用 PXE 通过网络部署 Windows](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)。

启用 PXE 时，Configuration Manager 会在服务器上安装 Windows 部署服务 (WDS)（如果需要）。 WDS 是执行 PXE 启动以安装操作系统的服务。 完成创建分发点向导后，Configuration Manager 将在使用 PXE 启动功能的 WDS 中安装提供程序。

从版本 1806 开始，可在没有 WDS 的分发点上启用 PXE。

选择“为客户端启用 PXE 支持”选项，然后配置下列设置  ：  

> [!Note]  
> 在“查看 PXE 的所需端口”  对话框中，选择“是”  ，以确认你想要启用 PXE。 Configuration Manager 将在 Windows 防火墙上自动配置默认端口。 如果使用其他防火墙，请手动配置这些端口。  
>
> 如果在同一台服务器上安装 WDS 和 DHCP，请配置 WDS 以侦听其他端口。 默认情况下，DHCP 侦听同一端口。 有关详细信息，请参阅 [WDS 和 DHCP 在同一个服务器上时的注意事项](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#BKMK_WDSandDHCP)。  

- **允许此分发点响应传入的 PXE 请求**：指定是否启用 WDS 以响应 PXE 服务请求。 使用此设置来启用和禁用服务，而不从分发点中删除 PXE 功能。  

- **启用未知计算机支持**：指定是否启用对不受 Configuration Manager 管理的计算机的支持。 有关详细信息，请参阅[准备未知计算机部署](/sccm/osd/get-started/prepare-for-unknown-computer-deployments)。  

- **在没有 Windows 部署服务的情况下启用 PXE 响应方**：从版本 1806 开始，可通过此选项在分发点上启用 PXE 响应方，而不需要 WDS。 此 PXE 响应程序支持 IPv6 网络。 如果在已启用 PXE 的分发点上启用此选项，Configuration Manager 将暂停 WDS 服务。 如果禁用此选项，但仍使用“为客户端启用 PXE 支持”  ，分发点会重新启用 WDS。<!--1357580-->  

    > [!Note]  
    > 在版本 1810 及更低版本中，不支持在同时运行 DHCP 服务器的服务器上使用不含 WDS 的 PXE 响应程序。
    >
    > 自版本 1902 起，如果你对分发点启用不含 Windows 部署服务的 PXE 响应程序，它现在与 DHCP 服务位于同一服务器上。 <!--3734270-->  

- **当计算机使用 PXE 时要求密码**：为了提高 PXE 部署的安全性，请指定强密码。  

- **用户设备相关性**：指定你希望分发点如何将用户与 PXE 部署的目标计算机关联。 选择下列选项之一：  

  - **通过自动批准允许用户设备相关性**：选择此设置以自动将用户与目标计算机关联，而无需等待批准。  

  - **允许用户设备相关性挂起管理员批准**：选择此设置以在将用户与目标计算机关联之前等待管理用户批准。  

  - **不允许用户设备相关性**：选择此设置以指定不将用户与目标计算机关联。 此设置为默认设置。  

    有关用户设备相关性的详细信息，请参阅[将用户和设备同用户设备相关性相链接](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)。  

- **网络接口**：指定分发点响应来自所有网络接口或来自特定网络接口的 PXE 请求。 如果分发点响应特定网络接口，然后提供每个网络接口的 MAC 地址。  

    > [!Note]  
    > 更改网络接口时，请重新启动 WDS 服务以确保正确保存配置。 自版本 1806 起，使用 PXE 响应程序服务时，重启“ConfigMgr PXE 响应程序服务”  (SccmPxe)。<!--SCCMDocs issue 642-->  

- **指定 PXE 服务器响应延迟(秒)** ：使用多个 PXE 服务器时，请指定启用了 PXE 的此分发点在响应计算机请求之前应等待的时长。 默认情况下，启用了 Configuration Manager PXE 的分发点会立即响应。  

### <a name="bkmk_config-multicast"></a>多播  

指定是否在分发点上启用多播。 多播部署将数据同时发送到多个 Configuration Manager 客户端，从而节省网络带宽。 如果不使用多播，服务器会通过单独的连接向每个客户端发送一份数据副本。 有关使用 OS 部署的多播的详细信息，请参阅[使用多播通过网络部署 Windows](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)。

启用多播时，Configuration Manager 会在服务器上安装 Windows 部署服务 (WDS)（如有需要）。  

选择“启用多播以将数据同时发送到多个客户端”选项，然后配置下列设置  ：  

- **多播连接帐户**：指定在为多播配置 Configuration Manager 数据库连接时使用的帐户。 有关详细信息，请参阅[多播连接帐户](/sccm/core/plan-design/hierarchy/accounts#multicast-connection-account)。  

- **多播地址设置**：指定 IP 地址，用于将数据发送到目标计算机。 默认情况下，它从为分发多播地址启用的 DHCP 服务器中获取 IP 地址。 根据网络环境，可以指定从 239.0.0.0 到 239.255.255.255 的 IP 地址范围。  

    > [!IMPORTANT]  
    > 请求 OS 映像的目标计算机必须可访问你配置的 IP 地址。 验证路由器和防火墙是否允许目标计算机和分发点之间的多播流量。  

- **用于多播的 UDP 端口范围**：指定用于将数据发送到目标计算机的 UDP 端口的范围。  

    > [!IMPORTANT]  
    > 请求 OS 映像的目标计算机必须可访问 UDP 端口。 验证路由器和防火墙是否允许目标计算机和站点服务器之间的多播流量。  

- **最大客户端数**：指定可从此分发点下载 OS 映像的目标计算机的最大数量。  

- **启用计划的多播**：指定 Configuration Manager 如何控制何时开始将操作系统部署到目标计算机。 配置以下选项：  

    - **会话启动延迟(分钟)** ：指定 Configuration Manager 在响应第一个部署请求之前等待的分钟数。  

    - **最小会话大小(客户端)** ：指定在 Configuration Manager 开始部署操作系统之前必须收到的请求数。  

> [!IMPORTANT]  
> 从版本 1806 开始，若要启用和配置分发点属性“多播”选项卡上的多播，分发点必须使用 Windows 部署服务  。  
>
> - 如果你“为客户端启用 PXE 支持”并“启用多播以将数据同时发送到多个客户端”，则无法“在没有 Windows 部署服务的情况下启用 PXE 响应程序”    。  
>
> - 如果你“为客户端启用 PXE 支持”并“在没有 Windows 部署服务的情况下启用 PXE 响应程序”，则无法“启用多播以将数据同时发送到多个客户端”     

### <a name="bkmk_config-group"></a>组关系  

> [!NOTE]  
> 这些选项仅在编辑以前安装的分发点的属性时可用。  

管理此分发点所属的分发点组。  

要将此分发点作为成员添加到现有分发点组，请选择“添加”  。 在“添加到分发点组”窗口中，选择现有组，然后选择“确定”  。  

要从分发点组中删除此分发点，请在列表中选择组，然后选择“删除”  。 从分发点组中删除分发点不会删除分发点中的任何内容。

### <a name="bkmk_config-content"></a>内容  

> [!NOTE]  
> 这些选项仅在编辑以前安装的分发点的属性时可用。  

管理已分发到分发点的内容。 从部署包列表中进行选择，然后执行以下操作：  

- **验证**：启动对软件内容文件的完整性进行验证的过程。 若要查看内容验证过程的结果，请在“监视”  工作区中展开“分发状态”  ，然后选择“内容状态”  节点。 有关详细信息，请参阅[验证内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content)。  

- **重新分发**：将所选软件的所有内容文件复制到分发点，并覆盖现有文件。 通常使用此操作来修复内容文件。 有关详细信息，请参阅[重新分发内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#redistribute-content)。  

- **删除**：从分发点删除软件的内容文件。 有关详细信息，请参阅[删除内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#remove-content)。  

### <a name="bkmk_config-valid"></a>内容验证  

设置计划以验证分发点上内容文件的完整性。 如果按计划启用内容验证，Configuration Manager 将在计划的时间启动进程。 它根据本地 SMS_PackagesInContLib SCCMDP 类验证分发点上的所有内容。 你还可以配置内容验证优先级。 默认情况下，优先级设置为“最低”  。 在验证过程中，提高优先级可能会增加服务器上的处理器和磁盘利用率，但应会更快完成。

若要查看内容验证过程的结果，请在“监视”  工作区中展开“分发状态”  ，然后选择“内容状态”  节点。 会显示每种软件类型（例如，应用程序、软件更新包以及启动映像）的内容。  

> [!WARNING]  
> 虽然使用计算机的本地时间来指定内容验证计划，但 Configuration Manager 控制台仍会在 UTC 中显示该计划。  

有关详细信息，请参阅[验证内容](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content)。

### <a name="bkmk_config-boundary"></a> Boundary groups  

管理为其分配此分发点的边界组。 将分发点添加到至少一个边界组中。 在内容部署过程中，客户端必须位于与分发点关联的边界组中，才能将此分发点用作内容源位置。

配置边界组关系，定义客户端为查找内容而回退的时间以及可回退到的边界组  。 有关详细信息，请参阅[边界组](/sccm/core/servers/deploy/configure/boundary-groups)。

选择“添加”  ，然后从列表中选择现有边界组。

要为此分发点创建新边界组，请选择“创建”  。 有关如何创建和配置边界组的详细信息，请参阅[边界组的过程](/sccm/core/servers/deploy/configure/boundary-group-procedures)。

编辑以前安装的分发点的属性时，请管理“启用按需分发”选项  。 此选项允许 Configuration Manager 在客户端请求时自动将内容分发到此服务器。 有关详细信息，请参阅[按需内容分发](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution)。

### <a name="bkmk_config-sched"></a>计划  

> [!NOTE]  
> 这些选项仅在编辑以前安装的分发点的属性时可用。
>
> 仅当编辑站点服务器的远程分发点的属性时，此选项卡才可用。  

配置一个计划，该计划限制 Configuration Manager 何时可将数据传输到分发点。 按优先级来限制数据或为所选时间段关闭连接。

要限制数据，请在网格中选择时间段，并选择下列任一“可用性”设置  ：  

- **为所有优先级打开**：Configuration Manager 将数据发送到分发点而不受任何限制。 此设置是所有时间段的默认设置。  

- **允许中和高优先级**：Configuration Manager 仅向分发点发送中等优先级和高优先级数据。  

- **仅允许高优先级**：Configuration Manager 仅向分发点发送高优先级数据。  

- **已关闭**：Configuration Manager 不向分发点发送任何数据。  

在软件属性的“分发设置”选项卡上配置软件的“分发优先级”   。

> [!IMPORTANT]  
> 计划基于发送站点的时区，而不是分发点的时区。  

### <a name="bkmk_config-rate"></a>速率限制  

> [!NOTE]  
> 这些选项仅在编辑以前安装的分发点的属性时可用。  
>
> 仅当编辑站点服务器的远程分发点的属性时，此选项卡才可用。  

配置速率限制，以控制 Configuration Manager 用于将内容传输到分发点的网络带宽。 选择从以下选项：  

- **发送到此目标时无限制**：Configuration Manager 在不受速率限制约束的情况下将内容发送到分发点。 此设置为默认设置。  

- **脉冲模式**：此选项指定站点服务器发送到分发点的数据块的大小。 你也可以指定在两次发送各个数据块之间的时间延迟。 如果必须在连接到分发点的极低带宽网络上发送数据，请使用此选项。 例如，你有每五秒发送 1 KB 数据的约束，而不管某个给定时间的链接速度或其使用率如何。  

- **限制为按小时指定的最大传输速率**：指定此设置可以让站点仅使用你配置的一定比例时间，将数据发送到分发点。 使用此选项时，Configuration Manager 无法识别网络的可用带宽。 它划分了可发送数据的时间。 服务器发送数据的时间很短，在此时间后是不发送数据的时间段。 例如，如果将“限制可用带宽”设置为 50%，Configuration Manager 传输数据一段时间后，在相同的时间内不发送任何数据   。 不会管理实际数据量大小或数据块大小。 它只管理发送数据的时间量。  
