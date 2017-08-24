---
title: "配置 Endpoint Protection 警报 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中配置 Endpoint Protection 警报。"
ms.custom: na
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 7f4329b289b606dee5bf31aad8207de52667229f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中为 Endpoint Protection 配置警报

*适用范围：System Center Configuration Manager (Current Branch)*

 可以在 Microsoft System Center Configuration Manager 中配置 Endpoint Protection 警报，以便在层次结构中发生特定事件（如恶意软件感染时）通知管理用户。 通知会显示在 Configuration Manager 控制台 Endpoint Protection 仪表板中“监视”工作区的“警报”节点中，或是可以通过电子邮件发送到指定用户。

 使用本主题中的下列步骤和补充过程在 Configuration Manager 中为 Endpoint Protection 配置警报。

> [!IMPORTANT]
>  你必须具有集合的“强制实施安全”权限才能配置 Endpoint Protection 警报。

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>在 Configuration Manager 中为 Endpoint Protection 配置警报的步骤

1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。

2.  在“资产和符合性”  工作区中，单击“设备集合” 。

3.  在“设备集合”  列表中，选择要为其配置警报的集合，然后，在“主页”  选项卡中的“属性”  组中单击“属性” 。

    > [!NOTE]
    >  无法为用户集合配置警报。

4.  如果你想要在 Configuration Manager 控制台的“监视”工作区中查看有关此集合的反恶意软件操作的详细信息，则在“<集合名称\>属性”对话框的“警报”选项卡中，选择“在 Endpoint Protection 仪表板中查看此集合”。

    > [!NOTE]
    >  此选项不可用于“所有系统”  集合。

5.  在“<集合名称\>属性”对话框的“警报”选项卡上，单击“添加”。

6.  在“添加新的集合警报”对话框中的“这些条件适用时生成警报”部分中，选择在指定的 Endpoint Protection 事件发生时想要 Configuration Manager 生成的警报，然后单击“确定”。

7.  在“警报”选项卡的“条件”列表中，选择每个 Endpoint Protection 警报，然后指定下列信息：

    -   **警报名称** - 接受默认名称，或者输入新的警报名称。

    -   **警报严重性** - 在列表中，选择要在 Configuration Manager 控制台中显示的警报级别。

8.  根据你选择的警报，指定以下其他信息：

    -   **恶意软件检测** - 如果在所监视集合中的任何计算机上检测到恶意软件，则会生成此警报。 **恶意软件检测阈值**指定生成此警报时的恶意软件检测级别：

        -   **高 - 所有检测** - 当在指定集合中的一台或多台计算机上检测到任何恶意软件时且无论 Endpoint Protection 客户端执行何种操作，将生成此警报。

        -   **中 - 检测到，挂起操作** - 当在指定集合中的一台或多台计算机上检测到恶意软件时且必须手动删除此恶意软件，将生成此警报。

        -   **低 - 检测到，仍处于活动状态** - 当在指定集合中的一台或多台计算机上检测到恶意软件且软件仍处于活动状态时，将生成此警报。

    -   **恶意软件爆发** - 如果在你监视的集合中指定百分比的计算机上检测到指定的恶意软件，则将生成此警报。

        -   **检测到恶意软件的计算机的百分比** - 当集合中检测到恶意软件的计算机的百分比超过你指定的百分比时，将生成此警报。 指定介于“1”  到“99” 之间的百分比。

            > [!NOTE]
            >  百分比值基于集合中的计算机数，但不包括没有安装 Configuration Manager 客户端的计算机。 其中包括尚未安装 Endpoint Protection 客户端的计算机。

    -   **已重复恶意软件检测** - 如果在你监视的集合中的计算机上，在指定的小时数内检测到特定恶意软件的次数超出指定次数，则会生成此警报。 指定以下信息以配置此警报：

        -   **检测到恶意软件的次数：** - 当在集合中的计算机上检测到同一恶意软件的次数超过指定次数时，则会生成此警报。 指定一个介于“2”  到“32” 之间的数字。

        -   **检测间隔（小时）：** 指定在其间必须发生指定的恶意软件检测次数的检测间隔（以小时为单位）。 指定一个介于“1”  到“168” 之间的数字。

    -   **多恶意软件检测** - 如果在所监视集合中的计算机上，在指定的小时数内检测到的恶意软件类型超出指定数量，则会生成此警报。 指定以下信息以配置此警报：

        -   **检测到的恶意软件类型数：** 当在集合中的计算机上检测到指定数量的不同恶意软件类型时，则会生成此警报。 指定一个介于“2”  到“32” 之间的数字。

        -   **检测间隔（小时）：** 指定在其间必须发生指定的恶意软件检测次数的检测间隔（以小时为单位）。 指定一个介于“1”  到“168” 之间的数字。

9. 单击“确定”关闭“<集合名称\>属性”对话框。  

## <a name="alert-for-outdated-malware-client"></a>过时的恶意软件客户端的警报

从 Configuration Manager 版本 1702 开始，可以配置警报，以确保 Endpoint Protection 客户端不会过时。 现在，可通过转到“资产和符合性” > “概述” > “设备” > “所有桌面和服务器客户端”来查看“反恶意软件客户端版本”和“Endpoint Protection 部署状态”。 若要查看警报，请在“监视”工作区中查看“警报”。 如果超过 20% 托管客户端运行反恶意软件的过期版本，将显示“反恶意软件客户端版本已过期”警报。 此警报不会出现在“监视” > “概述”选项卡中。 若要更新过期的反恶意软件客户端，可启用反恶意软件客户端的软件更新。

若要配置生成警报的百分比，请展开“监视” > “警报” > “所有警报”，双击“反恶意软件客户端已过期”，然后修改“如果具有过期版本的反恶意软件客户端的托管客户端百分比超过以下值，发出警报”选项。

> [!div class="button"]
[下一步 >](endpoint-definition-updates.md)

> [!div class="button"]
[返回 >](endpoint-protection-site-role.md)
