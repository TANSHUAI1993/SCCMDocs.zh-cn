---
title: "安装程序下载程序 | System Center Configuration Manager"
description: "阅读有关此独立应用程序的信息，该应用程序可确保站点安装使用的是当前版本的关键安装文件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 574e4d450126d2c4411292b6dd52e18049d296f6

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>System Center Configuration Manager 安装程序下载程序

*适用范围：System Center Configuration Manager (Current Branch)*

在运行安装程序以安装或升级 System Center Configuration Manager 站点之前，可以从要安装的 Configuration Manager 版本使用此独立应用程序 (**Setupdl.exe**) 来下载安装程序所需已更新的安装程序文件。  

使用更新的安装程序文件可确保站点安装使用当前版本的关键安装文件：  

-   在启动安装程序之前使用安装程序下载程序来下载文件时，指定一个文件夹来放置这些文件。  

-   用来运行安装程序下载程序的帐户必须具有对此下载文件夹的“完全控制”权限。  

-   运行安装程序以安装或升级站点时，可以指示它使用以前下载文件的本地副本。 这样在开始安装或升级站点时，安装程序无需连接到 Microsoft。  

-   你可将相同的安装程序文件本地副本用于后续站点安装或升级。  

安装程序下载程序下载以下类型的文件：  

-   必需的先决条件可再发行文件  

-   语言包  

-   安装程序的最新产品更新  

可以使用以下两个选项来运行安装程序下载程序：  

## <a name="run-setup-downloader-with-the-user-interface"></a>使用用户界面运行安装程序下载程序  

1.  在具有 Internet 访问的计算机上，打开 Windows 资源管理器，并浏览至 **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  双击“Setupdl.exe”。 安装程序下载程序将打开。  

3.  指定将承载更新的安装文件的文件夹的路径，然后单击“下载”。 安装程序下载程序将验证文件当前是否已位于下载文件夹中，并只会下载缺少的文件或比现有文件新的文件。 安装程序下载程序将为下载的语言创建子文件夹。 安装程序下载程序将创建文件夹（如果不存在）。  

4.  查看驱动器 C 根目录中的 **ConfigMgrSetup.log** 文件以查看下载结果。  

## <a name="run-setup-downloader-from-a-command-prompt"></a>从命令提示符运行安装程序下载程序  

1.  打开命令提示符窗口，并浏览到 **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  运行 **setupdl.exe** 以打开安装程序下载程序。 或可将以下命令行选项配合 setupdl.exe 使用：  

    -   **/VERIFY**：使用此选项来验证下载文件夹中的文件（包括语言文件）。 查看驱动器 C 根目录中的 ConfigMgrSetup.log 文件以获得过期的文件的列表。 使用此选项时不会下载文件。  

    -   **/VERIFYLANG**：使用此选项来验证下载文件夹中的语言文件。 查看驱动器 C 根目录中的 ConfigMgrSetup.log 文件以获得过期的语言文件的列表/  

    -   **/LANG**：使用此选项以便仅将语言文件下载到下载文件夹。  

    -   **/NOUI**：使用此选项以启动安装程序下载程序而不显示用户界面。 如果使用此选项，必须指定“下载路径”作为命令行的一部分。  

    -   **&lt;DownloadPath\>**：可以指定下载文件夹的路径以自动启动验证或下载过程。 使用“/NOUI”选项时必须指定下载路径。 如果未指定下载路径，你必须在安装程序下载程序打开时指定该路径。 安装程序下载程序将创建文件夹（如果不存在）。  

    用法示例：  

    -   **setupd &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的文件，并仅下载缺少的文件或比现有文件更新的文件  

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   安装程序下载程序将启动并验证指定下载文件夹中的文件  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的文件，并仅下载缺少的文件或比现有文件更新的文件  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的语言文件，并仅下载缺少的语言文件或比现有文件更新的文件  

    -   **setupdl /VERIFY**  

        -   安装程序下载程序将启动，然后你必须指定下载文件夹的路径。 接下来，单击“验证”之后，安装程序下载程序将验证下载文件夹中的文件  

3.  查看驱动器 C 根目录中的 **ConfigMgrSetup.log** 文件以查看下载结果  



<!--HONumber=Nov16_HO1-->


