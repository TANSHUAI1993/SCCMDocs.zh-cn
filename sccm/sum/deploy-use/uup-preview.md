---
title: UUP 预览版
titleSuffix: Configuration Manager
description: 有关 UUP 集成预览版的说明
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: d2aac5945d4b7678acf78d215c557a34aaef9c72
ms.sourcegitcommit: f5fa9e657350ceb963a7928497d2adca9caef3d4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2018
ms.locfileid: "53748552"
---
# <a name="uup-private-preview-instructions"></a>UUP 个人预览版说明

> [!Note]  
> 该信息涉及预览功能，该预览功能可能会在其商业发行之前进行大幅度修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="benefits"></a>优点

### <a name="feature-updates"></a>功能更新

使用 UUP 进行功能更新旨在缓解客户目前在服务方面遇到的诸多问题。 尝试 UUP 功能更新，包括：

- 直接升级到最新的安全符合性级别，而不再需要在升级后立即安装安全更新以符合要求。 每月发布一个新功能更新，以包含最新的累积安全更新。 无需每月重新下载或分发大部分功能更新内容，只需安装更新组件，该组件也可与累积更新共享。

- 在升级过程中，应保留所有 FOD 和语言包，而不是丢弃。

- 使用 UUP 的功能更新支持快速安装文件，使客户能够减少每个客户端必须下载的内容量。

### <a name="cumulative-updates"></a>累积更新

使用 UUP 的累积更新允许对 FOD 和语言包的内容进行脱机分发，从而使最终用户能够按需获取它们，而无需上网或管理员进行繁琐的暂存工作。



## <a name="set-up-instructions"></a>设置说明

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1.将 WSUS ID 发送到 Microsoft 的 UUP 预览版联系人

要参与 UUP 个人预览版，必须与 Microsoft 共享 WSUS ID，以便我们将你的环境列入预览版。 若没有此 ID，在预览版发布之前，你将无法看到任何 UUP 更新。

