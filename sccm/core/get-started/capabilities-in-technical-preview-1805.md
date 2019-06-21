---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview 1805 版中提供的新功能。
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4da8ff0e4d35284c5b1f2f465da468677cdfbb65
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286068"
---
# <a name="capabilities-in-technical-preview-1805-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1805 中的功能

适用范围：  System Center Configuration Manager (Technical Preview)

本文介绍 Configuration Manager Technical Preview 1805 版中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 

安装此更新之前，请查看 [Technical Preview](/sccm/core/get-started/technical-preview) 一文。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**以下是此版本可以试用的新功能。**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>使用手动配置的任务序列阶段创建分阶段部署
<!--1358148-->
现在可以使用手动配置的任务序列阶段[创建分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)。 可以从“创建分阶段部署”向导的“阶段”  选项卡添加最多 10 个其他阶段。 


### <a name="try-it-out"></a>试试看！
按照说明创建在其中手动配置所有阶段的分阶段部署。 发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。 

1. 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”    。  

2. 右键单击现有任务序列并选择“创建分阶段部署”  。  

3. 在“常规”  选项卡上，为分阶段部署提供名称、说明（可选），并选择“手动配置所有阶段”  。  

4. 在“阶段”  选项卡上，单击“添加”  。  

5. 指定该阶段**名称**，然后浏览到目标“阶段集合”  。  

6. 在“阶段设置”  选项卡上，为每个计划设置选择一个选项，然后在完成后选择“下一步”  。  

    - 上一阶段成功的标准（此选项对第一阶段禁用。）
        - **部署成功百分比**：指定根据上一阶段成功标准成功完成部署的设备所占的百分比。  

    - 在上一阶段成功后开始此阶段部署的条件  
        - **在延迟时间段(以天为单位)后自动开始此阶段**：选择在上一阶段成功后开始下一阶段之前等待的天数。 
        - **手动开始此阶段部署**：在上一阶段成功后不自动开始此阶段。  

    - 设备成为目标后，安装软件
        - **尽快**：确定目标设备后立即设置设备上的安装截止时间。
        - **截止时间(相对于确定目标设备的时间)** ：确定目标设备后设置特定天数的安装截止时间。  
     
7. 完成阶段设置向导。

8. 在创建分阶段部署向导的“阶段”  选项卡上，现在可以添加、删除、重新排序，或编辑此部署的各个阶段。  

