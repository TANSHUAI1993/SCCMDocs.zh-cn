---
title: "测试数据库更新 | Microsoft Docs"
description: "安装 Configuration Manager 更新时测试站点数据库升级。"
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6b76c97cd205bb02683a7bfa1eb378471a75551d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>安装更新时测试数据库升级

*适用范围：System Center Configuration Manager (Current Branch)*

本主题中的信息可以帮助你在为 Configuration Manager 的当前分支安装控制台内更新之前，运行测试数据库升级。 但是，测试升级不再是必需的或建议的步骤，除非你的数据库处于可疑状态，或由 Configuration Manager 未显式支持的自定义项进行了修改。

## <a name="do-i-need-to-run-a-test-upgrade"></a>是否需要运行测试升级？
由于 System Center Configuration Manager 引入了更改，可能会弃用此升级测试。 这些更改简化了将生产环境更新为较新版本的过程和速度。 这种重新设计是为了帮助客户在安装每个新更新时保持最新状态，并将风险级别和运营开销保持在较低水平。

这些更改涉及如何安装更新，包括无需运行站点恢复即可自动回滚失败的更新的逻辑。 这些更改实现了使用控制台来管理更新安装，且包括[重试失败更新的安装](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry)选项。

> [!TIP]
> 从较旧的产品（如 System Center 2012 Configuration Manager）升级到 System Center Configuration Manager 时，[测试数据库升级仍是建议的步骤](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade)。

如果你仍计划在安装控制台内更新时测试站点数据库的升级，可使用以下信息作为对[有关安装控制台内更新的指导](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)的补充。

## <a name="prepare-to-run-a-test-database-upgrade"></a>准备运行测试数据库升级  
在层次结构中安装新的更新（如更新 1702）之前，可以测试站点数据库的升级。

若要运行升级测试，请从运行你要更新到的 Configuration Manager 版本的站点的 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder)的源文件中使用 Configuration Manager 安装程序。 此要求意味着要对 1702 更新测试数据库更新，必须考虑以下事项：
-   必须至少有一个运行版本 1702 的站点，这样你可以从中获取该 CD.Latest 文件夹。
-   如果你没有用于运行所需版本的站点，请考虑在实验室环境中安装站点，然后将该站点更新到新版本。 这将使用正确版本的源文件创建 CD.Latest 文件夹。

针对你还原到 SQL Server 独立实例的站点数据库的备份运行升级测试。  使用 testdbupgrade 命令行开关从 CD.Latest 文件夹运行安装程序以测试还原了数据库副本的升级。 测试升级完成后，将放弃升级后的数据库。 它不能由 Configuration Manager 站点使用。

如果更新安装失败，应该不需要恢复站点。 但可以从控制台中重试更新的安装。

##  <a name="run-the-test-upgrade"></a>运行测试升级    
1.  使用 Configuration Manager 安装程序以及运行你计划更新到的版本的站点的 CD.Latest 文件夹中的源文件。  

2.  将 CD.Latest 文件夹复制到要用于运行测试数据库升级的 SQL Server 实例上的某个位置。

3.  为要测试升级的站点数据库创建备份。 接下来，将数据库的副本还原到未托管 Configuration Manager 站点的 SQL Server 实例。 该 SQL Server 实例使用的 SQL Server 版本必须与站点数据库相同。  

4.  还原数据库副本之后，从包含要更新到的版本的源文件的 CD.Latest 文件夹中运行安装程序。 运行安装程序时，使用 **/TESTDBUPGRADE** 命令行选项。 如果托管数据库副本的 SQL Server 实例不是默认实例，请提供命令行参数以确定托管站点数据库副本的实例。   

  例如，已有数据库名称为 SMS_ABC 的站点数据库。 你将此站点数据库的副本还原到实例名称为 DBTest 的受支持 SQL Server 实例。 要测试站点数据库的此副本的升级，请使用以下命令行：**Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**。  

  可以在 System Center Configuration Manager 的源媒体上的下列位置中找到 Setup.exe：**SMSSETUP\BIN\X64**。  

5.  在运行升级测试的 SQL Server 实例上，监视系统驱动器根目录中的 ConfigMgrSetup.log 以了解进度和成功与否。  

     如果测试升级失败，请修复与站点数据库升级失败相关的任何问题。 然后，新建站点数据库的备份并测试数据库的新副本升级。  



## <a name="next-steps"></a>后续步骤
测试数据库更新成功完成后，放弃已更新的数据库。 它不能由 Configuration Manager 站点使用。 随后你可以返回到活动站点并[开始执行更新安装](/sccm/core/servers/manage/install-in-console-updates)。
