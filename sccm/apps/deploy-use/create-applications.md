---
title: "创建应用程序 | System Center Configuration Manager"
description: "使用 System Center Configuration Manager 创建和部署应用程序和部署类型。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7aca3f0a261a5506d68c57904c9b9f0d023c84e2


---
# <a name="create-applications-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建应用程序

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 应用程序包含将软件部署到设备所需的文件和信息。 应用程序包含一个或多个构成安装文件的部署类型以及安装软件所需的信息。 部署类型还包含指定软件的部署时间和方法的规则。  

 可以使用下列方法创建应用程序：  

-   通过读取应用程序安装文件来自动创建应用程序和部署类型。  

-   手动创建应用程序并稍后添加部署类型。  

-   从文件导入应用程序。  

 使用下列步骤创建 Configuration Manager 应用程序和部署类型。  

## <a name="start-the-create-application-wizard"></a>启动创建应用程序向导  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建应用程序” 。  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>指定是要自动检测应用程序信息还是手动定义该信息  

-   如果要创建具有单一部署类型（例如没有依赖关系或要求的 Windows Installer 文件）的简单应用程序，请使用“自动检测应用程序信息” 。 使用此过程创建了应用程序后，你可以根据需要对其进行编辑，以便添加或更改部署类型以及添加检测方法、依赖关系或要求。  

-   使用“手动指定应用程序信息” 来创建具有多个部署类型、依赖关系、检测方法或要求的更复杂的应用程序。  

### <a name="automatically-detect-application-information"></a>自动检测应用程序信息  

1.  在创建应用程序向导的“常规”  页上，选择“自动检测安装文件中有关此应用程序的信息”  复选框。  

2.  在“类型”  下拉列表中，选择要用于检测应用程序信息的应用程序安装文件类型。 有关可用安装类型的信息，请参阅本主题中的 [Configuration Manager 支持的部署类型](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager)。  
  
3.  在“位置”字段中，以 \\\\server\\share\\\filename 格式或以要用来检测应用程序信息的应用程序安装文件的存储链接来指定 UNC 路径。 或者，单击“浏览”以浏览到安装文件。  
    > [!IMPORTANT]  
    >  如果选择“Windows Installer(\*.msi 文件)”作为应用程序类型，则指定文件夹中的所有文件都将随应用程序导入，并将发送到分发点。 请确保你指定的文件夹中只有安装应用程序所必需的文件。 Configuration Manager 经测试可支持应用程序包中多达 20,000 个应用程序文件。 如果你的应用程序包含更多文件，请考虑创建具有较少数量文件的多个应用程序。  
    >  对于包含应用程序的 UNC 路径以及包含应用程序内容的任何子文件夹，你必须具有访问权限。  

4.  在“创建应用程序向导”的“导入信息”页上，查看已导入的信息，然后单击“下一步”。 如有必要，可以单击“上一步”以返回并更正任何错误。  

5.  在“创建应用程序向导”的“常规信息”页上，指定以下信息：  

    > [!NOTE]  
    >  如果已从应用程序安装文件中自动获取了其中的一些信息，这些信息可能已填充。 此外，显示的选项可能会因创建的应用程序类型而异。  

    -   提供有关应用程序的常规信息，例如应用程序名称、备注、版本以及可选的引用，有助于在 Configuration Manager 控制台中引用应用程序。  

    -   **安装程序** - 指定安装应用程序部署类型所需的安装程序和任何必需属性。  

        > [!TIP]  
        >  如果未显示安装程序，请单击“浏览”  并浏览到安装程序位置。  

    -   **安装行为** - 指定是仅为当前已登录用户还是为所有用户安装应用程序部署类型。 你也可以指定为所有用户安装部署类型（如果部署到设备）或仅安装到指定用户（如果部署到用户）。  

    -   **使用自动 VPN 连接（若已配置）** - 如果向启动应用程序的设备部署了 VPN 配置文件，则在应用启动时启动 VPN 连接（仅适用于 Windows 8.1 和 Windows Phone 8.1）。  

         在 Windows Phone 8.1 设备上，如果有多个 VPN 配置文件部署到设备，则不支持自动 VPN 连接。  
  
         有关 VPN 配置文件的详细信息，请参阅 [VPN 配置文件](../../protect/deploy-use/vpn-profiles.md)。  
  
