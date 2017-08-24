---
title: "先决条件检查程序 | Microsoft Docs"
description: "了解如何使用先决条件检查程序识别并修复可能会阻止安装站点或站点系统角色的问题。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f0d44f82a0b6068f8cecc5808774677eccb0f8d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>System Center Configuration Manager 的先决条件检查程序

*适用范围：System Center Configuration Manager (Current Branch)*

 在运行安装程序安装或升级 System Center Configuration Manager 站点之前，或在新的服务器上安装站点系统角色之前，可从想要用于验证服务器是否已准备就绪的 Configuration Manager 版本，使用此独立应用程序 (**Prereqchk.exe**)。 使用先决条件检查程序识别并修复会阻止安装站点或站点系统角色的问题。  

> [!NOTE]  
>  先决条件检查程序始终作为安装程序的一部分运行。  

情况下，运行先决条件检查程序时：  

-   会对运行它的服务器进行验证。  
-   扫描本地计算机查找现有站点服务器，且仅运行适用于站点的检查。  
-   如果未检测到现有站点，则会运行所有先决条件规则。  
-   它检查规则以验证安装程序所需的软件和设置是否已安装。 必备软件可能需要未经先决条件检查程序验证的其他配置或软件更新。  
-   它会在计算机系统驱动器的 **ConfigMgrPrereq.log** 文件中记录其结果。 日志文件可能包含应用程序界面中未显示的其他信息。  

在命令提示符处运行先决条件检查程序并指定具体的命令行选项：  

-   先决条件检查程序仅执行与命令行中指定的站点服务器或站点系统关联的检查。  
-   若要检查远程计算机，用户帐户必须具有远程计算机的管理员权限。  

若要深入了解先决条件检查程序所执行的检查，请参阅 [System Center Configuration Manager 的先决条件检查列表](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)。  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>将先决条件检查程序文件复制到另一台计算机  

1.  在 Windows 资源管理器中，转到以下位置之一：  

    -   **&lt;*Configuration Manager 安装介质*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager 安装路径*\>\BIN\X64**  

2.  将以下文件复制到另一台计算机上的目标文件夹：  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>运行先决条件检查程序进行默认检查  

1.  在 Windows 资源管理器中，转到以下位置之一：  

    -   **&lt;*Configuration Manager 安装介质*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager 安装路径*\>\BIN\X64**  

2.  运行 **prereqchk.exe** 以启动先决条件检查程序。   
    先决条件检查程序将检测现有站点，如果找到，则执行针对升级准备情况的检查。 如果未找到站点，则执行所有检查。 “站点类型”  列提供有关规则与之关联的站点服务器或站点系统的信息。  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>针对所有默认检查，从命令提示符运行先决条件检查程序  

1.  打开命令提示符窗口并将目录更改为以下位置之一：  

    -   **&lt;*Configuration Manager 安装介质*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager 安装路径*\>\BIN\X64**  

2.  输入  **prereqchk.exe /LOCAL** 以启动先决条件检查程序，并在服务器上运行所有先决条件检查。  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>从命令提示符运行先决条件检查程序以使用各选项  

1.  打开命令提示符窗口并将目录更改为以下位置之一：  

    -   **&lt;*Configuration Manager 安装介质*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager 安装路径*\>\BIN\X64**  

