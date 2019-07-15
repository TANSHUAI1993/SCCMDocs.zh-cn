---
title: '创建客户端托管的 Mac 的配置项目 '
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager Mac OS X 配置项目管理对 Mac OS X 设备的设置。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 346848bf3cd8b69b3bcecb479fb82250943dfd49
ms.sourcegitcommit: de3c86077bbf91b793e94e1f60814df18da11bab
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726156"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Mac OS X 设备创建配置项目
使用 System Center Configuration Manager Mac OS X（自定义）  配置项目，管理由 Configuration Manager 客户端托管的 Mac OS X 设备的设置。  
  
Mac OS X 操作系统使用属性列表 (.plist) 文件来存储应用程序设置。 使用符合性设置来评估和修正属性列表文件中的设置。 还可以通过编写 shell 脚本来管理 Mac OS X 设置，此脚本会返回可用于评估设置是否相容并修正设置的值。  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>创建自定义 Mac OS X 配置项目  
  
1. 在 Configuration Manager 控制台中，选择“资产和合规性”  。  
  
2. 在“资产和合规性”  工作区中，展开“合规性设置”  ，再选择“配置项目”  。  
  
3. 在“主页”  选项卡的“创建”  组中，选择“创建配置项目”  。  
  
4. 在“创建配置项目”  向导的“常规”  页上，指定配置项目的名称和可选说明。  
  
5. 在“指定要创建的配置项目的类型”  下，选择“Mac OS X（自定义）”  。  
  
6. 若要创建和分配有助于在 Configuration Manager 控制台中搜索和筛选配置项目的类别，请选择“类别”  。  
  
7. 在向导的“支持的平台”  页中，选择将评估配置项目的特定 Mac OS X 版本。  
  
8. 在向导的“设置”  页中，添加要在 Mac 计算机上评估是否相容的新设置。 选择“新建”  ，以打开“创建设置”  对话框。  
  
9. 在“创建设置”  对话框框中，输入设置的唯一名称和描述。  
  
10. 选择**设置类型**想，，然后提供所需的信息：  
  
    -   **Mac OS X 首选项**  
  
        -   **应用程序 ID**：指定要用于评估密钥是否相容的属性列表文件的应用程序 ID。  
  
             例如，如果您想要编辑的 Safari Web 浏览器设置，则可能会使用 **com.apple.Safari.plist**。  
  
        -   **密钥**：指定要在 Mac 计算机上评估是否相容的密钥的名称。 使用以下语法： */<dictionary\>/<keyname\>* 。  
  
            > [!IMPORTANT]  
            >  密钥名称区分大小写；如果这些名称与 Mac 计算机上的密钥名称不同，则不会对它们进行评估。 而且，指定密钥名称后，便无法编辑它。 如果需要编辑密钥名称，请删除并重新创建此设置。  
  
    -   **脚本**  
  
        -   **发现脚本**：选择“添加脚本”  ，然后输入用于在 Mac 计算机上评估设置是否相容的 shell 脚本。 使用 shell 脚本中的 **echo** 命令，向 Configuration Manager 返回值以实现符合性。 Configuration Manager 使用 **STDOUT** 中返回的结果评估符合性。  
  
            > [!IMPORTANT]  
            >  请勿在发现脚本中添加“重新启动”  命令。 因为发现脚本在每次客户端重启时都会运行，所以这会导致 Mac 计算机不断重启。  
  
        -   **修正脚本(可选)** ：视需要选择“添加脚本”  ，然后输入用于修正在 Mac 客户端计算机上发现的任何不相容设置的 shell 脚本。  
  
            > [!IMPORTANT]  
            >  若要确保不引入 Mac 计算机无法解释的格式字符，不使用复制和粘贴。 相反，键入在脚本中。  
  
11. 选择“数据类型”  ，这是在它用于评估设置之前条件返回数据所用的格式。  
  
    > [!NOTE]  
    >  **浮点数** 小数点后的数据类型支持只需 3 位数字。  
    >   
    >  Configuration Manager 不支持对 Mac 配置项目脚本设置使用“布尔”  数据类型。 相反，应将数据类型设置为“整数”  ，并确保脚本返回整数值。  
  
