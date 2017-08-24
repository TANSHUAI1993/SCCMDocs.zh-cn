---
title: "自定义启动映像 - Configuration Manager | Microsoft Docs"
description: "了解使用 Configuration Manager 或部署映像服务和管理 (DISM) 命令行工具自定义启动映像的几种方式。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: ab2ecb64c9c80b4effed79ba08769c99473db0c4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 自定义启动映像

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 的每个版本都支持特定版本的 Windows 评估和部署工具包 (Windows ADK)。 如果启动映像基于来自受支持的 Windows ADK 版本中的 Windows PE 版本，则可以从 Configuration Manager 控制台中维护或自定义启动映像。 对于其他启动映像，你必须使用其他方法自定义它们，如使用 Windows AIK 和 Windows ADK 中的部署映像服务和管理 (DISM) 命令行工具。  

 下面提供了受支持的 Windows ADK 版本、可在 Configuration Manager 控制台中自定义的启动映像所基于的 Windows PE 版本，以及可使用 DISM 自定义，然后将映像添加到 Configuration Manager 的启动映像所基于的 Windows PE 版本。  

-   **Windows ADK 版本**  

     适用于 Windows 10 的 Windows ADK  

-   **可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 版本**  

     Windows PE 10  

-   **不可从 Configuration Manager 控制台中自定义的启动映像的 Windows PE 支持版本**  

     Windows PE 3.1<sup>1</sup> 和 Windows PE 5  

     <sup>1</sup> 只有当启动映像基于 Windows PE 3.1 时才能将该映像添加到 Configuration Manager 中。 安装适用于 Windows 7 SP1 的 Windows AIK 补充，以使用适用于 Windows 7 SP1（基于 Windows PE 3.1）的 Windows AIK 补充升级适用于 Windows 7（基于 Windows PE 3）的 Windows AIK。 你可以从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充。  

     例如，如果具有 Configuration Manager，则可以利用 Configuration Manager 控制台自定义适用于 Windows 10 的 Windows ADK 中的启动映像（基于 Windows PE 10）。 但是，当支持基于 Windows PE 5 的启动映像时，你必须在不同的计算机中自定义它们，并使用随适用于 Windows 8 的 Windows ADK 一起安装的 DISM 版本。 然后，可以向 Configuration Manager 控制台添加启动映像。  

 本主题中的过程演示如何使用以下 Windows PE 包将 Configuration Manager 所需的可选组件添加到启动映像中：  

-   **WinPE-WMI**：添加 Windows Management Instrumentation (WMI) 支持。  

-   **WinPE 脚本**：添加 Windows 脚本宿主 (WSH) 支持。  

-   **WinPE WDS 工具**：安装 Windows 部署服务工具。  

 有可供添加的其他 Windows PE 程序包。 以下资源提供了有关可以添加到启动映像的可选组件的详细信息。  

-   对于 Windows PE 5，请参阅 [WinPE: Add packages (Optional Components Reference)（WinPE：添加包（可选组件参考））](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

-   对于 Windows PE 3.1，请参阅 Windows 7 TechNet 文档库中的 [将程序包添加到 Windows PE 映像中](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) 主题。  

> [!NOTE]
>从包含所添加的工具的自定义启动映射启动到 WinPE 时，可以从 WinPE 打开命令提示符并输入工具的文件名以运行它。 这些工具的位置会自动添加到路径变量。 仅当在“自定义”选项卡上的启动映像属性中选择了“启用命令支持(仅限测试)”时，才能添加命令提示符。

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>自定义使用 Windows PE 5 的启动映像  
 要自定义使用 Windows PE 5 的启动映像，必须安装 Windows ADK、使用 DISM 命令行工具安装启动映像、添加可选组件和驱动程序，以及提交启动映像更改。 使用下列过程来自定义启动映像。  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>若要自定义使用 Windows PE 5 的启动映像  

1.  在无其他 Windows AIK 或 Windows ADK 版本且未安装任何 Configuration Manager 组件的计算机上安装 Windows ADK。  

2.  请从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=39982)下载适用于 Windows 8.1 的 Windows ADK  

3.  将启动映像 (wimpe.wim) 从 Windows ADK 安装文件夹（例如，<*安装路径*>\Windows Kits\\<版本>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<x86 或 amd64>\\<区域设置>）复制到将自定义启动映像的计算机上的目标文件夹。 此过程使用 C:\WinPEWAIK 作为目标文件夹名称。  