检索 WSUS ID：

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId
```

### <a name="2-upgrade-configmgr-to-a-supported-version"></a>2.将 ConfigMgr 升级到支持的版本

若要在环境中同步快速安装文件，则生产环境需要安装 ConfigMgr 1810（TAP、快速通道或正式发行版本均可接受），或 Technical Preview 环境需要安装 1812 Technical Preview。

若要在环境中同步快速安装文件，则生产环境需要安装基于 1810 正式发行版 的 ConfigMgr 1810 UUP 修补程序，或技术预览环境需要安装 1812 Technical Preview。


#### <a name="configmgr-1810-uup-hotfix-kb4482615-from-1810-ga-slow-ring"></a>来自 1810 正式发行版（慢速通道）的 ConfigMgr 1810 UUP 修补程序 (KB4482615)
如果当前使用的是 ConfigMgr 1810 GA（慢速通道），则将需要将 ConfigMgr 更新到 UUP 汇总。

1. 应用“Configuration Manager 1810 修补程序 (KB4482615)”(package GUI 86450B7D-3574-4CF7-8B11-486A2C1F62A6) - 此修补程序将为非快速方案启用 UUP。  

    1. 从 Microsoft 下载中心下载此修补程序（链接将在发布后提供）  

    2. 下载此修补程序后，请参阅以下 Microsoft Docs 网页以获取安装说明：[使用更新注册工具导入修补程序](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

    3. 有关如何下载 Microsoft 支持文件的详细信息，请单击以下文章编号以查看 Microsoft 知识库中的文章：[如何从联机服务获取 Microsoft 支持文件](https://support.microsoft.com/help/119591/how-to-obtain-microsoft-support-files-from-online-services)  

2. 升级到 UUP 修补程序后，请将 ConfigMgr 客户端升级到与之匹配的版本。 必须升级所有针对 UUP 更新的客户端，以防止不必要地将大约 6 GB 的未使用内容下载到客户端。

#### <a name="configmgr-1810-uup-hotfix-kb4482615-from-1810-fast-ring"></a>来自 1810 快速通道的 ConfigMgr 1810 UUP 修补程序 (KB4482615)
如果当前使用的是 ConfigMgr 1810 快速通道，则需要升级 ConfigMgr 并进行两次服务更新，但是在部署客户端升级之前要先暂停部署，这样只需要升级一次客户端。

1. 我们很快就会推出一个可以升级到 1810 GA 的修补程序（预计 1 月初），直到你看到更新出现在“更新与维护服务”中。  

2. 升级（仅限站点服务器，而不是客户端）到“Configuration Manager 1810 修补程序 (KB4479288)”(package GUID 930FA45E-530F-4B08-B1BF-DE3F5267B03C)  

3. 再次升级到“Configuration Manager 1810 修补程序 (KB4482615)”(package GUID 86450B7D-3574-4CF7-8B11-486A2C1F62A6) - 此修补程序将启用 UUP 用于非快速方案。  

    1. 从 Microsoft 下载中心下载此修补程序（链接将在发布后提供）  

    2. 下载此修补程序后，请参阅以下 Microsoft Docs 网页以获取安装说明：[使用更新注册工具导入修补程序](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

    3. 有关如何下载 Microsoft 支持文件的详细信息，请单击以下文章编号以查看 Microsoft 知识库中的文章：[如何从联机服务获取 Microsoft 支持文件](https://support.microsoft.com/help/119591/how-to-obtain-microsoft-support-files-from-online-services)  

4. 升级到 UUP 修补程序后，请将 ConfigMgr 客户端升级到与之匹配的版本。 必须升级所有针对 UUP 更新的客户端，以防止不必要地将大约 6 GB 的未使用内容下载到客户端。

#### <a name="1812-technical-preview"></a>1812 Technical Preview
1812 Technical Preview 在受支持的 UUP 方案中相当于 ConfigMgr 1810 UUP 修补程序 (KB4482615)。

唯一需要注意的是，1812 Technical Preview 的客户端升级已从 1810.1 TP 或 1811 TP 断开。 要解决此问题，需要卸载 1810.1 TP 和 1811 TP 客户端，然后完全安装 1812 TP 客户端。 所有针对 UUP 更新的客户端都必须处于 1812 Technical Preview（或更高版本），以防止不必要地将大约 6 GB 的未使用内容下载到客户端。


### <a name="3-update-windows-clients-to-supported-versions"></a>3.将 Windows 客户端更新为支持的版本

#### <a name="for-express-installation-file-sync"></a>对于快速安装文件同步
对于快速内容，受支持的 Windows 版本包括：

- Windows 10 版本 1709 和 [KB4338825](https://support.microsoft.com/help/4338825)（2017 年 7 月累计安全更新）或更高版本  

- Windows 10 版本 1803 和 [KB4284835](https://support.microsoft.com/help/4284835)（2017 年 6 月累计安全更新）或更高版本  

- Windows 10 版本 1809 和尚未发布的 1 月累积非安全更新（或以下 2 月累积安全更新）或更高版本

#### <a name="for-non-express-installation-file-sync"></a>对于非快速安装文件同步
对于非快速内容，必须应用其他修补程序。 此路径在目录 12/20 上以非累积格式提供，并将在 1 月下旬以正常累积格式提供。

Windows 10 版本 1709 和 Windows 10 版本 1803 的任何一种：
- 12 - 1 月版本：客户端必须具有基本累积更新级别和非累积更新  
    - 累积更新  
        - 1709：[KB4338825](https://support.microsoft.com/help/4338825)（2017 年 7 月累积安全更新）到 2019 年 1 月安全累积更新（包括在内）  
        - 1803：[KB4284835](https://support.microsoft.com/help/4284835)（2017 年 6 月累积安全更新）到 2019 年 1 月累积安全更新（包括在内）  
    - 非累积更新：此更新仅在目录中可用，并且不直接同步到 WSUS。 要将更新导入环境以进行部署，请参阅[从 Microsoft 更新目录导入更新](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)。  
        - 1709：[KB4483530](https://support.microsoft.com/help/4483530)  
        - 1803：[KB4483541](https://support.microsoft.com/help/4483541)  
- 2 月及更高版本：对于累积更新，仅限于尚未发布的 1 月累积非安全更新（或以下 2 月累积安全更新）或更高版本   

Windows 10 版本 1809 和尚未发布的 1 月累积非安全更新（或以下 2 月累积安全更新）或更高版本


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4.在客户端设置中启用客户端上的快速安装

无论是否同步快速内容，都必须为 UUP 更新设置可启用快速安装的客户端设置。 通过此设置，ConfigMgr 可借助 WUA 确定需要下载到客户端的内容，而不是下载所有与 UUP 更新相关的内容。 该设置甚至对于非快速方案也是必需的，因为存在可选的 FOD 和语言包内容，导致大量不重要的额外数据，而所有与更新关联的客户端都不需要这些数据。

启用此设置不会影响服务器内容下载，只会影响客户端下载行为。 如果尚未启用此设置，则必须在启用此设置之前使用上面明确说明的 ConfigMgr 和 Windows 客户端版本，因为这些版本解决了直接在 WSUS 中批准更新的兼容性问题，使 ConfigMgr 能够使用此通道进行 UUP 更新，即使快速内容没有同步。

在客户端上启用快速安装：

1. 在 Configuration Manager 控制台中，浏览到“管理” \ “客户端设置”  

2. 打开要使用的客户端设置的属性，或者根据需要创建一个新的客户端设置。  

3. 在“软件更新”组下，将“在客户端上启用快速安装文件的安装”设置为“是”

![突出显示“软件更新”组中的客户端设置](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5.请确保已按需设置 ADR 

在启用 UUP 更新的同步之前，请考虑 ADR 以及所具有的任何其他更新的基础结构。 如果不希望这些更新作为现有 ADR 和服务计划的一部分自动进行部署，请务必更新 ADR 以将其筛选掉，请参阅[如何查找同步的 UUP 更新](#how-to-find-synced-uup-updates)。 现有服务计划仅在默认情况下部署非 UUP，但可更新该计划以更改此行为。

还要考虑这些更新是否会影响任何符合性报告或其他基础结构，只需通过将其同步并提前进行任何所需的更改即可。 例如，如果测量所有产品的符合性，将看到 UUP 和非 UUP 累积 Windows 10 更新都是不符合或符合要求的，因此会使数字出现偏差。



## <a name="enable-uup-and-start-testing"></a>启用 UUP 并开始测试

### <a name="select-products-and-classifications-to-sync"></a>选择要同步的产品和分类

一旦已准备好开始同步 UUP 更新并试用，且已收到 Microsoft 的消息，即我们已启用你的 WSUS 以查看试用版，请启用新产品。

1. [同步软件更新](/sccm/sum/get-started/synchronize-software-updates)以允许要填充的新产品  

2. 在 Configuration Manager 控制台中，浏览到“管理” \ “站点配置” \ “站点”。  

3. 选择顶层站点（CAS 或独立主站点）  

4. 打开“配置站点组件” \ “软件更新点”  

5. 在“产品”选项卡上，将 WSUS 服务器添加到预览版后，应显示两个新产品。 这些产品包含预览版 UUP 内容。  

    - **Windows 10 UUP 试点**：Windows 工作站 UUP 更新  
    - **Windows Server 2016 UUP**：Windows UUP 更新  

6. 在“分类”选项卡上，请务必选择：  

    - **安全更新**：查看 UUP 累积更新  
    - **升级**：查看 UUP 功能更新  

7. 同步软件更新以查看新的 UUP 更新


### <a name="how-to-find-synced-uup-updates"></a>如何查找同步的 UUP 更新

将 UUP 更新同步到环境后，需要找到它们以进行测试。 有两种简单的方法可以在 Configuration Manager 控制台中查找预览版更新。

- 由于这些预览版更新位于不同的产品中，因此始终可以使用该产品筛选或查找这些更新。 产品筛选器已添加到服务计划中，可选择是否要部署 UUP 或非 UUP 功能更新。  

- 在软件库的“所有软件更新”和“所有 Windows 10 更新”节点和 ADR 中的筛选器中，都有一个新的可选列，即“标记”。 此字段对于 UUP 更新设置为“UUP”，对于非 UUP 更新设置为空。  


### <a name="updates-available-during-preview"></a>在预览期间可用的更新

- Windows 10 1709 累积更新
    - 12 月安全更新 (12/11)
    - 1 月安全更新 (1/8)
    - 1 月非安全更新 (1/15)
    - 2 月安全更新 (2/12)  

- Windows 10 1803 累积更新
    - 12 月安全更新 (12/11)
    - 1 月安全更新 (1/8)
    - 1 月非安全更新 (1/15)
    - 2 月安全更新 (2/12)  

- Windows 10 1809 累积更新
    - 2 月安全更新 (2/12)  

- Windows 10 1803 功能更新（版本 1709 或 1803）   
    - 12 月安全更新符合性 (12/11)
    - 1 月安全更新符合性 (1/8)
    - 2 月安全更新符合性 (2/12)  

- Windows 10 1809 功能更新（版本 1709 或 1803）
    - 12 月 (12/11) 安全更新符合性
    - 1 月 (1/8) 安全更新符合性
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
与之前的非 UUP 更新相比，每个主要版本（1709、1803、1809）、体系结构和语言组合的第一次更新对文件数和磁盘空间量的要求似乎都比较大。 此额外内容主要用于所有 FOD 和语言包以进行累积更新。 对于功能更新，特别是如果启用了快速更新，则会为第一次更新提供额外的内容。 

但是，后续更新（累积更新和具有更高符合性级别的每月功能更新）需要下载和分发的新内容量将会小得多，因为所有 FOD 和语言包内容都会在更新中智能共享而不是重新加载或重新分配。 在预览期间，在版本 1709 和 1803 中，此月度下载大约相当于你在非 UUP 方案中看到的累积更新的大小。 然而，在版本 1809 中，由于累积更新的增量下载每月都要小得多，情况会好得多。 

查看非快速在 12 个月内下载和分发的总内容时，使用 UUP 的 1803 版应大约相当于不使用 UUP 的 1809 版，并且在这个临界点之后，UUP 在整个发布周期内下载和分发的内容总量在 1809 版会有所减少。 对于快速更新，转折点比 1809 更早，快速更新仅用于功能更新而不是累积更新，因此快速更新的大服务器内容成本仅为每次发布（而不是每月）一次。

#### <a name="supported-content-channels"></a>支持的内容通道
对于预览版，请借助你在实际企业环境中使用的内容进行测试。 UUP 将支持所有内容通道，包括：
- Windows 传递优化
- Configuration Manager 对等缓存
- Windows BranchCache
- 部署而不下载到服务器（没有部署包），直接从 MU 下载，如果你正在使用 MU，建议结合使用 DO
- 第三方替换内容提供程序

有关详细信息，请参阅[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)。
