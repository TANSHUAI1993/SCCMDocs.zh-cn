---
title: 关于安全内容自动化协议 (SCAP) 扩展
titleSuffix: Configuraton Manager
description: 了解安全内容自动化协议 (SCAP) 扩展
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 18463e4f87c60135bdc29d0f7ce4cb2f80a0eea7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>关于安全内容自动化协议 (SCAP) 扩展

*适用范围：System Center Configuration Manager (Current Branch)*

> [!Tip]  
> 此功能在 Technical Preview 1803 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 SCAP 扩展的此预发行版本可以安装在当前支持的任何 Configuration Manager Current Branch 和 LTSB 1606 版本上。 从 1803 Technical Preview 开始，安装文件位于 cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi 中。 

Microsoft System Center Configuration Manager 的 SCAP 扩展有助于分析和评估你的网络环境是否符合安全内容自动化协议 (SCAP)。 SCAP 由美国定义和维护。国家标准技术研究院 (NIST)。

Microsoft System Center Configuration Manager 的 SCAP 扩展使用 Microsoft System Center Configuration Manager 中的符合性设置功能来扫描环境中的计算机，然后记录其与美国政府配置基线 (USGCB) 授权的符合度。

此扩展使 Configuration Manager 能够使用安全内容自动化协议 (SCAP) 数据流、评估系统的符合性以及以 SCAP 格式生成报表结果。 你的组织可以使用现有的 Configuration Manager 基础结构，确保你所管理的计算机满足此联邦符合性要求，并为美国国家标准技术研究院 (NIST) 以及美国行政管理和预算局 (OMB) 生成必要的 USGCB 报告。行政管理和预算局 (OMB)。

本指南提供的信息可帮助你在 System Center Configuration Manager 基础结构中安装、配置和运行 SCAP 扩展。



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Microsoft System Center Configuration Manager 的 SCAP 扩展预发行版中的新增功能

通过此部分来了解最新版本中的新增功能。

System Center Configuration Manager 的 SCAP 扩展预发行版：

- 包含 Configuration Manager 控制台扩展，完全支持将 SCAP 内容转换为 System Center Configuration Manager Current Branch 的符合性设置基线
- 支持 SCAP 1.2 版并且可向后兼容 SCAP 1.1 版和 1.0 版。


  - 支持可扩展配置清单描述格式 (XCCDF) 1.2 版。
  - 支持高达 5.10 版的开放漏洞和评估语言 (OVAL) 版本。
  - 支持生成资产报告格式 (ARF) 1.1 的报表。
  - 支持通用平台枚举 (CPE) 2.3
  - 支持通用漏洞和披露 (CVE)
  - 支持通用配置枚举 (CCE) 版本 5
  - 支持 USGCB Internet Explorer 8、USGCB Windows 7 和 USGCB Windows 7 防火墙。

- 包含一个 UI 向导，用于导入 SCAP 1.2/1.1/1.0 和 OVAL 内容以转换为配置基线。


  - 允许选择 SCAP 源数据流以及 XCCDF 基准和配置文件进行转换。

- 包含一个 UI 向导，用于将配置评估结果导出到 SCAP 格式的 XML 报告


  - 显示用于生成基线的源文件、SCAP 数据流、XCCDF 基准和 XCCDF 配置文件。
  - 支持生成 Cyberscope 轻型资产汇总结果 (LASR) 报表。

- 支持基于配置基线部署生成 SCAP 报告。 包含一个新仪表板，可直观地查看客户端符合性和 XCCDF 规则符合性。 该仪表板支持钻取更多详细报告，你可以对这些报告进行搜索和筛选。
- 改进从 OVAL 测试转换的多种配置项目的性能，从而可以更快速地进行评估。

- 解决了 Windows 10 DISA v1r3 内容中发现的几个问题。

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Microsoft System Center Configuration Manager 的 SCAP 扩展部署过程

