---
title: 安装控制台
titleSuffix: Configuration Manager
description: 安装 Configuration Manager 控制台以连接到管理中心站点或主站点。
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1469845ce89b0de08a687baf3d518c1bd6d5294d
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069528"
---
# <a name="install-the-configuration-manager-console"></a>安装 Configuration Manager 控制台

适用范围：System Center Configuration Manager (Current Branch)

管理员使用 Configuration Manager 控制台管理 Configuration Manager 环境。 每个 Configuration Manager 控制台都可以连接到管理中心站点 (CAS) 或主站点。 但是，无法将 Configuration Manager 控制台连接到辅助站点。

Configuration Manager 控制台始终安装在 CAS 或主站点的站点服务器上。 要安装独立于站点服务器安装的控制台，请运行独立安装程序。  



## <a name="prerequisites"></a>先决条件

- 具有控制台的目标计算机上的本地“管理员”权限。  

- 具有 Configuration Manager 控制台安装文件位置的**读取**权限。  



## <a name="source-paths"></a>源路径

决定要使用的源路径：  

- 站点服务器上的 ConsoleSetup 文件夹：`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    安装站点服务器时，它会将控制台安装文件和受支持的站点语言包复制到 Tools\ConsoleSetup 子文件夹中。 你可以根据需要将 **ConsoleSetup** 文件夹复制到替代位置以启动安装。 更新站点时，它会始终将其本地版本保持为最新状态。  

- Configuration Manager 安装介质：`<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    从安装介质安装 Configuration Manager 控制台始终安装英文版本。 即使站点服务器支持不同语言，或目标计算机的 OS 设置为不同语言，也会发生此行为。  

如果可能，请从 ConsoleSetup 文件夹（而不是从源媒体中）启动控制台安装程序。

> [!Important]  
> 请勿使用 CD.Latest 源文件安装控制台。 不支持此方案，它可能会导致控制台安装出现问题。 有关详细信息，请参阅 [CD.Latest 文件夹](/sccm/core/servers/manage/the-cd.latest-folder#unsupported-scenarios)。<!-- SCCMDocs issue 1359 -->  

如果创建用于在其他计算机上安装控制台的程序包，请确保该程序包包含以下文件：<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab（从版本 1902 开始）
- ConfigMgr.AC_Extension.amd64.cab（从版本 1902 开始）



## <a name="use-the-setup-wizard"></a>使用安装向导  

1. 浏览到源路径，并打开 ConsoleSetup.exe。  

    > [!IMPORTANT]  
    > 请始终使用 ConsoleSetup.exe 来安装控制台。 虽然可通过运行 AdminConsole.msi 来安装 Configuration Manager 控制台，但此方法不会运行先决条件或依赖项检查。 安装程序可能无法正确安装。  

2. 在向导中，选择“下一步”。  

3. 在“站点服务器”页上，输入 Configuration Manager 控制台将连接的站点服务器的完全限定的域名 (FQDN)。  

4. 在“安装文件夹”页面上，输入 Configuration Manager 控制台的安装文件夹。 文件夹路径不能包含尾随空格或 Unicode 字符。  

5. 在“客户体验改善计划”页上，选择是否参加客户体验改善计划 (CEIP)。  

    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

6. 在“准备安装”页上，选择“安装”。  



## <a name="install-from-a-command-prompt"></a>通过命令提示符安装  

> [!TIP]  
> 从命令提示符安装 Configuration Manager 控制台始终安装英文版本。 即使目标计算机的 OS 设置为不同语言，也会发生此行为。 若要使用英语以外的语言安装 Configuration Manager 控制台，请[使用安装向导](#use-the-setup-wizard)。  


### <a name="consolesetupexe-command-line-options"></a>ConsoleSetup.exe 命令行选项

#### <a name="q"></a>/q

以无人参与的方式安装 Configuration Manager 控制台。 使用此选项时，需要 **EnableSQM**、 **TargetDir**和 **DefaultSiteServerName** 选项。

#### <a name="uninstall"></a>/uninstall

卸载 Configuration Manager 控制台。 与 /q 选项配合使用时，请首先指定此选项。

#### <a name="langpackdir"></a>LangPackDir

指定包含语言文件的文件夹的路径。 你可以使用 **安装程序下载程序** 下载语言文件。 如果不使用此选项，则安装程序会在当前文件夹中查找语言文件夹。 如果未找到语言文件夹，则安装程序仅继续安装英文版。 有关详细信息，请参阅[安装程序下载程序](setup-downloader.md)。

#### <a name="targetdir"></a>TargetDir

指定安装文件夹以安装 Configuration Manager 控制台。 当你使用 **/q** 选项时，需要此选项。

#### <a name="enablesqm"></a>EnableSQM

指定是否要加入客户体验改善计划 (CEIP)。 使用 **1** 的值加入 CEIP，使用 **0** 的值不加入计划。 当你使用 **/q** 选项时，需要此选项。

> [!Important]  
> 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。 使用参数将导致安装失败。

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

指定打开控制台时控制台所连接到的站点服务器的 FQDN。 当你使用 **/q** 选项时，需要此选项。


### <a name="examples"></a>示例

> [!Important]  
> 对于版本 1802 和更高版本，不包括 EnableSQM 参数

#### <a name="silent-install"></a>无提示安装

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>无提示安装语言包

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>无提示卸载

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>另请参阅

管理员根据分配给其用户帐户的权限在控制台中查看对象。 有关详细信息，请参阅[基于角色的管理基础](/sccm/core/understand/fundamentals-of-role-based-administration)。

有关导航 Configuration Manager 控制台的基础知识的详细信息，请参阅[使用控制台](/sccm/core/servers/manage/admin-console)。
