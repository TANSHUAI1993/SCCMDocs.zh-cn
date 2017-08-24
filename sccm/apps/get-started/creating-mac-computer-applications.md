---
title: "创建 Mac 计算机应用程序 | Microsoft Docs"
description: "请参阅创建和部署适用于 Mac 计算机的应用程序时必须考虑的注意事项。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: ffd66a4047ec253704e9772e2c3e3a4d9db7c46f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建 Mac 计算机应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

创建和部署适用于 Mac 计算机的应用程序时，请记住以下注意事项。  

> [!IMPORTANT]  
>  本主题中的过程涵盖了有关将应用程序部署到安装了 Configuration Manager 客户端的 Mac 计算机的信息。 使用 Microsoft Intune 注册的 Mac 计算机不支持应用程序部署。  

## <a name="general-considerations"></a>一般注意事项  
 可以使用 System Center Configuration Manager 将应用程序部署到运行 Configuration Manager Mac 客户端的 Mac 计算机。 将软件部署到 Mac 计算机的步骤与将软件部署到 Windows 计算机的步骤相似。 但是，在为 Configuration Manager 管理的 Mac 计算机创建和部署应用程序之前，请考虑以下事项：  

-   将 Mac 应用程序包部署到 Mac 计算机之前，必须使用 Mac 计算机上的 **CMAppUtil** 工具将这些应用程序转换为 Configuration Manager 可以读取的格式。  

-   Configuration Manager 不支持对用户部署 Mac 应用程序。 而是必须将这些应用程序部署到设备。 同样，对于 Mac 应用程序部署，Configuration Manager 不支持“部署软件向导”的“部署设置”页上的“将软件预先部署到用户的主要设备”选项。  

-   Mac 应用程序支持模拟的部署。  

-   无法将应用程序部署到目的为“可用” 的 Mac 计算机。  

-   Mac 计算机不支持用于在部署软件时发送唤醒数据包的选项。  

-   Mac 计算机不支持使用后台智能传输服务 (BITS) 下载应用程序内容。 如果应用程序下载失败，则将从头重新开始下载。  

-   为 Mac 计算机创建部署类型时，Configuration Manager 不支持全局条件。  

## <a name="steps-to-create-and-deploy-an-application"></a>用于创建和部署应用程序的步骤  
 下表提供了为 Mac 计算机创建和部署应用程序的步骤、详细信息和其他信息。  

|步骤|详细信息|  
|----------|-------------|  
|**步骤 1**：准备用于 Configuration Manager 的 Mac 应用程序|从 Mac 软件包中创建 Configuration Manager 应用程序之前，必须使用 Mac 计算机上的 **CMAppUtil** 工具将 Mac 软件转换为 Configuration Manager**.cmmac** 文件。|  
|**步骤 2**：创建包含 Mac 软件的 Configuration Manager 应用程序|请使用“创建应用程序向导”为 Mac 软件创建应用程序。|  
|**步骤 3**：创建 Mac 应用程序部署类型|只有在未从应用程序中自动导入此信息的情况下，才需要执行此步骤。|  
|**步骤 4**：部署 Mac 应用程序|使用“部署软件向导”将应用程序部署到 Mac 计算机。|  
|**步骤 5**：监视 Mac 应用程序的部署|监视到 Mac 计算机的应用程序部署是否成功。|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>为 Mac 计算机创建和部署应用程序的补充过程  
 使用以下过程为 Configuration Manager 管理的 Mac 计算机创建和部署应用程序。  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>步骤 1：准备用于 Configuration Manager 的 Mac 应用程序  
 为 Mac 计算机创建和部署 Configuration Manager 应用程序的过程类似于 Windows 计算机的部署过程。 但是，在创建包含 Mac 部署类型的 Configuration Manager 应用程序之前，必须使用 **CMAppUtil** 工具准备应用程序。 此工具是与 Mac 客户端安装文件一起下载的。 **CMAppUtil** 工具可以收集有关应用程序的信息，此信息包含以下 Mac 包中的检测数据：  

-   Apple 磁盘映像 (.dmg)  

-   元包文件 (.mpkg)  

-   Mac OS X 安装程序包 (.pkg)  

-   Mac OS X 应用程序 (.app)  

