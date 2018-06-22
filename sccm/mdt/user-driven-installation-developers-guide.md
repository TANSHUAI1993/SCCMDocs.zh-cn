---
title: 用户驱动安装
titleSuffix: Microsoft Deployment Toolkit
description: 'Microsoft Deployment Toolkit 2013 用户驱动安装的开发人员指南。 '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821081"
---
# <a name="user-driven-installation---developers-guide"></a>用户驱动的安装 - 开发人员指南
用户驱动安装 (UDI) 有助于简化使用 Microsoft® System Center 2012 R2 Configuration Manager 中的操作系统部署 (OSD) 功能将 Windows® 客户端操作系统（如 Windows 8.1）部署到计算机的过程。 UDI 是 Microsoft Deployment Toolkit (MDT) 的一部分。  

## <a name="introduction"></a>简介  
 通常，在使用 OSD 功能部署操作系统时，必须提供部署操作系统所需的全部信息。 在配置文件或数据库（例如 CustomSettings.ini 文件或 MDT 数据库 [MDT DB]）中配置信息。 必须先提供所有配置设置，然后才能开始部署。  

 通过 UDI 提供的向导驱动接口，可以在执行部署之前直接提供配置信息。 通过此行为可创建泛型 OSD 任务序列，然后在部署时提供特定于计算机的信息，这为部署过程提供了更大的灵活性。  

### <a name="target-audience"></a>目标受众  
 本指南专门针对为 UDI 向导创建自定义向导页以及为 UDI 向导设计器创建自定义向导页编辑器的开发人员编写。 本指南假定你熟悉使用以下语言开发 Windows 应用程序：  

-   C++，用于创建自定义向导页  

-   Microsoft.NET Framework，用于创建自定义向导页编辑器  

-   Windows Presentation Foundation (WPF)，用于创建自定义向导页编辑器  

-   WPF 支持的语言（如 C#、C++ 或 Microsoft Visual Basic® .NET），用于创建自定义向导页编辑器  

### <a name="about-this-guide"></a>关于本指南  
 本指南提供必要的参考信息，可帮助你为组织自定义 UTI。 本指南不讨论管理或操作主题，例如安装 MDT（包括 UDI）、配置 UDI 以部署操作系统和应用程序，或者使用 UDI 向导执行部署。 有关这些主题的详细信息，请参阅 MDT 中随附的《使用 Microsoft Deployment Toolkit》中的 UDI 主题。  

## <a name="udi-development-overview"></a>UDI 开发概述  
 通过 UDI 开发，可扩展 UDI 提供的功能。 通常情况下，如果想要收集 UDI 部署过程使用的其他信息，则需要 UDI 开发。 此附加信息通常保存为任务序列变量，由 Configuration Manager 中 UDI 任务序列的任务序列步骤读取。  

### <a name="udi-architecture"></a>UDI 体系结构  
 UDI 开发的高级目标是创建可在 UDI 向导中显示的自定义向导页。 可通过创建自定义向导页扩展 UDI 的现有功能，从而满足组织的业务和技术要求。 自定义向导页收集除 UDI 提供的向导页之外的信息或代替 UDI 提供的向导页的信息。  

 图 1 说明 UDI 向导设计器和 UDI 向导之间的关系。  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
图 1. UDI 向导和 UDI 向导设计器之间的关系  

 **图 1.UDI 向导和 UDI 向导设计器之间的关系**  

 从概念上讲，UDI 开发包括创建：  

-   **自定义向导页**。 向导页显示在 UDI 向导中，它收集完成部署过程所需的信息。 可在 Microsoft Visual Studio® 中使用 C++ 创建向导页。 自定义向导页是作为 UDI 向导读取的 DLL 实现的。 UDI 软件开发工具包 (SDK) 包含如何创建自定义向导页的示例。  

-   **自定义向导页编辑器**。 可使用向导页编辑器来配置自定义向导页的行为。 自定义向导页编辑器是作为 UDI 向导设计器读取的 DLL 实现的。 使用以下工具创建向导页编辑器：  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) 4.0 版本  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) 4.0 版本  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) 2.1 版本  

     MDT 包含所需的所有程序集，用于创建在 UDI 向导设计器中使用的自定义向导页编辑器。 UDI SDK 包含如何创建自定义向导页编辑器的示例。  

 此外，UDI 向导设计器使用支持的向导页编辑器配置文件。 创建向导页编辑器配置文件是创建自定义向导页和自定义向导页编辑器过程的一部分。 UDI 向导设计器在 UDI 向导配置文件和相应的 .app 文件中创建所需的 XML 信息。  

### <a name="preparing-the-udi-development-environment"></a>准备 UDI 开发环境  
 在开始创建自己的自定义向导页和向导页编辑器之前，请执行以下步骤以准备 UDI 开发环境：  

