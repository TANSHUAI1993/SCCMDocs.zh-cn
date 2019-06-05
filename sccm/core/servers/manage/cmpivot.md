---
title: 使用 CMPivot 获得实时数据
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 CMPivot 实时查询客户端。
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 975768c5bfaf239c1f8cd342c988e06dac5d1269
ms.sourcegitcommit: abfc9e1b3945637fa93ca8d3a11519493a5d5391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66264569"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>在 Configuration Manager 中使用 CMPivot 获得实时数据

<!--1358456-->

适用范围：*System Center Configuration Manager (Current Branch)*

Configuration Manager 总是提供设备数据的大型集中式存储，客户可将其用于报告目的。 该站点通常每周都会收集这些数据。 从 1806 版开始，CMPivot 这种新的控制台中实用工具现提供对环境中设备实时状态的访问。 它立即对目标集合中的所有连接设备运行查询，并返回结果。 可以在工具中对此数据进行筛选和分组。 通过提供来自联机客户端的实时数据，可以更快地回答业务问题、解决问题并对安全事件作出响应。

例如，在[缓解推测执行端通道漏洞](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/)中，其中一个要求是更新系统 BIOS。 可以使用 CMPivot 来快速查询系统 BIOS 信息，并查找不符合要求的客户端。

 > [!Tip]  
 > 某些安全软件可能会阻止 c:\windows\ccm\scriptstore 中运行的脚本。 这会阻止 CMPivot 查询的成功执行。 运行 CMPivot PowerShell 时，某些安全软件可能还会生成审核事件或警报。


## <a name="prerequisites"></a>先决条件

若要使用 CMPivot，需要以下组件：

- 将目标设备升级到 Configuration Manager 客户端的最新版本。  

- CMPivot 的权限：
  - “SMS 脚本”对象上的“读取权限”  
  - “集合”上的“运行脚本”权限  
  - “清单报表”上的“读取”权限  
  - 默认范围。 

- 目标客户端至少需要 PowerShell 版本 4。

- 若要收集有关以下实体的数据，目标客户端需要 PowerShell 5.0 版：  
  - 管理员
  - 连接
  - IPConfig
  - SMBConfig

 
## <a name="limitations"></a>限制

