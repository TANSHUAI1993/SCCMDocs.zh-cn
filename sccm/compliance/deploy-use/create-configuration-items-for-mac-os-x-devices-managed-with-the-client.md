---
title: "为客户端托管的 Mac 创建配置项 - Configuration Manager | Microsoft Docs"
description: "使用 System Center Configuration Manager Mac OS X 配置项目管理对 Mac OS X 设备的设置。"
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 541e5ad629a9e2ed9c353dff150f9b86b9d12b7d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>如何为使用 System Center Configuration Manager 客户端管理的 Mac OS X设备创建配置项目
使用 System Center Configuration Manager **Mac OS X（自定义）**配置项目，管理由 Configuration Manager 客户端托管的 Mac OS X 设备的设置。  
  
 Mac OS X 操作系统使用属性列表（或列表）文件来存储应用程序设置。 使用符合性设置来评估和修正属性列表文件中的设置。 还可以通过编写一个 Shell 脚本来管理 Mac OS X 设置，该脚本会返回一个值，可以评估和修正符合性。  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>创建自定义 Mac OS X 配置项目  
  
1.  在 Configuration Manager 控制台中，单击“资产和符合性”。  
  
2.  在“资产和符合性”  工作区中，展开“符合性设置” ，然后单击“配置项目” 。  
  
3.  在“主页”  选项卡上的“创建”  组中，单击“创建配置项目” 。  
  
4.  在“创建配置项目向导”  的“常规” 页面上，指定配置项目的名称和可选描述。  
  
5.  在“指定要创建的配置项目的类型” 下，选择“Mac OS X（自定义）” 。  
  
6.  如果创建并分配类别以帮助在 Configuration Manager 控制台中搜索和筛选配置项目，请单击“类别”。  
  
7.  在向导的“支持的平台”  页中，选择将评估配置项目的特定 Mac OS X 版本。  
  
8.  在向导的“设置”  页面中，将添加要评估在 Mac 计算机上的符合性的新设置。 单击“新建”  以打开“创建设置”  对话框。  
  
9. 在“创建设置”  对话框框中，输入设置的唯一名称和描述。  
  
10. 选择需要的“设置类型”  ，然后提供下表所示的所需信息：  
  
    -   **Mac OS X 首选项** -  
  
        -   **应用程序 ID** – 指定想要用于评估符合性键的属性列表文件的应用程序 ID。  
  
             例如，如果您想要编辑的 Safari Web 浏览器设置，则可能会使用 **com.apple.Safari.plist**。  
  
        -   **密钥** – 指定要在 Mac 计算机上的符合性评估的键的名称。 使用以下语法：*/<dictionary\>/<keyname\>*。  
  
            > [!IMPORTANT]  
            >  键名区分大小写，如果这些名称与 Mac 计算机上的键名不同，将不会对它们进行评估。 而且，无法在指定键名后对其进行编辑。 如果您需要编辑的项名称，删除并重新创建该设置。  
  
    -   **脚本** -  
  
        -   **发现脚本** – 单击“添加脚本” ，然后输入一个 shell 脚本，以评估 Mac 计算机上设置的符合性。 使用 shell 脚本中的 **echo** 命令，向 Configuration Manager 返回值以实现符合性。 Configuration Manager 使用 **STDOUT** 中返回的结果评估符合性。  
  
            > [!IMPORTANT]  
            >  发现脚本中不包括“重新启动”  命令。 因为发现脚本在每次客户端重新启动时运行，这将导致 Mac 计算机不断重新启动。  
  
        -   **修正脚本（可选）** – 也可单击“添加脚本”  ，然后输入一个 shell 脚本，用于修正 Mac 客户端计算机上发现的任何不符合要求的设置。  
  
            > [!IMPORTANT]  
            >  为了确保不引入 Mac 计算机无法解释的格式字符，请勿使用复制与粘贴，而键入脚本。  
  
