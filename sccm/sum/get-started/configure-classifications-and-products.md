---
title: 配置分类和产品
titleSuffix: Configuration Manager
description: 按照以下步骤在 Configuration Manager 控制台中配置要同步的软件更新分类和产品。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/25/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2edf117f27eda3ee3c9e587edb9f69c8d84bf5dc
ms.sourcegitcommit: 670cfed1e47a7a4a73aa4ccb873c6312be3c21ff
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71311586"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

*适用范围：System Center Configuration Manager (Current Branch)*

在 Configuration Manager 中，将根据你在软件更新点组件属性中指定的设置在同步过程期间检索软件更新元数据。 首次同步软件更新后，或者当发布新产品和分类时，必须转到这些属性以选择新项。 使用下列过程来配置要同步的分类和产品。  

> [!NOTE]  
> 请仅在顶层站点上使用本部分中的过程。  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>配置要同步的分类和产品  

1. 在 **Configuration Manager** 控制台中，导航到“管理”   > “站点配置”   > “站点”  。

2. 选择管理中心站点或独立主站点。  

3. 在“主页”  选项卡上的“设置”  组中，单击“配置站点组件”  ，再单击“软件更新点”  。

4. 在“分类”  选项卡上，指定要为其同步软件更新的软件更新分类。  

    每个软件更新都是利用更新分类定义的，此分类能帮助组织不同的更新类型。 同步过程中，将对指定的分类的软件更新元数据进行同步。 Configuration Manager 使你可将软件更新与下列更新分类进行同步：  

     - **关键更新**：指定为特定问题广泛发布的修复，旨在解决与安全无关的关键 bug。  
     - **定义更新**：指定广泛发布且频率较高的软件更新，其中包含对产品的定义数据库的新增内容。  
     - **功能包**：指定新的产品功能，该功能首次在产品版本以外分发，而且通常包含在下一个完整的产品版本中。  
     - **安全更新**：指定一个广泛发布的修复程序，旨在修复特定于产品的安全相关漏洞。  
     - **服务包**：指定一个经过测试、逐渐累积的集合，其中包含所有的修补程序、安全更新、关键更新和适用于某个产品的更新。 此外，服务包可能还包含旨在解决产品发布以来内部发现的问题的其他修补程序。  
     - **工具**：指定可帮助完成一项或多项任务的实用程序或功能。  
     - **更新汇总**：指定为便于部署而一起打包的修补程序、安全更新、关键更新和其他更新的经过测试的累积集合。 更新汇总通常解决特定领域的问题，例如安全性或产品组件问题。  
     - **更新**：指定广泛发布的针对特定问题的修补程序。 更新解决了非关键且与安全无关的 bug。  
     - **升级**：为 Windows 10 特性和功能指定升级。 软件更新点和站点必须运行最低具有[修补程序 3095113](https://support.microsoft.com/kb/3095113) 的 WSUS 6.2 来获取“升级”  分类。 有关安装此更新和其他**升级**更新的详细信息，请参阅[软件更新的先决条件](/sccm/sum/plan-design/prerequisites-for-software-updates#BKMK_wsus2012)。

    > [!NOTE] 
    > 
    > 从 Configuration Manager 版本 1706 开始，可以选中“包括 Microsoft Surface 驱动程序和固件更新”  复选框来同步 Microsoft Surface 驱动程序。<!--1098490--> 所有软件更新点都必须运行 Windows Server 2016 才能成功同步 Surface 驱动程序。 如果启用 Surface 驱动程序后，在运行 Windows Server 2012 的计算机上启用软件更新点，则驱动程序更新的扫描结果不准确。 这会导致在 Configuration Manager 控制台和 Configuration Manager 报表中显示不正确的符合性数据。  
    >  
    > - 此功能在 1706 版中首次引入，属于[预发行功能](/sccm/core/servers/manage/pre-release-features)。 从版本 1710 开始，此功能不再属于预发行功能。  
    >  
    > - 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](/sccm/core/servers/manage/install-in-console-updates#bkmk_options)。<!--505213-->  

5. 在“产品”  选项卡上，指定要为其同步软件更新的产品，然后单击“关闭”  。  

    - Configuration Manager 存储产品和产品系列的列表，你在初次安装软件更新点时可以从此列表中进行选择。 如果某些产品和产品系列是在发布 Configuration Manager 之后发布的，那么，在完成软件更新同步（这将更新可供你从中进行选择的可用产品和产品系列的列表）之前，可能无法选择它们。  

    - 每个软件更新的元数据都定义了更新适用于的产品。 产品是指特定版本的操作系统或应用程序，例如 Microsoft Windows Server 2012。 产品家族是指从中派生单个产品的基本操作系统或应用程序。 产品系列的示例是 Windows，而 Windows Server 2012 是其成员之一。 可以指定产品系列或产品系列中的各个产品。 选择的产品越多，同步软件更新所需的时间就越长。  

    - 当软件更新适用于多个产品，且至少选中其中一个产品进行同步时，所有产品都将在 Configuration Manager 控制台中显示，即使未选中某些产品也是如此。 例如，Windows Server 2012 是你选择的唯一操作系统，而且软件更新适用于 Windows 8 和 Windows Server 2012，那么，这两个产品都会显示在 Configuration Manager 控制台中。  

    > [!NOTE]  
    > Windows 10 1903 版以及更高版本都已经作为其自身产品添加到 Microsoft 更新中，而不像早期版本那样作为 Windows 10 产品的一部分进行添加   。 这项更改需要你执行许多手动步骤，才可确保客户端显示这些更新。 我们已帮助减少 Configuration Manager 版本1906中的新产品需要执行的手动步骤数。 <!--4682946-->
    >
    > 更新至 Configuration Manager 1906 版，并选择了 Windows 10 产品进行同步后，系统将自动执行以下操作  ：
    > - 已添加 Windows 10 1903 版以及更高版本产品用于进行同步操作  。
    > - 包含 Windows 10 产品的[自动部署规则](/sccm/sum/deploy-use/automatically-deploy-software-updates#bkmk_adr-process)将更新为包含 Windows 10 1903 版和更高版本   。
    > - [维护服务计划](/sccm/osd/deploy-use/manage-windows-as-a-service#servicing-plan-workflow)将更新为包含 Windows 10 1903 版和更高版本产品  。

## <a name="bkmk_WIfB"></a>Windows 预览体验计划
<!--3556023-->
从2019年9月开始，你可以通过 Configuration Manager 来服务和更新运行 Windows 有问必答 Preview 版本的设备。 此更改意味着，你可以管理这些设备，而无需更改正常过程或启用 Windows 更新 for Business。 你可以将 Windows 预览体验预览版的功能更新和累积更新下载到 Configuration Manager，就像任何其他 Windows 10 更新或升级一样。 有关详细信息，请参阅[发布预发布 Windows 10 功能更新到 WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054)博客文章。

有关 Configuration Manager 中的 Windows 内幕支持的详细信息，请参阅[对 windows 10 的支持](/sccm/core/plan-design/configs/support-for-windows-10bkmk_WIfB-support)。

### <a name="prerequisites"></a>先决条件

- Configuration Manager 版本1906或更高版本，配置为[软件更新管理](/sccm/sum/plan-design/plan-for-software-updates)。
- 运行[Windows 内幕预览版](https://insider.windows.com/en-us/how-to-pc/)的 windows 10 设备。<!--the direct page link doesn't work without a locale :(-->
- 包含 Windows 有问必答设备的集合。


### <a name="enable-windows-insider-upgrades-and-updates"></a>启用 Windows 有问必答升级和更新

你需要为 Windows 有问必答升级和更新启用产品和分类。 Windows 预览体验的功能更新位于**Windows 有问必答版预发行版**产品下。 但是，Windows 有问必答的累积更新和其他更新将在**windows 10 版本1903及更高版本**下。

1. 在 **Configuration Manager** 控制台中，导航到“管理”   > “站点配置”   > “站点”  。
2. 选择管理中心站点或独立主站点。  
3. 在“主页”  选项卡上的“设置”  组中，单击“配置站点组件”  ，再单击“软件更新点”  。
4. 在 "**产品**" 选项卡上，确保选择了以下产品进行同步：
    - Windows 预览体验预发行版
    - Windows 10 版本 1903 及更高版本
5. 在 "**分类**" 选项卡上，确保选择了以下分类进行同步：
    - 升级
    - 安全更新
    - 更新（可选）
6. 单击“确定”  关闭“软件更新点组件属性”  。

### <a name="upgrading-windows-insider-devices"></a>升级 Windows 有问必答设备

对 windows 预览体验的升级完成同步后，可以从**软件库** > **Windows 10** > 中看到它们，以处理**所有 Windows 10 更新**。

![Windows 10 维护服务的 windows 预览体验版功能更新](media/3556023-windows-insiders-pre-release-feature-update.png)

将 Windows 有问必答的功能更新部署到目标集合中，就像任何其他升级一样。 但是，在部署以下功能更新时，需要记住以下各项：

- 这些升级适用于所有 Windows 10 客户端1903或更早版本，并具有匹配的体系结构、版本和语言。
- 存在许可条款，你的部署必须接受条款才能进行安装。
- 请考虑[在客户端设置中使用线程优先级](/sccm/core/clients/deploy/about-client-settings#bkmk_thread-priority)。
- 动态更新会直接从 Microsoft 更新中自动安装关键更新，包括最新的累积更新。 此行为是通过适用于 Windows 10 版本1903的功能更新开始的。 
  - 可以[在客户端设置中](/sccm/core/clients/deploy/about-client-settings#bkmk_du)或使用[setupconfig 文件](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)显式禁用动态更新。 
  - 有关详细信息，请参阅[Windows 10 动态更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)博客文章。

有关如何部署升级的详细信息，请参阅将[Windows 作为服务进行管理](/sccm/osd/deploy-use/manage-windows-as-a-service)。


### <a name="keeping-insider-devices-up-to-date"></a>使内幕设备保持最新

适用于 Configuration Manager 的 WSUS 和扩展将提供适用于 Windows 有问必答的累积更新。 这些累积更新的发布频率类似于 Windows 10 版本1903累积更新。 Windows 内幕累积更新位于**windows 10 版本1903及更高版本**的产品类别中，并归类为**安全更新**或**更新**。 你可以使用常规软件更新过程（如使用[自动部署规则](/sccm/sum/deploy-use/automatically-deploy-software-updates)或[分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)）为 Windows 有问必答部署累积更新。


## <a name="next-steps"></a>后续步骤

启动软件更新同步以根据新条件检索软件更新。 有关详细信息，请参阅[同步软件更新](synchronize-software-updates.md)。