6.  单击“下一步” ，查看“摘要”  页上的应用程序信息，然后完成创建应用程序向导。  

 新的应用程序显示在 Configuration Manager 控制台中的“应用程序”节点中，且已完成创建一个应用程序的过程。 如果想要将更多部署类型添加到应用程序，请参阅本主题中的[为应用程序创建部署类型](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application)。  

### <a name="manually-specify-application-information"></a>手动指定应用程序信息  

1.  在“创建应用程序向导”的“常规”页上，选择“手动指定应用程序信息”，然后单击“下一步”。  

2.  指定有关应用程序的常规信息，例如应用程序名称、备注、版本以及可选的引用，有助于在 Configuration Manager 控制台中查找应用程序。  

3.  在“创建应用程序向导”的**应用程序目录**页上，指定以下信息：  

    -   **所选语言** - 在下拉列表中选择要配置的应用程序的语言版本。 单击“添加/删除”  为此应用程序配置更多语言。  

    -   **本地化的应用程序名称** - 以在“所选语言”  下拉列表中选择的语言指定应用程序名称。  

        > [!IMPORTANT]  
        >  你必须为配置的每个语言版本指定一个本地化应用程序名称。  

    -   **用户类别** - 单击“编辑”  以在“所选语言”  下拉列表中选择的语言指定应用程序类别。 软件中心的用户可以使用这些所选类别来帮助对可用应用程序进行筛选和排序。  

    -   **用户文档** - 单击“浏览”  指定文件的 URL 或 UNC 路径和文件名，软件中心的用户可阅读该文件来获取有关此应用程序的详细信息。  

    -   **链接文本** - 指定将取代应用程序的 URL 显示的文本。  

    -   **应用程序隐私 URL** - 指定链接到应用程序的隐私声明的 URL。  

    -   **本地化的描述** - 以在“所选语言”  下拉列表中选择的语言为此应用程序输入描述。  

    -   **关键字** - 以在“所选语言”  下拉列表中选择的语言输入关键字的列表。 这些关键字将帮助软件中心的用户搜索应用程序。  

    -   **图标** - 单击“浏览”  从可用图标中为此应用程序选择一个图标。 如果不指定图标，则会为此应用程序使用默认图标。  

    -   **将此应用显示为特色应用并在公司门户中突出显示** - 选择此选项可在公司门户中突出显示应用。  

4.  在创建应用程序向导的“部署类型”  页上，单击“添加”  创建一个新部署类型。  
有关详细信息，请参阅本主题中的[为应用程序创建部署类型](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application)。  

5.  单击“下一步” ，查看“摘要”  页上的应用程序信息，然后完成创建应用程序向导。  

 新应用程序会出现在 Configuration Manager 控制台的“应用程序”节点中。  

##  <a name="create-deployment-types-for-the-application"></a>为应用程序创建部署类型  
 如果在创建部署类型向导的“常规”  页上选择“从安装文件中自动识别有关此部署类型的信息”  复选框，则你可能无需完成下列过程中的某些步骤。  

## <a name="start-the-create-deployment-type-wizard"></a>启动创建部署类型向导  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。  

3.  选择应用程序，然后在“主页”选项卡上的“应用程序”组中，单击“创建部署类型”。  

> [!TIP]  
>  你还可以从“创建应用程序向导”和从 <应用程序名称\>“属性”对话框的“部署类型”选项卡中启动“创建部署类型向导”。  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-configure-the-information"></a>指定是要自动检测部署类型信息还是手动配置该信息  
 使用下列过程之一来自动检测或手动配置部署类型信息。  

### <a name="automatically-detect-the-deployment-type-information"></a>自动检测部署类型信息  

1.  在“创建部署类型向导”的“常规”页上，选择“从安装文件中自动识别有关此部署类型的信息”复选框。  

2.  在“类型”字段中，选择要用于检测部署类型信息的应用程序安装文件类型。  
  
3.  在“位置”字段中，以 \\\\server\\share\\filename 格式，或以指向应用程序安装文件的存储链接和要用于检测部署类型信息的内容来指定 UNC 路径。 还可以单击“浏览”以找到安装文件。  
    > [!NOTE]  
    >  对于包含应用程序的 UNC 路径以及包含应用程序内容的任何子文件夹，你必须具有访问权限。  

