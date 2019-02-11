---
title: UUP 预览版
titleSuffix: Configuration Manager
description: 有关 UUP 集成预览版的说明
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fde592b02d78c0a2ab29d77f7e55273c143b09ee
ms.sourcegitcommit: f7b2fe522134cf102a3447505841cee315d3680c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570126"
---
# <a name="uup-private-preview-instructions"></a>UUP 个人预览版说明

> [!Note]  
> 该信息涉及预览功能，该预览功能可能会在其商业发行之前进行大幅度修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="benefits"></a>优点

### <a name="feature-updates"></a>功能更新

使用 Windows 10 统一更新平台 (UUP) 进行功能更新旨在缓解客户目前在服务方面遇到的诸多问题。 尝试 UUP 功能更新，包括：

- 直接升级到最新的安全符合性级别，而不再需要在升级后立即安装安全更新以符合要求。 每月发布一个新功能更新，以包含最新的累积安全更新。 无需每月重新下载或分发大部分功能更新内容，只需安装更新组件，该组件也可与累积更新共享。

- 在升级过程中，应保留所有按需功能 (FOD) 和语言包，而不是丢弃。

- 使用 UUP 的功能更新支持快速安装文件，使客户能够减少每个客户端必须下载的内容量。

有关 UUP 的详细信息，请参阅 Windows 博客文章[有关我们的统一更新平台 (UUP) 的更新](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/)。


### <a name="cumulative-updates"></a>累积更新

- 使用 UUP 的累积更新允许对 FOD 和语言包的内容进行脱机分发，从而使最终用户能够按需获取它们，而无需上网或管理员进行繁琐的暂存工作。

- 使用 UUP 的累积更新包括每月累积安全更新的服务堆栈更新。 这样可解决协调这两种更新的难题。 它可确保及时提供服务堆栈更新以安装累积更新，而无需管理和协调关系。



## <a name="set-up-instructions"></a>设置说明

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1.将 WSUS ID 发送到 Microsoft 的 UUP 预览版联系人

要参与 UUP 个人预览版，必须与 Microsoft 共享 WSUS ID，以便我们将你的环境列入预览版。 若没有此 ID，在预览版发布之前，你将无法看到任何 UUP 更新。

检索 WSUS ID：

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

MUUrl 属性应为 `https://sws.update.microsoft.com`。 若要更改它，请参阅以下支持文章中的解决办法：[WSUS 同步失败，出现 SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)


### <a name="2-update-configmgr"></a>2.更新 ConfigMgr

对 Configuration Manager 站点进行以下更改，以支持此 UUP 预览版：


#### <a name="diagnostics-and-usage-data-level"></a>诊断和使用情况数据级别
请考虑在此预览期间提高 Configuration Manager 诊断和数据使用情况级别。 “完整”级别可帮助 Microsoft 更好地分析和排查此新功能的问题。 有关详细信息，请参阅 [1810 版的诊断使用情况数据收集的级别](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)。


#### <a name="update-rollup-for-configmgr-1810-4486457"></a>ConfigMgr 1810 (4486457) 的更新汇总

1. 使用版本 1810 的更新汇总更新站点。 有关详细信息，请参阅[安装控制台内部更新](/sccm/core/servers/manage/install-in-console-updates)。  

2. 更新客户端。  

    - 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade)。  

    - 必须升级所有针对 UUP 更新的客户端，以防止不必要地将大约 6 GB 的未使用内容下载到客户端。

