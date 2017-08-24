---
title: "不使用 Internet 连接同步更新 - Configuration Manager | Microsoft Docs"
description: "在断开 Internet 连接的顶层软件更新点上运行软件更新同步。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
ms.openlocfilehash: fd9c1e9418ff1956c6ef98753e23a293440179be
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>从断开连接的软件更新点中同步软件更新  

*适用范围：System Center Configuration Manager (Current Branch)*

 如果顶层站点上的软件更新点从 Internet 断开连接，你必须使用 WSUSUtil 工具的导出和导入功能来同步软件更新元数据。 可以选择不属于 Configuration Manager 层次结构的现有 WSUS 服务器作为同步源。 本主题提供有关如何使用 WSUSUtil 工具的导出和导入功能的信息。  

 要导出和导入软件更新元数据，你必须从指定导出服务器上的 WSUS 数据库中导出软件更新元数据，接着将本地存储的许可条款文件复制到断开连接的软件更新点，然后将软件更新元数据导入断开连接的软件更新点上的 WSUS 数据库。  

 使用下表来确定要在其中导出软件更新元数据的导出服务器。  

|软件更新点|连接的软件更新点的上游更新源|断开连接的软件更新点的导出服务器|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|管理中心站点|Microsoft 更新 (Internet)<br /><br /> 现有 WSUS 服务器|通过使用 Configuration Manager 环境中所需的软件更新分类、产品和语言选择与 Microsoft 更新同步的 WSUS 服务器。|  
|独立主站点|Microsoft 更新 (Internet)<br /><br /> 现有 WSUS 服务器|通过使用 Configuration Manager 环境中所需的软件更新分类、产品和语言选择与 Microsoft 更新同步的 WSUS 服务器。|  

 在开始导出过程之前，请验证软件更新同步是否已在所选导出服务器上完成，以确保同步最新的软件更新元数据。 要验证软件更新同步是否已成功完成，请使用下列过程。  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>验证软件更新同步是否已在导出服务器上成功完成  

1.  在导出服务器上打开 WSUS 管理控制台并连接到 WSUS 数据库。  

2.  在 WSUS 管理控制台中，单击“同步” 。 软件更新同步尝试的列表将显示在结果窗格中。  

3.  在结果窗格中，找到最新的软件更新同步尝试并验证该尝试是否已成功完成。  

> [!IMPORTANT]  
>  WSUSUtil 工具必须以本地方式在导出服务器上运行才能导出软件更新元数据，并且它还必须在断开连接的软件更新点服务器上运行才能导入软件更新元数据。 此外，运行 WSUSUtil 工具的用户必须是每个服务器上的本地管理员组的成员。  

## <a name="export-process-for-software-updates"></a>软件更新的导出过程  
 软件更新导出过程包括两个主要步骤：将本地存储的许可条款文件复制到断开连接的软件更新点，以及从导出服务器上的 WSUS 数据库中导出软件更新元数据。  

 使用下列过程将本地许可条款元数据复制到断开连接的软件更新点。  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>将本地文件从导出服务器复制到断开连接的软件更新点服务器  

1.  在导出服务器上，导航到存储软件更新和软件更新许可条款的文件夹。 默认情况下，WSUS 服务器将文件存储在 <*WSUSInstallationDrive*>\WSUS\WSUSContent\\ 下，其中 *WSUSInstallationDrive* 是安装了 WSUS 的驱动器。  

2.  将所有文件和文件夹从此位置复制到断开连接的软件更新点服务器上的 WSUSContent 文件夹。  

 使用下列过程从导出服务器上的 WSUS 数据库中导出软件更新元数据。  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>从导出服务器上的 WSUS 数据库中导出软件更新元数据  

1.  在导出服务器上的命令提示符处，导航到包含 WSUSutil.exe 的文件夹。 默认情况下，该工具位于 %*ProgramFiles*%\Update Services\Tools。 例如，如果该工具位于默认位置中，则键入 **cd %ProgramFiles%\Update Services\Tools**。  

2.  键入下列命令以将软件更新元数据导出为一个包文件：  

     **wsusutil.exe export**  *packagename*  *logfile*  

     例如：  

     **wsusutil.exe export export.cab export.log**  

     此格式可以汇总为如下：WSUSutil.exe 后跟导出选项、在导出操作过程中创建的导出 .cab 文件的名称，以及日志文件的名称。 WSUSutil.exe 从导出服务器中导出元数据，并创建操作的日志文件。  

    > [!NOTE]  
    >  包（.cab 文件）和日志文件名称在当前文件夹中必须唯一。  

3.  将导出包移动到导入 WSUS 服务器上包含 WSUSutil.exe 的文件夹。  

    > [!NOTE]  
    >  如果将包移动到此文件夹，导入体验可能会更加轻松。 你可以将包移动到导入服务器可访问的任何位置，然后在运行 WSUSutil.exe 时指定该位置。  

## <a name="import-software-updates-metadata"></a>导入软件更新元数据  
 使用下列过程将软件更新元数据从导出服务器导入到断开连接的软件更新点。  

> [!IMPORTANT]  
>  决不要导入从你不信任的源中导出的任何数据。 如果导入你不信任的源中的内容，将可能会危害 WSUS 服务器的安全性。  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>将元数据导入到导入服务器的数据库  

1.  在导入 WSUS 服务器上的命令提示符下，导航到包含 WSUSutil.exe 的文件夹。 默认情况下，该工具位于 %*ProgramFiles*%\Update Services\Tools。  

2.  键入下列命令：  

     **wsusutil.exe import**  *packagename*  *logfile*  

     例如：  

     **wsusutil.exe import export.cab import.log**  

     此格式可以汇总为如下：WSUSutil.exe 后跟导入命令、在导出操作过程中创建的包文件 (.cab) 的名称、包文件的路径（如果该文件位于其他文件夹中），以及日志文件的名称。 WSUSutil.exe 从导出服务器中导入元数据，并创建操作的日志文件。  

## <a name="next-steps"></a>后续步骤
在首次同步软件更新后，或有新的可用分类或产品时，必须[配置新的分类和产品](configure-classifications-and-products.md)以便通过新条件同步软件更新。

通过所需的条件同步软件更新后，[管理软件更新的设置](manage-settings-for-software-updates.md)。  