收集应用程序信息之后， **CMAppUtil** 则会创建扩展名为 **.cmmac**的文件。 此文件包含 Mac 软件的安装文件和有关可用于评估应用程序是否已安装的检测方法的信息。 **CMAppUtil** 还可以处理包含多个 Mac 应用程序的 **.dmg** 文件并为每个应用程序创建不同的部署类型。  

1.  将 Mac 软件安装包复制到 Mac 计算机上的文件夹中，你在该文件夹中已经提取了从 Microsoft 下载中心下载的 **macclient.dmg** 文件的内容。  

2.  在相同的 Mac 计算机上，打开终端窗口并导航到在其中提取 **macclient.dmg** 文件内容的文件夹。  

3.  导航到“工具”文件夹并键入以下命令行命令：  

     **./CMAppUtil** *<properties\>*  

     例如，想将存储在用户的桌面文件夹中，名为 **MySoftware.dmg** 的 Apple 磁盘图像文件转换为同一文件夹中的 **cmmac** 文件。 还需为磁盘图像文件中找到的所有应用程序创建 **cmmac** 文件。 若要执行此操作，请使用以下命令行：  

     **./CMApputil –c /Users/** *<User Name\>* **/Desktop/MySoftware.dmg -o /Users/** *<User Name\>* **/Desktop -a**  

    > [!NOTE]  
    >  应用程序名称不能超过 128 个字符。  

     若要为 **CMAppUtil**配置选项，请使用下表中的命令行属性：  

  	|属性|更多信息|  
  	|--------------|----------------------|  
  	|**-h**|显示可用命令行属性。|  
  	|**-r**|将提供的 **detection.xml** 文件的 **.cmmac** 输出到 **stdout**。 输出包含检测参数以及用于创建 **CMAppUtil** 文件的 **.cmmac** 的版本。|  
  	|**-c**|指定要转换的源文件。|  
  	|**-o**|指定输出路径，同时连带 –c 属性。|  
  	|**-a**|针对磁盘图像文件中的所有应用程序和包，自动创建 .cmmac 文件，同时连带 –c 属性。|  
  	|**-s**|在未找到检测参数的情况下跳过生成 **detection.xml** ，并强制创建无 **.cmmac** 文件的 **detection.xml** 文件。|  
  	|**-v**|显示 **CMAppUtil** 工具中的更多详细输出，以及诊断信息。|  

4.  确保在你指定的输出文件夹中已经创建了 **.cmmac** 文件。  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>创建包含 Mac 软件的 Configuration Manager 应用程序  

使用以下过程帮助你为 Configuration Manager 管理的 Mac 计算机创建应用程序。  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用程序”。  

3.  在“主页”选项卡上的“创建”组中，选择“创建应用程序”。  

4.  在“创建应用程序向导”  的“常规” 页上，选择“自动检测安装文件中有关此应用程序的信息” 。  

    > [!NOTE]  
    >  如果想要自已指定有关应用程序的信息，请选择“手动指定应用程序信息”。 有关如何手动指定信息的详细信息，请参阅 [如何使用 System Center Configuration Manager 创建应用程序](../../apps/deploy-use/create-applications.md)。  

5.  在“类型”  下拉列表中选择“Mac OS X” 。  

6.  在“位置”字段中，指定采用 *\\\\<server\>\\<share\>\\<filename\>* 形式且指向将检测应用程序信息的 Mac 应用程序安装文件（**.cmmac** 文件）的 UNC 路径。 或者，选择“浏览”以浏览和指定安装文件位置。  

    > [!NOTE]  
    >  你必须具有对包含该应用程序的 UNC 路径的访问权限。  

7.  选择“下一步”。  

8.  在“创建应用程序向导”的“导入信息”页上，查看已导入的信息。 如有必要，可以选择“上一步”以返回并更正任何错误。 选择“下一步”以继续。  

9. 在“创建应用程序向导”的“常规信息”页上，指定有关应用程序的信息，如应用程序名称、备注、版本和可选参考，以帮助你在 Configuration Manager 控制台中引用应用程序。  

    > [!NOTE]  
    >  如果以前从应用程序安装文件中获取了某些应用程序信息，则此页上可能已经有这些信息。  

10. 选择“下一步”，查看“摘要”页上的应用程序信息，然后完成“创建应用程序向导”。  

11. 新应用程序会显示在 Configuration Manager 控制台的“应用程序”节点中。  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>步骤 3：创建 Mac 应用程序部署类型  
 使用以下过程帮助你为 Configuration Manager 管理的 Mac 计算机创建部署类型。  

