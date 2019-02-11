---
title: SCAP 扩展
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 的安全内容自动化协议 (SCAP) 扩展。
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e42027663f06bff715cb7e9087ececbc421cc495
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482446"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>关于安全内容自动化协议 (SCAP) 扩展

适用范围：System Center Configuration Manager (Current Branch)

Configuration Manager 的 SCAP 扩展有助于分析和评估网络环境是否符合安全内容自动化协议 (SCAP)。 SCAP 由美国国家标准技术研究院 (NIST) 定义和维护。 有关详细信息，请参阅 [SCAP 项目概述](https://csrc.nist.gov/projects/security-content-automation-protocol)。

> [!Note]  
> 此版本的工具是预发布功能，仅在版本 1806 中提供。 此版本未通过 NIST 认证。 <!--SCCMDocs-pr issue 3323-->
> 
> 如果需要使用已认证的工具或正在使用 Configuration Manager 当前分支的其他版本，请使用以下版本的 SCAP 扩展：
> - [下载 System Center Configuration Manager 的 SCAP 扩展](https://www.microsoft.com/download/details.aspx?id=48741)
> - [SCAP 扩展版本 3.0 的文档](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/mt228311\(v%3dtechnet.10\))

Configuration Manager 的 SCAP 扩展使用符合性设置功能首先扫描环境中的计算机。 然后，记录这些计算机对美国政府配置基线 (USGCB) 的符合性级别。

此扩展使 Configuration Manager 能够使用 SCAP 数据流、评估系统的符合性以及以 SCAP 格式生成报表结果。 组织可使用现有的 Configuration Manager 基础结构，帮助确保所管理的计算机满足此联邦符合性要求。 还可以使用 Configuration Manager 生成 NIST 和行政管理和预算局 (OMB) 所需的 USGCB 报告。

本文提供的信息可帮助在 Configuration Manager 基础结构中安装、配置和运行 SCAP 扩展。



## <a name="whats-new"></a>新增功能

此版本的 Configuration Manager SCEP 扩展包括并支持以下功能：  

- Configuration Manager 控制台扩展，可将 SCAP 内容转换为符合性设置基线。  

- SCAP 1.2 版，包括以下组件：  

  - 可扩展配置清单描述格式 (XCCDF) 1.2 版
  - 高达 5.10 版的开放漏洞和评估语言 (OVAL)
  - 生成资产报告格式 (ARF) 1.1 的报表
  - 通用平台枚举 (CPE) 2.3
  - 通用漏洞和披露 (CVE)
  - 通用配置枚举 (CCE) 版本 5
  - USGCB Internet Explorer 8、USGCB Windows 7 和 USGCB Windows 7 防火墙  

- 可向后兼容 SCAP 1.1 版和 1.0 版。  

- 用于导入 SCAP 1.2/1.1/1.0 和 OVAL 内容以转换为配置基线的控制台向导。  

  - 允许选择 SCAP 源数据流以及 XCCDF 基准和配置文件进行转换。

- 用于将配置评估结果导出到 SCAP 格式的 XML 报告的控制台向导。  

  - 显示用于生成基线的源文件、SCAP 数据流、XCCDF 基准和 XCCDF 配置文件。
  - 生成 Cyberscope 轻型资产汇总结果 (LASR) 报表。  

- 基于配置基线部署生成 SCAP 报告。 此组件包含一个新仪表板，可直观地查看客户端符合性和 XCCDF 规则符合性。 该仪表板支持钻取更多详细报告，你可以对这些报告进行搜索和筛选。  

- 改进了从 OVAL 测试转换的多种配置项的性能，从而可以更快速地进行评估。  

- 解决了 Windows 10 DISA v1r3 内容中发现的几个问题。  



## <a name="terms"></a>术语

- **OVAL ID**：符合 OVAL ID 格式的特定 OVAL 定义的标识符。  

- **SCAP 结果数据流**：一个由 SCAP 组件以及 SCAP 组件之间的引用映射组成的捆绑包，用于保存输出（结果）内容。  

- **SCAP 源数据流**：一个由 SCAP 组件以及 SCAP 组件之间的引用映射组成的捆绑包，用于保存输入（源）内容。



## <a name="deployment-process"></a>部署过程

下面是整个部署过程摘要：  

- [准备基础结构](#bkmk_prepare)以使用扩展  

- [安装和配置 Configuration Manager 的 SCAP 扩展](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install)  

- 从 NIST [下载并安装 SCAP 数据流文件](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files)  

- 转换 SCAP 数据流文件并将其导入到 Configuration Manager 符合性设置基线。 使用以下两种方法之一：   

    - [手动过程](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import)：在 Configuration Manager 控制台中使用导入向导  

    - [自动过程](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import)：使用 Microsoft.Sces.ScapToDcm.exe 命令行工具  

- 将配置基线[部署](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy)到集合  

- [监视](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor)符合性数据  

- 使用以下两种方法之一将符合性结果导出为 SCAP 格式：  

    - [手动过程](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export)：在控制台中使用导出向导  

    - [自动过程](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export)：使用 Microsoft.Sces.DcmToScap.exe 命令行工具  



## <a name="bkmk_prepare"></a>准备基础结构

### <a name="software-requirements"></a>软件要求

若要安装、配置和运行 Configuration Manager 的 SCAP 扩展，所用计算机需具备以下软件：

- [受支持的](/sccm/core/servers/manage/current-branch-versions-supported) Configuration Manager Current Branch 控制台版本。  

- 与 Configuration Manager 控制台兼容的操作系统版本。 有关详细信息，请参阅 [Configuration Manager 控制台支持的操作系统](/sccm/core/plan-design/configs/supported-operating-systems-consoles)。  

除了运行 SCAP 扩展的计算机，还需要以下各项：

- Configuration Manager Current Branch 基础结构。 有关 Configuration Manager 部署要求的详细信息，请参阅 [Configuration Manager 支持的配置](/sccm/core/plan-design/configs/supported-configurations)一文。  

想要对其进行 SCAP 符合性评估的计算机需要以下软件和配置：

- Configuration Manager 客户端。  

- Windows PowerShell 2.0 或更高版本。  

- Configuration Manager PowerShell 执行策略设置为“绕过”。 有关详细信息，请参阅 [PowerShell 执行策略](/sccm/core/clients/deploy/about-client-settings#computer-agent)一文。  

- 以下操作系统之一：  
  - Windows 7 SP1，32 位或 64 位
  - Windows 10，32 位或 64 位
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>硬件要求

有关 Configuration Manager 最低系统要求的详细信息，请参阅[为 Configuration Manager 规划硬件配置](/sccm/core/plan-design/configs/recommended-hardware)。



## <a name="accessibility-features"></a>辅助功能

Configuration Manager 的 SCAP 扩展包含 Windows 命令行工具。 这些工具可以利用 Windows 中的辅助功能和工具。

- 记录了 Microsoft.Sces.ScapToDcm.exe 和 Microsoft.Sces.DcmToScap.exe 的命令行参数。 有关详细信息，请参阅 [Microsoft.Sces.ScapToDcm.exe。命令行参数](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters)和 [Microsoft.Sces.DcmToScap.exe 命令行参数](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters)。  

- 各个工具的命令行参数 `-help` 和 `-?` 将其使用情况显示在屏幕上。 这些使用详情随后可供屏幕读取器和其他辅助技术使用。  

- 有关详细信息，请参阅 [Windows 辅助功能](http://windows.microsoft.com/windows/help/accessibility)。

SCAP 扩展还利用 Configuration Manager 中的辅助功能。 有关详细信息，请参阅 [Configuration Manager 中的辅助功能](/sccm/core/understand/accessibility-features)。

有关 Microsoft 辅助功能产品和服务的详细信息，请参阅 [Microsoft Accessibility 网站](http://go.microsoft.com/fwlink/p/?LinkId=9212)。



## <a name="next-step"></a>下一步
> [!div class="nextstepaction"]
> [安装和配置 SCAP 扩展](/sccm/compliance/plan-design/scap/install-configure-scap)