1.  按照[准备 UDI 开发环境必备项](#PrepareUDIDevelopmentEnvironmentPrerequisites)中所述，准备 UDI 开发环境的必备项。  

2.  按照[配置 UDI 开发环境](#ConfigureUDIDevelopmentEnvironment)中所述，配置 UDI 开发环境。  

3.  按照[验证 UDI 开发环境](#VerifyUDIDeploymentEnvironment)中所述，验证是否正确配置 UDI 开发环境。  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> 准备 UDI 开发环境必备项  
 若要准备 UDI 开发环境必备项，请执行以下步骤：  

1.  按照[准备 UDI 开发环境硬件必备项](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites)中所述，准备 UDI 开发环境硬件必备项。  

2.  按照[准备 UDI 开发环境软件必备项](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites)中所述，准备 UDI 开发环境软件必备项。  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> 准备 UDI 开发环境硬件必备项  
 UDI 开发环境硬件必备项与你正在使用的 Microsoft Visual Studio 2010 的硬件要求相同。 有关这些要求的详细信息，请参阅 [Visual Studio 2010 产品](http://www.microsoft.com/visualstudio/products/2010-editions)中每个版本的系统要求。  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> 准备 UDI 开发环境软件必备项  
 UDI 开发环境具有以下软件必备项：  

-   Visual Studio 2010 支持的任何 Windows 操作系统（建议使用 Windows 7 或 Windows Server® 2008 R2）。  

     Windows 操作系统需要支持要开发的处理器体系结构。 可使用 64 位操作系统执行 32 位和 64 位的 UDI 开发。 32 位操作系统上只能执行 32 位的 UDI 开发。 为此，应使用 64 位操作系统。  

    > [!NOTE]
    >  UDI 开发环境不支持 Windows 操作系统的 Intel Itanium 版本 (IA-64)。  

     有关 Visual Studio 2010 支持的操作系统的详细信息，请参阅 [Visual Studio 2010 产品](http://www.microsoft.com/visualstudio/products/2010-editions)中每个版本的系统要求。  

-   Microsoft.NET Framework 4.0 版本（Visual Studio 2010 要求）  

-   C++ 语言（用于扩展 UDI 向导页的语言）  

-   WPF 支持的其他语言（如 C#、Visual Basic .NET 或 C++/公共语言基础结构），用于扩展 UDI 向导设计器向导页编辑器  

    > [!NOTE]
    >  UDI 向导设计器向导页编辑器的示例源代码是用 C# 编写的。 如果想要使用示例源代码，请安装 C# 语言。  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> 配置 UDI 开发环境  
 满足 UDI 开发环境必备项之后，请执行以下步骤以配置 UDI 开发环境：  

1.  安装 Visual Studio 2010。  

     确保安装 C++ 语言和 WPF 支持的任何其他语言。  

    > [!NOTE]
    >  UDI 向导设计器编辑器页的示例源代码是用 C++ 编写的。 如果想要使用示例源代码，请安装 C# 语言。  

     有关安装 Visual Studio 2010 的详细信息，请参阅[安装 Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx)。  

2.  安装 MDT。  

     有关如何安装 MDT 的详细信息，请参阅 MDT 文档《使用 Microsoft Deployment Toolkit》中的“安装或升级到 MDT”部分。  

3.  在 Windows 资源管理器中，创建 local_folder（其中，local_folder 是位于开发计算机本地驱动器上的任意文件夹）。  

4.  将 installation_folder\SDK 文件夹复制到 local_folder（其中，installation_folder 是安装 MDT 的文件夹，local_folder 是位于开发计算机本地驱动器上的任意文件夹）。  

     将 SDK 文件夹复制到其他位置，因为 MDT 安装在 Program Files 文件夹中，无法在没有提升权限的情况下写入该文件夹。 通过将 SDK 文件夹复制到其他位置，可在无需提升权限的情况下修改 SDK 文件夹中的文件。  

5.  将 installation_folder\Templates\Distribution\Tools 文件夹复制到 local_folder（其中，installation_folder 是安装 MDT 的文件夹，local_folder 是你之前在此过程中创建的文件夹）。  

6.  将 local_folder\Tools 文件夹重命名为 local_folder\OSDSetupWizard（其中，local_folder 是你之前在此过程中创建的文件夹）。  

     完成后，local_folder 下方的文件夹结构应当与图 2 中所示文件夹结构类似（其中 local_folder 是你之前在此过程中创建的文件夹，在图中显示为 UDIDevelopment）。  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
图 2. UDI 开发的文件夹结构  

     **图 2.UDI 开发的文件夹结构**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> 验证 UDI 开发环境  
 配置 UDI 开发环境后，通过确保在 Visual Studio 2010 中正确生成示例项目来验证是否正确配置 UDI 开发环境。  

 可通过确定以下内容来验证是否正确配置 UDI 开发环境：  

-   是否按照[验证是否正确生成 SamplePage 项目](#VerifySamplePageProjectBuildsCorrectly)中所述正确生成 SamplePage 项目  

-   按照[验证是否正确生成 SampleEditor 项目](#VerifySampleEditorProjectBuildsCorrectly)中所述正确生成 SampleEditor 项目  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> 验证是否正确生成 SamplePage 项目  
 SamplePage 项目提供如何为 UDI 向导创建自定义向导页的示例。 有关 SamplePage 项目的详细信息，请参阅[查看 SamplePage Visual Studio 解决方案](#ReviewSamplePageVisualStudioSolution)。  

 **验证是否正确生成 SamplePage 项目**  

1.  启动 Visual Studio 2010。  

2.  打开 SamplePage 项目。  

     SamplePage 项目位于 local_folder\SDK\UDI\SamplePage 文件夹中（其中，local_folder 是你之前在此过程中创建的文件夹）。  

3.  在 Visual Studio 2010 的解决方案资源管理器中，右键单击 SamplePage 项目，然后单击“属性”。  

     随即出现“SamplePage 属性页”对话框。  

4.  在“SamplePage 属性页”对话框中，转到“配置属性”/“调试”。  

5.  在“调试”属性的“配置”下，选择“所有配置”。  

6.  在“调试”属性的“命令”下，键入“$(TargetDir)\OSDSetupWizard.exe”。  

7.  在“调试”属性的“工作目录”下，键入“$(TargetDir)”。  

8.  在“SamplePage 属性页”对话框中，转到“配置属性”/“调试”/“生成事件”/“生成后事件”。  

9. 在“生成后事件”属性中的“命令行”下，键入以下内容：  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. 在“SamplePage 属性页”对话框中，单击“确定”。  

11. 保存项目。  

12. 在“调试”菜单中，单击“启动调试”。  

     随即出现“Microsoft Visual Studio”对话框，指示源已过期，并询问你是否想要生成项目。  

13. 在“Microsoft Visual Studio”对话框中，单击“是”。  

     随即出现“无调试信息”对话框，通知你没有可用于 OSDSetupWizard.exe 的调试信息。  

14. 在“无调试信息”对话框中，单击“是”。  

     UDI 向导随即打开，并显示自定义向导页。  

15. 验证是否可以在“选择你的位置”中选择值。  

16. 在“包含示例的向导页”窗体中，单击“取消”。  

     随即出现“取消向导”对话框。  

17. 在“取消向导”对话框中，单击“是”。  

18. 关闭 Visual Studio 2010。  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> 验证是否正确生成 SampleEditor 项目  
 SampleEditor 项目提供如何为 UDI 向导设计器创建自定义向导页编辑器的示例。 有关 SampleEditor 项目的详细信息，请参阅[查看 SamplePage Visual Studio 解决方案](#ReviewSamplePageVisualStudioSolution)。  

 **验证是否正确生成 SampleEditor 项目**  

1.  启动 Visual Studio 2010。  

2.  打开 SampleEditor 项目。  

     SampleEditor 项目位于 local_folder\SDK\UDI\SampleEditor 文件夹中（其中，local_folder 是你之前在此过程中创建的文件夹）。  

3.  在 Visual Studio 2010 的解决方案资源管理器中，选择 SampleEditor 项目。  

4.  在“项目”菜单中，单击“添加引用”。  

     “添加引用”对话框随即打开。  

5.  在“添加引用”对话框中，单击“浏览”选项卡。  

6.  在“浏览”选项卡上，转到 installation_folder\Bin（其中，installation_folder 是安装 MDT 的文件夹）。 选择以下文件，然后单击“确定”：  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  单击文件时按住 Ctrl，可在“浏览”选项卡上选择多个文件。  

7.  在解决方案资源管理器中，转到“SampleEditor”/“引用”。  

8.  验证是否所有引用均无任何警告或错误。  

9. 在解决方案资源管理器中，右键单击 SampleEditor 项目，然后单击“属性”。  

     随即出现“SampleEditor 属性页”对话框。  

10. 在“SampleEditor 属性页”对话框中，单击“调试”选项卡。  

11. 在“调试”选项卡上，单击“启动外部程序”。  

12. 在“启动外部程序”中，键入“installation_folder\Bin\UDIDesigner.exe”（其中，installation_folder 是安装 MDT 的文件夹），然后单击“确定”。  

    > [!TIP]
    >  可单击省略号 (…) 按钮以浏览到该文件夹，然后选择“UDIDesigner.exe”。  

13. 在“文件”菜单中，单击“全部保存”。  

14. 将 local_folder\SDK\SamplePage\SamplePage.dll.config 文件复制到 installation_folder\Bin\Config 文件夹（其中，local_folder 是你之前在配置过程中创建的文件夹，installation_folder 是安装 MDT 的文件夹）。  

15. 在 Visual Studio 2010 的“调试”菜单中，单击“开始调试”。  

     UDI 向导设计器随即启动。  

16. 在 UDI 向导设计器的功能区中，单击“打开”。  

     随即出现“打开”对话框。  

17. 在“打开”对话框中，打开 local_folder\SDK\SamplePage\SamplePage\Config.xml 文件（其中，local_folder 是你之前在配置过程中创建的文件夹）。  

     Config.xml 文件打开后，详细信息窗格中将显示自定义 [StageGroup](#StageGroup)。  

18. 在详细信息窗格中，单击“配置”选项卡。  

19. 查看“位置”框的配置信息，其中包括：  

    -   “解锁”按钮，用于启用或禁用“位置”框  

    -   “默认值”框，可在其中输入要在“位置”框中显示的默认值  

    -   “摘要页中可见的友好显示名称”，可在其中输入显示在“摘要”页上的信息标题  

    -   “位置”列表框，包括可能的位置的列表  

20. 关闭 UDI 向导设计器。  

21. 关闭 Visual Studio 2010。  

## <a name="reviewing-the-udi-sdk-examples"></a>查看 UDI SDK 示例  
 开始开发之前，请查看 UDI SDK 中提供的示例。 通过本指南中的信息和示例中的源代码来帮助创建自己的 UDI 自定义向导页和向导页编辑器。  

 通过查看以下内容来查看 UDI SDK 示例：  

-   按照[查看 SDK 文件夹的内容](#ReviewContentsofSDKFolder)中所述，查看之前在安装过程中复制的 SDK 文件夹的内容  

-   自定义 UDI 向导页示例，如[查看 SamplePage Visual Studio 解决方案](#ReviewSamplePageVisualStudioSolution)中所述  

-   自定义 UDI 向导页编辑器示例，按照[查看 SampleEditor Visual Studio 解决方案](#ReviewSampleEditorVisualStudioSolution)中所述  

###  <a name="ReviewContentsofSDKFolder"></a> 查看 SDK 文件夹的内容  
 在配置 UDI 开发环境期间，将 SDK 文件夹从安装了 MDT 的文件夹中复制到创建的另一个文件夹。 表 1 列出了紧跟在 SDK 文件夹下方的文件夹，并提供每个文件夹的简要描述。  

### <a name="table-1-folders-in-the-udi-sdk"></a>表 1. UDI SDK 中的文件夹  

|**文件夹**|**此文件夹包含**|  
|-|-|  
|Includes|创建 UDI 向导的自定义向导页所需的 C++ 头文件|  
|Libs|将链接到自定义页面的 C++ 库文件；有 32 位和 64 位版本的静态链接库。 注意：库的 Itanium 版本 (IA-64) 不可用。|  
|SampleEditor|用于生成自定义编辑器（用于在 UDI 向导设计器中编辑 SamplePage 页）的 Visual Studio 项目，采用 C# 编写|  
|SamplePage|用于生成自定义 UDI 向导页的 Visual Studio 项目，采用 Visual C++ 编写|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> 查看 SamplePage Visual Studio 解决方案  
 在开始创建自定义向导页和向导页编辑器之前，请执行以下任务以准备 UDI 开发环境：  

-   按照[查看向导页生命周期](#ReviewWizardPageLifeCycle)中所述，查看 UDI 向导页生命周期中的阶段。  

-   按照[查看 SamplePage 示例](#ReviewSamplePageExample)中所述，查看 UDI SDK 中 SamplePage 示例的 Visual Studio 解决方案。  

####  <a name="ReviewWizardPageLifeCycle"></a> 查看向导页生命周期  
 UDI 向导页有对应页面生命周期中每个阶段的方法。 在创建自定义向导页过程中，需要使用代码替代这些方法。 表 2 列出了需要替代的方法，并提供每个方法的简要描述（包括何时在向导页生命周期中使用该方法）。  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>表 2. 向导页生命周期中的方法  

|**方法**|**描述**|  
|-|-|  
|**OnWindowCreated**|创建该页面的窗口后，调用一次此方法。<br /><br /> 针对此方法，编写第一次初始化该页面的代码，只需执行一次。 例如，使用此方法初始化字段或从 UDI 向导配置文件中的 Setter 元素读取配置信息。|  
|**OnWindowShown**|每当在 UDI 向导中显示该页面时，都会调用此方法。 第一次显示该页面和每当通过单击向导中的“下一步”或“上一步”导航到该页面时调用它。<br /><br /> 针对此方法，编写准备显示该页面的代码（如读取内存变量、任务序列变量或环境变量），然后基于对这些变量的任何更改来更新该页面。|  
|**OnCommonControlEvent**|每当显示向导页以及接收到来自子元素（通常为公共控件）的 WM_NOTIFY 消息时，都可调用此方法。<br /><br /> 针对此方法，编写基于通知消息处理 WM_NOTIFY 的代码。 例如，你可能希望响应来自公共控件的事件，例如响应 TreeView 控件的单击或双击事件。|  
|**OnUnhandledEvent**|每当向导页出现未处理的窗口消息时，将调用此方法。 此方法提供截获和处理这些未以其他方式处理的窗口消息的机会。<br /><br /> 针对此方法，编写处理与向导页相关的窗口消息的代码。 通常情况下，不需要替代此方法。|  
|**OnNextClicked**|在向导中单击“下一步”时，调用此方法。<br /><br /> 针对此方法，编写转到下一个向导页之前执行任何必要操作的代码（如执行验证操作可能需要很长时间）。 如果验证失败，则可以取消“下一步”请求并显示一条消息。|  
|**OnWindowHidden**|每当显示上一个或下一个向导页隐藏该页面时，都会调用此方法。<br /><br /> 针对此方法，编写在隐藏该页面后且显示另一个页面之前执行任何操作的代码。 通常情况下，不需要替代此方法。|  

####  <a name="ReviewSamplePageExample"></a> 查看 SamplePage 示例  
 使用以下列表（表示 SamplePage 示例的向导页生命周期内的事件序列）查看 SamplePage 示例：  

1.  UDI 向导 (OSDSetupWizard.exe) 从示例的 UDI 向导配置文件（Config.xml 文件）中读取配置信息，如[步骤 1：UDI 向导 (OSDSetupWizard.exe) 读取 Config.xml 文件](#UDIWizardReadstheConfigFile)中所述。  

2.  UDI 向导加载 UDI 向导配置文件中列出的每个向导页所需的 DLL，如[步骤 2：UDI 向导加载自定义向导页的 DLL](#UDIWizardLoadstheDLLforCustomWizardPage) 中所述。  

3.  UDI 向导显示自定义向导页，并允许进行所需的控件交互，如[步骤 3：UDI 向导显示自定义向导页](#UDIWizardDisplaysCustomWizardPage)中所述。  

4.  自定义向导页收集了信息后，在单击“下一步”之前执行任何必要的任务，以转到下一个向导，如[步骤 4：在自定义向导页中单击“下一步”按钮](#TheNextButtonisClickedinCustomWizardPage)中所述。  

#####  <a name="UDIWizardReadstheConfigFile"></a>步骤 1：UDI 向导 (OSDSetupWizard.exe) 读取 Config.xml 文件  
 当 UDI 向导 (OSDSetupWizard.exe) 启动时，它默认读取 UDI 向导配置文件，该文件是 UDIWizard_Config.xml 文件，即 UDI 向导的主配置文件。  

> [!NOTE]
>  该示例使用 Config.xml 文件作为配置文件。 在 MDT 中，默认配置文件是 UDIWizard_Config.xml 文件，它位于用于配置的 MDT 文件包的脚本文件夹中。  

 可通过修改 UDI 向导任务序列步骤来使用 /definition 参数，替代 UDI 向导使用的默认配置文件。 有关替代 UDI 向导使用的默认配置文件的详细信息，请参阅“替代 UDI 向导使用的配置文件”。  

 Config.xml 文件中的顶层元素为  

-   [DLLs](#DLLs) 元素  

-   [Style](#Style) 元素  

-   [Pages](#Pages) 元素  

-   [StageGroups](#StageGroups) 元素  

 有关 UDI 向导配置文件和每个元素的架构的详细信息，请参阅 [UDI 向导配置文件架构参考](#UDIWizardConfigurationFileSchemaReference)。  

 UDI 向导扫描 DLL 元素，查找要加载的 .dll 文件。 在本示例中，列出了两个 .dll 文件：SamplePage.dll 和 SharedPages.dll。 这些 .dll 文件须位于与 OSDSetupWizard.exe 相同的文件夹中，即 Tools\\platform 文件夹（其中，platform 为 32 位版本的 x86 或 64 位版本的 x64）。  

 UDI 向导扫描 Pages 元素，它查找定义的页面。 在本示例中，定义了两个页面：自定义和 SummaryPage。 在 PageClassIDs.h 文件中定义 Page 元素的 Type 特性，并唯一地定义自定义页面的类型。  

 本示例中，定义的类型为 Microsoft.SamplePage.LocationPage。 针对自定义页面，为避免与将来可能创建的其他页面发生任何潜在冲突，请替换以下内容：  

-   使用组织名称代替 Microsoft。  

-   使用项目名称代替 SamplePage。  

-   使用自定义向导页名称代替 LocationPage。  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> 步骤 2：UDI 向导加载自定义向导页的 DLL  
 当 UDI 向导加载 DLL 时，它会调用 RegisterFactories 函数，该函数必须在 .dll 文件中实现。 本示例中，在 dllmain.ccp 文件中实现该函数。 创建的每个向导页都必须实现 RegisterFactories 函数。  

 RegisterFactories 函数用于向 UDI 向导的类工厂注册表注册向导页的工厂类。 Class factories 是可以创建另一个类的实例的类。 RegisterFactories 函数创建工厂类的新实例，并将该类传递给 UDI 向导的类工厂注册表，这样即可将该工厂类提供给向导。 UDI 向导将查找注册 ID 与自定义向导页 Page 元素的 Type 特性相匹配的工厂类。  

 在本示例中，ID 在 PageClassIds.h 文件中定义为 ID_Location，类型为 Microsoft.SamplePage.LocationPage，它与 Config.xml 文件中 Page 元素的 Type 特性相匹配。 将 ID_Location 作为 dllmain.ccp 文件中实现的 RegisterFactories 函数的参数传递。  

 可使用 Register_name 函数模板创建一个函数来简化创建新工厂实例和注册新创建的实例。 使用 Register 函数模板提供的 name 值需要实现 iClassFactory 接口。 [ClassFactoryImpl 类](#ClassFactoryImplClass)处理实现类工厂的大部分细节。  

 还可使用 RegisterFactories 函数来注册任务类型和验证程序类型。 有关详细信息，请参阅以下内容：  

-   [创建自定义 UDI 任务](#CreatingCustomUDITasks)  

-   [创建自定义 UDI 验证程序](#CreatingCustomUDIValidators)  

> [!NOTE]
>  示例仅包含并注册一个自定义向导页。 示例不包含自定义任务或验证程序，因此不会注册任何自定义任务或验证程序。  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> 步骤 3：UDI 向导显示自定义向导页  
 本示例中，在 LocationPage.cpp 文件中定义示例中的自定义向导页。 向导页派生自模板类，它提供页面具有的大部分功能。 所有向导页都应派生自实现 [IWizardPage 接口](#IWizardPageInterface)的 [WizardPageImpl 模板类](#WizardPageImplTemplateClass)。 每个向导页都可根据页面需求实现其他可选模板类和相应接口。  

 [WizardPageImpl 模板类](#WizardPageImplTemplateClass)具有几个有用的接口，可帮助你编写自定义向导页。 将 [WizardPageImpl 模板类](#WizardPageImplTemplateClass)作为自定义向导页的基类实现。  

 关于可用的列表：  

-   向导页的模板类，请参阅[向导页帮助程序类](#WizardPageHelperClasses)  

-   向导页模板类的接口，请参阅[向导页接口](#WizardPageInterfaces)  

 示例中的自定义向导页派生自 [WizardPageImpl 模板类](#WizardPageImplTemplateClass)，并实现 [IWizardPage 接口](#IWizardPageInterface)。 此外，自定义向导页实现 IFieldCallback 接口。 两者均在 LocationPage.cpp 文件中实现。  

 示例自定义向导页将替代以下方法：  

-   **OnWindowCreated**。 示例向导页中的 OnWindowCreated 方法调用以下方法：  

    -   [AddField](#AddField)。 此方法将 IDD_LOCATION_PAGE 资源中的 IDC_COMBO_LOCATION 框控件与 Config.xml 文件中名为 Location 的 [Data](#Data) 元素相关联。  

         除了 AddField 方法外，还可使用 [AddRadioGroup](#AddRadioGroup) 和 [AddToGroup](#AddToGroup) 方法来支持其他控件和行为。  

        > [!NOTE]
        >  确保在调用 [InitFields](#InitFields) 方法之前，先调用 [AddField](#AddField)、[AddRadioGroup](#AddRadioGroup) 或 [AddToGroup](#AddToGroup) 方法。  

    -   [InitFields](#InitFields)。 使用此方法初始化添加到窗体的字段（控件）。 页面的指针是一个参数。 在本示例中，传递 this 指针，该指针指向当前页面。  

        > [!NOTE]
        >  为支持 this 指针的使用，除了 **WizardPageImpl** 模板类支持的接口之外，还必须实现 [IFieldCallback](#WizardPageImplTemplateClass) 接口。  

         IFieldCallback 接口调用 SetFieldDefault 方法，该方法用于设置除文本框和复选框控件以外的控件的默认值。 在本示例中，SetFieldDefault 方法在 Config.xml 文件中基于 [Field](#Field) 元素的 Default 元素中指定的默认值设置组合框控件的初始索引。  

     OnWindowCreated 方法使用 [IFormControlle 接口](#IFormController-Interface)来设置窗体控制器。 有关设置窗体控制器的详细信息，请参阅[设置窗体](#SettingUptheForm)。  

-   **InitLocations**。 此方法从 Config.xml 文件中的位置列表填充组合框。 [Data](#Data) 元素和子元素 [DataItem](#DataItem) 元素 Confg.xml 文件提供可能值的列表。  

-   **OnNextClicked**。 此方法执行以下任务：  

    -   使用 SaveFields 方法将 TSLocation 任务序列变量更新为组合框中所选的值  

    -   使用 SaveFields 方法添加要在摘要页上显示的信息  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"> </a> 步骤4：在自定义向导页中单击“下一步”按钮  
 当用户完成自定义向导页上字段的填写时，单击“下一步”，会调用 OnNextClicked 方法。 在继续到下一个向导页之前，OnNextClicked 方法会执行任何必要的任务，例如记录在自定义向导页上进行的任何配置更改。  

 对于自定义向导页示例，在 LocationPage.ccp 文件中实现 OnNextClicked 方法的替代。 在示例自定义向导页的 OnNextClicked 方法中，调用以下方法：  

1.  [InitSection](#InitSection)。 此方法将初始化显示在“摘要”页上的摘要数据的标头（标签标题）。 通常情况下，可使用 DisplayName() 函数来设置此值。 使用 [SaveFields](#SaveFields) 方法保存与此标题相关的数据。  

2.  [SaveFields](#SaveFields)。 此方法将字段值保存到任务序列变量和显示在“摘要”页上的数据。  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> 查看 SampleEditor Visual Studio 解决方案  
 在开始创建自己的自定义向导页和向导页编辑器之前，请执行以下步骤以准备 UDI 开发环境：  

-   按照[查看 UDI 向导设计器体系结构](#ReviewUDIWizardDesignerArchitecture)中所述，查看 UDI 向导设计器的体系结构。  

-   按照[查看 UDI 向导页的可配置组件](#ReviewConfigurableComponentsofUDIWizardPage)中所述，查看可使用 UDI 向导配置文件自定义的 UDI 向导页组件。  

-   按照[查看 EditorPage 示例](#ReviewEditorPageExample)中所述，查看 UDI SDK 中提供的 EditorPage 示例。  

####  <a name="ReviewUDIWizardDesignerArchitecture"> </a>查看 UDI 向导设计器体系结构  
 使用 WPF、Prism 和 Unity 开发 UDI 向导设计器。 UDI 设计器用于编辑 UDI 向导配置文件 (UDIWizard_Config.xml)，UDI 向导 (OSDSetupWizard.exe) 在运行时读取该配置文件。 UDI 向导配置文件中的 [Pages](#Pages) 元素包含一个页面列表，每个向导页都有一个单独的 [Page](#Page) 元素。  

 编辑向导页的配置设置时，UDI 向导设计器将加载对应向导页类型的自定义页面编辑器。 自定义向导页编辑器是作为 WPF 用户控件开发的。 自定义向导页编辑器页面使用 WPF 的 [模型-视图-视图模型](http://msdn.microsoft.com/magazine/dd419663.aspx) (MVVM) 设计模式。  

 MVVM 设计模式有助于将用户界面（UI；演示）与呈现的数据分开。 该数据是 UDI 向导配置文件（本示例中为 Config.xml 文件）中的 [Page](#Page) 元素的外观，可使用 [IDataService](#IDataService) 接口的 [CurrentPage](#CurrentPage) 属性访问。  

 UDI 向导设计器使用 DependencyAttribute 获取对基于 Unity 中依赖项注入框架的 DataService 类的访问。 有关 Unity 中依赖项注入框架的详细信息，请参阅 [Inject Some Life into Your Applications—Getting to Know the Unity Application Block](http://msdn.microsoft.com/library/ff650806.aspx)（为应用程序注入一些活力 - 了解 Unity 应用程序块）。  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> 查看 UDI 向导页的可配置组件  
 在创建自定义向导页时，可能会在代码中设置一些配置设置，这些设置在编译该页面后无法更改。 但是，对于其他配置设置，需要使用 UDI 向导设计器更改这些配置设置。  

 通常情况下，在 UDI 向导配置文件（本示例中为 Config.xml 文件）中保存要使用 UDI 向导设计器配置的配置设置。 但是，如有必要，也可创建自己的独立配置文件。 使用独立配置文件的一个示例是 UDIWizard_Config.xml.app 文件，即“应用程序发现”任务和 ApplicationPage 向导页类型使用的文件。  

 以下是可使用 UDI 向导设计器管理的典型配置设置的列表：  

-   **Field**。 通过字段，用户可以提供输入。 在 UDI 向导配置文件 (UDIWizard_Config.xml) 中，字段显示为 [Field](#Field) 元素，其中包含每个字段的配置设置。 相应的向导页编辑器需要提供使用 [FieldElementControl](#FieldElementControl) 编辑该字段的字段配置设置的方法。  

-   **属性**。 资源库有助于为页面上的实体创建属性，例如 [Page](#Page) 元素中的页面、[Field](#Field) 元素中的字段或者 [Data](#Data) 或 [DataItem](#DataItem) 元素中的数据。 可在 [Setter]() 元素中配置属性。 为要定义的每个属性添加一个单独的 [Setter]() 元素。 可使用 [SetterControl](#SetterControl) 编辑属性，以及使用其他控件配置其他 [Setter]() 元素。  

-   **数据**。 数据用于存储供向导页和其他组件使用的信息。 可使用 [Data](#Data) 或 [DataItem](#DataItem) 元素为页面或字段定义数据。 通过正确使用 [Data](#Data) 或 [DataItem](#DataItem) 元素，可以在平面或层次结构中定义数据。 在 SDK 的示例中，Config.xml 演示了如何生成平面数据结构。  

 所创建的自定义向导页编辑器必须能够管理这些配置设置。  

####  <a name="ReviewEditorPageExample"></a> 查看 EditorPage 示例  
 EditorPage 示例用于在 UDI 向导配置文件中配置 SamplePage 向导页的配置设置。 EditorPage 示例有以下主要组件：  

-   用于配置“位置”组合框设置的 UI  

-   用于添加或编辑可能位置列表中的位置的 UI，显示在“位置”组合框中  

-   从 UDI 向导配置文件读取和保存到该文件的配置设置  

-   用于其他组件的支持代码  

 通过执行以下步骤查看 Visual Studio 中的 EditorPage 示例：  

1.  按照[查看向导页编辑器的加载和初始化](#ReviewWizardPageEditorLoadingInitialization)中所述，查看如何在 UDI 向导设计器中加载和初始化 SampleEditor 向导页编辑器。  

2.  按照[查看用于配置“位置”组合框的用户界面](#ReviewUserInterfaceUsedtoConfigureLocationComboBox)中所述，查看用于在 LocationPageEditor.xaml 和 LocationPageEditor.xaml.cs 文件中编辑“位置”组合框的 UI。  

3.  按照[查看用于修改可能位置列表的用户界面](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations)中所述，查看用于在 AddEditLocationView.xaml 和 AddEditLocationView.xaml.cs 文件的列表中添加或编辑位置的 UI。  

4.  按照[查看用于管理配置信息的代码](#ReviewCodeUsedtoManageConfigurationInformation)中所述，查看用于管理保存在 UDI 向导配置文件中的配置信息的代码。  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> 查看向导页编辑器的加载和初始化  
 按照 UDI 向导设计器的要求，加载自定义向导页编辑器。 在启动 UDI 向导设计器时加载 UDI 向导设计器配置文件。 对于具有 .config 文件扩展名的文件，UDI 向导设计器会扫描 install_folder\Bin\Config 文件夹（其中，install_folder 是安装 MDT 的文件夹的名称）。  

 在配置 UDI 开发环境期间，将 SamplePage.dll.confg 文件复制到 install_folder\Bin\Config 文件夹。 在启动 UDI 向导设计器时，找到并加载示例 Page.dll.config 文件。  

 UDI 向导设计器在 SamplePage.dll.confg 文件中使用 [Page](#Page) 元素的以下特性来加载和初始化 EditorPage 示例：  

-   **DesignerAssembly**。 此特性确定要加载的 DLL 的名称。 需要将此 DLL 与 UDIDesigner.exe 文件放在同一文件夹中，即 install_folder\Bin 文件夹（其中，install_folder 是安装 MDT 的文件夹的名称）。  

-   **DesignerType**。 此特性是包含 WPF 用户控件的类的 Microsoft .NET 类型名称。  

-   **类型**。 使用此特性可配置 UDI 向导加载的自定义向导页的页面类型。 UDI 向导设计器使用此特性在 UDI 向导配置文件中找到相应的 [Page](#Page) 元素。  

-   **Dll**。 使用此特性可在 UDI 向导配置文件中配置 UDI 向导设计器创建的 [DLL](#DLL) 元素。  

-   **说明**。 使用此特性来提供有关向导页编辑器的信息。 此特性的值显示在 UDI 向导设计器的“添加新页面”对话框中，此对话框用于将向导页添加到“页面库”。  

-   **DisplayName**。 使用此特性来提供显示在 UDI 向导设计器的自定义向导页中的名称。 此特性的值显示在 UDI 向导设计器的“添加新页面”对话框中，此对话框用于将向导页添加到“页面库”。  

     在本示例中，自定义向导页的 SamplePage 类型为 Microsoft.SamplePage.LocationPage，它保存在 Config.xml 文件中。 Config.xml 文件位于 local_folder\SDK\SamplePage\SamplePage 文件夹中（其中，local_folder 是你之前通过开发计算机在配置过程中创建的文件夹）。  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> 查看用于配置“位置”组合框的用户界面  
 加载和初始化向导页编辑器后，会在编辑类型为 Microsoft.SamplePage.LocationPage 的页面时加载 SampleEditor 向导页编辑器。 页面编辑器的 UI 存储在 LocationPageEditor.xaml 文件中。  

 如果检查“设计”选项卡上的 UI 和“XAML”选项卡上的代码，则可以看到图形 UI 与 Extensible Application Markup Language (XAML) 的元素和特性之间的关系。  

 例如，如果查看 XAML 中的 Controls:FieldElementControl 元素，则可以看到它与相应 UI 布局之间的关系。 使用 Controls:FieldElementControl 元素来定义 [FieldElementControl](#FieldElementControl) 控件。  

 XAML 文件中的 Binding 参数将示例页面编辑器上的字段与 UDI 向导配置文件中的信息绑定在一起。 例如，以下代码将“默认值”文本框与 UDI 向导配置文件（本示例中为 Config.xml）中的 [Default](#Default) 元素绑定在一起：  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 有关详细信息，请参阅 [How to: Make Data Available for Binding in XAML](http://msdn.microsoft.com/library/ms748857.aspx)（如何在 XAML 中使数据可用于绑定）。  

 在 XAML中使用 Views:CollectionTControl.ColumnCollectionView 元素编辑网格视图中可用位置的列表。 使用 [CollectionTControl](#CollectionTControl) 控件显示网格视图，并将网格视图绑定到 UDI 配置文件中名为 Location 的 [Data](#Data) 元素。  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> 查看用于修改可能位置的列表的用户界面  
 用于修改可能位置的列表的 UI 包括：  

-   上下文相关菜单和功能区按钮，用于添加、编辑、删除或更改位置列表中项的顺序，如[查看用于修改位置列表的上下文相关菜单和功能区按钮](#ReviewContextSensitiveMenuandRibbonButtons)中所述  

-   一个对话框，它在选择添加或编辑位置列表中的项时启动，如[查看用于添加或编辑位置的对话框](#ReviewDialogBoxforAddingEditingLocations)中所述  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> 查看用于修改位置列表的上下文相关菜单和功能区按钮  
 在包含位置列表的列表框中右键单击时，会显示一个上下文相关菜单。 功能区具有相应的按钮，可用于执行相同的任务。 LocationPageEditor.xaml 文件中的 Views:CollectionsTControl 控件元素根据设置的操作和属性来定义调用的方法，如下所示：  

-   **SelectedItem**。 当用户从列表中选择某个项时会激活该数据绑定属性。 该属性在视图模型中绑定 CurrentLocation 属性，它位于 LocationPageEditorViewModel.cs 文件中，在编辑或删除某个现有项时，[CollectionTControl](#CollectionTControl) 控件会使用它来传递选定的项。  

-   **AddItemAction**。 当用户单击上下文相关菜单中的“添加项”选项或功能区上的相应按钮时，会执行此操作。 视图模型中有一个绑定到某个属性的数据，它返回 AddLocationAction 对象。 该对象是位于 LocationPageEditorViewModel.cs 文件中的 AddLocationCallback 方法，并在 AddEditLocationView.xaml 文件中显示对话框。  

-   **EditItemAction**。 当用户从上下文相关菜单中单击“编辑项”选项时，会执行此操作。 视图模型中有一个绑定到属性的数据，它返回 EditLocationAction 对象。 该对象是位于 LocationPageEditorViewModel.cs 文件中的 EditLocationCallback 方法，并在 AddEditLocationView.xaml 文件中显示对话框。  

-   **RemoveAction** 当用户从上下文相关菜单中单击“删除项”选项时，会执行此操作。 视图模型中有一个绑定到某个属性的数据，它返回 RemoveAction 对象。 该对象是位于 LocationPageEditorViewModel.cs 文件中的 EditLocationCallback 方法，并显示确认删除位置的消息。  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> 查看用于添加或编辑位置的对话框  
 如果将新位置添加到位置列表或编辑现有位置，则会在 AddEditLocationView.xaml 文件中显示一条消息。 该消息在 LocationPageEditorViewModel.cs 文件中通过 [ShowDialogWindow](#ShowDialogWindow) 窗口方法显示。  

 AddEditLocationView.xaml 文件中的 UI 包括：  

-   一个名为 DialogFrame 的对话框，其中包含以下元素：  

    -   一个标题，可使用对话框的 DialogTitle 特性进行配置  

    -   一个“确定”按钮，它将 Approved 属性的返回状态设置为“True”（返回状态签入 LocationPageEditorViewModel.cs 文件中的 AddLocationCallback 方法，用于确定用户是否单击“确定”。）  

    -   一个“取消”按钮，它将 Approved 属性的返回状态设置为“False”（返回状态签入 LocationPageEditorViewModel.cs 文件中的 AddLocationCallback 方法，用于确定用户是否单击“取消”。）  

-   一个 WPF 元素，其中包含：  

    -   一个标签，它使用 Content 特性进行配置  

    -   一个文本框，它绑定到 UDI 配置文件（本示例中为 Config.xml 文件）中名为 Location 的[ Data ](#Data)元素。  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> 查看用于管理配置信息的代码  
 自定义向导页的配置信息存储在 UDI 向导配置文件中，它是：  

-   UDI SDK 在本示例中所提供的 Config.xml 文件（该文件仅包含此示例的配置设置。）  

-   MDT 提供的 UDIWizard_Config.xml 文件，它存储在 installation_folder\Templates\Distribution\Scripts 文件夹中（其中，installation_folder 是安装 MDT 的文件夹）；该文件包含所有内置向导页和阶段的配置设置  

 在 SampleEditor 示例中，Locations 例程有助于管理配置信息，它位于 LocationPageEditorViewModel.cs 文件中。 Locations 例程从 UDI 向导配置文件返回一个位置列表。 具体而言，返回的列表会包含 UDI 向导配置文件中每个 [DataItem](#DataItem) 元素的项。  

## <a name="creating-custom-udi-wizard-pages"></a>创建自定义 UDI 向导页  
 创建自定义 UDI 向导页的高级过程如下所示：  

1.  首先，创建 SamplePage 解决方案的副本。  

2.  将所需控件（字段）放置在窗体上。  

3.  编写代码，以便在加载向导页时执行相应的任务（替代 OnWindowCreated 方法），其中包括以下步骤：  

    1.  初始化窗体。  

    2.  读取内存变量、任务序列变量、环境变量或 XML 文件信息（例如 Setter 属性）。  

4.  编写任意代码，以便在显示页面时执行相应的任务（重写 OnWindowShown 方法），其中包括以下步骤：  

    1.  基于在步骤 3 中加载页面时读取的信息启用或禁用控件。  

    2.  基于在步骤 3 中加载页面时读取的信息更新控件（例如基于读取的信息填充控件）。  

5.  编写任意代码，以便在用户与向导页交互时执行相应的任务。  

6.  编写任意代码，以便用户在 UDI 向导中单击“下一步”（替代 OnNextClicked 方法）时执行相应的任务，包括以下步骤：  

    1.  更新任意内存变量、任务序列变量、环境变量或 XML 文件信息。  

    2.  更新摘要页信息（如果不是由页面上的字段执行）。  

7.  生成解决方案。  

     确保创建的 DLL 版本与 MDT 安装的处理器平台相同，具体而言，是指 Windows 预安装环境 (Windows PE) 的处理器平台。 UDI 向导可在以下操作系统中运行：  

    -   **目标计算机上的现有操作系统**。 可以在 32 位或 64 位的 Windows 操作系统上运行 32 位版本的向导页。 但是，只能在 64 位的 Windows 操作系统上运行 64 位版本的向导页。  

    -   **目标计算机上的 Windows PE**。 Windows PE 不支持在 64 位版本的 Windows PE 上运行 32 位应用程序。 因此，对于计划使用的每个 Windows PE 处理器体系结构，都需要为向导页生成一个版本。  

8.  将自定义向导页的 DLL 复制到 installation_folder\Templates\Distribution\Tools\platform 文件夹（其中，installation_folder 是安装 MDT 的文件夹，platform 为 32 位版本的 x86 或 64 位版本的 x64）。  

9. 完成创建自定义页面编辑器的步骤。  

## <a name="creating-custom-wizard-page-editors"></a>创建自定义向导页编辑器  
 创建自定义 UDI 向导页编辑器的高级过程如下所示：  

1.  首先，创建 SampleEditor 解决方案的副本。  

2.  在 .xaml 文件中创建主页面编辑器 UI。  

3.  按照要配置的向导页的要求，添加 [FieldElementControl](#FieldElementControl) 控件的实例（如果需要）。  

4.  按照要配置的向导页的要求，添加 [SetterControl](#SetterControl) 控件的实例（如果需要）。  

5.  按照要配置的向导页的要求，添加 [CollectionTControl](#CollectionTControl) 控件的实例（如果需要）。  

6.  添加 [IDataService](#IDataService) 接口。  

7.  使用自定义向导页编辑器编写相应代码，以便基于要配置的配置设置更新 UDI 向导配置文件。  

8.  按照要配置的向导页的要求，在 .xaml 文件中创建子对话框，并使用 [IMessageBoxService](#IMessageBoxService) 接口从主页面编辑器调用子对话框。  

9. 基于要配置的向导页的要求，将相应接口添加到 UDI 向导设计器功能区。  

10. 生成解决方案。  

    > [!NOTE]
    >  确保创建的 DLL 版本与 MDT 安装的处理器平台相同。 例如，如果安装 64 位版本的 MDT，则可以生成 64 位版本的自定义页面编辑器。  

11. 创建 UDI 向导设计器配置文件，用于加载所需的 DLL 以及在向导页编辑器和相应向导页（本示例中为 SamplePage.dll.config 文件）之间执行映射。  

     有关在向导页和向导页编辑器之间执行映射所需元素的更多信息，请参阅 [DesignerMappings](#DesignerMappings) 元素、子元素和相应特性。  

12. 将上一步创建的 UDI 向导设计器配置文件复制到 installation_folder\Bin\Config 文件夹（其中，installation_folder 是安装 MDT 版本的文件夹）。  

13. 将自定义向导页编辑器的 DLL 复制到 installation_folder\Bin 文件夹（其中，installation_folder 是安装 MDT 的文件夹）。  

##  <a name="CreatingCustomUDITasks"></a> 创建自定义 UDI 任务  
 UDI 任务是采用 C++ 编写的 DLL，它们实现 [ITask 接口](#ITaskinterface)。 通过创建 UDI 向导设计器配置文件（.config 文件）并将其放置在 installation_folder\Bin\Config 文件夹（其中，installation_folder 是安装 MDT 的文件夹）中来向 UDI 向导设计器任务库注册 DLL。  

> [!NOTE]
>  可在同一个 .dll 文件中创建包含向导页、任务和验证程序的 DLL。 还可在 DLL 中创建包含向导页、任务和验证程序的配置设置的单个 UDI 向导设计器配置文件 (.config)。  

 **创建自定义 UDI 任务**  

1.  编写实现 [ITask 接口](#ITaskinterface)和以下方法的代码：  

    -   [Init](#Init)。 调用此方法来初始化任务。  

    -   [Execute](#Execute)。 调用此方法来运行任务。  

2.  编写向工厂注册表注册自定义任务类工厂的代码。  

3.  为自定义任务生成解决方案。  

    > [!NOTE]
    >  确保创建的 DLL 版本与 MDT 安装的处理器平台相同。 例如，如果安装 64 位版本的 MDT，则可以生成 64 位版本的自定义 UDI 任务。  

4.  在 UDI 向导设计器配置文件的 [TaskLibrary](#TaskLibrary) 元素下创建一个 [Task](#Task) 元素，类似于以下摘录：  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  所有 [Task](#Task) 元素都应包含 BitmapFilename 参数。 根据任务要求指定所有其他参数。 例如，在前面的摘录中，log 参数用于为日志文件的位置指定一个参数。  

5.  将上一步创建的 UDI 向导设计器配置文件复制到 installation_folder\Bin\Config 文件夹（其中，installation_folder 是安装 MDT 的文件夹）。  

6.  将自定义任务的 DLL 复制到 installation_folder\Templates\Distribution\Tools\platform 文件夹（其中，installation_folder 是安装 MDT 的文件夹，platform 为 32 位版本的 x86 或 64 位版本的 x64）。  

##  <a name="CreatingCustomUDIValidators"></a> 创建自定义 UDI 验证程序  
 UDI 验证程序是采用 C++ 编写的 DLL，它们实现 IValidator 接口。 通过创建 UDI 向导设计器配置文件（.config 文件）并将其放置在 installation_folder\Bin\Config 文件夹（其中，installation_folder 是安装 MDT 的文件夹）中来向 UDI 向导设计器验证程序库注册 DLL。  

 **创建自定义 UDI 验证程序**  

1.  编写创建 BaseValidator 类的子类并实现以下方法的代码：  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. 窗体控制器调用 Init 成员来初始化验证程序。 此方法必须调用 BaseValidator 类的 Init 方法。 它通常从 UDI 向导配置文件中读取为验证程序设置的任何属性。 例如，InvalidCharactersValidator 验证程序使用此方法检索 InvalidChars 属性的值。  

    -   **IsValid**。 窗体控制器调用此方法来查看控件是否包含有效的文本。 以下是用于验证该字段不为空的验证程序的 IsValid 方法示例：  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, LPCTSTR message)**. 窗体控制器为每个击键和其他事件调用该成员，以便验证程序可以验证（或清除）控件和向导页底部更新消息的内容。  

     通常情况下，只需要替代这些方法。 但是，根据不同的验证程序，可能需要在创建的 BaseValidator 类的子类中替代其他方法。 有关这些其他方法的更多信息，请参阅 BaseValidator 类。  

2.  编写向注册表工厂注册自定义任务类的代码。  

3.  为自定义任务生成解决方案。  

    > [!NOTE]
    >  确保创建的 DLL 版本与 MDT 安装的处理器平台相同。 例如，如果安装 64 位版本的 MDT，则可以生成 64 位版本的自定义 UDI 任务。  

4.  在 UDI 向导设计器配置文件的 ValidatorLibrary 元素下创建一个 [Validator](#Validator) 元素，类似于以下摘录：  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  所有 [Validator](#Validator) 元素都应包含 Message 参数。 按照验证程序的要求指定所有其他参数。 例如，在前面的摘录中，NamedPattern 参数用于为预定义的正则表达式模式的名称指定一个参数。  

5.  将上一步创建的 UDI 向导设计器配置文件复制到 installation_folder\Bin\Config 文件夹（其中，installation_folder 是安装 MDT 的文件夹）。  

6.  将自定义任务的 DLL 复制到 installation_folder\Templates\Distribution\Tools\platform 文件夹（其中，installation_folder 是安装 MDT 的文件夹，platform 为 32 位版本的 x86 或 64 位版本的 x64）。  

## <a name="udi-wizard-reference"></a>UDI 向导参考  

### <a name="wizard-page-components"></a>向导页组件  
 可使用任意预生成组件来生成自定义页面。  

#### <a name="creating-component-instances"></a>创建组件实例  
 UDI 向导使用类工厂创建对象的新实例。 这些工厂注册到工厂注册表，使用字符串作为工厂的键。 例如，WmiRepository 组件由“Microsoft.Wizard.WmiRepository”字符串标识，它在 IWmiRepository 头文件中作为 ID_WmiRepository 使用。  

 假设已将页面编写为 WizardPageImpl 的子类，则可以创建一个 WmiRepoistory 的新实例（与以下所示类似）：  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 CreateInstance 函数是用于创建组件新实例的类型安全模板函数。 PWmiRepository 是一个智能指针，因此它可以处理引用计数。  

#### <a name="creatable-components"></a>可创建的组件  
 有一组可以注册到注册表的组件。 由于主要的 UDI 向导可执行文件提供第一组组件，因此始终会对其进行注册。 “可选”DLL 中会提供另外两组组件。 若要提供这些组件，必须在 .config XML 文件的 DLL 节中列出该 DLL。 代码无需知道哪个可执行文件包含了特定的组件。  

 对于注册到工厂注册表（它在 OSDSetupWizard 中进行定义）的组件，表 3 中显示了其组件 ID 的列表（组件名称与组件 ID 相同，不过没有开头的“ID_”）。  

### <a name="table-3-component-ids"></a>表 3. 组件 ID  

|**ID**|**描述**|  
|-|-|  
|ID_ACPowerTask|(ITask, IWizardComponent) 是确保计算机不单独依靠电池运行的预检任务|  
|ID_AppDiscoveryTask|(ITask, IWizardComponent) 是用于发现计算机上已安装的软件项的专用任务|  
|**ID_BackgroundTask**|(IBackgroundTask, IWizardComponent) 可用于在其他线程上运行任务|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) 用于复制一个或多个文件的任务|  
|**ID_FormController**|(**IFormController**) 你将很可能无需自己创建实例，因为页面会接收它自己的实例|  
|**ID_InvalidCharactersValidator**|(**IValidator**) 确保没有文本字段包含提供给验证程序的列表中的字符|  
|**ID_Logger**|(**ILogger**) 你将很可能不用自己创建实例，因为页面会接收到一个指向共享实例的指针|  
|**ID_NonEmptyValidator**|(**IValidator**) 确保没有字段为空的验证程序|  
|**ID_PasswordValidator**|(**IValidator**) 确保两个文本字段没有相同内容的验证程序|  
|**ID_Regex**|(**IRegEx**) 计算正则表达式，查找匹配项|  
|**ID_RegExValidator**|(**IValidator**) 用于验证正则表达式或已知模式的验证程序|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) 提供一种不需要使用 XML 即可将属性发送到任务的简单方法|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) 执行外部程序|  
|**ID_SummaryBag**|(**ISummaryBag**) 可通过 Form 方法从页面间接获得|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) 管理一组运行的任务和 UI|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) 可通过它运行 Windows Management Instrumentation (WMI) 查询|  
|**ID_IXmlDocument**|(**IXmlDocument**) 提供用于读取和写入 XML 文档的外观|  

 表 4 和表 5 中显示了定义的 OSDRefreshWizard.dll、共享的页面和其他控件组件。  

### <a name="table-4-directory-controls"></a>表 4. 目录控件  

|**ID**|**描述**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) 用于从文件系统中获取目录信息的外观|  

### <a name="table-5-defined-sharedpagesdll"></a>表 5. Defined SharedPages.dll  

|**ID**|**描述**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) 为 Active Directory® 域服务 (AD DS) 中的一组有限功能提供一个外观|  
|**ID_CpuInfo**|(**ICpuInfo**) 确定你的 CPU 是 32 位还是 64 位|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) 有一些用于检查是否允许一组凭据加入域的方法|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) 使用 WMI 获取计算机上的驱动器列表|  
|**ID_WiredNetworkTask**|(**ITask**) 检查是否使用硬连线（而不是无线）网络适配器连接到网络的任务|  

#### <a name="control-components"></a>控件组件  
 可通过 GetControlWrapper 模板函数与页面上的控件进行交互，该函数提供对表 6 中列出的某一组件类型的访问。  

### <a name="table-6-components"></a>表 6. 组件数  

|**对话框控件类型**|**描述**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) 用于复选框控件的外观|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) 组合框控件的外观|  
|**CONTROL_GENERIC**|(**IControl**) 可通过它使用大多数类型的控件，以便控制启用和可见状态|  
|**CONTROL_LIST_VIEW**|(**IListView**) 可提供对列表视图控件功能的访问的外观|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) 用于进度栏控件位置的外观|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) 用于单选按钮控件的外观|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) 一个提供控件（如标签或文本框）文本读/写权限的外观|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) 用于树状视图控件的外观|  

#### <a name="image-list-component"></a>图像列表组件  
 该组件是页面上 ImageList 控件的外观。 通过 IListView 或 ITreeView 接口创建图像列表。  

#### <a name="formcontroller-component"></a>FormController 组件  
 该向导会创建此组件并将其传递到你的页面。 可使用 Form 方法（由 WizardPageImpl 基类实现）从页面访问该组件。  

#### <a name="invalidcharactervalidator-component"></a>InvalidCharacterValidator 组件  
 这是一种类型的验证程序，可包含在页面中。 ID 为 ID_InvalidCharactersValidator（在 IValidator.h 中定义），其文本值为“Microsoft.Wizard.Validation.InvalidChars.”  

 此验证程序查找名为 InvalidChars 的单个属性（.config 文件中的 Setter 元素），它是不被允许的字符的列表。 它检查文本框中的字符；如果文本包含此列表中的任何字符，则该组件会报告失败。  

#### <a name="nonemptyvalidator-component"></a>NonEmptyValidator 组件  
 这是一种类型的验证程序，可包含在页面中。 ID 为 ID_NonEmptyValidator（在 IValidator.h 中定义），其文本值为“Microsoft.Wizard.Validation.NonEmpty.”  

 如果文本框（或支持 IStaticText 的任何其他控件）有空字符串值，则此验证程序将报告失败。  

#### <a name="passwordvalidator-component"></a>PasswordValidator 组件  
 这是一种类型的验证程序，可包含在页面中。 ID 为 ID_PasswordValidator（在 IValidator.h 中定义），其文本值为“Microsoft.Wizard.Validation.Password.”  

 此验证程序使用两个不同的文本控件（支持 IStaticText 的控件），如果它们包含的值不同，则会报告失败。 换言之，如果“密码”和“确认密码”文本框不匹配，则会失败。  

 由于此验证程序需要两个控件，因此需要的设置比其他验证程序更多。 这些设置可能与以下所示类似：  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 首先，将“确认密码”控件定义为“密码”控件的"子级"。 这样一来，如果窗体控制器禁用“密码”控件，它也将禁用“确认密码”控件。 接下来，将密码验证程序添加到窗体。 最后，为密码验证程序提供“确认密码”控件的接口。  

 由于需要两个控件，因此须使用代码而不是 .config XML 文件来设置此验证程序。  

#### <a name="regexvalidator-component"></a>RegExValidator 组件  
 这是一种类型的验证程序，可包含在页面中。 ID 为 ID_RegExValidator（在 IValidator.h 中定义），其文本值为“Microsoft.Wizard.Validation.RegEx.”  

 此验证程序将文本控件（支持 IStaticText ）的内容与正则表达式进行比较，如果文本与正则表达式不匹配，则会失败。  

 或者，可以将此验证程序与预定义的命名模式一起使用。 若要使用正则表达式，XML 必须包含名为 Pattern 的资源库属性。 若要改用命名模式，请使用设置为表 7 中某个值的名为 NamedPattern 的资源库。  

### <a name="table-7-named-pattern-setters"></a>表 7. 命名模式资源库  

|**模式**|**描述**|  
|-|-|  
|用户名|验证该文本是窗体域\用户还是 user@domain|  
|ComputerName|该名称的长度必须介于 1 到 15 个字符之间，并且不能包含一组字符（如 : 和 ?）|  
|工作组|该名称的长度必须介于 1 到 15 个字符之间，并且不能包含一组字符（如 =、+ 和 ?）|  

#### <a name="factoryregistry-component"></a>FactoryRegistry 组件  
 该组件跟踪所有类工厂和服务。 它实现 IFactoryRegistry 接口，通过页面的 Container 方法间接提供。 此外，注册表加载扩展 DLL。 在它加载 DLL 后，注册表会查找名为 RegisterFactories 的导出函数。 必须实现此函数，并在其中为页面、任务和验证程序注册类工厂（以及要注册的任何其他类工厂）。 以下是示例项目的一个示例：  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Logger 组件  
 该组件通过 Logger 方法（由 WizardPageImpl 实现）提供给你的页面。 使用此方法将条目写入日志文件。 日志文件的内容对于诊断用户在运行 UDI 向导时可能遇到的问题会非常有用。  

#### <a name="propertybag-component"></a>PropertyBag 组件  
 属性包是内存变量的容器。 可使用 Container()->Properties() 从页面中获得它。 若要在不同页面之间传递临时数据，内存变量会非常有用。  

#### <a name="tsvariablebag-and-tsrepository-components"></a>TSVariableBag 和 TSRepository 组件  
 可通过 TSVariableBag 组件读取和写入任务序列变量。 默认情况下，它将值保存在内存中，直到用户单击“完成”。 可通过页面的 TSVariables 方法（由 WizardPageImpl 基类实现）访问 TSVariable 包。 这些组件记录任务序列变量的所有读取和写入。  

#### <a name="wmirepository-component"></a>WmiRepository 组件  
 该组件提供一个用于 WMI 查询的外观。 可使用 ID_WmiRepository 调用 CreateInstance 帮助程序函数以获取此组件的实例，它支持 IWmiRepository 接口。 该组件通过 IWmiIterator 接口返回结果记录。  

###  <a name="WizardPageHelperClasses"></a> 向导页帮助程序类  
 可使用 UDI SDK 提供的内置帮助程序类来创建自定义 UDI 向导页。 表 8 列出了可用于创建自定义向导页的帮助程序类。  

### <a name="table-8-helper-classes"></a>表 8. 帮助程序类  

|**帮助程序类**|**描述**|  
|-|-|  
|[ClassFactoryImpl 类](#ClassFactoryImplClass)|它是用于创建类工厂的有用基类，可注册到工厂注册表。|  
|[Interface 模板类](#InterfaceTemplateClass)|若要生成实现多个接口的组件，请使用此模板类。|  
|[Path 帮助程序类](#PathHelperClass)|此类提供常见的文件/目录操作。|  
|[Pointer 模板类](#PointerTemplateClass)|此类为 COM 组件中的生存期管理提供引用计数。 请务必在完成时发布接口。 此模板类会自动处理生存期。|  
|[PUnknown 类](#PUnkownClass)|此类是专门针对 IUnknown 接口的智能指针。 对于所有其他接口，请使用 Pointer 模板类。|  
|[StringUtil 帮助程序类](#StringUtilHelperClass)|此类提供帮助程序方法，可以更轻松地处理字符串。|  
|[SubInterface 模板类](#SubInterfaceTemplateClass)|对于本身继承自其他接口的接口，此基类可以更轻松地实现支持它的组件。|  
|[UnknownImpl 模板类](#UnknownImplTemplateClass)|此类处理创建 COM 组件的大部分细节。|  
|[WizardComponent 模板类](#WizardComponentTemplateClass)|此基类用于创建需要访问向导服务的组件，例如组件的创建和日志记录。|  
|[WizardPageImpl 模板类](#WizardPageImplTemplateClass)|此基类应用作所有自定义向导页的基类|  

####  <a name="ClassFactoryImplClass"></a> ClassFactoryImpl 类  
 它是用于创建类工厂的有用基类，可注册到工厂注册表。  

 以下是示例项目中 LocationPage.h 文件的摘录，用于定义 ClassFactoryImpl 类。  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 以下是示例向导页中 LocationPage.cpp 文件的摘录，用于定义该页面的类工厂。  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> Interface 模板类  
 若要生成实现多个接口的组件，请使用此模板类，例如：  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 对于 IFieldCalback 以及 WizardPageImpl 支持的接口，此代码会创建支持它们的基类链（正好是 IWizardPage）。  

####  <a name="PathHelperClass"></a> Path 帮助程序类  
 此类提供常见的文件/目录操作：  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 它还会使用提供给此方法的实例图柄返回 .exe 或 .dll 文件的完整路径：  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 此类使用提供给此方法的实例图柄返回 .exe 或 .dll 文件的完整路径和文件名：  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 。 。 。 或仅返回不包含文件名的路径：  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 如果文件名中包含路径，则路径帮助程序类仅返回文件名：  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 最后，此类返回一个新的字符串，它是组合的路径和文件名（或另一个路径）。  

####  <a name="PointerTemplateClass"></a> Pointer 模板类  
 在 Pointer.h 中定义此类。 因为 COM 组件使用引用计数来执行生存期管理，所以完成时请务必发布接口。 Microsoft 提供自动处理生存期的模板类。 例如，如果需要 XML 接口的智能指针，则可以编写与以下所示类似的内容：  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 第一行定义智能指针。 第二行显示通过另一个调用检索智能指针。 如果 & 运算符包含一个接口并返回内部指针的地址，它始终会发布一个现有接口。 检索到这样的指针后，如果变量超出范围，指针实例则会调用 Release。 Microsoft 建议你使用智能指针而不是手动调用 AddRef 和 Release。  

 另外，Pointer 智能指针类会调用 QueryInterface 来检索其他接口。 例如，当工厂注册表创建组件的新实例时，它会有与以下所示类似的代码：  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 第一行在后台调用 QueryInterface 以请求 IWizardComponent 接口。 如果组件不支持该接口，则生成的智能指针将等于 nullptr。  

####  <a name="PUnkownClass"></a> PUnknown 类  
 此类是专门针对 IUnknown 接口的智能指针。 对于所有其他接口，请使用 Pointer 模板类。  

####  <a name="StringUtilHelperClass"></a> StringUtil 帮助程序类  
 在 Utilities.h 中定义此类，它提供帮助程序方法，可以更轻松地处理字符串：  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 此方法对两个字符串进行比较，同时忽略大小写（请参阅表 9）。  

### <a name="table-9-stringutil-helper-class"></a>表 9. StringUtil 帮助程序类  

|**返回**|**描述**|  
|-|-|  
|**0**|字符串相匹配，忽略大小写|  
|**<0**|第一个 < 第二个|  
|**>0**|第一个 > 第二个|  

 下面是一个示例：  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 这些方法与 Microsoft .NET Format 方法有些类似，因为参数的形式都为“{0}”。 但是，它们不对输入执行任何格式设置，只进行替换：  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 这些是 StringCchPrintf 的包装器，它们返回一个 wstring ，因此不必自行为字符串或缓冲区分配内存。  

####  <a name="SubInterfaceTemplateClass"></a> SubInterface 模板类  
 对于本身继承自其他接口的接口，此基类可以更轻松地实现支持它的组件。 例如，ICheckBox 接口继承自 IControl。 以下演示如何使用此类定义 CheckBoxWrapper：  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 基接口是第一个参数，而派生的接口是第二个参数。  

####  <a name="UnknownImplTemplateClass"></a> UnknownImpl 模板类  
 在 UnknownImpl.h 中定义此类，它处理创建 COM 组件的大部分细节。 以下示例介绍如何用此基类：  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 此代码定义支持 IDirectory 接口的类。  

####  <a name="WizardComponentTemplateClass"></a> WizardComponent 模板类  
 在 IWizardComponent.h 中定义此类，对于创建需要访问向导服务的组件（例如组件的创建和日志记录），它是非常有用的基类。  

 以下是如何定义 CopyFilesTask 组件的示例：  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 在任务为 ITask 的情况下，此模板类的参数是要用于组件的“主”接口。 使用 WizardComponent 表示组件支持你提供的接口（本例中为 ITask ）和 IWizardComponent。  

 每当使用类工厂注册表创建新组件时，注册表都会调用组件的 IWizardComponent->SetContainer 方法，以便向组件提供对向导服务的访问。  

####  <a name="WizardPageImplTemplateClass"></a> WizardPageImpl 模板类  
 将此类用作自定义页的基类，例如：  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 此参数是对话框模板的资源 ID。  

###  <a name="WizardPageInterfaces"></a> 向导页接口  
 UDI 向导使用接口来访问页面上的不同控件。 在页面中，使用 GetControlWrapper 函数检索控件包装器。 下面是一个示例：  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 此处，PStaticText 是指向 IStaticText 接口的智能指针。 当智能指针超出范围或者将变量的地址（如 &pFormat ）传递给某个方法时，它会自动调用 COM Release() 方法。  

#### <a name="iadhelper-interface"></a>IADHelper 接口  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 初始化此组件，将其传递给记录器，以便记录信息。  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 此方法验证一组凭证是否有效，如表 10 所示。  

### <a name="table-10-hresultvalidlogon"></a>表 10. HResultValidLogon  

|**HResult**|**描述**|  
|-|-|  
|S_OK|凭据有效|  
|S_FALSE|凭据无效|  
|E_FAIL|找不到域控制器；请查看日志了解详细信息|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 此方法验证一组凭证是否对 AD DS 中的计算机对象具有读/写权限，如表 11 所示。  

### <a name="table-11-hresult-hasaccess"></a>表 11. HResult HasAccess  

|**HRESULT**|**描述**|  
|-|-|  
|S_OK|用户具有访问权限|  
|E_FAIL|用户没有访问权限。 请查看日志文件，了解其他信息。|  

#### <a name="ibackgroundtask-interface"></a>IBackgroundTask 接口  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>概述  
 “进度”页使用此类在单独的线程上运行任务。 如果要在单独的线程上执行操作，也可使用该类。 Task 是支持 ITask 接口的任何类。  

 此接口由 ID_BackgroundTask （“Microsoft.Wizard.BackgroundTask”）组件实现，在 IBackgroundTask.h 接口中进行定义。  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 此接口初始化该组件，如表 12 所示。  

### <a name="table-12-hresult-init"></a>表 12. HRESULT Init  

|**参数**|**描述**|  
|-|-|  
|**pTask**|指向类（该类包含要在另一个线程上运行的代码）的指针|  
|**Id**|可在回调的 Finished 方法中使用的数字，用于指示完成运行的任务；如果使用相同的回调方法启动多个任务，那么它会非常有用|  
|**pCallback**|实现 Finished 方法的类，每当任务完成运行时都会调用该方法；将在后台线程而不是 UI 线程上调用 Finished 方法|  

##### <a name="void-startvoid"></a>void Start(void)  
 此方法在后台线程上启动任务并返回表 13 中所示的元素。  

### <a name="table-13-return-background-thread"></a>表 13. 返回后台线程  

|**返回**|**描述**|  
|-|-|  
|**E_INVALIDARG**|已经正在运行该任务，因此无法立即启动。|  
|**E_FAIL**|启动线程时出错。|  
|**S_OK**|已启动线程。|  

##### <a name="bool-running"></a>BOOL Running()  
 如果后台任务正在运行，则此方法返回 TRUE；如果未运行，则返回 FALSE。  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 此方法会一直等待，直到线程停止运行或毫秒数结束。  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 此方法会终止正在运行的线程（请参阅表 14 和表 15）。 此方法返回后，可能需要一小段时间才能完成此过程。  

### <a name="table-14-hresult-terminate-exit-code"></a>表 14. HRESULT 终止退出代码  

|**参数**|**描述**|  
|-|-|  
|**exitCode**|可发送到 Finished 回调方法的退出代码，它也可通过 GetExitCode 方法提供。|  

### <a name="table-15-termination-codes"></a>表 15. 终止代码  

|**返回**|**描述**|  
|-|-|  
|**E_FAIL**|终止调用失败。|  
|**S_OK**|已成功请求终止线程。|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 使用此方法获取在后台线程上运行任务的结果（请参阅表 16）。  

### <a name="table-16-result-codes"></a>表 16. 结果代码  

|**参数**|**描述**|  
|-|-|  
|**pCode**|返回时，将设置指向 DWORD 的指针，如果不需要返回值则会设置为 nullptr。 退出时，如果线程正在运行，则此参数设置为 STILL_ACTIVE；如果调用此方法，则为任务的 Execute 方法返回的代码或传递给 Terminate 方法的值。|  
|**pHresult**|返回时，将设置指向 HRESULT 的指针，如果不需要 HRESULT 值则会设置为 nullptr。|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 此方法发布后台线程。 如果线程当前正在运行，它会返回 E_INVALIDARG，否则返回 S_OK。  

#### <a name="icheckbox-interface"></a>ICheckBox 接口  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 设置复选框的选中状态。 当方法为 TRUE 时，选中复选框；当方法为 FALSE 时，清除复选框。  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 此方法报告复选框当前的复选状态。  

#### <a name="icombobox-interface"></a>IComboBox 接口  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 CheckBoxWrapper 组件实现。 使用类型为 CONTROL_COMBO_BOX 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 当有一个实现 IBindableList 接口的数据源时使用此方法。 列表框使用此列表中的标题初始化内容。  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 在索引处选择组合框中的项。  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 如果未选择任何内容，则此方法会返回所选项的索引或 -1。  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR caption)  
 手动将项目添加到组合框。  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 在组合框中检索当前选定项的字符串。  

##### <a name="void-clear"></a>void Clear()  
 从组合框中删除所有项。  

#### <a name="icontrol-interface"></a>IControl 接口  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 ControlWrapper 组件实现。 使用类型为 CONTROL_GENERIC 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 启用或禁用控件。  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 如果启用控件，则返回 TRUE，否则返回 FALSE。  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 显示或隐藏控件。  

#### <a name="icpuinfo-interface"></a>ICpuInfo 接口  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>概述  
 可通过创建一个新的 ID_CpuInfo 组件来获得此接口。 单个方法报告 CPU 是 32 位还是 64 位。 注意，如果在 64 位的计算机上有 32 位的操作系统，则此方法返回 TRUE，因为它只报告 CPU（而非操作系统）的宽度。  

##### <a name="idirectory-interface"></a>IDirectory 接口  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>概述  
 使用 ID_Directory 创建的 Directory 组件提供用于文件系统中的目录的外观。  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 如果存在一个使用你提供的名称的文件，则此方法返回 TRUE。  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 此方法为你所提供的名称查找首次匹配项。 它支持通配符并返回文件和目录名。 如果找到匹配项，则该方法返回 TRUE，否则返回 FALSE。  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 此方法通过调用 FindFirst 或 FindNext 来检索找到的文件的名称。  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 此方法返回最新找到的文件或目录的特性。 可使用如下代码来测试它是否为目录：  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 查找下一个。 如果找到其他匹配项，则该方法返回 TRUE，否则返回 FALSE。  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 此方法发布用于 Find 操作的资源。  

#### <a name="idomainjoinvalidator-interface"></a>IDomainJoinValidator 接口  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>概述  
 可使用 CreateInstance 模板函数的 ID_DomainJoinValidator 值来获取此接口的实例。  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 初始化该实例，如表 17 所示。  

### <a name="table-17-hresult-init---instance-initialization"></a>表 17. HRESULT Init - 实例的初始化  

|**参数**|**描述**|  
|-|-|  
|**pLogger**|记录器实例，可通过页面的 **Logger** 方法提供给你的页面|  
|**pContainer**|从页面的 Container 方法传递结果|  
|**pUsername**|包含要验证的用户名的文本框|  
|**pPassword**|包含要验证的密码的文本框|  
|**PComputerName**|包含计算机（最终将加入域）的名称的文本框|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 此方法使用 IADHelper->ValidLogon 方法来执行此操作。 有关详细信息，请参阅该方法。  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 验证用户是否有权修改计算机条目。 大部分工作由 IADHelper->HasAccess 完成。 如果此方法返回 FALSE，请查看日志文件，了解详细信息。  

#### <a name="idrivelist-interface"></a>IDriveList 接口  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 在调用任何其他组件之前，先调用此方法。 在调用此方法之前，需要先创建一个新的 WmiRepository。  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 通过此方法可添加将在查询中显示为“where”子句的文本。 例如，以下行仅返回 USB 驱动器：  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 为将从查询返回的驱动器设置最小化的驱动器大小（以字节为单位）。  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 执行查询。 调用此方法后提供的驱动器列表按驱动器号进行排序。  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 此方法添加要在查询结果中提供的其他属性的名称。 在调用 Update 之前，先调用此方法。 表 18 显示了三个有用的属性。  

### <a name="table-18-hresult-addproperty-useful-properties"></a>表 18. HRESULT AddProperty：有用属性  

|**Section**|**属性**|**描述**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Size**|大小（以字节为单位），用字符串来表示|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|磁盘号使用从 0 开始的整数来表示|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|卷标|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 查询返回的记录数。 在调用此方法之前，先调用 Update。  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value)  
 此方法从查询结果中检索属性的值，如表 19 所示。  

### <a name="table-19-hresult-getproperty"></a>表 19. HRESULT GetProperty  

|**参数**|**描述**|  
|-|-|  
|**Index**|结果记录的从零开始的索引|  
|**propName**|属性的名称，如“Size”|  
|**值**|返回时，此参数包含属性的变量值|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index,  LPBSTR pCaption)  
 此方法检索与 Caption 属性相同的记录的标题。  

#### <a name="iimagelist-interface"></a>IImageList 接口  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 ImageList 组件实现。 从 IListView 接口检索此组件的实例。  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 创建该组件管理的新图像列表。 只调用一次此方法。  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 如果需要在图像列表上执行其他操作，则此方法返回图像列表的图柄。  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HInstance hInstance, int resourceId)  
 将新图像添加到某个资源的图像列表中，如表 20 所示。  

### <a name="table-20-hresult-iimagelist-interface"></a>表 20. HRESULT IImageList 接口  

|**参数**|**描述**|  
|-|-|  
|**hInstance**|包含位图资源的模块的实例图柄|  
|**resourceId**|要加载到图像列表中的资源 ID|  

#### <a name="ilistview-interface"></a>IListView 接口  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 ControlWrapper 组件实现。 使用类型为 CONTROL_LIST_VIEW 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 将新行添加到列表框中。 该方法返回刚添加的项的索引。  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 将新列添加到列表视图。  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 在除列表框第一列之外的某列中设置文本，如表 21 所示。  

### <a name="table-21-hresult-setsubitem"></a>表 21. HRESULT SetSubItem  

|**参数**|**描述**|  
|-|-|  
|**index**|要修改的列表项的索引|  
|**column**|要更新的列的索引；第一列使用 AddItem 设置，第二列及后续列使用此方法设置|  
|**text**|要在列中显示的字符串|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 此方法返回整个文本框的宽度。  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 通过此方法可在列表框中设置扩展的样式，例如：  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 此方法返回当前选定的列表视图项的索引。  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 将列表中的选定项设置为此索引。  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 如果选中列表中的某个项，则此方法返回 TRUE。 此方法需要调用 SetExtendedStyle 以设置复选框样式。  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 此方法返回列表视图中的项数。  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 创建一个新的图像列表，并将其附加到列表视图。  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 将图像添加到列表视图的图像列表。 首先，需要调用 CreateImageList。  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 为特定的列表视图项设置要在左侧显示的图像。  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 从列表视图中移除所有项。  

#### <a name="iprogressbar-interface"></a>IProgressBar 接口  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 ProgressBarWrapper 组件实现。 使用类型为 CONTROL_PROGRESS_BAR 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 使用介于 0 和 100 之间的数字设置进度栏的位置。 默认情况下，新的 Win32® 进度条的最大范围为 100。  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 此方法返回进度栏的当前位置。  

#### <a name="iradiobutton-interface"></a>IRadioButton 接口  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 RadioButtonWrapper 组件实现。 使用类型为 CONTROL_RADIO_BUTTON 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int firstId, int lastId)  
 为包装器提供应视为组的单选按钮的范围。 在调用 CheckRadio 之前，先调用此方法。  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 将特定的单选按钮设置为所选单选按钮组中的单个按钮。 在调用此方法之前，先调用 SetGroup。  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 如果当前已选定该单选按钮，则此方法返回 TRUE，否则返回 FALSE。  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 此方法启用或禁用单选按钮。  

#### <a name="istatictext-interface"></a>IStaticText 接口  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 StaticTextWrapper 组件实现。 使用类型为 CONTROL_STATIC_TEXT 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 设置控件的文本。  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 此方法返回控件文本的当前值。  

####  <a name="ITaskinterface"></a> ITask 接口  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 如果希望组件用作预检页中的某个任务，或者希望使用 BackgroundTask 组件在后台线程上执行工作，则实现此接口。  

 以下是实现 ITask 接口的组件：  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>初始  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 如果正在为预检页编写任务，则调用此方法来初始化任务。 .config 文件包含的 XML 可能与以下所示类似：  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 pProperties 参数提供对三个资源库值的访问，而 pTaskSettings 参数提供对 Task 元素和子元素的访问。 大多数任务只需通过 pProperties 参数读取数据。  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 这是编写执行任务的代码的位置。 如果没有出现错误，此方法应返回 S_OK；如果在任务运行期间出现错误，则此方法可返回另一个 HRESULT。 如果正在使用预检页，则此方法返回的 S_OK 以外的值与 <ExitCodes\> 节中的 <Error\> 元素匹配。  

 pReturnCode 参数必须更新为含有可报告任务状态的数字。 这些值通过预检页与 <ExitCode\> 元素进行匹配。  

#### <a name="itreeview-interface"></a>ITreeView 接口  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 TreeViewWrapper 组件实现。 使用类型为 CONTROL_TREE_VIEW 的 GetControlWrapper 帮助程序函数检索此组件的实例。  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 此方法通过设置 TVS_CHECKBOXES 样式来打开树状视图控件中的复选框。  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 将新的图像列表添加到树状视图控件。 在对 ImageList_Create Win32 函数的调用中传递 flags 参数。  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 在具有 hInstance 实例图柄的模块中，将图像从某个资源 (resourceId) 添加到图像列表。  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 将节点添加到树状视图。 如果 hParent 为 NULL，则新节点将添加到顶级。 否则，将图柄提供给要添加新项的父项。 此方法将图柄返回给新项。  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 设置要用于树状视图项的图像。 可设置正常图像和展开图像。  

##### <a name="void-clearvoid"></a>void Clear(void)  
 从树状视图中移除所有项。  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 确保树状视图项可见。 如果需要将该项设置为可见，则树状视图将滚动。  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 将当前选定项设置为所提供的项。 在此之后，可调用 SetFirstVisible，确保新选定的项可见。  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 此方法主要设置将在树状视图中针对复选框显示的图像。 这些图像位于单独的 ImageList 控件（由树状视图管理）中。 默认情况下，该图像列表中有三个图像，如表 22 所示。  

### <a name="table-22void-checkitem-image-list-default"></a>表 22. void CheckItem 图像列表默认值  

|**复选状态**|**描述**|  
|-|-|  
|**0**|空|  
|**1**|清除|  
|**2**|选定|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 此方法返回当前选定的树状视图项的索引。  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 此方法设置树状视图控件中所有项的高度（以像素为单位）。 它返回以前的高度（以像素为单位）。  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 此方法启用或禁用树中的单个项。 禁用含子级的项不会禁用子项。  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 此方法展开或折叠树中的节点。  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 此方法返回树状视图项的第一个子级；如果没有子级，则返回 NULL。  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 此方法返回树状视图中节点的父级图柄；如果节点位于顶层，则返回 NULL。  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 可使用 GetChild 返回的图柄调用此方法，用于循环访问节点的所有子级。 此方法返回树中共享相同父级的下一个同层级。  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 如果未选择树状视图节点，则此方法返回 0，如果已选择，则返回 1。  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 如果启用树状视图节点，则此方法返回 TRUE；否则，此方法返回 FALSE。  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 此方法仅供内部使用。  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 如果要在选定项发生更改或用户更改树状视图项的复选状态时接收通知，请调用此方法。 必须在组件中实现 ITreeViewEvent 以接收这些回调。  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 设置选定项使用的背景色。  

#### <a name="iwmiiteration-interface"></a>IWmiIteration 接口  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>概述  
 在使用 WMI 调用时，通常使用此接口以及 IWmiRepository。 通过 IWmiIteration 接口可以循环访问查询返回的值。  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 移动到查询结果中的下一项，如表 23 所示。  

### <a name="table-23-hresult-nextvoid-query-returns"></a>表 23. HRESULT Next(void) 查询返回  

|**HRRESULT**|**描述**|  
|-|-|  
|**S_OK**|移动到下一个结果；可使用 GetProperty 来检索该结果的属性。|  
|**S_FALSE**|列表中没有任何项。|  
|**E_NOT_SET**|没有查询结果|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 此方法从当前结果记录中检索属性的值，如表 24 和表 25 所示。  

### <a name="table-24-hresult-getproperty"></a>表 24. HRESULT GetProperty  

|**参数**|**描述**|  
|-|-|  
|**propertyName**|要检索的属性的名称|  
|**pValue**|指向返回时包含属性值的 VARIANT 结构|  

### <a name="table-25-hresult-getproperty-result"></a>表 25. HRESULT GetProperty 结果  

|**HRESULT**|**描述**|  
|-|-|  
|**S_OK**|已检索属性值。|  
|**WBEM_E_NOT_FOUND**|没有含该名称的任何属性。|  
|**E_NOT_VALID_STATE**|没有最新记录。|  

> [!NOTE]
>  GetProperty 方法可返回除表 25 中列出的其他 WMI 错误代码。 列出的值是返回的常见结果。  

#### <a name="iwmirepository-interface"></a>IWmiRepository 接口  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 WmiRepository 组件 (ID_WmiRepository) 实现。  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 此方法设置将用于此查询的 WMI 命名空间。 在调用 ExecQuery 之前，先调用此方法。 如果不调用此方法，则命名空间将为 root\cimv2。 此方法始终返回 S_OK。  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 通过调用 SetNamespace 来对 WMI 命名空间集执行某个查询，如表 26 和表 27 所示。  

### <a name="table-26-hresult-execquery"></a>表 26. HRESULT ExecQuery  

|**参数**|**描述**|  
|-|-|  
|**Query**|要执行 WMI 查询的字符串|  
|**ppIterator**|将指针传递给接口指针，这样返回时会使用接口进行填充，从而让你可以访问查询结果|  

### <a name="table-27-hresult-query-result"></a>表 27. HRESULT 查询结果  

|**HRESULT**|**描述**|  
|-|-|  
|**S_OK**|查询成功|  
|**Other**|如果查询未成功，则返回 WMI HRESULT|  

#### <a name="iformcontroller-interface"></a>IFormController 接口  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>概述  
 UDI 向导中的每个页面都有自己的窗体控制器，可用于实现此接口。 可使用此控制器将 .config XML 文件中的字段数据连接到页面上的控件。 然后，窗体控制器会处理大部分细节。  

#####  <a name="SettingUptheForm"></a> 设置窗体  
 通常情况下，采用页面的 OnWindowCreated 方法设置窗体控制器。 此操作通常涉及调用表 28 中所示的方法。  

### <a name="table-28-onwindowcreated-method"></a>表 28. OnWindowCreated 方法  

|**方法**|**描述**|  
|-|-|  
|**Init**|初始化窗体控制器|  
|**AddField**|提供在 .config XML 文件中作为字符串名称的字段和在页面对话框中作为 ID 的控件之间的连接|  
|**AddRadioGroup**|用于在对话框中将单选按钮连接到组和控件|  
|**AddToGroup**|将随其父级一同启用/禁用或基于选定的单选按钮的控件设置为“子级”|  
|**InitFields**|在调用了所有 Add 方法之后调用它来设置窗体|  
|**Validate**|执行初始验证|  

##### <a name="processing-form-events"></a>处理窗体事件  
 将以下调用添加到 OnControlEvent 方法中：  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 此调用将事件传递给窗体控制器，以便它处理与窗体相关的事件。  

##### <a name="save-form-data"></a>保存窗体数据  
 在 OnNextClicked 方法中，调用表 29 中所示的窗体方法。  

### <a name="table-29-onnextclicked-method"></a>表 29. OnNextClicked 方法  

|**方法**|**描述**|  
|-|-|  
|**InitSection**|提供将在此页面的“摘要”页上显示的节的名称|  
|**SaveFields**|将字段值保存到任务序列变量和“摘要”页|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 通常在页面的 OnWindowCreated 方法开始处附近调用此方法。 该命令应该与以下所示类似：  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 此方法在内部调用，而不应自行调用。 它将页面的 XML 提供给窗体控制器。  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 此方法执行所有附加到控件的验证程序。 如果验证程序没有通过，则窗体控制器将显示警告消息并禁用“下一步”按钮，然后停止处理验证程序。 通常情况下，只需在 OnWindowCreated 方法的末尾调用此方法；它始终返回 S_OK。  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 此方法将控件添加为复选框或单选按钮的“子级”，如表 30 中所示。 如果未选择父控件，则会禁用所有此类子控件。 此方法始终返回 S_OK。  

### <a name="table-30-addtogroup"></a>表 30. AddToGroup  

|**参数**|**描述**|  
|-|-|  
|**groupControlId**|复选框或单选按钮的 ID，它将控制子控件的启用状态|  
|**Controlld**|想要添加为子级的控件的 ID|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 此方法基于父控件的状态更新组的子控件的启用或禁用状态。 通常情况下，无需自行调用，因为窗体控制器会调用此方法。  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 只有希望使用代码而不是 XML 创建验证程序时才调用此方法。 此方法始终返回 S_OK。  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 只有希望使用代码而不是 XML 创建验证程序时才调用此方法。  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 调用此方法可显式禁用控件的验证程序或还原正常验证，如表 31 所示。 例如，如果对未涵盖在窗体验证内的控件设置启用/禁用规则，并且需要为控件禁用验证，此方法则会非常有用。 换言之，通常不会调用此方法。 此方法始终返回 S_OK。  

### <a name="table-31-hresult-disablevalidation"></a>表 31. HRESULT DisableValidation  

|**参数**|**描述**|  
|-|-|  
|**controlId**|要启用或禁用验证的控件|  
|**禁用**|设置为 TRUE 可禁用验证，设置为 FALSE 可还原正常验证|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 在 .config XML 文件中 Field 元素的名称与页面对话框中的控件 ID 之间添加控件映射，如表 32 所示。 在调用 InitFields 之前，必须先调用此方法，因为 InitFields 会使用此信息。 此方法始终返回 S_OK。  

### <a name="table-32-hresult-addfield"></a>表 32. HRESULT AddField  

|**参数**|**描述**|  
|-|-|  
|**Fieldname**|显示在页面的 XML 中的字段名称|  
|**controlId**|页面对话框模板中的控件的 ID|  
|**suppressLog**|如果不希望将该字段中的值写入日志文件，则设置为 TRUE；对于密码或 PIN 字段，始终将此参数设置为 TRUE|  
|**类型**|控件的类型为以下所列之一：<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 此方法将控件添加到已命名的单选按钮组，如表 33 所示。 在调用 InitFields 方法之前，必须先调用此方法，因为此方法使用 RadioGroup 元素上的特性来控制组中所有单选按钮控件的设置。 例如，可以锁定单选按钮组，从而禁用所有单选按钮，但仅根据选定的单选按钮启用或禁用子控件。 此方法始终返回 S_OK。  

### <a name="table-33-hresult-addradiogroup"></a>表 33. HRESULT AddRadioGroup  

|**参数**|**描述**|  
|-|-|  
|**groupName**|在此页面上定义一组单选按钮的字符串|  
|**radioControlId**|要添加到此组的单个单选按钮的 ID|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 可通过此方法启用或禁用整个单选按钮组。 禁用单选按钮组会禁用组中的所有单选按钮控件以及那些 AddToGroup 添加的单选按钮的任何子级。 请参阅表 34 和表 35。  

### <a name="table-34-enableradiogroup"></a>表 34. EnableRadioGroup  

|**参数**|**描述**|  
|-|-|  
|**groupName**|通过调用 AddRadioGroup 来定义的单选按钮组的名称|  
|**启用**|设置为 TRUE 可启用单选按钮组，设置为 FALSE 可禁用该组|  

### <a name="table-35-hresult-enableradiogroup"></a>表 35. HRESULT EnableRadioGroup  

|**HRESULT**|**描述**|  
|-|-|  
|**S_OK**|启用或禁用的组|  
|**E_INVALIDARG**|没有包含所提供名称的单选按钮组|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 在调用此方法之前，先为 XML 控制的每个字段调用 AddField。 此方法始终返回 S_OK。  

 pFieldCallback 参数为可选项。 如果提供该参数，对于不是 CONTROL_STATIC_TEXT 或 CONTROL_CHECK_BOX 的控件，窗体控制器则会为其调用 SetFieldDefault。 通过此行为，可以从 XML 中检索默认值，并在控件中自行设置该值。  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 此方法将字段值保存到任务序列变量和要在“摘要”页上显示的摘要数据。 通过在 pFieldCallback 中提供一个指针，可以为不支持 CONTROL_STATIC_TEXT 的控件处理保存值。  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 可通过此方法确定是否禁用 XML 中的字段。  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 此方法初始化要在“摘要”页上显示的摘要数据，如表 36 所示。 在调用 SaveFields 之前，先在 OnNextClicked 方法中调用此方法。 此方法始终返回 S_OK。  

### <a name="table-36-hresult-initsection"></a>表 36. HRESULT InitSection  

|**参数**|**描述**|  
|-|-|  
|**Key**|此参数对于你的页面来说应是唯一的。 它用于确保每个页面都有其自己的摘要信息。|  
|**sectionCaption**|将在此页面的摘要信息的“摘要”页上显示的标头。 通常情况下，使用 DisplayName() 作为此参数的值。|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 通过此方法，可以将使用 XML 设置的项以外的摘要项添加到“摘要”页。 请参阅表 37。  

### <a name="table-37-hresult-addsummaryitem"></a>表 37. HRESULT AddSummaryItem  

|**参数**|**描述**|  
|-|-|  
|**First**|摘要项的标题，显示在左侧|  
|**Second**|将在右侧显示的值|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 对于不希望将这些值写入日志文件中的任务序列变量，为其调用此方法。 对于存储用户可能输入的密码、PIN 或其他敏感值的任务序列变量，为其调用此方法。  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 此方法将文本控件的值保存到某个任务序列变量和摘要节。 通常情况下，无需自行调用，因为窗体控制器会为所有字段调用此方法。 请参阅表 38。  

### <a name="table-38-hresult-savetext"></a>表 38. HRESULT SaveText  

|**参数**|**描述**|  
|-|-|  
|**controlId**|文本框的 ID，它包含要保存的值（或任何其他可以返回文本的控件）|  
|**tsVariableName**|要修改的任务序列变量的名称|  
|**summaryCaption**|“摘要”页上此值的标题|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 此方法读取任务序列变量的值，并将文本框设置为该值。  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 在 OnControlEvent 方法上调用此方法，确保窗体控制器可以处理控件事件，它需要执行此操作才能正常工作。 传递给此方法的值与传递给 OnControlEvent 方法的值相同。  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 此方法返回窗体最新验证的状态。 如果任何控件验证程序报告了一个错误，则此方法返回 FALSE。 换言之，仅当页面上的所有控件都有效时才返回 TRUE。  

#### <a name="ivalidator-interface"></a>IValidator 接口  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>概述  
 验证程序是可以在页面上验证单个控件的组件。 实现验证程序最简单方法是将其设置为在 BaseValidator.h 头文件中定义的 BaseValidator 类的子类。  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 如果以代码形式创建验证程序，可以调用此方法来初始化验证程序。 请参阅表 39。  

### <a name="table-39-hresult-init"></a>表 39. HRESULT Init  

|**参数**|**描述**|  
|-|-|  
|**pControl**|验证程序必须验证的控件|  
|**Message**|控件无效时显示在页面上的消息|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 窗体控制器调用此方法来初始化基于页面的 XML 创建的验证程序。 请参阅表 40。  

### <a name="table-40-hresult-init-method"></a>表 40. HRESULT Init 方法  

|**参数**|**描述**|  
|-|-|  
|**pControl**|验证程序必须验证的控件|  
|**pContainer**|如果验证程序需要访问记录器或需要创建其他组件|  
|**pProperties**|为验证程序提供对属性（资源库元素）的访问|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 如果控件有效，该方法返回 TRUE；如果控件无效，则返回 FALSE。 返回时，应使用新的 BSTR（其中包含在控件无效时显示的消息）填充 pMessage。  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 如果需要未在 XML 中提供的额外值，则可以实现此方法。  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 如果需要未在 XML 中提供的额外值，则可以实现此方法。  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 如果需要未在 XML 中提供的额外值，则可以实现此方法。  

#### <a name="iregex-interface"></a>IRegEx 接口  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 此方法由 ID_Regex 组件 (IRegex.h) 实现并为正则表达式处理提供支持。  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 此方法对输入文本运行正则表达式。 它使用 C++ 标准库的 regex_match 函数来完成实际的工作。 如果有匹配项，该方法返回 TRUE；否则返回 FALSE。  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 通过此方法，可以从最新的 MatchesRegex 调用检索匹配项。 注意，此方法中没有错误处理，它会返回 S_OK 或引发异常。  

#### <a name="isummaryinfo-interface"></a>ISummaryInfo 接口  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 无需直接使用此接口。 请改用 IFormController。  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 无需直接使用此接口。 请改用 IFormController。  

#### <a name="itsvariablebag-interface"></a>ITSVariableBag 接口  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 此接口提供对任务序列变量的访问。 可使用页面的 TSVariables() 方法访问此接口。  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 此方法读取任务序列变量的值。  

> [!NOTE]
>  第一次读取后会缓存这些值。  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 此方法设置任务序列变量的值。 该值保存在内存中。 在 UDI 向导中单击“完成”后，会写入任务序列值。  

##### <a name="void-clearvoid"></a>void Clear(void)  
 此方法删除已保存在内存中的所有任务序列值。  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 此方法从内存中删除特定的任务序列值。 下次使用相同的任务序列名称调用 GetValue 时，此方法会尝试从任务序列中对其进行检索。  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 每当写入任务序列变量（如在 UDI 向导中单击“完成”）时，名称和值都会写入日志文件。 调用此方法来禁止记录特定任务序列变量的敏感值（如密码或 PIN）。  

##### <a name="void-savevoid"></a>void Save(void)  
 此方法保存通过调用 SetValue 设置的所有任务序列值。  

#### <a name="itsvariablerepository-interface"></a>ITSVariableRepository 接口  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 此接口供 TSVariableBag 在内部使用，用于读取和写入任务序列变量。  

#### <a name="iwizardfinish-interface"></a>IWizardFinish 接口  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 如果希望在 UDI 向导中单击“完成”或“取消”时执行其他处理，针对这样的高级方案，此接口会非常有用。 UDI 向导包含一个 Finish 任务，单击“完成”时，该任务会保存任务序列变量。 如果取消向导，该任务只将 OSDSetupWizCancelled 任务序列变量设置为 TRUE，并且不会保存对任何其他任务序列变量的更改。  

 如果创建自己的 finish 组件，则需要使用与以下类似的代码注册该组件：  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>IBindableList 接口  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 如果想要通过调用某个数据源组件的 Bind 方法来将它绑定到组合框，请实现此接口。  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 此方法返回列表中的项数。  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 此方法返回特定索引处的项的标题。  

#### <a name="idatanodes-interface"></a>IDataNodes 接口  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 对于可保存在页面中的层次结构数据，此接口提供对其的访问。 可通过 ISettingsProperties 接口上的方法获取此接口，它通过 Settings 方法提供给你的页面。  

 页面的 XML 中的数据可能与此类似  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 通过调用 Settings()->GetDataNode(L"Network", &pData)，可获得含两个数据项（每个数据项都有两个属性）的 IDataNodes 实例。  

##### <a name="sizet-count"></a>size_t Count()  
 此方法返回 DataItem 元素的数量。  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 支持此接口的组件也支持 IBindableList ，这样便于使用页面的 XML 中的数据填充组合框。 此方法控制每个 DataItem 元素中用于此绑定的具体属性（资源库）。 例如，可使用 DisplayName 调用此方法，它会使用该资源库属性绑定数据。 然后，组合框将包含 Public 和 Dev Team 作为项。  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 此方法从某个 DataItem 元素中获取属性。 请参阅表 41 和表 42。  

### <a name="table-41-dataitem-getproperty"></a>表 41. DataItem GetProperty  

|**参数**|**描述**|  
|-|-|  
|**Index**|要为其检索属性值的 DataItem 的索引值（从 0 开始）|  
|**propertyName**|要为其检索值的资源库属性的名称|  
|**propertyValue**|返回时，包含属性的字符串值|  

### <a name="table-42-hresult-getproperty"></a>表 42. HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**描述**|  
|**S_OK**|已检索该属性。|  
|**E_INVALIDARG**|索引超出数组的末尾。|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 此方法类似于 GetProperty ，但不是从 DataItem 返回一个值，而是返回包装在 ISettingsProperties 接口中的整个 DataItem。 请参阅表 43 和表 44。  

### <a name="table-43-hresult-getnode"></a>表 43. HRESULT GetNode  

|**参数**|**描述**|  
|-|-|  
|索引|要为其检索属性值的 DataItem 的索引值（从 0 开始）|  
|**ppNode**|退出时，包装 DataItem 节点的 ISettingsProperties 接口|  

### <a name="table-44-hresult-getnode-results"></a>表 44. HRESULT GetNode 结果  

|**HRESULT**|**描述**|  
|-|-|  
|**S_OK**|已检索到节点。|  
|**E_INVALIDARG**|索引超出数组的末尾。|  

#### <a name="ifactoryregistry-interface"></a>IFactoryRegistry 接口  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>概述  
 创建新的自定义页面时，至少需要创建一个 page factory（它是实现 IClassFactory 的类）。 （可使用 ClassFactoryImpl 作为工厂的基类。）  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type,  IClassFactory \*pFactory)  
 此方法向注册表注册一个类工厂。 请参阅表 45。  

### <a name="table-45-iclassfactory-void-register"></a>表 45. IClassFactory void 注册  

|**参数**|**描述**|  
|-|-|  
|**类型**|一个字符串，它标识要注册的工厂；通常情况下，该参数在字符串中应包含公司名称，以确保其唯一性|  
|**pFactory**|指向类工厂实例的指针|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 此方法仅供内部使用。  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 此方法通常仅供内部使用。 它检查是否已为类型注册类工厂。  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory)  
 可通过此方法检索类工厂。 通常情况下，将调用 CreateInstance。 但是，如果要创建大量相同的组件，它可以更高效地检索工厂，然后让其创建实例。  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance)  
 此方法创建组件的新实例（如果给定其类型）。 改用 CreateInstance 模板方法，可通过它创建类型安全的对象。  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 此方法仅供内部使用。  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 Services 是可在多个位置使用的组件的单个实例。 可使用此方法在一个页面上注册服务，然后从另一个页面检索相同的实例。  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid,  IUnknown **ppService)  
 此方法检索以前通过调用 RegisterService 注册的服务。  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 此方法将 UDI 向导的语言设置为 languageId 参数中提供的语言标识符。  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 此方法返回 UDI 向导的 /locale 命令行参数提供的语言标识符的值。 此方法返回下列某个值：  

-   /locale 命令行参数提供的语言标识符的值  

-   如果未提供 /locale 命令行参数，则为 0  

#### <a name="ilogger-interface"></a>ILogger 接口  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>概述  
 UDI 向导将信息记录到日志文件，这有助于解决字段中发现的问题。 这是页面记录信息的好方法。 可使用页面的 Logger() 方法从页面内获取指向此接口的指针。 日志文件中的行包含一个“级别”号，用于表示错误、普通、详细或调试消息。  

> [!NOTE]
>  调试消息不会保存到日志文件中，除非打开调试支持。 可将以下行添加到 .config 文件的 Style 元素中，打开调试支持：  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>初始  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 此方法仅供内部使用。  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 此方法仅供内部使用。  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 此方法仅供内部使用。  

##### <a name="log"></a>日志  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 此方法仅供内部使用。  

##### <a name="error"></a>错误  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 调用此方法可记录有关错误的信息。 请参阅表 46。  

### <a name="table-46-hresult-error"></a>表 46. HRESULT 错误  

|**参数**|**描述**|  
|-|-|  
|**错误**|由调用返回的错误代码（此代码在日志项目中显示为数字。）|  
|**组件**|一个字符串，它标识错误的源（通常为编写的页面或组件）|  
|**Message**|解释导致错误的原因的消息|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 此方法与 Error 方法类似，但通过它可以提供两部分构成的消息。 最后一条消息将有“message”，然后在输出文件中是“message2”。 这是一种简便的方法。  

##### <a name="normal"></a>普通  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 此方法记录普通消息。 有关参数，请参阅 [Error](#Error) 方法的说明。  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 此方法记录普通消息。 有关参数，请参阅 [Error2](#Error2) 方法的说明。  

##### <a name="verbose"></a>详细  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 此方法记录详细消息。 有关参数，请参阅 [Error](#Error) 方法的说明。  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 此方法记录详细消息。 有关参数，请参阅 [Error2](#Error2) 方法的说明。  

##### <a name="debug"></a>调试  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 此方法记录调试消息。 有关参数，请参阅 [Error](#Error) 方法的说明。 调试消息只有启用后才保存到文件。 请参阅“概述”部分了解详细信息。  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 此方法仅供内部使用。  

##### <a name="close"></a>关闭  

```  
HRESULT Close(void)  
```  

 此方法仅供内部使用。  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 此方法检索日志文件的名称。  

#### <a name="iorientation-interface"></a>IOrientation 接口  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 此接口仅供内部使用。  

#### <a name="isettings-interface"></a>ISettings Interface接口  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 此接口仅供内部使用。  

#### <a name="isettingsproperties-interface"></a>ISettingsProperties 接口  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>概述  
 此接口提供对页面数据的访问。 要访问顶层页面数据，请使用页面的 Settings() 方法。  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName,  LPBSTR attributeValue)  
 可通过此方法检索主节点上的特性值，主节点是指在使用页面的 Settings() 方法时的“Page”节点。  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 此方法提供对主节点下的资源库属性值的访问。 对于页面来说，这些都是顶层属性。  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath,  IXMLDOMNodeList **ppList)  
 如果要使用 XPath 表达式直接获取 XML 节点的列表，请调用此方法。 如果可以，最好使用其他某个方法。 仅当无法以其他方式访问节点时才使用此方法。  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath,  IXMLDOMNode **ppNode)  
 如果要使用 XPath 表达式直接获取单个 XML 节点，请调用此方法。 如果可以，最好使用其他某个方法。 仅当无法以其他方式访问节点时才使用此方法。  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name,  ISettingsProperties **ppNode)  
 基于该元素的 Name 特性检索 Data 元素。  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 此方法检索当前节点下的 DataItem 元素的列表。 从页面级别中调用 GetDataNode，用于为数据检索 ISettingsProperty 接口。 然后，在该实例上调用 GetDataNodes，用于检索记录列表。 例如，给定此 XML：  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName,  IDataNodes **ppNodes)  
 可通过此方法快速访问特定 Data 节点下的 DataItem 节点集。 使用 GetDataNodes 示例中的 XML，则以下代码与 GetDataNodes 示例中的四行代码 的功能完全相同，但还提供错误检查：  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>ISimpleStringProperties 接口  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 就其本身而言，此接口可能没有用。 但是，它由 ID_SimpleStringProperties 组件实现，该组件还实现 IStringProperties 接口。 如果需要将一组属性传递给另一个组件（如任务），但希望以编程方式添加值而不是使用 XML中的值，则可以使用此组件。 以下示例介绍如何使用此接口：  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 对于来自 XML 的一组资源库元素，此接口提供对其的简单访问。 此接口适用于使用 Settings()->Properties() 的页面的属性。  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 此方法检索单个属性值。 请参阅表 47 和表 48。  

### <a name="table-47-ihresult-get-property-value"></a>表 47. IHRESULT Get 属性值  

|**参数**|**描述**|  
|-|-|  
|**propertyName**|要读取的属性的名称|  
|**pPropValue**|退出时，将属性值包含为字符串（如果没有此类属性，则该值为 nullptr。）|  

### <a name="table-48-ihresult-get-property-value-results"></a>表 48. IHRESULT Get 属性值结果  

|||  
|-|-|  
|**HRESULT**|**描述**|  
|**S_OK**|已检索属性值。|  
|**E_INVALIDARG**|没有包含所提供名称的属性。|  

#### <a name="itaskmanager-interface"></a>ITaskManager 接口  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 此接口由在预检页上运行任务的 TaskManager 组件（ITaskManager.h 中的 ID_TaskManager）实现。 可直接使用预检页（大多数时候是这种情况）或生成自己的页面来让该组件完成大部分工作。  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 在调用任何其他方法之前，必须先调用此方法。 它初始化 TaskManager 组件。 请参阅表 49。  

### <a name="table-49-hresult-init"></a>表 49. HRESULT Init  

|**参数**|**描述**|  
|-|-|  
|**pPageView**|提供对将要运行任务的页面的访问（此页面必须有一组特定的控件，在接下来的几个参数中会对其进行概述。）|  
|**idListView**|ListView 控件的控件 ID，它将显示任务列表及这些任务的状态|  
|**idMessage**|一个文本框的控件 ID，该文本框将用于为所选任务显示一条消息|  
|**idRetryButton**|一个按钮的控件 ID，单击该按钮，可再次运行任务|  
|**pPageInfo**|页面的 XML 的包装器（TaskManager 将从此 XML 中加载要运行的任务集。）|  
|**pCallback**|可以为 null（如果此参数不为 null，则 TaskManager 在启动任务时会调用 Started 方法，并为每个完成运行的任务调用 Finished 方法。）|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 此方法设置将在一个或多个任务失败时显示的消息。  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 此方法启动所有任务。 每个任务都在单独的线程上启动。  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 此方法仅供内部使用。 它根据某个任务在任务列表中的索引为其检索当前的消息。  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType)(size_t index, LPBSTR type)  
 此方法为某个任务检索当前的“类型”。 表 50 显示了可用的类型。  

### <a name="table-50-hresult-getresulttype"></a>表 50. HRESULT GetResultType  

|**类型**|**描述**|  
|-|-|  
|**0**|表示成功的任务|  
|**1**|表示返回一条警告的任务|  
|**-1**|表示失败的任务|  

 通过查看任务的退出或错误代码以及在任务的 <ExitCodes\> XML 元素中查找匹配项来检索此类型。  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 进度和预检页使用此方法检索 BitmapFilename 资源库属性，从而让它可以在突出显示的任务消息旁显示图像。 换言之，可以将自定义资源库添加到任务的 XML，然后使用此方法对其进行检索。  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 此方法检索当前所选任务的索引，如果想要检索显示在所选任务上的相关附加信息（请参阅 GetProperty 方法），则它会非常有用。 进度和预检页使用此方法显示所选任务的图像。  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 此方法主要为单元测试提供帮助，以便测试可以确保在单元测试退出之前完成任务。 通常情况下不会调用此方法。 它会在所有任务完成运行或等待时间结束后返回。  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 此方法返回当前标记为失败的任务数。  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 此方法返回当前标记为警告的任务数。  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 此方法返回当前标记为成功的任务数。  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 此方法返回当前正在运行的任务数。  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo)  
 从页面的 OnCommonControlEvent 调用此方法，以便 TaskManager 可以处理所需事件。  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD eventId, WORD controlId)  
 从页面的 OnControlEvent 调用此方法，以便 TaskManager 可以处理所需事件。  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 此方法仅供内部使用。  

#### <a name="iwizardcomponent-interface"></a>IWizardComponent 接口  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>概述  
 通常情况下，不用直接实现此接口，而是通过 WizardComponent 模板类来实现。 如果组件实现此接口，并且已向注册表注册了一个类工厂，那么组件在创建时会收到一个指向 IWizardPageContainer 实例的指针。 例如，这样可帮助你访问记录器或注册表，以创建组件可能需要的其他组件。  

#### <a name="iwizarddialogcontroller-interface"></a>IWizardDialogController 接口  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 此接口仅供内部使用。  

#### <a name="iwizarddialogview-interface"></a>IWizardDialogView 接口  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 此接口仅供内部使用。  

####  <a name="IWizardPageInterface"></a> IWizardPage 接口  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 WizardPageImpl 实现，因此一般无需自己实现。 该向导在与自定义页面进行交互时会为你调用所有这些方法。  

#### <a name="iwizardpagecontainer-interface"></a>IWizardPageContainer 接口  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>概述  
 此接口通过 Container 方法（由 WizardPageImpl 实现）提供给你的页面，可通过它访问向导的各种服务。  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 使用此方法将消息写入日志文件 - 例如：  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 此方法提供对“内存”变量的访问，这些变量是仅在 UDI 向导运行时才存在于内存中的属性。 这些属性通过 $memoryVarName$ 语法以代码或 XML 形式提供给其他页面。  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 可通过此方法创建已注册的任何组件的新实例。 但是，最好使用模板函数 CreateInstance，因为它是强类型。  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 可通过此方法检索已注册的服务。 但是，最好调用强类型的 GetService 模板函数（而不是使用 IUnknown）。  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 此方法处理字符串值中的变量。 它支持表 51 和表 52 中所示的格式。  

### <a name="table-51-hresult-replacevariables"></a>表 51. HRESULT ReplaceVariables  

|**格式**|**描述**|  
|-|-|  
|**$Name$**|将内存变量的值替换为此名称（如果没有含此名称的内存变量，将删除“令牌”。）|  
|**%Name%**|一个任务序列变量或环境变量。 顺序如下：<br /><br /> 1.使用任务序列变量的值（如果存在）。<br />2.使用环境变量的值（如果存在）。<br />3.否则，请从字符串中删除此文本。|  

### <a name="table-52-hresult-parameter"></a>表 52. HRESULT 参数  

|**参数**|**描述**|  
|-|-|  
|**源**|输入字符串，可包含 $ 和 % 变量的任意组合，或者不含这两者|  
|**pDest**|返回时包含一个新字符串，该字符串具有根据表 51 进行替换的所有令牌|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 此方法尚未完整测试。 你可以基于 .config XML 文件中定义的页面名称直接切换到特定页面。 调用此方法会跳过页面上的 OnNextClicked。 另外，此方法的行为可能会发生更改，因此需自行承担使用风险。  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 此方法显示一个消息框，其中包含所提供的文本和标题。 uType 参数是可提供给 MessageBox Win32 函数的任何值。  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 如果通过提供 /preview 切换在“预览”模式下启动向导，则此方法返回 TRUE。 在预览模式下，永远不会禁用“下一步”按钮。 可通过此方法在预览模式下跳过代码，例如，当页面上没有有效数据时，这样做可能会引发问题。  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 此方法为主对话框返回 HWND。 谨慎使用此方法。 通常情况下，通过 UDI 向导应用程序编程接口，你永远无法直接使用窗口图柄。  

#### <a name="iwizardpageview-interface"></a>IWizardPageView 接口  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 此接口通过 View 方法（由 WizardPageImpl 实现）提供给页面中的代码。  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 UDI 向导使用包装器，它们实际上是用于与页面上的控件进行交互的外观。 使用这些外观而不是实际的控件可以更加轻松地为页面编写测试，因为可以提供测试中的模拟外观。  

 不应直接使用此方法，最好使用强类型的 GetControlWrapper 模板方法，例如：  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 此方法返回页面的窗口图柄。 通常情况下，无需访问此窗口图柄。  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 如有必要，可调用此方法来获取页面中控件的窗口图柄。 （最好调用 GetControlWrapper 模板函数）。  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 此方法仅供内部使用。  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 此方法仅供内部使用。  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 将输入焦点设置为特定控件。  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 此方法仅供内部使用。  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 此方法仅供内部使用。  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 将焦点设置为某个向导按钮。WizardButtons 有两个值（BackButton 和 NextButton）。  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 请求启用或禁用的某个向导按钮。 该按钮可能与请求的状态不匹配。 例如，如果使用 /preview 切换运行 UDI 向导，将始终启用按钮。 WizardButtons 有两个值（BackButton 和 NextButton）。  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 此方法在页面内容区域的底部显示警告消息。 此消息可为任何所需的文本。  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 隐藏通过调用 ShowWarningMessage 显示的警告消息。  

#### <a name="ixmldocument-interface"></a>IXmlDocument 接口  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>概述  
 此接口由 ID_IXmlDocument 组件实现，该组件是一个旨在使用 C++ 轻松处理 XML 文档的外观。  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 此方法从外部文件加载 XML 文档。 如果加载文件时没有出现错误，返回 S_OK；如果出现错误，则返回 S_FALSE。 出现错误时，可通过调用 GetParseErrorMessage 来获取错误消息。  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 此方法从字符串而不是外部文件中加载 XML 文档。 除了读取 XML 的源代码之外，其行为与 Load 方法相同。  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 此方法将内存中的 XML 文档保存到外部文件。  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 此方法返回一个新字符串，以及加载 XML 文档时的错误消息（如果有）。 它始终返回 S_OK。  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 通过此方法，可使用 XPath 表达式从文档中检索节点集合。 它始终返回 S_OK。  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 通过此方法，可使用 XPath 表达式从文档中检索节点。 它始终返回 S_OK。  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 此方法添加一个外部架构文件的名称，用于在加载时验证 XML 文档的架构。 提供的命名空间是可以在 XPath 查询中使用的字符串，尽管尚未进行测试。  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 此方法将新特性添加到 XML 文档中的现有节点。 请参阅表 53。  

### <a name="table-53-hresult-addattribute"></a>表 53. HRESULT AddAttribute  

|**参数**|**描述**|  
|-|-|  
|**pNode**|要向其添加特性的节点|  
|**Name**|新特性的名称|  
|**值**|新特性的值|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 调用此方法来创建新节点：  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 创建新节点后，可通过调用父级的 appendChild 方法将其作为子节点添加到另一个节点。  

### <a name="helper-functions"></a>帮助程序函数  

#### <a name="createinstance-template-function"></a>CreateInstance 模板函数  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 在 IWizardPageContainer.h 中定义此函数，它通过 IWizardPageContainer->CreateInstance 方法提供类型安全的包装器，例如：  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 此代码创建新的 ID_Directory 组件，用于检索该组件的 IDirectory 接口。  

#### <a name="getservice-template-function"></a>GetService 模板函数  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 在 IWizardPageContainer.h 中定义此函数，它通过 IWizardPageContainer->GetService 方法提供类型安全的包装器，例如：  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 此函数检索支持 ITSVariableBag 接口的任务序列组件。 （对于 ITSVariableBag，可改用 WizardPageImpl 类的 TSVariables 方法。）  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>UDI 向导设计器配置文件架构参考  
 UDI 向导设计器使用此文件。 为每个自定义 .dll 文件创建单独的文件，其中可包含自定义向导页编辑器、自定义任务或自定义验证程序。 该文件必须以 .config 结尾并驻留在 installation_folder\Bin\Config 文件夹中（其中，installation_folder 是安装 MDT 的文件夹）。  

  表 54 列出了 UDI 向导设计器配置文件中的元素及其描述。 DesignerConfig 元素是此引用的根节点。  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>表 54. UDI 向导设计器配置文件中的元素及其描述  

|**元素名称**|**描述**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|指定所有其他元素的根|  
|[DesignerMappings](#DesignerMappings)|对一组 [Page](#Page) 元素进行分组|  
|[Page](#Page)|指定要在 UDI 向导设计器中加载的向导页编辑器，用于编辑向导页的配置设置|  
|[Param](#Param)|指定传递给 [Task](#Task) 或 [Validator](#Validator) 父元素和对应 UDI 向导配置文件中 [Setter]() 元素的参数，注意：如果父级是 [Task](#Task) 或 [Validator](#Validator) 元素，则此元素的特性不同。|  
|[Task](#Task)|指定任务库中的任务|  
|[TaskItem](#TaskItem)|指定一组传递给任务的参数|  
|[TaskLibrary](#TaskLibrary)|对一组 [Task](#Task) 元素进行分组|  
|[Validator](#Validator)|指定验证程序库中的验证程序|  
|[ValidatorLibrary](#ValidatorLibrary)|对一组 [Validator](#Validator) 元素进行分组|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 此元素指定所有其他元素的根。  

##### <a name="element-information"></a>元素信息  
  表 55 提供了有关 [DesignerConfig](#DesignerConfig) 元素的信息。  

### <a name="table-55-designerconfig-element-information"></a>表 55. DesignerConfig 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|1：此元素是必需的。|  
|Parent elements|无|  
|内容|DesignerMappings, TaskLibrary, ValidatorLibrary|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 此元素对一组 [Page](#Page) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
  表 56 提供了有关 [DesignerMappings](#DesignerMappings) 元素的信息。  

### <a name="table-56-designermappings-element-information"></a>表 56. DesignerMappings 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [DesignerConfig](#DesignerConfig) 元素中为 0 或 1（如果 DLL 中没有对应此 UDI 向导设计器配置文件的自定义向导页，则此元素是可选的。）|  
|Parent elements|DesignerConfig|  
|内容|Page|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 此元素指定将要加载到 UDI 向导设计器中的向导页面编辑器，用于编辑向导页的配置设置。  

##### <a name="element-information"></a>元素信息  
表 57 提供了有关 [Page](#Page) 元素的信息。  

### <a name="table-57-page-element-information"></a>表 57. Page 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|对于 [DesignerMappings](#DesignerMappings) 元素中定义的每个向导页，为 1 或 1 以上|  
|Parent elements|DesignerMappings|  
|内容|任何格式良好的 XML 内容|  

##### <a name="element-attributes"></a>元素特性  
表 58 列出了 [Page](#Page) 元素的特性，并提供每个特性的描述。  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>表 58. Page 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**描述**|指定提供此参数信息的文本，它显示在 UDI 向导设计器中|  
|**DesignerAssembly**|指定与向导页编辑器关联的 .dll 文件 的名称（.dll 文件必须在 installation_folder\Bin 文件夹中（其中，installation_folder 是安装 MDT 的文件夹。）|  
|**DesignerType**|在 .dll 文件中指定 DesignerAssembly 特性（这是向导页面编辑器的 Microsoft .NET 类型，具有完全限定的命名空间）中定义的向导页编辑器的名称。|  
|**DisplayName**|指定页面编辑器的用户友好名称，它显示在 UDI 向导设计器中|  
|**DLL**|指定与向导页关联的 .dll 文件的名称（.dll 文件必须在 installation_folder\Templates\Distribution\Tools\\platform 文件夹中，其中，installation_folder 是安装 MDT 的文件夹，platform 为 32 位版本的 x86 或 64 位版本的 x64。）注意：请确保 DLL 处理器体系结构与安装的 MDT 处理器体系结构相匹配。 例如，如果安装了 32 位版本的 MDT，对于向导页，请确保使用 32 位的 DLL。|  
|**Image**|指定可移植网络图形 (PNG) 格式的页面图像的名称（.png 文件必须在 installation_folder\Bin\Images 文件夹中；其中，installation_folder 是安装 MDT 的文件夹。）|  
|**类型**|指定向导页编辑器，它必须与命名的编辑器（在注册自定义页面时使用）相匹配|  

##### <a name="remarks"></a>备注  
 UDI 向导设计器使用 [Page](#Page) 元素（如模板）为新向导创建初始 XML。 UDI 向导设计器执行架构验证，以确保 [Page](#Page) 和子元素的格式有效。 对于 UDI 向导页类型以及 UDI 向导设计器使用自定义页面编辑器编辑和创建此类型的页面时所需的信息，此元素提供两者之间的映射。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Param"></a> Param  
 此元素指定传递给 [Task](#Task) 或 [Validator](#Validator) 父元素和对应 UDI 向导配置文件中 [Setter]() 元素的参数。  

> [!NOTE]
>  如果父级是 [Task](#Task) 或 [Validator](#Validator) 元素，则此元素的特性不同。  

##### <a name="element-information"></a>元素信息  
 表 59 提供了有关 [Param](#Param) 元素的信息。  

### <a name="table-59-param-element-information"></a>表 59. Param 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|对于每个 [TaskItem](#TaskItem) 或 [Validator](#Validator) 父元素，为 1 或 1 以上|  
|Parent elements|TaskItem, Validator|  
|内容|任何格式良好的 XML 内容|  

##### <a name="element-attributes"></a>元素特性  
  表 60 列出了 [Param](#Param) 元素的特性，并提供每个特性的描述。  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>表 60. Param 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**描述**|指定提供此参数信息的文本，它显示在 UDI 向导设计器中，注意：此特性仅对 [Validator](#Validator) 元素有效。|  
|**DisplayName**|指定验证程序参数的用户友好名称，它显示在 UDI 向导设计器相应的 UDI 向导页中（此名称通常比 Name 特性更具描述性。）注意：此特性仅对 [Validator](#Validator) 元素有效。|  
|**Name**|指定传递给任务或验证程序的参数的名称，具体取决于父元素（此特性在 UDI 向导配置文件的 [Setter]() 元素中将变为 Property 特性。）注意：此参数用于 [TaskItem](#TaskItem) 和 [Validator](#Validator) 父元素。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Task"></a> Task  
 此元素指定任务库中的任务。  

##### <a name="element-information"></a>元素信息  
 表 61 提供了有关 [Task](#Task) 元素的信息。  

### <a name="table-61-task-element-information"></a>表 61. Task 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [TaskLibrary](#TaskLibrary) 元素中为 1 或 1 以上（如果指定了 TaskLibrary 元素，则此元素不是可选的。）|  
|Parent elements|TaskLibrary|  
|内容|TaskItem|  

##### <a name="element-attributes"></a>元素特性  
  表 62 列出了 [Task](#Task) 元素的特性，并提供每个特性的描述。  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>表 62. Task 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**描述**|指定提供此任务信息的文本，它显示在 UDI 向导设计器中|  
|**DLL**|指定与任务关联的 .dll 文件的名称（.dll 文件必须在 installation_folder\Templates\Distribution\Tools\\platform 文件夹中，其中，installation_folder 是安装 MDT 的文件夹，platform 为 32 位版本的 x86 或 64 位版本的 x64。）|  
|**Name**|指定任务的名称，它显示在相应的 UDI 向导页和 UDI 向导设计器中|  
|**类型**|指定任务类型，该类型注册到工厂注册表，用于调用 .dll 文件中的特定任务|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="TaskItem"></a> TaskItem  
 此元素指定一组传递给任务的参数。  

##### <a name="element-information"></a>元素信息  
  表 63 提供了有关 [TaskItem](#TaskItem) 元素的信息。  

### <a name="table-63-taskitem-element-information"></a>表 63. TaskItem 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|对于每个 Task 元素，为 1 或 1 以上|  
|Parent elements|Task|  
|内容|Param|  

##### <a name="element-attributes"></a>元素特性  
 表 64 列出了 [TaskItem](#TaskItem) 元素的特性，并提供每个特性的描述。  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>表 64. TaskItem 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**类型**|指定将在 UDI 向导配置文件中创建的元素类型。 将创建一个对应此特性值的 XML 元素。 例如，如果此特性的值为 [File](#File)，将在 UDI 向导配置文件中创建一个 File 元素。<br /><br /> 目前唯一支持的值是：<br /><br /> -   File，它需要两个 [Param](#Param) 子元素（其中一个 Param 子元素的 Name 特性设置为 Source，另一个 Param 子元素的 Name 特性设置为 Dest）<br />-   [Setter]()，它需要一个 Param 子元素|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="TaskLibrary"></a> TaskLibrary  
 此元素对一组 [Task](#Task) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
 表 65 提供了有关 [TaskLibrary](#TaskLibrary) 元素的信息。  

### <a name="table-65-tasklibrary-element-information"></a>表 65. TaskLibrary 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [DesignerConfig](#DesignerConfig) 元素中为 0 或 1（如果 DLL 中没有对应此 UDI 向导设计器配置文件的自定义任务，则此元素是可选的。）|  
|Parent elements|DesignerConfig|  
|内容|Task|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 此元素指定验证程序库中的验证程序。  

##### <a name="element-information"></a>元素信息  
 表 66 提供了有关 [Validator](#Validator) 元素的信息。  

### <a name="table-66-validator-element-information"></a>表 66. Validator 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [ValidatorLibrary](#ValidatorLibrary) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|**ValidatorLibrary**|  
|内容|Param|  

##### <a name="element-attributes"></a>元素特性  
表 67 列出了 [Validator](#Validator) 元素的特性，并提供每个特性的描述。  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>表 67. Validator 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**描述**|指定提供此验证程序信息的文本，它显示在 UDI 向导设计器中|  
|**DisplayName**|指定显示在 UDI 向导设计器中的验证程序的用户友好名称（此名称通常比 Name 特性更具描述性。）|  
|**DLL**|指定与验证程序关联的 .dll 文件的名称（.dll 文件必须在 installation_folder\Templates\Distribution\Tools\\platform 文件夹中，其中，installation_folder 是安装 MDT 的文件夹，platform 为 32 位版本的 x86 或 64 位版本的 x64。）|  
|**Name**|指定验证程序的名称，它显示在相应的 UDI 向导页和 UDI 向导设计器中|  
|**类型**|指定验证程序类型，该类型注册到工厂注册表，用于调用 .dll 文件中的特定验证程序|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 此元素对一组 [Validator](#Validator) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
 表 68 提供了有关 [ValidatorLibrary](#ValidatorLibrary) 元素的信息。  

### <a name="table-68-validatorlibrary-element-information"></a>表 68. ValidatorLibrary 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [DesignerConfig](#DesignerConfig) 元素中为 0 或 1（如果 DLL 中没有对应此 UDI 向导设计器配置文件的自定义验证程序，则此元素是可选的。）|  
|Parent elements|DesignerConfig|  
|内容|**Validator**|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 <DesignerConfig\>   + <TaskLibrary\>   - <ValidatorLibrary\>        +<Validator DLL="" Description="Requires text in a field" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Doesn't allow certain characters to be in a field" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Require the contents match a regular expression" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>UDI 向导设计器参考  

### <a name="controls"></a>控件  
 用于创建在 UDI 向导设计器中使用的自定义向导页编辑器的控件为 WPF UserControl 实例。 表 69 列出了可用于创建自定义向导页编辑器的控件。  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>表 69. 可用于创建自定义向导页编辑器的控件  

|控制|说明|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|此控件用于编辑存储在 [Page](#Page) 元素的[Data](#Data)元素中的数据。|  
|[FieldElementControl](#FieldElementControl)|此控件用于编辑字段，通常会链接到 .xaml 页上的 TextBox 控件。|  
|[SetterControl](#SetterControl)|此控件用于修改 UDI 向导配置文件中 [setter]() 元素的值。|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 此控件提供许多编辑数据的功能。 若要了解如何使用此控件，最佳方法是查看介绍如何在页面的 Data 元素下编辑数据的示例。 该示例详细介绍了如何在此控件中添加、删除和编辑项。  

####  <a name="FieldElementControl"></a> FieldElementControl  
 使用此控件编辑字段，通常会链接到 .xaml 页上的 TextBox 控件。  

##### <a name="example"></a>示例  
 以下内容摘自 .xaml 文件，介绍了如何通过 FieldElementControl 来使用 TextBox 子控件为向导页中的字段配置默认值：  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>属性  

###### <a name="fielddata"></a>FieldData  
 该字符串属性包含用于将 FieldElementControl 连接到字段的基础 XML 的信息。 连接了页面编辑器接口的属性。 以下内容摘自 .xaml 文件，介绍了 FieldData 属性的用法：  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 在此摘录中，页面编辑器接口名为 ControlRoot，在 ElementName 参数中指定此接口。 对 ControlRoot 页面编辑器接口的 DataContext.Location 属性执行绑定。 DataContext 是一个视图模型，指向 UDI 向导配置文件中的 [Page](#Page) 元素。 Location 是视图的一个属性，它返回可能位置的列表，由 UDI 向导配置文件中的 [Data](#Data) 元素定义。 UDI 向导配置文件中的 [DataItem](#DataItem) 元素定义每个位置。  

###### <a name="headertext"></a>HeaderText  
 可通过该字符串属性为 [FieldElementControl](#FieldElementControl) 控件指定标头。 标头充当控件的标题，其格式为粗体、橙色文本、直接显示在控件上方。  

###### <a name="instructiontext"></a>InstructionText  
 可通过该字符串属性为 [FieldElementControl](#FieldElementControl) 控件指定信息文本。 通常情况下，文本提供该字段的简要说明，并说明配置该字段对相应向导页的影响。  

###### <a name="hideenablebutton"></a>HideEnableButton  
 可通过此布尔属性控制更改“未锁定”和“锁定”（启用或禁用）状态的按钮是否可见。 如果设置为：  

-   True，按钮不可见  

-   False，按钮可见（此为默认值。）  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 对于包含用于设置默认值的控件的节，可通过此布尔属性控制其是否可见。 尽管该属性引用选项卡，但 [FieldElementControl](#FieldElementControl) 上没有选项卡，而是一个可以隐藏的节。 如果设置为：  

-   True，节不可见  

-   False，节可见（此为默认值。）  

###### <a name="hideborder"></a>HideBorder  
 可通过此布尔属性控制字段控件周围的边框是否可见。 如果设置为：  

-   True，边框不可见  

-   False，边框可见（此为默认值。）  

###### <a name="hideimage"></a>HideImage  
 对于 FieldImageSource 属性配置的图像，可通过此布尔属性控制其是否可见。 如果设置为：  

-   True，图像不可见  

-   False，图像可见（此为默认值。）  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 对于管理验证程序列表的节，可通过此布尔属性控制其是否可见。 尽管该属性引用选项卡，但 [FieldElementControl](#FieldElementControl) 上没有选项卡，而是一个可以隐藏的节。 如果设置为：  

-   True，节不可见  

-   False，节可见（此为默认值。）  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 对于配置字段摘要标题的节，可通过此布尔属性控制其是否可见。 字段中的标题和相应的值显示在阶段流的 SummaryPage 向导页类型中。 尽管该属性引用选项卡，但 [FieldElementControl](#FieldElementControl) 上没有选项卡，而是一个可以隐藏的节。 如果设置为：  

-   True，节不可见  

-   False，节可见（此为默认值。）  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 对于配置对应字段的任务序列变量的节，可通过此布尔属性控制其是否可见。 尽管该属性引用选项卡，但 [FieldElementControl](#FieldElementControl) 上没有选项卡，而是一个可以隐藏的节。 如果设置为：  

-   True，节不可见  

-   False，节可见（此为默认值。）  


####  <a name="SetterControl"></a> SetterControl  
 使用此控件修改 UDI 向导配置文件中 [Setter]() 元素的值。 此控件包含用于修改 setter 元素值的子控件。  

##### <a name="example"></a>示例  
 以下内容摘自 .xaml 文件，介绍了如何通过 SetterControl 来使用 TextBox 子控件修改名为 KeyLocationSetter 的 [Setter]() 元素。  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>属性  

###### <a name="setterdata"></a>SetterData  
 需要将其绑定到连接到资源库的视图或视图模型的属性。 此操作类似于绑定到某个字段，如 FieldElementControl 所述。  

###### <a name="headertext"></a>HeaderText  
 可通过此属性设置显示在控件标头中的文本。 将此属性视为控件的标题；默认情况下，它显示为粗体橙色文本。  

###### <a name="instructiontext"></a>InstructionText  
 将此属性设置为显示在标头下面的文本，通常为说明文本，告知自定义编辑器用户何时以及为何他/她想要修改该字段的行为。  

### <a name="interfaces"></a>界面  
表 70 列出了可用于创建自定义向导页编辑器的接口。  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>表 70. 可用于创建自定义向导页编辑器的接口  

|**接口**|**描述**|  
|-|-|  
|[IDataService](#IDataService)|使用此接口将字段连接到 UDI 向导配置文件中的 Data 元素。|  
|[IMessageBoxService](#IMessageBoxService)|可通过此接口访问用于显示消息框的方法。|  

####  <a name="IDataService"></a> IDataService  
 此接口包含一些属性和方法，但你只需要一个属性。 此处只提供该属性。  

 通过在类中使用与以下类似的代码，可使用依赖项注入来获取指向此接口的指针：  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>属性  
 表 71 列出了 IDataService 接口的属性。  

### <a name="table-71-properties-for-the-idataservice-interface"></a>表 71. IDataService 接口的属性  

|**接口**|**描述**|  
|-|-|  
|[CurrentPage](#CurrentPage)|对于正在 UDI 向导配置文件中进行编辑的当前页面的上下文，此属性提供对其之下的 XML 元素、特性和值的访问|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 此属性提供对当前页面 XML 的访问。 决不能设置此属性，但可以随意修改页面的 XML。 示例页编辑器显示了修改 XML 的示例。 在拥有自定义数据时，主要使用此属性。 对于字段和属性（资源库），可使用预生成的控件来处理所有细节。  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 可通过此接口访问用于显示消息框的方法。 你可能想知道为什么需要一个接口来显示消息框。 实际情况是，你不需要此接口：Microsoft 在编码时使用此接口是因为它有助于为设计器页面编写自动化测试。  

 但使用这些方法的确提供了一个有用之处：对话框始终将“所有者”设置为 UDI 向导，这样可确保对话框正确地分组到主窗口。  

 通过在类中使用与以下类似的代码，可使用依赖项注入来获取指向此接口的指针：  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>方法  
 表 72 列出了 IMessageBoxService 接口的方法。  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>表 72. IMessageBoxService 接口的方法  

|**方法**|**描述**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|可使用此重载方法显示包含下列成员的消息框：<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|调用此方法来创建新的对话框。|  
|[ShowWizardWindow](#ShowWizardWindow)|在包含“下一步”和“上一步”导航按钮的对话框中，使用此方法显示自定义编辑器。|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 此方法显示一个消息框，它是自定义向导页编辑器的子级。 重载此成员：表 73 包含成员列表和每个成员的简要描述。 有关每个成员的完整信息（包括语法、使用情况和示例），请参阅对应每个成员的部分。  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>表 73. ShowMessagBox 方法的重载成员  

|成员|说明|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|显示带有图标和“确定”按钮的消息框|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|显示带有图标和不同的按钮组合的消息框|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|显示一个提供异常消息和“确定”按钮的消息框|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(String message, String caption, MessageBoxImage icon)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 此方法显示带有“确定”按钮的消息框。 请参阅表 74。  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>表 74. ShowMessageBox(String message, String caption, MessageBoxImage icon) 方法的参数  

|**参数**|**描述**|  
|-|-|  
|**message**|将在消息框的内容区域中显示的消息|  
|**caption**|将在对话框的标题栏中显示的文本|  
|**icon**|将在消息框中显示的图标类型|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 此方法显示一个消息框，其中包含要显示的一组按钮，并报告单击的具体按钮。 请参阅表 75。  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>表 75. ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon) 方法的参数  

|**参数**|**描述**|  
|-|-|  
|**message**|将在消息框的内容区域中显示的消息|  
|**caption**|将在对话框的标题栏中显示的文本|  
|**button**|要显示的按钮|  
|**icon**|将在消息框中显示的图标类型|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 此方法会显示一个消息框，报告有关异常的信息。 此消息框带有单个“确定”按钮。 请参阅表 76。  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>表 76. ShowMessageBox(Exception exception) 方法的参数  

|**参数**|**描述**|  
|-|-|  
|**exception**|要报告的异常（对话框使用 exception.Message 作为内容。）|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 此方法创建新的对话框，它的内容为 viewType 中提供的文本。 UDI 设计器创建此类型的新实例，并将其包装在带有“确定”和“Cancel”按钮的对话框中。  

 使用 dialogPayload 参数将数据传递给控件。 SDK 目录中的 SampleEditor 解决方案提供了如何使用此功能的示例。  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 在包含“下一步”和“上一步”导航按钮的对话框中，使用此方法显示一个自定义编辑器。 Microsoft 尚未提供如何使用此方法的示例。  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> UDI 向导设计器配置文件架构参考  
 UDI 向导使用此文件，UDI 向导设计器配置此文件。 此文件用于配置：  

-   显示在 UDI 向导中的向导页  

-   UDI 向导中向导页的序列  

-   每个向导页上的字段设置  

-   UDI 向导设计器中可用的 StageGroups  

-   UDI 向导设计器中每个部署向导的可用 Stages  

  表 77 列出了 UDI 向导配置文件中的元素及其描述。 Wizard 元素是此引用的根节点。  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>表 77. UDI 向导配置文件中的元素及其描述  

|**元素名称**|**描述**|  
|-|-|  
|[Data](#Data)|在 [Page](#Page) 元素内对但单个 [DataItem](#DataItem) 元素进行分组，然后由 Name 特性进行命名。|  
|[DataItem](#DataItem)|在 [Page](#Page) 元素内对单个 [Setter]() 元素进行分组。 可通过在 [DataItem](#DataItem) 元素中包含一个或多个 [Data](#Data) 元素来创建层次结构数据。 每个 DataItem 元素都表示一个项。 例如，可用驱动器的列表可能会有显示名称的 DataItem 和相应驱动器号的另一个 DataItem 元素。|  
|[默认值](#Default)|为 [Field](#Field) 或 [RadioGroup](#RadioGroup) 元素中指定的字段指定默认值。 默认值设置为此元素括起来的值。|  
|[DLL](#DLL)|指定由 UDI 向导和 UDI 向导设计器加载和引用的 DLL。|  
|[DLLs](#DLLs)|对单个 [DLL](#DLL) 元素进行分组。|  
|[错误](#Error)|指定可能的错误代码，该代码可由任务返回。 任务的 HRESULT 返回并捕获错误代码的值，以便提供更具体的错误信息。|  
|[ExitCode](#ExitCode)|为任务指定可能的退出代码。 退出代码是任务需要的返回代码。 为每个可能的退出代码创建 ExitCode 元素。 或者，可以在 Value 特性中指定一个星号（\*），用于处理其他 ExitCode 元素中没有列出的返回代码。|  
|[ExitCodes](#ExitCodes)|针对 [Task](#Task) 元素或 Error 元素，对一组 [ExitCode](#ExitCode) 和 [Error](#Error) 元素进行分组。|  
|[Field](#Field)|在 [Page](#Page) 元素中指定一个控件的实例，用于通过 XML 提供自定义。 并非所有控件都可通过 XML 来进行自定义，只有使用 [Field](#Field) 元素的控件才可以。|  
|[Fields](#Fields)|在 [Page](#Page) 元素内对单个 [Field](#Field) 元素进行分组。|  
|[File](#File)|使用 Microsoft.Wizard.CopyFilesTask 任务类型为文件复制操作指定源和目标。 可包含一个单独的 File 元素，用于在单个任务中复制多个文件。|  
|[Page](#Page)|指定页面的实例并包含页面的所有配置设置。|  
|[PageRef](#PageRef)|在 [StageGroup](#StageGroup) 的 [Stage](#Stage) 中指定页面实例的引用。|  
|[Pages](#Pages)|对单个 [Page](#Page) 元素进行分组。|  
|[RadioGroup](#RadioGroup)|在 [Field](#Field) 元素中，指定一组单选按钮。|  
|[StageGroup](#StageGroup)|指定一个或多个阶段组。|  
|[StageGroups](#StageGroups)|在 UDI 向导配置文件中，对一组阶段组进行分组。|  
|[Setter]()|为 Property 属性中命名的属性的值指定属性设置。|  
|[Stage](#Stage)|在 [StageGroup](#StageGroup) 中指定一个 stage 并包含一个或多个 [PageRef](#PageRef) 元素。|  
|[Style](#Style)|对配置 UDI 向导外观和体验（包括向导顶部显示的标题和 UDI 向导中显示的横幅图像。）的单个 [setter]() 元素进行分组。|  
|[Task](#Task)|指定要在 [Page](#Page) 父元素中指定的页面上运行的任务。|  
|[任务](#Tasks)|针对 [Page](#Page) 元素，对一组任务进行分组。|  
|[Validator](#Validator)|为 [Field](#Field) 父元素中指定的字段控件指定验证程序。|  
|[Wizard](#Wizard)|指定所有其他元素的根。|  

####  <a name="Data"></a> Data  
 此元素在 [Page](#Page) 元素内对单个 [DataItem](#DataItem) 元素进行分组，然后由 Name 特性进行命名。  

##### <a name="element-information"></a>元素信息  
表 78 提供了有关 [Data](#Data) 元素的信息。  

### <a name="table-78-data-element-information"></a>表 78. Data 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Page](#Page) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|**Page**, **DataItem**|  
|内容|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>元素特性  
 表 79 列出了 [Data](#Data) 元素的特性，并提供每个特性的描述。  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>表 79. Data 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**Name**|指定 [Data](#Data) 元素的名称|  

##### <a name="remarks"></a>备注  
 通过 Name 特性，代码可以检索特定的一组数据。  

##### <a name="example"></a>示例  
 无。  

####  <a name="DataItem"></a> DataItem  
 此元素在 [Page](#Page) 元素内对单个 [Setter]() 元素进行分组。 可通过在 [DataItem](#DataItem) 元素中包含一个或多个 [Data](#Data) 元素来创建层次结构数据。 每个 DataItem 元素都表示一个项。 例如，可用驱动器的列表可能会有显示名称的 DataItem 和相应驱动器号的另一个 DataItem 元素。  

##### <a name="element-information"></a>元素信息  
 表 80 提供了有关 [DataItem](#DataItem) 元素的信息。  

### <a name="table-80-dataitem-element-information"></a>表 80. DataItem 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Data](#Data) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|Data|  
|内容|Data, Setter|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

#### <a name="default"></a>默认  
 此元素为 [Field](#Field) 或 [RadioGroup](#RadioGroup) 父元素中的字段指定默认值。 默认值设置为此元素括起来的值。  

##### <a name="element-information"></a>元素信息  
表 81 提供了有关 [Default](#Default) 元素的信息。  

### <a name="table-81-default-element-information"></a>表 81. Default 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences |在 [Field](#Field) 或 [RadioGroup](#RadioGroup) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|Field, RadioGroup|  
|内容|可以是任何格式良好的 XML 内容，但通常是标准文本|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 在以下示例中，TimeZone 字段的默认值设置为“太平洋标准时间”：  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 此元素为 UDI 向导和 UDI 向导设计器指定一个 DLL，用于加载和引用。  

##### <a name="element-information"></a>元素信息  
表 82 提供了有关 [DLL](#DLL) 元素的信息。  

### <a name="table-82-dll-element-information"></a>表 82. DLL 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [DLLs](#DLLs) 元素中为 1 或 1 以上|  
|父元素|DLLs|  
|内容|此元素不支持任何内容|  

##### <a name="element-attributes"></a>元素特性  
 表 83 列出了 [DLL](#DLL) 元素的特性，并提供每个特性的描述。  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>表 83. DLL 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|名称|为 UDI 向导和 UDI 向导设计器指定 DLL 的名称，用于引用|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 此元素对单个 [DLL](#DLL) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
表 84 提供了有关 [DLLs](#DLLs) 元素的信息。  

### <a name="table-84-dlls-element-information"></a>表 84. DLLs 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|一台|  
|Parent elements|Wizard|  
|内容|DLL|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Error  
 此元素指定可能的错误代码，该代码可由任务返回。 任务的 HRESULT 返回并捕获错误代码的值，以便提供更具体的错误信息。  

##### <a name="element-information"></a>元素信息  
 表 85 提供了有关 [Error](#Error) 元素的信息。  

### <a name="table-85-error-element-information"></a>表 85. Error 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [ExitCode](#ExitCode) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|ExitCodes|  
|内容|任何格式良好的 XML 内容|  

##### <a name="element-attributes"></a>元素特性  
 表 86 列出了 [Error](#Error) 元素的特性，并提供每个特性的描述。  

###  

|**特性**|**描述**|  
|-|-|  
|**状态**|指定出错的任务的返回状态。 通常情况下，此特性的值设置为 Error。 在 UDI 向导中，此值显示在向导页的 State 列中。|  
|**Text**|指定描述性文本，该文本描述任务遇到的错误状态。|  
|**类型**|指定此元素表示错误、警告还是成功。 Type 中指定的值在 [ExitCodes](#ExitCodes) 元素中必须是唯一的。 此元素的有效值如下：<br /><br /> -   **0**，此元素表示成功。<br />-   **1**， 此元素表示警告。<br />-   **-1**， 此元素表示错误。|  
|**值**|指定任务以数值返回的代码值。 指定星号 (*) 的值，用于指示未在其他 [Error](#Error) 元素中列出的返回代码的默认元素。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="ExitCode"></a> ExitCode  
 此元素为任务指定可能的退出代码。 退出代码是任务需要的返回代码。 为每个可能的退出代码创建 ExitCode 元素。 或者，可以在 Value 特性中指定一个星号（\*），用于处理其他 ExitCode 元素中没有列出的返回代码。  

##### <a name="element-information"></a>元素信息  
表 87 提供了有关 [ExitCode](#ExitCode) 元素的信息。  

### <a name="table-87-exitcode-element-information"></a>表 87. ExitCode 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [ExitCodes](#ExitCodes) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|ExitCodes|  
|内容|至少一个 [ExitCode](#ExitCode) 元素以及零个或多个 [Error](#Error) 元素|  

##### <a name="element-attributes"></a>元素特性  
表 88 列出了 [ExitCode](#ExitCode) 元素的特性，并提供每个特性的描述。  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>表 88. ExitCode 元素的特性和对应的值  

|**特性**|说明|  
|-|-|  
|**状态**|指定任务的返回状态。 在 UDI 向导中，此特性的值显示在相应向导页的“状态”列中。 对于此特性，可使用对任务有意义的任何值。 此特性使用的典型值如下：<br /><br /> -   Success<br />-   Warning<br />-   Error|  
|**Text**|指定描述性文本，该文本描述任务的现有代码。|  
|**类型**|指定此元素表示错误、警告还是成功。 类型中指定的值在 [ExitCodes](#ExitCodes) 元素中必须是唯一的。 此元素的有效值如下：<br /><br /> -   **0**， 此元素表示成功。<br />-   **1**， 此元素表示警告。<br />-   **-1**， 此元素表示错误。|  
|**值**|指定任务以数值返回的代码值。 指定星号 (*) 的值，用于指示未在其他 [ExitCode](#ExitCode) 元素中列出的返回代码的默认元素。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="ExitCodes"></a> ExitCodes  
 此元素针对 [Task](#Task) 或 Error 元素，对一组 [ExitCode](#ExitCode) 和 [Error](#Error) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
表 89 提供了有关 [ExitCodes](#ExitCodes) 元素的信息。  

### <a name="table-89-exitcodes-element-information"></a>表 89. ExitCodes 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在每个 [Task](#Task) 元素中为 1|  
|Parent elements|Task|  
|内容|Error, ExitCode|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Field"></a> Field  
 此元素在 [Page](#Page) 元素中指定一个控件的实例，用于通过 XML 提供自定义。 并非所有控件都可通过 XML 来进行自定义，只有使用 [Field](#Field) 元素的控件才可以。  

##### <a name="element-information"></a>元素信息  
 表 90 提供了有关 [Field](#Field) 元素的信息。  

### <a name="table-90-field-element-information"></a>表 90. Field 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Field](#Field) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|Fields|  
|内容|Default, Validator|  

##### <a name="element-attributes"></a>元素特性  
表 91 列出了 [Field](#Field) 元素的特性，并提供每个特性的描述。  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>表 91. Field 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**Enabled**|指定是否为用户输入启用字段（此特性可以设置为 True 或 False。）|  
|**Name**|指定字段的名称|  
|**摘要**|为此字段设置的值指定显示在“摘要”向导页中的描述性文本。|  
|**VarName**|指定使用 [Field](#Field) 父元素中的字段读取或配置的任务序列变量名称|  

##### <a name="remarks"></a>备注  
 此元素可包含零个或多个 [Default](#Default) 元素以及零个或多个 [Validator](#Validator) 元素。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Fields"></a> Fields  
 此元素在 [Page](#Page) 元素内对单个 [Field](#Field) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
表 92 提供了有关 [Fields](#Fields) 元素的信息。  

### <a name="table-92-fields-element-information"></a>表 92. Fields 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Page](#Page) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|Page|  
|内容|Field, RadioGroup|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="File"></a> File  
 此元素使用 Microsoft.Wizard.CopyFilesTask 任务类型为文件复制操作指定源和目标。 可包含一个单独的 [File](#File) 元素，用于在单个任务中复制多个文件。  

##### <a name="element-information"></a>元素信息  
 表 93 提供了有关 [File](#File) 元素的信息。  

### <a name="table-93-file-element-information"></a>表 93. File 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|对于具有 Microsoft.Wizard.CopyFilesTask 任务类型的每个任务，为 1 或 1 以上|  
|Parent elements|Task|  
|内容|无|  

##### <a name="element-attributes"></a>元素特性  
 表 94 列出了 [File](#File) 元素的特性，并提供每个特性的描述。  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>表 94. File 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**Dest**|为 Source 特性中指定的文件指定目标文件夹的绝对或相对路径。 环境变量可作为路径的一部分。|  
|**源**|指定 Microsoft.Wizard.CopyFilesTask 任务类型复制的源文件的绝对或相对路径。 此特性支持通配符，从而可以使用单个 [File](#File) 元素复制多个文件。 环境变量可作为路径的一部分。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="PageElement"></a> Page  
 此元素指定页面的实例并包含页面的所有配置设置。  

##### <a name="element-information"></a>元素信息  
表 95 提供了有关 [Page](#Page) 元素的信息。  

### <a name="table-95-page-element-information"></a>表 95. Page 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在每个 [Pages](#Pages) 元素中为 1 或 1 以上|  
|Parent elements|Pages|  
|内容|Data, Fields, Setter, Tasks|  

##### <a name="element-attributes"></a>元素特性  
表 96 列出了 [Page](#Page) 元素的特性，并提供每个特性的描述。  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>表 96. Page 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**DisplayName**|指定显示在 UDI 向导设计器中的向导页的用户友好名称。 此名称通常比 Name 特性更具描述性。|  
|**Name**|指定显示在 UDI 向导设计器中的向导页的名称。|  
|**类型**|指定直接与 DLL 中特定向导页相关的向导页类型。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="PageRef"></a> PageRef  
 此元素在 [StageGroup](#StageGroup) 的 [Stage](#Stage) 中指定页面实例的引用。  

##### <a name="element-information"></a>元素信息  
表 97 提供了有关 [PageRef](#PageRef) 元素的信息。  

### <a name="table-97-pageref-element-information"></a>表 97. PageRef 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Stage](#Stage) 元素中为 1 或 1 以上|  
|Parent elements|Stage|  
|内容|无|  

##### <a name="element-attributes"></a>元素特性  
表 98 列出了 [PageRef](#PageRef) 元素的特性，并提供它的描述。  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>表 98. PageRef 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**Page**|在 [StageGroup](#StageGroup) 的 [Stage](#Stage) 中指定页面的实例。 将此值设置为 [Page](#Page) 元素的 Name 特性。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Pages"></a> Pages  
 此元素对单个 [Page](#Page) 元素进行分组。  

##### <a name="element-information"></a>元素信息  
表 99 提供了有关 [Pages](#Pages) 元素的信息。  

### <a name="table-99-pages-element-information"></a>表 99. Pages 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|一台|  
|Parent elements|Wizard|  
|内容|**Page**|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 此元素在 [Field](#Field) 元素中，指定一组单选按钮。  

##### <a name="element-information"></a>元素信息  
表 100 提供了有关 [RadioGroup](#RadioGroup) 元素的信息。  

### <a name="table-100-radiogroup-element-information"></a>表 100. RadioGroup 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Fields](#Fields) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|Fields|  
|内容|**默认值**|  

##### <a name="element-attributes"></a>元素特性  
 表 101 列出了 [RadioGroup](#RadioGroup) 元素的特性，并提供每个特性的描述。  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>表 101. RadioGroup 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**Locked**|指定是否为用户输入启用单选按钮组。 此特性可以设置为：<br /><br /> -   **True**。 指定单选按钮处于禁用状态，用户无法选择组中的单选按钮。<br />-   **False**。 指定单选按钮处于启用状态，用户可以选择组中的单选按钮。|  
|**Name**|指定的单选选项组的名称。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="StageGroup"></a> StageGroup  
 此元素指定部署阶段组。  

##### <a name="element-information"></a>元素信息  
表 102 提供了有关 [StageGroup](#StageGroup) 元素的信息。  

### <a name="table-102-stagegroup-element-information"></a>表 102. StageGroup 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [StageGroups](#StageGroups) 元素中为 1 或 1 以上|  
|Parent elements|StageGroups|  
|内容|Stage|  

##### <a name="element-attributes"></a>元素特性  
 表 103 列出了 [StageGroup](#StageGroup) 元素的特性，并提供每个特性的描述。  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>表 103. StageGroup 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**DisplayName**|指定显示在 UDI 向导设计器中的阶段组的用户友好名称。 此名称通常比 Name 特性更具描述性。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="StageGroups"></a> StageGroups  
 此元素在 UDI 向导配置文件中，对一组阶段组进行分组。  

##### <a name="element-information"></a>元素信息  
表 104 提供了有关 [StageGroups](#StageGroups) 元素的信息。  

### <a name="table-104-stagegroups-element-information"></a>表 104. StageGroups 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Wizard](#Wizard) 元素中为 0 或 0 以上|  
|Parent elements|Wizard|  
|内容|StageGroup|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Setter"></a> Setter  
 此元素为 Property 属性中命名的属性的值指定属性设置。  

##### <a name="element-information"></a>元素信息  
 表 105 提供了有关 [Setter]() 元素的信息。  

### <a name="table-105-setter-element-information"></a>表 105. Setter 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在每个父元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|Data, DataItem, Page, Style, Task, Validator|  
|内容|包含 Property 特性中的字符串值|  

##### <a name="element-attributes"></a>元素特性  
表 106 列出了 [Setter]() 元素的特性，并提供它的描述。  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>表 106. Setter 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**属性**|指定正在设置的属性名称。 属性名称设置为此特性括起来的值。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

#### <a name="stage"></a>阶段  
 此元素在 [StageGroup](#PageRef) 内指定一个 [Stage](#Stage) 并包含一个或多个 [PageRef](#StageGroup) 元素。  

##### <a name="element-information"></a>元素信息  
表 107 提供了有关 [Stage](#Stage) 元素的信息。  

### <a name="table-107-stage-element-information"></a>表 107. Stage 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [StageGroup](#StageGroup) 元素中为 1 或 1 以上|  
|Parent elements|StageGroup|  
|内容|PageRef|  

##### <a name="element-attributes"></a>元素特性  
表 108 列出了 [Stage](#Stage) 元素的特性，并提供每个特性的描述。  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>表 108. Stage 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**DisplayName**|指定显示在 UDI 向导设计器中的向导页的用户友好名称。 此名称通常比 Name 特性更具描述性。|  
|**Name**|指定阶段的名称。 使用 /stage: name 命令行参数启动 UDI 向导时，会使用此元素的值。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Style"></a> Style  
 此元素对配置 UDI 向导外观和体验（包括向导顶部显示的标题和 UDI 向导中显示的横幅图像。）的单个 [etter]() 元素进行分组。  

##### <a name="element-information"></a>元素信息  
表 109 提供了有关 Style 元素的信息。  

### <a name="table-109-style-element-information"></a>表 109. Style 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|一台|  
|Parent elements|Wizard|  
|内容|Setter|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 此元素指定要在 [Page](#Page) 父元素中指定的页面上运行的任务。  

##### <a name="element-information"></a>元素信息  
表 110 提供了有关 [Task](#Task) 元素的信息。  

### <a name="table-110-task-element-information"></a>表 110. Task 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Tasks](#Tasks) 元素中为 1 或 1 以上|  
|Parent elements|**任务**|  
|内容|ExitCodes, File, Setter|  

##### <a name="element-attributes"></a>元素特性  
表 111 列出了 [Task](#Task) 元素的特性，并提供每个特性的描述。  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>表 111. Task 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**DependsOn**|指定任务是否依赖于另一个任务。 此特性的值设置为另一个 [Task](#Task) 元素的 Name 特性。 注意：不能使用 UDI 向导设计器配置此特性。 但可以通过直接修改 .xml 文件手动将此特性添加到 [Task](#Task) 元素。|  
|**DisplayName**|指定显示在 UDI 向导设计器中的任务的用户友好名称。 此名称通常比 Name 特性更具描述性。|  
|**Name**|指定任务的名称。 此名称必须是唯一的。|  
|键入|指定用于运行任务的任务类型，它在包含该任务的 DLL 中定义。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Tasks"></a> Tasks  
 此元素针对 [Page](#Page) 元素，对一组任务进行分组。  

##### <a name="element-information"></a>元素信息  
表 112 提供了有关 [Tasks](#Tasks) 元素的信息。  

### <a name="table-112-tasks-element-information"></a>表 112. Tasks 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在每个 [Page](#Page) 元素中为 0 或 0 以上（此元素是可选的。）|  
|Parent elements|**Page**|  
|内容|Task|  

##### <a name="element-attributes"></a>元素特性  
表 113 列出了 [Tasks](#Tasks) 元素的特性，并提供每个特性的描述。  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>表 113. Tasks 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|**NameTitle**|指定显示在列（包含相应向导页中任务的名称）顶部的标题。|  
|**StatusTitle**|指定显示在列（包含相应向导页中任务的状态）顶部的标题。|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="ValidatorElement"></a> Validator  
 此元素为 [Field](#Field) 父元素中指定的字段控件指定验证程序。  

##### <a name="element-information"></a>元素信息  
表 114 提供了有关 [Validator](#Validator) 元素的信息。  

### <a name="table-114-validator-element-information"></a>表 114. Validator 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|在 [Field](#Field) 元素中为 0 或 0 以上|  
|Parent elements|Field|  
|内容|Setter|  

##### <a name="element-attributes"></a>元素特性  
表 115 列出了 [Validator](#Validator) 元素的特性，并提供它的描述。  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>表 115. Validator 元素的特性和对应的值  

|**特性**|**描述**|  
|-|-|  
|键入|指定验证程序的类型，它在包含该验证程序的 DLL 中定义|  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  
 无。  

####  <a name="Wizard"></a> Wizard  
 此元素指定所有其他元素的根。  

##### <a name="element-information"></a>元素信息  
表 116 提供了有关 [Wizard](#Wizard) 元素的信息。  

### <a name="table-116-wizard-element-information"></a>表 116. Wizard 元素的信息  

|**特性**|**值**|  
|-|-|  
|Number of occurrences|一台|  
|Parent elements|无|  
|内容|DLL, Pages, StageGroups, Style|  

##### <a name="element-attributes"></a>元素特性  
 此元素无任何特性。  

##### <a name="remarks"></a>备注  
 无。  

##### <a name="example"></a>示例  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
