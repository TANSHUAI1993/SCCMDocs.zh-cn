---
title: "创建和部署应用程序 | Microsoft Docs"
description: "创建和部署包含业务线应用的应用程序并了解如何有效地管理应用。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: bbbf278f5d31c51bfe061dd44e170f7ab1ca70ad
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建和部署应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

在本主题中，将直接开始使用 System Center Configuration Manager 创建应用程序。 在此示例中，将为 Windows 电脑创建并部署一个包含业务线应用的应用程序，该应用程序名为“Contoso.msi”且必须安装在用户公司中运行 Windows 10 的所有电脑上。 与此同时，你将了解许多可以执行的操作，以便有效管理应用程序。  

 此过程旨在为用户提供有关如何创建和部署 Configuration Manager 应用程序的概述。 但是，它并未涵盖所有配置选项，也未涵盖如何为其他平台创建和部署应用程序的内容。  

 有关每个平台的相关特定详细信息，请参阅以下主题之一：  

-   [创建 Windows 应用程序](../../apps/get-started/creating-windows-applications.md)  
-   [创建 iOS 应用程序](../../apps/get-started/creating-ios-applications.md)  
-   [创建 Android 应用程序](../../apps/get-started/creating-android-applications.md)  
-   [创建 Windows Phone 应用程序](../../apps/get-started/creating-windows-phone-applications.md)  
-   [创建 Mac 计算机应用程序](../../apps/get-started/creating-mac-computer-applications.md)  
-   [创建 Linux 和 UNIX 服务器应用程序](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [创建 Windows Embedded 应用程序](../../apps/get-started/creating-windows-embedded-applications.md)


如果已经熟悉 Configuration Manager 应用程序，则可以跳过本主题。 然而，在创建和部署应用程序时，可能需要查看[创建应用程序](../../apps/deploy-use/create-applications.md)以了解所有可用的选项。  

## <a name="before-you-start"></a>开始之前  

请务必查看[应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)中的信息，以确保已准备好站点以安装应用程序并确保已了解本主题中使用的术语。  

 此外，请确保“Contoso.msi”应用的安装文件位于网络上的可访问位置。  

## <a name="create-the-configuration-manager-application"></a>创建 Configuration Manager 应用程序  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>启动创建应用程序向导并创建应用程序  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用程序”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建应用程序”。  

4.  在“创建应用程序向导”的“常规”页上，选择“自动检测安装文件中有关此应用程序的信息”。 这将使用从 .msi 安装文件中提取出来的信息预设向导中的某些信息。 然后指定以下信息：  

    -   **类型**：选择“Windows Installer (\*.msi 文件)”。  

    -   **位置**：键入安装文件 **Contoso.msi** 的位置（或选择“浏览”以选择位置）。 注意，必须以 *\\\Server\Share\File* 格式指定位置，以便 Configuration Manager 找到安装文件。  

    此时的屏幕截图如下：  

    ![应用管理向导常规页](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

5.  选择“下一步”。 “导入信息”页上，会显示有关该应用以及导入到 Configuration Manager 的任何关联文件的一些信息。 完成后，再次选择“下一步”。  

6.  在“常规信息”页上，可以提供有关该应用程序进一步的信息，以帮助在 Configuration Manager 控制台中进行排序和查找。  

     此外，通过“安装程序”字段，可以指定将用于在电脑上安装该应用程序的完整命令行。 可以编辑此字段以添加自己的属性（例如添加“/q”以进行无人参与的安装）。  

    > [!TIP]  
    >  导入应用程序安装文件后，向导的此页上的某些字段可能已自动填充。  

     此时的屏幕截图如下：  

     ![应用管理向导常规信息页](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

7.  选择“下一步”。 在“摘要”页面上，可以确认应用程序设置，然后完成向导。  

 应用创建结束。 若要找到它，请在“软件库”工作区中，展开“应用程序管理”，然后选择“应用程序”。 对于此示例，你将看到：  

 ![最终应用图形](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>检查应用文件的属性及其部署类型  

你已创建了应用程序，现在便可以优化应用程序设置（如果需要）。 若要查看应用程序属性，请选择应用，然后在“主页”选项卡的“属性”组中，选择“属性”。  

 在“<Contoso\> 应用程序属性”对话框中，会显示许多项，可以通过配置这些项对应用程序的行为进行微调。 有关可配置的所有设置的详细信息，请参阅 [Create applications](../../apps/deploy-use/create-applications.md)（创建应用程序）。 就本示例而言，你只是改变应用程序部署类型的某些属性。  

 选择“部署类型”选项卡>“Contoso 应用程序”部署类型 >“编辑”。  

此时将看到如下所示的对话框：  

![应用管理应用属性页](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>将要求添加到部署类型  
 这些要求指定必须满足什么条件才能将应用程序安装到设备上。  可以从内置要求中选择或创建自己的要求。 在此示例中，添加指定仅在运行 Windows 10 的电脑上安装应用程序的要求。  

1.  在刚打开的部署类型属性页中，选择“要求”选项卡。  

2.  选择“添加”以打开“创建要求”对话框。  

3.  在“创建要求”  对话框中，指定以下信息：  

    -   “类别”：“设备”  

    -   “条件”：“操作系统”  

    -   “规则类型”：“值”  

    -   “运算符”：“其中一个”  

    -   从操作系统列表中，选择“Windows 10” 。  

    将显示如下对话框：  

    ![应用管理要求页](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  选择“确定”以关闭打开的每个属性页。 然后返回到 Configuration Manager 控制台中的“应用程序”列表。  

> [!TIP]  
>  这些要求有助于减少所需的 Configuration Manager 集合的数量。 由于指定了只能在运行 Windows 10 的电脑上安装该应用程序，因此稍后可以将它部署到包含运行各种不同操作系统的电脑的集合。 但是，该应用程序只能安装在 Windows 10 电脑上。  

## <a name="add-the-application-content-to-a-distribution-point"></a>将应用程序内容添加到分发点  

接下来，若要将应用程序部署到电脑，请确保将应用程序内容复制到分发点。 电脑将访问分发点以安装应用程序。  

> [!TIP]  
>  若要查找有关 Configuration Manager 中的分发点和内容管理的详细信息，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

1.  在 Configuration Manager 控制台中，选择“软件库”。  

2.  在“软件库”工作区中，展开“应用程序”。 然后，在应用程序列表中，选择已创建的“Contoso 应用程序”。  

3.  在“主页”选项卡上的“部署”组中，选择“分发内容”。  

4.  在“分发内容向导”的“常规”页上，检查应用程序名称是否正确，然后选择“下一步”。  

5.  在“内容”页上，查看将被复制到分发点的信息，然后选择“下一步”。  

6.  在“内容目标”页上，选择“添加”以选择一个或多个分发点或要在其上安装应用程序内容的分发点组。  

7.  完成向导。  

可以从“监视”工作区中的“分发状态” > “内容状态”下检查是否已将应用程序内容成功复制到了分发点。  

## <a name="deploy-the-application"></a>部署应用程序  

接下来，将应用程序部署到层次结构中的设备集合。 在此示例中，需要将应用程序部署到“所有系统”设备集合。  

> [!TIP]  
>  请记住，根据之前选定的要求，只有 Windows 10 计算机将安装应用程序。  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用程序”。  

3.  从应用程序列表中，选择之前创建的应用程序（“Contoso 应用程序”），然后在“主页”选项卡上的“部署”组中，选择“部署”。  

4.  在“部署软件向导”的“常规”页上，选择“浏览”以选择“所有系统”设备集合。  

5.  在“内容”页上，检查是否已选择了要让电脑从中安装应用程序的分发点。  

6.  在“部署设置”页上，确保将部署操作设置为“安装”，并且将部署目的设置为“必需”。  

    > [!TIP]  
    >  通过将部署目的设置为“必需”，确保在满足设定要求的电脑上安装应用程序。 如果将该值设置为“可用” ，则用户可以根据软件中心的要求安装应用程序。  

7.  在“计划”  页上，你可以配置安装应用程序的时间。 对于此示例，选择“在可用时间之后尽快” 。  

8.  在“用户体验”页上，选择“下一步”以接受默认值。  

9. 完成向导。  

使用以下“监视应用程序”部分中的信息，查看应用程序部署的状态。  

## <a name="monitor-the-application"></a>监视应用程序  
 在本部分中，将快速查看刚才部署的应用程序的部署状态。  

### <a name="to-review-the-deployment-status"></a>若要查看部署状态  

1.  在 Configuration Manager 控制台中，选择“监视” > “部署”。  

3.  从部署列表中选择“Contoso 应用程序” 。  

4.  在“主页”选项卡上的“部署”组中，选择“查看状态”。  

5.  选择以下选项卡之一，以查看有关应用程序部署的更多更新状态：  

    -   **成功**：应用程序已成功安装在了指定的电脑上。  

    -   **正在进行**：应用程序尚未完成安装。  

    -   **错误**：在指定的电脑上安装应用程序时出现了错误。 此外还会显示有关错误的更多信息。  

    -   **不符合要求**：未在指定的设备上尝试安装，因为它们不符合配置的要求（在此示例中，因为它们未运行 Windows 10）。  

    -   **未知**：Configuration Manager 无法报告部署状态。 稍后重新检查。  

> [!TIP]  
>  可以采用几种方式来监视应用程序部署。 有关完整详细信息，请参阅[监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  

## <a name="end-user-experience"></a>最终用户体验  

如果用户的电脑由 Configuration Manager 管理且运行的是 Windows 10，则会看到一条消息，告知他们必须安装 Contoso 应用程序。 用户接受安装后，将安装应用程序。  
