---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 10/04/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7d24b4032f893cfbbb347a1d0a37090f308c365
ms.sourcegitcommit: b631fcb2669ac2a5801e70620b0c3e81431bea8f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2019
ms.locfileid: "71975508"
---
### <a name="ki_hinv"></a> 硬件清单报告

<!--5468413-->
若尝试运行依赖硬件清单的报告，它将返回错误。 例如，BitLocker 报告返回类似以下消息的错误：

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

还可能在 dataldr.log 文件中看到下面的错误： 

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

依赖硬件清单的控制台仪表板也可能受到影响。

此问题由特定硬件清单表上的数据库架构更改导致。

#### <a name="workaround"></a>解决方法

解决方法为弃用数据库中预先存在的属性。 然后数据加载程序站点组件可以创建新的属性。 在站点数据库服务器上运行以下 SQL 脚本，以修复表架构：

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