本指南介绍了如何使用 Microsoft System Center Configuration Manager 的 SCAP 扩展来分析、评估和报告 SCAP 符合性。 下面简要概述了需要遵循的步骤：

- 准备利用这些扩展所需的必备基础结构。
- 安装并配置 Microsoft System Center Configuration Manager 的 SCAP 扩展。
- 从[美国国家漏洞数据库](http://nvd.nist.gov) (NVD) 下载、安装和配置 SCAP 数据流文件。
- 使用导入向导**或**通过 Cabinet (.cab) 文件使用命令行 Microsoft.Sces.ScapToDcm.exe 工具，将 SCAP 数据流文件直接转换并导入到 System Center Configuration Manager 符合性设置基线中。
- 使用导出向导或命令行 Microsoft.Sces.DcmToScap.exe 工具将符合性结果导出为 SCAP 格式。

# <a name="terms"></a>术语

**OVAL ID：**符合 OVAL ID 格式的特定 OVAL 定义的标识符。

**SCAP 结果数据流：**一个由 SCAP 组件以及 SCAP 组件之间的引用映射组成的捆绑包，用于保存输出（结果）内容。

**SCAP 源数据流：**一个由 SCAP 组件以及 SCAP 组件之间的引用映射组成的捆绑包，用于保存输入（源）内容。

# <a name="prepare-the-prerequisite-infrastructure"></a>准备必备的基础结构

确保满足以下软件和硬件要求，以利用 Microsoft System Center Configuration Manager 的 SCAP 扩展。

## <a name="software-requirements"></a>软件要求

若要安装、配置和运行 Microsoft System Center Configuration Manager 的 SCAP 扩展，你需要带有以下软件的计算机：

- [受支持的](/sccm/core/servers/manage/current-branch-versions-supported) System Center Configuration Manager Current Branch 控制台版本。
- 与 System Center Configuration Manager 控制台兼容的操作系统。 有关兼容操作系统的列表，请参阅 [System Center Configuration Manager 控制台支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-consoles)一文。

除了运行 SCAP 扩展的计算机，还需要以下各项：

- System Center Configuration Manager Current Branch 基础结构。 有关 Configuration Manager 部署要求的详细信息，请参阅 [Configuration Manager 支持的配置](/sccm/core/plan-design/configs/supported-configurations)一文。

想要对其进行 SCAP 符合性评估的计算机需要以下软件和配置：

- 在 Configuration Manager 客户端上启用的符合性和设置管理组件。
- Windows PowerShell 2.0 或更高版本。
- Configuration Manager PowerShell 执行策略设置为“绕过”。 有关详细信息，请参阅 [PowerShell 执行策略](/sccm/core/clients/deploy/about-client-settings#computer-agent)一文。
- 以下操作系统之一
  - Windows 7 发行版本或 SP1，32 位或 64 位。
  - Windows 10 32 位或 64 位
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>硬件要求

下面提供了最低系统要求：

[为 Configuration Manager 规划硬件配置](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>辅助功能

System Center Configuration Manager 的 SCAP 扩展包含一些 Windows 命令行工具，它们可利用 Windows 中的辅助功能和工具。

- 此用户指南记录了 Microsoft.Sces.ScapToDcm.exe 和 Microsoft.Sces.DcmToScap.exe 的命令行参数。
- -help 和 -? 将工具使用情况打印到屏幕，提供给屏幕阅读器和其他辅助技术。
- Windows [辅助功能](http://windows.microsoft.com/windows/help/accessibility)

SCAP 扩展还利用 System Center Configuration Manager 中的功能。  Configuration Manager 包含可让残障人士更轻松地使用该产品的功能。

- [System Center Configuration Manager 中的辅助功能](/sccm/core/understand/accessibility-features)

有关 Microsoft 辅助功能产品和服务的常规信息，请访问 [Microsoft Accessibility 网站](http://go.microsoft.com/fwlink/p/?LinkId=9212)。

## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [安装和配置 SCAP 扩展](/sccm/compliance/plan-design/scap/install-configure-scap)
