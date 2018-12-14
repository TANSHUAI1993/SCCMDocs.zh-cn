---
title: 包转换管理器
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用包转换管理器将包转换为应用程序。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 41dd6ad6f8a0292fdb16a0d727665b17e038f87b
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820035"
---
# <a name="package-conversion-manager"></a>包转换管理器

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1357861-->

从版本 1806 开始，包转换管理器可帮助你将旧的 Configuration Manager 包转换成应用程序。 应用程序会有很多其他好处，诸如依赖关系、要求规则、检测方法和用户设备相关性等。

> [!Tip]  
> 此功能在版本 1806 中作为[预发行功能](/sccm/core/servers/manage/pre-release-features)首次引入。 从版本 1810 开始，此功能不再属于预发行功能。  


一个 Configuration Manager 应用程序包含可部署到客户端设备的文件和程序。 但是，与旧版包和程序不同，应用程序可提供以用户为中心的其他功能。 例如，应用程序可能包含用于软件包、虚拟应用程序包或移动设备应用程序版本的本地安装的部署类型。

有关详细信息，请参阅下列文章： 
- [应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)  
- [包和程序](/sccm/apps/deploy-use/packages-and-programs)  

> [!Important]  
> 如果以前安装了较旧版本的包转换管理器，请在升级站点之前先卸载它。 此集成版本不需要安装，但可能会与现有版本发生冲突。  

此集成版本的包转换管理器适用于 Configuration Manager 当前分支站点中的包。 它不是一个独立的工具。 如果有较旧版本的 Configuration Manager 包和程序，请首先将包迁移到当前分支站点。 有关详细信息，请参阅[在层次结构之间迁移数据](/sccm/core/migration/migrate-data-between-hierarchies)。



## <a name="planning"></a>规划

在开始将包转换为应用程序之前，请先制定计划。 以下举例说明如何制定计划：

