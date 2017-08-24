---
title: "适用性规则 |Microsoft 文档"
description: "管理 System Center Updates Publisher 中的适用性规则"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 2925abda07abaa46ad56b9b433ce003c22aede5e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>管理 Updates Publisher 中的适用性规则

*适用范围：System Center Updates Publisher*

借助 Updates Publisher，适用性规则可定义设备在安装更新之前必须满足的要求。 这些规则还可用于确定计算机是否已安装更新。 包含多个部分的复杂适用性规则被称为“规则集”。

更新捆绑包不使用适用性规则。

## <a name="overview-of-applicability-rules"></a>适用性规则概述
可以在“规则工作区”中管理适用性规则。 创建规则时，可指定一个或多个条件。 如果指定多个条件，可以配置条件关系，以便能够依序求值或合并到 **And** 或 **Or** 逻辑语句中。

例如，下面是包含三条规则的规则集。 第一条规则验证 *MyFile* 文件是否存在，第二条和第三条规则验证 Windows 操作系统的语言是英语还是日语。

    And  
      File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
      Or  
        Windows Language is English   
        Windows Language is Japanese

所有更新都要求至少满足一条适用性规则。 适用性规则应用于已导入的更新。创建你自己的更新时，必须向其添加一条或多条规则。 可以修改和扩展 Updates Publisher 中任意更新的规则。

若要查看已创建的规则，请转到“规则工作区”，从“我保存的规则”列表中选择规则。 规则的各个条件和逻辑运算显示在控制台的“适用性规则”窗格中。 对于导入的更新，只有在编辑更新时才能查看并修改其规则。

可以在 Updates Publisher 中的两个位置创建规则：

-   在“规则工作区”中，可以创建并**保存**规则集，以供稍后使用。 编辑或创建更新时，可以选择“已保存的规则”作为“规则类型”，然后从预建规则集列表中进行选择。

-   也可以在创建或编辑更新时新建规则。 无法保存通过这种方式创建的规则以供将来使用。

## <a name="create-applicability-rule"></a>创建适用性规则
下面介绍的步骤与在[“创建更新向导”](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard)中创建规则的方式类似。 与此向导的不同之处在于，可以视需要保存规则集以供将来使用。

1.  在“规则工作区”中，选择“创建”，打开“创建规则”向导。

2.  指定规则名称，然后单击“新建规则”![](media/newrule.png)。 此时，“适用性规则”页会打开，可以在其中配置规则。

3.  对于“规则类型”，请选择下列选项之一。 必须配置的选项因规则类型而异：

    -   文件 - 使用此规则可要求设备必须包含属性符合你指定的一个或多个条件的文件，然后才能应用此更新。

    -   注册表 - 使用此类型可指定必须有注册表详细信息，然后设备才符合此更新的安装条件。

    -   系统 - 此规则使用系统详细信息来确定适用性。 可以选择定义 Windows 版本、Windows 语言还是处理器体系结构，也可以指定 WMI 查询来标识设备操作系统。

    -   Windows Installer - 使用此规则类型可根据已安装的 .MSI 或 Windows Installer 修补程序 (.MSP) 确定适用性。 还可以确定是否已根据要求安装特定组件或功能。

       > [!IMPORTANT]   
       > 对于受管理设备，Windows 更新代理无法检测针对每个用户安装的 Windows Installer 包。 使用此规则类型时，请配置其他适用性规则（如文件版本或注册项值），以便能够正确地检测 Windows Installer 包，无论是针对每个用户安装，还是针对每个系统安装。

    -   已保存的规则 - 使用此选项，可以查找和使用以前配置和保存的规则。

4.  根据需要，继续添加并配置其他规则。

5.  使用逻辑运算按钮对不同的规则进行排序和分组，以创建更复杂的先决条件检查。

6.  创建完规则集后，单击“确定”进行保存。 此时，该规则集会出现在“我保存的规则”列表中。

## <a name="edit-applicability-rule-sets"></a>编辑适用性规则集
若要编辑适用性规则，请转到“规则工作区”，选择在“我保存的规则”列表中保存的任意规则，然后从功能区中选择“编辑”。 此时，“编辑规则”向导会打开。

“编辑规则”向导显示规则集的现有规则。 规则编辑方式与使用“创建规则”向导新建规则的方式相同。 可以使用此向导重命名规则集、删除规则、重新排序规则和关系或添加新规则。

执行完更改后，请选择“确定”，保存所做的更改并关闭向导。

若要详细了解如何使用规则向导，请参阅[创建更新向导](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard)**第 7 步**中的适用性规则页。

## <a name="delete-applicability-rules"></a>删除适用性规则
若要删除已保存的适用性规则，请转到“规则工作区”，从“我保存的规则”列表中选择规则或规则集，然后从功能区中选择“删除”。 这会从 Updates Publisher 中删除已保存的规则或规则集。

必须[编辑更新](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles)，才能删除特定更新中的规则。
