---
title: 无人参与的恢复
titleSuffix: Configuration Manager
description: 使用脚本恢复 Configuration Manager 中的站点。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0da207f92ea2c11266831a0c03f5b846654e83a4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128994"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Configuration Manager 的无人参与站点恢复   

适用范围：System Center Configuration Manager (Current Branch)

 要对 Configuration Manager 管理中心站点或主站点执行[无人参与恢复](/sccm/protect/understand/recover-sites#site-recovery-procedures)，可以创建一个无人参与安装脚本并将安装程序与 /script 命令选项一起使用。 此脚本提供的信息的类型与安装向导提示输入的信息的类型相同，不同的是没有默认设置。 必须为适用于你要使用的恢复类型的安装密钥指定所有值。

 若要使用 /script 安装程序命令行选项，必须创建一个初始化文件。 然后根据此 /script 选项指定此文件的名称。 只要文件的名称具有 .ini 文件扩展名，文件的名称并不重要。 如果从命令行引用安装程序初始化文件，则必须提供文件的完整路径。 例如，安装程序初始化文件的名称为 setup.ini，并且此文件存储在 C:\setup 文件夹中，则命令行应为：

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  必须具有管理员权限才能运行安装程序。 使用无人参与脚本运行安装程序时，请使用“以管理员身份运行”在管理员上下文中启动命令提示符。

 脚本包含部分名称、项名称和值。 所需部分项名称因你正在为其编写脚本的恢复类型而异。 部分内项的顺序和文件中部分的顺序并不重要。 项不区分大小写。 当你为项提供值时，项名称后面必须跟一个等号 (=) 以及该项的值。

 使用下列部分来帮助你为无人参与的站点恢复创建脚本。 表格列出了可用的安装程序脚本项、其对应的值、是否需要它们、它们用于哪种安装类型以及项的简要描述。

## <a name="recover-a-central-administration-site-unattended"></a>在无人参与的情况下恢复管理中心站点
 使用下列信息，配置无人参与的安装程序脚本文件以恢复管理中心站点。

 **标识**

-   **密钥名称：** 操作

    -   **必需：** 是
    -   **值：** RecoverCCAR
    -   **详细信息：** 恢复管理中心站点


-   **密钥名称：** CDLatest

    -   **必需：** 是（仅在使用 CD.Latest 文件夹中的介质时）。
    -   **值：** 1. 1 以外的任何值均视为不使用 CD.Latest。
    -   **详细信息：** 从 CD.Latest 文件夹中的介质运行安装程序时，你的脚本必须包含该密钥和值，以安装主站点或管理中心站点，或恢复主站点或管理中心站点。 该值将告知安装程序当前使用介质形式 CD.Latest。

**RecoveryOptions**   
-   **密钥名称：** ServerRecoveryOptions   

    -   **必需：** 是
    -   **值：** 1、2 或 4  
         1 = 恢复站点服务器和 SQL Server。   
         2 = 仅恢复站点服务器。  
         4 = 仅恢复 SQL Server。
    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：  
        -   **值 = 1** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

             如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

        -   **值 = 2** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

        -   **值 = 4** 如果为 **BackupLocation** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

-   **密钥名称：** DatabaseRecoveryOptions

    -   **必需：** 可能
    -   **值：**   
         - **10** = 从备份中还原站点数据库。  
         - **20** = 使用已通过另一种方法手动恢复的站点数据库。   
         - **40** = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  
         - **80** = 跳过数据库恢复。
    -   **详细信息：** 指定安装程序如何恢复 SQL Server 中的站点数据库。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。


-   **密钥名称：** ReferenceSite  

    -   **必需：** 可能
    -   **值：**&lt;ReferenceSiteFQDN\>
    -   **详细信息：** 指定引用主站点。 如果数据库备份早于更改跟踪保持期，或者不使用备份来恢复站点，管理中心站点将使用此引用站点来恢复全局数据。

         如果未指定引用站点，并且备份早于更改跟踪保持期，则会使用管理中心站点中的还原数据重新初始化所有主站点。

         如果未指定引用站点，并且备份在更改跟踪保持期中，则从主站点中仅复制备份以后的更改。 如果不同的主站点中具有冲突的更改，则管理中心站点使用它收到的第一个更改。

         当 **DatabaseRecoveryOptions** 设置的值为 **40**时，需要此项。

-   **密钥名称：** SiteServerBackupLocation

    -   **必需：** 否
    -   **值：**&lt;PathToSiteServerBackupSet\>
    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。


-   **密钥名称：** BackupLocation

    -   **必需：** 可能
    -   **值：**&lt;PathToSiteDatabaseBackupSet\>
    -   **详细信息：** 指定站点数据库备份集的路径。 如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4** ，并为 **DatabaseRecoveryOptions** 项配置了值 **10** ，则需要 **BackupLocation** 项。


**选项**

- **密钥名称：** ProductID
  -   **必需：** 是
  -   **值：**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - 评估版
  -   **详细信息：** Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 可以安装 Configuration Manager 的评估版。  


- **密钥名称：** 站点代码

  -   **必需：** 是
  -   **值：**&lt;站点代码\>
  -   **详细信息：** 三个字母数字字符，用于唯一标识层次结构中的站点。 指定在发生故障之前站点使用的站点代码。


- **密钥名称：** SiteName

  -   **必需：** 是
  -   **值：** SiteName
  -   **详细信息：** 此站点的描述。


- **密钥名称：** SMSInstallDir

  - **必需：** 是
  - **值：**&lt;*ConfigMgrInstallationPath*>
  - **详细信息：** 指定 Configuration Manager 程序文件的安装文件夹。
    > [!NOTE]   
    >  可以指定要用于 Configuration Manager 安装的原始路径或新路径。

- **密钥名称：** SDKServer

  -   **必需：** 是
  -   **值：**&lt;*SMS 提供程序的 FQDN*>
  -   **详细信息：** 指定托管 SMS 提供程序的服务器的 FQDN。 指定在发生故障之前托管 SMS 提供程序的服务器。

       你可以在初始安装后为站点配置其他 SMS 提供程序。

- **密钥名称：** PrerequisiteComp

  -   **必需：** 是
  -   **值：** 0 或 1  
       0 = 下载   
       1 = 已下载
  -   **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 0，则安装程序将下载文件。  


- **密钥名称：** PrerequisitePath

  -   **必需：** 是
  -   **值：**&lt;*PathToSetupPrerequisiteFiles*>
  -   **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件。

- **密钥名称：** AdminConsole

  -   **必需：** 可能
  -   **值：** 0 或 1 0 = 不安装   
       1 = 安装
  -   **详细信息：** 指定是否安装 Configuration Manager 控制台。 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。


- **密钥名称：** JoinCEIP   
  > [!Note]  
  > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

  -   **必需：** 是
  -   **值：** 0 或 1  
       0 = 不加入  
       1 = 加入
  -   **详细信息：** 指定是否加入客户体验改善计划。

**SQLConfigOptions**

-   **密钥名称：** SQLServerName 

    -   **必需：** 是
    -   **值：***&lt;SQLServerName\>*
    -   **详细信息：** 运行托管站点数据库的 SQL Server 的服务器名称或群集实例名称。 指定在发生故障之前托管站点数据库的同一服务器。


-   **密钥名称：** DatabaseName

    -   **必需：** 是
    -   **值：***&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **详细信息：** 要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 指定在发生故障之前使用的同一数据库名称。

        > [!IMPORTANT]  
        >  如果未使用默认实例，则必须指定实例名称和站点数据库名称。

-   **密钥名称：** SQLSSBPort

    -   **必需：** 否
    -   **值：**&lt;*SSBPortNumber*>
    -   **详细信息：** 指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。 指定在发生故障之前使用的相同 SSB 端口。

## <a name="recover-a-primary-site-unattended"></a>在无人参与的情况下恢复主站点
 使用下列信息，配置无人参与的安装程序脚本文件以恢复管理中心站点。

 **标识**

-   **密钥名称：** 操作

    -   **必需：** 是
    -   **值：** RecoverPrimarySite
    -   **详细信息：** 恢复主站点


-   **密钥名称：** CDLatest

    -   **必需：** 是（仅在使用 CD.Latest 文件夹中的介质时）。
    -   **值：** 1. 1 以外的任何值均视为不使用 CD.Latest。
    -   **详细信息：** 从 CD.Latest 文件夹中的介质运行安装程序时，你的脚本必须包含该密钥和值，以安装主站点或管理中心站点，或恢复主站点或管理中心站点。 该值将告知安装程序当前使用介质形式 CD.Latest。

**RecoveryOptions**

-   **密钥名称：** ServerRecoveryOptions

    -   **必需：** 是
    -   **值：** 1、2 或 4    
         1 = 恢复站点服务器和 SQL Server。   
         2 = 仅恢复站点服务器。  
         4 = 仅恢复 SQL Server。
    -   **详细信息：** 指定安装程序是恢复站点服务器、SQL Server 还是两者都恢复。 设置 ServerRecoveryOptions 设置的以下值时需要关联的项：

        -   **值 = 1** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

             如果为 **DatabaseRecoveryOptions** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

        -   **值 = 2** 你可以选择为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。

        -   **值 = 4** 如果为 **BackupLocation** 项（用于从备份中还原站点数据库）配置了值 **10** ，则需要 **BackupLocation** 项。

-   **密钥名称：** DatabaseRecoveryOptions

    -   **必需：** 可能
    -   **值：**   
         - **10** = 从备份中还原站点数据库。  
         - **20** = 使用已通过另一种方法手动恢复的站点数据库。     
         - **40** = 为站点创建新数据库。 没有可用的站点数据库备份时，请使用此选项。 通过其他站点中的复制来恢复全局数据和站点数据。  
         - **80** = 跳过数据库恢复。
    -   **详细信息：** 指定安装程序如何恢复 SQL Server 中的站点数据库。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **4**时，需要此项。


-   **密钥名称：** SiteServerBackupLocation

    -   **必需：** 否
    -   **值：**&lt;PathToSiteServerBackupSet\>
    -   **详细信息：** 指定站点服务器备份集的路径。 当 **ServerRecoveryOptions** 设置的值为 **1** 或 **2**时，此项是可选的。 为 **SiteServerBackupLocation** 项指定值以使用站点备份来恢复站点。 如果未指定值，则会重新安装站点，而不是从备份集中还原站点。     


-   **密钥名称：** BackupLocation

    -   **必需：** 可能
    -   **值：**&lt;PathToSiteDatabaseBackupSet\>
    -   **详细信息：** 指定站点数据库备份集的路径。 如果为 **ServerRecoveryOptions** 项配置了值 **1** 或 **4** ，并为 **DatabaseRecoveryOptions** 项配置了值 **10** ，则需要 **BackupLocation** 项。

**选项**

-   **密钥名称：** ProductID

    -   **必需：** 是
    -   **值：**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - 评估版     
    -   **详细信息：** Configuration Manager 安装产品密钥，包括短划线。 输入 **Eval** 可以安装 Configuration Manager 的评估版。  


-   **密钥名称：** 站点代码

    -   **必需：** 是
    -   **值：**&lt;站点代码\>
    -   **详细信息：** 三个字母数字字符，用于唯一标识层次结构中的站点。 指定在发生故障之前站点使用的站点代码。


-   **密钥名称：** SiteName

    -   **必需：** 是
    -   **值：** SiteName
    -   **详细信息：** 此站点的描述。


-   **密钥名称：** SMSInstallDir

    -   **必需：** 是
    -   **值：**&lt;*ConfigMgrInstallationPath*>
    -   **详细信息：** 指定 Configuration Manager 程序文件的安装文件夹。

        > [!NOTE]   
        >  可以指定要用于 Configuration Manager 安装的原始路径或新路径。

-   **密钥名称：** SDKServer

    -   **必需：** 是
    -   **值：**&lt;*SMS 提供程序的 FQDN*>
    -   **详细信息：** 指定托管 SMS 提供程序的服务器的 FQDN。 指定在发生故障之前托管 SMS 提供程序的服务器。

         你可以在初始安装后为站点配置其他 SMS 提供程序。

-   **密钥名称：** PrerequisiteComp

    -   **必需：** 是
    -   **值：** 0 或 1    
         0 = 下载   
         1 = 已下载   
    -   **详细信息：** 指定是否已下载安装程序的必备文件。 例如，如果使用值 0，则安装程序将下载文件。


-   **密钥名称：** PrerequisitePath

    -   **必需：** 是
    -   **值：**&lt;*PathToSetupPrerequisiteFiles*>
    -   **详细信息：** 指定安装程序必备文件的路径。 根据 PrerequisiteComp 值，安装程序将使用此路径来存储已下载的文件或查找以前下载的文件。


-   **密钥名称：** AdminConsole

    -   **必需：** 可能
    -   **值：** 0 或 1  
         0 = 不安装   
         1 = 安装  
    -   **详细信息：** 指定是否安装 Configuration Manager 控制台。 除非 **ServerRecoveryOptions** 设置的值为 **4**，否则此项为必需。

-   **密钥名称：** JoinCEIP  
    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

    -   **必需：** 是
    -   **值：** 0 或 1    
         0 = 不加入  
         1 = 加入
    -   **详细信息：** 指定是否加入客户体验改善计划。


**SQLConfigOptions**

-   **密钥名称：** SQLServerName 

    -   **必需：** 是
    -   **值：***&lt;SQLServerName\>*
    -   **详细信息：** 运行托管站点数据库的 SQL Server 的服务器名称或群集实例名称。 指定在发生故障之前托管站点数据库的同一服务器。


-   **密钥名称：** DatabaseName

    -   **必需：** 是
    -   **值：***&lt;SiteDatabaseName\>* 或 *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **详细信息：** 要创建或用于安装管理中心站点数据库的 SQL Server 数据库的名称。 指定在发生故障之前使用的同一数据库名称。

        > [!IMPORTANT]    
        >  如果未使用默认实例，则必须指定实例名称和站点数据库名称。

-   **密钥名称：** SQLSSBPort

    -   **必需：** 否
    -   **值：**&lt;*SSBPortNumber*>
    -   **详细信息：** 指定 SQL Server 使用的 SQL Server Service Broker (SSB) 端口。 通常，SSB 配置为使用 TCP 端口 4022，但也支持其他端口。 指定在发生故障之前使用的相同 SSB 端口。

**层次结构扩展选项**

-   **密钥名称：** CCARSiteServer

    -   **必需：** 可能
    -   **值：**&lt;*SiteCodeForCentralAdministrationSite*>
    -   **详细信息：** 指定主站点加入 Configuration Manager 层次结构时要附加到的管理中心站点。 如果在发生故障之前主站点已附加到管理中心站点，则此设置为必需。 指定在发生故障之前用于管理中心站点的站点代码。

-   **密钥名称：** CASRetryInterval

    -   **必需：** 否
    -   **值：**&lt;*间隔*>
    -   **详细信息：** 指定在连接失败后尝试连接到管理中心站点的重试间隔（以分钟为单位）。 例如，如果连接到管理中心站点失败，则主站点将等待你为 CASRetryInterval 指定的分钟数，然后重新尝试连接。


-   **密钥名称：** WaitForCASTimeout

    -   **必需：** 否
    -   **值：**&lt;*超时*>
    -   **详细信息：** 指定主站点连接到管理中心站点的最大超时值（以分钟为单位）。 例如，主站点未能连接到管理中心站点，则在达到 WaitForCASTimeout 期间之前，主站点将基于 CASRetryInterval 重新尝试连接到管理中心站点。 你可以指定 0 到 100 的值。
