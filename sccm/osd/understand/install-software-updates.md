---
title: 安装软件更新
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 任务序列步骤“安装软件更新”的建议。
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6699b73bd9a3a911fef788f25cbf2140e90cbe92
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355053"
---
# <a name="install-software-updates"></a>安装软件更新

*适用范围：System Center Configuration Manager (Current Branch)*

通常，会在 Configuration Manager 任务序列中使用“安装软件更新”  步骤。 安装或更新 OS 时，它会触发软件更新组件以扫描和部署更新。 某些客户在执行此步骤时可能会遇到问题，例如长时间超时延迟或错过更新。 使用本文中的信息有助于解决此步骤中的常见问题，并且更易于在出现问题时进行故障排除。

有关此步骤的详细信息，请参阅[安装软件更新](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>建议

为成功执行此过程，请使用下面的建议内容：

- [使用离线维护](#use-offline-servicing)
- [单一索引](#single-index)
- [减小映像大小](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>使用离线维护

使用 Configuration Manager 定期将适用的软件更新安装到映像文件。 这种做法可以减少在任务序列期间需要安装的更新数量。

有关详细信息，请参阅[将软件更新应用到映像](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates)。

### <a name="single-index"></a>单一索引

许多映像文件包含多个索引，如适用于不同版本的 Windows。 可以将映像文件缩减为需要的单个索引。 这种做法减少了将软件更新应用到映像的时间。 它还实现了下一个建议：减小映像大小。

从版本 1902 开始，在向站点添加 OS 映像时自动执行此过程。 有关详细信息，请参阅[添加 OS 映像](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages)。<!--3719699-->

### <a name="bkmk_resetbase"></a>减小映像大小

向映像应用软件更新时，可以通过删除任何被取代的更新来优化输出。 使用 DISM 命令行工具，例如：

```
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

从版本 1902 开始，有新选项可用于自动执行此过程。 有关详细信息，请参阅[经优化的映像维护](/sccm/osd/get-started/manage-operating-system-images#bkmk_resetbase)。<!--3555951-->


## <a name="image-engineering-decisions"></a>映像工程决策

在设计映像过程时，有几个选项可能会影响软件更新的安装：

- [定期重新捕获映像](#bkmk_goldimage)  
- [使用离线维护](#bkmk_offline)  
- [仅使用默认映像](#bkmk_installwim)

### <a name="bkmk_goldimage"></a>定期重新捕获映像

定期捕获自定义 OS 映像是一个自动执行的过程。 此捕获任务序列将安装最新的软件更新。 这些更新可以包括累积更新、非累积更新和其他关键更新，如服务堆栈更新 (SSU)。 部署任务序列在捕获后安装任何其他更新。

有关此过程的详细信息，请参阅[创建用于捕获 OS 的任务序列](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)。

#### <a name="advantages"></a>优点

- 减少了每个客户端在部署时应用的更新，从而节省了部署过程所需的时间和带宽
- 减少了担心导致重启的更新
- 为组织提供自定义的映像
- 减少了部署时所需的变量

#### <a name="disadvantages"></a>缺点

- 增加了创建和捕获映像的时间（即使该操作主要是自动执行的）
- 增加了将映像分发到分发点的时间，这可以被视为活动部署的中断
- 通过预生产环境进行测试的时间可能比 OS 修补周期要长，这可能使更新的映像无足轻重


### <a name="bkmk_offline"></a>使用离线维护

安排 Configuration Manager 将软件更新应用到映像。

有关详细信息，请参阅[将软件更新应用到映像](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates)。

#### <a name="advantages"></a>优点

- 减少了每个客户端在部署时应用的更新，从而节省了部署过程所需的时间和带宽
- 减少了担心导致重启的更新
- 可以计划现场维护流程

#### <a name="disadvantages"></a>缺点

- 手动选择更新
- 增加了将映像分发到分发点的时间
- 仅支持基于 CBS 的更新。 无法应用 Office 更新

> [!Tip]  
> 可以使用 PowerShell 自动选择软件更新。 使用 [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) cmdlet 获取更新列表。 然后，使用 [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) cmdlet 创建离线维护计划。 以下示例介绍了一种自动执行此操作的方法：
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="bkmk_installwim"></a>仅使用默认映像

在部署任务序列中使用默认的 Windows install.wim 映像文件。

#### <a name="advantages"></a>优点

- 已知来源可靠，可降低可能出现的映像损坏风险
- 消除了映像可能被修改的问题

#### <a name="disadvantages"></a>缺点

- 部署期间可能会进行大量更新
- 增加了每台设备的部署时间
- 可能没有必需的自定义设置，需要执行额外的任务序列步骤来自定义



## <a name="flowchart"></a>流程图

此流程图显示了在任务序列中加入“安装软件更新”步骤的过程。

[以完整尺寸查看关系图](media/ts-step-install-software-updates.svg)

![“安装软件更新”任务序列步骤的流程图](media/ts-step-install-software-updates.svg)  

1. **在客户端上启动的流程**：在客户端上运行的任务序列包括“安装软件更新”步骤。
2. **编译和评估策略**：客户端将所有软件更新策略编译为 WMI RequestedConfigs 命名空间。 (CIAgent.log)
3. *这个实例是第一次被调用吗？*  
    1. **是**：转到“完全扫描”   
    2. **否**：是否为步骤配置了[从缓存扫描结果评估软件更新](/sccm/osd/understand/task-sequence-steps#evaluate-software-updates-from-cached-scan-results)的选项？ 
        1. **是**：转到“从缓存结果扫描” 
        2. **否**：转到“完全扫描” 
4. 扫描过程：完全扫描或从缓存结果扫描，并行执行监视过程。
    1. **完全扫描**：任务序列引擎通过 Update Scan API 调用软件更新代理以执行完全扫描  。 （WUAHandler.log、ScanAgent.log）  
        1. **SUM 代理扫描 - 完全**：通过 Windows 更新代理 (WUA) 执行的常规扫描过程，它与运行 WSUS 的软件更新点进行通信。 它会将任何适用的更新添加到本地更新存储中。 （WindowsUpdate.log、UpdateStore.log）
    2. **从缓存结果扫描**：任务序列引擎通过更新扫描 API 调用软件更新代理以针对缓存的元数据执行扫描。 （WUAHandler.log、ScanAgent.log）
        1. **SUM 代理扫描 - 缓存**：Windows 更新代理 (WUA) 检查已在本地更新存储中缓存的更新。 （WindowsUpdate.log、UpdateStore.log）
    3. **启动扫描计时器**：任务序列引擎启动计时器并等待。 （此过程与完全扫描或从缓存结果扫描的过程并行执行。）
        1. **监视**：任务序列引擎监视 SUM 代理的状态。
        2.  SUM 代理的响应是什么？
            - **正在进行**：计时器是否已达到任务序列变量 [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout) 中的值？ （默认值为 1 小时）
                - **是**：步骤失败。
                - **否**：转到“监视” 
            - **失败**：步骤失败。
            - **完成**：转到“枚举更新列表” 
5. **枚举更新列表**：SUM 代理枚举扫描返回的更新列表，确定哪些是可用更新，哪些是强制更新。
6.  扫描结果列表中是否有任何更新？
    - **是**：转到“安装更新” 
    - **否**：无需安装，步骤成功完成。
7. 部署过程：安装更新过程与部署监视过程并行执行。
    1. **安装更新**：任务序列引擎通过更新部署 API 调用 SUM 代理，以安装所有可用更新，或仅安装强制更新。 此行为取决于步骤的配置，是选择“需要安装 - 仅安装强制软件更新”  ，还是选择“可用于安装 - 所有软件更新”  。 还可以使用 [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget) 变量指定此行为。
        1. **SUM 代理安装**：使用现有缓存更新列表的常规安装过程，具有标准内容下载。 通过 Windows 更新代理 (WUA) 安装更新。 （UpdatesDeployment.log、UpdatesHandler.log、WuaHandler.log、WindowsUpdate.log）
    2. **启动部署计时器并显示进度**：任务序列引擎启动安装计时器，在 TS Progress UI 中以 10% 的间隔显示子进度，然后等待。
        1. **监视**：任务序列引擎轮询 SUM 代理的状态。
        2.  SUM 代理的响应是什么？
            - **正在进行**：安装过程是否已处于非活动状态达 8 小时？ 
                - **是**：步骤失败。
                - **否**：转到“监视” 
            - **失败**：步骤失败。
            - **完成**：转到“是否为步骤配置了‘从缓存扫描结果评估软件更新’的选项？”  


### <a name="timeouts"></a>超时

该关系图包括适用于此步骤的两个超时变量。 其他组件还包含其他可能会影响此过程的标准计时器。

- 更新扫描超时：1 小时 (smsts.log)  
- 位置请求超时：1 小时（LocationServices.log、CAS.log）  
- 内容下载超时：1 小时 (DTS.log)  
- 非活动分发点超时：1 小时（LocationServices.log、CAS.log）  
- 总安装非活动状态超时：8 小时 (smsts.log)  



## <a name="troubleshooting"></a>故障排除

使用以下资源和其他信息来帮助排查此步骤的问题：

- 确保将软件更新部署定位到与任务序列部署相同的集合。  

- 确保在边界组中包含软件更新点。 有关详细信息，请参阅此[Microsoft 支持文章](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager)。  

- 为帮助排查软件更新管理过程的问题，请参阅[软件更新管理疑难解答](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager)。  

- 要帮助提高整体性能，请减小软件更新目录的大小。 例如：  

    - 删除不必要的分类、产品和语言。 有关详细信息，请参阅[配置要同步的分类和产品](/sccm/sum/get-started/configure-classifications-and-products)。  

    - 为站点数据库重新编制索引并重新生成统计信息。 有关详细信息，请参阅 [Configuration Manager 性能和缩放指南白皮书](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e)。  

    - 拒绝不必要的更新，例如：
        - 已取代（从版本 1810 开始，Configuration Manager 会为你执行此操作。 有关详细信息，请参阅[从版本 1810 开始的 WSUS 清理行为](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810)。）
        - Itanium
        - Beta
        - 下一版本
        - ARM
        - 未在部署的 Windows 版本