2.  输入 **prereqchk.exe**，并在后面添加以下一个或多个命令行选项。  

    例如，可使用以下方法检查主站点：  

       **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN of SQL Server\> /SDK &lt;FQDN of SMS Provider\> [/JOIN &lt;FQDN of central administration site\>] [/MP &lt;FQDN of management point\>] [/DP &lt;FQDN of distribution point\>]**  

    **管理中心站点服务器：**  

    -   **/NOUI**  

         不需要。 启动先决条件检查程序而不显示用户界面。 你必须在命令行中的任何其他选项之前指定此选项。  

    -   **/CAS**  

         必需。 验证本地计算机是否满足管理中心站点的要求。  

    -   **/SQL &lt;*FQDN of SQL Server*>**  

         必需。 使用完全限定的域名 (FQDN)，验证指定计算机是否满足用于托管 Configuration Manager 站点数据库的 SQL Server 的要求。  

    -   **/SDK &lt;*FQDN of SMS Provider*>**  

         必需。 验证指定计算机是否满足 SMS 提供程序的要求。  

    -   **/Ssbport**  

         不需要。 验证防火墙例外是否生效以允许 SQL Server Service Broker (SSB) 端口上的通信。 默认 SSB 端口为 4022。  

    -   **InstallDir &lt;*Configuration Manager 安装路径*>**  

         不需要。 验证站点安装的最小磁盘空间要求。  

    **主站点服务器：**  

    -   **/NOUI**  

        不需要。 启动先决条件检查程序而不显示用户界面。 你必须在命令行中的任何其他选项之前指定此选项。  

    -   **/PRI**  

         必需。 验证本地计算机是否满足主站点的要求。  

    -   **/SQL &lt;*FQDN of SQL Server*>**  

         必需。 验证指定计算机是否满足用于托管 Configuration Manager 站点数据库的 SQL Server 的要求。  

    -   **/SDK &lt;*FQDN of SMS Provider*>**  

         必需。 验证指定计算机是否满足 SMS 提供程序的要求。  

    -   **/JOIN &lt;*FQDN of central administration site*>**  

         不需要。 验证本地计算机是否满足用于连接到管理中心站点服务器的要求。  

    -   **/MP &lt;*FQDN of management point*>**  

         不需要。 验证指定计算机是否满足管理点站点系统角色的要求。 只有当你使用 **/PRI** 选项时，才支持此选项。  

    -   **/DP &lt;*FQDN of distribution point*>**  

         不需要。 验证指定计算机是否满足分发点站点系统角色的要求。 只有当你使用 **/PRI** 选项时，才支持此选项。  

    -   **/Ssbport**  

         不需要。 验证防火墙例外是否生效以允许 SSB 端口上的通信。 默认 SSB 端口为 4022。  

    -   **InstallDir &lt;*Configuration Manager 安装路径*>**  

         不需要。 验证站点安装的最小磁盘空间要求。  

    **辅助站点服务器：**  

    -   **/NOUI**  

         不需要。 启动先决条件检查程序而不显示用户界面。 你必须在命令行中的任何其他选项之前指定此选项。  

    -   **/SEC &lt;*FQDN of secondary site server*>**  

         必需。 验证指定计算机是否满足辅助站点的要求。  

    -   **/INSTALLSQLEXPRESS**  

         不需要。 验证是否可在指定计算机上安装 SQL Server Express。  

    -   **/Ssbport**  

         不需要。 验证防火墙例外是否生效以允许 SSB 端口的通信。 默认 SSB 端口为 4022。  

    -   **/Sqlport**  

         不需要。 验证防火墙例外是否生效以允许 SQL Server 服务端口的通信，并且该端口未由 SQL Server 的另一个命名实例使用。 默认端口为 1433。  

    -   **InstallDir &lt;*Configuration Manager 安装路径*>**  

         不需要。 验证站点安装的最小磁盘空间要求。  

    -   **/SourceDir**  

         不需要。 验证辅助站点的计算机帐户是否可访问承载安装程序源文件的文件夹。  

   **Configuration Manager 控制台：**  

    -   **/Adminui**  

         必需。 验证本地计算机是否满足 Configuration Manager 的安装要求。  

3.  在先决条件检查程序用户界面中，先决条件检查程序将在“先决条件结果”部分中创建一个已发现问题的列表。  

    -   单击列表中的项目以了解有关如何解决问题的详细信息。  
    -   在安装站点服务器、站点系统或 Configuration Manager 控制台之前，必须解决列表中状态为“错误”的所有项目。  
    -   也可打开系统驱动器根目录中的 **ConfigMgrPrereq.log** 文件，查看先决条件检查程序结果。 该日志文件可能包含先决条件检查程序用户界面中未显示的其他信息。  
