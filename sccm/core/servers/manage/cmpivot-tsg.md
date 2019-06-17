---
title: CMPivot 疑难解答
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中对 CMPivot 进行故障排除。
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8cada39ac2514b6e2c7a6dabbbc54e7585ee7c9b
ms.sourcegitcommit: 7dd42b5a280e64feb69a947dae082fdaf1571272
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66716018"
---
# <a name="troubleshooting-cmpivot"></a>CMPivot 疑难解答

CMPivot 是一种控制台中实用工具，现提供对环境中设备实时状态的访问。 它立即对目标集合中的所有连接设备运行查询，并返回结果。 有时，你可能会发现自己需要对 CMPivot 进行故障排除。 例如，可能会看到客户端发送 CMPivot 状态消息。 但是，站点服务器不处理消息，因为它已损坏。 可通过本文了解 CMPivot 的信息流。

## <a name="get-information-from-the-site-server"></a>从站点服务器中获取信息

默认情况下，日志文件位于 C:\Program Files\Microsoft Configuration Manager\logs 中。 此位置可能会有变化，具体取决于为安装目录指定的位置，如果卸载项（例如 SMS 提供程序）到另一台服务器，此位置也会不同。

查看此行的 smsprov.log  ：

```
Auditing: User <username> initiated client operation 135 to collection <CollectionId>.
```

在 CMPivot 窗口中查找 ID。 此 ID 为 ClientOperationID  。

![突出显示 ClientOperationID 的 CMPivot 窗口](media/cmpivot-clientoperationid.png)

在 ClientAction 表中查找 TaskID  。 TaskID 对应 ClientAction 表中的 UniqueID   。 

```SQL
select * from ClientAction where ClientOperationId=<id>
```

在 BgbServer.log 中查找从 SQL 中收集的 TaskID   。 在 Bgbserver.log 中，它将标记为 TaskGUID  。 例如： 


   - 开始将推送任务 (PushID:260 TaskID:258 TaskGUID:**F8C7C37F-B42B-4C0A-B050-2BB44DF1098A** TaskType:15 TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0 UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW 1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2 NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW 1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU 2NyaXB0Q29udGVudD4=-) 发送到具有限制的 5 个客户端（策略：1 个参数：42）已完成将推送任务 (PushID:260 TaskID:258）发送到 5 个客户端

## <a name="client-logs"></a>客户端日志

获得来自站点服务器的信息后，请查看客户端日志。 默认情况下，客户端日志位于 C:\Windows\CCM\Logs。

查看 CcmNotificationAgent.log  。 你会找到以下项的日志：  

   - **错误！未定义书签。** +PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0 UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW 1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2 NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW 1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU 2NyaXB0Q29udGVudD4=-

查看 TaskID 的 Scripts.log   。 在以下示例中，可以看到“任务 ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}”  ：

```
Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
State message: Task Id {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A} Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

查看 StateMessage.log  。 示例 TaskID 位于 &lt;Param> 旁的消息的底部  。 应看见类似于下面的行：

```xml
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
StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

> [!NOTE]
> 只有为 SMS_STATE_SYSTEM 组件启用详细日志记录后，StateSys.log 中的上述日志项目才可见，可通过修改下面的注册表项来启用它：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_STATE_SYSTEM\详细日志记录 = 1（默认值为 0）

## <a name="review-messages-on-the-site-server"></a>审阅站点服务器上的消息

打开 statesys.log，查看否已收到和处理消息  。 示例 TaskID 位于 &lt;Param> 旁的消息的底部  。

```xml
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

```SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

## <a name="next-steps"></a>后续步骤

[使用 CMPivot](/sccm/core/servers/manage/cmpivot)

[创建并运行 PowerShell 脚本](/sccm/apps/deploy-use/create-deploy-scripts)
