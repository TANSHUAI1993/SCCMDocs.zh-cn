---
title: "查看诊断数据 | Microsoft Docs"
description: "查看诊断和使用情况数据，确保 System Center Configuration Manager 层次结构中未包含敏感信息。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0932e2b2a4f3e13c35d6b7b0446083f1c233ce03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>如何查看 System Center Configuration Manager 的诊断和使用情况数据

*适用范围：System Center Configuration Manager (Current Branch)*

你可以查看 System Center Configuration Manager 层次结构中的诊断和使用情况数据，确保其中未包括敏感信息或身份信息。 遥测数据在站点数据库的 **TEL_TelemetryResults** 表中汇总并存储，并设置为可用于高效编程的格式。 尽管以下选项可让你查看究竟向 Microsoft 发送了哪些数据，但这些数据不会用于其他目的（如数据分析）。  

使用以下 SQL 命令来查看此表的内容，并显示发送的确切数据。 （还可以将此数据导出到文本文件）：  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  在安装 1602 版之前，存储遥测数据的表是 **TelemetryResults**。  

当服务连接点处于脱机模式时，可以使用服务连接工具将当前诊断和使用情况数据导出到逗号分隔值 (CSV) 文件中。 使用 **-Export** 参数在服务连接点上运行服务连接工具。  

##  <a name="bkmk_hashes"></a>单向哈希  
某些数据包含由随机字母数字字符构成的字符串。 Configuration Manager 使用 SHA-256 算法（此算法使用单向哈希）来确保不会收集可能敏感的数据。 该算法让数据仍可用于关联和比较方面的用途。 例如，单向哈希是根据每个表名进行捕获，而不是在站点数据库中收集表的名称。 这可确保由用户或其他产品附加设备创建的任何自定义表名称不可见。 然后，对于在默认情况下随产品一起提供的 SQL 表名称，我们可以执行相同的单向哈希，并对比两个查询的结果，以确定数据库架构距离产品默认设置的偏差。 比较结果可用于改进需要更改 SQL 架构的更新。  

查看原始数据时，每行数据中将显示一个常见哈希值。 这是层次结构 ID。 此哈希值用于在不识别客户或来源的情况下确保数据与同一层次结构关联。  

#### <a name="to-see-how-the-one-way-hash-works"></a>查看单向哈希的工作原理  

1.  通过在 SQL Management Studio 中针对 Configuration Manager 数据库运行以下 SQL 语句来获取层次结构 ID：**select [dbo].[fnGetHierarchyID]\(\)**  

2.  使用以下 Windows PowerShell 脚本来执行从数据库中获取的 GUID 的单向哈希。 然后可以将此与原始数据中的层次结构 ID 比较，以了解我们如何掩蔽此数据。  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  
