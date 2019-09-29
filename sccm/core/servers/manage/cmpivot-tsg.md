---
title: CMPivot 疑难解答
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中对 CMPivot 进行故障排除。
ms.date: 09/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09c748e563ea6410b7f2ebc842c77707cf29494a
ms.sourcegitcommit: 013596de802ac0eb416118169ad049733b5a63e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71198199"
---
# <a name="troubleshooting-cmpivot"></a>CMPivot 疑难解答

CMPivot 是一种实用工具，它提供对环境中设备实时状态的访问。 它立即对目标集合中的所有连接设备运行查询，并返回结果。 有时，你可能会发现自己需要对 CMPivot 进行故障排除。 例如，可能会看到客户端发送 CMPivot 状态消息。 但是，站点服务器不处理消息，因为它已损坏。 可通过本文了解 CMPivot 的信息流。

## <a name="bkmk_CMPivot-1902"></a> 版本 1902 及更高版本中的 CMPivot 故障排除

从 Configuration Manager 版本 1902 开始，可以在层次结构中从管理中心站点 (CAS) 运行 CMPivot。 主站点仍可处理与客户端的通信。 从管理中心站点运行 CMPivot 时，它将通过高速消息订阅通道与主站点通信。 该通信不依赖于站点之间的标准 SQL 复制。 若是远程 SQL Server 或提供程序，或使用 SQL Always On，将获得 CMPivot“双跃点方案”。 有关如何为“双跃点方案”定义约束委派的信息，请参阅[自版本 1902 起的版本中的 CMPivot](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1902)。

>[!IMPORTANT]
> 排除 CMPivot 故障时，启用 MP 的详细日志记录以及站点服务器的 SMS_MESSAGE_PROCESSING_ENGINE，以获取更多信息。 若客户端的输出超过 80 KB，则启用 MP 的详细日志记录以及站点服务器的 SMS_STATE_SYSTEM 组件。 有关启用详细日志记录的信息，请参阅[站点服务器日志记录选项](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site)。

### <a name="get-information-from-the-site-server"></a>从站点服务器中获取信息

默认情况下，日志文件位于 C:\Program Files\Microsoft Configuration Manager\logs 中。 此位置可能会有变化，具体取决于为安装目录指定的位置，如果卸载项（例如 SMS 提供程序）到另一台服务器，此位置也会不同。 若正在从 CAS 运行 CMPivot，日志将位于主站点服务器。

查看下列行的 smsprov.log  ：

- Configuration Manager 版本 1906：
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager 版本 1902：
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>



7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 是 CMPivot 的 Script-Guid。  也可以从 [CMPivot 审核状态消息](/sccm/core/servers/manage/cmpivot#cmpivot-audit-status-messages)查看此 GUID。

接下来，在 CMPivot 窗口中查找 ID。 此 ID 为 ClientOperationID  。

![突出显示 ClientOperationID 的 CMPivot 窗口](media/cmpivot-client-operationid-1902.png)

在 ClientAction 表中查找 TaskID  。 TaskID 对应 ClientAction 表中的 UniqueID   。

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

在 BgbServer.log 中查找从 SQL 中收集的 TaskID   ，并记录 PushID  。 在 Bgbserver.log 中，TaskID 将标记为 TaskGUID   。 例如：

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>客户端日志

获得来自站点服务器的信息后，请查看客户端日志。 默认情况下，客户端日志位于 C:\Windows\CCM\Logs。

查看 CcmNotificationAgent.log  。 你会找到类似下列行的日志条目：  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

查看 TaskID 的 Scripts.log   。 在下面的示例中将看到任务 ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}： 

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> 若未在 Scripts.log 中看到“(fast)”，则数据可能超过 80 KB。  在此示例中会将此信息作为状态消息发送到站点服务器。 使用客户端的 StateMessage.log 以及站点服务器的 Statesys.log。  

### <a name="review-messages-on-the-site-server"></a>审阅站点服务器上的消息