4.  在“创建部署类型向导”的“导入信息”页上，查看已导入的信息，然后单击“下一步”。 你也可以单击“上一步”返回并更正任何错误。  

5.  在“创建部署类型向导”的“常规信息”页上，指定以下信息：  

    > [!NOTE]  
    >  如果从应用程序安装文件中读取了某些部署类型信息，则可能已经存在这些信息。 此外，显示的选项可能会因你创建的部署类型而异。  

    -   指定有关部署类型的常规信息，例如名称、管理员备注和可用语言。  

    -   **安装程序** - 指定安装部署类型所需的安装程序和任何属性。  

    -   **安装行为** - 指定是为当前已登录用户还是为所有用户安装部署类型。 你也可以指定是为所有用户安装部署类型（如果部署到设备），还是仅为某个用户安装部署类型（如果部署到用户）。  

    -   **使用自动 VPN 连接(若已配置)** - 如果向启动应用程序的设备部署了 VPN 配置文件，则在应用启动时启动 VPN 连接（仅适用于 Windows 8.1 和 Windows Phone 8.1）。 如果已将多个 VPN 配置文件部署到 Windows 8.1 设备，则默认情况下使用第一个部署的 VPN 配置文件。  

         在 Windows Phone 8.1 设备上，如果有多个 VPN 配置文件部署到设备，则不支持自动 VPN 连接。  

         有关 VPN 配置文件的详细信息，请参阅 [System Center Configuration Manager 中的 VPN 配置文件](../../protect/deploy-use/vpn-profiles.md)。  

6.  单击“下一步” ，然后继续[为部署类型指定内容选项](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type)。  

### <a name="manually-configure-the-deployment-type-information"></a>手动配置部署类型信息  

1.  在“创建部署类型向导”的“常规”  页上，选择“手动指定部署类型信息” 。  

2.  在“类型”字段中，选择要用于检测部署类型信息的应用程序安装文件类型。 你可以选择将在自动检测部署类型信息时使用的相同安装类型，此外还可以指定用于安装部署类型的脚本。  

3.  在“创建部署类型向导”的“常规信息”页上，指定部署类型的名称、可选描述、提供此部署类型所要采用的语言，然后单击“下一步”。  

4.  转至[为部署类型指定内容选项](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type)。  

##  <a name="specify-content-options-for-the-deployment-type"></a>为部署类型指定内容选项  

1.  在“创建部署类型向导”的“内容”页上，指定以下信息：  
  
    -   内容位置 - 为此部署类型的内容指定位置，或单击“浏览”选择部署类型内容文件夹。  
        > [!IMPORTANT]  
        >  站点服务器计算机的系统帐户必须具有所指定内容位置的权限。  

    -   **保留客户端缓存中的内容** - 选择此选项，指定是否应将内容无限期保留在客户端计算机上的缓存中（即使它已运行）。 尽管此选项对于某些部署（例如基于 Windows Installer 的软件，该软件需要有本地源副本才能应用更新）可能很有用，但它会减少可用缓存空间。 如果选择此选项，在缓存没有足够的可用空间的情况下，将可能会导致大型部署稍后失败。  

    -   **允许客户端与同一子网上的其他客户端共享内容** - 选择此选项，通过允许客户端从网络上已下载并缓存了内容的其他本地客户端下载内容来减轻网络上的负载。 此选项使用 Windows BranchCache 技术。  

    -   **安装程序** - 指定安装程序的名称和任何所需安装参数，或单击“浏览”  以找到安装文件。  

    -   **安装开始于** -（可选）指定包含部署类型的安装程序的文件夹。 此文件夹可以是客户端上的绝对路径，或包含安装文件的分发点文件夹的路径。  

    -   **卸载程序** -（可选）指定卸载程序的名称和任何所需参数，或单击“浏览”  以找到它。  

    -   **卸载开始于** -（可选）指定包含部署类型的卸载程序的文件夹。 此文件夹可以是客户端上的绝对路径，或者是相对于包含包的分发点文件夹的路径。  

    -   **在 64 位客户端上以 32 位进程形式运行安装和卸载计划** - 使用基于 Windows 的计算机上的 32 位文件和注册表位置来运行部署类型的安装程序。  