有关此更新的详细信息，请参阅 [System Center Configuration Manager Current Branch（版本 1810）更新汇总](https://support.microsoft.com/help/4486457)。


<!-- 
#### 1812 Technical Preview
The 1812 Technical Preview is equivalent in supported UUP scenarios to the ConfigMgr 1810 UUP Hotfix (KB4482615).

The only note is that client upgrade of 1812 Technical Preview is broken from 1810.1 TP or 1811 TP. To work around this issue, you'll need to uninstall 1810.1 TP and 1811 TP clients, then install the 1812 TP client cleanly. All clients you target UUP updates to must be on 1812 Technical Preview (or later) to prevent **unnecessarily downloading around 6 GB** of unused content to the client.
 -->


### <a name="3-update-windows-clients-to-supported-versions"></a>3.将 Windows 客户端更新为支持的版本

#### <a name="for-express-installation-file-sync"></a>对于快速安装文件同步
对于快速内容，受支持的 Windows 版本包括：

- 具有非安全性累计更新 [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976)（1 月 22 日发布）或更高版本的 Windows 10 版本 1809。 此更新仅在目录中可用，并且不直接同步到 WSUS。 要将更新导入环境以进行部署，请参阅[从 Microsoft 更新目录导入更新](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。

- Windows 10 版本 1803 和 [KB4284835](https://support.microsoft.com/help/4284835)（2017 年 6 月累计安全更新）或更高版本  

- Windows 10 版本 1709 和 [KB4338825](https://support.microsoft.com/help/4338825)（2017 年 7 月累计安全更新）或更高版本  


#### <a name="for-non-express-installation-file-sync"></a>对于非快速安装文件同步
对于非快速内容，必须应用其他修补程序。 此更新非常重要，可防止不必要地将大约 6 GB 的未使用内容下载到客户端。 受支持的 Windows 版本包括以下内部版本：

- 具有非安全性累计更新 [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976)（1 月 22 日发布）或更高版本的 Windows 10 版本 1809。 此更新仅在目录中可用，并且不直接同步到 WSUS。 要将更新导入环境以进行部署，请参阅[从 Microsoft 更新目录导入更新](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。


- Windows 10 版本 1803 和 Windows 10 版本 1709 客户端必须具有基本累积更新级别和非累积更新：
    - 累积更新
        - 1803：[KB4284835](https://support.microsoft.com/help/4284835)（2017 年 6 月累积安全更新）到 2019 年 1 月累积安全更新（包括在内）
        - 1709：[KB4338825](https://support.microsoft.com/help/4338825)（2017 年 7 月累积安全更新）到 2019 年 1 月安全累积更新（包括在内）
    - 非累积更新：此更新仅在目录中可用，并且不直接同步到 WSUS。 要将更新导入环境以进行部署，请参阅[从 Microsoft 更新目录导入更新](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。
        - 1803：[KB4483541](https://support.microsoft.com/help/4483541)
        - 1709：[KB4483530](https://support.microsoft.com/help/4483530)


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4.在客户端设置中启用客户端上的快速安装

无论是否同步快速内容，都必须为 UUP 更新设置可启用快速安装的客户端设置。 通过此设置，ConfigMgr 可借助 Windows 更新代理 (WUA) 确定需要下载到客户端的内容，而不是下载所有与 UUP 更新相关的内容。 该设置甚至对于非快速方案也是必需的，因为存在可选的 FOD 和语言包内容，导致大量不重要的额外数据，而所有与更新关联的客户端都不需要这些数据。

启用此设置不会影响服务器内容下载，只会影响客户端下载行为。 如果尚未启用此设置，则必须在启用此设置之前使用上面明确说明的 ConfigMgr 和 Windows 客户端版本，因为这些版本解决了直接在 WSUS 中批准更新的兼容性问题，使 ConfigMgr 能够使用此通道进行 UUP 更新，即使快速内容没有同步。

在客户端上启用快速安装：

1. 在 Configuration Manager 控制台中，浏览到“管理” \ “客户端设置”  

2. 打开要使用的客户端设置的属性，或者根据需要创建一个新的客户端设置。  

3. 在“软件更新”组下，将“在客户端上启用快速安装文件的安装”设置为“是”

![突出显示“软件更新”组中的客户端设置](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5.请确保已按需设置 ADR 

在启用 UUP 更新的同步之前，请考虑自动部署规则 (ADR) 以及所具有的任何其他更新的基础结构。 如果不希望这些更新作为现有 ADR 和服务计划的一部分自动进行部署，请务必更新 ADR 以将其筛选掉，请参阅[如何查找同步的 UUP 更新](#how-to-find-synced-uup-updates)。 现有服务计划仅在默认情况下部署非 UUP，但可更新该计划以更改此行为。

还要考虑这些更新是否会影响任何符合性报告或其他基础结构，只需通过将其同步并提前进行任何所需的更改即可。 例如，如果测量所有产品的符合性，将看到 UUP 和非 UUP 累积 Windows 10 更新都是不符合或符合要求的，因此会使数字出现偏差。



## <a name="enable-uup-and-start-testing"></a>启用 UUP 并开始测试

### <a name="select-products-and-classifications-to-sync"></a>选择要同步的产品和分类

一旦已准备好开始同步 UUP 更新并试用，且已收到 Microsoft 的消息，即我们已启用你的 WSUS 以查看试用版，请启用新产品。

1. [同步软件更新](/sccm/sum/get-started/synchronize-software-updates)以允许要填充的新产品  

2. 在 Configuration Manager 控制台中，浏览到“管理” \ “站点配置” \ “站点”。  

3. 选择顶层站点，它是管理中心站点 (CAS) 或独立主站点  

4. 打开“配置站点组件” \ “软件更新点”  

5. 在“产品”选项卡上，将 WSUS 服务器添加到预览版后，应显示两个新产品。 这些产品包含预览版 UUP 内容。  

    - **Windows 10 UUP 预览版**  
    - **Windows Server UUP 预览版**  

6. 在“分类”选项卡上，请务必选择：  

    - **安全更新**：查看 UUP 累积更新  
    - **升级**：查看 UUP 功能更新  

7. 同步软件更新以查看新的 UUP 更新


### <a name="how-to-find-synced-uup-updates"></a>如何查找同步的 UUP 更新

将 UUP 更新同步到环境后，需要找到它们以进行测试。 有两种简单的方法可以在 Configuration Manager 控制台中查找预览版更新。

- 由于这些预览版更新位于不同的产品中，因此始终可以使用该产品筛选或查找这些更新。 产品筛选器已添加到服务计划中，可选择是否要部署 UUP 或非 UUP 功能更新。  

- 在软件库的“所有软件更新”和“所有 Windows 10 更新”节点和 ADR 中的筛选器中，都有一个新的可选列，即“标记”。 此字段对于 UUP 更新设置为“UUP”，对于非 UUP 更新设置为空。  


### <a name="updates-available-during-preview"></a>在预览期间可用的更新

- Windows 10 1809 累积更新
    - 2 月安全更新 (2/12)  

- Windows 10 1803 累积更新
    - 12 月安全更新 (12/11)
    - 1 月安全更新 (1/8)
    - 1 月非安全更新 (1/15)
    - 2 月安全更新 (2/12)  

- Windows 10 1709 累积更新
    - 12 月安全更新 (12/11)
    - 1 月安全更新 (1/8)
    - 1 月非安全更新 (1/15)
    - 2 月安全更新 (2/12)  

- Windows 10 1809 功能更新（版本 1709 或 1803）
    - 12 月 (12/11) 安全更新符合性
    - 1 月 (1/8) 安全更新符合性
    - 2 月安全更新符合性 (2/12)  

- Windows 10 1803 功能更新（版本 1709 或 1803）   
    - 12 月安全更新符合性 (12/11)
    - 1 月安全更新符合性 (1/8)
    - 2 月安全更新符合性 (2/12)  

必要时，只要 UUP 仍处于预览状态（个人版或公共版），3 月和未来的安全更新将继续在所有这些区域中发布。 完成预览后，生产中将仅支持 Windows 10 版本 1809 累积更新和功能更新（Windows 10 版本 1803）。


### <a name="scenarios-to-try"></a>试用方案

#### <a name="feature-updates"></a>功能更新
- 直接升级到你选择的安全符合性级别  

- 使用在升级之前安装的 FOD 和语言包进行升级，通过升级以将其保留  

- （可选）启用同步快速安装文件以进行功能更新，以减少每个客户端必须下载的内容量。  

    > [!Note]  
    > 这种客户端的好处是，避免以更大的服务器下载和分发为代价，就像累积更新的快速安装文件一样。  

#### <a name="cumulative-updates"></a>累积更新
在预览期间，使用 UUP 类型更新保持客户端符合多个连续更新要求，体会持续更新的感觉。

#### <a name="content"></a>Content
与之前的非 UUP 更新相比，每个主要版本（1809、1803、1709）、体系结构和语言组合的第一次更新对文件数和磁盘空间量的要求似乎都比较大。 此额外内容主要用于所有 FOD 和语言包以进行累积更新。 对于功能更新，特别是如果启用了快速更新，则会为第一次更新提供额外的内容。 

但是，后续更新（累积更新和具有更高符合性级别的每月功能更新）需要下载和分发的新内容量将会小得多，因为所有 FOD 和语言包内容都会在更新中智能共享而不是重新加载或重新分配。 在预览期间，在版本 1709 和 1803 中，此月度下载大约相当于你在非 UUP 方案中看到的累积更新的大小。 然而，在版本 1809 中，由于累积更新的增量下载每月都要小得多，情况会好得多。 

查看非快速在 12 个月内下载和分发的总内容时，使用 UUP 的 1803 版应大约相当于不使用 UUP 的 1809 版，并且在这个临界点之后，UUP 在整个发布周期内下载和分发的内容总量在 1809 版会有所减少。 对于快速更新，转折点比 1809 更早，快速更新仅用于功能更新而不是累积更新，因此快速更新的大服务器内容成本仅为每次发布（而不是每月）一次。

#### <a name="supported-content-channels"></a>支持的内容通道
对于预览版，请借助你在实际企业环境中使用的内容进行测试。 UUP 将支持所有内容通道，包括：
- Windows 传递优化
- Configuration Manager 对等缓存
- Windows BranchCache
- 部署而不下载到服务器（没有部署包），直接从 Microsoft 更新下载，如果你正在使用 Microsoft 更新，建议结合使用传递优化
- 第三方替换内容提供程序

有关详细信息，请参阅[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)。
