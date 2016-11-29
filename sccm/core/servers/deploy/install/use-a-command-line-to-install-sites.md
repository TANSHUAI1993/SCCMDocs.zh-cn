---
title: "命令行安装 | System Center Configuration Manager"
description: "了解如何从命令提示符处运行 System Center Configuration Manager 安装程序来安装多个站点。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ea097188351cd60a13659e2860c5e0a2bac2c069

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>使用命令行安装 System Center Configuration Manager 站点

*适用范围：System Center Configuration Manager (Current Branch)*

 如果选择此项，则可以从命令提示符处运行 System Center Configuration Manager 安装程序来安装多个站点。

 ## <a name="supported-tasks-for-command-line-installs"></a>命令行安装支持的任务
 此种运行安装程序的方式支持以下站点安装和站点维护任务：

-   **从命令行安装管理中心站点或主站点：**  
  查看[适用于安装程序的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

 -  **修改管理中心站点或主站点中使用的语言：**  
    若要从命令行修改安装在站点上的语言（包括用于移动设备的语言），你必须：  

     -   从站点服务器上的 **&lt;ConfigMgrInstallationPath\>\Bin\X64** 运行安装程序
     -   使用 **/MANAGELANGS** 命令行选项
     -   指定语言脚本文件，该文件可指定你想要添加或删除的语言  

    例如，使用以下语法：**setupwpf.exe /MANAGELANGS &lt;language script file\>**  

    若要创建语言脚本文件，请使用[用于管理语言的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)中的信息  

 -  **将安装脚本文件用于无人参与的站点安装或站点恢复：**  
    你可以从命令行运行安装程序并指导安装程序使用安装脚本，以及运行无人参与的站点安装。 还可以使用此选项来恢复站点。    

    若要将脚本用于安装程序：  

    -   使用命令行选项 **/SCRIPT** 运行安装程序和指定脚本文件  

    -   必须使用所需的密钥和值配置脚本文件  

    对于管理中心站点或主站点的无人参与的安装，该脚本文件必须配置以下部分：  

    -   标识    
    -   选项    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    要恢复站点，则必须使用脚本文件的以下部分：  

    -   标识  

    -   恢复

     有关备份和恢复的详细信息，请参阅 Configuration Manager 主题中“备份和恢复”的“无人参与站点恢复脚本文件密钥”部分。  

    查看[无人参与的安装程序脚本文件密钥](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)，找到要在无人参与的安装脚本文件中使用的一系列密钥和值。  

## <a name="about-the-command-line-script-file"></a>关于命令行脚本文件  

 对于 Configuration Manager 的无人参与安装，可以使用命令行选项 **/SCRIPT** 运行安装程序，并指定包含安装选项的脚本文件。 此方法支持下列任务：  

-   安装管理中心站点  

-   安装主站点  

-   安装 Configuration Manager 控制台  

-   恢复站点  

> [!NOTE]  
>  你无法使用无人参与脚本文件将评估版站点升级为 Configuration Manager 的许可版安装。  

**创建脚本**：  
[使用用户界面运行安装程序以安装站点](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)时会自动创建安装脚本。  在向导的“摘要”  页上确认设置时：  

-   安装程序创建脚本 **%TEMP%\ConfigMgrAutoSave.ini**。  在使用之前，你可以重命名此文件，但它必须保留 .ini 文件扩展名。  

-   无人参与安装脚本包含你在向导中选择的设置。  

-   创建了脚本后，你可以修改脚本以在层次结构中安装其他站点。  

-   然后，你可以使用此脚本来执行 Configuration Manager 的无人参与安装。  

此脚本文件提供的信息与安装向导提示输入的信息相同，不同的是没有默认设置。   
必须为适用于你要使用的安装类型的安装程序项指定所有值。  

当安装程序创建无人参与安装脚本时，会使用你在安装过程中输入的产品密钥值填充该脚本。 它可以是有效的产品密钥，或在你安装评估版本的 Configuration Manager 时等同于 EVAL。 脚本中的产品密钥值已填充，以便能够完成先决条件检查。  

当安装程序启动实际站点安装时，会再次写入自动创建的脚本以清除它创建的脚本中的产品密钥值。 在为新站点的无人参与安装使用脚本之前，你可以编辑脚本以提供有效的产品密钥，或指定 Configuration Manager 的评估版安装。  

**脚本包含部分名称、密钥名称和值：**  

-   所需部分项名称因你正在为其编写脚本的安装类型而异  

-   部分内项的顺序和文件中部分的顺序并不重要  

-   项不区分大小写  

-   当你为项提供值时，项名称后面必须跟一个等号 (=) 以及该项的值  

> [!TIP]  
>  若要查看完整的选项集，请参阅[适用于安装程序和脚本的命令行选项](../../../../core/servers/deploy/install/command-line-options-for-setup.md)。  

## <a name="to-use-the-script-setup-command-line-option"></a>若要使用 /SCRIPT 安装程序命令行选项：

-   必须使用安装程序脚本文件并指定 **/SCRIPT** 安装程序命令行选项之后的文件名称。  

    -   该文件的名称必须有 **.ini** 文件扩展名  

    -   如果在命令提示符处引用安装程序脚本文件，则必须提供文件的完整路径。 例如，如果安装程序初始化文件的名称为 Setup.ini，并且此文件存储在 C:\Setup 文件夹中，请在命令提示符处键入：  **setup /script c:\setup\setup.ini**  

-   运行安装程序的帐户必须具有计算机上的管理凭据。 使用无人参与脚本运行安装程序时，请通过使用 **Run as administrator**启动命令提示符。  



<!--HONumber=Nov16_HO1-->