> [!NOTE]  
>  如果在“创建应用程序向导”中自动导入了关于应用程序的信息，则可能已经创建了应用程序的部署类型。  

1.  在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用程序”。  

3.  选择应用程序。 然后在“主页”选项卡上的“应用程序”组中，选择“创建部署类型”以为此应用程序创建新部署类型。  

    > [!NOTE]  
    >  还可以从“创建应用程序向导”和“<应用程序名称\>”“属性”对话框的“部署类型”选项卡中启动“创建部署类型向导”。  

4.  在“创建部署类型向导”的“常规”页上的“类型”拉列表中选择“Mac OS X”。  

5.  在“位置”字段中，指定采用 \\\\<server\>\\<share\>\\<filename\> 形式且指向应用程序安装文件（**.cmmac** 文件）的 UNC 路径。 或者，选择“浏览”以浏览和指定安装文件位置。  

    > [!NOTE]  
    >  你必须具有对包含该应用程序的 UNC 路径的访问权限。  

6.  选择“下一步”。  

7.  在“创建部署类型向导”  的“导入信息” 页上，查看已导入的信息。 如有必要，选择“上一步”以返回并更正任何错误。 选择“下一步”以继续。  

8.  在“创建部署类型向导”  的“常规信息” 页上，指定有关应用程序的信息，如应用程序名称、备注以及部署类型可采用的语言。  

    > [!NOTE]  
    >  如果以前从应用程序安装文件中获取了某些部署类型信息，则此页上可能已经有这些信息。  

9. 选择“下一步”。  

10. 在“创建部署类型向导”的“要求”页上，可以指定在 Mac 计算机上安装部署类型之前必须满足的条件。  

11. 选择“添加”以打开“创建要求”对话框并添加新要求。  

    > [!NOTE]  
    >  还可以在“<部署类型名称\> 属性”对话框的“要求”选项卡上添加新要求。  

12. 从“类别”  下拉列表中选择“此要求适用于设备”。  

13. 从“条件”下拉列表中，选择要用于评估 Mac 计算机是否满足安装要求的条件。 根据所选择的类别，此列表的内容会有所不同。  

14. 从“运算符”下拉列表中，选择运算符，此运算符用于将所选条件与指定值进行比较以评估用户或设备是否满足安装要求。 可用运算符将因所选条件而异。  

15. 在“值”字段中指定值，这些值将与所选条件和运算符一起用于评估用户或设备是否满足安装要求。 可用值将因所选条件和运算符而异。

16. 选择“确定”以保存要求规则并退出“创建要求”对话框。  

17. 在“创建部署类型向导”的“要求”页上，选择“下一步”。  

18. 在“创建部署类型向导”  的“摘要” 页上，查看向导要采取的操作。  如有必要，选择“上一步”以返回并更改部署类型设置。 选择“下一步”以创建部署类型。  

19. 在“进度”页面完成之后，查看已采取的操作，然后选择“关闭”以完成“创建部署类型向导”。  

20. 如果从“创建应用程序向导”中启动了此向导，则将返回“部署类型”页。  

###  <a name="deploy-the-mac-application"></a>部署 Mac 应用程序  
 将应用程序部署到 Mac 计算机的步骤与将应用程序部署到 Windows 计算机的步骤相同，但以下差异除外：  

-   不支持对用户部署应用程序。  

-   不支持目的为“可用”  的部署。  

-   不支持“部署软件向导”的“部署设置”页上的“将软件预先部署到用户的主要设备”选项。  

-   因为 Mac 计算机不支持软件中心，所以会忽略“部署软件向导”的“用户体验”页上的“用户通知”设置。  

-   Mac 计算机不支持用于在部署软件时发送唤醒数据包的选项。  

> [!NOTE]  
>  可以构建一个只包含 Mac 计算机的集合。 为此，请创建一个使用查询规则的集合，并使用[如何创建查询](../../core/servers/manage/create-queries.md)主题中的 WQL 查询示例。  

 有关详细信息，请参阅[部署应用程序](../../apps/deploy-use/deploy-applications.md)。  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>步骤 5：监视 Mac 应用程序的部署  
 你可以使用监视 Windows 计算机应用程序部署的过程来监视 Mac 计算机应用程序部署。  

 有关详细信息，请参阅[监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)。  