2.  单击“下一步” 。  

## <a name="configure-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>将检测方法配置为指明部署类型的状态（仅适用于 Windows PC）  
 此过程配置用于指示部署类型是否已安装的检测方法。  

1.  在“创建部署类型向导”的“检测方法”页上，选择“配置对此部署类型的状态进行检测的规则”，然后单击“添加子句”。  

    > [!NOTE]  
    >  你也可以选择“使用自定义脚本检测此部署类型的状态”。 有关详细信息，请参阅本主题中的“使用自定义脚本确定部署类型的状态”部分。  

2.  在“检测规则”对话框的“设置类型”下拉列表中，选择要用于检测部署类型的状态的方法。 你可以从下列可用的方法中选择：  

    -   **文件系统** - 使用此方法检测客户端设备上是否存在指定的文件或文件夹，从而指明已经安装了应用程序。  

        > [!NOTE]  
        >  “文件系统”  设置类型不支持在“路径”字段中指定网络共享的 UNC 路径。 你只能指定客户端设备上的本地路径。  
        >   
        >  选择“此文件或文件夹与 64 位系统中的 32 位应用程序相关联”选项，以首先检查 32 位文件位置中是否有指定的文件或文件夹。 如果未找到此文件或文件夹，则将搜索 64 位位置。  

    -   **注册表** - 你可以使用此方法检测客户端设备上是否存在指定的注册表项或注册表值，从而指明已经安装了应用程序。  

        > [!NOTE]  
        >  选择“此注册表项与 64 位系统上的 32 位应用程序相关联”  选项，以首先检查 32 位注册表位置中是否有指定的注册表项。 如果未找到此注册表项，则将搜索 64 位位置。  

    -   **Windows Installer** - 使用此方法检测客户端设备上是否存在指定的 Windows Installer 文件，从而指明已经安装了应用程序。  

3.  指定想要用于检测是否安装了此部署类型的项目的详细信息。 例如，可以使用文件、文件夹、注册表项、注册表值或者 Windows Installer 产品代码。  

4.  指定想要按照项目（用于检测是否安装了此部署类型）评估的值的详细信息。 例如，你使用文件来确定是否安装了部署类型，则可以选择“为了指明此应用程序的状态，目标系统上必须存在文件系统设置”复选框。  

5.  单击“下一步”以关闭“检测规则”对话框。  

###  <a name="use-a-custom-script-to-determine-the-presence-of-a-deployment-type"></a>使用自定义脚本确定部署类型的状态  

1.  在“创建部署类型向导”的“检测方法”页上，选择“使用自定义脚本检测此部署类型的状态”复选框，然后单击“编辑”。  

2.  在“脚本编辑器”对话框的“脚本类型”下拉列表中，选择要用于检测部署类型的脚本语言。  

3.  在“脚本内容”字段中，输入要使用的脚本。 你还可以将现有脚本的内容粘贴在此字段中，或单击“打开”以浏览到现有的已保存脚本。 Configuration Manager 通过读取写入到“标准输出 (STDOUT)”输出流、“标准错误 (STDERR)”输出流和来自脚本的退出代码的值来确定从脚本得到的结果。 如果退出代码为非零值，则脚本已经失败，并且应用程序检测状态为未知。 如果退出代码为零，并且 STDOUT 包含数据，则应用程序检测状态为“已安装”。  

使用下表确定如何使用脚本输出来确定是否安装了应用程序。  

