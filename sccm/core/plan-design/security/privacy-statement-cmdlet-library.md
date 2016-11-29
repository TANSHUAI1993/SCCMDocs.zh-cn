---
title: "System Center Configuration Manager 隐私声明 – Configuration Manager Cmdlet 库"
description: "了解 Microsoft 如何收集和使用与 System Center Configuration Manager Cmdlet 库相关的数据。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager 隐私声明 – Configuration Manager Cmdlet 库

*适用范围：System Center Configuration Manager (Current Branch)*

本隐私声明涵盖 System Center Configuration Manager Cmdlet 库的功能。  

## <a name="usage-data"></a>使用数据  
 **此功能的作用：**   
System Center Configuration Manager Cmdlet 库允许你通过使用 Windows PowerShell cmdlet 和脚本来管理 Configuration Manager 层次结构。 Cmdlet 库收集有关你如何使用库中包含的 cmdlet 来确定趋势和使用模式的信息。  Cmdlet 库还会收集你在使用 cmdlet 时所遇到错误的类型和数目信息。  

 **收集、处理或传输的信息：**   
收集的使用数据包括 cmdlet 的开始、停止和终止，不推荐使用的 cmdlet 的运行，以及与这些 cmdlet 相关的 SMS 提供程序操作的活动指标。 此类信息不能确定个人身份。  收集的错误信息包括 cmdlet 返回的错误以及异常错误的详情。 某些错误详情报告可能无意中包含个人身份标识符，如连接到你计算机的设备的序列号。 Cmdlet 库筛选器并匿名化错误报告中包含的信息，以删除所有个人身份标识符，然后再将错误报告发送给 Microsoft。  

 **信息的用途：**   
我们利用此信息来提高所提供产品和服务的质量、安全性和完整性。  

 **选择/控制：**   
此“使用数据”功能默认处于启用状态。 System Center Configuration Manager Cmdlet 库包括两个注册表项来控制此功能。  

 若要完全退出，你需要设置这两个注册表项的值，每个值针对一个 Windows 事件跟踪 (ETW) 提供程序：  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0（驱动提供程序“使用数据”功能的退出）  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0（cmdlet“使用数据”功能的退出）  

 “使用数据”设置的更改特定于在其中进行更改的计算机。  

 有关如何配置“使用数据”（集合）的信息，请参见 [System Center Configuration Manager Cmdlet 库文档](https://technet.microsoft.com/en-us/library/dn958404.aspx)。  

## <a name="update-check"></a>更新检查  
 **此功能的作用：**   
System Center Configuration Manager Cmdlet 库每天都会自动检查库更新，并通知你下载更新的库。  

 **收集、处理或传输的信息：**   
Cmdlet 库更新检查将从 Microsoft 下载中心下载一个小文本文件，以执行版本检查。   此文件不存储在本地。  Cmdlet 库不会自动升级软件。  

 **信息的用途：**   
我们利用此信息来提高所提供产品和服务的质量、安全性和完整性。  

 **选择/控制：**   
“更新检查”功能默认处于启用状态。  System Center Configuration Manager Cmdlet 库包括以下 cmdlet 来控制更新通知功能：  

-   `Get-CMCmdletUpdateCheck` 获取更新功能配置，并将指示系统策略是否会重写用户策略。  

-   `Send-CMCmdletUpdateCheck` 允许执行计划外的更新检查。 计划外的检查不考虑策略设置。  

-   `Set-CMCmdletUpdateCheck` 在每个用户或每个系统的基础上配置更新检查设置。 你必须以管理员身份运行才能设置系统设置。  

 有关如何配置更新的详细信息，请查看 [System Center Configuration Manager Cmdlet 库文档](https://technet.microsoft.com/en-us/library/dn958404.aspx)。  



<!--HONumber=Nov16_HO1-->


