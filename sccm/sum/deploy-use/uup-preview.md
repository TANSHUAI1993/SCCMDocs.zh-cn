---
title: UUP 预览版
titleSuffix: Configuration Manager
description: 有关 UUP 集成预览版的说明
ms.date: 10/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ab35b96431fccf86e8bce09059f33c6a82d9ff10
ms.sourcegitcommit: 44c48e2cb00e60d6ccb1ddde62a6159663917e2d
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923907"
---
# <a name="uup-private-preview-instructions"></a>UUP 个人预览版说明

> [!Note]  
> 该信息涉及预览功能，该预览功能可能会在其商业发行之前进行大幅度修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="introduction"></a>简介

统一更新平台（UUP）是使用者和企业设备接收来自 Windows 更新 for Business 更新的打包和发布平台。 UUP 专用预览计划适用于已同意帮助 Microsoft 验证在 Configuration Manager 中使用 UUP 更新的客户。 这些更新当前未公开提供。

有关 UUP 的详细信息，请参阅以下 Windows 博客文章：[有关我们的统一更新平台 (UUP) 的更新](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/)。

## <a name="benefits"></a>优点

Windows 10 UUP 功能和累积更新可帮助解决客户目前向 Windows 提供服务的多个问题。

### <a name="feature-updates"></a>功能更新

- 通过 UUP 功能更新，Windows 更新过程会保留点播功能（FOD）和语言包。

- 直接更新到最新的安全符合性级别。 不需要在功能更新后立即安装安全更新。 Microsoft 每月发布一次新的功能更新，并提供最新的累积安全更新。 每个月都无需下载或分发大多数功能更新内容。 你只会下载安全更新，该更新将 UUP 与累积更新共享。

### <a name="cumulative-updates"></a>累积更新

- UUP 累积更新包括含每月累积安全更新的服务堆栈更新 (SSU)。 这样可解决协调这两种更新的难题。 它可确保提供服务堆栈更新以安装累积更新。 无需管理和协调这些关系。

- 利用 UUP 的累积更新，你可以脱机分发 FOD 和语言包内容。 此行为使用户能够按需添加它们。 用户无需从 internet 下载，也无需确定如何预安排此内容。

## <a name="set-up"></a>开始参与

### <a name="1-send-your-wsus-id-to-microsoft"></a>1.将 WSUS ID 发送给 Microsoft

若要参与 UUP 个人预览版，请与 UUP preview 联系人共享 WSUS ID。 Microsoft 将 WSUS 环境审批到 UUP preview 计划中。 若没有此 ID，在预览版发布之前，你无法看到任何 UUP 更新。

若要获取 WSUS ID，请运行以下 PowerShell 脚本：

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

MUUrl 属性应为 `https://sws.update.microsoft.com`  。 若要更改它，请参阅以下支持文章中的解决方法： [WSUS 同步失败，并出现 SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)。

### <a name="2-update-configuration-manager"></a>2.更新 Configuration Manager

对 Configuration Manager 站点进行以下更改，以支持此 UUP 预览版：

#### <a name="diagnostics-and-usage-data-level"></a>诊断和使用情况数据级别

请考虑在此预览期间提高 Configuration Manager 诊断和数据使用情况级别。 “完整”级别可帮助 Microsoft 更好地分析和排查此新功能的问题  。 有关详细信息，请参阅 [1906 版的诊断使用情况数据收集的级别](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906)。

#### <a name="install-the-latest-update"></a>安装最新更新

