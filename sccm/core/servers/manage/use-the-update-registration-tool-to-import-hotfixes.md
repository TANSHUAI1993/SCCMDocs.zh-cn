---
title: "更新注册工具 | Microsoft Docs"
description: "了解何时以及如何使用更新注册工具来手动将更新导入 Configuration Manager 控制台。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 35a4c201f73469fdfaa5bb8629e91886f7ae8751
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>使用更新注册工具将修补程序导入 System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 的某些更新无法从 Microsoft 云服务获取，只能在带外获取。 用于解决特定问题的受限版本修补程序是一个示例。   
必须安装带外版本，并且更新或修补程序文件名以扩展名 **update.exe** 结尾时，需使用**更新注册工具**手动将更新导入 Configuration Manager 控制台。 该工具使你可以提取更新包并将它传输到站点服务器，然后向 Configuration Manager 控制台注册更新。  

 如果修补程序文件有 **.exe** 文件扩展名（不是 **update.exe**），请参阅[使用修补程序安装程序来安装 System Center Configuration Manager 的更新](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  本主题提供有关如何安装更新 System Center Configuration Manager 的修补程序的常规指导。 有关特定修补程序或更新的详细信息，请参阅 Microsoft 支持上该更新的相应知识库 (KB) 文章。  

 **使用更新注册工具的先决条件：**  

-   只有以 **.update.exe** 扩展名结尾的带外更新才能使用此工具安装  

-   该工具自包含有直接从 Microsoft 获取的各个更新  

-   该工具不依赖于服务连接点的模式  

-   该工具必须在承载服务连接点的计算机上运行  

-   运行该工具的计算机（服务连接点计算机）必须安装 .NET Framework 4.52  

-   用于运行该工具的帐户必须在托管服务连接点的计算机上具有“本地管理员”权限（工具在此计算机上运行）  

-   用于运行该工具的帐户必须对托管服务连接点的计算机上的以下文件夹具有“写入”权限：**&lt;ConfigMgr Installation directory\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>使用更新注册工具  

1.  在承载服务连接点的计算机上：  

    -   使用管理特权打开命令提示符，然后将目录更改为包含 **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>ConfigMgr.Update.exe** 的位置  

2.  运行以下命令以启动更新注册工具：  

    -   **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-ConfigMgr.Update.exe**  

    修补程序进行注册之后，它会在 24 小时内在控制台中显示为新的更新。  你可以加快此进程：

    - 打开 Configuration Manager 控制台并转到“管理” > “更新和服务”，然后单击“检查更新”。 （在版本 1702 之前，“更新和服务”在“管理” > “云服务”下。） 

    更新注册工具会将其操作记录到本地计算机上的 .log 文件。 该日志文件与修补程序 .exe 文件同名，并且会写入到 **%SystemRoot%Temp** 文件夹中。  

     注册更新之后，可以关闭更新注册工具。  

3.  打开 Configuration Manager 控制台并导航到“管理” > “更新和服务”。 现在即可安装之前导入的修补程序。 （在版本 1702 之前，“更新和服务”在“管理” > “云服务”下。）

 有关安装更新的信息，请参阅[安装 System Center Configuration Manager 在控制台的更新](../../../core/servers/manage/install-in-console-updates.md)  
