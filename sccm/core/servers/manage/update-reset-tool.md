---
title: "更新重置工具 | Microsoft Docs"
description: "将更新重置工具用于 System Center Configuration Manager 的控制台中更新。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1960f86e98a957559f379b9eeb6d293f7e4182e5
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="update-reset-tool"></a>更新重置工具

*适用范围：System Center Configuration Manager (Current Branch)*  


从版本 1706 开始，Configuration Manager 主站点和管理中心站点包含 Configuration Manager 更新重置工具，即 CMUpdateReset.exe。 控制台中更新存在下载或复制问题时，使用此工具修复问题。 可在站点服务器的 \cd.latest\SMSSETUP\TOOLS 文件夹中找到此工具。

可通过当前仍受支持的分支的任意版本使用此工具。

[控制台中更新](/sccm/core/servers/manage/install-in-console-updates)尚未安装且处于失败状态时，使用此工具。 失败状态表示更新下载正在进行，但是处于停滞状态，或者花费的时间过长。 时间过长是指小时数大于对同等大小的更新包的历史预期。 另外，也可能是无法将更新复制到子主站点。  

运行此工具时，它会基于你指定的更新运行。 默认情况下，该工具不会删除已成功安装或下载的更新。  

### <a name="prerequisites"></a>先决条件
用于运行此工具的帐户需要具有以下权限：
-   对管理中心站点和层次结构中每个主站点的站点数据库的“读取”和“写入”权限。 若要设置这些权限，可以将用户帐户添加为每个站点的 Configuration Manager 数据库上 db_datawriter 和 db_datareader[固定数据库角色](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles)的成员。 该工具不与辅助站点进行交互。
-   在层次结构的顶层站点上为“本地管理员”。
-   在托管服务连接点的计算机上为“本地管理员”。

需要你希望进行重置的更新包的 GUID。 要获取 GUID，请执行以下操作：
  1.   在控制台中，转到“管理” > “更新与服务”。
  2.   在显示窗格中，右键单击某一列的标题（如“状态”），然后选择“包 GUID”，将该列添加到显示内容中。
  3.   现在此列显示更新包 GUID。

> [!TIP]  
> 若要复制此 GUID，请选择想要重置的更新包的行，然后使用 CTRL+C 复制该行。 如果将复制的选定内容粘贴到文本编辑器，则可以在运行该工具时仅复制 GUID 用作命令行参数。

### <a name="run-the-tool"></a>运行该工具    
该工具必须在层次结构的顶层站点上运行。

运行此工具时，使用命令行参数指定以下内容：
  -   位于层次结构顶层站点的 SQL Server。
  -   位于顶层站点的站点数据库名称。
  -   你希望进行重置的更新包的 GUID。

该工具根据更新状态确定它需要访问的其他服务器。   

如果更新包处于下载后状态，则该工具不会清理此包。 或者，也可以使用强制删除参数强制删除已成功下载的更新（请参阅本主题后续介绍的命令行参数）。

运行该工具后：
-   如果包已被删除，则在顶层站点重启 SMS_Executive 服务。 然后，检查更新，以便可以重新下载此包。
-   如果包未被删除，则无需执行任何操作。 更新将重新进行初始化，然后重新开始复制或安装。

**命令行参数：**  

| 参数        |描述                 |  
|------------------|----------------------------|  
|**-S &lt;顶层站点的 SQL Server 的 FQDN>** | *必需* <br> 指定为层次结构的顶层站点托管站点数据库的 SQL Server 的 FQDN。    |  
| **-D &lt;数据库名称>**                        | *必需* <br> 指定顶层站点的数据库的名称。  |  
| **-P &lt;包 GUID>**                         | *必需* <br> 指定想要重置的更新包的 GUID。   |  
| **-I &lt;SQL Server 实例名称>**             | *可选* <br> 确定托管站点数据库的 SQL Server 的实例。 |
| **-FDELETE**                              | *可选* <br> 强制删除已成功下载的更新包。 |  
 **示例：**  
 在一个典型方案中，你想要重置具有下载问题的更新。 SQL Server FQDN 是 server1.fabrikam.com，站点数据库是 CM_XYZ，包 GUID 是 61F16B3C-F1F6-4F9F-8647-2A524B0C802C。  可以运行：CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C

 在比较极端的情形下，你希望强制删除存在问题的更新包。 SQL Server FQDN 是 server1.fabrikam.com，站点数据库是 CM_XYZ，包 GUID 是 61F16B3C-F1F6-4F9F-8647-2A524B0C802C。  可以运行：CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C