1. 用以下更新之一更新站点：

    - 版本1902与[更新汇总](https://support.microsoft.com/help/4500571)
    - [版本 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906)

    有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。

2. 更新客户端。  

    - 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  

    - 若要防止不必要地将大约 6 GB 的未使用内容下载到客户端  ，请更新所有针对 UUP 更新的客户端。

### <a name="3-update-windows-clients-to-a-supported-version"></a>3.将 Windows 客户端更新为支持的版本

若要成功安装 UUP 更新，请安装以下两个更新：

1. 特定的最低每月累计符合性级别。

2. Microsoft 更新目录中的特定非累积、非安全更新。 若要将更新导入到 Configuration Manager 进行部署，请参阅[从 Microsoft 更新目录导入更新](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>受支持的 Windows 10 版本和所需更新

| Windows 10 版本 | 最低符合性级别 | 其他目录更新 |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10 版本 1809** | 2019年8月， [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10 版本 1803** | 2019年4月， [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10 版本 1709** | 2019年4月， [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4.在有可用内容时，允许客户端下载增量内容

要使 UUP 更新正确下载，请启用客户端设置以**允许客户端下载增量内容（如果可用**）。 此设置使 Configuration Manager 可以让 Windows 更新代理（WUA）确定要下载到客户端的必需内容。 此行为而不是默认情况下，Configuration Manager 客户端下载与 UUP 更新关联的所有内容。 当你启用此设置时，WUA 将确定每个 UUP 更新需要的附加内容。 例如，只需所需的 FOD 和语言包。

当你启用此设置时，它不会影响从 internet 下载服务器内容。 它仅适用于客户端下载。 将 UUP 更新部署到客户端之前，请将此设置应用于满足 UUP 支持的版本的客户端。 必备客户端更新修复 WSUS 和 Configuration Manager 中的 UUP 更新的兼容性问题。

有关此客户端设置的详细信息，请参阅[关于客户端设置 - 软件更新](/sccm/core/clients/deploy/about-client-settings#allow-clients-to-download-delta-content-when-available)

### <a name="5-review-your-software-update-infrastructure"></a>5.查看软件更新基础结构

在同步 UUP 更新之前，请查看自动部署规则（ADR）和维护服务计划。 如果你不希望这些更新自动部署，请修改你的 Adr 来筛选它们。有关详细信息，请参阅[如何查找同步的 UUP 更新](#how-to-find-synced-uup-updates)。 默认情况下，现有维护服务计划仅部署非 UUP 的更新。 您可以修改维护计划以更改此行为。

查看符合性报告并根据需要进行修订。 例如，如果在所有产品中测量符合性，现在会看到 UUP 和非 UUP 累积更新。 对于这两种类型的更新，设备将报告符合性。 请确保符合性报告满足此更改。

## <a name="enable-uup-and-start-testing"></a>启用 UUP 并开始测试

### <a name="select-products-and-classifications-to-sync"></a>选择要同步的产品和分类

准备好开始同步 UUP 更新后，Microsoft 已批准 WSUS ID，启用新产品：

1. [同步软件更新](/sccm/sum/get-started/synchronize-software-updates)以填充新产品。  

2. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。

3. 选择顶层站点，它是管理中心站点 (CAS) 或独立主站点。

4. 在功能区中，选择“配置站点组件”，然后选择“软件更新点”   。

5. 切换到 "**产品**" 选项卡，然后选择以下一个或多个产品： 

    - **Windows 10 UUP 预览版**
    - **Windows Server UUP 预览版**

6. 切换到 "**分类**" 选项卡，然后选择以下选项：  

    - **安全更新**：若要查看 UUP 累积更新  
    - **升级**：查看 UUP 功能更新  

7. 再次同步软件更新以查看新的 UUP 更新。

### <a name="how-to-find-synced-uup-updates"></a>如何查找同步的 UUP 更新

将 UUP 更新同步到你的环境后，请在 Configuration Manager 控制台中找到它们进行测试。 可以通过两种方法查找预览更新：

- 由于这些预览更新在单独的产品中，因此请使用产品进行筛选以查找这些更新。 使用维护计划的产品筛选器部署 UUP 或非 UUP 功能更新。  

- 在软件库的“所有软件更新”和“所有 Windows 10 更新”节点中，都有一个新的可选列，即“标记”     。 此属性还可用作 Adr 中的筛选器。 对于 UUP 更新，请在此字段中搜索 `UUP`。 对于非 UUP 的更新，它是空白的。  

### <a name="updates-available-during-preview"></a>在预览期间可用的更新

有关 Microsoft 发布的所有 Windows 10 更新的详细信息，请参阅[windows 10 发布信息](https://docs.microsoft.com/windows/release-information/)。

#### <a name="cumulative-updates-to-test"></a>要测试的累积更新

尽管你可能会看到多个 UUP 标记的更新，但请从 2019-09 **2019 年9月**版更新或更高版本开始。 例如：

- 2019-09 适用于基于 x64 的系统的 Windows 10 版本1809累积更新（KB4512578）
- 2019-09 适用于基于 x64 的系统的 Windows 10 版本1803累积更新（KB4516058）
- 2019-09 适用于基于 x64 的系统的 Windows 10 版本1709累积更新（KB4516066）

#### <a name="feature-updates-to-test"></a>要测试的功能更新

尽管可能会看到多个 UUP 标记的可用更新，但请从**9 月 2019** （2019-09B）更新或更高版本开始。 例如：

- Windows 10 版本 1809 x64 2019 的功能更新-09B
- Windows 10 版本 1803 x64 2019 的功能更新-09B

### <a name="scenarios-to-test"></a>测试方案

#### <a name="test-feature-updates"></a>测试功能更新

- 直接更新到所选安全符合性级别  

- 在更新之前安装 FODs 和语言包。 请确保更新保留这些组件。  

#### <a name="test-cumulative-updates"></a>测试累积更新

在预览期间，使用 UUP 类型更新来使客户端符合多个连续更新。 此测试可帮助你了解当前的行为。

#### <a name="test-content"></a>测试内容

每个主版本（1809、1803、1709）、体系结构和语言组合的第一个更新将显示为大。 与以前在 UUP 更新中看到的内容相比，此大小与文件和磁盘空间的数量相同。 此额外内容主要用于所有 FOD 和语言包以进行累积更新。 对于功能更新，此首次更新提供了更大的内容。

对于未来的累积和功能更新，站点下载和分发的新内容量要小得多。 UUP 智能地在更新之间共享所有 FOD 和语言包内容。 不需要重新下载或重新分发此共享内容。 在预览期间，在 Windows 10 版本1709和1803中，每月下载与非 UUP 方案中累积更新的大小有关。 在 Windows 10 版本1809及更高版本中，累积更新的增量下载每月都很小。

查看在无需 UUP 的12个月期间内下载和分发的所有内容*时，不*使用的 Windows 10 版本1803应与具有 UUP 的版本1809大致相同。 在版本1809中，通过 UUP 下载和分发的内容总数更小。

#### <a name="supported-content-channels"></a>支持的内容通道

对于预览，请测试典型的实际方案。 UUP 支持所有内容通道，包括：

- Windows 传递优化 (DO)
- Configuration Manager 对等缓存
- Windows BranchCache
- 使用 "**无部署包**" 选项，客户端直接从 Microsoft 更新下载。 将此选项与传递优化配合使用。
- 第三方替换内容提供程序

有关详细信息，请参阅[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)。

<!-- TODO: Addlink to WSUS Perf documentation-->
