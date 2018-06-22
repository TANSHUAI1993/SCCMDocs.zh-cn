---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: 了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1802 中的可用功能。
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c960ee37e5f4b7b3b644afd06a04c2747cc1f1eb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343215"
---
# <a name="capabilities-in-technical-preview-1802-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1802 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了适用于 System Center Configuration Manager 的 Technical Preview 版本 1802 中的可用功能。 你可以安装此版本，以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 

在安装此版本的 Technical Preview 之前，请查看[适用于 System Center Configuration Manager 的 Technical Preview](/sccm/core/get-started/technical-preview)。 该文章将帮助你熟悉使用 Technical Preview 的常规要求和限制，如何在版本之间进行更新以及如何提供相关的反馈。     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>此 Technical Preview 中的已知问题
-   如果站点服务器处于被动模式，则无法更新到新的预览版本。 如果具有[被动模式的主站点服务器](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)，那么在更新到此新的预览版本之前，必须卸载该被动模式站点服务器。 可以在站点完成更新后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在 Configuration Manager 控制台中，依次转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”，再选择被动模式站点服务器。
  2. 在“站点系统角色”窗格中，右键单击“站点服务器”角色，再选择“删除角色”。
  3. 右键单击被动模式站点服务器，再选择“删除”。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE。
<!--sms 489412-->


</br>

**以下是此版本可以试用的新功能。**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>使用共同管理将 Endpoint Protection 工作负荷转移到 Intune    
<!-- 1357365 -->
在此版本中，你现在可以在启用共同管理后，将 Endpoint Protection 工作负荷从 Configuration Manager 转移到 Intune。 若要转移 Endpoint Protection 工作负荷，请转到共同管理属性页，并将滚动条从 Configuration Manager 移动到“试点”或“所有”。 有关详细信息，请参阅[适用于 Windows 10 设备的共同管理](/sccm/core/clients/manage/co-management-overview)。


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>配置 Windows 传递优化以使用 Configuration Manager 边界组
<!-- 1324696 -->
使用 Configuration Manager 边界组来定义和控制跨公司网络和到远程办公室的内容分发。 [Windows 传递优化](/windows/deployment/update/waas-delivery-optimization)是一种基于云的对等技术，用于在 Windows 10 设备之间共享内容。 从此版本开始，配置传递优化以在对等方之间共享内容时使用边界组。 新的客户端设置将边界组标识符用作客户端上的传递优化组标识符。 当客户端与传递优化云服务进行通信时，它使用此标识符来查找具有所需内容的对等方。 

### <a name="prerequisites"></a>先决条件
- 传递优化仅可用于 Windows 10 客户端

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 在 Configuration Manager 控制台中，通过“管理”工作区中的“客户端设置”节点来创建自定义客户端设备设置策略。
2. 选择新的“传递优化”组。
3. 启用设置“将配置管理器边界组用于交付优化组 ID”。