12. 单击“确定”  以保存设置，并关闭“创建设置”  对话框。 然后，继续根据需要添加任意多个设置。  
  
13. 在向导的“合规性规则”  页中，指定定义配置项目合规性的条件。 必须至少具有一个符合性规则，才可以评估设置的符合性。 选择“新建”  ，以添加新规则。  
  
14. 在 **Create Rule** 对话框框中，提供以下信息：  
  
    -   **名称**：输入符合性规则的名称。  
  
    -   **说明**：输入符合性规则的说明。  
  
    -   **选定设置**：选择“浏览”  ，以打开“选择设置”  对话框。 选择要为其定义规则的设置，或单击“新建设置”  。 完成后，选择“选择”  。  
  
        > [!TIP]  
        >  还可以选择“属性”  ，以查看当前选定设置的相关信息。  
  
    -   **规则类型**:选择您想要使用的符合性规则的类型：  
  
        -   **值**：创建将配置项目返回的值与指定值进行比较的规则。  
  
        -   **现有**：创建根据设置是否存在于设备上来评估设置的规则。  
  
    -   为规则类型的 **值**, ，指定以下信息：  
  
        -   **设置必须符合以下规则**：选择用于评估选定设置是否相容的运算符和值。 可以使用以下运算符：  
  
            -   **等于**  
  
            -   **不等于**  
  
            -   **大于**  
  
            -   **小于**  
  
            -   **之间**  
  
            -   **大于或等于**  
  
            -   **小于或等于**  
  
            -   **任一**：在文本框中，每行指定一个条目。  
  
            -   **无**：在文本框中，每行指定一个条目。  
  
        -   **在支持时修正不相容规则**：如果希望 Configuration Manager 自动修正不相容规则，请选择此选项。  
  
            > [!IMPORTANT]  
            >  仅当规则运算符设置为“等于”  时，才能修正非符合性规则。  
  
        -   **在找不到此设置实例时报告不相容**：如果在 Mac 计算机上找不到此设置，配置项目报告不相容。  
  
        -   **报表的不相容严重性**：指定在不符合此合规性规则时报告的严重性级别。 可用的严重性级别包括：  
  
            -   **无**：对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  
  
            -   **信息**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**信息**。  
  
            -   **警告**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**警告**。  
  
            -   **严重**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。  
  
            -   **事件严重**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。 Mac 客户端计算机还将记录此严重性级别。  
  
    -   对于规则类型“现有”  ，指定以下信息：  
  
        -   选择：  
  
            -   **此设置必须存在于客户端设备**  
  
            -   **设置不得存在于客户端设备**  
  
        -   **报表的不相容严重性**：指定在不符合此合规性规则时报告的严重性级别。 可用的严重性级别包括：  
  
            -   **无**：对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  
  
            -   **信息**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**信息**。  
  
            -   **警告**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**警告**。  
  
            -   **严重**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。  
  
            -   **事件严重**：对于 Configuration Manager 报表，不符合此合规性规则的计算机将报告故障严重性**严重**。 Mac 客户端计算机还将记录此严重性级别。  
  
        > [!NOTE]  
        >  显示的选项因你要为其配置规则的设置类型而异。  
  
15. 单击“确定”  ，以关闭“创建规则”  对话框。  
  
16. 上**摘要**页上，确认新的配置项目的设置。 然后完成该向导。  
  
此时，应该会在“资产和合规性”  工作区的“配置项目”  节点中看到新配置项目。  
  
如果现在想要将此配置项目添加到配置基线，请参阅[如何在 System Center Configuration Manager 中创建配置基线](../../compliance/deploy-use/create-configuration-baselines.md)。  
  
## <a name="next-steps"></a>后续步骤

 [使用 System Center Configuration Manager 客户端管理的设备的配置项目](../../compliance/deploy-use/create-configuration-items.md)