|脚本退出代码|详细信息|
|-|-|
|0|**从 STDOUT 中读取的数据** - 空<br /><br /> **从 STDERR 中读取的数据** - 空<br /><br /> **脚本结果** - 成功<br /><br /> **应用程序检测状态** - 未安装|  
|0|**从 STDOUT 中读取的数据** - 空<br /><br /> **从 STDERR 中读取的数据** - 不为空<br /><br /> **脚本结果** - 失败<br /><br /> **应用程序检测状态** - 未知|  
|0|**从 STDOUT 中读取的数据** - 不为空<br /><br /> **从 STDERR 中读取的数据** - 空<br /><br /> **脚本结果** - 成功<br /><br /> **应用程序检测状态** - 已安装|  
|0|**从 STDOUT 中读取的数据** - 不为空<br /><br /> **从 STDERR 中读取的数据** - 不为空<br /><br /> **脚本结果** - 成功<br /><br /> **应用程序检测状态** - 已安装|  
|非零值|**从 STDOUT 中读取的数据** - 空<br /><br /> **从 STDERR 中读取的数据** - 空<br /><br /> **脚本结果** - 失败<br /><br /> **应用程序检测状态** - 未知|  
|非零值|**从 STDOUT 中读取的数据** - 空<br /><br /> **从 STDERR 中读取的数据** - 不为空<br /><br /> **脚本结果** - 失败<br /><br /> **应用程序检测状态** - 未知|  
|非零值|**从 STDOUT 中读取的数据** - 不为空<br /><br /> **从 STDERR 中读取的数据** - 空<br /><br /> **脚本结果** - 失败<br /><br /> **应用程序检测状态** - 未知|  
|非零值|**从 STDOUT 中读取的数据** - 不为空<br /><br /> **从 STDERR 中读取的数据** - 不为空<br /><br /> **脚本结果** - 失败<br /><br /> **应用程序检测状态** - 未知|  

下表包含可用于编写自己的应用程序检测脚本的 Microsoft Visual Basic (VB) 示例脚本。  

|Visual Basic 示例脚本|描述|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|此脚本返回不为零的退出代码，这表示它未成功运行。 在这种情况下，应用程序检测状态为未知。|  
|**WScript.StdErr.Write "Script failed"**<br /><br /> **WScript.Quit(0)**|此脚本返回零退出代码，但是 STDERR 的值不为空，这表示脚本未成功运行。 在这种情况下，应用程序检测状态为未知。|  
|**WScript.Quit(0)**|此脚本返回零退出代码，这表示它已成功运行。 但是，STDOUT 的值为空，这表示未安装应用程序。|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.Quit(0)**|此脚本返回零退出代码，这表示它已成功运行。 STDOUT 的值不为空，这表示安装了应用程序。|  
|**WScript.StdOut.Write "The application is installed"**<br /><br /> **WScript.StdErr.Write "Completed"**<br /><br /> **WScript.Quit(0)**|此脚本返回零退出代码，这表示它已成功运行。 STDOUT 和 STDERR 的值不为空，这表示安装了应用程序。|  

> [!NOTE]  
    >  可用于脚本的最大大小为 32 KB。  

4.  单击“确定”  以关闭“脚本编辑器”  对话框。  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>指定部署类型的用户体验选项  
 这些设置指定将应用程序安装到设备上的方式和用户将看到的内容。  

1.  在“创建部署类型向导”的“用户体验”页上，指定下列信息：  

    -   **安装行为** - 在下拉列表中选择以下选项之一：  

        -   **针对用户安装** - 仅针对应用程序所部署到的用户安装应用程序。  

        -   **针对系统安装** - 应用程序仅安装一次并且可供所有用户使用。  

        -   **如果资源是设备，则针对系统安装；否则针对用户安装** - 如果将应用程序部署到设备，则将为所有用户安装它。 如果将应用程序部署到用户，则将仅为该用户安装应用程序。  

    -   **登录要求** - 从以下选项中指定此部署类型的登录要求：  

        -   **仅当用户登录时**  

        -   **无论用户是否登录**  

        -   **仅当无用户登录时**  

        > [!NOTE]  
        >  此选项默认为“仅当用户登录时” ，如果在“安装行为”  下拉列表中选择了“针对用户安装”  ，则无法更改它。  

    -   **安装程序可见性** - 指定部署类型在客户端设备上运行将处于的模式。 可用选项如下：  

        -   **最大化** - 部署类型在客户端设备上以最大化模式运行。 用户将看到所有安装活动。  

        -   **正常** - 部署类型基于系统和程序默认值在正常模式下运行。 此为默认模式。  

        -   **最小化** - 部署类型在客户端设备上以最小化模式运行。 用户可能会在通知区域或任务栏中看到安装活动。  

        -   **隐藏** - 部署类型在客户端设备上以隐藏模式运行，用户将看不到安装活动。  

    -   **允许用户查看程序安装并与其交互** - 指定用户是否可以与部署类型安装交互以配置安装选项。  

        > [!NOTE]  
        >  如果在“安装行为”  下拉列表中选择了“针对用户安装”  选项，则默认情况下启用此选项。  

    -   **最大允许运行时间(分钟)** - 指定程序在客户端上预计运行的最长时间。 你可以将此设置指定为一个大于零的整数。 默认设置为 120 分钟。  

         此值用于：  

        -   监视部署类型中的结果。  

        -   确定在客户端设备上定义维护时段时是否将安装部署类型。 当处于维护时段时，只有在维护时段中有足够的可用时间来适应“最大允许运行时间”  设置时，程序才会运行。  

        > [!IMPORTANT]  
        >  如果“最大允许运行时间”  比计划维护时段长，则可能会发生冲突。 如果用户设置的最大运行时间超过了任何可用维护时段，该部署类型将不会运行。  

