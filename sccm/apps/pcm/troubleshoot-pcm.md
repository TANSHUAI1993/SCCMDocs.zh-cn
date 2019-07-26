---
title: 包转换管理器故障排除
titleSuffix: Configuration Manager
description: 了解如果解决 Configuration Manager 中包转换管理器的问题。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 475f80dc4d5841eb014b8f1ecb4d23ffdb699944
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339197"
---
# <a name="troubleshoot-package-conversion-manager"></a>包转换管理器故障排除

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1357861-->

当使用包转换管理器时，使用本文中的信息帮助你进行故障排除。



## <a name="sms-provider"></a>SMS 提供程序

包转换管理器使用 SMS 提供程序。 有关详细信息，请参阅[规划 SMS 提供程序](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)。

如果 SMS 提供程序不能正常工作，包含包转换管理器的 Configuration Manager 控制台将不起作用。



## <a name="package-readiness"></a>包准备情况

在将包转换为应用程序之前，使用包转换管理器“分析”  功能对包进行分析。 完成分析后，在 Configuration Manager 控制台的“包”  节点中添加“准备情况”  列。 包列表显示已分析包的以下就绪状态之一：

-  自动：可以使用“转换”  功能直接转换包。      

  > [!NOTE]  
  > 自动转换不会将 WQL 查询转换为应用程序要求。 使用“修复和转换”  过程来转换这些查询。  

-  手动：包需要一些添加或修改才能使用“修复和转换”  功能进行转换。  

-  不适用：包不适合进行转换。 请更正包存在的任何问题，或继续将其部署为一个包。  

-  错误：包中包含错误。 手动更正这些错误后，才能进行分析和转换。  

Configuration Manager 控制台中“包”  节点的细节窗格显示任何准备情况问题。 选择一个包，然后在细节窗格中选择“摘要”  选项卡。



## <a name="log-files"></a>日志文件

### <a name="enable-logging"></a>启用日志记录

启用包转换管理器的日志记录时，它会记录其所有操作、异常和错误。 

若要在 Configuration Manager 中启用此组件的日志记录，请修改 Microsoft.ConfigurationManagement.exe.Config  。默认情况下，此配置文件位于以下路径：  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

在 system.diagnostics  元素中，在最后一个 sources  元素后插入以下 switches  和 trace  XML 元素：

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

此示例使用文件 PCMTrace.log  。 此日志在运行 Configuration Manager 控制台的计算机上，位于以下路径：  
`%UserProfile%\AppData\Local\Temp`

若要配置详细级别，请更改“PcmLogging”  跟踪开关设置。 将该值设置为四个详细级别，从最不详细 (`1`) 到最详细 (`4`)。


### <a name="smsprovlog"></a>SMSProv.log

在某些情况下，与包转换过程的故障排除相关的信息位于 SMSProv.log  文件中。 此文件捕获来自 Configuration Manager SMS 提供程序的信息。

默认情况下，此日志文件位于以下路径的 Configuration Manager 站点服务器上：  
`C:\Program Files\Microsoft Configuration Manager\Logs`

如果看到以下错误消息之一，SMSProv.log  文件可能包含相关故障排除信息：

- `The SMS Provider reported an error`

- `Generic Failure`

这些错误消息通常指示站点服务器上发生了错误，并且错误信息未被发送到 Configuration Manager 控制台。

有关详细信息，请参阅[包转换管理器错误消息的技术参考](/sccm/apps/pcm/error-messages)。



## <a name="changing-package-attributes-after-analysis"></a>分析后更改包属性

对包进行分析后且包的就绪状态为“自动”  或“手动”  ，如果更改了任何相关属性，转换过程可能就会失败。

例如，你对包进行分析且其就绪状态为“自动”  。 然后你将另一个程序添加到包。 包转换可能会失败。

如果需要在分析后对包进行更改，请在转换前重新运行分析。 



## <a name="see-also"></a>另请参阅

[包转换管理器错误消息的技术参考](/sccm/apps/pcm/error-messages)
