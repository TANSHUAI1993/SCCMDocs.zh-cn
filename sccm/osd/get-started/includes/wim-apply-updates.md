---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: 1f809ca6499b502520a7662d9947f0799369bef2
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67534566"
---
## <a name="BKMK_OSImagesApplyUpdates"></a> 将软件更新应用于映像

> [!Note]  
> 本部分适用于“OS 映像”和“OS 升级包”   。 它使用通用术语“映像”来指代 Windows 映像文件 (WIM)。 这两个对象都具有包含 Windows 安装文件的 WIM。 软件更新适用于这两个对象中的文件。 此过程的行为在两个对象之间是相同的。  

每个月都有适用于该映像的新软件更新。 在向其应用软件更新之前，需要满足以下先决条件：

- 软件更新基础结构  
- 成功同步软件更新  
- 将软件更新下载到站点服务器上的内容库  

有关详细信息，请参阅[部署软件更新](/sccm/sum/deploy-use/deploy-software-updates)。  

根据指定的计划将适用的软件更新应用于映像。 此过程有时称为脱机服务  。 在此计划中，Configuration Manager 将选定的软件更新应用于映像。 然后，它还可以将更新的映像重新分发到分发点。

> [!Important]  
> 尽管可以根据版本选择适用于映像的任何软件更新，但 DISM 只能对映像应用某些类型的更新。 **OfflineServicingMgr.log** 文件显示以下条目：`Not applying this update binary, it is not supported`。<!-- SCCMDocs issue 1324 -->

站点数据库存储有关映像的信息，包括导入时应用的软件更新。 自映像最初添加以来已应用于映像的软件更新也存储在站点数据库中。 当启动向导以应用软件更新时，它将检索该站点尚未应用于映像的适用软件更新列表。 Configuration Manager 复制从站点服务器上的内容库中选择的软件更新。 然后，将软件更新应用于映像。  

### <a name="servicing-process"></a>维护过程

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统映像”或“操作系统升级包”     。  

2. 选择要向其应用软件更新的对象。  

3. 在功能区中，选择“计划更新”以启动向导  。  

4. 在“选择更新”页上，选择要应用于映像的软件更新  。 可能需要一些时间才能在向导中显示更新列表。 使用“筛选器”搜索元数据中的字符串  。 使用“系统体系结构”下拉列表筛选 X86、X64 或“全部”     。 可在列表中选择一个、多个或所有更新。 选择完更新后，选择“下一步”  。  

5. 在“设置计划”  页上，指定以下设置，然后单击“下一步”  。  

    1. **计划**：指定站点将软件更新应用于映像的时间表。  

    2. **出错时继续**：选择此选项以便即使在出错时也继续将软件更新应用于映像。  

    3. **使用映像更新分发点**：选择此选项可在站点应用软件更新后更新分发点上的映像。  

6. 完成计划更新向导。  

> [!NOTE]  
> 为了最大程度减少有效负载大小，OS 升级包和 OS 映像的维护过程将删除旧版本。  

### <a name="servicing-operations"></a>维护操作

在 Configuration Manager 控制台的“OS 映像”或“OS 升级包”节点中，将以下列添加到视图中   ：

- **计划的更新日期**：此属性显示已定义的下一个计划。  
- **计划的更新状态**：此属性显示状态。 例如，“成功”或“正在处理”   。  

选择特定的映像对象，然后切换到结果窗格中的“更新状态”选项卡  。 此选项卡显示映像中的更新列表。

选择特定映像对象，然后在功能区中选择“属性”  。 “已安装的更新”选项卡显示映像中的更新列表  。 “服务”选项卡是当前服务计划和你计划应用的更新的只读视图  。

当状态为“正在处理”时，可在功能区上选择“取消计划的更新”   。 此操作将取消活动的服务过程。

要对此过程进行故障排除，请查看站点服务器上的 OfflineServicingMgr.log 和 dism.log 文件   。 有关详细信息，请参阅[日志文件](/sccm/core/plan-design/hierarchy/log-files)。

### <a name="bkmk_servicing-drive"></a> 指定用于为脱机 OS 映像提供服务的驱动器

<!--1358924-->

从版本 1810 开始，指定 Configuration Manager 在 OS 映像的脱机服务期间使用的驱动器。 此进程可能会占用临时文件的大量磁盘空间。 此选项使你可以灵活地选择要使用的驱动器。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。 在功能区中，单击“配置站点组件”，然后选择“操作系统部署”   。  

2. 在“脱机服务”选项卡上，为“映像的脱机服务所使用的本地驱动器”指定选项   。  

默认情况下，此设置为“自动”  。 Configuration Manager 使用此值来选择安装它的驱动器。

如果选择站点服务器上不存在的驱动器，则 Configuration Manager 的行为与选择“自动”时的行为相同  。

在脱机服务期间，Configuration Manager 将临时文件存储在文件夹 `<drive>:\ConfigMgr_OfflineImageServicing` 中。 它还会将 OS 映像装载在此文件夹中。

### <a name="bkmk_resetbase"></a>经优化的映像维护

<!--3555951-->

从版本 1902 开始，向 OS 映像应用软件更新时，具有通过删除任何被取代更新来优化输出的新选项。 脱机维护优化仅适用于具有单个索引的映像。

当安排站点以向 OS 映像应用软件更新时，它使用 Windows 部署映像服务和管理 (DISM) 命令行工具。 在维护过程中，此更改引入了以下两个附加步骤：  

- 它使用参数 `/Cleanup-Image /StartComponentCleanup /ResetBase` 针对已装载脱机映像运行 DISM。 如果此命令失败，则当前的维护过程失败。 它不会向映像提交任何更改。  

- Configuration Manager 向映像提交更改并从文件系统中将其卸载后，它会将映像导出到另一个文件。 此步骤使用 DISM 参数 `/Export-Image`。 它将从映像中删除不需要的文件，从而减少大小。  

Microsoft 建议定期向脱机映像应用更新。 无需在每次维护映像时均使用此选项。 每月执行此过程时，随时间的推移，使用此新选项将为你提供最大优势。 有关详细信息，请参阅[有关“安装软件更新”步骤的建议](/sccm/osd/understand/install-software-updates#recommendations)。

虽然此选项可帮助减少维护映像的总体大小，但完成此过程确实会花费更长时间。 使用向导，计划在方便的时间进行维护。 它还需要站点服务器上的附加存储。 可以自定义站点，以使用备用位置。 有关详细信息，请参阅[指定用于为脱机 OS 映像提供服务的驱动器](#bkmk_servicing-drive)。

#### <a name="process-to-optimize-image-servicing"></a>优化映像维护的过程

1. 开始[维护过程](#servicing-process)。  

2. 在“设置计划”页上，选择“更新映像后删除被取代的更新”选项   。 不会自动启用此选项。 如果映像具有多个索引，则不能使用此选项。  

3. 若要计划映像维护，请完成此向导。  

使用 **OfflineServicing.log** 验证并监视此过程。
