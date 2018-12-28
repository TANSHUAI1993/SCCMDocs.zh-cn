---
title: 使用应用配置策略配置 Android for Work 应用
titleSuffix: Configuration Manager
description: 通过在用户运行应用之前向其部署应用配置策略，帮助消除运行 Android for Work 的设备上的配置问题。
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f83f26f746c54e3d1defe31df47b3c7c8a7e117
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417942"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中将设置应用于使用应用配置策略的 Android for Work 应用

*适用于：System Center Configuration Manager (Current Branch)*

可以使用 System Center Configuration Manager 中的应用配置策略来分发用户运行应用时可能需要的设置。 例如，应用可能要求用户指定以下详细信息：
- 自定义端口号
- 语言设置
- 安全设置
- 公司徽标之类的品牌设置

如果用户设置输入错误，则修复它们的重担将落到支持人员身上，并且应用部署也将变慢。 为了帮助避免这类问题，可以使用应用配置策略在用户运行应用前先部署所需设置。 这些设置自动与用户关联。 用户无需采取任何操作。
无需将配置策略直接部署到用户和设备，只需部署应用时将策略与部署类型关联。 每当应用检查是否存在策略设置时（通常是应用首次运行时），便应用这些策略设置。

Android 应用配置政策仅适用于运行 Android for Work 的设备。 应用配置策略适用于已从 Play for Work 应用商店批准的应用。 有关批量采购 Android 应用的详细信息，请参阅[如何向 Android for Work 设备部署应用](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps)。

有关应用安装类型的详细信息，请参阅[应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。

## <a name="create-an-app-configuration-policy"></a>创建应用配置策略

1. 在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用配置策略”。
2. 在“主页”选项卡的“应用配置策略”组中，选择“创建应用配置策略”。
3. 在“创建应用配置策略”向导的“常规”页上，设置此策略信息：
   - **名称**。 输入策略的唯一名称。
   - **说明**。 （可选）为了便于轻松识别策略，可以添加说明。
   -  **选择配置策略类型**。 指定应用配置策略的目标平台：**Android for Work 应用配置策略**。
   -  **分配类别以改进搜索和筛选**。 （可选）若要对策略创建和分配类别，选择“类别”。 类别可以方便用户在 Configuration Manager 控制台中对项目进行排序和查找。
4. 在“Android for Work 策略”页上，选择设置配置策略信息的方式：
   - **指定名称和值对**。 可以将此选项用于不使用嵌套的属性列表文件。 指定名称和值对：
        1. 若要添加新的 JSON 对，请选择“新建”。
        2. 在“添加名称/值对”对话框中，指定以下详细信息：
            - **类型**。 从列表中，选择要指定的值的类型。
            - **名称**。 输入要为其指定值的属性列表键的名称。
            - **值**。 输入将应用于所输入的键的值。

   - **浏览到属性列表 JSON 文件**。 如果已经有一个应用配置 JSON 文件或使用嵌套的更复杂的文件，使用此选项。 在“应用配置策略”字段中，以正确的 JSON 格式输入属性列表信息。
5. 若要导入以前创建的 JSON 文件，请选择“选择文件”。
6. 选择“下一步”。 如果 JSON 代码中存在错误，则必须在继续之前更正这些错误。
7. 完成向导中的步骤。

新应配置策略显示在“软件库”工作区的“应用配置策略”节点中。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>将应用配置策略与 Configuration Manager 应用程序关联

若要将应用配置策略与 Android for Work 应用的部署相关联，可按通常方式使用[部署应用程序](/sccm/apps/deploy-use/deploy-applications)主题中的过程来部署应用程序。

在“部署软件向导”的“应用配置策略”页上，选择“新建”。 在“选择应用配置策略”对话框中，选择应用程序部署类型和要将其与之关联的应用配置策略。
安装部署类型后，应用配置策略设置将自动应用。
