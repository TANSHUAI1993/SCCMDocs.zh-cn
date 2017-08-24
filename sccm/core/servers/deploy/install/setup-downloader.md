---
title: "安装程序下载程序 | Microsoft Docs"
description: "阅读有关此独立应用程序的信息，该应用程序可确保站点安装使用的是当前版本的关键安装文件。"
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b72148ecc16141843178cbd220fe021fab8be992
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>System Center Configuration Manager 安装程序下载程序

*适用范围：System Center Configuration Manager (Current Branch)*

在运行安装程序安装或升级 System Center Configuration Manager 站点之前，可从要安装的 Configuration Manager 版本中使用安装程序下载程序独立应用程序下载更新的安装程序文件。  

使用更新的安装程序文件可确保站点安装使用当前版本的关键安装文件。 在概述中：   
-   在启动安装程序之前使用安装程序下载程序来下载文件时，指定一个文件夹来放置这些文件。  
-   用来运行安装程序下载程序的帐户必须具有对此下载文件夹的“完全控制”权限。  
-   运行安装程序以安装或升级站点时，可以指示它使用以前下载文件的本地副本。 这样在开始安装或升级站点时，安装程序无需连接到 Microsoft。  
-   你可将相同的安装程序文件本地副本用于后续站点安装或升级。  

安装程序下载程序下载以下类型的文件：  
-   必需的先决条件可再发行文件  
-   语言包  
-   安装程序的最新产品更新  

可使用两个选项来运行安装程序下载程序：
- 使用用户界面运行应用程序
- 对于命令行选项，请在命令提示符处运行应用程序


## <a name="run-setup-downloader-with-the-user-interface"></a>使用用户界面运行安装程序下载程序  

1.  在具有 Internet 访问的计算机上，打开 Windows 资源管理器，并转到 &lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64。  

2.  若要打开安装程序下载程序，请双击“Setupdl.exe”。   

3. 指定将承载更新的安装文件的文件夹的路径，然后单击“下载”。 安装程序下载程序将验证当前位于下载文件夹中的文件。 它仅下载缺少的文件或比现有文件更新的文件。 安装程序下载程序将创建用于下载的语言的子文件夹和其他所需的子文件夹。  

4.  若要查看下载结果，请打开驱动器 C 的根目录中的“ConfigMgrSetup.log”文件。  

## <a name="run-setup-downloader-from-a-command-prompt"></a>从命令提示符运行安装程序下载程序  

1.  在命令提示符窗口中，转到 &lt;Configuration Manager installation media\>\SMSSETUP\BIN\X64**。   

2.  若要打开安装程序下载程序，请运行“Setupdl.exe”。

    可将以下命令行选项配合“Setupdl.exe”使用：   

    -   **/VERIFY**：使用此选项来验证下载文件夹中的文件（包括语言文件）。 查看驱动器 C 根目录中的 ConfigMgrSetup.log 文件，获取过期文件的列表。 使用此选项时不会下载文件。  

    -   **/VERIFYLANG**：使用此选项来验证下载文件夹中的语言文件。 查看驱动器 C 根目录中的 ConfigMgrSetup.log 文件，获取过期语言文件的列表。

    -   **/LANG**：使用此选项以便仅将语言文件下载到下载文件夹。  

    -   **/NOUI**：使用此选项以启动安装程序下载程序而不显示用户界面。 如果使用此选项，必须指定“下载路径”作为命令提示符中命令的一部分。  

    -   **&lt;DownloadPath\>**：可以指定下载文件夹的路径以自动启动验证或下载过程。 使用“/NOUI”选项时必须指定下载路径。 如果未指定下载路径，则必须在安装程序下载程序打开时指定该路径。 安装程序下载程序会创建文件夹（如果不存在）。  

    示例命令：

    -   **setupd &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的文件，然后仅下载缺少的文件或比现有文件版本更新的文件。     

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   安装程序下载程序将启动并验证指定下载文件夹中的文件。  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的文件，然后仅下载缺少的文件或比现有文件更新的文件。  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   安装程序下载程序将启动，验证指定下载文件夹中的语言文件，然后仅下载缺少的语言文件或比现有文件更新的语言文件。  

    -   **setupdl /VERIFY**  

        -   安装程序下载程序将启动，然后你必须指定下载文件夹的路径。 接下来，单击“验证”之后，安装程序下载程序将验证下载文件夹中的文件。  

3.  若要查看下载结果，请打开驱动器 C 的根目录中的“ConfigMgrSetup.log”文件。