4.  使用 DISM 将启动映像安装到本地 Windows PE 文件夹。 例如，键入下列命令行：  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     其中 C:\WinPEWAIK 是包含启动映像的文件夹，C:\WinPEMount 是安装文件夹。  

    > [!NOTE]
    >  有关 DISM 的详细信息，请参阅 Windows 8.1 和 Windows 8 TechNet 文档库中的 [DISM - Deployment Image Servicing and Management Technical Reference（DISM - 部署映像服务和管理技术参考）](http://technet.microsoft.com/library/hh824821.aspx) 主题。

5.  安装启动映像之后，请使用 DISM 将可选组件添加到启动映像中。 在 Windows PE 5 中，64 位可选组件位于 <*Installation path*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs。  

    > [!NOTE]
    >  此过程将下列位置用于可选组件：C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs。 根据你为 Windows ADK 选择的版本和安装选项，你使用的路径可能不同。  

     键入下列命令以安装可选组件：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-SecureStartup_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WMI_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-Scripting** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<locale\>* **\WinPE-WDS-Tools_** *<locale\>* **.cab"**  

     其中 C:\WinPEMount 是装载的文件夹，区域设置是适用于组件的区域设置。 例如，对于 **en-us** 区域设置，你需要键入：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

    > [!TIP]
    >  有关可以添加到启动映像的可选组件的详细信息，请参阅 Windows 8.1 和 Windows 8 TechNet 文档库中的 [Windows PE 可选组件参考](http://technet.microsoft.com/library/hh824926.aspx) 主题。  

6.  需要时使用 DISM 将特定驱动程序添加到启动映像中。 请键入下列命令以将驱动程序添加到启动映像中：  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *path to driver .inf file* **>**  

     其中 C:\WinPEMount 是安装文件夹。  

7.  键入以下命令以卸载启动映像文件并提交更改。  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     其中 C:\WinPEMount 是安装文件夹。  

8.  将更新的启动映像添加到 Configuration Manager，以使其在你的任务序列中可用。 使用下列步骤导入更新后的启动映像：  

    1.  在 Configuration Manager 控制台中，单击“软件库” 。  

    2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

    3.  在“主页”  选项卡上的“创建”  组中，单击“添加启动映像包”  以启动添加启动映像包向导。  

    4.  在“数据源”  页上，指定以下选项，然后单击“下一步” 。  

        -   在“路径”  框中，指定更新的启动映像文件的路径。 指定的路径必须是 UNC 格式的有效网络路径。 例如：**\\\\<**服务器名称**>\\<**WinPEWAIK 共享**>\winpe.wim**。  

        -   从“启动映像”  下拉列表中选择启动映像。 如果 WIM 文件包含多个启动映像，则会列出每个映像。  

    5.  在“常规”  页上，指定以下选项，然后单击“下一步” 。  

        -   在“名称”  框中，为启动映像指定唯一名称。  

        -   在“版本”  框中，为启动映像指定版本号。  

        -   在“备注”  框中，指定有关启动映像使用方式的简要描述。  

    6.  完成向导。  

9. 你可以在启动映像中启用命令解释器以在 Windows PE 中对其进行调试和疑难解答。 使用以下步骤启用命令解释器。  

    1.  在 Configuration Manager 控制台中，单击“软件库” 。  

    2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

    3.  在列表中查找新启动映像，并标识该映像的程序包 ID。 你可以在启动映像的“映像 ID”  列中查找程序包 ID。  

    4.  从命令提示符处键入 **wbemtest** 以打开 Windows Management Instrumentation 测试器。  

    5.  在“命名空间”中键入 **\\\\<**SMS 提供程序计算机**>\root\sms\site_<**站点代码**>**，然后单击“连接”。  

    6.  单击“打开实例”，键入 **sms_bootimagepackage.packageID="<packageID\>"**，然后单击“确定”。 对于 packageID，请输入在步骤 3 中标识的值。  

    7.  单击“刷新对象” ，然后在“属性”  窗格中单击“EnableLabShell”  。  

    8.  单击“编辑属性” ，将值改为 **TRUE**，然后单击“保存属性” 。  

    9. 单击“保存对象” ，然后退出 Windows Management Instrumentation 测试器。  

10. 但是，你必须将启动映像分发到分发点、分发点组或与分发点组关联的集合，然后才能在任务序列中使用该启动映像。 使用以下步骤分发启动映像。  

    1.  在 Configuration Manager 控制台中，单击“软件库” 。  

    2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

    3.  单击在步骤 3 中标识的启动映像。  

    4.  在“主页”  选项卡上的“部署”  组中，单击“更新分发点” 。  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>自定义使用 Windows PE 3.1 的启动映像  
 要自定义使用 WinPE 3.1 的启动映像，你必须安装 Windows AIK、安装适用于 Windows 7 SP1 的 Windows AIK 补充，使用 DISM 命令行工具安装启动映像、添加其他组件和驱动程序，以及提交启动映像更改。 使用下列过程来自定义启动映像。  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>自定义使用 Windows PE 3.1 的启动映像  

1.  在无其他 Windows AIK 或 Windows ADK 版本且未安装任何 Configuration Manager 组件的计算机上安装 Windows AIK。 请从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=5753)下载 Windows AIK。  

2.  在步骤 1 中的计算机上安装适用于带 SP1 的 Windows 7 的 Windows AIK 补充程序。 从 [Microsoft 下载中心](http://www.microsoft.com/download/details.aspx?id=5188)下载适用于 Windows 7 SP1 的 Windows AIK 补充程序。  

3.  将启动映像 (wimpe.wim) 从 Windows AIK 安装文件夹（例如，<*InstallationPath*>\Windows AIK\Tools\PETools\amd64\\）复制到将自定义启动映像的计算机上的文件夹。 此过程使用 C:\WinPEWAIK 作为文件夹名称。  

4.  使用 DISM 将启动映像安装到本地 Windows PE 文件夹。 例如，键入下列命令行：  

     **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

     其中 C:\WinPEWAIK 是包含启动映像的文件夹，C:\WinPEMount 是安装文件夹。  

    > [!NOTE]
    >  有关 DISM 的详细信息，请参阅 Windows 7 TechNet 文档库中的[部署映像服务和管理技术参考](http://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx)主题。  

5.  安装启动映像之后，请使用 DISM 将可选组件添加到启动映像中。 例如，在 Windows PE 3.1 中，可选组件位于安装路径 <*InstallationPath*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\中。  

    > [!NOTE]
    >  此过程将下列位置用于可选组件：C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs。 根据你为 Windows AIK 选择的版本和安装选项，你使用的路径可能不同。  

     键入下列命令以安装可选组件：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wmi_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-scripting_** *<locale\>* **.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wds-tools_** *<locale\>* **.cab"**  

     其中 C:\WinPEMount 是装载的文件夹，区域设置是适用于组件的区域设置。 例如，对于 **en-us** 区域设置，你需要键入：  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

     **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

    > [!TIP]
    >  有关可以添加到启动映像的不同程序包的详细信息，请参阅 Windows 7 TechNet 文档库中的[将包添加到 Windows PE 映像中](http://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx)主题。  

6.  需要时使用 DISM 将特定驱动程序添加到启动映像中。 如果需要，请键入下列命令以将驱动程序添加到启动映像中：  

     **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *path to driver .inf file* **>**  

     其中 C:\WinPEMount 是安装文件夹。  

7.  键入以下命令以卸载启动映像文件并提交更改。  

     **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

     其中 C:\WinPEMount 是安装文件夹。  

8.  将更新的启动映像添加到 Configuration Manager，以使其在你的任务序列中可用。 使用下列步骤导入更新后的启动映像：  

    1.  在 Configuration Manager 控制台中，单击“软件库” 。  

    2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

    3.  在“主页”  选项卡上的“创建”  组中，单击“添加启动映像包”  以启动添加启动映像包向导。  

    4.  在“数据源”  页上，指定以下选项，然后单击“下一步” 。  

        -   在“路径”  框中，指定更新的启动映像文件的路径。 指定的路径必须是 UNC 格式的有效网络路径。 例如：**\\\\<**服务器名称**>\\<**WinPEWAIK 共享**>\winpe.wim**。  

        -   从“启动映像”  下拉列表中选择启动映像。 如果 WIM 文件包含多个启动映像，则会列出每个映像。  

    5.  在“常规”  页上，指定以下选项，然后单击“下一步” 。  

        -   在“名称”  框中，为启动映像指定唯一名称。  

        -   在“版本”  框中，为启动映像指定版本号。  

        -   在“备注”  框中，指定有关启动映像使用方式的简要描述。  

    6.  完成向导。  

9. 你可以在启动映像中启用命令解释器以在 Windows PE 中对其进行调试和疑难解答。 使用以下步骤启用命令解释器。  

    1.  在 Configuration Manager 控制台中，单击“软件库” 。  

    2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

    3.  在列表中查找新启动映像，并标识该映像的程序包 ID。 你可以在启动映像的“映像 ID”  列中查找程序包 ID。  

    4.  从命令提示符处键入 **wbemtest** 以打开 Windows Management Instrumentation 测试器。  

    5.  在“命名空间”中键入 **\\\\<**SMS 提供程序计算机**>\root\sms\site_<**站点代码**>**，然后单击“连接”。  

    6.  单击“打开实例”，键入 **sms_bootimagepackage.packageID="<packageID\>"**，然后单击“确定”。 对于 packageID，请输入在步骤 3 中标识的值。  

    7.  单击“刷新对象” ，然后在“属性”  窗格中单击“EnableLabShell”  。  

    8.  单击“编辑属性” ，将值改为 **TRUE**，然后单击“保存属性” 。  

    9. 单击“保存对象” ，然后退出 Windows Management Instrumentation 测试器。  

10. 但是，你必须将启动映像分发到分发点、分发点组或与分发点组关联的集合，然后才能在任务序列中使用该启动映像。 使用以下步骤分发启动映像。  

    1.  在 Configuration Manager 控制台中，单击“软件库” 。  

    2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“启动映像包” 。  

    3.  单击在步骤 3 中标识的启动映像。  

    4.  在“主页”  选项卡上的“部署”  组中，单击“更新分发点” 。  
