---
title: "命令行安装 | Microsoft Docs"
description: "了解如何在命令提示符处运行 System Center Configuration Manager 安装程序来安装多个站点。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8ff48b08d1abb7481592c0ea076d4efa15c3d8ee
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>使用命令行安装 System Center Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*

 可在命令提示符处运行 System Center Configuration Manager 安装程序来安装多个站点类型。

## <a name="supported-tasks-for-command-line-installations"></a>命令行安装支持的任务
 此种运行安装程序的方式支持以下站点安装和站点维护任务：

-   **从命令提示符处安装管理中心站点或主站点**  
  查看[适用于安装程序的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

-  **修改管理中心站点或主站点中使用的语言**  
    若要从命令提示符处修改站点上安装的语言（包括用于移动设备的语言），必须：  

     -   从站点服务器上的 **&lt;ConfigMgrInstallationPath\>\Bin\X64** 运行安装程序，
     -   使用 **/MANAGELANGS** 命令行选项，
     -   指定语言脚本文件，该文件可指定要添加或删除的语言，  

    例如，使用以下语法：**setupwpf.exe /MANAGELANGS &lt;language script file\>**  

    若要创建语言脚本文件，请使用[用于管理语言的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)中的信息  

-  **将安装脚本文件用于无人参与的站点安装或站点恢复**  
    可使用安装脚本从命令提示符运行安装程序，并可运行无人参与的站点安装。 还可以使用此选项来恢复站点。    

    若要将脚本用于安装程序：  

    -   使用命令行选项 **/SCRIPT** 运行安装程序并指定脚本文件。  

    -   必须使用所需的密钥和值配置脚本文件。  

    对于无人参与的管理中心站点或主站点安装，该脚本文件必须具有以下部分：  

    -   标识    
    -   选项    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    若要恢复站点，还必须包括脚本文件的以下部分：  

    -   标识  
    -   恢复

有关详细信息，请参阅 [Configuration Manager 的无人参与站点恢复](/sccm/protect/understand/unattended-recovery)。  

若要了解将在无人参与的安装脚本文件中使用的一系列密钥和值，请查看[无人参与的安装程序脚本文件密钥](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)。  

## <a name="about-the-command-line-script-file"></a>关于命令行脚本文件  
 对于无人参与的 Configuration Manager 安装，可使用命令行选项 **/SCRIPT** 运行安装程序，并指定包含安装选项的脚本文件。 使用此方法支持以下任务：  

-   安装管理中心站点  
-   安装主站点  
-   安装 Configuration Manager 控制台  
-   恢复站点  

> [!NOTE]  
>  你无法使用无人参与脚本文件将评估版站点升级为 Configuration Manager 的许可版安装。  

### <a name="the-cdlatest-key-name"></a>CDLatest 密钥名称
使用 CD.Latest 文件夹中的介质运行以下四个安装选项的脚本化安装时，你的脚本必须包含值为 **1** 的 **CDLatest** 密钥：
- 安装新的管理中心站点
- 安装新的主站点
- 恢复管理中心站点
- 恢复主站点

该值不支持用于从 Microsoft 批量许可站点中获取的安装介质。
请参阅[命令行选项](/sccm/core/servers/deploy/install/command-line-options-for-setup)获取有关如何在脚本文件中使用此密钥名称的信息。



### <a name="create-the-script"></a>创建脚本
[使用用户界面运行安装程序以安装站点](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)时会自动创建安装脚本。  在向导的“摘要”页上确认设置时，会发生以下情况：  

-   安装程序创建脚本 **%TEMP%\ConfigMgrAutoSave.ini**。  在使用之前，你可以重命名此文件，但它必须保留 .ini 文件扩展名。  
-   无人参与安装脚本包含你在向导中选择的设置。  
-   创建了脚本后，你可以修改脚本以在层次结构中安装其他站点。  
-   然后，你可以使用此脚本来执行 Configuration Manager 的无人参与安装。  

此脚本文件提供的信息与安装向导提示输入的信息相同，不同的是没有默认设置。   
针对适用于要使用的安装类型的安装程序项，必须指定所有值。   

当安装程序创建无人参与的安装脚本时，会使用安装过程中输入的产品密钥值填充该脚本。 它可以是有效的产品密钥，或是安装 Configuration Manager 评估版时所用的 **EVAL**。 将填入脚本中的产品密钥值，便于完成先决条件检查。   

当安装程序启动实际站点安装时，会再次写入自动创建的脚本以清除它创建的脚本中的产品密钥值。 在为无人参与的新站点安装使用脚本之前，可编辑该脚本以提供有效的产品密钥，或指定 Configuration Manager 的评估版安装。  

### <a name="section-names-key-names-and-values"></a>部分名称、项名称和值
脚本包含部分名称、项名称和值。 请注意下列信息：
-   所需部分项名称因你正在为其编写脚本的安装类型而异。
-   部分内项的顺序和文件中部分的顺序并不重要。     
-   项不区分大小写。  
-   当你为项提供值时，项名称后面必须跟一个等号 (=) 以及该项的值。    

> [!TIP]  
>  若要查看完整的选项集，请参阅[适用于安装程序和脚本的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md)。  

## <a name="use-the-script-setup-command-line-option"></a>使用 /SCRIPT 安装程序命令行选项

-   必须使用安装程序脚本文件，并指定 **/SCRIPT** 安装程序命令行选项后面的文件名称。 请注意下列信息：   
    -   该文件名必须有 **.ini** 文件扩展名。  
    -   如果在命令提示符处引用安装程序脚本文件，则必须提供文件的完整路径。 例如，如果安装程序初始化文件的名称为 Setup.ini，并且此文件存储在 C:\Setup 文件夹中，请在命令提示符处键入：**setup /script c:\setup\setup.ini**。  

-   运行安装程序的帐户必须具有计算机上的“管理员”权限。 使用无人参与脚本运行安装程序时，请使用“以管理员身份运行”选项打开命令提示符窗口。   
