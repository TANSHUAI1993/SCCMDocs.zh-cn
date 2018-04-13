---
title: 安装控制台
titleSuffix: Configuration Manager
description: 安装 Configuration Manager 控制台以连接到管理中心站点或主站点。
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 05d19258b9bfc2a033eb4d7974f17fc0eb3d4c72
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2018
---
# <a name="install-the-system-center-configuration-manager-console"></a>安装 System Center Configuration Manager 控制台

*适用范围：System Center Configuration Manager (Current Branch)*

管理员使用 Configuration Manager 控制台管理 Configuration Manager 环境。 每个 Configuration Manager 控制台可以连接到管理中心站点或主站点。 但是，无法将 Configuration Manager 控制台连接到辅助站点。

> [!NOTE]  
>  管理员根据分配给其用户帐户的权限在控制台中查看对象。 有关基于角色的管理的详细信息，请参阅[基于角色的管理的基础](../../../../core/understand/fundamentals-of-role-based-administration.md)。  

 安装站点服务器时，可同时安装 Configuration Manager 控制台。 要安装独立于站点服务器安装的控制台，请运行独立安装程序。  

 请按照以下过程，使用独立安装程序安装 Configuration Manager 控制台。  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>始终使用安装向导安装 Configuration Manager 控制台  

1.  验证满足这些要求：  

    -  具有控制台的目标计算机上的本地“管理员”权限。  

    -   具有 Configuration Manager 控制台安装文件位置的**读取**权限。  

2.  请转到以下位置之一：  

    -   在站点服务器上，转到：`<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   从 Configuration Manager 源介质，转到：`<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  最佳做法是，从站点服务器而不是从 System Center Configuration Manager 安装介质启动 Configuration Manager 控制台安装程序。 安装站点服务器时，它会将 Configuration Manager 控制台安装文件和受支持的站点语言包复制到 Tools\ConsoleSetup 子文件夹中。 从安装介质安装 Configuration Manager 控制台始终安装英文版本。 即使站点服务器支持不同语言，或目标计算机的 OS 设置为不同语言，也会发生此行为。 你可以根据需要将 **ConsoleSetup** 文件夹复制到替代位置以启动安装。

3.  若要打开 Configuration Manager 控制台安装向导，请双击“consolesetup.exe”。  

    > [!IMPORTANT]  
    >  请始终使用 consoleSetup.exe 来安装 Configuration Manager 控制台。 虽然可通过运行 adminconsole.msi 来安装 Configuration Manager 控制台，但此方法不会运行先决条件或依赖项检查。 安装程序可能无法正确安装。  

4.  在向导中，选择“下一步”。  

5.  在“站点服务器”页上，输入 Configuration Manager 控制台将连接的站点服务器的完全限定的域名 (FQDN)。  

6.  在“安装文件夹”页面上，输入 Configuration Manager 控制台的安装文件夹。 文件夹路径不得包含尾随空格或 Unicode 字符。  

7.  在“客户体验改善计划”页上，选择是否参加客户体验改善计划 (CEIP)。  
    > [!Note]  
    > 从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。

8.  在“准备安装”页面上，选择“安装”以安装 Configuration Manager 控制台。  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>从命令提示符安装 Configuration Manager 控制台  

1.  在安装 Configuration Manager 控制台的服务器上，打开命令提示符窗口并转到以下位置之一：  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  从命令提示符安装 Configuration Manager 控制台始终安装英文版本。 即使目标计算机的 OS 设置为不同语言，也会发生此行为。 若要以非英语语言安装 Configuration Manager 控制台，则必须[使用安装向导安装 Configuration Manager 控制台](#to-install-the-configuration-manager-console-by-using-the-setup-wizard)。  

2.  在命令提示符处，键入“consolesetup.exe”。 从以下命令行选项中进行选择：  

|  命令行选项     | 说明     |
  |-------------|-------------|
  |/q|以无人参与的方式安装 Configuration Manager 控制台。 使用此选项时，需要 **EnableSQM**、 **TargetDir**和 **DefaultSiteServerName** 选项。|  
  |/uninstall|卸载 Configuration Manager 控制台。 与 /q 选项配合使用时，请首先指定此选项。|  
  |LangPackDir|指定包含语言文件的文件夹的路径。 你可以使用 **安装程序下载程序** 下载语言文件。 如果未使用此选项，则安装程序会在当前文件夹中查找语言文件夹。 如果未找到语言文件夹，则安装程序仅继续安装英文版。 有关详细信息，请参阅[安装程序下载程序](setup-downloader.md)。|  
  |TargetDir|指定安装文件夹以安装 Configuration Manager 控制台。 当你使用 **/q** 选项时，需要此选项。|  
  |EnableSQM|指定是否要加入客户体验改善计划 (CEIP)。 使用 **1** 的值加入 CEIP，使用 **0** 的值不加入计划。 当你使用 **/q** 选项时，需要此选项。</br></br>注意：从 Configuration Manager 版本 1802 开始，从产品中删除了 CEIP 功能。|  
  |DefaultSiteServerName|指定打开控制台时控制台所连接到的站点服务器的 FQDN。 当你使用 **/q** 选项时，需要此选项。|  


  ### <a name="examples"></a>示例

  -  `consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com`  

  -  `consolesetup.exe /uninstall /q`  
