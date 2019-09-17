---
title: 查看诊断数据
titleSuffix: Configuration Manager
description: 查看诊断和使用情况数据，确保 System Center Configuration Manager 层次结构中未包含敏感信息。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68155a31d1d50d1df4c06882416f158f9a71c8d2
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70889458"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>如何查看 Configuration Manager 的诊断和使用情况数据

适用范围：  System Center Configuration Manager (Current Branch)

可以查看 Configuration Manager 层次结构中的诊断和使用情况数据，确保其中未包括敏感信息或身份信息。 站点会汇总其诊断数据，并存储在站点数据库的 TEL_TelemetryResults 表中  。 站点将数据设置为在编程方式下可使用并有效的格式。

本文中的信息可让你了解向 Microsoft 发送的确切数据。 这些数据不会用于其他目的，如数据分析。  

## <a name="view-data-in-database"></a>查看数据库中的数据

使用以下 SQL 命令来查看此表的内容，并显示发送的确切数据：  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>导出数据

当服务连接点处于脱机模式时，使用服务连接工具将当前数据导出到逗号分隔值 (CSV) 文件中。 使用 **-Export** 参数在服务连接点上运行服务连接工具。

有关详细信息，请参阅[使用服务连接工具](/sccm/core/servers/manage/use-the-service-connection-tool)。

## <a name="bkmk_hashes"></a>单向哈希

某些数据包含由随机字母数字字符构成的字符串。 Configuration Manager 使用 SHA-256 算法来创建单向哈希。 此过程可确保 Microsoft 不会收集可能敏感的数据。 哈希数据仍可用于关联和比较目的。

例如，它捕获每个表名的单向哈希，而不是在站点数据库中收集表的名称。 此行为可确保任何自定义表名称均不可见。 然后，Microsoft 对默认 SQL 表名称执行相同的单向哈希处理。 比较两个查询的结果可确定数据库架构与产品默认值的偏差。 此信息可用于改进需要更改 SQL 架构的更新。  

查看原始数据时，每行数据中显示一个常见哈希值。 此哈希值是层次结构 ID。 它用于在不识别客户或来源的情况下将数据与同一层次结构关联。

### <a name="how-the-one-way-hash-works"></a>单向哈希的工作原理

1. 通过在 SQL Management Studio 中针对 Configuration Manager 数据库运行以下 SQL 查询来获取层次结构 ID：

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. 使用以下 Windows PowerShell 脚本来执行层次结构 ID 的单向哈希。  

    ``` PowerShell
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

3. 比较脚本输出与原始数据中的 GUID。 此过程显示数据的模糊程度。
