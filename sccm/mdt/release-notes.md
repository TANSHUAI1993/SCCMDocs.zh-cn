---
title: MDT 发行说明
description: 了解 Microsoft Deployment Toolkit 支持的平台、先决条件和限制。
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814274"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Microsoft Deployment Toolkit 发行说明  

本文详细介绍 Microsoft Deployment Toolkit (MDT) 的最新版本。 这些详细信息包括支持的平台、先决条件及各项限制。 本文假定你熟悉 MDT 版本的概念、特点和功能。



## <a name="latest-release"></a>最新版本

**MDT 内部版本 8450** 是最新版本，可在 [Microsoft 下载中心](https://aka.ms/mdtdownload) 找到。 

此更新开始支持适用于 Windows 10（版本 1709）的 Windows 评估和部署工具包 (ADK)。 

***更新***：自 2018 年 5 月起，此内部版本还支持 Windows 10（版本 1803）。

有关详细信息，请参阅[支持的平台](#supported-platforms)部分。


### <a name="significant-changes"></a>重大更改
这款 MDT 内部版本中出现的重大更改汇总如下。

#### <a name="supported-configuration-updates"></a>支持的配置更新
- 适用于 Windows 10 版本 1709 的 Windows ADK
- Windows 10 版本 1709
- Configuration Manager 版本 1710

#### <a name="quality-updates"></a>质量更新
此版本中修复的 Bug 如下所示：
- Win10 旁加载应用依赖项和许可证未安装
- CaptureOnly 任务序列不允许捕获映像
- 启动 MDT 任务序列时出现错误：指定的 DeploymentType 值 "" 无效。 将停止部署
- ZTIMoveStateStore 在错误位置查找状态存储文件夹，导致文件夹无法移动
- xml 中存在简单的拼写错误，导致出现意外行为
- 安装角色和功能不适用于 Windows Server 2016 IIS 管理控制台功能
- 使用文件夹时，无法在升级任务序列中浏览操作系统映像
- MDT 工具错误地将 TPM 预配为“缩减功能状态”。 有关详细信息，请参阅 [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi)。
- TIGather 底盘类型检测逻辑更新
- 操作系统升级步骤遗漏了 SetupComplete.cmd，导致后续部署中断
- 一些硬件上的 Windows 10 ADK 1607 及更高版本的 UEFI 启动问题
- 包括已更新的 Configuration Manager 任务序列二进制文件



## <a name="supported-platforms"></a>受支持的平台

MDT 版本不再按年或更新版本进行标记。 为了更好地适应 Windows 10 和 Configuration Manager 的当前分支，同时简化品牌化和发布流程，该软件现在仅为 Microsoft Deployment Toolkit。 内部版本号用于区分各个版本。 例如，可供下载的最新版本是 8450。

与预先确定了发布计划的 Configuration Manager 不同，MDT 仅根据需要进行发布，目的是支持 Windows 10、Windows ADK 和 Configuration Manager Current Branch 的新版本。 必要时，本文将记录这些组件的所有已知问题。

以下操作系统版本可使用 MDT 进行部署：
- Windows 10 版本 1803
- Windows 10 版本 1709
- 其他[受支持的 Windows 10 版本](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>先决条件

MDT 需使用 Windows 中包含的以下组件：
- Microsoft .NET Framework 4.0
- Windows PowerShell 3.0 版

使用[适用于 Windows 10 的 Windows ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install) 的最新版本。 

> [!Note]  
> Windows 建议使用与要部署的 Windows 版本匹配的 Windows ADK。 例如，部署 Windows 10 版本 1703 时，使用适用于 Windows 10 版本 1703 的 Windows ADK。 有关 Windows ADK 组件支持能力的详细信息，请参阅 [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)（DISM 支持的平台）和 [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)（USMT 要求）。

若要集成 MDT 和 Configuration Manager 以实现 ZTI 和 UDI 方案，请使用 Configuration Manager 当前分支的最新版本。



## <a name="upgrading-mdt"></a>升级 MDT

MDT 安装进程会删除同一台计算机上当前安装的所有 MDT 实例。 此过程中，现有的部署共享内容、分发点和数据库均将保留。 在安装完成后必须将它们升级。

MDT 的当前版本支持通过以下 MDT 版本进行升级：
- MDT 版本 8443

> [!Tip]  
> 在尝试升级前，请创建现有 MDT 基础结构的备份。

### <a name="lti"></a>LTI
MDT 安装完成后，通过部署工作台的“部署共享”节点运行“打开部署共享向导”，以升级现有部署共享。 指定到现有部署共享目录的路径，然后选择“升级”复选框。 此过程还会升级现有网络部署共享和媒体部署共享，因此这些共享内容应该是可访问的。 部署时不要进行此升级，因为使用文件可能导致出现升级问题。

### <a name="zti"></a>ZTI
在 MDT 安装过程中，不修改 Configuration Manager 中的现有 MDT 任务序列。 它们应该能继续正常工作。 未提供任何用于升级这些任务序列的机制。 若要使用任何 MDT 新功能，请在 Configuration Manager 新建与 MDT 集成的任务序列。

完成升级后，请执行以下操作：  

- 在升级后运行“配置 ConfigMgr 集成向导”。 此向导会注册新的组件并安装已更新的 ZTI 任务序列模板。  

- 为所有新建的 ZTI 任务序列创建新的 Microsoft Deployment Toolkit 文件包。 对于在升级前创建的 ZTI 任务序列，可使用现有的 Microsoft Deployment Toolkit 文件包，但需要为新的 ZTI 任务序列创建新的 Microsoft Deployment Toolkit 文件包。



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>常见问题

#### <a name="whats-the-mdt-support-life-cycle"></a>什么是 MDT 支持生命周期？  
有关详细信息，请参阅 [Microsoft Deployment Toolkit 支持生命周期](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle)。

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>此版本是否只受 Windows 10、Windows ADK 或 Configuration Manager 版本 X 支持？
我们主要采用了以上列出的配置测试此版本的 MDT。 上述配置以外的情况很可能也可以正常运行此版本，除非存在明确的问题。 由于未明确测试其他组合，因此实际的使用情况可能有所不同。

#### <a name="how-do-i-get-help-with-mdt"></a>如何获取 MDT 方面的帮助？
可使用以下方法获取 MDT 相关帮助（按优先顺序排列）：

1. 发布到 [MDT 论坛](https://social.technet.microsoft.com/Forums/en/home?forum=mdt)。 社区中的 MVP 和其他人会在此处查看并答复大家发布的内容。 这可能是获取帮助最有效的途径。
2. 联系 Microsoft 支持部门。 创建支持案例并获取专业协助。
3. 如果可准确重现所遇到的问题并认为它是一个产品 Bug，请在 Windows 10 [反馈中心](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)提交问题。 产品团队会就报告的每项问题展开调查。 在提交反馈时，请选择“企业管理”类别和“操作系统部署”子类别。 选择这些类别有助于将你的反馈分类并路由给 MDT 团队。
     - 还可在反馈中心提交产品相关建议（设计更改请求 (DCR)）。
     - 如果你已通过联系支持部门提交反馈，则无需在反馈中心重新提交。