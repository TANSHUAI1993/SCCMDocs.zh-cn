---
title: 如何使用转换插件
titleSuffix: Configuration Manager
description: 使用包转换管理器插件自定义分析和转换进程。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 5ed885ba459a584939881235e44d632515138cdf
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896356"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>如何使用包转换管理器插件

适用范围：System Center Configuration Manager (Current Branch)

<!--1357861-->

包转换管理器插件可帮助你自定义分析和转换进程。 若要使用包转换管理器插件，请编写执行自定义操作的可执行文件或脚本文件。 然后编辑配置文件 Microsoft.ConfigurationManagement.exe.config，以调用可执行文件或脚本。 用于编写脚本的最通用语言是 VBScript 或 PowerShell。

对于每个包，包转换管理器插件运行一次。 如果一次分析或转换多个包，包转换管理器插件每次都会运行。

> [!NOTE]  
> 有关 Configuration Manager 配置文件中的包转换管理器元素的详细信息，请参阅[包转换管理器插件配置 XML 的技术参考](/sccm/apps/pcm/plugin-config-xml)。



## <a name="default-process"></a>默认进程

默认情况下，包转换管理器执行以下操作：

1.  读取一个 Configuration Manager 包。  

2.  从包创建一个应用程序并添加默认属性。  

3.  分析该应用程序并确定包就绪状态。  

4.  根据包转换管理器操作，执行以下操作之一：  

    - 分析：在 Configuration Manager 控制台中显示包就绪状态。  

    - 转换：将应用程序写入 Configuration Manager 数据库。  


## <a name="plug-in-based-process"></a>基于插件的过程 

使用插件时，包转换管理器执行以下操作：

1.  读取一个 Configuration Manager 包。  

2.  从包创建一个应用程序并添加默认属性。  

3.  将应用程序转换为 XML。 然后将该文件保存到磁盘。  

4.  运行插件脚本来修改应用程序 XML。 有关详细信息，请参阅[包转换管理器插件配置 XML 的技术参考](/sccm/apps/pcm/plugin-config-xml)。  

5.  将应用程序 XML 转换为 Configuration Manager 应用程序。  

6.  分析该应用程序并确定包就绪状态。  

7.  根据包转换管理器操作，执行以下操作之一：  

    - 分析：在 Configuration Manager 控制台中显示包就绪状态。  

    - 转换：将应用程序写入 Configuration Manager 数据库。  



## <a name="see-also"></a>另请参阅

[包转换管理器插件配置 XML 的技术参考](/sccm/apps/pcm/plugin-config-xml)