- [定义详细的包转换计划](#bkmk_define)  

- [选择和准备待转换的包](#bkmk_prepare)  

- [选择测试包](#bkmk_test)  

- [分析、调查并转换包](#bkmk_analyze)  

- [测试和部署应用程序](#bkmk_deploy)  


### <a name="bkmk_define"></a> 定义详细的包转换计划

本部分介绍两个示例包转换计划：  

- [资源充足的测试环境](#bkmk_define-high)：你拥有的测试环境具有资源、权限和体系结构，可完全复制你的生产环境。  

- [资源受限的测试环境](#bkmk_define-limited)：你拥有的测试环境无法完全复制你的生产环境。  

针对其他特定于环境的问题，请根据需要调整这些计划。

#### <a name="bkmk_define-high"></a> 资源充足的测试环境的示例计划

测试环境包含类似于生产环境的资源、权限和体系结构。 使用测试环境可有效分析和转换所有包，然后测试所有 Configuration Manager 应用程序。 完成该测试工作后，将其转移到生产环境。 

包转换计划可能类似于以下步骤：  

1.  选择你想要转换的包。  

2.  将待转换的包迁移到测试环境。  

3.  准备待转换的包。  

4.  选择测试包。  

5.  分析、调查并转换测试包。  

6.  测试转换后的应用程序。  

7.  分析并转换剩余（非测试）包。  

8.  从测试环境导出应用程序。 将其导入生产环境。  

#### <a name="bkmk_define-limited"></a> 资源受限的测试环境的示例计划

测试环境没有类似于生产环境的资源、权限和体系结构。 无法分析、测试和转换所有包。 在这种方案中，仅可对测试包进行分析、调查、转换和测试。 然后，将剩余的包迁移到生产环境进行分析和转换。 

包转换计划可能类似于以下步骤：

1.  选择你想要转换的包。  

2.  选择测试包。  

3.  将测试包迁移到测试环境。  

4.  准备待转换的测试包。  

5.  分析、调查并转换测试包。  

6.  测试转换后的应用程序。  

7.  从测试环境导出测试应用程序。 然后将其导入生产环境。  

8.  将剩余的包迁移到生产环境并准备用于转换。  

9.  在生产环境中分析、调查并转换剩余的包。  

10. 将剩余的应用程序发布到生产环境。  


### <a name="bkmk_prepare"></a> 选择和准备待转换的包

#### <a name="bkmk_prepare-select"></a> 选择你想要转换的包

并非所有包都适合转换为应用程序。 在开始转换包之前，标识将不会转换的包。 

最适合转换为应用程序的包类型是包含面向用户的软件的包，例如：  

 - Windows Installer 文件（.msi 和 .msu）  

 - Microsoft Application Virtualization (App-V) 程序  

 - Windows 可执行文件 (.exe)  

最好保存为包（而不转换为应用程序的包）的类型包括：

 - 系统维护工具。 例如脚本或备份实用程序。  

 - 不支持的软件包。

> [!Tip]  
> 在标识不适合转换为应用程序的包之后，将它们移入 Configuration Manager 控制台的单独文件夹中。 在 Configuration Manager 控制台中创建包文件夹：  
> - 右键单击“包”节点。  
> - 选择“文件夹”，然后选择“创建文件夹”。  
> - 输入文件夹的名称，例如 `Not Converted`。  
> - 单击" **确定**"。  

#### <a name="prepare-the-packages-for-conversion"></a>准备待转换的包

对于你想转换的每个包，请确保它们符合以下条件：  

 - 源文件的位置是完整的 UNC 路径，例如 `\\Server\Share\File`。  

 - Windows Installer 文件仅使用一个唯一的产品代码。  


### <a name="bkmk_test"></a> 选择测试包

测试包组应尽量包括满足以下条件的包：  

 - 至少一个测试包的就绪状态为“自动” 。  

 - 至少一个测试包的就绪状态为“手动” 。  

理想情况下，测试包应为核心包，例如：  

 - 你熟悉的包。  

 - 对你的组织最重要的包。  

 - 可以最轻松地对其进行测试的包。  

标识适用于测试的包。 然后将其移至 Configuration Manager 控制台中单独的文件夹。


### <a name="bkmk_analyze"></a> 分析、调查并转换测试包

#### <a name="analyze-packages"></a>分析包

若要分析单个包或一个小组，使用在 Configuration Manager 控制台中集成的包转换管理器。 有关详细信息，请参阅[如何分析和转换包](/sccm/apps/pcm/how-to-analyze-and-convert)。  

> [!NOTE]  
> 查看“监视”工作区中的“包转换状态”节点。 它显示有关分析和转换进程的摘要信息。  

#### <a name="investigate-analysis-results"></a>调查分析结果

分析测试包后，调查就绪状态为“手动”  或“错误” 的包。 确定其具有该状态的原因。 “手动”  或“错误”  就绪状态的一些常见原因包括：

 - 包中没有在应用程序部署类型中创建检测方法时所需的信息。  

 - 包中没有将集合转换为全局条件和要求时所需的信息。  

 - 包中具有多个程序。  

 - 此包依赖于尚未转换为应用程序的另一个包。  

有关详细信息，请使用以下资源：  

- 有关错误消息和修复方法，请参阅[包转换管理器错误消息的技术参考](/sccm/apps/pcm/error-messages)  

- 查看日志文件 PCMTrace.log  

- [包转换管理器故障排除](/sccm/apps/pcm/troubleshoot-pcm)  

#### <a name="convert-the-packages"></a>转换包

有关如何转换包的详细信息，请参阅[如何分析和转换包](/sccm/apps/pcm/how-to-analyze-and-convert)。

> [!NOTE]  
> 查看“监视”工作区中的“包转换状态”节点。 它显示有关分析和转换进程的摘要信息。  


### <a name="bkmk_deploy"></a> 测试和部署应用程序

根据详细的包转换计划，在测试环境或生产环境中测试应用程序。



## <a name="recommendations"></a>建议

- 使用“监视”工作区中的“包转换状态”节点。 它显示有关分析和转换进程的摘要信息。  

- 调查包中称为“包装器”的程序。 使用包转换管理器插件将其功能转换成等效的 Configuration Manager 功能。  

- 请确保先对每个转换后的应用程序进行全面测试，再将其部署到生产环境中。  



## <a name="next-steps"></a>后续步骤

[如何分析和转换包](/sccm/apps/pcm/how-to-analyze-and-convert)