2.  **估计安装时间(分钟)** - 指定安装部署类型将需要的估计时间。 将向软件中心的用户显示此项。  

## <a name="specify-requirements-for-the-deployment-type"></a>指定部署类型的要求  

1.  在“创建部署类型向导”的“要求”  页上，单击“添加”  以打开“创建要求”  对话框，并添加新要求。  

    > [!NOTE]  
    >  还可以在 <部署类型名称\>“属性”对话框的“要求”选项卡上添加新要求。  
  
2.  在“类别”下拉列表中，选择此要求是用于设备还是用于用户，或者选择“自定义”以使用以前创建的全局条件。 选择“自定义”时，也可以单击“创建”以创建新全局条件。 有关全局条件的详细信息，请参阅[如何创建全局条件](../../apps/deploy-use/create-global-conditions.md)。  
  

    > [!IMPORTANT]  
    >  如果创建“用户”  类别和“主要设备” 条件的要求，然后将应用程序部署到设备集合，则会忽略要求。  
    >   
    >  如果你已创建 Windows 程序包和程序或任务序列（其将 Windows 10 作为使用 System Center 2012 R2 Configuration Manager SP1 的要求），然后升级至 System Center Configuration Manager，则针对于 Windows 10 的要求可能会被删除。 若要解决此问题，请再次指定要求。 请注意：虽然已从要求显示中删除要求，但设备上仍对其正确处理。  

3.  在“条件”  下拉列表中，选择想要用于评估用户或设备是否满足安装要求的条件。 根据所选类别，此列表的内容会有所不同。  

4.  在“运算符”  下拉列表中，选择运算符，此运算符用于将所选条件与指定值进行比较以评估用户或设备是否满足安装要求。 可用运算符将因所选条件而异。  

    > [!IMPORTANT]  
    >  根据部署类型所适用的设备类型的不同，可用要求将不同。  

5.  在“值”  字段中，指定值，这些值将与所选条件和运算符一起用于评估用户或设备是否满足安装要求。 可用值将因所选条件和所选运算符而异。  

6.  单击“确定”  以保存要求并关闭“创建要求”  对话框。  

## <a name="specify-dependencies-for-the-deployment-type"></a>指定部署类型的依赖关系  
 依赖关系定义在安装部署类型之前必须先安装的另一应用程序中的部署类型。 你可以将相关部署类型配置为在安装部署类型之前自动安装。  

> [!IMPORTANT]  
>  在某些情况下，部署类型依赖于同时包含依赖关系的部署类型。 在存在依赖关系链的这种情况下，链中支持的依赖关系的最大数量为 **5**。  

1.  在“创建部署类型向导”的“依赖关系”  页上，如果要指定在安装此部署类型之前必须安装的部署类型，请单击“添加”  。  

    > [!IMPORTANT]  
    >  还可在 <deployment type name\>“属性”对话框的“依赖项”选项卡上，添加新的依赖项。  

2.  在“添加依赖关系”  对话框中，单击“添加” 。  

3.  在“指定所需的应用程序”  对话框中，选择要用作依赖关系的现有应用程序和应用程序部署类型之一。  

    > [!TIP]  
    >  你可以单击“查看”  以显示所选应用程序或部署类型的属性。  

4.  单击“确定”  关闭“指定所需的应用程序”  对话框。  

5.  如果想要自动安装相关的应用程序，请选择相关应用程序旁边的“自动安装”  。  

    > [!NOTE]  
    >  若要自动安装，则不需要部署相关应用程序。  

