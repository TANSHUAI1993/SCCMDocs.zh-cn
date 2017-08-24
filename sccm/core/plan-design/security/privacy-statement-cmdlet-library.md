---
title: "System Center Configuration Manager 隐私声明 - Configuration Manager cmdlet 库 | Microsoft Docs"
description: "了解 Microsoft 如何收集和使用与 System Center Configuration Manager cmdlet 库相关的数据。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3936075555cc0bb370ea6e42c7e720b864d565f7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager 隐私声明 – Configuration Manager cmdlet 库

*适用范围：System Center Configuration Manager (Current Branch)*

本隐私声明涵盖 System Center Configuration Manager Cmdlet 库的功能。  

## <a name="usage-data"></a>使用情况数据  
 **此功能的作用：**   
System Center Configuration Manager cmdlet 库允许通过使用 Windows PowerShell cmdlet 和脚本来管理 Configuration Manager 层次结构。 Cmdlet 库收集有关如何使用库中的 cmdlet 来确定趋势和使用模式的信息。 Cmdlet 库还会收集使用 cmdlet 时遇到的错误类型和数目信息。  

 **收集、处理或传输的信息：**   
收集的使用数据包括 cmdlet 的开始、停止和终止数据，弃用的 cmdlet 运行数据，以及与这些 cmdlet 相关的 Systems Management Server (SMS) 提供程序操作的活动指标。 此类信息不能确定个人身份。  收集的错误信息包括 cmdlet 返回的错误以及异常错误的详情。 某些错误详情报告可能无意中包含个人身份标识符，如连接到计算机的设备的序列号。 Cmdlet 库筛选并匿名化错误报告中的信息，以删除个人身份标识符，然后再将错误报告发送给 Microsoft。  

 **信息的用途：**   
我们利用此信息来提高所提供产品和服务的质量、安全性和完整性。  

 **选择/控制：**   
此“使用数据”功能默认处于启用状态。 System Center Configuration Manager cmdlet 库具有控制此功能的两个注册表项。  

 若要完全退出，你需要设置这两个注册表项的值，每个值针对一个 Windows 事件跟踪 (ETW) 提供程序：  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0（驱动提供程序“使用数据”功能的退出）  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0（cmdlet“使用数据”功能的退出）  

 “使用数据”设置的更改特定于在其中进行更改的计算机。  

 有关如何配置使用数据（集合）的详细信息，请参阅 [System Center Configuration Manager Cmdlet 库文档](https://technet.microsoft.com/en-us/library/dn958404.aspx)。   
