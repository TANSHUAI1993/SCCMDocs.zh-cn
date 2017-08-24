---
title: "管理操作系统映像 | Microsoft Docs"
description: "在 Configuration Manager 中，了解如何管理存储在 Windows 映像 (WIM) 文件中的操作系统映像。"
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
caps.latest.revision: "17"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6953c3834ca303b949f22436010a87b3da9688dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 管理操作系统映像

*适用范围：System Center Configuration Manager (Current Branch)*

Configuration Manager 中的操作系统映像以 Windows 映像 (WIM) 文件格式存储，代表在计算机上成功安装和配置操作系统所需的引用文件和文件夹的压缩集合。 对于所有操作系统部署方案，必须选择操作系统映像。   你可以使用默认操作系统映像或从你配置的引用计算机生成操作系统映像。 在生成引用计算机时，在捕获操作系统以创建映像文件之前，你可以向其添加操作系统文件、驱动程序、支持文件、软件更新、工具和其他软件应用程序。 下面提供了有关每种方法的信息。  

 **默认映像**  

 默认操作系统映像 (install.wim) 包含在 Windows 操作系统安装文件中。 此映像是包含一组标准驱动程序的基本操作系统映像。 当你使用默认操作系统映像时，可以在操作系统安装之后使用任务序列步骤来安装应用和进行其他配置。  默认操作系统映像位于 <*操作系统源路径*>\Sources\install.wim。  

-   **优点**  

    -   映像大小小于捕获的映像。  

    -   使用任务序列步骤安装应用和配置可更加动态。 例如，你可以在任务序列中更改将安装的应用和配置，并且无需对操作系统进行重映像。  

-   **缺点**  

    -   操作系统安装可能需要更多时间，因为操作系统安装完成后将进行应用安装和其他配置。  

 **捕获的映像**  

 若要创建自定义操作系统映像，则构建具有所需的操作系统的引用计算机，并安装应用、配置设置等。然后，从引用计算机捕获操作系统映像以创建 WIM 文件。 你可以手动构建引用计算机，或者可以使用任务序列自动执行部分或所有构建步骤。   
有关创建自定义操作系统映像的步骤，请参阅[自定义操作系统映像](customize-operating-system-images.md)。  

-   **优点**  

    -   安装速度可以比使用默认映像更快。 例如，可以使用捕获的操作系统映像预安装应用，并且将无需在之后使用任务序列步骤来安装应用。  

-   **缺点**  

    -   操作系统安装可能需要更多时间，因为操作系统安装完成后将进行应用安装和其他配置。  


##  <a name="BKMK_AddOSImages"></a>将操作系统映像添加到 Configuration Manager  
 在可以使用操作系统映像之前，必须先将映像添加到 Configuration Manager 站点。 使用以下过程将操作系统映像添加到站点。  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>若要将操作系统映像添加到站点  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“操作系统映像包” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“添加操作系统映像包”  以启动添加操作系统映像包向导。  

4.  在“数据源”  页上，指定操作系统映像的网络路径。 例如，指定 **\\\server\path\OS.WIM**。  

5.  在“常规”  页上，指定以下信息，然后单击“下一步” 。 当你向同一站点中添加多个操作系统映像时，此信息在用于标识时非常有用。  

    -   **名称**：指定映像的名称。 默认情况下，映像的名称是从 WIM 文件中获取的。  

    -   **版本**：指定映像的版本。  

    -   **备注**：指定映像的简要描述。  

6.  完成向导。  

 现在可以将操作系统映像分发到分发点。  

##  <a name="BKMK_DistributeBootImages"></a>将操作系统映像分发到分发点  
 将采用与分发其他内容相同的方式将操作系统映像分发到分发点。 大多数情况下，部署操作系统之前必须将操作系统映像分发到至少一个分发点。 关于分发操作系统映像的步骤，请参阅 [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)。  

##  <a name="BKMK_OSImagesApplyUpdates"></a>将软件更新应用于操作系统映像  
 我们会定期发布适用于你的操作系统映像中的操作系统的新软件更新。 必须将软件更新基础结构实施到位，成功同步软件更新，并将软件更新下载到站点服务器上的内容库后才可将软件更新应用于映像。 有关详细信息，请参阅[部署软件更新](../../sum/deploy-use/deploy-software-updates.md)。  

 你可以按指定计划将适用的软件更新应用于映像。 Configuration Manager 按指定计划将选择的软件更新应用于操作系统映像，然后根据需要将更新的映像分发到分发点。 有关操作系统映像的信息存储在站点数据库中，包括在导入时应用的软件更新。 自映像最初添加以来已应用于映像的软件更新也存储在站点数据库中。 当你启动向导以将软件更新应用于操作系统映像时，向导将检索尚未应用于映像的适用软件更新的列表供你选择。 Configuration Manager 从站点服务器上的内容库中复制软件更新，然后将软件更新应用于操作系统映像。  

 使用以下过程将软件更新应用于操作系统映像。  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>将软件更新应用于操作系统映像  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“操作系统映像包” 。  

3.  选择要向其应用软件更新的操作系统映像。  

4.  在“主页”  选项卡上的“操作系统映像包”  组中，单击“计划更新”  以启动向导。  

5.  在“选择更新”  页上，选择要应用于操作系统映像的软件更新，然后单击“下一步” 。  

6.  在“设置计划”  页上，指定以下设置，然后单击“下一步” 。  

    1.  **计划**：指定有关何时将软件更新应用于操作系统映像的计划。  

    2.  **出错时继续**：选择此选项以便即使在出错时也继续将软件更新应用于映像。  

    3.  **将映像分发到分发点**：选择此选项以在应用了软件更新后更新分发点上的操作系统映像。  

7.  在“摘要”  页上，验证以下信息，然后单击“下一步” 。  

8.  在“完成”  页上，验证软件更新是否已成功应用于操作系统映像。  

##  <a name="BKMK_OSImageMulticast"></a>为多播部署准备操作系统映像  
 使用多播部署以允许多台计算机同时下载操作系统映像。 映像通过分发点多播给客户端，而不是让分发点通过单独连接向每个客户端发送映像的副本。 选择[使用多播通过网络部署 Windows](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) 操作系统部署方法时，必须先将操作系统映像包配置为支持多播，然后才能将操作系统映像分发到启用了多播的分发点。 使用下列过程来为现有操作系统映像包设置多播选项。  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>修改操作系统映像包以使用多播  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“操作系统映像包” 。  

3.  选择要分发到启用了多播的分发点的操作系统映像。  

4.  在“主页”  选项卡上的“属性”  组中，单击“属性” 。  

5.  选择“分发设置”  选项卡，并配置以下选项：  

    -   **允许通过多播传输此包(仅 WinPE)**：必须选择此选项以使 Configuration Manager 同时部署多个操作系统映像。  

    -   **加密多播包**：指定在将映像发送到分发点之前是否对其进行加密。 如果包中包含敏感信息，请使用此选项。 如果不对映像进行加密，则包的内容将以明文的形式出现在网络上并且可被未授予用户读取。  

    -   **仅通过多播传输此包**：指定是否希望分发点仅在多播会话期间部署映像。  

         如果选择“仅通过多播传输此包” ，则必须还要指定“需要时通过运行任务序列本地下载内容”  作为操作系统映像的部署选项。 你可以在部署操作系统映像时为映像指定部署选项，或者可以稍后通过编辑部署的属性来指定这些选项。 部署选项位于部署对象的“属性”  页的“分发点”  选项卡上。  

6.  单击" **确定**"。  