9. 完成“创建分阶段部署”向导。  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>对 Azure 资源管理器的云分发点支持
<!--1322209-->
在创建[云分发点](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)实例时，向导现提供选项来创建“Azure 资源管理器部署”  。 [Azure 资源管理器](/azure/azure-resource-manager/resource-group-overview)是一个现代平台，用于以单个实体（称为[资源组](/azure/azure-resource-manager/resource-group-overview#resource-groups)）的方式来管理所有解决方案资源。 如果在 Azure 资源管理器中部署云分发点，站点将使用 Azure Active Directory (Azure AD) 进行身份验证并创建必要的云资源。 此现代化部署不需要经典 Azure 管理证书。  

云分发点向导仍提供使用 Azure 管理证书的“经典服务部署”  选项。 若要简化资源的部署和管理，我们建议为所有新的云分发点使用 Azure 资源管理器部署模型。 如果可以，请通过资源管理器重新部署现有云分发点。

Configuration Manager 不会将现有经典云分发点迁移到 Azure 资源管理器部署模型。 使用 Azure 资源管理器部署创建新的云分发点，然后删除经典云分发点。 

> [!IMPORTANT]  
> 此功能不提供对 Azure 云服务提供商 (CSP) 的支持。 Azure 资源管理器中的云发分点部署将继续使用 CSP 不支持的经典云服务。 有关详细信息，请参阅 [Azure CSP 中可用的 Azure 服务](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  


### <a name="prerequisites"></a>先决条件  
- 与 [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure) 集成。 不需要 Azure AD 用户发现。  

- [云分发点要求](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_requirements)相同，除了 Azure 管理证书。  


### <a name="try-it-out"></a>试试看！  
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台的“管理”  工作区中，展开“云服务”  ，然后选择“云分发点”  。 单击功能区中的“创建云分发点”  。   

2. 在“常规”  页上，选择“Azure 资源管理器部署”  。 单击“登录”  以使用 Azure 订阅管理员帐户进行身份验证。 该向导使用集成先决条件过程中存储的 Azure AD 订阅信息，自动填充其余字段。 如果拥有多个订阅，请选择要使用的所需订阅。 单击“下一步”  。  

3. 在“设置”  页上，像往常一样提供服务器 PKI 证书文件  。 此证书定义Azure 使用的云分发点服务 FQDN  。 选择“区域”  ，然后选择资源组选项“新建”  或“使用现有”  。 输入新的资源组名称，或从下拉列表中选择现有资源组。  

4. 完成向导。  

> [!NOTE]  
> 对于所选的 Azure AD 服务器应用，Azure 将分配订阅“参与者”  权限。  

使用服务连接点上的“cloudmgr.log”  来监视服务部署进度。



## <a name="take-actions-based-on-management-insights"></a>根据管理见解执行操作
<!--1357930-->
某些[管理见解](/sccm/core/servers/manage/management-insights)现在可以选择执行一个操作。 根据规则，此操作会出现以下行为之一：  

- 在控制台中自动导航到可以采取进一步操作的节点。 例如，如果管理见解建议更改客户端设置，执行操作将导航到“客户端设置”节点。 可以通过修改默认或自定义客户端设置对象采取进一步操作。  

- 基于查询导航到筛选的视图。 例如，对空集合规则执行操作只会在集合列表中显示这些集合。 此处可以采取进一步操作，例如删除集合或修改其成员身份规则。  

以下管理见解规则在此版本中具有操作：
- 安全
    - 不受支持的反恶意软件客户端版本
- 软件中心
    - 使用新版软件中心
- 应用程序
    - 不具有部署的应用程序
- 简化管理
    - 非 CB 客户端版本
- 集合
    - 空集合 
- 云服务
    - 将客户端更新到 Windows 10 最新版本



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>使用共同管理将设备配置工作负荷转移到 Intune
<!--1357903-->

现在可以在启用共同管理后，将设备配置工作负荷从 Configuration Manager 转移到 Intune。 转移此工作负荷可以使用 Intune 部署 MDM 策略，同时继续使用 Configuration Manager 来部署应用程序。 

要转移此工作负荷，请转到共同管理属性页并将滚动条从 Configuration Manager 移到“试点”  或“全部”  。 有关详细信息，请参阅 [Windows 10 设备共同管理](/sccm/core/clients/manage/co-management-overview)。

> [!Note]  
> 移动此工作负荷也会移动“资源访问”  和“Endpoint Protection”  工作负荷，这些工作负荷是设备配置工作负荷的子集。

转移此工作负荷时，仍然可以将设置从 Configuration Manager 部署到共同托管设备，即使 Intune 为设备配置颁发机构。 此异常可用于配置组织所需但在 Intune 中尚不可用的设置。 在 Configuration Manager 配置基线上指定此异常。 创建基线时，或在现有基线属性的“常规”  选项卡上，启用选项“即使是共同托管客户端也要始终应用此基线”  。 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>启用分发点以使用网络拥塞控制
<!--1358112-->

Windows 低额外延迟后台传输 (LEDBAT) 是 Windows Server 的一项功能，可帮助管理后台网络传输。 对于在支持版本的 Windows Server 上运行的分发点，可以启用一个选项以帮助调整网络流量。 客户端仅在允许的情况下使用网络带宽。 

有关 Windows LEDBAT 的详细信息，请参阅[新建传输改进](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/)博客文章。


### <a name="prerequisites"></a>先决条件
- Windows Server 版本 1709 上的一个分发点。  

- 没有客户端先决条件。<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 选择“分发点”  节点。 选择目标分发点，然后单击功能区中的“属性”  。  

2. 在“常规”  选项卡上，启用“调整下载速度以使用未使用的网络带宽(Windows LEDBAT)”  。  



## <a name="cloud-management-dashboard"></a>云管理仪表板
<!--1358461-->
新云管理仪表板  为云管理网关 (CMG) 使用情况提供一个集中视图。 通过 Azure AD 载入网站时，它还显示有关云用户和设备的数据。  

下面的屏幕截图是云管理仪表板的一部分，显示了两个可用磁贴：  
![云管理仪表板磁贴 CMG 流量和当前联机客户端](media/1358461-cmg-dashboard.png)

此功能还包括用于实时验证的 CMG 连接分析器  ，为疑难解答提供帮助。 控制台中的实用工具检查该服务的当前状态，以及通过 CMG 连接点通往任何允许 CMG 流量的管理点的通信通道。


### <a name="prerequisites"></a>先决条件
- 由基于 Internet 的客户端使用的活动[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)。  

- 载入 [Azure 服务](/sccm/core/servers/deploy/configure/azure-services-wizard)以进行云管理的站点。  


### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

#### <a name="cloud-management-dashboard"></a>云管理仪表板

在 Configuration Manager 控制台中，转到“监视”  工作区。 选择“云管理”  节点，并查看仪表板磁贴。  

#### <a name="cmg-connection-analyzer"></a>CMG 连接分析器

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“云服务”  并选择“云管理网关”  。  

2. 选择目标 CMG 实例，然后选择功能区中的“连接分析器”  。  

3. 在 CMG 连接分析器窗口中，选择以下选项之一对服务进行身份验证：  

     1.  Azure AD 用户：使用此选项来模拟与登录到加入 Azure AD 的 Windows 10 设备的云端用户标识相同的通信。 单击“登录”  以安全输入此 Azure AD 用户帐户的凭据。  

     2.  客户端证书：使用此选项来模拟与具有[客户端身份验证证书](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth)的 Configuration Manager 客户端相同的通信。  

4. 单击“启动”  开始分析。 结果将显示在分析器窗口中。 选择一个条目，查看“说明”字段中的更多详细信息。  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager 总是提供设备数据的大型集中式存储，客户可将其用于报告目的。 然而，这些数据只和上次从客户端那里收集的数据一样。 

CMPivot 是一种新的控制台中实用工具，它提供对环境中设备实时状态的访问。 它立即对目标集合中的所有连接设备运行查询，并返回结果。 然后你可以在工具中对此数据进行筛选和分组。 通过提供来自联机客户端的实时数据，可以更快地回答业务问题、解决问题并对安全事件作出响应。

例如，在[缓解推测执行端通道漏洞](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/)中，其中一个要求是更新系统 BIOS。 可以使用 CMPivot 来快速查询系统 BIOS 信息，并查找不符合要求的客户端。 

在此屏幕截图中，CMPivot 显示两个单独的 BIOS 版本，每个版本都具有各自的设备计数。 在尝试 CMPivot 时，可以使用此示例查询：  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![带示例查询的 BIOSVersion CMPivot 窗口](media/1358456-cmpivot-biosversion.png)

可以单击设备计数向下钻取以查看特定设备。 显示 CMPivot 中的设备时，可以右键单击某个设备并选择以下[客户端通知操作](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode)：
- 运行脚本
- 远程控制
- 资源浏览器

右键单击特定设备时，还可以透视到特定设备视图的以下属性之一：
- 自动启动命令
- 已安装的产品
- Processes
- 服务
- 用户
- 活动连接
- 缺少更新

### <a name="prerequisites"></a>先决条件
- 目标客户端必须更新到最新版本。  

- Configuration Manager 管理员需要权限才能运行脚本。 有关详细信息，请参阅[脚本的安全角色](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles)。  

### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区，并选择“设备集合”  。 选择目标集合，然后单击功能区中的“启动 CMPivot”  ，以便启动该工具。  

2. 界面进一步提供有关使用该工具的信息。 
     - 可以在顶部手动输入查询字符串，或单击联机文档中的链接。
     - 单击其中一个实体  将其添加到查询字符串。 
     - 有关表运算符  、聚合函数  和标量函数  的链接，请在 Web 浏览器中打开语言参考文档。 CMPivot 使用相同的查询语言作为 [Azure 日志分析](https://docs.microsoft.com/azure/kusto/query/)。



## <a name="improved-secure-client-communications"></a>已改进安全客户端通信
<!--1356889,1358228,1358460-->
建议对于所有 Configuration Manager 通信路径使用 HTTPS 通信，但由于管理 PKI 证书的开销，对一些客户来说可能是一个挑战。 Azure Active Directory (Azure AD) 集成的引入可以减少某些证书要求但不是所有证书要求。 

此版本包括对客户端与站点系统之间的通信方式的改进。 这些改进有两个主要目标：  

- 可以保护客户端通信，而无需提供 PKI 服务器身份验证证书。  

- 客户端可以安全地从分发点访问内容，而无需网络访问帐户。  

> [!Note]  
> PKI 证书仍是想要使用它的客户的有效选项。  


### <a name="bkmk_token"></a> 方案
以下方案受益于这些改进：  

#### <a name="bkmk_token1"></a> 方案 1：客户端到管理点
<!--1356889-->
[加入 Azure AD 的设备](/azure/active-directory/device-management-introduction#azure-ad-joined-devices)能够通过云管理网关 (CMG) 与为 HTTP 配置的管理点进行通信。 站点服务器为管理点生成证书，使其能够通过安全通道进行通信。   

> [!Note]  
> 此行为在 Configuration Manager 当前分支版本 1802 中有所不同，在这种情况下，它需要一个启用了 HTTPS 的管理点。 有关详细信息，请参阅[为管理点启用 HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps)。  

#### <a name="bkmk_token2"></a> 方案 2：客户端到分发点
<!--1358228-->
工作组或加入 Azure AD 的客户端可以通过安全通道从为 HTTP 配置的分发点下载内容。   

#### <a name="bkmk_token3"></a> 方案 3：Azure AD 设备标识 
<!--1358460-->
没有 Azure AD 用户登录的加入 Azure AD 的或[混合 Azure AD 设备](/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices)可以安全地与它的分配站点进行通信。 基于云的设备标识现只需使用 CMG 和管理点进行身份验证。  


### <a name="prerequisites"></a>先决条件  

- 针对 HTTP 客户端连接配置的管理点。 在站点系统角色属性的“常规”  选项卡上设置此选项。  

- 针对 HTTP 客户端连接配置的分发点。 在站点系统角色属性的“常规”  选项卡上设置此选项。 请勿启用选项“允许客户端进行匿名连接”  。  

- 云管理网关。  

- 将站点载入 Azure AD 以便进行云管理。  

    - 如果你的站点已满足此先决条件，则需更新 Azure AD 应用程序。 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“云服务”  ，然后选择“Azure Active Directory 租户”  。 选择 Azure AD 租户，再选择“应用程序”  窗格中 Web 应用程序，然后单击功能区中的“更新应用程序设置”  。  

- 运行 Windows 10 版本 1803 和加入 Azure AD 的客户端。 （从技术上讲，此要求仅适用于[方案 3](#bkmk_token3)。） 


### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  。 选择一个站点，然后单击功能区中的“属性”  。  

2. 切换到“客户端计算机通信”  选项卡。选择选项“HTTPS 或 HTTP”  ，然后启用新选项“将 Configuration Manager 生成的证书用于 HTTP 站点系统”  。  

参阅之前的[方案列表](#bkmk_token)进行验证。

> [!Tip]
> 在此版本中，请等待 30 分钟以便管理点从站点接收并配置新证书。

可以在 Configuration Manager 控制台中查看这些证书。 转到“管理”  工作区，展开“安全”  ，然后选择“证书”  节点。 查找“SMS 发证”  根证书，以及由 SMS 发证根颁发的站点服务器角色证书。


### <a name="known-issues"></a>已知问题
- 用户不能在软件中心查看任何可供他们使用的应用程序。  

- 操作系统部署方案仍需要网络访问帐户。  

- 快速反复启用和禁用选项“将 Configuration Manager 生成的证书用于 HTTP 站点系统”  可能会导致证书不正确地绑定到站点系统角色。 由“SMS 发证”证书颁发的任何证书都不会绑定到 Windows Server Internet Information Services (IIS) 中的网站。 若要解决此问题，请从 Windows 的 SMS  证书存储中删除由“SMS 发证”颁发的所有证书，然后重启 smsexec 服务。



## <a name="improvements-for-enabling-third-party-software-update-support"></a>启用第三方软件更新支持的改进
<!--1357605-->
有关[第三方软件更新支持](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)的 UserVoice 反馈结果是，此版本进一步迭代与 System Center Updates Publisher 的集成 (SCUP)。 Configuration Manager Technical Preview [版本 1803](/sccm/core/get-started/capabilities-in-technical-preview-1803#enable-third-party-software-update-support-on-clients) 添加了从 WSUS 读取证书以便进行第三方更新，然后将该证书部署到客户端的功能。 但仍需要使用 SCUP 工具创建和管理证书以签署第三方软件更新。

在此版本中，可以启用 Configuration Manager 站点来自动配置证书。 站点与 WSUS 进行通信，以此为该目的生成一个证书。 然后，Configuration Manager 继续将该证书部署到客户端。 此迭代不再需要使用 SCUP 工具来创建和管理证书。 

有关 SCUP 工具一般用途的详细信息，请参阅 [System Center Updates Publisher](/sccm/sum/tools/updates-publisher)。

### <a name="prerequisites"></a>先决条件
- 启用和部署“软件更新”  组中的客户端设置 **“启用第三方软件更新”** 。
- 如果 WSUS 在软件更新点的单独服务器上，则必须在远程 WSUS 服务器上执行以下选项之一：
    - 启用 Windows 中的远程注册表服务  
    或
    - 在注册表项 `HKLM\Software\Microsoft\Update Services\Server\Setup` 中，创建一个名为“EnableSelfSignedCertificates”  的新 DWORD，值为 `1`。 

### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“站点配置”  并选择“站点”  。 选择顶层站点，单击功能区中的“配置站点组件”  ，然后选择“软件更新点”  。  

2. 切换到“第三方更新”  选项卡。选择选项“启用第三方软件更新”  ，然后选择选项“Configuration Manager 自动管理证书”  。

3. 继续执行典型 SCUP 工作流的其余部分以导入第三方软件更新目录，然后将更新部署到客户端。



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>对 Windows 10 就地升级任务序列的改进
<!--1358500-->

Windows 10 就地升级的默认任务序列模板现在包括在升级过程失败的情况下要添加的带建议操作的另一个新组。 这些操作有助于进行故障排除。

### <a name="new-groups-under-run-actions-on-failure"></a>“在失败情况下运行操作”  下的新组
- **收集日志**：若要从客户端中收集日志，请在此组中添加步骤。 
    - 一种常见的做法是将日志文件复制到网络共享中。 若要建立此连接，请使用[连接到网络文件夹](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)步骤。 
    - 若要执行复制操作，请通过[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)或[运行 PowerShell 脚本](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)步骤来使用自定义脚本或实用工具。
    - 要收集的文件可能包括以下日志：  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - 有关 Setupact.log 和其他 Windows 安装程序日志的详细信息，请参阅 [Windows 安装程序日志文件](/windows/deployment/upgrade/log-files)。
    - 有关 Configuration Manager 客户端日志的详细信息，请参阅 [Configuration Manager 客户端日志](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs)
    - 有关 _SMSTSLogPath 和其他有用变量的详细信息，请参阅[任务序列内置变量](/sccm/osd/understand/task-sequence-built-in-variables)

- **运行诊断工具**：若要运行其他诊断工具，请在此组中添加步骤。 这些工具应在出现故障后尽可能快地自动收集系统中的其他信息。
    - 其中一个工具是 Windows [SetupDiag](/windows/deployment/upgrade/setupdiag)。 它是一个独立的诊断工具，可用于获取有关 Windows 10 升级失败原因的详细信息。
         - 在 Configuration Manager 中，[创建工具包](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program)。
         - 向该组任务序列添加[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。 使用“包”  选项来引用该工具。 以下字符串是一个示例命令行  ：  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>与客户端一起安装的 CMTrace
<!--1357971-->

CMTrace 日志查看工具现自动与 Configuration Manager 客户端一起安装。 它被添加到客户端安装目录，默认情况下为 `%WinDir%\ccm\cmtrace.exe`。

> [!Note]  
> CMTrace *不会*自动注册 Windows 以打开 .log 文件扩展名。



## <a name="improvement-to-the-configuration-manager-console"></a>对 Configuration Manager 控制台的改进
<!--1358202-->
我们已对 Configuration Manager 控制台进行了以下改进：

- 现在，“资产和符合性”、“设备”下的设备列表默认显示当前登录用户。 此值与[客户端状态](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus)同步保持最新。 当用户注销时，将清除该值。 如果没有用户登录，则值为空。 

### <a name="known-issues"></a>已知问题
当前登录用户值在“设备”节点中为空，或者在查看“设备集合”节点下的设备列表时为空。 若要解决此问题，请下载此 [SQL 脚本](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c)。 在站点数据库服务器上，运行 sp_BgbUpdateLiveData.sql，然后重启管理点上的 smsexec 和 sms_notification_server 服务。<!--514471-->



## <a name="improvements-to-console-feedback"></a>对控制台反馈的改进
<!--1357542-->
此版本包含对 Configuration Manager 控制台中新[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)机制的以下改进：  

- 反馈对话框现在会记住以前的设置，例如选择的选项和电子邮件地址。  

- 它现在支持脱机反馈。 从控制台保存反馈，然后通过连接 internet 的系统上传到 Microsoft。 使用位于 `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe` 中的新脱机反馈上载程序工具。 若要查看可用和所需的命令行选项，使用 `--help` 选项运行工具。 已连接的系统需要访问 **petrol.office.microsoft.com**。

### <a name="known-issues"></a>已知问题
在连接 Internet 的计算机上的控制台内使用“发送笑脸”  或“发送苦脸”  时，可能会看到以下返回消息：“发送反馈时出错了”。 如果单击“更多详细信息”  ，它将显示以下文本：`{"Message":""}`。 此错误是由后端反馈系统中的响应的已知问题所导致的。 可以忽略此错误。 Microsoft 仍会收到你的反馈。 （如果详细信息显示其他消息，请使用脱机反馈选项在稍后重试发送反馈的步骤。）



## <a name="improvements-to-pxe-enabled-distribution-points"></a>对已启用 PXE 的分发点的改进
<!--1357580-->

使用分发点上的选项[**在没有 Windows 部署服务的情况下启用 PXE 响应程序**](/sccm/core/get-started/capabilities-in-technical-preview-1802#improvements-to-pxe-enabled-distribution-points)时，此版本包括以下其他改进：  

- 启用此选项时，会在分发点上自动创建 Windows 防火墙规则  
- 对组件日志记录的改进



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>对大整数值硬件清单的改进
<!--1357880-->
硬件清单当前对大于 4,294,967,296 (2^32) 的整数设定了限制。 对于诸如以字节为单位的硬盘大小之类的属性，可以达到此限制。 管理点不会处理超过此限制的整数值，因此数据库中不会存储任何值。 现在，此版本中的限制增加到了 18,446,744,073,709,551,616 (2^64)。 

对于值不变的属性（如总磁盘大小），可能在升级站点后不会立即看到值。 大多数硬件清单为增量报表。 客户端仅发送更改的值。 若要解决此行为，请将另一个属性添加到同一个类。 此操作会导致客户端更新已更改类中的所有属性。 



## <a name="improvement-to-wsus-maintenance"></a>WSUS 维护改进
<!--1357898-->

根据取代规则，WSUS 清理向导现拒绝已过期或被取代的更新。 这些规则在软件更新点组件属性中定义。

### <a name="try-it-out"></a>试试看！
尝试完成任务。 然后发送[反馈](capabilities-in-technical-preview-1804.md#bkmk_feedback)，以便我们了解其运作状况。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“站点配置”  并选择“站点”  。 选择顶层站点，单击功能区中的“配置站点组件”  ，然后选择“软件更新点”  。  

2. 切换到“取代规则”  选项卡。启用到选项“运行 WSUS 清理向导”  。 指定所需的取代行为。  

3. 查看 WSyncMgr.log 文件。



## <a name="improvement-to-support-for-cng-certificates"></a>对 CNG 证书支持的改进
<!--1357314-->
在此版本中，[CNG 证书](/sccm/core/plan-design/network/cng-certificates-overview)将用于下列其他已启用 HTTPS 的服务器角色：  
- 证书注册点，包括具有 Configuration Manager 策略模块的 NDES 服务器



## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