6.  在“添加依赖关系”  对话框内的“依赖关系组名称”  字段中，输入名称以引用此应用程序依赖关系组。  

7.  根据需要使用“提高优先级”  和“降低优先级”  按钮，以更改每个依赖关系的计算顺序。  

8.  单击“确定”  以关闭“添加依赖关系”  对话框。  

## <a name="confirm-the-deployment-type-settings-and-complete-the-wizard"></a>确认部署类型设置，然后完成向导  

1.  在“创建部署类型向导”的“摘要”  页上，查看向导将采取的操作。 单击“下一步”  以创建部署类型，或者单击“上一步”  以返回并更改部署类型设置。  

2.  在“进度”页面完成之后，查看向导已采取的操作，然后单击“关闭”以完成向导。  

3.  如果从“创建应用程序向导”中启动了“创建部署类型向导”，则将返回到“创建应用程序向导”的“部署类型”  页。  

## <a name="configure-additional-options-for-deployment-types-that-contain-virtual-applications"></a>配置包含虚拟应用程序的部署类型的其他选项  
 使用以下过程配置包含虚拟应用程序的部署类型的其他选项。  

### <a name="configure-content-options-for-application-virtualization-app-v-deployment-types"></a>配置 Application Virtualization (App-V) 部署类型的内容选项  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序”。  

3.  在“应用程序”  列表中，选择包含 App-V 部署类型的应用程序。 然后，在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

4.  在 <Application Name\>“属性”对话框中的“部署类型”选项卡上，选择 APP-V 部署类型，然后单击“编辑”。  

5.  在 <Deployment Type Name\>“属性”对话框中的“内容”选项卡上，配置以下选项（如有需要）：  

    -   **保留客户端缓存中的内容** - 选择此选项以确保不从 Configuration Manager 客户端缓存中删除此部署类型的内容。  

    -   **启动前将内容加载到 App-V 缓存中** - 选择此选项以确保在启动应用程序之前将虚拟应用程序的所有内容都加载到 App-V 缓存中。 选择此选项还可以确保不在缓存中固定应用程序内容，并且可以根据需要删除该应用程序内容。  

6.  单击“确定”，关闭 <Deployment Type Name\>“属性”对话框。  

7.  单击“确定”，关闭 <Application Name\>“属性”对话框。  

### <a name="configure-publishing-options-for-app-v-deployment-types"></a>配置 APP-V 部署类型的发布选项  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序”。  

3.  在“应用程序”  列表中，选择包含 App-V 部署类型的应用程序。 然后，在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

4.  在 <Application Name\>“属性”对话框中的“部署类型”选项卡上，选择 APP-V 部署类型，然后单击“编辑”。  

5.  在 <Deployment Type Name\>“属性”对话框中的“发布”选项卡上，在虚拟应用程序中选择想要发布的项目。  

6.  单击“确定”，关闭 <Deployment Type Name\>“属性”对话框。  

7.  单击“确定”，关闭 <Application Name\>“属性”对话框。  

## <a name="import-an-application"></a>导入应用程序  
 使用下列过程将应用程序导入 Configuration Manager。 有关如何导出应用程序的信息，请参阅 [System Center Configuration Manager 应用程序的管理任务](../../apps/deploy-use/management-tasks-applications.md)。  

1.  在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用程序”。  

3.  在“主页”选项卡上的“创建”组中，单击“导入应用程序”。  

4.  在“导入应用程序向导”的“常规”页上，单击“浏览”，然后指定 zip 文件的 UNC 路径，该路径包含要导入的应用程序。  

5.  在“文件内容”页上，选择在尝试导入的应用程序与现有应用程序重复的情况下将进行的操作。 你可以指定创建新应用程序，或忽略重复项并将新的修订添加到现有应用程序。  

6.  在“摘要”页上，查看要执行的操作，然后完成向导。  

 新应用程序会出现在“应用程序”节点中。  

> [!TIP]  
>  Windows PowerShell cmdlet **Import-CMApplication** 执行与此过程相同的功能。 有关详细信息，请参阅 Microsoft System Center 2012 Configuration Manager SP1 Cmdlet 参考文件中的 [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx)。  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Configuration Manager 支持的部署类型  