有关详细信息，请参阅[传递优化选项](/windows/deployment/update/waas-delivery-optimization#group-id)中的“组”传递模式选项。



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>通过云管理网关执行的 Windows 10 就地升级任务序列
<!-- 1357149 -->

Windows 10 [就地升级任务序列](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)现在支持部署到通过[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway)托管的基于 Internet 的客户端。 此功能可让远程用户更轻松地升级到 Windows 10，而无需连接公司网络。 

确保就地升级任务序列引用的所有内容均分发到[云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)。 否则设备无法运行任务序列。

在部署升级任务序列时，请使用以下设置：
- 部署“用户体验”选项卡上的“允许任务序列针对 Internet 上的客户端运行”。
- 部署“分发点”选项卡上的“启动任务序列之前本地下载所有内容”。 其他选项如“运行中任务序列需要时，从本地下载内容”在此方案中不起作用。 任务序列引擎当前无法从云分发点获取内容。 启动任务序列之前，Configuration Manager 客户端必须从云分发点下载内容。
- （可选）部署“常规”选项卡上的“此任务序列的预下载内容”。 有关详细信息，请参阅[配置预缓存内容](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)。



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>对 Windows 10 就地升级任务序列的改进
<!-- 1357425 -->
Windows 10 就地升级的默认任务序列模板现在包括在升级过程前后要添加的带建议操作的其他组。 这些操作在许多将设备成功升级到 Windows 10 的客户之间是通用的。 

### <a name="new-groups-under-prepare-for-upgrade"></a>“准备升级”下的新组
- 电池检查：在此组中添加步骤，以检查计算机使用的是电池还是有线电源。 此操作需要自定义脚本或实用工具来执行此检查。
- 网络/有线连接检查：在此组中添加步骤，以检查计算机是否已连接到网络，并且未使用无线连接。 此操作需要自定义脚本或实用工具来执行此检查。
- 删除不兼容的应用程序：在此组中添加步骤，以删除与此版本的 Windows 10 不兼容的任何应用程序。 卸载应用程序的方法不同。 如果应用程序使用 Windows Installer，则从应用程序的 Windows Installer 部署类型属性上的“程序”选项卡中复制“卸载程序”命令行。 然后在此组中添加“运行命令行”步骤，并附加卸载程序命令行。 例如： </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- 删除不兼容的驱动程序：在此组中添加步骤，以删除与此版本的 Windows 10 不兼容的任何驱动程序。
- 删除/暂停第三方安全程序：在此组中添加步骤，以删除或暂停第三方安全程序，如防病毒程序。
   - 如果你使用的是第三方磁盘加密程序，则可以为 Windows 安装程序的加密驱动程序提供 /ReflectDrivers [命令行选项](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。 在此组的任务序列中添加[设置任务序列变量](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)步骤。 将任务序列变量设置为“OSDSetupAdditionalUpgradeOptions”。 将值设置为“/ReflectDriver”，并附加驱动程序的路径。 此[任务序列操作变量](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system)附加了任务序列使用的 Windows 安装程序命令行。 请联系你的软件供应商，以获得有关此进程的任何其他指导。

### <a name="new-groups-under-post-processing"></a>“后处理”下的新组
- 应用基于安装程序的驱动程序：在此组中添加步骤，以从包中安装基于安装程序的驱动程序 (.exe)。
- 安装/启用第三方安全程序：在此组中添加步骤，以安装或启用第三方安全程序，如防病毒程序。 
- 设置 Windows 默认应用和关联：在此组中添加步骤，以设置 Windows 默认应用和文件关联。 首先要准备一台具备所需应用关联的参考计算机。 然后运行以下导出命令行： </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>将 XML 文件添加到包。 然后在此组中添加[运行命令行](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)步骤。 指定包含 XML 文件的包，然后指定以下命令行： </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> 有关详细信息，请参阅[导出或导入默认的应用关联](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)。
- 应用自定义和个性化：在此组中添加步骤以应用“开始”菜单自定义，如组织程序组。 有关详细信息，请参阅[自定义“开始”屏幕](/windows-hardware/manufacture/desktop/customize-the-start-screen)。

### <a name="additional-recommendations"></a>其他建议
- 查看 Windows 文档，以[解决 Windows 10 升级错误](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)。 本文还包含了关于升级过程的详细信息。
- 在默认的“检查准备情况”步骤中，启用“确保最小可用磁盘空间 (MB)”。 对于 32 位 OS 升级包，将值设置为至少 16384 (16 GB)，对于 64 位设置为至少 20480 (20 GB)。 
- 使用 SMSTSDownloadRetryCount [内置任务序列变量](/sccm/osd/understand/task-sequence-built-in-variables)重试下载策略。 当前在默认情况下，客户端重试两次；此变量设置为二 (2)。 如果客户端未连接到有线公司网络，额外的重试将帮助客户端获得策略。 使用该变量不会产生负面的副作用，如果不能下载策略，则会导致延迟失败。<!-- 501016 --> 此外，也可以增加“SMSTSDownloadRetryDelay”变量的值（默认值为 15 秒）。
- 执行内联兼容性评估。 
   - 在“准备升级”组中提前添加第二个“升级操作系统”步骤。 将其命名为“升级评估”。 指定相同的升级包，然后启用选项“不启动升级即执行 Windows 安装程序兼容性扫描”。 启用“选项”选项卡上的“出错时继续”。 
   - 紧跟此“升级评估”步骤，添加“运行命令行”步骤。 指定以下命令行：</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>在“选项”选项卡上，添加以下条件： </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>此返回代码为 MOSETUP_E_COMPAT_SCANONLY (0xC1900210) 的等效十进制数，表示不存在任何问题的成功兼容性扫描。 如果“升级评估”步骤成功并返回此代码，则跳过此步骤。 否则，如果评估步骤返回任何其他返回代码，则此步骤的任务序列将失败，并会从 Windows 安装程序兼容性扫描中返回代码。
   - 有关详细信息，请参阅[升级操作系统](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)。
- 如果要在此任务序列过程中将设备从 BIOS 更改为 UEFI，请参阅[在就地升级过程中从 BIOS 转换为 UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

如果你还有其他建议或意见，请从功能区的“主页”选项卡发送“反馈”。



## <a name="improvements-to-pxe-enabled-distribution-points"></a>对已启用 PXE 的分发点的改进
<!-- 1357580 -->
为阐明 Technical Preview 版本 1706 中首次引入的[新 PXE 功能](/sccm/core/get-started/capabilities-in-technical-preview-1706#pxe-network-boot-support-for-ipv6)，我们对“支持 IPv6”选项进行了更名。 在分发点属性的“PXE”选项卡上，选中“在没有 Windows 部署服务的情况下启用 PXE 响应者”。 

此选项在分发点上启用 PXE 响应者，而不需要 Windows 部署服务 (WDS)。 如果在已启用 PXE 的分发点上启用此新选项，Configuration Manager 将挂起 WDS 服务。 如果禁用此新选项，但仍“为客户端启用 PXE 支持”，分发点将重新启用 WDS。

因为 WDS 不是必需的，因此已启用 PXE 的分发点可以是客户端或服务器操作系统，包括 Windows Server Core。 此新的 PXE 响应者服务继续支持 IPv6，还增强了远程办公室中已启用 PXE 的分发点的灵活性。

> [!NOTE]
> 该服务使用与 Technical Preview 版本 1712 中的[基于客户端的 PXE 响应者服务](/sccm/core/get-started/capabilities-in-technical-preview-1712#client-based-pxe-responder-service)相同的基本技术。 该功能不需要分发点角色的开销。

### <a name="multicast"></a>多播
若要启用和配置分发点属性“多播”选项卡上的多播，分发点必须使用 WDS。 
- 如果你“为客户端启用 PXE 支持”并“启用多播以将数据同时发送到多个客户端”，则无法“在没有 Windows 部署服务的情况下启用 PXE 响应者”。
- 如果你“为客户端启用 PXE 支持”并“在没有 Windows 部署服务的情况下启用 PXE 响应者”，则无法“启用多播以将数据同时发送到多个客户端”



## <a name="deployment-templates-for-task-sequences"></a>任务序列的部署模板
<!-- 1357391 -->
任务序列的部署向导现在可以创建部署模板。 部署模板可以保存并应用到现有或新任务序列以创建部署。 

### <a name="try-it-out"></a>试试看！  
尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。 

 **创建新任务序列部署的部署模板** <br/> 
1. 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”。
2. 右键单击任务序列，然后选择“部署”。 
3. 在“常规”选项卡上，请注意现在有一个“选择部署模板”的选项。 
4. 选择任务序列的部署设置，继续完成“部署软件向导”。 
5. 在访问“部署软件向导”的“摘要”选项卡时，单击“另存为模板”。
6. 为模板指定一个名称，然后选择要保存在模板中的设置。 
7. 单击“保存” 。 现在可通过“选择部署模板”选项来使用模板。



## <a name="product-lifecycle-dashboard"></a>产品生命周期仪表板
<!--1319632-->
新的[产品生命周期仪表板](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard)显示在由 Configuration Manager 托管的设备上安装的 Microsoft 产品的 Microsoft 产品生命周期策略的状态。 仪表板为你提供有关环境中 Microsoft 产品的信息、可支持性状态以及支持结束日期。 可以使用仪表板来了解对每个产品的支持的可用性。 

若要访问生命周期仪表板，请在 Configuration Manager 控制台中，转到“资产和符合性” >“资产智能” >”产品生命周期”



## <a name="improvements-to-reporting"></a>报表改进
<!--1357653-->
根据[你的反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and)，我们添加了新的报表“特定集合的 Windows 10 服务详细信息”。 此报表显示 Windows 10 设备的资源 ID、NetBIOS 名称、OS 名称、OS 版本名称、内部版本、OS 分支和服务状态。 若要访问此报表，请转到“监视” >“报告” >“报表” >“操作系统” >“特定集合的 Windows 10 服务详细信息”。



## <a name="improvements-to-software-center"></a>对软件中心的改进
<!--1357592-->
根据[你的反馈](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid)，安装的应用程序现在可以在软件中心中隐藏。 启用此选项后，已安装的应用程序将不再显示在“应用程序”选项卡中。 

### <a name="try-it-out"></a>试试看！
在软件中心客户端设置中，启用“在软件中心隐藏已安装的应用程序”设置。 在最终用户安装应用程序时，请观察软件中心上的行为。



## <a name="improvements-to-run-scripts"></a>运行脚本的改进
<!--1236459-->
[运行脚本](/sccm/apps/deploy-use/create-deploy-scripts)功能现在可返回使用 JSON 格式的脚本输出。 此格式一致返回可读的脚本输出。 无法运行的脚本可能无法返回输出。 



## <a name="boundary-group-fallback-for-management-points"></a>管理点的边界组回退
<!-- 1324594 -->
从此版本开始，你可以在[边界组](/sccm/core/servers/deploy/configure/boundary-groups)之间配置管理点的回退关系。 此行为可以更好地控制客户端使用的管理点。 在边界组属性的“关系”选项卡上，有一个管理点新列。 在添加新回退边界组时，当前管理点的回退时间始终为零 (0)。 对于站点默认边界组上的“默认行为”，此行为是相同的。

在此之前，当安全网络中有一个受保护的管理点，会出现一个常见问题。 主要公司网络上的客户端接收策略，其中包括此受保护的管理点，即使它们无法通过防火墙与管理点进行通信。 若要解决此问题，请使用“从不回退”选项，以确保客户端仅回退到它们可以与之通信的管理点。

当站点升级到此版本时，Configuration Manager 会将所有非面向 Internet 的管理点添加到站点默认边界组。 此升级行为可确保旧版客户端继续与管理点通信。 若要充分利用此功能，请将管理点移到所需的边界组。

在客户端安装 (ccmsetup) 过程中，管理点边界组回退不会更改行为。 如果命令行未使用 /MP 参数指定初始管理点，新的客户端将收到完整的可用管理点列表。 在其初始启动过程中，客户端使用它可以访问的第一个管理点。 一旦客户端注册站点，它便会收到通过此新行为正确排序的管理点列表。 

### <a name="prerequisites"></a>先决条件
- 启用[首选管理点](/sccm/core/servers/deploy/configure/boundary-groups#preferred-management-points)。 在 Configuration Manager 控制台中，转到“管理”工作区。 展开“站点配置”并选择“站点”。 单击功能区中的“层次结构设置”。 在“常规”选项卡上，启用“客户端更愿意使用边界组中指定的管理点”。 

### <a name="known-issues"></a>已知问题
- 操作系统部署进程不知道边界组。

### <a name="troubleshooting"></a>故障排除
在“LocationServices.log”中出现新条目。 “Locality”属性标识以下状态之一：
- 0：未知
- 1：指定管理点仅在回退的站点默认边界组中
- 2：指定管理点位于远程或相邻边界组中。 当相邻和站点默认边界组中都存在管理点时，locality 为 2。
- 3：指定管理点位于本地或当前边界组中。 如果当前边界组以及相邻或站点默认边界组中均存在管理点，locality 为 3。 如果在“层次结构设置”中未启用首选管理点设置，locality 始终为 3，而不考虑管理点位于哪个边界组。

客户端首先使用本地管理点 (locality 3)，第二个为远程管理点 (locality 2)，然后使用回退 (locality 1)。 

如果客户端在十分钟内收到五个错误，并且无法与当前边界组中的管理点进行通信，它将尝试联系相邻或站点默认边界组中的管理点。 如果当前边界组中的管理点稍后重新联机，客户端将在下一个刷新周期返回到本地管理点。 刷新周期为 24 小时，或当 Configuration Manager 代理服务重新启动时。



## <a name="improved-support-for-cng-certificates"></a>改进了对 CNG 证书的支持
<!-- 1357314 -->
Configuration Manager（当前分支）版本 1710 支持[下一代加密技术 (CNG) 证书](/sccm/core/plan-design/network/cng-certificates-overview)。 版本 1710 在多种方案中对客户端证书提供有限支持。 

从此 Technical Preview 版本开始，CNG 证书将用于以下已启用 HTTPS 的服务器角色：
- 管理点
- 分发点
- 软件更新点

[不支持方案](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios)列表保持不变。



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>云管理网关支持 Azure 资源管理器
<!-- 1324735 -->
在创建[云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG) 实例时，向导现提供选项来创建“Azure 资源管理器部署”。 [Azure 资源管理器](/azure/azure-resource-manager/resource-group-overview)是一个现代平台，用于以单个实体（称为[资源组](/azure/azure-resource-manager/resource-group-overview#resource-groups)）的方式来管理所有解决方案资源。 如果在 Azure 资源管理器中部署 CMG，站点将使用 Azure Active Directory (Azure AD) 进行身份验证并创建必要的云资源。 此现代化部署不需要经典 Azure 管理证书。  

CMG 向导仍提供使用 Azure 管理证书的“经典服务部署”选项。 若要简化资源的部署和管理，我们建议为所有新的 CMG 实例使用 Azure 资源管理器部署模型。 如果可以，请通过资源管理器重新部署现有 CMG 实例。

Configuration Manager 不会将现有经典 CMG 实例迁移到 Azure 资源管理器部署模型。 使用 Azure 资源管理器部署创建新的 CMG 实例，然后删除经典 CMG 实例。 

> [!IMPORTANT]
> 此功能不提供对 Azure 云服务提供商 (CSP) 的支持。 Azure 资源管理器中的 CMG 部署将继续使用 CSP 不支持的经典云服务。 有关详细信息，请参阅 [Azure CSP 中可用的 Azure 服务](/azure/cloud-solution-provider/overview/azure-csp-available-services)。  

### <a name="prerequisites"></a>先决条件
- 与 [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure) 集成。 不需要 Azure AD 用户发现。
- [云管理网关要求](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway)相同，除了 Azure 管理证书。

### <a name="try-it-out"></a>试试看！  
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后选择“云管理网关”。 单击功能区中的“创建云管理网关”。 
2. 在“常规”页上，选择“Azure 资源管理器部署”。 单击“登录”以使用 Azure 订阅管理员帐户进行身份验证。 该向导使用集成先决条件过程中存储的 Azure AD 订阅信息，自动填充其余字段。 如果拥有多个订阅，请选择要使用的所需订阅。 单击“下一步” 。  
3. 在“设置”页上，像往常一样提供服务器 PKI 证书文件。 此证书在 Azure 中定义 CMG 服务名称。 选择“区域”，然后选择资源组选项“新建”或“使用现有”。 输入新的资源组名称，或从下拉列表中选择现有资源组。 
4. 完成向导。

> [!NOTE] 
> 对于所选的 Azure AD 服务器应用，Azure 将分配订阅“参与者”权限。 

使用服务连接点上的“cloudmgr.log”来监视服务部署进度。



## <a name="approve-application-requests-for-users-per-device"></a>审批每台设备的用户的应用程序请求
<!-- 1357015 -->
从此版本开始，当用户请求需要审批的应用程序时，特定设备名称现为请求的一部分。 如果管理员批准请求，则用户只能在该设备上安装应用程序。 用户必须提交另一个请求才能在另一台设备上安装应用程序。 

> [!NOTE]
> 此功能为可选。 更新到此版本时，在更新向导中启用此功能。 或者，稍后在控制台中启用该功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。

### <a name="prerequisites"></a>先决条件
- 将 Configuration Manager 客户端升级到最新版本
- 在[计算机代理](/sccm/core/clients/deploy/about-client-settings#computer-agent)组中启用客户端设置“使用新的软件中心”

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 将应用程序以可用的方式部署到用户集合。
2. 在“部署设置”页上，启用选项：“管理员必须批准对设备上的此应用程序的请求”。
3. 作为目标用户，请使用软件中心提交应用程序请求。 
4. 在 Configuration Manager 控制台的“软件库”工作区中，查看“应用程序管理”下的“批准请求”。 每个请求的列表现均提供“设备”列。 当针对此请求执行操作时，“应用程序请求”对话框还将包括用户从中提交请求的设备名称。



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>在已加入 Azure AD 的设备上，使用软件中心来浏览和安装用户可用的应用程序
<!-- 1322613 -->
如果将应用程序以可用的方式部署到用户，则他们现在可以通过 Azure Active Directory (Azure AD) 设备上的软件中心浏览和安装应用程序。  

### <a name="prerequisites"></a>先决条件
- 在管理点上启用 HTTPS
- 将站点与 [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure) 集成
- 将应用程序以可用的方式部署到用户集合
- 将任何应用程序内容分发到[云分发点](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- 在[计算机代理](/sccm/core/clients/deploy/about-client-settings#computer-agent)组中启用客户端设置“使用新的软件中心”
- 客户端必须满足下列要求： 
   - Windows 10
   - 已加入 Azure AD，也称为已加入云域
- 若要支持基于 Internet 的客户端：
    - [云管理网关](/sccm/core/clients/manage/plan-cloud-management-gateway) 
    - 启用客户端设置：[客户端策略](/sccm/core/clients/deploy/about-client-settings#client-policy)组中的“从 Internet 客户端启用用户策略请求”
- 若要在企业网络上支持客户端：
    - 将云分发点添加到客户端使用的边界组
    - 客户端必须能够解析已启用 HTTPS 的管理点的完全限定的域名 (FQDN)



## <a name="report-on-windows-autopilot-device-information"></a>关于 Windows AutoPilot 设备信息的报表
<!-- 1351442 -->
Windows AutoPilot 是以现代方式载入和配置新 Windows 10 设备的一种解决方案。 有关详细信息，请参阅 [Windows AutoPilot 概述](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)。 向 Windows AutoPilot 注册现有设备的一种方法是，将设备信息上传到 Microsoft Store 商业版和教育版。 此信息包括设备序列号、Windows 产品标识符和硬件标识符。 使用 Configuration Manager 收集和报告此设备信息。 

### <a name="prerequisites"></a>先决条件
- 此设备信息仅适用于 Windows 10 版本 1703 及更高版本上的客户端

### <a name="try-it-out"></a>试试看！
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

1. 在 Configuration Manager 控制台中的“监视”工作区中，展开“报告”节点，展开“报表”，然后选择“硬件 - 常规”节点。
2. 运行新的报表“Windows AutoPilot 设备信息”并查看结果。 
3. 在报表查看器中，单击“导出”图标，并选择“CSV （逗号分隔）”选项。
4. 在保存该文件后，将数据上传到 Microsoft Store 商业版和教育版。 有关详细信息，请参阅[在 Microsoft Store 商业版和教育版中添加设备](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile)。 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>对 Configuration Manager 的 Windows Defender 攻击防护策略的改进
<!-- 1356220 -->
在 Configuration Manager 中，为 [Windows Defender 攻击防护](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard)添加了有关攻击面减少和受控文件夹访问权限组件的其他策略设置。

**受控文件夹访问权限的新设置**<br/>
在配置受控文件夹访问权限时，有两个附加选项：“仅阻止磁盘扇区”和“仅审核磁盘扇区”。 这两个设置允许仅为引导扇区启用受控文件夹访问权限，而不启用对特定文件夹或默认受保护文件夹的保护。 

**攻击面减少的新设置**
- 对勒索软件启用高级防护。
- 阻止从 Windows 本地安全机构子系统中窃取凭据。 
- 阻止运行可执行文件，除非它们符合传播、年龄或受信任列表条件。 
- 阻止从 USB 运行不受信任和未签名的进程。



## <a name="microsoft-edge-browser-policies"></a>Microsoft Edge 浏览器策略
<!-- 1357310 -->
对于在 Windows 10 客户端上使用 [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web 浏览器的客户，现在可以创建 Configuration Manager 符合性设置策略，以配置多个 Microsoft Edge 设置。 此策略当前包括以下设置：
- 将 Microsoft Edge 浏览器设置为默认浏览器：将 Web 浏览器的 Windows 10 默认应用设置配置为 Microsoft Edge
- 允许地址栏下拉列表：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [AllowAddressBarDropdown 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)。
- 允许在 Microsoft 浏览器之间同步收藏夹：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [SyncFavoritesBetweenIEAndMicrosoftEdge 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)。
- 允许在退出时清除浏览数据：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [ClearBrowsingDataOnExit 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)。
- 允许使用 Do Not Track 标头：有关详细信息，请参阅 [AllowDoNotTrack 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)。
- 允许自动填充：有关详细信息，请参阅 [AllowAutofill 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)。
- 允许使用 Cookie：有关详细信息，请参阅 [AllowCookies 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)。
- 允许使用弹出窗口阻止程序：有关详细信息，请参阅 [AllowPopups 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)。
- 允许在地址栏中显示搜索建议：有关详细信息，请参阅 [AllowSearchSuggestionsinAddressBar 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)。
- 允许将 Intranet 流量发送到 Internet Explorer：有关详细信息，请参阅 [SendIntranetTraffictoInternetExplorer 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)。
- 允许使用密码管理器：有关详细信息，请参阅 [AllowPasswordManager 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)。
- 允许使用开发人员工具：有关详细信息，请参阅 [AllowDeveloperTools 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)。
- 允许使用扩展：有关详细信息，请参阅 [AllowExtensions 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)。

### <a name="prerequisites"></a>先决条件
- 已加入 Azure Active Directory 的 Windows 10 客户端。 

### <a name="known-issues"></a>已知问题
- 本地已加入域的设备无法在此版本中应用该策略。 该问题也适用于已加入混合域的设备。

### <a name="try-it-out"></a>试试看！  
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。

**创建策略**
1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区。 展开“符合性设置”，并选择新的“Microsoft Edge 浏览器配置文件”节点。 单击“创建 Microsoft Edge 浏览器策略”的功能区选项。
2. 指定策略“名称”，根据需要输入“说明”，然后单击“下一步”。
3. 在“设置”页上，将设置值更改为“已配置”以包括在此策略中，然后单击“下一步”。
4. 在“支持的平台”页上，选择要在其中应用此策略的操作系统版本和体系结构，并单击“下一步”。 
5. 完成向导。

**部署策略**
1. 选择策略，然后单击功能区选项“部署”。
2. 单击“浏览”以选择要在其中部署策略的用户或设备集合。 
3. 根据需要选择其他选项。 当策略不合规时生成警报。 设置客户端评估设备与此策略符合性所依据的计划。
4. 单击“确定”创建部署。

就像任何符合性设置策略，客户端会修正指定计划的设置。 在 Configuration Manager 控制台中[监视和报告设备合规性](/sccm/compliance/deploy-use/monitor-compliance-settings)。



## <a name="report-for-default-browser-counts"></a>默认浏览器计数报表
<!-- 1357830 -->
现在提供了一个新报表来显示将特定 Web 浏览器作为 Windows 默认浏览器的客户端计数。 

### <a name="known-issues"></a>已知问题
- 在首次打开报表时，它只显示计数而不显示 BrowserProgID。 若要解决此问题，可以将报表查询编辑为以下语法：  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>试试看！  
 尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。
1. 在“Configuration Manager”控制台的“监视”工作区中，展开“报告”，展开“报表”，选择“软件 - 公司和产品”。
2. 运行“默认浏览器计数”报表。

对于常见 BrowserProgIDs，请使用以下引用：
- AppXq0fevzme2pys62n3e0fbqa7peapykr8v：Microsoft Edge
- IE.HTTP：Microsoft Internet Explorer
- ChromeHTML：Google Chrome
- OperaStable：Opera Software
- FirefoxURL-308046B0AF4A39CB：Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Windows 10 ARM64 设备支持
<!-- 1353704 -->
从此版本开始，Windows 10 ARM64 设备将支持 Configuration Manager 客户端。 现有客户端管理功能应适用于这些新设备。 例如，硬件和软件清单、软件更新和应用程序管理。 当前不支持操作系统部署。 

## <a name="changes-to-phased-deployments"></a>分阶段部署的更改
<!-- 1357405 -->
分阶段部署可在多个集合中自动协调有序地推出软件。 在此 Technical Preview 版本中，可针对管理控制台中的任务序列完成分阶段部署向导并创建部署。 但是，在满足第一阶段的成功条件后，第二个阶段不会自动启动。 第二个阶段可通过 SQL 语句手动启动。   

### <a name="try-it-out"></a>试试看！  
  尝试完成任务。 然后从功能区的“主文件夹”选项卡发送“反馈”，让我们了解其效果。
 
**针对任务序列创建分阶段部署** </br>
1. 在“软件库”工作区中，展开“操作系统”，并选择“任务序列”。
2. 右键单击现有任务序列并选择“创建分阶段部署”。 
3. 在“常规”选项卡上，为分阶段部署提供名称、说明（可选），并选择“自动创建默认的二阶段部署”。 
4. 填充“第一个集合”和“第二个集合”字段。 选择“下一步”。
5. 在“设置”选项卡上，为每个计划设置选择一个选项，然后在完成后选择“下一步”。 
6. 在“阶段”选项卡上，如果需要，可编辑其中任一阶段，然后单击“下一步”。
7. 在“摘要”选项卡上确认所选，然后单击“下一步”以继续操作。
8. 当已达到第一阶段的成功条件时，按照说明通过 SQL 语句启动第二个阶段。
 
**使用 SQL 语句启动第二个阶段**
1. 使用以下 SQL 查询标识所创建的部署的 PhasedDeploymentID：<br/> `Select * from PhasedDeployment`
2. 运行以下语句启动生产阶段：<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
