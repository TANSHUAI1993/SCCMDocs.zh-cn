---
title: MDT 示例
titleSuffix: Microsoft Deployment Toolkit
description: 'Microsoft Deployment Toolkit 示例。 '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2018
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Microsoft Deployment Toolkit 示例指南  
 本指南是 Microsoft®Deployment Toolkit (MDT) 2013 的一部分，通过部署 Windows 操作系统和 Microsoft Office 来指导专家团队。 具体而言，本指南旨在提供特定部署方案的示例配置设置。  

> [!NOTE]
>  本文档中的 Windows 适用于 Windows 8.1、Windows 8、Windows 7、Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2 操作系统，除非另行说明。 MDT 不支持基于 ARM 处理器的 Windows 版本。 同样，MDT 指 MDT 2013，除非另行说明。  

 **使用本指南**  

 查看目录中的方案主题列表。  

1.  选择最能代表你的组织部署目标的方案。  

2.  查看所选方案的示例配置设置。  

3.  使用示例配置设置作为环境中配置设置的基础。  

4.  自定义环境的示例配置设置。  

 在许多情况下，可能需要多个方案才能完成环境的配置设置。  

 由于本指南仅包含示例配置设置，因此查看下表中列出的指南可进一步帮助自定义环境的配置设置。  

 |指南|本指南可帮助|  
 |-|-|  
 |《Microsoft System Center 2012 R2 Configuration Manager 的快速入门指南》 |使用 System Center 2012 R2 Configuration Manager 在新计算机部署方案中安装 Windows 8.1 操作系统。|  
 |《Lite Touch 安装的快速入门指南》 |使用可启动介质通过 Lite Touch 安装 (LTI) 在新计算机部署方案中安装 Windows 8.1 操作系统。|  
 |《用户驱动的安装的快速入门指南》 |使用用户驱动的安装和 System Center 2012 R2 Configuration Manager 在新计算机部署方案中安装 Windows 8.1 操作系统。|  
 |*使用 Microsoft Deployment Toolkit* |进一步自定义 Zero Touch Installation (ZTI) 和 LTI 部署中使用的配置文件。 本指南还提供了通用配置指南和配置设置的技术参考。|


