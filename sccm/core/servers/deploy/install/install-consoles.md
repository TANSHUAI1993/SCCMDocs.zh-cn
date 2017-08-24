---
title: "安装控制台 | Microsoft Docs"
description: "阅读安装 Configuration Manager 控制台以连接到管理中心站点或主站点的信息。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 88ecbc48fd03ce988f04408d0378844cbed1de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>安装 System Center Configuration Manager 控制台

*适用范围：System Center Configuration Manager (Current Branch)*

管理员使用 System Center Configuration Manager 控制台管理 Configuration Manager 环境。 每个 Configuration Manager 控制台可以连接到管理中心站点或主站点。 但是，无法将 Configuration Manager 控制台连接到辅助站点。

> [!NOTE]  
>  运行控制台的管理员可以看到哪些对象取决于他们的用户帐户所分配到的权限。 有关基于角色的管理的详细信息，请参阅 [System Center Configuration Manager 的基于角色的管理基础](../../../../core/understand/fundamentals-of-role-based-administration.md)。  

 可在站点服务器安装期间通过安装向导安装 Configuration Manager 控制台，或者可以运行使用安装向导的独立安装应用程序。  

 请按照以下过程使用独立应用程序安装 Configuration Manager 控制台。  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>始终使用安装向导安装 Configuration Manager 控制台  

1.  验证满足这些要求：  

    -  具有将在其中运行控制台的计算机上的**本地管理员**权限。  

    -   具有 Configuration Manager 控制台安装文件位置的**读取**权限。  

2.  请转到以下位置之一：  

    -   在站点服务器上，转到 **<*Configuration Manager 站点服务器安装路径*>\Tools\ConsoleSetup**。  

    -   从 Configuration Manager 源媒体中，浏览到 **<*Configuration Manager 源文件*>\Smssetup\Bin\I386**。  

    > [!TIP]  
    >  最佳做法是，从站点服务器而不是从 System Center Configuration Manager 安装媒体启动 Configuration Manager 控制台安装。 站点服务器安装方法会将 Configuration Manager 控制台安装文件和站点的支持语言包复制到 **Tools\ConsoleSetup** 子文件夹中。 从安装媒体中安装 Configuration Manager 控制台始终会安装英文版，与站点服务器上支持的语言或在计算机上运行的操作系统的语言设置无关。 你可以根据需要将 **ConsoleSetup** 文件夹复制到替代位置以启动安装。

3.  若要打开 Configuration Manager 控制台安装向导，请双击“consolesetup.exe”。  

    > [!IMPORTANT]  
    >  请始终使用 consoleSetup.exe 来安装 Configuration Manager 控制台。 虽然可以通过运行 AdminConsole.msi 来安装 Configuration Manager 控制台，但此方法不会运行先决条件或依赖关系检查，因此可能不会正确进行安装。  

4.  在向导中，选择“下一步”。  

5.  在“站点服务器”页面上，输入 Configuration Manager 控制台将连接的站点服务器的完全限定域名 (FQDN)。  

6.  在“安装文件夹”页面上，输入 Configuration Manager 控制台的安装文件夹。 文件夹路径不得包含尾随空格或 Unicode 字符。  

7.  在“客户体验改善计划”页上，选择是否参加客户体验改善计划 (CEIP)。  

8.  在“准备安装”页面上，选择“安装”以安装 Configuration Manager 控制台。  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>从命令提示符安装 Configuration Manager 控制台  

1.  在安装 Configuration Manager 控制台的服务器上，打开命令提示符窗口并转到以下位置之一：  

    -   **<*Configuration Manager 站点服务器安装路径*>\Tools\ConsoleSetup**  

    -   **<*Configuration Manager 安装媒体*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  从命令提示符中安装 Configuration Manager 控制台时，会始终安装英文版，与在计算机上运行的操作系统的语言设置无关。 若要以非英语语言安装 Configuration Manager 控制台，则必须[使用安装向导安装 Configuration Manager 控制台](#to-install-the-configuration-manager-console-by-using-the-setup-wizard)。  

2.  在命令提示符处，键入“consolesetup.exe”。 从以下命令行选项中进行选择。  

|  命令行选项     | 描述     |
  | :------------- | :------------- |
  |/q|以无人参与的方式安装 Configuration Manager 控制台。 使用此选项时，需要 **EnableSQM**、 **TargetDir**和 **DefaultSiteServerName** 选项。|  
  |/uninstall|卸载 Configuration Manager 控制台。 与 **/q** 选项配合使用时，必须首先指定此选项。|  
  |LangPackDir|指定包含语言文件的文件夹的路径。 你可以使用 **安装程序下载程序** 下载语言文件。 如果未使用此选项，则安装程序会在当前文件夹中查找语言文件夹。 如果未找到语言文件夹，则安装程序仅继续安装英文版。 有关详细信息，请参阅[安装程序下载程序](setup-downloader.md)。|  
  |TargetDir|指定安装文件夹以安装 Configuration Manager 控制台。 当你使用 **/q** 选项时，需要此选项。|  
  |EnableSQM|指定是否要加入客户体验改善计划 (CEIP)。 使用 **1** 的值加入 CEIP，使用 **0** 的值不加入计划。 当你使用 **/q** 选项时，需要此选项。|  
  |DefaultSiteServerName|指定打开控制台时控制台所连接到的站点服务器的 FQDN。 当你使用 **/q** 选项时，需要此选项。|  


  **示例：**

  -  c**onsolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
