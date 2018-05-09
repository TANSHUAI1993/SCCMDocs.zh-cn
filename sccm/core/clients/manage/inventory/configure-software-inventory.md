---
title: 配置软件清单
titleSuffix: Configuration Manager
description: 配置软件清单，并从 Configuration Manager 中的软件清单中排除文件夹。
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 346ff3254f4c1833f49bf256cbf5ad0c489d77e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中配置软件清单

*适用范围：System Center Configuration Manager (Current Branch)*

此过程为软件清单配置默认客户端设置，并应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请创建自定义设备客户端设置，并将它分配给集合。 有关如何创建自定义设备设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。   

## <a name="to-configure-software-inventory"></a>若要配置软件清单  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置”、“默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认设置”对话框中，选择“软件清单”。  

6.  在“设备设置”  列表中，配置以下值：  

    -   **启用客户端上的软件清单** - 从下拉列表中选择“True”。  

    -   **软件清单和文件收集日程安排** – 配置客户端收集软件清单和文件的间隔。   

7.  配置所需的客户端设置。 [关于 System Center Configuration Manager 中的客户端设置](../../../../core/clients/deploy/about-client-settings.md#software-inventory)主题中的[软件清单](../../../../core/clients/deploy/about-client-settings.md)部分中有客户端设置的清单。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 要为单个客户端启动策略检索，请参阅 [如何在 System Center Configuration Manager 中管理客户端](../../../../core/clients/manage/manage-clients.md)。  

 > [!TIP]  
        >   Inventoryprovider.log 中的错误代码 80041006 表示 WMI 提供程序内存不足。 即已达到提供程序的内存配额限制，清单提供程序无法继续工作。
在这种情况下，清单代理创建 0 条目的报表，所以没有报告任何清单项。 <br/>
此错误可能的解决方法是，缩小软件清单收集的范围。 如果在限制清单范围后出现了该错误，提高 [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) 类中定义的 [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) 属性可以算是一种解决方案。

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>从软件清单中排除文件夹  

1.  使用 Notepad.exe，创建名为 **Skpswi.dat**的空文件。  

2.  右键单击 Skpswi.dat 文件，然后单击“属性”。 在 Skpswi.dat 文件的文件属性中，选择“隐藏”  属性。  

3.  将 **Skpswi.dat** 文件放置在要从软件清单中排除的每个客户端硬盘或文件夹结构的根目录中。  

> [!NOTE]  
>  除非在客户端计算机上删除此文件，否则软件清单将不会再次列出该客户端驱动器清单。