## <a name="deploying-windows-8-applications-using-mdt"></a>使用 MDT 部署 Windows 8 应用程序  
 MDT 可部署具有 .appx 文件扩展名的 Windows 8 应用程序包。 这些应用程序包是 Windows 8 的新增包。 有关这些应用程序的详细信息，请参阅 [Windows 应用商店应用开发](http://msdn.microsoft.com/windows/apps)。  

 通过执行以下步骤，使用 MDT 来部署 Windows 8 应用程序：  

-   如[使用 LTI 部署 Windows 8 应用程序](#DeployWin8LTI)中所述，使用 LTI 部署 Windows 8 应用程序。  

-   如[使用 UDI 部署 Windows 8 应用程序](#DeployWin8UDI)中所述，使用用户驱动的安装 (UDI) 部署 Windows 8 应用程序。  

###  <a name="DeployWin8LTI"></a> 使用 LTI 部署 Windows 8 应用程序  
 像部署从命令行启动安装进程的任何其他应用程序一样，可使用 LTI 部署 Windows 8 应用程序。 可将 Windows 8 应用程序添加到 Deployment Workbench 的“应用程序”节点中的 LTI 部署。  

 **使用 LTI 部署 Windows 8 应用程序**  

1.  创建一个用于存储应用程序的网络共享文件夹。  

2.  将 Windows 8 应用程序复制到上一步中创建的网络共享文件夹中。  

     确保复制的 Windows 8 应用程序 .appx 文件和任何其他必需的文件（如 .cer 文件）包含应用程序证书。  

3.  使用“新建应用程序向导”在 Deployment Workbench 的“应用程序”节点中为 Windows 8 应用程序创建 LTI 应用程序项。  

     完成“新建应用程序向导”时，在“命令详细信息”向导页上的“命令行”中，键入“app_file_name”（其中 app_file_name 是Windows 8 应用程序的名称）。  

     有关如何在 Deployment Workbench 中完成“新建应用程序向导”的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的以下各部分：  

    -   “创建从部署共享部署的新应用程序”  

    -   “创建从另一个网络共享文件夹部署的新应用程序”  

4.  在 LTI 任务序列中选择上一步中创建的 LTI 应用程序项。  

###  <a name="DeployWin8UDI"></a> 使用 UDI 部署 Windows 8 应用程序  
 像部署从命令行启动安装进程的任何其他应用程序一样，可使用 UDI 部署 Windows 8 应用程序。 可在 UDI 向导设计器的“ApplicationPage”向导页上将 Windows 8 应用程序添加到 UDI 部署。  

> [!NOTE]
>  使用 UDI 部署 Windows 8 和 Windows 8 应用程序时需要 System Center 2012 R2 Configuration Manager。  

 **使用 UDI 部署 Windows 8 应用程序**  

1.  创建一个用于存储应用程序的网络共享文件夹。  

     此文件夹将成为此过程中稍后创建的 Configuration Manager 应用程序的源文件夹。  

2.  将 Windows 8 应用程序复制到上一步中创建的网络共享文件夹中。  

     确保复制的 Windows 8 应用程序 .appx 文件和任何其他必需的文件（如 .cer 文件）包含应用程序证书。  

3.  将 Windows 8 应用程序添加为 Configuration Manager 应用程序  

4.  在 Configuration Manager 控制台中使用“创建应用程序向导”为 Windows 8 应用程序创建 Configuration Manager 应用程序项。  

     完成“创建应用程序向导”时，使用“创建部署类型向导”创建一个部署类型来部署 Windows 8 应用程序。 在“创建部署类型向导”的“内容”页上，在“安装程序”中键入“app_file_name”（其中 app_file_name 是Windows 8 应用程序的名称）。  

     有关如何在 Configuration Manager 控制台中完成“创建应用程序向导”的详细信息，请参阅 Configuration Manager 随附的 System Center 2012 Configuration Manager 文档库中的以下各部分：  

    -   [如何在 Configuration Manager 中创建应用程序](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [如何在 Configuration Manager 中创建部署类型](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [如何在 Configuration Manager 中管理应用程序和部署类型](http://technet.microsoft.com/library/gg682031)  

5.  确保 Configuration Manager 中的用户设备相关性 (UDA) 得到正确配置，以支持用户和设备之间的相关性便于部署 Configuration Manager 应用程序。  

     有关如何配置 UDA 以支持 Configuration Manager 应用程序部署的详细信息，请参阅[如何在 Configuration Manager 中管理用户设备相关性](http://technet.microsoft.com/library/gg699365)。  

6.  将步骤 4 中创建的应用程序部署到目标用户。  

     有关如何将应用程序部署到用户的详细信息，请参阅 [如何在 Configuration Manager 中部署应用程序](http://technet.microsoft.com/library/gg682082)。  

7.  使用 UDI 向导设计器配置“ApplicationPage”向导页以包含步骤 4 中创建的 Configuration Manager 应用程序。  

     有关如何使用 UDI 向导设计器配置“ApplicationPage”向导页的详细信息，请参阅 MDT 文档《用户驱动的安装的快速入门指南》中的“步骤 5-11：自定义目标计算机的 UDI 向导配置文件”部分。  

8.  在 UDI 任务序列中选择上一步中创建的 UDI 应用程序项。  

    > [!NOTE]
    >  Windows 8 应用程序不由任务序列安装，而是在用户首次使用 UDI 中以用户为中心的应用安装程序功能 (AppInstall.exe) 登录到目标计算机（如步骤 5 中配置的 UDA 设置所定义）时安装的。  

     有关 UDI 中以用户为中心的应用安装程序功能的详细信息，请参阅 MDT 文档《Toolkit 参考》中的“以用户为中心的应用安装程序参考”部分。  

## <a name="managing-mdt-using-windows-powershell"></a>使用 Windows PowerShell 管理 MDT  
 可使用 Deployment Workbench 和 Windows PowerShell 管理 MDT 部署共享。 MDT 包含 Windows PowerShell™ 管理单元 Microsoft.BDD.SnapIn，必须在使用 Windows PowerShell 中的 MDT 特定功能之前加载该单元。 MDT Windows PowerShell 管理单元包括：  

-   Windows PowerShell 提供程序 MDTProvider，提供对部署共享的内容的访问权限  

-   可以管理 MDT 部署共享的 Cmdlet  

 通过执行以下步骤，使用 Windows PowerShell 管理 MDT 部署共享：  

-   如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

-   如[使用 Windows PowerShell 创建部署共享](#CreateDeployShare)中所述，使用 Windows PowerShell 创建部署共享。  

-   如[使用 Windows PowerShell 查看部署共享属性](#ViewDeployShareProp)中所述，使用 Windows PowerShell 查看部署共享属性。  

-   如[使用 Windows PowerShell 查看部署共享列表](#ViewListDeployShare)中所述，使用 Windows PowerShell 查看部署共享列表。  

-   如[使用 Windows PowerShell 更新部署共享](#UpdateDeployShare)中所述，更新部署共享，生成新的 Windows 预安装环境 (Windows PE) 启动映像。  

-   如[使用 Windows PowerShell 更新链接的部署共享](#UpdateLinkedDeployShare)中所述，更新链接的部署共享，将内容从部署共享复制到链接的部署共享。  

-   如[使用 Windows PowerShell 更新部署介质](#UpdateDeployMedia)中所述，更新部署介质，将内容从部署共享复制到部署介质，然后生成新的可启动映像。  

-   如[使用 Windows PowerShell 管理部署共享中的项](#ManageItemDeployShare)中所述，管理部署共享中的项（例如操作系统、操作系统包、应用程序和设备驱动程序）。  

-   如[自动执行部署共享填充](#AutomatePopulateDeployShare)中所述，自动执行部署共享中项的填充（例如操作系统、操作系统包、应用程序和设备驱动程序）。  

-   如[使用 Windows PowerShell 管理部署共享文件夹](#ManageDeployShareFolder)中所述，使用 Windows PowerShell 管理部署共享中的文件夹。  

###  <a name="LoadMDTSnapIn"></a> 加载 MDT Windows PowerShell 管理单元  
 Windows PowerShell 管理单元 Microsoft.BDD.SnapIn 中提供了 MDT cmdlet，必须在使用 MDT cmdlet 之前加载该单元。 可使用以下任意一种方法加载 MDT Windows PowerShell 管理单元：  

-   如[使用导入系统模块任务加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapInImport)中所述，使用 Window PowerShell 模块控制台加载 MDT Windows PowerShell 管理单元。  

-   如[使用 Add-PSSnapIn cmdlet 加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapInCmdlet)中所述，使用 Add-PSSnapIn cmdlet 加载 MDT Windows PowerShell 管理单元。  

####  <a name="LoadMDTSnapInImport"></a> 使用导入系统模块任务加载 MDT Windows PowerShell 管理单元  
 导入系统模块任务自动包括 %Windir%\System32\WindowsPowerShell\1.0\Modules 目录的模块中含有的所有 Windows PowerShell 模块和管理单元。 在 MDT 安装过程中，MDT 会在该文件夹中自动安装 MDT Windows PowerShell 管理单元 Microsoft.BDD.SnapIn。  

> [!NOTE]
>  计算机上未安装 Windows PowerShell 3.0 时，导入系统模块任务只有在 Windows 7 和 Windows Server 2008 R2 中可用。 从 Windows PowerShell 3.0 开始，第一次在模块中使用 cmdlet 时会自动导入模块。  

 可通过执行以下过程之一，通过导入系统模块任务来启动 Windows PowerShell 控制台：  

-   在任务栏中，右键单击“Windows PowerShell”图标，然后单击“导入系统模块”。  

-   单击“开始”，指向“管理工具”，然后单击“Windows PowerShell 模块”。  

 有关使用导入系统模块启动 Windows PowerShell 控制台的详细信息，请参阅[使用导入系统模块启动 Windows PowerShell](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx)。  

####  <a name="LoadMDTSnapInCmdlet"></a> 使用 Add-PSSnapIn cmdlet 加载 MDT Windows PowerShell 管理单元  
 可使用 [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx) cmdlet 从任何 Windows PowerShell 环境中加载 MDT Windows PowerShell 管理单元 Microsoft.BDD.PSSnapIn，如以下示例所示：  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> 使用 Windows PowerShell 创建部署共享  
 可使用 MDT Windows PowerShell cmdlet 创建部署共享。 使用标准 Windows PowerShell cmdlet 并调用 Windows Management Instrumentation (WMI) 类命令，来创建和共享部署共享的根文件夹。 使用 MDTProvider Windows PowerShell 提供程序和 [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet 填充部署共享。 使用 Add-MDTPersistentDrive cmdlet 保留 MDTProvider Windows PowerShell 驱动器。  

 **使用 MDT Windows PowerShell cmdlet 准备部署共享**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  如[使用 New-Item Cmdlet](http://technet.microsoft.com/library/ee176914.aspx) 中所述，使用 New-Item cmdlet 创建将成为新部署共享根文件夹的文件夹，如以下示例所示：  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     此 cmdlet 显示成功创建文件夹。  

3.  使用 WMI win32_share 类共享上一步中创建的文件夹，如以下示例所示：  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     对 win32_share 类的调用返回调用的结果。 如果 ReturnValue 的值为零 (0)，则调用成功。  

4.  使用 [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) cmdlet 将新共享文件夹指定为部署共享，如以下示例所示：  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     此 cmdlet 自动开始创建部署共享并将模板信息复制到新部署共享中。 完成复制过程后，此 cmdlet 将显示新部署共享的信息。  

    > [!NOTE]
    >  Name 参数 (DS002) 中提供的值必须是唯一的，并且不能与现有的部署共享 Windows PowerShell 驱动器相同。  

5.  使用 dir 命令验证是否创建了适当的部署共享文件夹，如以下示例所示：  

    ```  
    dir ds002:  
    ```  

     显示部署共享根文件夹中的默认文件夹列表。  

6.  使用 Add-MDTPersistentDrive cmdlet 将新部署共享添加到保留的 MDT 部署共享列表中，如以下示例所示：  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     在此示例中，使用 $NewDS 变量可将新部署共享的 Windows PowerShell 驱动器对象传递给此 cmdlet。  

     或者，可结合使用 [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) 和 Add-MDTPersistentDrive cmdlet，如以下示例所示：  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     在前面的示例中，Windows PowerShell 管道提供了 Name 和 InputObject 参数。  

###  <a name="ViewDeployShareProp"></a> 使用 Windows PowerShell 查看部署共享属性  
 可使用 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet 和 MDTProvider Windows PowerShell 提供程序查看 MDT 部署共享的属性。 也可以在 Deployment Workbench 中查看这些相同的属性。  

 **使用 MDT Windows PowerShell cmdlet 查看部署共享属性**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原 MDT 部署共享 Windows PowerShell 驱动器，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 验证是否正确还原共享 Windows PowerShell 驱动器的 MDT 部署，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器列表。  

4.  使用 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet 查看部署共享的属性，如以下示例所示：  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。 此 cmdlet 返回部署共享的属性。  

###  <a name="ViewListDeployShare"></a> 使用 Windows PowerShell 查看部署共享的列表  
 可使用[Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 和 MDTProvider Windows PowerShell 提供程序查看 MDT 部署共享的列表。 也可在 Deployment Workbench 中查看相同的部署共享列表。  

 **使用 MDT Windows PowerShell cmdlet 查看部署共享的列表**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原 MDT 部署共享 Windows PowerShell 驱动器，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 来查看共享着 Windows PowerShell 驱动器的 MDT 部署的列表，每个部署共享有一个驱动器，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表，每个部署共享有一个驱动器。  

###  <a name="UpdateDeployShare"></a> 使用 Windows PowerShell 更新部署共享  
 可使用 Update-MDTDeploymentShare cmdlet 和 MDTProvider Windows PowerShell 提供程序来更新部署共享。 更新部署共享会创建启动 LTI 部署所需的 Windows PE 启动映像（WIM 和国际标准化组织 [ISO] 文件）。 如“在 Deployment Workbench 中更新部署共享”中所述，可使用 Deployment Workbench 执行相同的过程。  

 **使用 Windows PowerShell 更新部署共享**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 验证是否正确还原共享 Windows PowerShell 驱动器的 MDT 部署，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表。  

4.  使用 Update-MDTDeploymentShare cmdlet 更新部署共享，如以下示例所示：  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

    > [!NOTE]
    >  更新部署共享可能需要很长时间。 此 cmdlet 的进度显示在 Windows PowerShell 控制台的顶部。  

     如果更新成功，此 cmdlet 不返回输出。  

###  <a name="UpdateLinkedDeployShare"></a> 使用 Windows PowerShell 更新链接的部署共享  
 可使用 Update-MDTLinkedDS cmdlet 和 MDTProvider Windows PowerShell 提供程序来更新（复制）链接的部署共享。 更新链接的部署共享可将内容从原始部署共享复制到链接的部署共享。 如“在 Deployment Workbench 中复制链接的部署共享”中所述，可使用 Deployment Workbench 执行相同的过程。  

 **使用 Windows PowerShell 更新链接的部署共享**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 验证是否正确还原共享 Windows PowerShell 驱动器的 MDT 部署，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表。  

4.  使用 Update-MDTDeploymentShare cmdlet 更新部署共享，如以下示例所示：  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

    > [!NOTE]
    >  更新链接的部署共享可能需要很长时间。 此 cmdlet 的进度显示在 Windows PowerShell 控制台的顶部。  

     如果更新成功，此 cmdlet 不返回输出。  

###  <a name="UpdateDeployMedia"></a> 使用 Windows PowerShell 更新部署介质  
 可使用 Update-MDTMedia cmdlet 和 MDTProvider Windows PowerShell 提供程序来更新（生成）部署介质。 更新部署介质可将内容从原始部署共享复制到链接的部署共享，然后生成 .iso 和 .wim 文件。 如“在 Deployment Workbench 中生成介质映像”中所述，可使用 Deployment Workbench 执行相同的过程。  

 Update-MDTMedia cmdlet 完成时，会创建以下文件：  

-   media_folder 文件夹中的 .iso 文件（其中 media_folder 是为介质指定的文件夹名）  

     生成 .iso 文件是通过以下操作配置的选项：  

    -   在“介质属性”对话框的“常规”选项卡上选中“生成 Lite Touch 可启动的 ISO 映像”复选框（清除此复选框以减少生成介质所需的时间，除非需要创建可启动 DVD 或从 .iso 文件启动虚拟机 [VM]。）  

    -   使用 [Set-ItemProperty](http://technet.microsoft.com/library/hh849844) cmdlet 设置相同的属性  

-   media_folder\Content\Deploy\Boot folder 中的 WIM 文件（其中 media_folder 是为介质指定的文件夹名）  

 **使用 Windows PowerShell 更新链接的部署共享**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原 MDT 部署共享 Windows PowerShell 驱动器，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 验证是否正确还原共享 Windows PowerShell 驱动器的 MDT 部署，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表。  

4.  使用 Update-MDTDeploymentShare cmdlet 更新部署共享，如以下示例所示：  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

    > [!NOTE]
    >  更新链接的部署共享可能需要很长时间。 此 cmdlet 的进度显示在 Windows PowerShell 控制台的顶部。  

     如果更新成功，此 cmdlet 不返回输出。  

###  <a name="ManageItemDeployShare"></a> 使用 Windows PowerShell 管理部署共享中的项  
 部署共享包含用于执行部署的项，例如操作系统、应用程序、设备驱动程序、操作系统包和任务序列。 可使用 Windows PowerShell 的 cmdlet 和 MDT 提供的 cmdlet 管理这些项。  

 有关使用 Windows PowerShell cmdlet 来直接操作项的详细信息，请参阅[直接操作项](http://technet.microsoft.com/library/dd315266.aspx)。 也可使用 Windows PowerShell 管理部署共享的文件夹结构。 有关详细信息，请参阅[使用 Windows PowerShell 管理部署共享文件夹](#ManageDeployShareFolder)。  

####  <a name="ImportItemDeployShare"></a> 将项导入部署共享  
 可使用 MDT cmdlet 导入每种类型的项，如操作系统、应用程序或设备驱动程序。 对于每种类型的项，都有一个特定的 MDT cmdlet。 如果要使用 Windows PowerShell 将多个项导入部署共享，请参阅[自动执行部署共享填充](#AutomatePopulateDeployShare)。  

 下表列出了用于将项导入部署共享的 MDT Windows PowerShell cmdlet，并提供了每个 cmdlet 的简要描述。 与每个 cmdlet 对应的部分提供了如何使用每个 cmdlet 的示例。  

 |**Cmdlet** | **描述** |  
 |-|-|  
 |**Import-MDTApplication** |将应用程序导入部署共享|  
 |**Import-MDTDriver** |将一个或多个设备驱动程序导入部署共享|  
 |**Import-MDTOperatingSystem** |将一个或多个操作系统导入部署共享|  
 |**Import-MDTPackage** |将一个或多个操作系统包导入部署共享|  
 |**Import-MDTTaskSequence** |将任务序列导入部署共享|  

####  <a name="ViewPropertyDeployShare"></a> 查看部署共享中项的属性  
 部署共享中的每个项具有不同的属性集。 可使用 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet 查看部署共享中项的属性。 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet 使用 MDTProvider 来显示特定项的属性，就像可在 Deployment Workbench 中查看属性一样。  

 如果想要使用 Windows PowerShell 查看部署共享中多个项的属性，请参阅[自动执行部署共享填充](#AutomatePopulateDeployShare)。  

 **使用 Windows PowerShell 查看部署共享中项的属性**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 验证是否正确还原了共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表。  

4.  使用 [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet 返回想要查看其属性的那种项的项列表，如以下示例所示：  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     在前面的示例中，显示了部署共享中所有操作系统的列表。 将输出输送到 Format-List cmdlet，以便查看操作系统的长名称。 有关如何使用 Format-List cmdlet 的详细信息，请参阅[使用 Format-List Cmdlet](http://technet.microsoft.com/library/ee176830.aspx)。 可使用相同的过程返回其他类型的项的列表，如设备驱动程序或应用程序。  

    > [!TIP]
    >  也可使用 dir 命令查看操作系统列表，而不是使用 [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet。  

5.  使用 [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) cmdlet 查看上一步中列出的某个项的属性，如以下示例所示：  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     在此示例中，Path 参数的值是项的完全限定的 Windows PowerShell 路径，包括上一步中返回的文件名。 可使用相同的过程查看其他类型的项的属性，如设备驱动程序或应用程序。  

####  <a name="RemoveItemDeployShare"></a> 从部署共享中移除项  
 可使用 [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet 从部署共享中移除项。 [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet 使用 MDTProvider 移除特定项，就像可在 Deployment Workbench 中移除项一样。 如果想要使用 Windows PowerShell 移除部署共享中的多个项，请参阅[自动执行部署共享填充](#AutomatePopulateDeployShare)。  

> [!NOTE]
>  移除任务序列使用的项会导致任务序列失败。 在移除项之前确保部署共享中的其他项未引用该项。 一旦移除项，将无法恢复。  

 **使用 Windows PowerShell 从部署共享中移除项**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示。  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 验证是否正确还原了共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表。  

4.  使用 [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet 返回想要查看其属性的那种项的项列表，如以下示例所示：  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     在前面的示例中，显示了部署共享中所有操作系统的列表。 将输出输送到 Format-List cmdlet，以便查看操作系统的长名称。 有关如何使用 Format-List cmdlet 的详细信息，请参阅[使用 Format-List Cmdlet](http://technet.microsoft.com/library/ee176830.aspx)。 可使用相同的过程返回其他类型的项的列表，如设备驱动程序或应用程序。  

    > [!TIP]
    >  也可使用 dir 命令查看操作系统列表，而不是使用 [Get-Item](http://technet.microsoft.com/library/hh849788) cmdlet。  

5.  使用 [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet 移除上一步中列出的某个项，如以下示例所示：  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     在此示例中，Path 参数的值是项的完全限定的 Windows PowerShell 路径，包括上一步中返回的文件名。  

     可使用相同的过程移除其他类型的项，如设备驱动程序或应用程序。  

    > [!NOTE]
    >  移除任务序列使用的项会导致任务序列失败。 在移除项之前确保部署共享中的其他项未引用该项。  

###  <a name="AutomatePopulateDeployShare"></a> 自动执行部署共享填充  
 可通过 MDT Windows PowerShell cmdlet 管理单个项。 但是，通过 Windows PowerShell 中的某些脚本功能，可使用 cmdlet 来自动执行部署共享填充。  

 例如，组织可能需要为不同的业务部门部署多个部署共享，或者组织可能为其他组织提供操作系统部署服务。 在这两个示例中，组织都需要能够创建并填充配置得一致的部署共享。  

 管理多个项的一种方法是使用逗号分隔值 (CSV) 文件，其中包含要通过 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet 在部署共享中管理的所有项的列表。  

 以下是使用 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx)、[ForEach-Object](http://technet.microsoft.com/library/hh849731) 和 Import-MDTApplication cmdlet 基于 .csv 文件中的信息导入应用程序列表的 Windows PowerShell 脚本的摘录：  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 在此示例中，C:\MDT\Import-MDT-Apps.csv 文件包含导入应用程序所需的每个变量的字段。 有关如何创建用于 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet 的 .csv 文件的详细信息，请参阅[使用 Import-Csv Cmdlet](http://technet.microsoft.com/library/ee176874.aspx)。  

 通过执行以下步骤，可使用相同的方法来导入部署共享中的操作系统、设备驱动程序和其他项：  

1.  为想要填充的每种部署共享项创建一个 .csv 文件。  

2.  有关如何创建用于 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet 的 .csv 文件的详细信息，请参阅[使用 Import-Csv Cmdlet](http://technet.microsoft.com/library/ee176874.aspx)。  

3.  创建将用于自动执行部署共享填充的 Windows PowerShell 脚本文件。  

     有关如何创建 Windows PowerShell 脚本的详细信息，请参阅[通过 Windows PowerShell 编写脚本](http://technet.microsoft.com/scriptcenter/powershell.aspx)。  

4.  在导入部署共享项之前，请创建部署共享中所需的任何先决条件文件夹结构。  

     有关详细信息，请参阅[使用 Windows PowerShell 管理部署共享文件夹](#ManageDeployShareFolder)。  

5.  为步骤 1 中创建的某个 .csv 文件添加 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet 行。  

     有关 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet 的详细信息，请参阅[使用 Import-Csv Cmdlet](http://technet.microsoft.com/library/ee176874.aspx)。  

6.  创建 [ForEach-Object](http://technet.microsoft.com/library/hh849731) cmdlet 循环，可用于处理上一步的 [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) cmdlet 中引用的 .csv 文件的每个项。  

     有关 [ForEach-Object](http://technet.microsoft.com/library/hh849731) cmdlet 的详细信息，请参阅[使用 ForEach-Object Cmdlet](http://technet.microsoft.com/library/ee176828)。  

7.  添加相应的 MDT cmdlet，用于导入上一步中创建的 [ForEach-Object](http://technet.microsoft.com/library/hh849731) cmdlet 循环内的部署共享项。  

     有关用于将项导入部署共享的 MDT cmdlet 的详细信息，请参阅[将项导入部署共享](#ImportItemDeployShare)。  

###  <a name="ManageDeployShareFolder"></a> 使用 Windows PowerShell 管理部署共享文件夹  
 可使用命令行工具（如 mkdir 命令）或使用 Windows PowerShell cmdlet（如 [New-Item](http://technet.microsoft.com/library/hh849795) cmdlet 和 MDTProvider Windows PowerShell 提供程序）来管理部署共享中的文件夹。 也可在 Deployment Workbench 中查看和管理相同的部署共享的文件夹结构。 有关使用 Windows PowerShell cmdlet 来直接操作项的详细信息，请参阅[直接操作项](http://technet.microsoft.com/library/dd315266.aspx)。  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>使用 Windows PowerShell 在部署共享中创建文件夹  
 **使用 Windows PowerShell 在部署共享中创建文件夹**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 查看共享着 Windows PowerShell 驱动器的 MDT 部署的列表，每个部署共享有一个驱动器，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表，每个部署共享有一个驱动器  

4.  使用 mkdir 命令，在部署共享的“Operating Systems”文件夹中创建名为“Windows_8”的文件夹，如以下示例所示：  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

5.  输入以下命令验证是否正确创建文件夹：  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     显示“Operating Systems”文件夹中的 Windows_8 文件夹和任何其他现有文件夹。  

6.  如[使用 New-Item Cmdlet](http://technet.microsoft.com/library/ee176914.aspx) 中所述，使用 [New-Item](http://technet.microsoft.com/library/hh849795) cmdlet 在部署共享的“Operating Systems”文件夹中创建名为“Windows_7”的文件夹，如以下示例所示：  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     此 cmdlet 显示成功创建文件夹。  

7.  输入以下命令验证是否正确创建文件夹：  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     显示“Operating Systems”文件夹中的 Windows_7 文件夹和任何其他现有文件夹。  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>使用 Windows PowerShell 在部署共享中删除文件夹  
 **使用 Windows PowerShell 在部署共享中删除文件夹**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 查看共享着 Windows PowerShell 驱动器的 MDT 部署的列表，每个部署共享有一个驱动器，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表，每个部署共享有一个驱动器。  

4.  使用 mkdir 命令，在部署共享的“Operating Systems”文件夹中删除（移除）名为“Windows_8”的文件夹，如以下示例所示：  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

5.  输入以下命令验证是否正确移除文件夹：  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Windows_8 文件夹不再显示于“Operating Systems”文件夹的文件夹列表中  

6.  使用 [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet，在部署共享的“Operating Systems”文件夹中删除（移除）名为“Windows_7”的文件夹，如以下示例所示：  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     此 cmdlet 显示成功移除文件夹。  

7.  输入以下命令验证是否正确创建文件夹：  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Windows_7 文件夹不再显示于“Operating Systems”文件夹的文件夹列表中。  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>使用 Windows PowerShell 在部署共享中重命名文件夹  
 **使用 Windows PowerShell 在部署共享中重命名文件夹**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原 MDT 部署共享 Windows PowerShell 驱动器，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 查看共享着 Windows PowerShell 驱动器的 MDT 部署的列表，每个部署共享有一个驱动器，如下所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表，每个部署共享有一个驱动器。  

4.  使用 ren 命令，在部署共享的“Operating Systems”文件夹中将名为“Windows_8”的文件夹重命名为“Win_8”，如以下示例所示：  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

5.  输入以下命令验证是否正确移除文件夹：  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     将 Windows_8 文件夹重命名为“Win_8”。  

6.  使用 [Rename-Item](http://technet.microsoft.com/library/hh849763) cmdlet ，在部署共享的“Operating Systems”文件夹中将名为“Windows_7”的文件夹重命名为“Win-7”，如以下示例所示：  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     此 cmdlet 显示成功重命名文件夹。  

7.  输入以下命令验证是否正确创建文件夹：  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     将 Windows_7 文件夹重命名为“Win_7”。  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>在部署共享中自动应用操作系统服务包  
 操作系统服务包是软件生命周期的常规部分。 需要使用这些服务包来更新部署共享中的现有操作系统，以帮助确保新部署的或刷新的计算机当前使用最新的安全建议和配置设置。  

 如果组织具有多个部署共享且每个部署包含多个操作系统，那么使用服务包手动更新每个部署共享中的操作系统会非常耗时。 在部署共享中自动应用操作系统服务包的方法包括：  

-   如[通过更新的源介质自动应用操作系统服务包](#AutomateAppFromUSM)中所述，将已包含服务包（例如，具有 SP1 介质的 Windows 7）的已更新源内容复制到现有操作系统所在的部署共享中的文件夹  

-   如[使用引用计算机和 Windows PowerShell 自动应用操作系统服务包](#AutomateAppUsingRef)中所述，将服务包应用于引用计算机，然后从引用计算机捕获更新的映像  

###  <a name="AutomateAppFromUSM"></a> 通过更新的源介质自动应用操作系统服务包  
 具有包含服务包的源介质（如具有包含已集成 SP1 的 Windows 7 的 DVD）时，可使用 Windows PowerShell 自动执行更新操作系统服务包的过程。  

 对于此方法，在部署共享中使用 Windows PowerShell 将具有服务包的操作系统源介质复制到不具有服务包的现有操作系统文件上。  

 **使用 Windows PowerShell 从更新源介质自动应用操作系统服务包**  

1.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

2.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

3.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 查看共享着 Windows PowerShell 驱动器的 MDT 部署的列表，每个部署共享有一个驱动器，如以下示例所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表，每个部署共享有一个驱动器。  

4.  使用 [Get-ChildItem](http://technet.microsoft.com/library/hh849800) 和 [Remove-Item](http://technet.microsoft.com/library/hh849765) cmdlet 从部署共享中移除现有操作系统的文件夹，如以下示例所示：  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     在此示例中，DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

5.  使用 [Copy-Item](http://technet.microsoft.com/library/hh849793) cmdlet 复制已集成服务包的操作系统源文件的内容，如以下示例所示：  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     在此示例中，操作系统源文件位于驱动器 E 上，并且 DS002: 是步骤 3 中返回的 Windows PowerShell 驱动器的名称。  

6.  使用 Update-MDTMedia cmdlet 基于部署共享更新任何 MDT 部署介质。  

 有关如何使用 Update-MDTMedia cmdlet 基于部署共享更新 MDT 部署介质的详细信息，请参阅[使用 Windows PowerShell 更新部署介质](#UpdateDeployMedia)。  

###  <a name="AutomateAppUsingRef"></a> 使用引用计算机和 Windows PowerShell 自动应用操作系统服务包  
 如果只有尚未与操作系统集成的服务包（如尚未与 Windows 7 映像集成的 Windows 7 SP1），可使用 Windows PowerShell 自动执行更新操作系统服务包的过程。  

 对于此方法，请将不具有服务包的操作系统部署到引用计算机。 然后，将服务包应用于引用计算机。 接下来，捕获引用计算机的操作系统映像。 最后，使用 Windows PowerShell 将捕获的 .wim 文件复制到部署共享的操作系统的 Install.wim 文件中。  

 **使用 Windows PowerShell 从更新源介质自动应用操作系统服务包**  

1.  将目标操作系统部署到引用计算机。  

     有关如何部署引用计算机的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的以下资源：  

    -   “准备对引用计算机进行 LTI 部署”  

    -   “在 LTI 中部署和捕获引用计算机的映像”  

2.  将所需的服务包安装到引用计算机。  

     有关如何安装服务包的详细信息，请参阅服务包随附的文档。  

3.  基于 Sysprep 和 Capture 任务序列模板创建和部署任务序列，从而捕获引用计算机的映像。  

     有关基于 Sysprep 和 Capture 任务序列模板创建任务序列的详细信息，请参阅“在 Deployment Workbench 中创建新的任务序列”。  

4.  如[加载 MDT Windows PowerShell 管理单元](#LoadMDTSnapIn)中所述，加载 MDT Windows PowerShell 管理单元。  

5.  确保使用 Restore-MDTPersistentDrive cmdlet 来还原共享着 Windows PowerShell 驱动器的 MDT 部署，如以下示例所示：  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  如果共享着 Windows PowerShell 驱动器的 MDT 部署已还原，将收到一条警告消息，表示该 cmdlet 无法还原驱动器。  

6.  使用 [Get-PSDrive](http://technet.microsoft.com/library/hh849796) cmdlet 查看共享着 Windows PowerShell 驱动器的 MDT 部署的列表，每个部署共享有一个驱动器，如以下示例所示：  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     列出了使用 MDTProvider 提供的 Windows PowerShell 驱动器的列表，每个部署共享有一个驱动器。  

7.  使用 [Copy-Item](http://technet.microsoft.com/library/hh849793) cmdlet，将步骤 3 中捕获的 .wim 文件复制到部署共享的操作系统的 Install.wim 文件中，如以下示例所示：  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     在此示例中，共享 DS002: 的“Captures”文件夹中捕获的操作系统映像文件 (Win7SP1.wim) 是步骤 6 中返回的 Windows PowerShell 驱动器的名称，现有 Windows 7 操作系统存储在名为“Windows 7”的文件夹中。  

8.  使用 Update-MDTMedia cmdlet 基于部署共享更新任何 MDT 部署介质。  

     有关如何使用 Update-MDTMedia cmdlet 基于部署共享更新 MDT 部署介质的详细信息，请参阅[使用 Windows PowerShell 更新部署介质](#UpdateDeployMedia)。  

## <a name="customizing-deployment-based-on-chassis-type"></a>根据底盘类型自定义部署  
 可根据计算机的底盘类型自定义部署。 脚本创建可在 CustomSettings.ini 文件中处理的局部变量。 局部变量 `IsLaptop`、`IsDesktop` 和 `IsServer` 分别表示计算机是便携式计算机、台式计算机还是服务器。  

> [!NOTE]
>  在 Deployment Workbench 的早期版本中，`IsServer` 标志表示现有操作系统是服务器操作系统（如 Windows Server 2003 Enterprise Edition）。 此标志已重命名为 `IsServerOS`。  

 **在 CustomSettings.ini 文件中实现局部变量**  

1.  在 `[Settings]` 部分的 `Priority` 行上，添加自定义部分以根据底盘类型（以下示例中的 `ByChassisType`，其中 Chassis 代表计算机类型）自定义部署。  

2.  创建与步骤 1 中定义的自定义部分相对应的自定义部分（以下示例中的 `ByChassisType`，其中 Chassis 代表计算机的类型）。  

3.  为每个要检测的底盘类型定义一个子节（以下示例中的 `Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%`）。  

4.  为步骤 3 中定义的每个子节的每个 `True` 和 `False` 状态创建一个子节（如以下示例中的 `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]`）。  

5.  在每个 `True` 和 `False` 子节下，根据底盘类型添加适当的设置。  

 **列表 1.CustomSettings.ini 文件中根据底盘类型自定义部署的示例**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>根据应用程序的早期版本部署应用程序  
 通常情况下，在现有计算机上安装操作系统时，将安装以前安装在计算机上的相同应用程序。 使用 MDT 脚本（尤其是 ZTIGather.wsf）执行此操作来查询两个单独的信息源：  

-   **Configuration Manager 软件清单功能。** 针对上次 Configuration Manager 为计算机列出清单时所安装的每个应用程序包（在这种情况下，即为 Windows 8.1、Windows 8、Windows 7、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 的“程序和功能”中的清单），包含一条记录。  

-   **映射表。** 介绍需为每个记录安装的包和程序（因为“程序和功能”或者“添加或删除程序”记录未明确指定安装了应用程序的包，使得无法只根据清单自动选择包）。  

 **执行特定于计算机的动态应用程序安装**  

1.  使用 MDT DB 中的表格将特定包与目标操作系统中列出的应用程序相连。  

2.  使用数据填充表格，该数据将适当的包与“程序和功能”或者“添加或删除程序”中列出的应用程序相关联。

     **用于填充表的 SQL 查询**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     插入的行将具有条目 `Office12.0` 的计算机与 Microsoft Office 2010 Professional Plus 包相连。  

     这意味着 Microsoft Office 2010 Professional Plus 将安装在当前运行 2007 Microsoft Office 系统 (Office 12.0) 的任何计算机上。 为其他包添加类似条目。 忽略任何没有条目的项（将不安装任何包）。  

3.  创建存储过程以简化将新表中的信息与清单数据关联。  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     以上示例中的存储过程假定 Configuration Manager 中央主站点数据库驻留在 SQL Server 作为 MDT DB 运行于其中的计算机上。 如果中央主站点数据库驻留在其他计算机上，则需要对存储过程进行适当的修改。 另外，必须更新数据库的名称 (`CM_DB`)。 此外，请考虑授予其他帐户对 Configuration Manager 数据库中 v_GS_ADD_REMOVE_PROGRAMS 视图的读取访问权限。  

4.  通过指定指向数据库信息的部分（“优先级”列表中的 `[DynamicPackages]`）的名称来配置 CustomSettings.ini 文件以查询此数据库表。  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  创建 `[DynamicPackages]` 部分以指定数据库部分的名称。  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  创建数据库部分以指定数据库信息并查询详细信息。  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     在以上示例中，将查询计算机上名为 MDTDB 的 MDT DB，该计算机运行名为 SERVER1 的 SQL Server 实例。 数据库包含一个名为 `RetrievePackages` 的存储过程（在步骤 3 中创建）。  

 ZTIGather.wsf 运行时，会自动生成结构化查询语言 (SQL) `SELECT` 语句，并将 MakeModelQuery 自定义键的值作为参数传递给查询：  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 MACAddress 自定义键的实际值将替换相应的“?”。  此查询返回一个记录集，其中包含在步骤 2 中输入的行。  

 不能将数量不定的参数传递给存储过程。 因此，当一台计算机有多个 MAC 地址时，并非所有的 MAC 地址都可传递给存储过程。 或者，将存储过程替换为允许通过含 `IN` 子句的 `SELECT` 语句来查询该视图的视图，以传递所有 MAC 地址值。  

 根据此方案，如果当前计算机将值 `Office12.0` 插入表中（步骤 2），则返回一个行 (`XXX0000F:Install Office 2010 Professional Plus`)。 这表示包 XXX0000F:Install Office 2001 Professional Plus 将在状态还原阶段由 ZTI 进程安装。  

## <a name="fully-automated-lti-deployment-scenario"></a>全自动 LTI 部署方案  
 LTI 的主要目的是尽可能自动执行部署过程。 虽然 ZTI 使用 MDT 脚本和 Windows 部署服务提供完整的部署自动化，但 LTI 旨在以更少的基础结构要求运行。  

 可自动执行 LTI 部署过程中使用的“Windows 部署向导”，减少（或消除）显示的向导页。 可在 CustomSettings.ini 中指定 SkipWizard 属性来跳过整个“Windows 部署向导”。 若要跳过单个向导页，请使用以下属性：  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

有关这些单个属性的详细信息，请参阅 MDT 文档《Toolkit 参考》中的相应属性。  

对于跳过的每个向导页，请提供相应属性的值，此属性通常通过 CustomSettings.ini 和 BootStrap.ini 文件中的向导页收集。 有关必须在这些文件中配置的属性的详细信息，请参阅 MDT 文档《Toolkit 参考》中的“为跳过的部署向导页提供属性”部分。  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>用于刷新计算机方案的全自动 LTI 部署  
 以下展示了用于刷新计算机方案的 CustomSettings.ini 文件，可跳过所有“Windows 部署向导”页。 在此示例中，跳过向导页时提供的属性立即位于跳过该向导页的属性下方。  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>用于新计算机方案的全自动 LTI 部署  
 以下是用于新计算机方案的 CustomSettings.ini 文件的示例，可跳过所有“Windows 部署向导”页。 在此示例中，跳过向导页时提供的属性立即位于跳过该向导页的属性下方。  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>在 MDT 中调用 Web 服务  
 在 MDT 的早期版本中，规则处理通过 CustomSettings.ini 和数据库受到支持，基于此可从本地计算机（通常使用 WMI）检索值，以便决定部署期间每台计算机上需要完成的工作。 另外，可进行 SQL 查询和存储过程调用来从外部数据库检索其他信息。 但是，这种方法存在质疑 - 尤其是在建立安全的 SQL 连接时。  

 为了帮助解决这个问题，MDT 提供根据 CustomSettings.ini 中定义的简单规则进行 Web 服务调用的功能。 这些 Web 服务请求不需要任何特殊的安全性上下文，并且可以使用所需的任何 TCP/IP 端口来简化防火墙配置。  

 以下显示如何配置 CustomSettings.ini 来调用特定的 Web 服务。 在此情况下，Web 服务是从 Internet 搜索中随机选择的。 它将邮政编码作为输入，并（以字母形式）返回指定邮政编码的市/县、省/市/自治区、区域代码和时区。  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 执行此代码会产生类似于以下内容的输出：
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 运行 Web 服务时需要注意一些小问题：  

-   不要对代理服务器执行任何特殊操作。 如果存在匿名代理，请使用它，但验证代理时可能会出现问题。 在大多数情况下，将不会调用 Web 服务。  

-   CustomSettings.ini 或 ZTIGather.xml 搜索作为 Web 服务调用的结果而返回的 XML 标记中定义的属性（就像使用数据库查询或其他规则一样）。 但是，XML 搜索区分大小写。 幸运的是，此处描述的 Web 服务返回全部大写的属性名称，这是 ZTIGather.xml 所需要的。 可重映射小写或混合大小写的条目来避开此问题。  

-   建议向 Web 服务发送 `POST` 请求，因此 Web 服务调用必须能够支持 `POST`。  

## <a name="connecting-to-network-resources"></a>连接网络资源  
 在 LTI 和 ZTI 部署过程中，可能要求访问服务器上的网络资源，此服务器与托管部署共享的服务器不同。 必须在其他服务器上进行身份验证，以便访问那里的共享文件夹或服务。 例如，可从服务器上的共享文件夹安装应用程序，此服务器不同于托管 MDT 脚本所使用的部署共享的服务器。  

> [!NOTE]
>  若要查询托管部署共享服务器以外的服务器上托管的 SQL Server 数据库，请参阅 MDT 文档《Toolkit 参考》中的 Database、DBID、DBPwd、Instance、NetLib、Order、Parameters、ParameterCondition、SQLServer、SQLShare 以及 Table 属性。  

 使用 ZTIConnect.wsf 脚本，可连接到其他服务器并访问上面的资源。 ZTIConnect.wsf 脚本的语法如下（其中 unc_path 是连接到服务器的通用命名约定 [UNC] 路径）：  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 在大多数情况下，可运行 ZTIConnect.wsf 脚本作为任务顺序器任务。 先于需要访问服务器（此服务器不同于托管部署共享的服务器）的任务运行 ZTIConnect.wsf 脚本。  

 **将 ZTIConnect.wsf 脚本作为任务添加到生成的任务序列**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在详细信息窗格中，单击“task_sequence”（其中 task_sequence 是要修改的任务序列）。  

4.  在“操作”窗格中，单击“属性”。  

5.  单击“任务序列”选项卡，浏览到“group”（group 是要在其中运行 ZTIConnec.wsf 脚本的组），然后单击“添加”。 单击“常规”，然后单击“运行命令行”。  

    > [!NOTE]
    >  在添加任何需要访问目标服务器资源的任务之前添加任务。  

6.  使用以下信息，完成新任务的“属性”选项卡设置：

    |**在此框中** |**执行此操作** |  
    |-|-|  
    |**Name** |键入“连接到服务器”（其中服务器是要连接的服务器的名称）。|  
    |**描述** |输入解释为什么需要建立连接的文本。|  
    |**命令** |键入“Cscript.exe "%SCRIPTROOT%\ZTIConnect.wsf" /uncpath:unc_path”（其中 unc_path 是服务器上共享文件夹的 UNC 路径）。|  

7.  使用以下信息，完成新任务的“选项”选项卡设置。 除非另行指定，请接受默认值，然后单击“确定”。  

    |**在此框中** |**执行此操作** |  
    |-|-|  
    |**成功代码** |键入“0 3010”。 （ZTIConnect.wsf 脚本在完成成功时返回这些代码。）|  
    |**条件列表框** |添加可能必需的任何条件。 （大多数情况下，此任务不需要条件。）|  

 添加将运行 ZTIConnect.wsf 脚本的任务后，后续任务可以访问 ZTIConnect.wsf 脚本的 /uncpath 选项中指定的服务器上的网络资源。  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>使用相同的硬件设备但不同的品牌和型号将正确的设备驱动程序部署到计算机  
 驱动程序集中几乎没有差异的情况下，可存在型号和名称的变化。 由于这些型号和名称的变化，生成给定型号的多个数据库条目时可能花费不必要的时间。 以下过程显示如何使用返回型号子字符串的 user exit 函数调用来定义新属性。  

 **创建型号别名**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  在“属性”对话框中，单击“规则”选项卡。  

5.  在 MDT DB 的“品牌和型号”部分中为硬件类型创建别名。 在型号名称的左括号“(”处截断模型类型。 例如，HP DL360 (G112) 变为 HP DL360。  

6.  将自定义变量 ModelAlias 添加到每个部分。  

7.  创建新 `[SetModel]` 部分。  

8.  将 `[SetModel]` 部分添加到 `[Settings]` 部分中的“优先级”设置。  

9. 将行添加到 `ModelAlias` 部分以引用将在“(”处截断型号名称的用户出口脚本。  

10. 创建 ModelAlias 等于 Model 的 MMApplications 数据库查找。  

11. 创建一个用户出口脚本并将其放置在与 CustomSettings.ini 文件相同的目录中以截断型号名称。  

    以下分别显示了 CustomSettings.ini 和用户出口脚本。  

     **CustomSettings.ini**：  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **用户出口脚本**：  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>配置条件任务序列步骤  
 在某些情况下，请考虑根据定义的条件有条件地运行任务序列步骤。 可以添加这些条件的任意组合以确定任务序列步骤是否应该运行。 例如，使用任务序列变量的值和注册表设置的值来确定任务序列步骤是否应该运行。  

 使用 MDT，根据以下条件有条件地运行任务序列：  

-   一个或多个 IF 语句  

-   任务序列变量  

-   目标操作系统的版本  

-   WMI 查询的布尔结果  

-   注册表设置  

-   目标计算机上安装的软件  

-   文件夹的属性  

-   文件的属性  

### <a name="configuring-a-conditional-task-sequence-step"></a>配置条件任务序列步骤  
 在 Deployment Workbench 的任务序列步骤“选项”选项卡中配置条件任务序列步骤。 可将一个或多个条件添加到任务序列步骤，创建运行或不运行该步骤的适当条件。  

> [!NOTE]
>  每个条件任务序列步骤至少需要一个 IF 语句。  

 **查看任务序列步骤的“选项”选项卡**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在详细信息窗格中，单击“task_sequence”（其中 task_sequence 是要配置的任务序列的名称）。  

4.  在“操作”窗格中，单击“属性”。  

5.  在“task_sequence 属性”对话框中的“任务序列”选项卡上，单击“step”（其中 step 是要配置的任务序列步骤的名称），然后单击“选项”选项卡。  

 在任务序列步骤的“选项”选项卡上，执行以下操作：  

-   **添加。** 单击此按钮，将条件添加到任务序列步骤。  

-   **移除。** 单击此按钮，移除任务序列步骤中的现有条件。  

-   **编辑。** 单击此按钮，修改任务序列步骤中的现有条件。  

### <a name="if-statements-in-conditions"></a>条件中的 IF 语句  
 所有任务序列条件包含一个或多个 IF 语句。 IF 语句是创建条件任务序列步骤的基础。 任务序列步骤条件可只包含一个 IF 语句，但多个 IF 语句可嵌套在顶级 IF 语句之下，以创建更复杂的条件。  

 IF 语句可基于下表中列出的条件，这些条件是在“IF 语句属性”对话框中配置的。  

 |**条件** |**选择此选项以运行任务序列 if** |  
 |-|-|  
 |**所有条件** |此 IF 语句下的所有条件必须为 true。|  
 |**任意条件** |此 IF 语句下的任意条件为 true。|  
 |**无** |此 IF 语句下没有条件为 true。|  

 通过将其他标准添加到条件（例如，任务序列变量或注册表设置中的值），完成运行任务序列步骤的条件。  

 **将 IF 语句条件添加到任务序列步骤**  

1.  在“step 选项”选项卡上（其中 step 是要配置的任务序列步骤的名称），单击“添加”，然后单击“ If 语句”。  

2.  在“If 语句属性”对话框中，单击“condition”（其中 condition 是上表中列出的某个条件），然后单击“确定”。  

### <a name="task-sequence-variables-in-conditions"></a>条件中的任务序列变量  
 使用“任务序列变量”条件来评估由“设置任务序列变量”任务或任务序列中的任何任务所创建的任何任务序列变量。 例如，有一个网络包含属于域的一部分的 Windows XP 客户端计算机，还有一些计算机位于工作组中。 了解到当前域策略强制将所有用户设置保存在该网络上，可能只需要对不属于域的那部分计算机保存用户设置，即工作组中的计算机。 在此情况下，请将条件添加到以工作组中计算机为目标的“捕获用户文件和设置”任务。  

 **根据任务序列变量添加条件**  

1.  在“step 选项”选项卡上（其中 step 是要配置的任务序列步骤的名称），单击“添加条件”，然后单击“任务序列变量”。  

2.  在“任务序列变量”条件对话框的“变量”框中，键入“OSDJoinType”。  

    > [!NOTE]
    >  对于加入域的计算机，将此变量设置为 0，对于工作组中的计算机，将此变量设置为 1。  

3.  在“条件”框中，单击“相等”。  

4.  在“值”框中，键入 1，然后单击“确定”。  

### <a name="operating-system-version-in-conditions"></a>条件中的操作系统版本  
 使用“操作系统版本”条件来验证目标计算机或现在有客户端（捕获映像时）的现有操作系统版本。 例如，有一个网络包含多个将从 Windows Server 2003 升级到 Windows Server 2008 的服务器。 应复制网络设置并仅将其应用于运行 Windows Server 2003 的服务器。 所有其他服务器都将具有 Windows Server 2008 使用的默认网络设置。  

 **根据操作系统版本添加条件**  

1.  在任务序列编辑器中，单击“捕获网络设置”任务。  

2.  单击“添加条件”，然后单击“操作系统版本”。  

3.  在“体系结构”框中，单击相关服务器。 对于此示例，请单击“x86”。  

4.  在“操作系统”框中，单击要为其设置条件的操作系统和版本。 对于此示例，请单击“x86 Windows 2003”。  

5.  在“条件”框中，单击相关条件，然后单击“确定”。  

### <a name="file-properties-in-conditions"></a>条件中的文件属性  
 使用“文件属性”条件来验证给定文件的版本和/或时间戳，以确定是否运行一个任务或一组任务。 在此示例中，生产环境包含不断更新且用于添加到网络的每个新服务器的 Windows Server 2003 映像。 环境中的所有服务器计算机都运行自定义应用程序，该应用程序需要数字访问对象 (DAO) 应用程序编程接口 (API) 版本 3.60.6815。  

 所有现有的服务器都正常工作。 但是，每个使用映像添加到网络的新服务器都无法运行应用程序。 由于其他组来负责维护和更新映像，因此如果使用映像部署的现有 DAO 版本不正确，则决定是否更改部署任务序列以安装相关的 DAO 版本。  

 **将“文件属性”条件添加到 Configuration Manager 2007 R3 中的任务序列步骤**  

1.  在 Configuration Manager 2007 R3 中，创建包以安装 DAO 3.60.6815。 使用名为 InstallDAO 的程序调用此包 DAO。 若要了解有关创建包的详细信息，请参阅[如何创建包](http://technet.microsoft.com/library/bb693627.aspx)。  

2.  创建“安装软件”步骤来部署 DAO 包。  

3.  单击步骤 2 中创建的“安装软件”任务序列步骤，然后单击“选项”选项卡。  

4.  单击“添加条件”，然后单击“文件属性”。  

5.  在“路径”框中，键入“C:\Program Files\Microsoft Shared\DAO\dao360.dll”。  

6.  选中“检查版本”复选框，然后单击“不等于”条件。  

7.  在“版本”框中，键入“3.60.6815”。  

8.  在此情况下，清除“检查时间戳”复选框，然后单击“确定”。  

### <a name="folder-properties-in-conditions"></a>条件中的文件夹属性  
 使用“文件夹属性”条件来验证给定文件夹的时间戳，以确定是否运行一个任务或一组任务。 例如，假设内部开发的应用程序已更新为可与 Windows 8 一起使用。 但是，并非网络中的所有计算机都安装了最新版本的应用程序，并且必须先执行数据转换过程，然后才能升级应用程序。  

 如果在其中安装应用程序的文件夹的时间戳为 2007 年 12 月 31 日或更早，那么目标计算机正在运行不兼容的应用程序版本，你应在目标计算机上运行数据转换过程。 有条件地运行任务序列步骤，在有早期版本应用程序的计算机上运行数据转换过程。  

 **将“文件夹属性”条件添加到任务序列步骤**  

1.  在 Configuration Manager 控制台或 Deployment Workbench 的任务序列编辑器中，编辑“task_sequence”（其中 task sequence 是要编辑的任务序列）。  

2.  创建“命令行”任务，执行数据转换过程。  

3.  单击步骤 1 中创建的任务。  

4.  单击“添加条件”，然后单击“文件夹属性”。  

5.  在“路径”框中，键入包含该应用程序的文件夹路径。  

6.  选中“检查时间戳”复选框。  

7.  单击“小于或等于”条件。  

8.  在“日期”框中，单击“2007/12/31”。  

9. 在“时间”框中，单击“凌晨 12:00:00”，然后单击“确定”。  

### <a name="registry-settings-in-conditions"></a>条件中的注册表设置  
 使用“注册表设置”条件来验证注册表中是否存在项和值以及注册表值中存储的相应数据。 例如，假设当前在一小部分计算机上使用的应用程序无法在 Windows 8 上运行，并且 Windows 8 部署可用于升级当前运行 Windows XP 的计算机。 在最开始的任务序列中创建一个条件，检查不兼容应用程序的注册表项，并在找到时中断该计算机的部署进程。  

 **将“注册表设置”条件添加到任务序列步骤**  

1.  在 Configuration Manager 控制台或 Deployment Workbench 的任务序列编辑器中，编辑“task_sequence”（其中 task sequence 是部署 Windows 8 的任务序列）。  

2.  单击此序列中的第一个任务，然后单击“选项”选项卡。  

3.  单击“添加条件”，然后单击“注册表设置”。  

4.  在“根注册表项”列表中，单击“HKEY_LOCAL_MACHINE”。  

5.  在“注册表项”框中，键入“SOFTWARE\WOODGROVE”。  

6.  单击“不存在”条件。 在此情况下，该任务将运行，并且仅当注册表项不存在时序列才继续。  

7.  或者，如果在“值名称”框中键入值名称，此条件可检查值是否不存在。  

8.  如果使用“存在/不存在”以外的条件，请指定值以及值类型。  

9. 单击" **确定**"。  

### <a name="wmi-queries-in-conditions"></a>条件中的 WMI 查询  
 使用“WMI 查询”条件运行任何 WMI 查询。 如果查询返回至少一个记录，则条件评估结果为 True。 例如，假设部署团队需要升级给定型号的所有服务器的操作系统，例如戴尔 1950。 可使用 WMI 查询来检查每台计算机的型号，并仅在找到正确的型号时才继续进行部署。  

 **将“WMI 查询”条件添加到任务序列步骤**  

1.  在 Configuration Manager 控制台或 Deployment Workbench 的任务序列编辑器中，编辑“task_sequence”（其中 task sequence 是将升级服务器的任务序列）。  

2.  单击此序列中的第一个任务，然后单击“选项”选项卡。  

3.  单击“添加条件”，然后单击“查询 WMI”。  

4.  在“WMI 命名空间”框中，键入“root\cimv2”。  

5.  在“WQL 查询”框中，键入“Select \* From Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"”。 单击" **确定**"。  

### <a name="installed-software-in-conditions"></a>条件中的已安装软件  
 使用“已安装软件”条件来检查当前是否在目标计算机上安装了特定的软件。 只有使用 Microsoft Installer (MSI) 文件安装的软件才能使用此条件进行评估。 例如，假设要升级除运行 Microsoft SQL Server 2012 的服务器之外的所有服务器的操作系统。  

 **将“已安装软件”条件添加到任务序列步骤**  

1.  在 Configuration Manager 控制台或 Deployment Workbench 的任务序列编辑器中，编辑“task_sequence”（其中 task sequence 是将升级服务器的任务序列）。  

2.  单击此序列中的第一个任务，然后单击“选项”选项卡。  

3.  单击“添加条件”，然后单击“已安装软件”。  

4.  单击“浏览”，然后单击 SQL Server 2012 的 MSI 文件。  

5.  选中“匹配此特定产品”复选框，指定只有具有 SQL Server 2012 且不具有任何其他版本的计算机才是此查询应检测的目标计算机。  

6.  单击" **确定**"。  

### <a name="complex-conditions"></a>复杂条件  
 可以使用 IF 语句将多个条件组合，创建复杂条件。 例如，假设只针对运行 Windows Server 2003 或 Windows Server 2008 的 Contoso 1950 计算机运行特定步骤。 编写为程序化的 IF 语句时，应类似于以下内容：  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **添加复杂条件**  

1.  在 Configuration Manager 控制台或 Deployment Workbench 的任务序列编辑器中，编辑“task_sequence”（其中 task sequence 是将升级服务器的任务序列）。  

2.  单击要向其添加条件的任务序列步骤，然后单击“选项”选项卡。  

3.  单击“添加条件”和“If 语句”，然后单击“所有条件”。 单击" **确定**"。  

4.  单击条件语句，并单击“添加条件”，然后单击“WMI 查询”。  

5.  确保将 root\cimv2 指定为 WMI 名称空间，然后在“WQL 查询”框中键入“SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE "%Contoso%1950%"”。 单击" **确定**"。  

6.  单击 IF 语句，然后单击“添加条件”。 单击“If 语句”，然后单击“任何条件”。 单击" **确定**"。  

7.  单击第二个 IF 语句。 单击“添加条件”，然后单击“操作系统版本”。  

8.  在“体系结构”框中，单击服务器的体系结构。 对于此示例，请单击“x86”。  

9. 在“操作系统”框中，单击操作系统和版本。 对于此示例，请单击“x86 Windows 2003 原始版本”。 单击" **确定**"。  

10. 单击第二个 IF 语句。 单击“添加条件”，然后单击“操作系统版本”。  

11. 在“体系结构”框中，单击服务器的体系结构。 对于此示例，请单击“x86”。  

12. 在“操作系统”框中，单击操作系统和版本。 对于此示例，请单击“x86 Windows 2008 原始版本”。 单击" **确定**"。  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>创建高度可缩放的 LTI 部署基础结构  
 在此方案中，没有电子软件分发可供部署基础结构利用，因此使用 MDT 生成全自动 LTI 部署基础结构。 可缩放的 LTI 基础结构使用 SQL Server、Windows 部署服务和 Windows Server 2003 分布式文件系统复制 (DFS-R) 技术。  

 通过以下操作缩放 LTI 基础结构：  

-   如[确保存在适当的基础结构](#EnsureInfrastructure)中所述，确保存在适当的基础结构  

-   如[将内容添加到 MDT](#AddContent)中所述，将内容添加到 MDT  

-   如[准备 Windows 部署服务](#PrepareDeployment)中所述，准备 Windows 部署服务  

-   按[配置分布式文件系统复制](#ConfigureFileReplication)中所述，配置 DFS-R  

-   如[准备 SQL Server 复制](#PrepareSQLReplication)中所述，准备 SQL Server 复制  

-   如[配置 SQL Server 复制](#ConfigureSQLReplication)中所述，配置 SQL Server 复制  

 此方案假定 MDT 已在主部署服务器上配置，并且 MDT DB 的配置已完成（如本文档开头所述）。  

###  <a name="EnsureInfrastructure"></a> 确保存在适当的基础结构  
 高度可缩放的 LTI 部署基础结构使用集散拓扑来复制内容；因此，首先在生产环境中指定一个部署服务器，执行主部署服务器的角色。  下面列出了主部署服务器所需的组件。  

 |**所需的组件** |**用途/注释** |  
 |-|-|  
 |Windows Server 2003 R2|用于支持 DFS-R|  
 |MDT |包含部署共享的主控副本|  
 |SQL Server 2005|必须是完整版本才能允许复制 MDT DB|  
 |DFS-R |用于复制部署共享|  
 |Windows 部署服务 |用于允许启动基于 PXE 的网络安装|  

 已选择主部署服务器后，请在每个站点预配其他服务器以支持 LTI 部署。  下面列出了子部署服务器所需的组件。  

 |**所需的组件** |**用途/注释** |  
 |-|-|  
 |Windows Server 2003 R2|用于支持 DFS-R|  
 |Microsoft SQL Server 2005 Express Edition |接收 MDT DB 的复制的副本|  
 |DFS-R |用于复制部署共享|  
 |Windows 部署服务 |用于允许启动基于 PXE 的网络安装|  

> [!NOTE]
>  Windows 部署服务必须在每个子服务器上进行设置和配置，但不需要添加启动或安装映像。  

###  <a name="AddContent"></a> 将内容添加到 MDT  
 通过 Deployment Workbench 使用内容填充主部署服务器，并按照以下部分所述创建和填充 MDT DB。 若要了解使用以下内容填充数据库：  

-   应用程序，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置应用程序”部分  

-   操作系统，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置操作系统”部分  

-   操作系统包，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置包”部分  

-   设备驱动程序，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置设备驱动程序”部分  

-   任务序列，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置任务序列”部分  

> [!NOTE]
>  确保部署共享更新时创建的 LiteTouchPE_x86.wim 文件已添加到 Windows 部署服务。  

###  <a name="PrepareDeployment"></a> 准备 Windows 部署服务  
 由于将通过 DFS-R 复制组定期复制 LiteTouchPE_x86.wim 文件，所以必须定期更新引导配置数据存储以反映新复制的 Windows PE 环境。 在每个部署服务器上执行以下步骤。  

 **准备 Windows 部署服务**  

1.  打开命令提示符窗口。  

2.  键入“WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60”，然后按 Enter。  

> [!NOTE]
>  在此示例中，刷新周期设置为 60 分钟；但是，可将此值配置为在与 DFS-R 复制相等的时间段内进行复制。  

###  <a name="ConfigureFileReplication"></a> 配置分布式文件系统复制  
 缩放 LTI 部署体系结构时，可使用 DFS-R 作为从 MDT 部署共享和 Windows PE Lite Touch 启动环境复制内容的基础，以及作为将内容从主部署服务器复制到子部署服务器的基础。  

> [!NOTE]
>  执行以下步骤之前，请确保安装了 DFS-R。  

 **配置 DFS-R 以复制部署内容**  

1.  打开 DFS 管理控制台。  

2.  在 DFS 管理控制台中展开 DFS 管理。  

3.  右键单击“复制”，然后单击“新建复制组”。  

4.  在“新建复制组向导”的“复制组类型”页上，单击“新建多用途复制组”。  

5.  单击“下一步” 。  

6.  在“名称和域”页上，键入以下信息：  

    -   在“复制组名称”框中，键入复制组的名称（如 MDT 2010 复制组）。  

    -   在“复制组的可选描述”框中，键入复制组的描述（如 MDT 2010 数据复制组）。  

    -   确保“域”框包含中正确的域名。  

7.  单击“下一步” 。  

8.  在“复制组成员”页上，执行以下步骤：  

    1.  单击“添加” 。  

    2.  键入要成为此复制组成员的所有服务器的名称（例如，所有子部署服务器和主部署服务器）。  

    3.  单击" **确定**"。  

9. 单击“下一步” 。  

10. 在“拓扑选择”页上，单击“集散”，然后单击“下一步”。  

11. 在“中心成员”页上，单击主部署服务器，然后单击“添加”。  

12. 单击“下一步” 。  

13. 在“集散连接”页上，确保对于每个子部署服务器而言，列出的主部署服务器是“所需中心成员”。  

14. 单击“下一步” 。  

15. 在“复制组计划和带宽”页上，指定用于在服务器之间复制内容的计划。  

16. 单击“下一步” 。  

17. 在“主要成员”页上的“主要成员”框中，单击主部署服务器。  

18. 单击“下一步” 。  

19. 在“要复制的文件夹”页上，单击“添加”，然后执行以下操作：  

    1.  在“要复制的文件夹的本地路径”框中，单击“浏览”，转到“*X:\\*Deployment”文件夹（其中，*X* 是部署服务器上的驱动器号）。  

    2.  单击“使用基于路径的名称”。  

    3.  单击" **确定**"。  

    4.  单击“添加” 。  

    5.  在“添加要复制的文件夹”对话框中，单击“浏览”，转到 X:\RemoteInstall\Boot 文件夹。  

    6.  单击“使用基于路径的名称”。  

20. 单击“下一步” 。  

21. 在“其他成员上分发的本地路径”页上，执行以下步骤：  

    1.  选择分发组中的所有成员，然后单击“编辑”。  

    2.  在“编辑本地路径”对话框中，单击“启用”。  

    3.  键入其中“Deployment Share”文件夹应存储在子部署服务器上的路径，例如 X:\Deployment（其中 X 是部署服务器上的驱动器号）。  

    4.  单击" **确定**"。  

22. 单击“下一步” 。  

23. 在“其他成员上启动的本地路径”页上，执行以下步骤：  

    1.  选择分发组中的所有成员，然后单击“编辑”。  

    2.  在“编辑本地路径”对话框中，单击“启用”。  

    3.  键入其中“Boot”文件夹应存储在子部署服务器上的路径，例如 X:\RemoteInstall\Boot（其中 X 是部署服务器上的驱动器号）。  

    4.  单击" **确定**"。  

24. 单击“下一步” 。  

25. 在“远程设置和创建复制组”页上，单击“创建”，完成“新建复制组向导”。  

26. 在“确认”页上，单击“关闭”以关闭向导。  

> [!NOTE]
>  确保新复制组现在列于“复制”节点下。  

###  <a name="PrepareSQLReplication"></a> 准备 SQL Server 复制  
 在配置 SQL Server 复制之前，请完成几个预配置步骤以确保部署服务器配置正确。  

 **在主部署服务器上准备 SQL Server 复制**  

1.  创建文件夹来存储数据库快照，然后将该文件夹配置为共享。  

    > [!NOTE]
    >  有关保护快照文件夹的安全的详细信息，请参阅[保护快照文件夹](http://msdn2.microsoft.com/library/ms151151.aspx)。  

2.  确保 SQL Server Browser 服务已启用并设置为“自动”。  

3.  在“SQL Server 外围应用配置”框中，单击“本地和远程连接”。  

 **在子部署服务器上准备 SQL Server 复制**  

1.  在“SQL Server 外围应用配置”框中，单击“本地和远程连接”。  

2.  或者，创建一个空数据库来托管复制的 MDT DB。  

> [!NOTE]
>  此数据库必须与主部署服务器上的 MDT DB 具有相同的名称。 例如，如果主部署服务器上的 MDT DB 名为“MDTDB”，则在子部署服务器上创建一个名为“MDTDB”的空数据库。  

###  <a name="ConfigureSQLReplication"></a> 配置SQL Server复制  
 配置生成部署基础结构所需的文件和文件夹复制后，配置 SQL Server 以复制 MDT DB。  

> [!NOTE]
>  也可仅维护单个中央 MDT DB；但是，通过维护 MDT DB 的复制版本，可在广域网 (WAN) 上对数据传输维持更好的控制。  

 SQL Server 2005 使用与发行杂志模型类似的复制模型：  

1.  出版商提供（出版）杂志。  

2.  分销商分发出版物。  

3.  读者可订阅出版物，以便该出版物定期交付给订阅者（推送订阅）。  

 此术语用于 SQL Server 复制设置和配置向导中。  

#### <a name="configure-a-sql-server-publisher"></a>配置 SQL Server 发布服务器  
 若要将主部署服务器配置为 SQL Server 发布服务器，请执行以下操作：  

1.  打开 SQL Server Management Studio?  

2.  右键单击“复制”节点，然后单击“配置分发”。  

3.  在“配置分发向导”中，单击“下一步”。  

4.  在“分发服务器”页上，单击“将充当自己的分发服务器；SQL Server 将创建分发数据库和日志”，然后单击“下一步”。  

5.  在“快照文件夹”页上的“准备 SQL Server 复制”部分，键入创建的快照文件夹的 UNC 路径。  

6.  在“分发数据库”页上，单击“下一步”。  

7.  在“发布服务器”页上，单击主部署服务器，将其设置为分发服务器，然后单击“下一步”。  

8.  在“向导操作”页上，单击“配置分发”，然后单击“下一步”。  

9. 单击“完成”，然后向导完成后单击“关闭”。  

#### <a name="enable-the-mdt-db-for-replication"></a>启用 MDT DB 进行复制  
 要在主部署服务器上启用 MDT DB 进行复制，请执行以下步骤：  

1.  在 SQL Server Management Studio 中，右键单击“复制”节点，然后单击“发布服务器属性”。  

2.  在“发布服务器属性”页上，执行以下操作：  

    1.  单击“发布服务器数据库”。  

    2.  单击“MDT DB”，然后单击“事务”。  

    3.  单击" **确定**"。  

 现已为事务和快照复制配置了 MDT DB。  

#### <a name="create-a-publication-of-the-mdt-db"></a>创建 MDT DB 的发布  
 若要创建子部署服务器可以订阅的 MDT DB 的发布，请执行以下步骤：  

1.  在 SQL Server Management Studio 中，展开“复制”，右键单击“本地发布”，然后单击“新建发布”。  

2.  在“新建发布向导”中，单击“下一步”。  

3.  在“发布数据库”页中，单击“MDT DB”，然后单击“下一步”。  

4.  在“发布类型”页上，单击“快照发布”，然后单击“下一步”。  

5.  在“项目”页上，选择所有“表”、“存储过程”和“视图”，然后单击“下一步”。  

6.  在“项目问题”页上，单击“下一步”。  

7.  在“筛选表行”页上，单击“下一步”。  

8.  在“快照代理”页上，执行以下步骤：  

    1.  选择“立即创建快照并使快照保持可用状态，以初始化订阅”。  

    2.  单击“计划在以下时间运行快照代理”。  

    3.  单击“更改” 。  

    > [!NOTE]
    >  指定将在数据库复制前一小时出现的计划。  

9. 单击“下一步” 。  

10. 在“代理安全性”页上，单击快照代理将在其下运行的帐户，然后单击“下一步”。  

11. 在“向导操作”页上，单击“创建发布”，然后单击“下一步”。  

12. 在“完成该向导”页上的“发布名称”中键入发布的描述性名称。  

13. 单击“完成”以完成向导，然后在向导已创建发布时单击“关闭”。  

    > [!NOTE]
    >  发布现在将显示在 SQL Server Management Studio 中的“本地发布”节点下。  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>将子部署服务器订阅到已发布的 MDT DB  
 现在已发布 MDT DB，可将子部署服务器作为订阅服务器添加到此发布；也就是说，他们将按计划收到数据库副本，以便在部署期间，客户端计算机可查询网络的本地数据库，而不是跨 WAN 进行数据库查询。  

 **将子部署服务器订阅到 MDT DB 发布**  

1.  在 SQL Server Management Studio 中，转到 Replication/Local Publications。  

2.  右键单击之前部分中创建的发布，然后单击“新建订阅”。  

3.  在“新建订阅向导”中，单击“下一步”。  

4.  在“发布”页上，单击之前部分中创建的发布。  

5.  在“分发代理位置”页中，单击“在分发服务器 SERVERNAME 上运行所有代理(推送订阅)”，然后单击“下一步”。  

6.  在“订阅服务器”页上，执行以下步骤，添加每个子部署服务器：  

    1.  单击“添加订阅服务器”，然后单击“添加 SQL Server 订阅服务器”。  

    2.  添加每个子部署服务器。  

    3.  对于添加的每个子部署服务器，请在“订阅数据库”框中，单击该子部署服务器上的空白 MDT DB。  

    > [!NOTE]
    >  如果尚未创建空的 MDT DB，请在“订阅数据库”框中选择创建新数据库的选项。  

    > [!NOTE]
    >  此数据库必须与主部署服务器上的 MDT DB 具有相同的名称。 例如，如果主部署服务器上的 MDT DB 名为“MDTDB”，则在子部署服务器上创建一个名为“MDTDB”的空数据库。  

7.  单击“下一步” 。  

8.  在“分发代理安全性”页上，单击“…” 以打开“分发代理安全性”对话框。  

9. 键入用于分发代理的帐户的详细信息，然后单击“下一步”。  

10. 在“同步计划”页上，执行以下步骤：  

    1.  在“代理计划”框中，单击“<定义计划\>”。  

    2.  指定应用于在主部署服务器和子部署服务器之间复制数据库的计划，然后单击“下一步”。  

11. 在“初始化订阅”页上，单击“下一步”。  

12. 在“向导操作”页上，单击“创建订阅”，然后单击“下一步”。  

13. 单击“完成”，在向导成功完成后单击“关闭”。  

 现在配置了 SQL Server 复制，并且 MDT DB 将从主部署服务器复制到已定期订阅到该发布的所有子部署服务器。  

#### <a name="configure-customsettingsini"></a>配置 CustomSettings.ini  
 现已成功创建 LTI 部署基础结构，每个位置将包含一个 LTI 部署服务器，并具有以下内容的已复制副本：  

-   部署共享  

-   MDT DB  

-   已添加到 Windows部署服务的 LiteTouchPE_x86 Windows PE 环境  

 现在，可配置部署共享的 CustomSettings.ini 文件，通过其本地部署服务器，以及从 Windows 部署服务交付 LiteTouchPE_x86.wim 环境的服务器来使用部署内容（部署共享和数据库）。  

 从 Windows 部署服务交付 LiteTouchPE_x86.wim 文件时，通过正在使用的 Windows 部署服务服务器的名称来配置注册表项。 MDT 在可用于配置 CustomSettings.ini 的变量 (%WDSServer%) 中捕获此服务器名称。  

 **始终使用本地 LTI 部署服务器**  

> [!NOTE]
>  以下过程假定已创建部署共享并将其设置为 Deployment$ 共享。  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  点击“规则”选项卡，然后修改 CustomSettings.ini file 以配置以下属性：  

    -   对于已添加的每个 SQL Server 部分，请配置“SQLServer”以使用服务器名称“%WDSServer%”，例如“SQLServer=%WDSServer%”。  

    -   如果配置“DeployRoot”，请配置“DeployRoot”以使用“%WDSServer%”变量，例如“DeployRoot=\\\\%WDSServer%\Deployment$”。  

5.  单击“编辑 Bootstrap.ini”。  

6.  通过添加“DeployRoot”值或将其更改为“DeployRoot=\\\\%WDSServer%\Deployment$”，配置 BootStrap.ini 以使用“%WDSServer%”属性。  

7.  单击“文件”，然后单击“保存”以保存对 BootStrap.ini 文件所做的更改。  

8.  单击" **确定**"。  

     需要更新部署共享和 LiteTouchPE_x86.wim Windows PE 环境。  

9. 在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

10. 在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

11. 在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

12. 在“确认”页上，单击“完成”。  

 以下示例展示了执行本节中概述的步骤之后的 CustomSettings.ini。  

 **为可缩放 LTI 部署基础结构配置的示例 CustomSettings.ini**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>多个服务器存在时选择本地 MDT 服务器  
 在此方案中，多个 MDT 服务器正用于支持大量同时部署和跨多个站点的部署。 初始化 LTI 部署时，默认操作是请求 MDT 服务器的路径，连接并访问所需文件以开始部署过程。  

 Windows 部署向导可使用 LocalServer.xml 文件为每个位置提供已知部署服务器的选择。  

 通过以下方式使用 LocationServer.xml 文件：  

-   如[了解 LocationServer.xml](#UnderstandingLocationServer) 中所述，了解 LocationServer.xml 的用途和用法  

-   如[创建 LocationServer.xml 文件](#CreateLocationServer)中所述，创建 LocationServer.xml 文件  

-   如将 LocationServer.xml 文件添加到 Extra Files 目录中所述，将 LocationServer.xml 文件添加到 Extra Files 目录  

-   如[更新 BootStrap.ini 文件](#UpdateBootstrap)中所述，更新 BootStrap.ini 文件  

-   如[更新部署共享](#UpdateDeploymentShare)中所述，更新部署共享  

 此方案假定在部署服务器上配置了 MDT。  

###  <a name="UnderstandingLocationServer"></a> 了解 LocationServer.xml  
 首先，必须了解 MDT 如何使用 LocationServer.xml。 在 LTI 期间，MDT 脚本读取并处理 BootStrap.ini 文件，收集关于部署的初始信息。 这在与部署服务器建立连接之前发生。 因此，“DeployRoot”属性通常用于在 BootStrap.ini 文件中指定应与之建立连接的部署服务器。  

 如果 BootStrap.ini 文件不包含“DeployRoot”属性，则 MDT 脚本将加载向导页，提示用户输入部署服务器的路径。 初始化“HTML 应用程序(HTA)”向导页时，MDT 脚本检查是否存在 LocationServer.xml 文件，如果存在，则使用 LocationServer.xml 显示可用的部署服务器。  

#### <a name="understand-when-to-use-locationserverxml"></a>了解何时使用 LocationServer.xml  
 LTI 部署期间，MDT 提供多种方式来确定要连接到的服务器。 定位部署服务器的不同方法适用于不同的方案；因此，了解何时使用 LocationServer.xml 非常重要。  

 MDT 提供了几种自动发现和使用最佳部署服务器的方法。 下表列出了这些方法。

 |**方法** |**详细信息** |  
 |-|-|  
 |**%WDSServer%** |在 Windows 部署服务服务器上共同托管 MDT 服务器时使用此方法。<br /><br /> 从 Windows 部署服务启动 LTI 部署时，会创建一个环境变量 - %WDSServer%，并用 Windows 部署服务服务器的名称填充。<br /><br /> DeployRoot 变量可使用此变量自动连接到 Windows 部署服务服务器上的部署共享，例如：<br /><br /> DeployRoot=\\\\%WDSServer%\Deployment$ |  
 |**基于位置的自动化** |MDT 可使用 BootStrap.ini 文件中基于位置的自动化，确定应该部署的服务器。<br /><br /> 使用“默认网关”属性来区分不同的位置；为每个“默认网关”指定了不同的 MDT 服务器。<br /><br /> 有关使用基于位置的自动化的详细信息，请参阅“选择应用配置设置的方法”。|  

 上表中列出的每种方法都提供了一种方法，可自动执行特定方案的给定位置中的部署服务器选择。 这些方法针对特定的方案 - 例如，当使用 Windows 部署服务共同托管 MDT 服务器时。  

 这些方法不适用于某些情况 - 例如，如果在给定位置有多个部署服务器或自动化逻辑不可行（如网络分段不足，不能确定位置或将 MDT 服务器与 Windows 部署服务分离）。  

 在这些情况下，LocationServer.xml 文件提供了一种灵活的方式，可在部署时提供此信息，而无需了解服务器名称和部署共享名称。  

###  <a name="CreateLocationServer"></a> 创建 LocationServer.xml 文件  
 若要在 LTI 部署期间显示可用部署服务器的列表，请创建一个 LocationServer.xml 文件，其中包含有关每个服务器的详细信息。 MDT 中没有默认的 LocationServer.xml 文件，因此请使用以下指南创建一个。  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>创建一个 LocationServer.xml 文件以支持多个位置  
 创建和使用 LocationServer.xml 的最简单方法是创建一个 LocationServer.xml 文件，并为环境中的每个部署服务器（可位于相同位置或不同位置）添加条目。  

 通过为每个服务器创建一个新的节来构造 LocationServer.xml 文件，然后添加以下信息：  

-   唯一标识符  

-   位置名称，用于为该位置提供容易识别的名称  

-   该位置的 MDT 服务器的 UNC 路径  

 以下内容使用为多个位置配置的示例 LocationServer.xml 文件，说明了如何使用其中每个属性创建 LocationServer.xml 文件。  

 **支持多个位置的 LocationServer.xml 文件示例**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 使用此格式，为每个位置指定不同的服务器条目，或在单个位置存在多个服务器的情况下，为该位置的每个服务器指定不同的服务器条目，如以下示例所示。   

 **支持多个位置中多个服务器的 LocationServer.xml 文件示例**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>创建 LocationServer.xml 文件以对不同位置的多个服务器执行负载均衡  
 使用 LocationServer.xml，为每个位置条目指定多个服务器，然后执行基本的负载均衡，以便在选定位置时，MDT 从可用服务器列表中自动选择部署服务器。 为了提供此功能，LocationServer.xml 文件支持指定权重指标。  

 下面展示了为不同位置的多个服务器配置的示例 LocationServer.xml 文件。  

 **不同位置的 LocationServer.xml 文件示例**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 通过 MDT 在服务器选择过程中使用的 <server weight\> 标志来指定权重指标。 服务器入选的可能性计算如下：  

 **服务器权重/所有服务器权重总和**  

 在前面的示例中，将 Contoso HQ 中的三台服务器列为 1、2 和 4。 权重为 2 的服务器的入选可能性为七分之二。 因此，若要使用权重系统，请确定某个位置可用服务器的容量，并将服务器的容量与其他每个服务器相比来衡量该服务器。  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>将 LocationServer.xml 文件添加到 Extra Files 目录  
 创建 LocationServer.xml 文件后，将其添加到X:\\Deploy\Control folder 中的 LiteTouch_x86 和 LiteTouch_x64 Windows PE 启动映像。 使用 Deployment Workbench，通过指定要在部署共享属性中添加的其他目录，将其他文件和文件夹添加到这些 Windows PE 映像。  

 **将 LocationServer.xml 添加到部署共享**  

1.  在根部署共享文件夹（例如 D:\Production Deployment Share\Extra Files）中创建一个名为“Extra Files”的文件夹。  

2.  在“Extra Files”文件夹中创建文件夹结构，反映其他文件应驻留的 Windows PE 位置。  

     例如，LocationServer.xml 文件必须位于 Windows PE 中的 \Deploy\Control 文件夹；因此，在“Extra Files”下创建相同的文件夹结构（例如 D:\Production Deployment Share\Extra Files\Deploy\Control）。  

3.  将 LocationServer.xml 复制到 deployment_share\Extra Files\Deploy\Control 文件夹（其中 deployment_share 是部署共享的根文件夹的完全限定路径）。  

4.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

5.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

6.  在“操作”窗格中，单击“属性”。  

7.  在“eployment_shareProperties”对话框中（其中 deployment_share 是部署共享的名称），执行以下步骤：  

    1.  单击“Windows PE platform 设置”选项卡（其中 platform 是要配置的 Windows PE 映像的体系结构）。  

    2.  在“Windows PE 自定义”部分中的“要添加的其他目录”框中，键入“path”（其中 path 是“Extra Files”文件夹的完全限定的路径，例如 D:\Production Deployment Share\Extra Files），然后单击“确定”。  

###  <a name="UpdateBootstrap"></a> 更新 BootStrap.ini 文件  
 使用 Deployment Workbench 创建部署共享时，会自动创建“DeployRoot”属性并将其填充到 BootStrap.ini 文件中。 因为 LocationServer.xml 文件用于填充“DeployRoot”属性，所以必须从 BootStrap.ini 文件中移除此值。  

 **从 BootStrap.ini 文件移除 DeployRoot 属性**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  在“deployment_shareProperties”对话框中（其中 deployment_share 是部署共享的名称），单击“规则”选项卡，然后单击“编辑 BootStrap.ini”。  

5.  移除“DeployRoot”值（例如 DeployRoot=\\\Server\Deployment$）。  

6.  单击“文件”，然后单击“保存”以保存对 BootStrap.ini 文件所做的更改。  

7.  单击“确定”，提交所做的更改。  

###  <a name="UpdateDeploymentShare"></a> 更新部署共享  
 接下来必须更新部署共享，生成包含 LocationServer.xml 文件和更新的 BootStrap.ini 文件的新 LiteTouch_x86 和 LiteTouch_x64 启动环境。  

 **更新部署共享**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

4.  在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

5.  在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

6.  在“确认”页上，单击“完成”。  

> [!NOTE]
>  更新过程完成后，将新的 LiteTouch_x86 和 LiteTouch_x64 Windows PE 环境添加回 Windows 部署服务，或者将其刻录到部署期间要使用的启动介质。  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>通过 Lite Touch 安装使用新计算机替换现有计算机  
 可使用 MDT 将映像部署到新计算机，此计算机将替换企业架构中现有的计算机。 从一个操作系统升级到另一个操作系统时（新的操作系统可能需要新的硬件），或者组织需要更新更快的计算机来使用现有应用程序时，可能会出现这种情况。  

 用新计算机替换现有计算机时，Microsoft 建议考虑将所有设置从一台计算机迁移到另一台计算机，例如用户帐户和用户状态数据。 另外，在迁移失败的情况下，创建恢复解决方案非常重要。  

 在此示例部署中，通过从 WDG-EXIST-01 捕获用户状态数据并将其保存到网络共享中，在 CORP 域中用新计算机 (WDG-NEW-02) 替换现有计算机 (WDG-EXIST-01)。 然后，将现有映像部署到 WDG-NEW-02，最后将捕获的用户状态数据还原到 WDG-NEW-02。 将从部署服务器 (WDG-MDT-01) 执行部署。  

 在 MDT 中，使用“标准客户端替换任务序列”模板来创建将执行所有必要部署任务的任务序列。  

 此演示假设：  

-   已在部署服务器 (WDG MDT 01) 上安装了 MDT  

-   已创建并填充部署共享，包括操作系统映像、应用程序和设备驱动程序  

-   已捕获引用计算机的映像并将其部署到新计算机 (WDG NEW 02)  

-   已在具有适当共享权限的部署服务器 (WDG MDT 01) 上创建并共享网络共享文件夹 (UserStateCapture$)  

 在开始此示例之前，部署共享应存在。 有关创建部署共享的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中管理部署共享”部分。  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>步骤 1：创建任务序列以捕获用户状态  
 使用“新建任务序列向导”在 Deployment Workbench 的“任务序列”节点中创建 MDT 任务序列。 若要执行“替换计算机”部署方案的第一部分（捕获现有计算机上的用户状态），请在“新建任务序列向导”中选择“标准客户端替换任务序列”模板。  

 **创建任务序列以捕获“替换计算机”部署方案中的用户状态**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“新建任务序列”。  

     将启动“新建任务序列向导”。  

4.  使用以下信息，完成“新建任务序列向导”。 请接受默认值，除非另行说明。  

    |**在此向导页上** |**执行此操作** |  
    |-|-|  
    |**常规设置** |1.在“任务序列 ID”中，键入“VISTA_EXIST”。<br />2.在“任务序列名称”中，键入“在现有计算机上执行替换计算机方案”。<br />3.单击“下一步” 。|  
    |**选择模板** |在“以下任务序列模板可用”中， 选择所需的起始模板，并选择“标准客户端替换任务序列”，然后单击“下一步”。|  
    |**摘要** |验证配置详细信息是否正确，然后单击“下一步”。|  
    |**确认** |单击 **“完成”**。|  

 完成“新建任务序列向导”，将 VISTA_EXIST 任务序列添加到任务序列列表中。  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>步骤 2：创建任务序列以部署操作系统和还原用户状态  
 使用“新建任务序列向导”在 Deployment Workbench 的“任务序列”节点创建 MDT 任务序列。 若要执行“替换计算机”部署方案的第二部分（部署操作系统，然后还原现有计算机上的用户状态），请在“新建任务序列向导”中选择“标准客户端任务序列”模板。  

 **创建任务序列以部署“替换计算机”部署方案中的用户状态**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“新建任务序列”。  

     将启动“新建任务序列向导”。  

4.  使用以下信息，完成“新建任务序列向导”。 请接受默认值，除非另行说明。  

    |**在此向导页上**|**执行此操作**|  
    |-|-|  
    |**常规设置**|1.在“任务序列 ID”中，键入“VISTA_NEW”。<br />2.在“任务序列名称”中，键入“在新计算机上执行替换计算机方案”。<br />3.单击“下一步” 。|  
    |**选择模板**|在“以下任务序列模板可用”中， 选择所需的起始模板，并选择“标准客户端任务序列”，然后单击“下一步”。|  
    |**选择操作系统**|在“以下操作系统映像可使用此任务序列进行部署”中， 选择一个要使用的操作系统，并选择“captured_vista_image”（其中 captured_vista_image 是引用计算机添加到 Deployment Workbench 中“操作系统”节点的已捕获映像），然后单击“下一步”。|  
    |**指定产品密钥**|选择“不在此时指定产品密钥”，然后单击“下一步”。|  
    |操作系统设置|1.在“全名”中，键入“Woodgrove 职员”。<br />2.在“组织”中，键入“Woodgrove Bank”。<br />3.在“Internet Explorer 主页”中，键入“http://www.woodgrovebank.com”。<br />4.单击“下一步” 。|  
    |**管理员密码**|在“管理员密码”和“请确认管理员密码”中，键入“P@ssw0rd”，然后单击“完成”。|  
    |**确认**|单击 **“完成”**。|  

 完成“新建任务序列向导”，将 VISTA_NEW 任务序列添加到任务序列列表中。  

### <a name="step-3-customize-the-mdt-configuration-files"></a>步骤 3：自定义 MDT 配置文件  
 创建了 MDT 任务序列后，自定义提供用于捕获用户状态信息的配置设置的 MDT 配置文件。 具体而言，通过修改部署过程中早先创建的部署共享的属性中的文件来自定义 CustomSettings.ini 文件。 在稍后的步骤中，将更新部署共享以确保在部署共享中更新配置文件。  

 **自定义用于捕获用户状态信息的 MDT 配置文件**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

     出现“属性”对话框。  

4.  在“属性”对话框中，单击“规则”选项卡。  

5.  在“规则”选项卡上，修改 CustomSettings.ini 文件，反映必要的更改，如以下示例所示。 根据环境做出任何其他修改。  

     **自定义的 CustomSettings.ini 文件**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  在“属性”对话框中，单击“确定”。  

7.  关闭所有打开的窗口和对话框。  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>步骤 4：为部署共享配置 Windows PE 选项  
 在 Deployment Workbench 的“部署共享”节点中为部署共享配置 Windows PE 选项。  

> [!NOTE]
>  如果 Windows Vista 中包含现有计算机 (WDG-EXIST-01) 和新计算机 (WDG-NEW-01) 的设备驱动程序，请跳过此步骤并继续执行下面的步骤。  

 **为部署共享配置 Windows PE 选项**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

     出现“属性”对话框。  

4.  在“属性”对话框中，在“Windows PE platform 组件”选项卡上（其中 platform 是要配置的 Windows PE 映像的体系结构），在“选择配置文件”中选择“device_drivers”（其中 device_drivers 是设备驱动程序选择配置文件的名称），然后单击“确定”。  

### <a name="step-5-update-the-deployment-share"></a>步骤 5：更新部署共享  
 为部署共享配置 Windows PE 选项后，更新部署共享。 更新部署共享会更新所有 MDT 配置文件并生成 Windows PE 的自定义版本。 自定义版本的 Windows PE 用于启动引用计算机并启动 LTI 部署过程。  

 **在 Deployment Workbench 中更新部署共享**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

4.  在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

5.  在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

6.  在“确认”页上，单击“完成”。  

 Deployment Workbench 开始更新部署共享。 Deployment Workbench 在 deployment_share\Boot 文件夹创建 LiteTouchPE_x86.iso 和 LiteTouchPE_x86.wim 文件（用于 32 位目标计算机）或 LiteTouchPE_x64.iso 和 LiteTouchPE_x64.wim 文件（用于 64 位目标计算机）（其中 deployment_share 是用作部署共享的共享文件夹）。  

### <a name="step-6-create-the-lti-bootable-media"></a>步骤 6：创建 LTI 可启动介质  
 提供一种方法，用于在更新部署共享时使用创建的自定义 Windows PE 版本来启动计算机。 Deployment Workbench 在 deployment_share\Boot 文件夹创建 LiteTouchPE_x86.iso 和 LiteTouchPE_x86.wim 文件（用于 32 位目标计算机）或 LiteTouchPE_x64.iso 和 LiteTouchPE_x64.wim 文件（用于 64 位目标计算机）（其中 deployment_share 是用作部署共享的共享文件夹）。 通过其中一个映像创建适当的 LTI 可启动介质。  

 **创建 LTI 可启动介质**  

1.  在 Windows 资源管理器中，导航到 deployment_share\Boot 文件夹（其中 deployment_share 是用作部署共享的共享文件夹）。  

2.  根据用于现有计算机 (WDG-EXIST-01) 和新计算机 (WDG-NEW-02) 的计算机类型，执行以下任务之一：  

    -   如果引用计算机是物理计算机，则创建 ISO 文件的 CD 或 DVD。  

    -   如果引用计算机是虚拟机，则直接从 ISO 文件或者 ISO 文件的 CD 或 DVD 启动虚拟机。  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>步骤 7：使用 LTI 可启动介质启动现有计算机  
 使用过程中早前创建的 LTI 可启动介质启动现有计算机 (WDG-EXIST-01)。 该 CD 在现有计算机上启动 Windows PE 并启动 MDT 部署过程。 MDT 部署进程结束时，用户状态迁移信息存储在 UserStateCapture$ 共享文件夹中。  

> [!NOTE]
>  还可通过从 Windows 部署服务启动目标计算机来启动 MDT 过程。 有关详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“准备 Windows 部署服务”部分。  

 **使用 LTI 可启动介质启动现有计算机**  

1.  使用过程中早前创建的 LTI 可启动介质启动 WDG-EXIST-01。  

     将启动 Windows PE，然后启动 Windows 部署向导。  

2.  使用以下信息完成 Windows 部署向导。 请接受默认值，除非另行说明。  

    |**在此向导页上**|**执行此操作**|  
    |-|-|  
    |**欢迎使用部署**|单击“运行部署向导”安装新的操作系统，然后单击“下一步”。|  
    |**指定用于连接到网络共享的凭据**|1.在“用户名”中，键入“管理员”。<br />2.在“密码”中，键入“P@ssw0rd”。<br />3.在“域”中，键入“CORP”。<br />4.单击" **确定**"。|  
    |**选择要在此计算机上执行的任务序列**|单击“在现有计算机上执行替换计算机方案”，然后单击“下一步”。|  
    |**指定存储数据和设置的位置**|单击“下一步” 。|  
    |**指定存储完整计算机备份的位置**|单击“不备份现有计算机”，然后单击“下一步”。|  
    |**准备开始**|单击“开始”。|  

     如果出现任何错误或警告，请参阅 MDT 文档《疑难解答参考》。  

3.  在“部署摘要”对话框中，单击“详细信息”。  

     如果出现任何错误或警告，请查看错误或警告并记录所有诊断信息。  

4.  在“部署摘要”对话框中，单击“完成”。  

 捕获用户状态迁移信息并将其存储在过程中早前创建的网络共享文件夹 (UserStateCapture$) 中。  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>步骤 8：使用 LTI 可启动介质启动新计算机  
 使用过程中早前创建的 LTI 可启动介质启动现有新计算机 (WDG-NEW-02)。 此 CD 在引用计算机上启动 Windows PE 并启动 MDT 部署过程。 MDT 部署过程结束时，将在新计算机上部署 Windows Vista，并将捕获的用户状态迁移信息还原到新计算机。  

> [!NOTE]
>  还可通过从 Windows 部署服务启动目标计算机来启动 MDT 过程。 有关详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“准备 Windows 部署服务”部分。  

 **使用 LTI 可启动介质启动新计算机**  

1.  使用过程中早前创建的 LTI 可启动介质启动 WDG-NEW-02。  

     将启动 Windows PE，然后启动 Windows 部署向导。  

2.  使用以下信息完成 Windows 部署向导。 请接受默认值，除非另行说明。  

    |**在此向导页上**|**执行此操作**|  
    |--|--|
    |**欢迎使用部署**|单击“运行部署向导安装新操作系统”，然后单击“下一步”。|  
    |**指定用于连接到网络共享的凭据**|1.在“用户名”中，键入“管理员”。<br />2.在“密码”中，键入“P@ssw0rd”。<br />3.在“域”中，键入“CORP”。<br />4.单击" **确定**"。|  
    |**选择要在此计算机上执行的任务序列**|单击“在新计算机上执行替换计算机方案”，然后单击“下一步”。|  
    |**配置计算机名称**|在“计算机名称”中，键入“WDG-NEW-02”，然后单击“下一步”。|  
    |**将计算机加入域或工作组中**|单击“下一步” 。|  
    |**指定是否还原用户数据**|1.单击“指定位置”。<br />2.在“位置”中，键入“\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01”。<br />3.单击“下一步” 。|  
    |**区域设置选择**|单击“下一步” 。|  
    |**设置时区**|单击“下一步” 。|  
    |**指定是否捕获映像**|单击“不捕获此计算机的映像”，然单击“下一步”。|  
    |**指定 BitLocker 配置**|单击“不启用此计算机的 BitLocker”，然单击“下一步”。|  
    |**准备开始**|单击“开始”。|  

     如果出现任何错误或警告，请参阅 MDT 文档《疑难解答参考》。  

3.  在“部署摘要”对话框中，单击“详细信息”。  

     如果出现任何错误或警告，请查看错误或警告并记录所有诊断信息。  

4.  在“部署摘要”对话框中，单击“完成”。  

 Windows Vista 现在安装在新计算机上，并且也还原了捕获的用户状态迁移信息。  

## <a name="integrating-custom-deployment-code-into-mdt"></a>将自定义部署代码集成到 MDT  
 部署团队通常需要具有特定于其目标环境的复杂要求，但 Deployment Workbench 预定义任务序列操作或默认 MDT 配置文件无法满足这些要求。 在此情况下，实施自定义代码可满足他们的要求。  

 通过以下操作，将自定义部署代码集成到 MDT：  

-   如[选择适当的脚本语言](#ChooseAppropLanguage)中所述，选择一种脚本语言  

-   如[了解如何利用 ZTIUtility](#UnderstandLeverageZTI) 中所述，利用 ZTIUtility.vbs  

-   如[集成自定义部署代码](#IntegrateCustomDeploy)中所述，集成自定义部署代码  

 以下部分假定在部署服务器上配置了 MDT。  

###  <a name="ChooseAppropLanguage"></a> 选择适当的脚本语言  
 尽管可在 Windows 或 Windows PE 上运行的任何代码都可作为应用程序安装或通过 MDT 任务序列步骤进行调用，但 Microsoft 建议以 .vbs 或 .wsf 文件的形式使用脚本。  

 使用 .wsf 文件的优点除了 ZTI 和 LTI 过程已使用的一些其他预定义函数之外，还有就是内置日志记录。 这些函数在使用 MDT 分发的 ZTIUtility 脚本中可用。  

 从自定义脚本进行引用时，ZTIUtility 脚本将初始化 MDT 环境和设置类。 以下类可用：  

-   **Logging**。 此类提供了所有 MDT 脚本使用的日志记录功能。 它还为部署期间的每个脚本运行以及所有脚本的合并日志文件创建单个日志文件。 这些日志文件是以供 TRACE32 读取的格式创建的；此工具提供于 [System Center Configuration Manager 2007 Toolkit V2](https://www.microsoft.com/download/en/details.aspx?id=9257)。  

-   **Environment**。 此类配置通过 WMI 和 MDT 规则处理收集的环境变量，并可从脚本直接引用它们。 通过此操作，可读取部署属性，从而访问 ZTI 和 LTI 过程使用的所有配置信息。  

-   **Utility**。 此类提供整个 ZTI 和 LTI 脚本中使用的常规实用程序。 Microsoft 建议，无论何时开发自定义代码，都应该检查此类，看看是否可简单重用任何代码。 有关此类中提供的某些功能的其他信息将在本节后面介绍。  

-   **Database**。 此类执行的函数如连接到数据库和从数据库读取信息等。 通常，不建议直接访问数据库类；相反，应使用规则处理来执行数据库查找。  

-   **Strings**。 此类执行通用的字符串处理例程，如创建项目的分隔列表、显示十六进制值、从字符串中剪裁空格，右对齐字符串、左对齐字符串，将值强制到字符串格式、将值强制到数组格式、生成随机全局唯一标识符 (GUID) 和 Base64 转换。  

-   **FileHandling**。 此类执行规范化路径和复制、移动以及删除文件和文件夹等函数。  

-   **clsRegEx**。 此类执行正则表达式函数。  

 在 MDT 中，已经对脚本体系结构做了一些更改，使客户端 Microsoft Visual Basic® Scripting Edition (VBScript) 更稳定可靠。 这些更改包括：  

-   对 ZTIUtility.vbs（主脚本库）做的大量更改，包括新 API 和更好的错误处理  

-   ZTI_xxx.wsf 脚本的整体结构的新外观  

 也已更改 MDT 脚本的整体结构。 大多数 MDT 脚本现已封装在 VBScript Class 对象中。 使用 RunNewInstance 函数初始化并调用此类。  

> [!NOTE]
>  即使对 ZTIUtility.vbs 进行了大量更改，大多数现有的 MDT 2008 Update 1 脚本将在 MDT 中按原样运行，因为大多数 MDT 脚本都将包含 ZTIUtility.vbs。  

###  <a name="UnderstandLeverageZTI"></a> 了解如何利用 ZTIUtility  
 ZTIUtility.vbs 文件包含可在自定义代码中利用的对象类。 使用以下内容，将自定义代码与 MDT 集成：  

-   如[使用 ZTIUtility Logging 类](#UseZTILogging) 中所述的 ZTIUtility.vbs 中定义的 Logging 类  

-   如[使用 ZTIUtility Environment 类](#UseZTIEnvironment)中所述的 ZTIUtility.vbs 中定义的 Environment 类  

-   如[使用 ZTIUtility Utility 类](#UseZTIUtility)中所述的 ZTIUtility.vbs 中定义的 Utility 类  

####  <a name="UseZTILogging"></a> 使用 ZTIUtility Logging 类  
 ZTIUtiliy.vbs 中的 Logging 类为自定义代码提供了一种简单的机制，以便在 ZTI 或 LTI 部署期间，使用和其他脚本相同的方式记录状态信息、警告和错误。 此标准化还确保“LTI 部署摘要”对话框正确报告运行的任何自定义代码的状态。  

 以下展示了一个自定义代码脚本示例，它使用 oLogging.CreateEntry 和 TestAndFail 函数，根据不同脚本操作的结果记录不同类型的消息。  

 **使用 ZTIUtility Logging 的脚本示例：ZTI_Example.wsf**   

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  如果要继续使用通过 ProcessResults() 调用 ZTIProcess() 的脚本，则可继续这样操作。 但是，将不启用某些已增强的错误处理功能。  

####  <a name="UseZTIEnvironment"></a> 使用 ZTIUtility Environment 类  
 ZTIUtiliy.vbs 中的 Environment 类提供对 MDT 属性的访问以及更新 MDT 属性的能力。 在以上示例中，oEnvironment.Item("Memory") 用于检索可用 RAM 的数量；这也可用于检索 MDT 文档《Toolkit 参考》中所述的任何属性的值。  

####  <a name="UseZTIUtility"></a> 使用 ZTIUtility Utility 类  
 ZTIUtility.vbs 脚本包含任何自定义部署脚本都可使用的大量常用实用工具。 可使用与 oLogging 和 oEnvironment 类相同的方式将这些实用工具添加到任何脚本。  

下表详细说明了一些有用函数及其输出。 有关可用函数的完整列表，请参阅 ZTIUtility.vbs 文件。  

|**函数**|**输出**|  
|-|-|
|**oUtility.LocalRootPath**|返回目标计算机上部署过程使用的根文件夹的路径，例如 C:\MININT|  
|**oUtility.BootDevice**|返回系统启动设备，例如 MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|返回部署期间使用的日志文件夹的路径，例如 C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|返回当前配置的状态存储的路径，例如 C:\MININT\StateStore|  
|**oUtility.ScriptName**|返回调用函数的脚本名，例如 Z-RAMTest|  
|**oUtility.ScriptDir**|返回调用函数的脚本的路径，例如 \\\server_name\Deployment$\Scripts|  
|**oUtility.ComputerName**|确定生成过程中将使用的计算机名，例如 computer_name|  
|**oUtility.ReadIni(file, section, item)**|允许从 .ini 文件读取指定的项|  
|**oUtility.WriteIni(file, section, item, value)**|允许将指定的项写入 .ini 文件|  
|**oUtility.Sections(file)**|读取 .ini 文件的各个部分并将其存储在对象中以供引用|  
|**oUtility.SectionContents(file, section)**|读取指定的 .ini 文件的内容并将其存储在对象中|  
|**oUtility.RunWithHeartbeat(sCmd)**|运行命令时，每 0.5 秒将检测信号信息写入日志|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|搜索 DeployRoot 文件夹和标准子文件夹中的指定文件，包括服务、工具、USMT、模板、脚本和控件|  
|**oUtility.findMappedDrive(sServerUNC)**|检查是否将驱动器映射到指定的 UNC 路径并返回驱动器号|  
|**oUtility.ValidateConnection(sServerUNC)**|检查是否存在与指定服务器的现有连接，如果没有，则尝试创建一个|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|将驱动器号映射到指定为共享的 UNC 路径并返回使用的驱动器号；如果不成功，则返回错误|  
|**VerifyPathExists(strPath)**|验证是否存在指定路径|  
|**oEnvironment.Substitute(sVal)**|在给定字符串的情况下，扩展该字符串中的任何变量或函数|  
|**oEnvironment.Item**<br /><br /> **(sName)**|读取变量或将其写入持久性存储|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|测试是否存在该变量|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|读取“数组”类型的变量或将其写入持久存储|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|如果检测到无法恢复的错误，则用于执行结构化出口|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|将消息写入日志文件并将事件发布到定义的服务器|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|将消息写入日志文件|  
|**TestAndFail(iRc, iError, sMessage)**|如果 iRc 为 false 或失败，退出带有 iError 的脚本|  
|**TestAndLog(iRc , sMessage)**|仅当 iRc 为 false 或失败时才会记录警告|  

###  <a name="IntegrateCustomDeploy"></a> 集成自定义部署代码  
 自定义部署代码可以通过多种方式集成到 MDT 过程；然而，无论使用什么方法，都应该满足以下两条规则：  

-   自定义部署代码脚本名称应始终以字母 Z 开头。  

-   自定义部署代码应放置在部署共享上的“Scripts”文件夹中，例如 D:\Production Deployment Share\Scripts。  

 集成可确保一致日志记录的自定义代码的最常用方法有：  

-   以 MDT 应用程序形式部署代码  

-   以 MDT 任务序列命令形式启动代码  

-   以用户出口脚本形式启动代码  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>以 MDT 应用程序形式部署自定义代码  
 可将自定义部署代码导入到 Deployment Workbench，并使用和其他任何应用程序相同的方式进行管理。  

 **创建新应用程序以运行自定义部署代码**  

1.  将自定义部署代码复制到“deployment_share\Scripts”文件夹（其中 deployment_share 是部署共享的完全限定的路径）。  

2.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

3.  在 Deployment Workbench 控制台树中，转到 Deployment Shares/deployment_share/Applications（其中 deployment_share 是要配置的部署共享的名称）。  

4.  在“操作”窗格中，单击“新建应用程序”。  

     将启动“新建应用程序向导”。  

5.  使用以下信息完成“新建应用程序向导”。 接受默认设置，除非另行说明。  

    |**在此向导页上**|**执行此操作**|  
    |-|-|  
    |**应用程序类型**|单击“不含源文件或位于网络上其他地方的应用程序”，然后单击“下一步”。|  
    |**详细信息**|根据应用程序中的信息完成此页设置，然后单击“下一步”。|  
    |**命令详细信息**|1.在“命令行”框中，键入“cscript.exe %SCRIPTROOT%\custom_code”（其中 custom_code 是已开发的自定义代码的名称）。<br />2.在“工作目录”框中，键入“working_directory”（其中 working_directory 是自定义代码的工作目录的名称；这通常是“命令行”框中指定的相同文件夹）。<br />3.单击“下一步” 。|  
    |**摘要**|验证配置设置是否正确，然后单击“下一步”。|  
    |**确认**|单击 **“完成”**。|  

 该应用程序出现在 Deployment Workbench 的“应用程序”节点中。  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>将自定义代码作添加为任务序列步骤  
 可直接从任务序列中的任意点调用自定义部署代码；这可访问常用的任务序列规则和选项。  

 **将自定义部署代码添加到现有任务序列**  

1.  将自定义部署代码复制到“deployment_share\Scripts”文件夹（其中 deployment_share 是部署共享的完全限定的路径）。  

2.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

3.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

4.  在详细信息窗格中，单击“task_sequence”（其中 task_sequence 是运行自定义代码的任务序列的名称）。  

5.  在“操作”窗格中，单击“属性”。  

6.  在“task_sequenceProperties”对话框中，单击“任务序列”选项卡。  

7.  在控制台树种，转到 group（其中 group 是用于添加任务序列步骤的组）。  

8.  单击“添加”、“常规”，然后单击“运行命令行”。  

9. 在控制台树种，单击“运行命令行”，然后单击“属性”选项卡。  

10. 在“名称”框中，键入“name”（其中 name 是自定义代码的描述性名称）。  

11. 在“属性”选项卡上的“命令行”框中，键入“command_line”（其中 command_line 是要运行自定义代码的命令，例如 cscript.exe %SCRIPTROOT%\CustomCode.vbs）。  

12. 在“开始位置”框中，键入“path”（其中 path 是自定义代码的工作文件夹的完全限定路径；通常与“命令行”框中指定的路径相同），然后单击“确定”。  

 新创建的任务序列步骤出现在任务序列步骤的列表中。  

#### <a name="run-custom-code-as-a-user-exit-script"></a>以用户出口脚本形式运行自定义代码  
 也可使用 UserExit 指令，从 CustomSettings.ini 中以用户出口脚本形式运行自定义代码。 这提供了将信息传递到 CustomSettings.ini 规则验证过程的机制，并提供 MDT 属性的动态更新  

 有关用户出口脚本和 UserExit 指令的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“CustomSettings.ini 文件中的用户出口脚本”部分。  

## <a name="installing-device-drivers-using-various-installation-methods"></a>使用多种安装方法安装设备驱动程序  
 在此方案中，使用 MDT 将操作系统部署到不同类型的硬件。 作为部署过程的一部分，确定并安装设备驱动程序，以便每个硬件类型将正常工作。 有两种主要的设备驱动程序；在部署过程中必须以不同的方式处理它们：  

-   包含 .inf 文件的设备驱动程序，可用于将设备驱动程序导入 Deployment Workbench  

-   作为应用程序打包的设备驱动程序，必须作为应用程序进行安装  

 使用 MDT，可将这两种类型的驱动程序作为操作系统部署的一部分进行处理。  

 通过执行以下操作，安装设备驱动程序：  

-   如[确定使用哪种方法来安装设备驱动程序](#WhichMethodtoInstallDriver)中所述，确定安装每个设备驱动程序的方法  

-   如[使用即装即用驱动程序方法安装设备驱动程序](#InstallOutofBoxDrivers)中所述，使用即装即用驱动程序方法  

-   如[以应用程序形式安装设备驱动程序](#InstallDriversasApplications)中所述，将它们安装为应用程序  

 此方案假定部署服务器上正在运行 MDT。  

###  <a name="WhichMethodtoInstallDriver"></a> 确定使用哪种方法来安装设备驱动程序  
 硬件制造商以两种形式之一发布设备驱动程序：  

-   采用包的形式发布，其中包含用于将驱动程序导入 Deployment Workbench 的 .inf 文件，且可供你提取  

-   采用应用程序的形式发布，必须使用传统应用程序安装过程进行安装  

 通过首先将驱动程序导入 Deployment Workbench 中的“即装即用驱动设备”节点，可提取用于访问 .inf 文件的设备驱动程序包可以使用 MDT 自动驱动程序检测和安装过程。  

 如果设备驱动程序包无法提取以隔离 .inf 文件，或在未先使用应用程序安装程序（如 MSI 或 Setup.exe 文件）进行安装的情况下无法正常运行，则它们可使用 MDT 安装应用程序功能，并在部署过程中像安装任何常规应用程序一样安装设备驱动程序。  

###  <a name="InstallOutofBoxDrivers"></a> 使用即装即用设备驱动程序方法安装设备驱动程序  
 可将包含 .inf 文件的设备驱动程序包导入 Deployment Workbench，并将其作为部署过程的一部分自动安装。 若要执行此类设备驱动程序的部署，请首先将设备驱动程序添加到 Deployment Workbench。  

 **将设备驱动程序添加到 Deployment Workbench**  

1.  下载要部署的硬件类型所需的设备驱动程序，并将设备驱动程序包提取到临时位置。  

2.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

3.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Out-of-Box Drivers（其中 deployment_share 是要配置的部署共享的名称）。  

4.  在“操作”窗格中，单击“导入驱动程序”。  

     将启动“导入设备驱动程序向导”。  

5.  在“指定目录”页上的“驱动程序源”目录部分，单击“浏览”，转到包含新设备驱动程序的文件夹，然后单击“下一步”。  

    > [!NOTE]
    >  “新建设备驱动程序向导”将搜索驱动程序源目录的所有子目录，因此，如果要安装多个驱动程序，请将其提取到相同根目录中的文件夹，然后将驱动程序源目录设置为包含所有驱动程序源目录的根目录。  

6.  在“摘要”页，验证设置是否正确，然后单击“下一步”，将驱动程序导入 Deployment Workbench。  

7.  在“确认”页上，单击“完成”。  

 如果设备驱动程序包含启动关键驱动程序（如大容量存储或网络级驱动程序），必须更新部署共享以生成包含新驱动程序的新 LiteTouch_x86 和 LiteTouch_x64 启动环境。  

 **将设备驱动程序添加到 Lite Touch Windows PE 映像**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

4.  在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

5.  在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

6.  在“确认”页上，单击“完成”。  

###  <a name="InstallDriversasApplications"></a> 以应用程序形式安装设备驱动程序  
 对于作为应用程序打包的且无法提取到包含 .inf 文件的文件夹的设备驱动程序，应随驱动程序文件在部署过程中作为应用程序添加到 Deployment Workbench 以便安装。  

 可将应用程序指定为任务序列步骤或在 CustomSettings.ini 中指定；但是，只有在带有设备的计算机上运行任务序列时，才应安装设备驱动程序应用程序。 为了确保这一点，请运行任务序列步骤，将相关设备驱动程序应用程序作为条件任务序列步骤进行部署。 可指定条件标准，对目标计算机上的设备使用 WMI 查询运行任务序列步骤。  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>将设备驱动程序应用程序添加到 Deployment Workbench  
 必须先将每个设备驱动程序应用程序导入到 Deployment Workbench。  

> [!NOTE]
>  通过选中或清除“在部署向导中隐藏此应用程序”复选框，配置部署期间应用程序“属性”对话框上的应用程序是否可见。 为部署期间使用的每个设备驱动程序应用程序重复此过程。  

 **将设备驱动程序应用程序添加到 Deployment Workbench**  

1.  下载设备驱动程序应用程序，并将其保存到临时位置。  

2.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

3.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Applications（其中 deployment_share 是要配置的部署共享的名称）。  

4.  在“操作”窗格中，单击“新建应用程序”。  

     将启动“新建应用程序向导”。  

5.  在“应用程序类型”页上，单击“带有源文件的应用程序”，然后单击“下一步”。  

6.  在“详细信息”页上，键入应用程序的相关详细信息，然后单击“下一步”。  

7.  在“源”页上的“源目录”部分，单击“浏览”，转到相关文件夹，然后单击包含设备驱动程序应用程序源文件的目录。 单击" **确定**"。  

8.  单击“下一步” 。  

9. 在“目标”页，为目标目录键入名称，然后单击“下一步”。  

10. 在“命令详细信息”页上的“命令行”部分中，键入允许无提示安装设备驱动程序应用程序的命令。  

11. 在“摘要”页，验证设置是否正确，然后单击“下一步”，将设备驱动程序应用程序导入 Deployment Workbench。  

12. 在“确认”页上，单击“完成”。  

 将应用程序导入 Deployment Workbench 后，使用适当的逻辑将它们添加到部署过程中，以确保应用程序仅在正确的硬件上运行时才安装。 有不同的方法来实现此目的：  

-   将设备驱动程序应用程序指定为部署任务序列的一部分。  

-   在 CustomSettings.ini 中指定设备驱动程序应用程序。  

-   在 MDT DB 中指定设备驱动程序应用程序。  

 以下各节将更详细地讨论了每种方法。  

####  <a name="SpecifyDeviceAppTask"></a> 将设备驱动程序应用程序指定为任务序列的一部分  
 将设备驱动程序应用程序添加到部署过程的第一种方法是，使用任务序列为每个设备驱动程序应用程序添加步骤。  

 有两种主要方法用于管理任务序列中的设备驱动程序应用程序：  

-   为每个硬件型号创建一个新的任务序列组，然后，如果计算机匹配特定硬件类型，则添加查询以运行这组操作。  

-   为硬件特定的应用程序创建任务序列组，然后为每个任务序列操作添加查询，以便每个任务序列步骤都针对硬件类型进行评估，并且只有在找到匹配项时才会运行。  

 **为每种类型的硬件创建新任务序列组**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在详细信息窗格中，单击“task_sequence”（其中 task_sequence 是安装设备驱动程序应用程序所需的部署任务序列）。  

4.  在“操作”窗格中，单击“属性”。  

5.  在“task_sequenceProperties”对话框中的“任务序列”选项卡上，在详细信息窗格中，转到 State Restore/Windows Update（应用程序预安装）。  

6.  在“任务序列”选项卡上，单击“添加”，然后单击“新建组”。  

     此操作将在任务序列中创建新任务序列组。 使用此新的任务序列组创建步骤，用于安装特定于硬件的设备驱动程序应用程序。  

7.  在详细信息窗格中，单击“新建组”。  

8.  在“属性”选项卡上的“名称”框中，键入“group_name”（其中 group_name 是组名，例如 特定于硬件的应用程序 - Dell Computer Corporation）。  

9. 在“选项”选项卡上，单击“添加”，然后单击“查询 WMI”。  

10. 在“任务序列 WMI 条件”对话框中，键入以下详细信息：  

    -   在“WMI 命名空间”框中，键入“root\cimv2”。  

    -   在“WQL 查询”框中，使用 Win32_ComputerSystem 类键入 WMI 查询语言 (WQL) 查询，确保仅为特定应用程序类型安装此应用程序，例如：  

         Select \* FROM Win32_ComputerSystem WHERE Model LIKE %hardware_model% AND Manufacturer LIKE *%hardware_manufacturer%*  

         在此示例中，hardware_model 是计算机型号的名称（如 Latitude D620），hardware_manufacturer 是计算机品牌（如 Dell Corporation）。  

         % 符号是包含在名称中的通配符，允许管理员返回包含 hardware_model 或 hardware_manufacturer 的指定值的任何计算机型号或制造商。  

     有关 WMI 和 WQL 查询的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“将 WMI 查询添加到任务序列步骤条件”部分，并且参阅[使用 WQL 查询](http://msdn.microsoft.com/library/aa392902.aspx)。  

11. 单击“确定”提交查询，然后单击“确定”将更改提交到任务序列。  

> [!NOTE]
>  必须为每个要安装的设备驱动程序应用程序的每种硬件类型重复此过程。  

 在已创建硬件特定的任务序列组之后，可将设备驱动程序应用程序添加到每个组中。  

 **将设备驱动程序应用程序添加到硬件特定的任务序列组**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在详细信息窗格中，单击“task_sequence”（其中 task_sequence 是安装设备驱动程序应用程序所需的部署任务序列）。  

4.  在“操作”窗格中，单击“属性”。  

5.  在“task_sequenceProperties”对话框中，单击“任务序列”选项卡。  

6.  在详细信息窗格中，转到 State Restore/hardware_specific_group（其中 hardware_specific_group 是硬件特定的组的名称，将在此添加任务序列步骤以安装设备驱动程序应用程序）。  

7.  在“任务序列”选项卡上，单击“添加”、“常规”，然后单击“安装应用程序”。  

     “安装应用程序”任务序列步骤将出现在详细信息窗格中。  

8.  在详细信息窗格中，单击“安装应用程序”。  

9. 在“属性”选项卡上，单击“安装单个应用程序”，并在“要安装的应用程序”列表中，选择“hardware_application”（其中 hardware_application 是用于安装硬件特定的应用程序的应用程序）。  

> [!NOTE]
>  必须在部署期间，为每个需要使用的设备驱动程序应用程序重复此过程。  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>在 CustomSettings.ini 中指定设备驱动程序应用程序  
 当 LTI 或 ZTI 部署开始时，要完成的第一个操作之一是 BootStrap.ini 和 CustomSettings.ini 控件文件处理。 这两个文件都包含可用于动态定制部署的规则。  

 由于 MDT 处理 CustomSettings.ini 文件的方式，可使用它来根据特定条件添加应用程序。 此逻辑将用于在部署期间根据特定硬件类型添加设备驱动程序特定的应用程序。 应用程序的 GUID 在 CustomSettings.ini 中引用应用程序，GUID 位于部署共享中的 Applications.xml 文件中。  

 **查找导入的应用程序的 GUID**  

1.  在部署服务器的部署共享中，打开 Control 文件夹 - 例如 D:\Production Deployment Share\Control。  

2.  查找并打开 Applications.xml 文件。  

3.  查找所需的应用程序。  

4.  通过查找应用程序 `<guid>` 标记中包含的行，确定应用程序 GUID，例如 `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`。  

 作为初始化过程的一部分，LTI 和 ZTI 过程均收集它们在其中运行的计算机的相关信息。 作为此过程的一部分，将执行 WMI 查询，并将用于品牌和制造商的 Win32_ComputerSystem 类的值分别填充为变量 %Make% 和 %Model%。  

 这些值可在处理 CustomSettings.ini 文件期间根据检测到的品牌和型号动态读取文件的各个部分。  以下示例显示了 CustomSettings.ini 文件的示例。  

 **为硬件特定的应用程序安装配置的 CustomSettings.ini 示例**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 使用以下属性来指定 CustomSettings.ini 中的应用程序：  

-   **Applications**。 通过在 CustomSettings.ini 中指定 SkipApplications=YES，部署管理员不想在部署过程中显示应用程序向导时，可使用此属性。  

-   **MandatoryApplications**。 如果部署管理员想在部署过程中显示应用程序向导，使部署工程师可选择在部署期间安装其他应用程序，则可使用此属性。  

     如果在没有 MandatoryApplications 属性的情况下（例如 SkipApplications=NO）使用应用程序向导，将覆盖 Applications 属性指定的应用程序。  

     以上示例展示了如何使用 %Make% 和 %Model% 变量值，动态操作应用程序列表的生成方式。 可使用以下方法之一来查找每种类型硬件的品牌和型号的值：  

-   **系统信息工具**。 使用此工具中“系统摘要”节点，确定系统制造商（品牌）和系统型号（型号）。  

-   **Windows PowerShell**。 使用 Get-WMIObject –class Win32_ComputerSystem cmdlet 来确定计算机的品牌和型号。  

-   **Windows Management Instrumentation 命令行**。 使用 CSProduct Get Name, Vendor 返回计算机的名称（型号）和供应商（品牌）。  

 **修改 CustomSettings.ini 以添加硬件特定的逻辑**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  单击“规则”选项卡。  

5.  将此选项卡上键入的信息存储在 CustomSettings.ini 文件中。 如[将设备驱动程序应用程序指定为任务序列的一部分](#SpecifyDeviceAppTask)中所述，修改 CustomSettings.ini 文件条目，为每个带有设备驱动程序的硬件型号添加逻辑。  

6.  单击“确定”，提交所做的更改。  

7.  在详细信息窗格中，单击“deployment_share”（其中 deployment_share 是要配置的部署共享的名称）。  

8.  在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

9. 在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

10. 在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

11. 在“确认”页上，单击“完成”。  

 默认情况下，在 LTI 部署期间，所有可用的应用程序都显示在 Windows 部署向导中。 由于设备驱动程序特定的应用程序仅适用于特定的硬件类型，建议不要始终显示它们。 通过在 CustomSettings.ini 中指定设备驱动程序特定的应用程序包，可在应用程序配置中使用“在部署向导中隐藏此应用程序”选项来隐藏应用程序。  

 **在部署向导中隐藏应用程序**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Applications（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在详细信息窗格中，单击“device_driver_application”（其中 device_driver_application 是要从部署向导中隐藏的应用程序）。  

4.  在“操作”窗格中，单击“属性”。  

5.  在“常规”选项卡上，选中“在部署向导中隐藏此应用程序”复选框。  

6.  单击“应用”，然后关闭“属性”对话框。  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>在 MDT DB 中指定设备驱动程序应用程序  
 MDT DB 是 CustomSettings.ini 文件的数据库版本，可在部署时查询它获取部署期间要使用的信息。 有关使用 MDT DB 的详细信息，请参阅“选择应用配置设置的方法”。  

 在部署时查询 MDT DB 时，有三种方法可用于识别目标计算机：  

-   搜索个人计算机（使用 MAC 地址、资产标记或类似信息）。  

-   搜索计算机的位置（使用默认网关）。  

-   搜索计算机的品牌和型号（使用 WMI 制造商或品牌和型号查询）。  

 对于你创建的每个数据库条目，可指定部署属性、应用程序、管理员，以及是否使用 Configuration Manager 包。 通过在数据库中创建品牌和型号条目，可添加硬件特定的必需设备驱动程序应用程序。  

 **在 MDT DB 中创建条目以允许安装设备驱动程序应用程序**  

> [!NOTE]
>  对需要设备驱动程序应用程序的每个硬件品牌和型号重复此过程。  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Workbench/Deployment Shares/deployment_share/Advanced Configuration/Database/Make and Model（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“新建”。  

4.  在“属性”对话框中的“标识”选项卡上，在“品牌”框中，键入“make_name”（其中 make_name 是可轻松识别的名称，与目标计算机的制造商相关联）。  

5.  在“品牌”框中，键入“model_name”（其中 model_name 是可轻松识别的名称，与目标计算机的型号相关联）。  

6.  在“应用程序”选项卡上，添加该型号硬件所需的每个设备驱动程序应用程序。  

## <a name="initiating-mdt-using-windows-deployment-services"></a>使用 Windows 部署服务启动 MDT  
 Windows Server 2008 使用 Windows 部署服务作为远程安装服务的更新和重新设计版本，这是 Windows Server 2003 SP2 中的默认部署工具。 通过 Windows 部署服务，可使用计算机启用了 PXE 的网络适配器或启动介质，在网络上部署 Windows 操作系统 - 尤其是 Windows 7、Windows Server 2008 或更高版本的操作系统。  

 在部署 Windows 部署服务之前，确定以下哪种集成选项最适合你的环境：  

-   选项 1. 在 PXE 中引导计算机以启动 LTI 过程。  

-   选项 2. 从 Windows 部署服务映像存储中部署操作系统映像。  

-   选项 3. 对 MDT 和 Windows Server 2008 Windows 部署服务服务器角色使用多播。  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>选项 1：引导 PXE 中的计算机以启动 LTI 过程  
 通过使用 Windows 部署服务和动态主机配置协议启动 MDT 部署过程，帮助最大限度地降低管理操作系统部署的成本。 这消除了为每台目标计算机创建和传送可启动介质的需求。  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>创建 Deployment Workbench Windows PE 映像并将其导入 Windows 部署服务  
 创建新 MDT 部署共享或修改现有 MDT 部署共享时，可创建自定义的 Windows PE 启动映像。 更新部署共享时，Windows PE 启动映像将自动生成并更新有关部署共享的信息，也将注入部署共享配置期间指定的任何其他驱动程序或组件。  

 Windows PE 启动映像既可以作为可写入 CD 或 DVD 的 ISO 映像文件生成，也可以作为可启动的 WIM 文件生成。 可将 WIM 文件导入 Windows 部署服务，因此可在 PXE 中引导的计算机可以在用于初始化安装的网络上下载和运行 LTI Windows PE 启动映像。  

 **在 Deployment Workbench 中创建可启动 Windows PE 映像**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

     在“deployment_shareProperties”对话框中，单击“Windows PE platform 设置”选项卡（其中 platform 是要配置的 Windows PE 映像的体系结构）。  

4.  在“Lite Touch 启动映像设置”区域中，选中“生成 Lite Touch 可启动 RAM 磁盘 ISO 映像”复选框。  

5.  单击“Windows PE platform 组件”选项卡（其中 platform 是要配置的 Windows PE 映像的体系结构）。  

6.  在“驱动程序注入”部分，单击要包括的适当的驱动程序类型。  

    > [!NOTE]
    >  如果 Windows PE 已包含必要的设备驱动程序，则无需执行此步骤。  

7.  在“驱动程序注入”部分的“选择配置文件”列表中，选择适当的驱动器选择配置文件。  

8.  在“属性”对话框中，单击“确定”。  

    > [!NOTE]
    >  如果 Windows PE 已包含必要的设备驱动程序，则无需执行此步骤。  

9. 在详细信息窗格中，单击“deployment_share”（其中 deployment_share 是要配置的部署共享的名称）。  

10. 在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

11. 在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

12. 在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

13. 在“确认”页上，单击“完成”。  

     此过程完成后，部署共享中的 Boot 文件夹将包含许多启动映像 - 例如：  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 可以将已生成的 ISO 文件直接写入 CD 或 DVD，或使用它们在新硬件上初始化 LTI 过程。 还可将引导 WIM 文件导入到 Windows 部署服务，以便新计算机可以在不需要任何物理介质的情况下初始化 LTI 部署过程。  

 **将 Windows PE 导入到 Windows 部署服务**  

1.  启动 Windows 部署服务控制台，然后连接到 Windows 部署服务。  

2.  在控制台树种，右键单击“启动映像”，然后单击“添加启动映像”。  

3.  浏览到要导入的 WIM 映像，例如 D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim。  

4.  导入过程会自动读取启动映像中的元数据，但也可编辑“映像名称”和“映像描述”值；“映像名称”会影响客户端在 PXE 中启动时 Windows 引导管理器显示的启动选项信息。  

5.  导入启动映像后，任何以 PXE 引导并从 Windows 部署服务收到回复的计算机都将能够下载 LTI 启动映像并启动 LTI 安装。  

 本指南中未涵盖安装和配置 Windows 部署服务。 有关 Windows 部署服务的其他信息，请参阅 [Windows 部署服务指南](http://technet.microsoft.com/library/cc265612.aspx)。  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>使用 Windows 部署服务自动检测部署服务器  
 如果 MDT 部署共享托管在与 Windows 部署服务相同的服务器上，使用 Windows 部署服务托管 MDT 启动映像时可以使用其他选项。  

 当 PXE 客户端加载 MDT 启动映像时，将捕获托管启动映像的 Windows 部署服务服务器的名称并将其放置于 MDTProperty WDSServer 中。 然后，可通过“DeployRoot”属性在启动映像的 BootStrap.ini 文件和部署共享的 CustomSettings.ini 文件中引用此属性。 此操作会导致一个使用 Windows 部署服务服务器上托管的部署共享从 Windows 部署服务自动启动的客户端。 这消除了在任何配置文件中指定服务器名称的需要。  

 **设置本地 Windows 部署服务作为部署共享**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Advanced Configuration/Database（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  单击“规则”选项卡。  

     将此选项卡上键入的信息存储在 CustomSettings.ini 文件中。  

5.  配置“DeployRoot”属性以使用 %WDSServer% 变量，例如 DeployRoot=\\\\%WDSServer%\Deployment$。  

6.  单击“编辑 Bootstrap.ini”。  

7.  通过添加“DeployRoot”值或将其更改为“DeployRoot=\\\\%WDSServer%\Deployment$”，配置 BootStrap.ini 以使用“%WDSServer%”属性。  

8.  在“文件”菜单上，单击“保存”，保存对 BootStrap.ini 文件所做的更改。  

9. 单击" **确定**"。  

     需要更新部署共享。  

10. 在详细信息窗格中，单击“deployment_share”（其中 deployment_share 是要配置的部署共享的名称）。  

11. 在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

12. 在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

13. 在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

14. 在“确认”页上，单击“完成”。  

15. 将更新的引导 WIM 导入Windows 部署服务。  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>选项2：从 Windows 部署服务存储区部署操作系统映像  
 如果已使用 Windows 部署服务进行操作系统部署，则通过配置 MDT 以引用已使用中的 Windows 部署服务操作系统映像，而非使用 MDT 自己的存储来展开 MDT 的功能，并使用驱动程序管理、应用程序部署、更新安装、规则处理和其他 MDT 功能对 Windows 部署服务包署进行补充。 在 MDT 引用 Windows 部署服务操作系统映像之后，可像处理已转移到 MDT 部署共享的任何操作系统一样处理它。  

 **引用 Windows 部署服务操作系统映像**  

> [!NOTE]
>  以下步骤要求至少有一个操作系统映像先前已导入 Windows 部署服务服务器。  

1.  通过将 Windows 介质的 Sources 文件夹中的以下文件复制到 Windows 部署服务服务器上的 C:\Program Files\Microsoft Deployment Toolkit\bin 文件夹来更新 MDT，以便能够访问 Windows 部署服务映像：  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll（仅适用于从 Windows Server 2008 源目录进行复制的情况）  

    > [!NOTE]
    >  正在使用的 Windows 源目录必须与安装 MDT 的计算机上运行的操作系统的平台相匹配。  

2.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

3.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Operating Systems（其中 deployment_share 是要配置的部署共享的名称）。  

4.  在“操作”窗格中，单击“导入操作系统”。  

     将启动“新建操作系统向导”。  

5.  在“操作系统类型”页上，单击“Windows 部署服务映像”，然后单击“下一步”。  

6.  在“WDS 服务器”页上，键入要引用的 Windows 部署服务服务器的名称，例如 WDSSvr001，然后单击“下一步”。  

7.  在“摘要”页上，验证设置是否正确，然后单击“下一步”。  

8.  在“确认”页上，单击“完成”。  

     Windows 部署服务服务器上提供的所有映像现在都可用于 MDT 任务序列。  

> [!NOTE]
>  从 Windows 部署服务导入映像不会将源文件从 Windows 部署服务服务器复制到部署共享。 MDT 继续从源文件的原始位置使用源文件。  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>选项 3：对 MDT 和 Windows Server 2008 Windows 部署服务服务器角色使用多播  
 随着 Windows Server 2008 的发布，增强了 Windows 部署服务以支持使用多播传输部署映像。 MDT 还包括将 MDT 与 Windows 部署服务多播集成的更新。  

 另外，更新的 Windows 自动安装工具包 (Windows AIK) 1.1 版包含 Wdsmcast.exe。 可手动联接多播会话，并允许客户端启动 Wdsmcast.exe 从活动的多播会话中复制文件。  

 LTIApply.wsf 脚本从部署共享访问操作系统源文件时使用 Wdsmcast.exe。 根据正在运行的 Windows PE 版本，LTIApply.wsf 在 deployment_share\Tools\x86 文件夹或 the deployment_share\Tools\x64 文件夹（其中 deployment_share 是包含部署共享的文件系统文件夹的名称）中的部署共享上查找 Wdsmcast.exe。  

 LTIApply.wsf 运行时，它总是尝试从现有的多播流中访问和下载 WIM 映像，但如果多播流不存在，它将回退到标准文件副本。  

> [!NOTE]
>  此过程仅适用于 WIM 映像文件。  

 准备 MDT 多播的部署服务器先决条件是：  

-   部署服务器必须运行 Windows Server 2008 或更高版本  

-   必须从服务器管理控制台安装 Windows 部署服务角色  

-   必须安装 Windows AIK 1.1 for Windows Server 2008  

-   必须安装 MDT  

-   与使用 MDT 的任何部署一样，必须至少已导入一个操作系统 WIM 映像，既可以完整源文件集的形式，也可以带有安装文件的自定义映像的形式  

> [!NOTE]
>  使用最新版本的 Windows AIK 进行多播非常重要；早期版本的 Windows AIK 中包含的 Windows PE 副本（例如 Windows AIK 1.0）不支持从多播服务器进行下载。  

 **从现有部署共享配置 MDT 进行多播**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share（其中 deployment_share 是要配置的部署共享的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  在“常规”选项卡上，选中“为此部署共享启用多播(需要 Windows Server 2008 Windows 部署服务)”复选框。  

5.  单击" **确定**"。  

6.  在“操作”窗格中，单击“更新部署共享”。  

     将启动“更新部署共享向导”。  

7.  在“选项”页上，选择用于更新部署共享的所需选项，然后单击“下一步”。  

8.  在“摘要”页上，验证详细信息是否正确，然后单击“下一步”。  

9. 在“确认”页上，单击“完成”。  

 现在为 Windows 部署服务多播传输配置了部署共享。  

 此过程将创建一个直接使用现有 MDT 部署共享的 Auto-Cast Windows 部署服务多播传输。 MDT 不创建 Scheduled-Cast 传输。 另请注意，没有其他映像导入到 Windows 部署服务中，并且无法将多播用于启动映像，因为多播客户端在 Windows PE 运行之后才能加载。  

 **验证 Windows 部署服务中是否已生成多播传输**  

1.  单击“开始”，指向“管理工具”，然后单击“Windows 部署服务”。  

2.  在 Windows 部署服务控制台树中，右键单击“服务器”，然后单击“添加服务器”。  

3.  在“添加服务器”对话框中，单击“本地计算机”，然后单击“确定”。  

4.  在 Windows 部署服务控制台树种，单击“服务”，然后单击“server_name”（其中 server_name 是运行 Windows 部署服务的计算机的名称）。 单击“多播传输”。  

5.  在详细信息窗格中，将列出部署共享的新 Auto-Cast 传输，例如 BDD Share Deployment$。  

6.  验证 BDD Share Deployment$ Auto-Cast 传输的状态是否设置为“活动”。  

 计算机部署完成后，通过检查 \Windows\Temp\DeploymentLogs 文件夹中的 BDD.log 文件来验证操作系统是否已从多播传输下载。  

 日志文件夹中将有两个条目，均以“Multicast transfer”开头；检查它们以验证传输是否成功。 有关 MDT 和 Windows 部署服务中的多播传输的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中“为 LTI 部署启用 Windows 部署服务多播部署”部分。  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>使用 MDT 执行预留部署（OEM 预加载）  
 在许多组织中，在部署到生产网络之前都会通过操作系统映像加载计算机。 在某些情况下，由组织内负责在过渡环境中构建计算机的团队执行加载操作系统映像操作。 在其他情况下，加载操作系统映像由计算机硬件供应商（也称为原始设备制造商 (OEM)）执行。  

> [!NOTE]
>  只有在使用 LTI 执行部署时，MDT 中才支持 OEM 预加载过程。 对于Configuration Manager，请使用预留介质功能。  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>MDT 中的 OEM 预加载过程概述  
 OEM 预加载过程分为三个阶段：  

-   **阶段 1**。 创建要在过渡环境中应用的引用计算机的基于介质的映像。  

-   **阶段 2**。 在过渡环境中将引用计算机映像应用于目标计算机。  

-   **阶段 3**。 在生产环境中完成目标计算机的部署。  

 阶段 1 和阶段 3 通常由部署组织执行。 根据组织中 OEM 预加载过程的使用情况，阶段 2 可由组织或供应计算机的计算机硬件供应商执行。 如果组织执行阶段 2，则过渡环境位于组织内。 如果 OEM 执行阶段 2，则过渡环境位于 OEM 的环境中。  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>OEM 预加载过程中的 MDT 配置文件概述  
 单独的 MDT 配置文件 (CustomSettings.ini and Bootstrap.ini) 由任务序列运行在 OEM 预加载过程的阶段 1 和阶段 3 期间使用。 但是，两个配置文件同时存在于不同的文件夹结构中。  

 在第一阶段中，创建引用计算机期间使用配置文件，并将其存储在特定于该阶段中使用的任务序列的文件夹中。 OEM 预加载过程的第三个阶段和最后一个阶段中使用的配置文件存储在特定于该阶段中使用的任务序列的文件夹中。  

 在对配置文件进行修改时，请确保该修改对应于每个 OEM 预加载过程阶段中相应的任务序列。  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>OEM 预加载过程中的 MDT 日志文件概述  
 在 OEM 预加载过程的阶段 1 和阶段 3 期间生成单独的 MDT 日志文件：  

-   阶段 1 的 MDT 日志文件存储在 C:\MININT 和 C:\SMSTSLog 文件夹中。  

-   阶段 3 的 MDT 日志文件存储在 %WINDIR%\System32\CCM\Logs 文件夹中（针对基于 x86 的部署），或存储在 %WINDIR%\SysWow64\CCM\Logs 文件夹中（针对基于 x64 的部署）。  

 诊断或故障排除与 MDT 相关的部署问题时，请使用适当的文件夹。  

### <a name="staged-deployments-using-lti"></a>使用 LTI 的预留部署  
 对于 LTI 部署，使用可移动介质 (Media) 部署共享类型执行 OEM 预加载过程。 OEM 预加载过程不支持其他部署共享类型。  

 若要执行 OEM 预加载过程，除了将用于部署目标操作系统的任何任务序列外，还应根据 Litetouch OEM Task Sequence 任务序列模板创建任务序列。 然后，创建一个可移动介质 (Media) 部署共享，最终将创建部署共享内容的 ISO 文件，尤其是 LiteTouchPE_x86.iso 文件或 LiteTouchPE_x64.iso 文件（基于目标计算机的处理器平台）。 部署共享更新过程还会创建可用于创建通用磁盘格式介质的文件夹结构。  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>LTI OEM 预加载过程 - 阶段 1：创建基于介质的映像  
 部署组织在 OEM 预加载过程中执行第一阶段。 此阶段的最终可交付结果是发送到 OEM 或部署组织内过渡环境的可启动映像（如 ISO 文件）或介质（如 DVD）。 大部分步骤都在 Deployment Workbench 中执行。  

 **创建基于介质的映像，以便将其交付到 OEM 或部署组织内的过渡环境**  

1.  在 Deployment Workbench 中填充部署共享的以下节点：  

    -   操作系统  

    -   应用程序  

    -   包  

    -   即装即用驱动程序  

     有关执行此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中管理部署共享”部分。  

2.  根据 Deployment Workbench 中的“Litetouch OEM 任务序列”任务序列模板创建新的任务序列。  

     有关执行此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置任务序列”部分。  

3.  在生产环境中部署后，创建一个或多个用于在目标计算机上部署目标操作系统的任务序列。  

     有关执行此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“在 Deployment Workbench 中配置任务序列”部分。  

4.  创建一个选择配置文件，其中包含 OEM 部署所需的应用程序、操作系统、驱动程序、包和任务序列。  

     有关执行此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“管理选择配置文件”部分。  

5.  创建部署介质。  

     有关执行此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“管理 LTI 部署介质”部分。  

6.  更新上一步在 Deployment Workbench 中创建的部署介质。  

     更新部署介质时，Deployment Workbench 会创建 LiteTouchMedia.iso 文件。 有关执行此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“管理 LTI 部署介质”部分。  

7.  刻录上一步中创建的 LiteTouchMedia.iso 文件的 DVD。  

    > [!NOTE]
    >  如果将 ISO 文件交付到 OEM 或组织的过渡环境，则无需操作此步骤。  

8.  将 ISO 文件或 DVD 交付给 OEM 或组织的过渡环境。  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>LTI OEM 预加载过程 - 阶段 2：将映像应用到目标计算机  
 OEM 预加载过程的第二阶段由 OEM 或由部署团队在部署组织的过渡环境中执行。 在此过程的这一阶段，阶段 1 中创建的 .iso 文件或 DVD 应用于目标计算机。 此阶段的可交付结果是部署在目标计算机上的映像，以便它们转备好在生产环境中部署。  

 **将映像应用于目标计算机**  

1.  使用在阶段 1 中创建的映像启动目标计算机。  

     将启动 Windows PE，然后启动 Windows 部署向导。  

2.  在 Windows 部署向导中，单击“过渡环境的 OEM 预安装任务序列”任务序列。  

     任务序列将启动并且将可启动介质的内容复制到目标计算机的本地硬盘。  

3.  完成“过渡环境的 OEM 预安装任务序列”任务序列的 Windows 部署向导时，通过为用于部署操作系统的其他任务序列运行 Windows 部署向导，硬盘将准备好启动部署过程的其余部分。  

     “过渡环境的 OEM 预安装任务序列”任务序列负责将映像部署到目标计算机并启动 LTI 过程。 Windows 部署向导将再次启动以运行用于在目标计算机上部署操作系统的任务序列。  

4.  根据需要将第一个硬盘的内容克隆到过渡环境中的众多目标计算机。  

5.  将目标计算机交付到生产环境进行部署。  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>LTI OEM 预加载过程 - 阶段 3：完成目标计算机部署  
 OEM 预加载过程的第三个也是最后一个阶段是在部署组织的生产环境中执行的。 在这一阶段内，启动目标计算机，上一阶段内放置在过渡环境中的硬盘上的可启动介质映像将启动。  

 **在生产环境中完成目标计算机的部署**  

1.  启动目标计算机。  

     将启动 Windows PE，然后启动 Windows 部署向导。  

2.  使用每台目标计算机的特定配置信息完成 Windows 部署向导。  

     有关完成此步骤的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“运行部署向导”部分。  

 当这个阶段完成时，目标计算机将准备好在生产环境中使用。  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>使用 Windows PowerShell 执行常见任务  
 Deployment Workbench 中的 MDT 管理任务由基础 Windows PowerShell cmdlet 执行，可用其来自动执行管理任务，例如以下各节中的管理任务。  

 可执行以下步骤来自动执行 MDT 管理：  

-   按照[创建新部署共享](#CreateNewDeployShare)中所述，创建新的部署共享。  

-   如[创建文件夹](#CreateFolder)中所述，在部署共享中创建文件夹。  

-   如[删除文件夹](#DeleteFolder)中所述，从部署共享中删除文件夹。  

-   如[导入设备驱动程序](#ImportDeviceDriver)中所述，将设备驱动程序导入部署共享。  

-   如[删除设备驱动程序](#DeleteDeviceDriver)中所述，从部署共享中删除设备驱动程序。  

-   如[导入操作系统包](#ImportOpSysPackage)中所述，将操作系统包导入部署共享。  

-   如[删除操作系统包](#DeleteOpSysPackage)中所述，从部署共享删除操作系统包。  

-   如[导入操作系统](#ImportOpSys)中所述，将操作系统导入部署共享。  

-   如[删除操作系统](#DeleteOpSys)中所述，从部署共享删除操作系统。  

-   如[创建应用程序](#CreateApplication)中所述，在部署共享中创建应用程序。  

-   如[删除应用程序](#DeleteApplication)中所述，从部署共享删除应用程序。  

-   如[创建任务序列](#CreateTaskSequence)中所述，在部署共享中创建任务序列。  

-   如[删除任务序列](#DeleteTaskSequence)中所述，从部署共享删除任务序列。  

-   如[创建 MDT DB](#CreateMDTDB) 中所述，创建 MDT DB。  

-   如[创建选择配置文件](#CreateSelectProfile)中所述，创建选择配置文件。  

-   如[更新部署共享](#UpdatingDeployShare)中所述，更新部署共享。  

-   如[创建链接的部署共享](#CreateLinkedDeployShare)中所述，创建链接的部署共享。  

-   如[更新链接的部署共享](#UpdatingLinkedDeployShare)中所述，更新链接的部署共享。  

-   如[删除链接的部署共享](#DeleteLinkedDeployShare)中所述，删除链接的部署共享。  

-   如[创建介质](#CreateMedia)中的所述，创建部署介质。  

-   如[生成介质](#GenerateMedia)中所述，生成部署介质。  

-   如[删除介质](#DeleteMedia)中所述，删除部署介质。  

###  <a name="CreateNewDeployShare"></a> 创建新部署共享  
 以下 Windows PowerShell 命令在 D:\Production Deployment Share 上创建名为“Production$”的新部署共享。 新的部署共享将在 Deployment Workbench 中显示为 Production。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> 创建文件夹  
 以下 Windows PowerShell 命令在 Deployment Workbench\/Deployment Shares\/Production\/Applications 的 Deployment Workbench 控制台树中创建一个 Adobe 文件夹。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  将“`remove-psdrive`”添加到脚本，确保在后台进程在处理之前结束。  

###  <a name="DeleteFolder"></a> 删除文件夹  
 以下 Windows PowerShell 命令删除 Deployment Workbench\/Deployment Shares\/Production\/Applications\/Adobe 文件夹。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  如果文件夹为空，脚本将失败。  

###  <a name="ImportDeviceDriver"></a> 导入设备驱动程序  
 以下 Windows PowerShell 命令会将 Dell 2407 WFP 监视器设备驱动程序导入 Production 部署共享。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> 删除设备驱动程序  
 以下 Windows PowerShell 命令从 Production 部署共享删除 Dell 2407 WFP 监视器驱动程序。  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> 导入操作系统包  
 以下 Windows PowerShell 命令导入位于 D:\\Updates\\Microsoft\\Vista 下的所有操作系统包。 这些操作系统包将存储在位于 D:\\Production Deployment Share 中的 Production 部署共享。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> 删除操作系统包  
 以下 Windows PowerShell 命令从 Production 部署共享删除指定的操作系统包。  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> 导入操作系统  
 以下 Windows PowerShell 命令导入位于 D:\\Operating Systems\\Windows Vista x86 中的 Windows Vista 操作系统。 操作系统将存储在位于 D:\\Production Deployment Share 中的 Production 部署共享。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> 删除操作系统  
 以下 Windows PowerShell 命令从 Production 部署共享删除 Windows Vista HOMEBASIC 操作系统。  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> 创建应用程序  
 以下 Windows PowerShell 命令使用 D:\\Software\\Adobe\\Reader 9 中的源文件，创建 Adobe Reader 9 应用程序。 应用程序将存储在位于 D:\\Production Deployment Share 中的 Production 部署共享。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> 删除应用程序  
 以下 Windows PowerShell 命令从 Production 部署共享删除 Adobe Reader 9 应用程序。  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> 创建任务序列  
 以下 Windows PowerShell 命令在位于 D:\\Production Deployment Share 的 Production 部署共享中创建“Windows Vista 生产版本”任务序列。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> 删除任务序列  
 以下 Windows PowerShell 命令从 Production 部署共享删除“Windows Vista 生产版本”任务序列。  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> 创建 MDT DB  
 以下 Windows PowerShell 命令在 Production 部署共享的 deployment\_server 服务器上创建新 MDT DB。 将通过 TCP\/IP 进行数据库连接。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> 创建选择配置文件  
 以下 Windows PowerShell 命令创建新的 Applications 选择配置文件。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> 更新部署共享  
 以下 Windows PowerShell 命令更新位于D:\\Production Deployment Share 中的 Production 部署共享。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> 创建链接的部署共享  
 以下 Windows PowerShell 命令创建链接到 Production 部署共享的部署共享，并位于 \\\\*remote\_server\_name*\\Deployment$ share 下。 Everything 选择配置文件用于确定将哪些内容复制到链接的部署共享。 Production 部署共享中的内容将与已存在于 \\\\*remote\_server\_name*\\Deployment$ share 中的内容合并。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> 更新链接的部署共享  
 以下 Windows PowerShell 命令更新 LINKED001 部署共享。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> 删除链接的部署共享  
 以下 Windows PowerShell 命令删除 LINKED001 部署共享。  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> 创建介质  
 以下 Windows PowerShell 命令创建包含用于创建可启动介质的内容的源文件夹。 Production 部署共享将用作源。 Everything 选择配置文件确定将什么内容放置在介质内容文件夹中。 LiteTouchMedia.iso 文件将在介质生成时创建。 介质将支持 x86 和 x64 平台。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> 生成介质  
 以下 Windows PowerShell 命令在 D:\\Media 中创建 LiteTouchMedia.iso 文件，可使用 MEDIA001 介质源文件夹中的内容。  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> 删除介质  
 以下 Windows PowerShell 命令从 Production 部署共享中删除 MEDIA001 介质。  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>延迟域联接以避免应用组策略对象  
 组策略是一种丰富而灵活的技术，通过集中式的一对多模型提供高效管理大量 Active Directory 域服务 (AD DS) 计算机和用户对象的功能。 组策略设置包含在组策略对象 (GPO) 中并链接到一个或多个 AD DS 服务容器 - 站点、域和组织单位 (OU)。  

 某些组织具有限制性的组策略设置，并可能在操作系统部署期间造成问题。 例如，以下组策略设置可能会中断自动登录过程：  

-   自动登录限制  

-   管理员帐户重命名  

-   法律横幅和标题栏  

-   限制性安全策略（例如，专用安全限制功能 [SSLF] 策略）  

 克服部署过程中 GPO 可能导致的问题的一种方法是，在部署过程中尽可能晚地将计算机联接到域。 可使用运行 ZTIDomainJoin.wsf 脚本的自定义任务序列步骤完成此联接。  

 若要将目标计算机联接到域，ZTIDomainJoin.wsf 脚本使用 DomainAdmin、DomainAdminDomain、DomainAdminPassword、JoinDomain 和 MachineObjectOU 属性。 可使用 Windows 部署向导、部署共享规则、MDT DB 以及 Configuration Manager 计算机和收集规则来声明这些属性。 使用的帐户必须具有在域中创建和删除计算机对象所需的权限。  

 通常，ZTIConfigure.wsf 脚本使用这些属性指定的值更新 Unattend.xml 或 Unattend.txt 文件。 然后，Windows 安装程序分析这些设置，系统尝试在部署过程早期联接到域。 此操作可让目标计算机服从域 GPO 中指定的设置，并可能导致部署过程失败。  

 若要在部署过程中有意延迟将目标计算机联接到域，可从 Unattend.xml 文件删除某些元素。 如果文件中缺少相关的属性元素，则 ZTIConfigure.wsf 脚本将跳过将属性写入 Unattend.xml 文件的步骤。  

> [!NOTE]
>  此解决方法示例仅在部署 Windows 7、Windows Server 2008 或 Windows Server 2008 R2 操作系统时有效。  

 **准备 unattend.xml 文件，以便目标计算机在 Windows 安装过程中不尝试加入域**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences/task_sequence（其中 deployment_share 是要配置的部署共享的名称，task_sequence 是要配置的任务序列的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  在“操作系统信息”选项卡上，单击“编辑 Unattend.xml”。  

     将启动 Windows 系统映像管理器 (Windows SIM)。  

5.  在“答案文件”窗格中，转到 4 specialize/Identification/Credentials。 右键单击“凭据”，然后单击“删除”。  

6.  单击“是” 。  

7.  保存答案文件，然后退出 Windows SIM。  

8.  在任务序列“属性”对话框上单击“确定”。  

 由于 unattend.xml 文件中缺少 `Credentials` 元素，ZTIConfigure.wsf 脚本无法填充 Unattend.xml 文件中的域加入信息，这将阻止 Windows 安装程序尝试加入域。  

 **添加将目标计算机联接到域的任务序列步骤**  

1.  单击“开始”，然后指向“所有程序”。 指向“Microsoft Deployment Toolkit”，然后单击“Deployment Workbench”。  

2.  在 Deployment Workbench 控制台树中，转到 Deployment Workbench/Deployment Shares/deployment_share/Task Sequences/task_sequence（其中 deployment_share 是要配置的部署共享的名称，task_sequence 是要配置的任务序列的名称）。  

3.  在“操作”窗格中，单击“属性”。  

4.  在“任务序列”选项卡上，转到并展开“状态还原”节点。  

5.  验证是否存在“从域中恢复”任务序列步骤。 如果是，继续执行步骤 9。  

6.  在任务序列“属性”对话框中，单击“添加”，转到“设置”，然后单击“从域中恢复”。  

7.  将“从域中恢复”任务序列步骤添加到任务序列编辑器。 验证步骤是否处于任务序列中所需的位置。  

8.  验证是否已按需求配置“从域中恢复”任务序列步骤的设置。  

9. 在任务序列“属性”对话框上，单击“确定”，保存任务序列。