在管理点上启用[详细日志记录](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-client)后，可以看到处理传入客户端消息的方式。 在 MP_RelayMsgMgr.log 中查找 TaskID。  

MP_RelayMsgMgr.log 示例显示了客户端 ID (GUID:83F67728-2E6D-4E4F-8075-ED035C31B783) 以及任务 ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}。   为客户端响应分配消息 ID，然后将响应发送给消息处理引擎：

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

在 MS_MESSAGE_PROCESSING_ENGINE.log 上启用[详细日志记录](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_logoptions)后，将显示正在处理客户端结果。  请使用从 MP_RelayMsgMgr.log 中找到的消息 ID。  处理日志条目类似于以下示例条目：

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

  - 若在处理期间收到异常，可以运行以下 SQL 查询并查看“异常”列来查看它。 处理消息后，它将不再在 MPE_RequestMessages_Instant 表中。

    ```SQL
    select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
    ```

在 BgbServer.log 中，查找 PushID，查看上报或发生故障的客户端数。  

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

使用 TaskID 查看来自 SQL 的 CMPivot 监视视图  。

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

![版本 1902 中用于故障排除的 CMPivot SQL 查询](media/cmpivot-sql-queries-1902.png)

## <a name="bkmk_CMPivot-1810"> 1810 及早期版本中的 CMPivot 故障排除</a>

### <a name="get-information-from-the-site-server"></a>从站点服务器中获取信息

默认情况下，日志文件位于 C:\Program Files\Microsoft Configuration Manager\logs 中。 此位置可能会有变化，具体取决于为安装目录指定的位置，如果卸载项（例如 SMS 提供程序）到另一台服务器，此位置也会不同。

查看此行的 smsprov.log  ：

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

在 CMPivot 窗口中查找 ID。 此 ID 为 ClientOperationID  。

![突出显示 ClientOperationID 的 CMPivot 窗口](media/cmpivot-clientoperationid.png)

在 ClientAction 表中查找 TaskID  。 TaskID 对应 ClientAction 表中的 UniqueID   。 

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

在 BgbServer.log 中查找从 SQL 中收集的 TaskID   。 在 Bgbserver.log 中，它将标记为 TaskGUID  。 例如：

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>客户端日志

获得来自站点服务器的信息后，请查看客户端日志。 默认情况下，客户端日志位于 C:\Windows\CCM\Logs。

查看 CcmNotificationAgent.log  。 你会找到以下项的日志：  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

查看 TaskID 的 Scripts.log   。 在以下示例中，可以看到“任务 ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}”  ：

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

查看 StateMessage.log  。 示例 TaskID 位于 \<Param> 旁的消息的底部  。 应看见类似于下面的行：

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>审阅站点服务器上的消息

打开 statesys.log，查看否已收到和处理消息  。 示例 TaskID 位于 \<Param> 旁的消息的底部  。 必须在 SMS_STATE_SYSTEM 组件上启用[详细日志记录](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_logoptions)，才能看到这些日志条目。  

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

如果未看到消息已被处理，请查看状态消息收件箱。 收件箱的默认位置为 C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\。 文件将位于以下任一位置：
  
- 传入
- 已损坏
- 过程

使用 TaskID 查看来自 SQL 的 CMPivot 监视视图  。

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>对于使用版本 1810 或更高版本的客户端，只有输出超过 80 KB 时，才会使用状态处理。 在这些情况下排除 CMPivot 故障时，请启用 MP 的详细日志记录以及站点服务器的 SMS_MESSAGE_PROCESSING_ENGINE，以获取更多信息。 有关启用详细日志记录的信息，请参阅[站点服务器日志记录选项](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site)。
> 
> 使用以下日志进行故障诊断：
> - MP_Relay.log
> - SMS_MESSAGE_PROCESSING_ENGINE.log

## <a name="next-steps"></a>后续步骤

[使用 CMPivot](/sccm/core/servers/manage/cmpivot)

[创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)
