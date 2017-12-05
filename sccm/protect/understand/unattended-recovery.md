---
title: "无人参与的恢复"
titleSuffix: Configuration Manager
description: "使用脚本恢复 System Center Configuration Manager 中的站点。"
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: be561de1fd14245e3cf52148683611a307484d3d
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Configuration Manager 的无人参与站点恢复   

适用于：System Center Configuration Manager (Current Branch) 若要对 Configuration Manager 管理中心站点或主站点执行[无人参与恢复](/sccm/protect/understand/recover-sites#site-recovery-procedures)，可以创建无人参与安装脚本，并结合使用安装程序和 /script 命令选项。 此脚本提供的信息的类型与安装向导提示输入的信息的类型相同，不同的是没有默认设置。 必须为适用于你要使用的恢复类型的安装密钥指定所有值。

 要使用 /script 安装程序命令行选项，你必须创建一个初始化文件并在 /script 安装程序命令行选项后面指定初始化文件名。 只要文件的名称具有 .ini 文件扩展名，文件的名称并不重要。 如果从命令行引用安装程序初始化文件，则必须提供文件的完整路径。 例如，安装程序初始化文件的名称为 setup.ini，并且此文件存储在 C:\setup 文件夹中，则命令行应为：

 **setup /script c:\setup\setup.ini**。

> [!IMPORTANT]  
>  你必须具有管理员权限才能运行安装程序。 使用无人参与脚本运行安装程序时，请使用“以管理员身份运行” 在管理员上下文中启动命令提示符。

 脚本包含部分名称、项名称和值。 所需部分项名称因你正在为其编写脚本的恢复类型而异。 部分内项的顺序和文件中部分的顺序并不重要。 项不区分大小写。 当你为项提供值时，项名称后面必须跟一个等号 (=) 以及该项的值。

 使用下列部分来帮助你为无人参与的站点恢复创建脚本。 表格列出了可用的安装程序脚本项、其对应的值、是否需要它们、它们用于哪种安装类型以及项的简要描述。

## <a name="recover-a-central-administration-site-unattended"></a>在无人参与的情况下恢复管理中心站点
 使用下列信息，配置无人参与的安装程序脚本文件以恢复管理中心站点。

 **标识**

-   **项名称：** Action

    -   **是否必需：** 是
    -   **值：** RecoverCCAR
    -   **详细信息：** 恢复管理中心站点


-   **密钥名称：**CDLatest

    -   **必备：**是（仅在使用 CD.Latest 文件夹中的介质时）。
    -   **值：**1。1 以外的任何值均视为不使用 CD.Latest。
    -   **详细信息：**从 CD.Latest 文件夹中的介质运行安装程序时，你的脚本必须包含该密钥和值，以安装主站点或管理中心站点，或恢复主站点或管理中心站点。 该值将告知安装程序当前使用介质形式 CD.Latest。

**RecoveryOptions**   
-   **项名称：** ServerRecoveryOptions   

    -   **是否必需：** 是
    -   **值：** 1、2 或 4  
         1 = 恢复站点服务器和 SQL Server。   
         2 = 仅恢复站点服务器。  
         4 = 仅恢复 SQL Server。
    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：  
        -   **值 = 1** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

             如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

        -   **值 = 2** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

        -   **值 = 4** 如果为 **BackupLocation** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

-   **项名称：** DatabaseRecoveryOptions

    -   **是否必需：** 可能
    -   **值：** 10、20、40、80  
         10 = 从备份中还原站点数据库。  
         20 = 使用已通过另一种方法手动恢复的站点数据库。   
         40 = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  
         80 = 跳过数据库恢复。
    -   **详细信息：** 指定安装程序将如何恢复 SQL Server 中的站点数据库。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。


-   **项名称：** ReferenceSite  

    -   **是否必需：** 可能
    -   **值：**&lt;ReferenceSiteFQDN\>
    -   **详细信息：** 指定在数据库备份早于更改跟踪保持期或者在没有备份的情况下恢复站点时，管理中心站点用于恢复全局数据的引用主站点。

         如果未指定引用站点，并且备份早于更改跟踪保持期，则会使用管理中心站点中的还原数据重新初始化所有主站点。

         如果未指定引用站点，并且备份在更改跟踪保持期中，则从主站点中仅复制备份以后的更改。 如果不同的主站点中具有冲突的更改，则管理中心站点使用它收到的第一个更改。

         当 **DatabaseRecoveryOptions** 设置的值为 **40**时，需要此项。

-   **项名称：** SiteServerBackupLocation

    -   **是否必需：** 否
    -   **值：**&lt;PathToSiteServerBackupSet\>
    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。


-   **项名称：** BackupLocation

    -   **是否必需：** 可能
    -   &lt;PathToSiteDatabaseBackupSet\>
    -   **详细信息：** 指定站点数据库备份集的路径。 如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4** ，并为 **DatabaseRecoveryOptions** 项配置了值 **10** ，则需要 **BackupLocation** 项。


**选项**

-   **项名称：** ProductID
    -   **是否必需：** 是
    -   **值：**   
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
          评估版
    -   **详细信息：**Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 可以安装 Configuration Manager 的评估版。  


-   **项名称：** SiteCode

    -   **是否必需：** 是
    -   **值：**&lt;Site code\>
    -   **详细信息：** 三个字母数字字符，用于唯一标识层次结构中的站点。 你必须指定在发生故障之前站点使用的站点代码。


-   **项名称：** SiteName

    -   **是否必需：** 是
    -   **值：** SiteName
    -   **详细信息：** 此站点的描述。


-   **项名称：** SMSInstallDir

    -   **是否必需：** 是
    -   &lt;*ConfigMgrInstallationPath*>
    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。
        > [!NOTE]   
        >  可以指定要用于 Configuration Manager 安装的原始路径或新路径。

-   **项名称：** SDKServer

    -   **是否必需：** 是
    -   **值：**&lt;SMS 提供程序的 FQDN>
    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。 你必须指定在发生故障之前承载 SMS 提供程序的服务器。

         你可以在初始安装后为站点配置其他 SMS 提供程序。

-   **项名称：** PrerequisiteComp

    -   **是否必需：** 是
    -   **值：** 0 或 1  
         0 = 下载   
         1 = 已下载
    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。  


-   **项名称：** PrerequisitePath

    -   **是否必需：** 是
    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>
    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。

-   **项名称：** AdminConsole

    -   **是否必需：** 可能
    -   **值：**0 或 1 0 = 不安装   
         1 = 安装
    -   **详细信息：**指定是否安装 Configuration Manager 控制台。 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。


-   **项名称：** JoinCEIP

    -   **是否必需：** 是
    -   **值：** 0 或 1  
         0 = 不加入  
         1 = 加入
    -   **详细信息：** 指定是否加入客户体验改善计划。

**SQLConfigOptions**

-   **项名称：** SQLServerName

    -   **是否必需：** 是
    -   **值：***&lt;SQLServerName\>*
    -   **详细信息：**运行将托管站点数据库的 SQL Server 的服务器名称或群集实例名称。 你必须指定在发生故障之前承载站点数据库的同一服务器。


-   **项名称：** DatabaseName

    -   **是否必需：** 是
    -   **值：**&lt;SiteDatabaseName\> 或 &lt;InstanceName\>\\&lt;SiteDatabaseName\>
    -   **详细信息：**要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 你必须指定在发生故障之前使用的同一数据库名称。

        > [!IMPORTANT]  
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。

-   **项名称：**SQLSSBPort

    -   **是否必需：**否
    -   **值：**&lt;*SSBPortNumber*>
    -   **详细信息：**指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。 你必须指定在发生故障之前使用的相同 SSB 端口。

## <a name="recover-a-primary-site-unattended"></a>在无人参与的情况下恢复主站点
 使用下列信息，配置无人参与的安装程序脚本文件以恢复管理中心站点。

 **标识**

-   **项名称：** Action

    -   **是否必需：**是
    -   **值：**RecoverPrimarySite
    -   **详细信息：**恢复主站点


-   **密钥名称：**CDLatest

    -   **必备：**是（仅在使用 CD.Latest 文件夹中的介质时）。
    -   **值：**1。1 以外的任何值均视为不使用 CD.Latest。
    -   **详细信息：**从 CD.Latest 文件夹中的介质运行安装程序时，你的脚本必须包含该密钥和值，以安装主站点或管理中心站点，或恢复主站点或管理中心站点。 该值将告知安装程序当前使用介质形式 CD.Latest。

**RecoveryOptions**

-   **项名称：** ServerRecoveryOptions

    -   **是否必需：** 是
    -   **值：** 1、2 或 4    
         1 = 恢复站点服务器和 SQL Server。   
         2 = 仅恢复站点服务器。  
         4 = 仅恢复 SQL Server。
    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：

        -   **值 = 1** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

             如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

        -   **值 = 2** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

        -   **值 = 4** 如果为 **BackupLocation** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

-   **项名称：** DatabaseRecoveryOptions

    -   **是否必需：** 可能
    -   **值：** 10、20、40、80  
         10 = 从备份中还原站点数据库。  
         20 = 使用已通过另一种方法手动恢复的站点数据库。     
         40 = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  
         80 = 跳过数据库恢复。
    -   **详细信息：** 指定安装程序将如何恢复 SQL Server 中的站点数据库。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。


-   **项名称：**SiteServerBackupLocation

    -   **是否必需：** 否
    -   **值：**&lt;PathToSiteServerBackupSet\>
    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。     


-   **项名称：** BackupLocation

    -   **是否必需：** 可能
    -   &lt;PathToSiteDatabaseBackupSet\>
    -   **详细信息：** 指定站点数据库备份集的路径。 如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4** ，并为 **DatabaseRecoveryOptions** 项配置了值 **10** ，则需要 **BackupLocation** 项。

**选项**

-   **项名称：** ProductID

    -   **是否必需：** 是
    -   **值：**     
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         评估版     
    -   **详细信息：**Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 可以安装 Configuration Manager 的评估版。  


-   **项名称：** SiteCode

    -   **是否必需：** 是
    -   **值：**&lt;Site code\>
    -   **详细信息：** 三个字母数字字符，用于唯一标识层次结构中的站点。 你必须指定在发生故障之前站点使用的站点代码。


-   **项名称：** SiteName

    -   **是否必需：** 是
    -   **值：** SiteName
    -   **详细信息：** 此站点的描述。


-   **项名称：** SMSInstallDir

    -   **是否必需：** 是
    -   &lt;*ConfigMgrInstallationPath*>
    -   **详细信息：**指定 Configuration Manager 程序文件的安装文件夹。

        > [!NOTE]   
        >  可以指定要用于 Configuration Manager 安装的原始路径或新路径。

-   **项名称：** SDKServer

    -   **是否必需：** 是
    -   **值：**&lt;SMS 提供程序的 FQDN>
    -   **详细信息：** 指定将托管 SMS 提供程序的服务器的 FQDN。 你必须指定在发生故障之前承载 SMS 提供程序的服务器。

         你可以在初始安装后为站点配置其他 SMS 提供程序。

-   **项名称：** PrerequisiteComp

    -   **是否必需：** 是
    -   **值：** 0 或 1    
         0 = 下载   
         1 = 已下载   
    -   **详细信息：** 指定安装程序必备文件是否已下载。 例如，如果使用值 0，则安装程序将下载文件。


-   **项名称：** PrerequisitePath

    -   **是否必需：** 是
    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>
    -   **详细信息：** 指定安装程序必备文件的路径。 根据 **PrerequisiteComp** 值，安装程序将使用此路径来存储已下载文件或查找以前下载的文件。


-   **项名称：** AdminConsole

    -   **是否必需：**可能
    -   **值：**0 或 1  
         0 = 不安装   
         1 = 安装  
    -   **详细信息：**指定是否安装 Configuration Manager 控制台。 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。

-   **项名称：** JoinCEIP

    -   **是否必需：** 是
    -   **值：** 0 或 1    
         0 = 不加入  
         1 = 加入
    -   **详细信息：** 指定是否加入客户体验改善计划。


**SQLConfigOptions**

-   **项名称：** SQLServerName

    -   **是否必需：** 是
    -   **值：***&lt;SQLServerName\>*
    -   **详细信息：**运行将托管站点数据库的 SQL Server 的服务器名称或群集实例名称。 你必须指定在发生故障之前承载站点数据库的同一服务器。


-   **项名称：** DatabaseName

    -   **是否必需：** 是
    -   **值：**&lt;SiteDatabaseName\> 或 &lt;InstanceName\>\\&lt;SiteDatabaseName\>
    -   **详细信息：**要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 你必须指定在发生故障之前使用的同一数据库名称。

        > [!IMPORTANT]    
        >  如果未使用默认实例，你必须指定实例名称和站点数据库名称。

-   **项名称：**SQLSSBPort

    -   **是否必需：**否
    -   **值：**&lt;*SSBPortNumber*>
    -   **详细信息：**指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。 你必须指定在发生故障之前使用的相同 SSB 端口。

**层次结构扩展选项**

-   **项名称：**CCARSiteServer

    -   **是否必需：**可能
    -   **值：** &lt;SiteCodeForCentralAdministrationSite>
    -   **详细信息：**指定主站点加入 Configuration Manager 层次结构时将要附加到的管理中心站点。 如果在发生故障之前主站点已附加到管理中心站点，则此设置为必需。 你必须指定在发生故障之前用于管理中心站点的站点代码。

-   **项名称：** CASRetryInterval

    -   **是否必需：** 否
    -   **值：**&lt;Interval>
    -   **详细信息：** 指定连接失败后尝试连接到管理中心站点的重试间隔（以分钟为单位）。 例如，如果连接到管理中心站点失败，则主站点将等待你为 CASRetryInterval 指定的分钟数，然后重新尝试连接。


-   **项名称：** WaitForCASTimeout

    -   **是否必需：** 否
    -   **值：** &lt;Timeout>
    -   **详细信息：** 指定主站点连接到管理中心站点的最大超时值（以分钟为单位）。 例如，主站点未能连接到管理中心站点，则在达到 WaitForCASTimeout 期间之前，主站点将基于 CASRetryInterval 重新尝试连接到管理中心站点。 你可以指定 0 到 100 的值。