11. 选择“数据类型”  ，它是用于评估设置之前条件返回数据的格式。  
  
    > [!NOTE]  
    >  “浮点”  数据类型仅支持小数点后 3 个数字。  
    >   
    >  Configuration Manager 不支持对 Mac 配置项目脚本设置使用**布尔**数据类型。 而应将数据类型设置为“整数”  ，并确保脚本返回一个整数值。  
  
12. 单击“确定”  以保存设置并关闭“创建设置”  对话框，然后继续根据需要添加多项设置。  
  
13. 在向导的“符合性规则”  页面中，可指定定义配置项目的符合性的条件。 必须至少具有一个符合性规则，才可以评估设置的符合性。 单击“新建”  以添加新规则。  
  
14. 在“创建规则”  对话框中，提供以下信息：  
  
    -   **名称：** 输入符合性规则的名称。  
  
    -   **描述:** 输入符合性规则的说明。  
  
    -   **选定的设置：** 单击 **浏览** 若要打开 **选择设置** 对话框。 选择您想要定义的规则，或单击设置 **新设置**。 在完成，请单击 **选择**。  
  
        > [!TIP]  
        >  您也可以单击 **属性** 若要查看有关当前所选设置的信息。  
  
    -   **规则类型：** 选择要使用的符合性规则的类型：  
  
        -   **值：** 创建将配置项目返回的值与指定值进行比较的一条规则。  
  
        -   **现有** – 创建根据设置是否存在来评估它的一条规则。  
  
    -   对于规则类型“值” ，指定以下信息：  
  
        -   设置必须符合以下规则 – 选择运算符以及对其评估与所选设置的符合性的值。 可以使用以下运算符：  
  
            -   **等于**  
  
            -   **不等于**  
  
            -   **大于**  
  
            -   **小于**  
  
            -   **之间**  
  
            -   **大于或等于**  
  
            -   **小于或等于**  
  
            -   **之一** – 在文本框中，每行指定一个条目。  
  
            -   **无** – 在文本框中，每行指定一个条目。  
  
        -   “在支持时修正不符合性规则” – 如果希望 Configuration Manager 自动修正不符合性规则，则选择此选项。  
  
            > [!IMPORTANT]  
            >  仅当规则运算符设置为“等于” 时，才能修正非符合性规则。  
  
        -   **找不到此设置实例的情况下的报表不符合性** – 如果在 Mac 计算机上找不到此设置，则配置项目报告不符合性。  
  
    -   **报表的不符合性严重性** – 指定不符合此符合性规则时报告的严重性级别。 可用的严重性级别如下：  
  
        -   **无** - 对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  
  
        -   **信息** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**信息**。  
  
        -   **警告** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**警告**。  
  
        -   **严重** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。  
  
        -   **事件严重** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。 此严重性级别也由 Mac 客户端计算机记录。  
  
    -   对于规则类型“现有” ，指定以下信息：  
  
        -   选择以下选项之一：  
  
            -   **此设置必须存在于客户端设备**  
  
            -   **设置不得存在于客户端设备**  
  
        -   **报表的不符合性严重性：** 指定如果此符合性规则失败报告的严重性级别。 可用的严重性级别如下：  
  
            -   **无** - 对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  
  
            -   **信息** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**信息**。  
  
            -   **警告** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**警告**。  
  
            -   **严重** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。  
  
            -   **事件严重** - 对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。 此严重性级别也由 Mac 客户端计算机记录。  
  
        > [!NOTE]  
        >  根据为其配置规则的设置类型，显示的选项可能有所不同。  
  
    -   单击“确定”  关闭“创建规则”  对话框。  
  
15. 在“摘要”  页上，确认新配置项目的设置，然后完成此向导。  
  
 新配置项目会显示在“资产和符合性”  工作区的“配置项目”  节点中。  
  
 如果现在想要将此配置项目添加到配置基线，请参阅[如何在 System Center Configuration Manager 中创建配置基线](../../compliance/deploy-use/create-configuration-baselines.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