- 在层次结构中，将 Configuration Manager 控制台连接到主站点以运行 CMPivot  。 当“启动 CMPivot”操作连接到管理中心站点 (CAS) 时，它不会出现在控制台中  。
  - 从 Configuration Manager 版本 1902 开始，就可以从 CAS 运行 CMPivot。 在某些环境中，需要其他权限。 有关详细信息，请参阅[从版本 1902 开始的 CMPivot](#bkmk_cmpivot1902)。

- CMPivot 仅返回用于将客户端连接到当前站点的数据。  

- 如果集合包含来自其他站点的设备，则 CMPivot 结果仅来自当前站点中的设备。  

- 用户无法自定义实体属性、结果列或设备上的操作。  

- 只有一个 CMPivot 实例可以在运行 Configuration Manager 控制台的计算机上同时运行。  

- 在版本 1806 中，只有在组名为“管理员”时，对“管理员”  实体的查询才起作用。 如果组名已本地化，则不起作用。 例如，法语“Administrateurs”。<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>启动 CMPivot

1. 在 Configuration Manager 控制台中，连接到主站点。 转到“资产和符合性”  工作区，并选择“设备集合”  节点。 选择目标集合，然后单击功能区中的“启动 CMPivot”  ，以便启动该工具。  

    > [!Tip]  
    > 如果看不到此选项，请检查以下配置：  
    > 
    > - 与站点管理员确认你的帐户具有所需权限。 有关详细信息，请参阅[先决条件](#prerequisites)。  
    > 
    > - 将控制台连接到主站点  。  

2. 界面进一步提供有关使用该工具的信息。  

     - 可在顶部手动输入查询字符串，或单击联机文档中的链接。  

     - 单击其中一个实体  将其添加到查询字符串。  

     - 有关表运算符  、聚合函数  和标量函数  的链接，请在 Web 浏览器中打开语言参考文档。 CMPivot 使用 [Kusto 查询语言 (KQL)](https://docs.microsoft.com/azure/kusto/query/)。  

3. 打开 CMPivot 窗口，查看来自客户端的结果。 关闭 CMPivot 窗口时，会话已完成。  

    > [!Note]  
    > 如果已发送查询，客户端仍会向服务器发送状况消息响应。  



## <a name="how-to-use-cmpivot"></a>如何使用 CMPivot

![CMPivot 窗口示例](media/1358456-cmpivot-sample.png)

CMPivot 窗口包含以下元素：  

1. CMPivot 当前定位的集合位于顶部的标题栏和窗口底部的状态栏中。 例如，上面屏幕截图中的“PM_Team_Machines”。  

2. 左侧窗格列出了客户端上可用的实体  。 一些实体依赖于 WMI，而其他实体则使用 PowerShell 从客户端获取数据。   

    - 右键单击实体，执行以下操作：  

       - **插入**：将实体添加到当前游标位置的查询中。 查询不会自动运行。 双击某个实体时，此操作是默认操作。 生成查询时，请使用此操作。  

       - **查询全部**：针对此实体运行查询（包含所有属性）。 使用此操作可快速查询单个实体。  

       - **按设备查询**：针对此实体运行查询并对结果进行分组。 例如 `Disk | summarize dcount( Device ) by Name`  

    - 展开实体以查看每个实体可用的特定属性。 双击某个属性，将其添加到当前游标位置的查询。  

3. “主页”选项卡显示有关 CMPivot 的常规信息，包括示例查询和支持文档的链接  。  

4. “查询”选项卡显示查询窗格、结果窗格和状态栏  。 在上面的屏幕截图示例中选中了“查询”选项卡。  

5. 通过查询窗格，可以在集合中生成或键入要在客户端上运行的查询。  

    - CMPivot 使用 [Kusto 查询语言 (KQL)](https://docs.microsoft.com/azure/kusto/query/) 子集。  

    - 在查询窗格中剪切、复制或粘贴内容。  

    - 默认情况下，此窗格使用 IntelliSense。 例如，如果开始键入 `D`，IntelliSense 会建议以该字母开头的所有实体。 选择一个选项，然后按 Tab 将其插入。 键入一个管道字符和一个空格 `| `，然后 IntelliSense 便会建议所有表运算符。 插入 `summarize` 并键入空格，IntelliSense 会建议所有聚合函数。 有关这些运算符和函数的详细信息，请单击 CMPivot 中的“主页”选项卡  。  

    - 查询窗格还提供以下选项：  

        - 运行该查询。  

        - 在查询历史记录列表中前后移动。  

        - 创建直属成员资格集合。  

        - 将查询结果导出到 CSV 或剪贴板。  

6. 结果窗格会显示活动客户端针对查询返回的数据。  

   - 可用的列视实体和查询而定。  

   - 单击列名以按照该属性对结果进行排序。  

   - 右键单击任何列名，按照该列中的相同信息对结果进行分组，或者排序。  

   - 右键单击设备名称，在设备上执行以下附加操作：  

      - **切换到**：查询此设备上的其他实体。  

      - **运行脚本**：启动“运行脚本”向导，在此设备上运行现有 PowerShell 脚本。 有关详细信息，请参阅[运行脚本](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script)。  

      - **远程控制**：在此设备上启动 Configuration Manager 远程控制会话。 有关详细信息，请参阅[如何远程管理 Windows 客户端计算机](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer)。  

      - **资源浏览器**：启动此设备的 Configuration Manager 资源浏览器。 有关详细信息，请参阅[查看硬件清单](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory)或[查看软件清单](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory)。  

   - 右键单击任何非设备单元格，以执行以下附加操作：  

     - **复制**：将单元格的文本复制到剪贴板。  

     - **显示具备以下条件的设备**：查询具有此属性值的设备。 例如，从 `OS` 查询的结果中，在“版本”行中的单元格上选择此选项：`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **显示不具备以下条件的设备**：查询没有此属性值的设备。 例如，从 `OS` 查询的结果中，在“版本”行中的单元格上选择此选项：`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **使用必应进行搜索**：使用此值作为查询字符串，启动默认 Web 浏览器以转到 www.bing.com 。  

   - 单击任何超链接文本，可转到针对该特定信息的视图。  

   - 结果窗格显示的行不会超过 20,000 个。 调整查询以进一步筛选数据，或者在较小的集合上重新启动 CMPivot。  

7. 状态栏显示以下信息（从左到右）：  

   - 目标集合的当前查询状态。 此状态包括：  
     - 完成查询的活动客户端数量 (3)  
     - 客户端总数 (5)  
     - 脱机客户端数量 (2)  
     - 返回失败的任何客户端 (0)  

       例如：`Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - 客户端操作的 ID。 例如：`id(16780221)`  

   - 当前集合。 例如：`PM_Team_Machines`  

   - 结果窗格中的总行数。 例如 `1 objects`  



## <a name="example-scenarios"></a>方案示例

以下部分提供了有关如何在环境中使用 CMPivot 的示例：


### <a name="example-1-stop-a-running-service"></a>示例 1：停止正在运行的服务

安全管理员要求尽快对会计部门的所有设备停止并禁用计算机浏览器服务。 可对会计部门中所有设备的集合启动 CMPivot，并在“Service”实体上选择“查询全部”   。 

`Service`

显示结果时，右键单击“Name”列，然后选择“分组依据”   。 

`Service | summarize dcount( Device ) by Name`

在“浏览器”服务的行中，单击“dcount_”列中的超链接数字   。 

`Service | where (Name == 'Browser') | summarize count() by Device`

可以选择多个设备，右键单击所选设备，然后选择“运行脚本”  。 此操作将启动“运行脚本”向导，你可以通过该向导运行用于停止和禁用服务的现有脚本。 借助 CMPivot，可以快速响应所有活动计算机的安全事件，并在“运行脚本”向导中查看结果。 然后继续创建配置基线，以修复集合中的其他计算机，因为它们将来会变为活动状态。 

![浏览器服务和“运行脚本”操作的 CMPivot 示例](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>示例 2：主动解决应用程序故障  

为主动进行操作维护，可每周一次对管理的服务器集合运行 CMPivot，并在“AppCrash”实体上选择“查询所有”   。 右键单击“FileName”列，然后选择“升序排序”   。 一台设备会为 sqlsqm.exe 返回七个结果，时间戳大约为每天 03:00。 你可以在其中一行中选择文件名，右键单击该名称，然后选择“使用必应进行搜索”  。 在 Web 浏览器中浏览搜索结果时，可找到有关此问题的 Microsoft 支持文章，其中会包含详细信息和解决方案。 


### <a name="example-3-bios-version"></a>示例 3：BIOS 版本

若要[缓解推测执行端通道漏洞](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/)，其中一个要求就是更新系统 BIOS。 首先查询 BIOS 实体  。 然后按“Version”属性进行分组   。 再右键单击某个特定值，例如“LENOVO - 1140”，并选择“显示具备以下条件的设备”  。  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>示例 4：可用磁盘空间

需要在网络文件服务器上临时存储大型文件，但不确定哪个磁盘拥有足够的容量。 对文件服务器集合启动 CMPivot，并查询“Disk”实体  。 修改 CMPivot 的查询以快速返回包含实时存储数据的活动服务器列表：  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="bkmk_cmpivot"></a> 从版本 1810 开始的 CMPivot
<!--1359068, 3607759-->

从 Configuration Manager 版本 1810 开始，CMPivot 就包括以下改进：

- [CMPivot 实用工具和性能](#bkmk_cmpivot-perf)
- [标量函数](#bkmk_cmpivot-functions)  
- [呈现可视化效果](#bkmk_cmpivot-charts)  
- [硬件清单](#bkmk_cmpivot-hinv)  
- [标量运算符](#bkmk_cmpivot-operators)  
- [查询摘要](#bkmk_cmpivot-summary)  
- [审核状态消息](#cmpivot-audit-status-messages)

### <a name="bkmk_cmpivot-perf"></a> CMPivot 实用工具和性能

- CMPivot 最多返回 100,000 个单元格而不是 20,000 行。
  - 如果实体有 5 个属性，即表示将显示 5 列和最多 20,000 行。
  - 对于有 10 个属性的实体，最多显示 10,000 行。
  - 显示的总数据将小于或等于 100,000 个单元格。
- 在“查询摘要”选项卡上，选择“故障”或“脱机”设备的计数，然后选择“创建集合”选项。  使用此选项，可通过修正部署轻松定位这些设备。
- 通过单击文件夹图标保存收藏夹查询  。
   ![在 CMPivot 中保存收藏夹查询的示例](media/cmpivot-favorite.png)

- 更新至 1810 版本的客户端会通过快速信道将不超过 80 KB 的输出返回到站点。
  - 这一更改提高了查看脚本或查询输出的性能。
  - 如果脚本或查询输出大于 80 KB，客户端会通过状态消息发送数据。
  - 如果客户端未更新至 1810 客户端版本，它将继续使用状态消息。

### <a name="bkmk_cmpivot-functions"></a>标量函数
CMPivot 支持下列标量函数：
- **ago()** ：从当前的 UTC 时钟时间减去给定的时间跨度  
- **datetime_diff()** :计算两个日期/时间值之间的日历间隔  
- **now()** ：返回当前 UTC 时钟时间  
- **bin()** ：将值舍入为给定装箱大小的整数倍数  

> [!Note]  
> 日期/时间数据类型表示某个时刻，通常表示为当天的日期和时间。 时间值以 1 秒为单位进行测量。 日期/时间值始终位于 UTC 时区中。 始终采用 ISO 8601 格式表示日期时间文本，例如 `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>示例
- `datetime(2015-12-31 23:59:59.9)`：特定的日期时间文本   
- `now()`：当前时间  
- `ago(1d)`：当前时间减去一天  


### <a name="bkmk_cmpivot-charts"></a> 呈现可视化效果

CMPivot 现在包括对 KQL [render 运算符](https://docs.microsoft.com/azure/kusto/query/renderoperator)的基本支持。 此支持包括以下类型：  
- **条形图**：第一列是 x 轴，可以为文本、日期/时间或数值。 第二个列必须是数字，并显示为水平条带。  
- **柱形图**：与条形图类似，带有垂直条带而不是水平条带。  
- **饼图**：第一列是颜色轴，第二列是数值。  
- **时间图**：折线图。 第一列是 x 轴，且应为日期/时间。 第二列是 y 轴。  

#### <a name="example-bar-chart"></a>示例：条形图
以下查询以条形图呈现最近使用的应用程序：

```
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```
![CMPivot 条形图可视化效果示例](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>示例：时间图
要呈现时间图，请使用新的 bin() 运算符对某段时间的事件进行分组  。 以下查询显示过去七天内设备启动的时间：

``` 
OperatingSystem 
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```
![CMPivot 时间图可视化效果示例](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>示例：饼图
以下查询显示饼图中的所有 OS 版本：

```
OperatingSystem 
| summarize count() by Caption
| render piechart
```
![CMPivot 饼图可视化效果示例](media/1359068-cmpivot-piechart.png)


### <a name="bkmk_cmpivot-hinv"></a>硬件清单
使用 CMPivot 查询任何硬件清单类。 这些类包括对硬件清单所做的任何自定义扩展。 CMPivot 立即返回存储在站点数据库中的上次硬件清单扫描的缓存结果。 同时，它会根据需要使用来自任何在线客户端的实时数据更新结果。

结果表或图表中数据的颜色饱和度表示数据是实时的还是缓存的。 例如，深蓝色是来自在线客户端的实时数据。 浅蓝色是缓存数据。

#### <a name="example"></a>示例
```
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```
![带柱形图可视化效果的 CMPivot 清单查询示例](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>限制
- 以下硬件清单实体不受支持：  
    - 数组属性，例如 IP 地址  
    - Real32/Real64 <!--example?-->  
    - 嵌入的对象属性 <!--example?-->  
- 清单实体名称必须以字符开头
- 不能通过创建具有相同名称的清单实体覆盖内置实体  


### <a name="bkmk_cmpivot-operators"></a>标量运算符
CMPivot 包括以下标量运算符：  

> [!Note]  
> - LHS：运算符左侧的字符串  
> - RHS：运算符右侧的字符串  


|运算符|说明|示例（生成 true）|
|--------|-----------|---------------------|
|==|等于|`"aBc" == "aBc"`|
|!=|不等于|`"abc" != "ABC"`|
|like|LHS 包含 RHS 的匹配项|`"FabriKam" like "%Brik%"`|
|!like|LHS 不包含 RHS 的匹配项|`"Fabrikam" !like "%xyz%"`|
|包含|RHS 以 LHS 子序列的形式存在|`"FabriKam" contains "BRik"`|
|!contains|LHS 中未出现 RHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS 是 LHS 的初始子序列|`"Fabrikam" startswith "fab"`|
|!startswith|RHS 不是 LHS 的初始子序列|`"Fabrikam" !startswith "kam"`|
|endswith|RHS 是 LHS 的闭合子序列|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS 不是 LHS 的闭合子序列|`"Fabrikam" !endswith "brik"`|


### <a name="bkmk_cmpivot-summary"></a>查询摘要

选择 CMPivot 窗口底部的“查询摘要”选项卡  。 此状态可帮助你识别离线的客户端，或排查可能发生的故障。 在“计数”列中选择一个值以打开具有该状态的特定设备的列表。 

例如，选择状态为“故障”的设备的计数。 请查看特定的错误消息，并导出这些设备列表。 如果错误是无法识别的特定 cmdlet，请使用导出的设备列表创建集合以部署 Windows PowerShell 更新。  

### <a name="cmpivot-audit-status-messages"></a>CMPivot 审核状态消息

从版本 1810 开始，运行 CMPivot 时，MessageID 40805 会创建审核状态消息  。 可通过转到“监视” < “系统状态” < “状态消息查询”    查看状态消息。 可为指定用户运行所有审核状态消息，为指定站点运行所有审核状态消息，或创建自己的状态消息查询   。

消息使用以下格式：

MessageId 40805:User &lt;UserName> ran script &lt;Script-Guid> with hash &lt;Script-Hash> on collection &lt;Collection-ID>。

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 是 CMPivot 的 Script-Guid。
- 可以在客户端的 scripts.log 文件中查看 Script-Hash。
- 也可以查看存储在客户端脚本分数中的哈希。 客户端上的文件名为 &lt;Script-Guid>_&lt;Script-Hash>。
    - 示例文件名：C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![CMPivot 审核状态消息示例](media/cmpivot-audit-status-message.png)

## <a name="bkmk_cmpivot1902"></a> 从版本 1902 开始的 CMPivot
<!--3610960-->
从 Configuration Manager 版本 1902 开始，可以在层次结构中从管理中心站点 (CAS) 运行 CMPivot。 主站点仍可处理与客户端的通信。 从管理中心站点运行 CMPivot 时，它将通过高速消息订阅通道与主站点通信。 该通信不依赖于站点之间的标准 SQL 复制。

当 SQL 或提供程序不在同一台计算机上时，或在 SQL Always On 配置的情况下，在 CAS 上运行 CMPivot 将需要其他权限。 使用这些远程配置，即可为 CMPivot 配置“双跃点方案”。

要在这种“双跃点方案”中让 CMPivot 使用 CAS，可以定义约束委派。 若要了解此配置的安全隐患，请阅读 [Kerberos 约束委派](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview)一文。 如果正在使用或未使用 CAS 并置多个远程配置（例如 SQL 或 SCCM 提供程序），可能需要权限设置组合。 下面是你需要遵循的步骤：

### <a name="cas-has-a-remote-sql-server"></a>CAS 具有远程 SQL Server

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 远程 SQL Server 和 CAS 站点服务器添加到 [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess) 组。
   ![主站点 SQL Server 上的 Configmgr_DviewAccess 组](media/cmpivot-dviewaccess-group.png)
1. 转到 Active Directory 用户和计算机。
   1. 对于每个主站点服务器，请右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加 CAS SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 对于 CAS 站点，请右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！

   ![双跃点的 CMPivot AD 委派示例](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CAS 具有远程提供程序

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 提供程序计算机帐户和 CAS 站点服务器添加到 [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess) 组。
1. 转到 Active Directory 用户和计算机。
   1. 选择 CAS 提供程序计算机，右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 选择 CAS 站点服务器，右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
1. 重启 CAS 远程提供程序计算机。

### <a name="sql-always-on"></a>SQL Always On

1. 请转到每个主站点的 SQL Server。
   1. 将 CAS 站点服务器添加到 [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess) 组。
1. 转到 Active Directory 用户和计算机。
   1. 对于每个主站点服务器，请右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例为 SQL 节点添加 CAS SQL Server 服务帐户。
      1. 请确保这些更改与公司安全策略保持一致！
   1. 选择 CAS 站点服务器，右键单击并选择“属性”  。
      1. 在委托选项卡上，选择第三个选项，“仅信任此计算机委派指定的服务”  。 
      1. 选择“仅使用 Kerberos”  。
      1. 使用端口和实例添加每个主站点的 SQL Server 服务。
      1. 请确保这些更改与公司安全策略保持一致！
1. 请确保 [SPN 发布](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs)使用 CAS SQL 侦听器名称和每个主 SQL 侦听器名称。
1. 重启主 SQL Server。
1. 重启 CAS 站点服务器和 CAS SQL Server。


## <a name="inside-cmpivot"></a>深入了解 CMPivot

CMPivot 使用 Configuration Manager“快速通道”向客户端发送查询。 其他功能也使用这个从服务器到客户端的信道，例如客户端通知操作、客户端状态和 Endpoint Protection。 客户端通过类似的快速状况消息系统返回结果。 状况消息临时存储在数据库中。 如需深入了解用于客户端通知的端口，请参阅[端口](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsClient-MP)一文。

查询和结果都只是文本。 InstallSoftware 和 Process 实体均返回一些最大的结果集   。 性能测试期间，对于这些查询而言，来自一个客户端的最大状态消息文件大小小于 1 KB  。 扩展到包含 50,000 个活动客户端的大型环境后，此一次性查询将在网络上生成不超过 50 MB 的数据。 欢迎页上所有带下划线的项，每个客户端将返回不超过 1k 的信息。

![CMPivot 带下划线的实体示例](media/cmpivot-underlined-entities.png)

从 Configuration Manager 1810 开始，CMPivot 可以查询硬件清单数据，包括扩展的硬件清单类。 这些新实体（欢迎页上不带下划线的实体）可能返回更大的数据集，具体取决于给定硬件清单属性定义的数据量。 例如，“InstalledExecutable”实体每客户端可能会返回多个 MB 数据，具体取决于查询的特定数据。 使用 CMPivot 从更大的集合中返回更大的硬件清单数据集时，请注意性能和可伸缩性。

查询在一小时后超时。 例如，一个集合有 500 台设备，450 个客户端当前处于联机状态。 这些活动设备接收查询后，几乎可以立即返回结果。 如果打开 CMPivot 窗口，当其他 50 个客户端联机时，它们也会收到查询并返回结果。 

## <a name="log-files"></a>日志文件

 CMPivot 交互将记录到以下日志文件：

 服务器端：
- SmsProv.log
- BgbServer.log
- StateSys.log

 客户端：
 - CCMNotificationAgent.log
 - Scripts.log
 - StateMessage.log

有关详细信息，请参阅[日志文件](/sccm/core/plan-design/hierarchy/log-files)和[CMPivot 疑难解答](/sccm/core/servers/manage/cmpivot-tsg)。

## <a name="next-steps"></a>后续步骤
 
[CMPivot 疑难解答](/sccm/core/servers/manage/cmpivot-tsg)

[创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)


