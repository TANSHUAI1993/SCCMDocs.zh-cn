---
title: Configuration Manager Cmdlet 库的隐私声明
description: 了解 Microsoft 如何收集和使用与 System Center Configuration Manager cmdlet 库相关的数据。
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6a996c4f1e00c05c0b3766b8955130529832063
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager 隐私声明 – Configuration Manager cmdlet 库

*适用范围：System Center Configuration Manager (Current Branch)*

本隐私声明涵盖 System Center Configuration Manager Cmdlet 库的功能。  

## <a name="usage-data"></a>使用情况数据  

#### <a name="what-this-feature-does"></a>此功能的作用   

System Center Configuration Manager cmdlet 库允许通过使用 Windows PowerShell cmdlet 和脚本来管理 Configuration Manager 层次结构。 Cmdlet 库收集有关如何使用库中的 cmdlet 来确定趋势和使用模式的信息。 Cmdlet 库还收集使用 cmdlet 时收到的错误类型和数目信息。  

#### <a name="information-collected-processed-or-transmitted"></a>收集、处理或传输的信息
   
收集的使用情况数据包括 cmdlet 的启动、停止和终止数据，弃用的 cmdlet 的运行数据，以及与这些 cmdlet 相关的 SMS 提供程序操作的活动指标。 此类信息不能确定个人身份。 收集的错误信息包括 cmdlet 返回的错误以及异常错误的详情。 某些错误详情报告可能无意中包含个人身份标识符，如连接到计算机的设备的序列号。 Cmdlet 库筛选并匿名化错误报告中的信息，以删除个人身份标识符，然后再将错误报告发送给 Microsoft。  

#### <a name="use-of-information"></a>信息的用途
   
Microsoft 利用此信息来提高所提供产品和服务的质量、安全性和完整性。  

#### <a name="choicecontrol"></a>选择/控制   

此“使用数据”功能默认处于启用状态。 System Center Configuration Manager cmdlet 库具有控制此功能的两个注册表项。  

 若要完全退出，请设置这两个注册表项的值。 每个值针对一个 Windows 事件跟踪 (ETW) 提供程序：  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0（驱动器提供程序“使用情况数据”功能的退出）  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0（cmdlet“使用情况数据”功能的退出）  

 “使用情况数据”设置的更改特定于在其中进行更改的计算机。  


## <a name="next-steps"></a>后续步骤

[System Center Configuration Manager Cmdlet 库文档](https://docs.microsoft.com/powershell/sccm/configurationmanager/)。   