|部署类型名称|更多信息|  
|--------------------------|----------------------|  
|**Windows Installer（\*.msi 文件）**|通过 Windows Installer 文件创建部署类型。|  
|**Windows 应用包（\*.appx、\*.appxbundle）**|通过 Windows 应用包文件或 Windows 应用捆绑包为 Windows 8、Windows RT 或更高版本创建部署类型。|  
|**Windows 应用包（在 Windows 应用商店中）**|通过指定指向 Windows 应用商店中应用的链接，或通过浏览应用商店选择你需要的应用，为 Windows 8、Windows RT 或更高版本创建部署类型。<br /><br /> 如果要以指向 Windows 应用商店的链接的形式部署应用，请确保组策略设置“关闭应用商店应用程序”  设置为“已禁用”  或“未配置” 。 如果启用此设置，客户端将无法连接到 Windows 应用商店来下载和安装应用程序。<br /><br /> 使用存储链接的 Windows 8 部署类型始终在其他部署类型之前进行评估（不考虑其优先级）。|  
|**脚本安装程序**|创建一个部署类型，该部署类型指定在客户端设备上运行以安装内容或执行操作的脚本。|  
|**Microsoft Application Virtualization 4**|通过 Microsoft Application Virtualization 4 清单创建部署类型|  
|**Microsoft Application Virtualization 5**|通过 Microsoft Application Virtualization 5 包文件创建部署类型。|  
|**Windows Phone 应用包（\*.xap 文件）**|通过 Windows Phone 应用包文件创建部署类型。|  
|**Windows Phone 应用包（在 Windows Phone 应用商店中）**|通过指定指向 Windows Phone 应用商店中的应用的链接来创建部署类型。|  
|**Windows Mobile Cabinet**|通过 Windows Mobile Cabinet (CAB) 文件为 Windows Mobile 设备创建部署类型。|  
|**iOS 应用包（\*.ipa 文件）**|通过 iOS 应用包文件创建部署类型。|  
|**App Store 中的 iOS 应用包**|通过指定指向应用商店中的 iOS 应用的链接来创建部署类型。|  
|**Android 应用包（\*.apk 文件）**|通过 Android 应用包文件创建部署类型。|  
|**Google Play 上的 Android 应用包**|通过指定指向 Google Play 上的应用的链接来创建部署类型。|  
|**Mac OS X**|通过你使用 CMAppUtil 工具创建的 .cmmac 文件为 Mac 计算机创建部署类型。<br /><br /> 仅适用于运行 Configuration Manager 客户端的 Mac 计算机。|  
|**Web 应用程序**|创建一个部署类型，该部署类型指定指向 Web 应用程序的链接。 该部署类型在用户的设备上安装 Web 应用程序的快捷方式。<br /><br /> 如果已在你管理的 iOS 或 Android 设备上安装了 Intune 托管浏览器，则可以确保用户只能使用托管浏览器打开应用。 为此，请在指定应用链接时使用以下格式之一，方法是将 **http:** 替换为 **http-intunemam:** 或将 **https:** 替换为 **https-intunemam:**<br /><br /> - **http-intunemam://<path to web app\>**<br /><br /> - **https-intunemam://<path to web app\>**<br /><br /> 可以使用 Configuration Manager 应用程序要求确保将要与托管浏览器关联的应用仅安装到 iOS 和 Android 设备。<br />aspx)。<br /><br /> 有关 Intune 管理的浏览器的详细信息，请参阅[使用托管浏览器策略管理 Internet 访问](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md)。|  
|**通过 MDM 的 Windows Installer (\*.msi)**|此安装程序类型允许你创建基于 Windows Installer 的应用，并将其部署到运行 Windows 10 的 PC。<br /><br /> 使用此安装程序类型时，需要考虑下列注意事项：<br><br>- 只能上载扩展名为 .msi 的单个文件。<br /><br /> - 该文件的产品代码和产品版本将用于应用检测。<br /><br /> - 将使用该应用的默认重启行为。 Configuration Manager 不对此进行控制。<br /><br /> - 将为单个用户安装每个用户 MSI 包。<br /><br /> - 将为设备上的所有用户安装每个计算机 MSI 包。<br /><br /> - 当前仅为设备上的所有用户安装双模式 MSI 包。<br /><br /> - 当每个版本的 MSI 产品代码相同时，支持应用更新。|  



<!--HONumber=Nov16_HO1-->


