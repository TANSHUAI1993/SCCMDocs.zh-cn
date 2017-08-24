---
title: "Endpoint Protection 恶意软件定义 | Microsoft Docs"
description: "了解如何配置 Configuration Manager 软件更新以将定义更新交付到客户端计算机。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: ca40c2c745ea516b56b637249b892cd44e570a9d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>使用 Configuration Manager 软件更新将定义更新交付

*适用范围：System Center Configuration Manager (Current Branch)*


 可以配置 Configuration Manager 软件更新以将定义更新交付到客户端计算机。 可通过配置自动部署规则完成此操作。 在开始创建自动部署规则之前，请确保你已配置了 Configuration Manager 软件更新。 有关详细信息，请参阅 [System Center Configuration Manager 中的软件更新简介](/sccm/sum/understand/software-updates-introduction)。

> [!NOTE]
>  此过程仅用于必须专门为 Endpoint Protection 配置的项。 有关创建自动部署规则向导的详细信息，请参阅[自动部署规则更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>若要配置自动部署规则以提供定义更新

1.  在 Configuration Manager 控制台中，单击“软件库” 。

2.  在“软件库”  工作区中，展开“软件更新” ，然后单击“自动部署规则” 。

3.  在“主页”  选项卡上的“创建”  组中，单击“创建自动部署规则” 。

4.  在“创建自动部署规则向导”  的“常规” 页上，指定下列信息：

    -   “名称”：输入自动部署规则的唯一名称。

    -   **集合**：选择你想要将定义更新部署到的客户端计算机的集合。

        > [!NOTE]
        >  不能将定义更新部署到用户集合。

5.  单击“添加到现有软件更新组” 。

6.  确保选中“运行此规则后启用部署”   复选框，然后单击“下一步” 。

7.  在向导的“部署设置”  页上的“详细信息级别”  列表中，选择“最小” ，然后单击“下一步” 。

    > [!NOTE]
    >  在“详细信息级别”列表中，选择“最小”（不带 Service Pack 的 Configuration Manager）或“仅错误消息”(Configuration Manager)。 这将减少定义部署返回的状态消息数。 此配置有助于降低 Configuration Manager 服务器上的 CPU 处理使用率。

8.  在“属性筛选器”  列表中，选择“更新分类”  复选框。

9. 在“搜索条件”列表中，单击“<要查找的项\>”。 然后，在“搜索条件”  对话框中的“指定要搜索的值”  列表中，选择“定义更新” 。

10. 单击“确定”  以关闭“搜索条件”  对话框。

11. 在“属性筛选器”  列表中，选择“产品”  复选框。

12. 在“搜索条件”列表中，单击“<要查找的项\>”。 然后，在“搜索条件”  对话框中的“指定要搜索的值”  列表中，选择适用于 Windows 8.1 及更早版本的“Forefront Endpoint Protection 2010”  或适用于 Windows 10 及更高版本的“Windows Defender”  。

13. 单击“确定”  以关闭“搜索条件”  对话框，然后单击“下一步” 。

14. 在“属性筛选器”  列表中，选择“被取代”  复选框。

15. 在“搜索条件”列表中，单击“<要查找的项\>”。 然后，在“搜索条件”  对话框中的“指定要搜索的值”  列表中，选择“否” 。

16. 单击“确定”  以关闭“搜索条件”  对话框，然后单击“下一步” 。

17. 在向导的“评估计划”  页中，选择“启用规则以按计划运行” ，然后配置下载定义更新所依据的计划。 至少将规则设置为在每个软件更新点同步之后运行两个小时。 单击“下一步” 。

18. 在向导的“部署计划”  页上配置下列设置：

    -   “时间根据”：如果希望层次结构中的所有客户端同时安装最新定义，则选择“”  。 实际安装时间将在两小时时段内有所变化。 此设置是建议的最佳方案。

    -   **软件可用时间**：指定可用于由此规则创建的部署的时间。 指定的时间必须至少为自动部署规则运行之后的一小时。 这有助于确保有足够时间将内容复制到层次结构中的分发点。 一些定义更新还可能包括反恶意软件引擎更新，这些更新可能要花更长时间才能到达分发点。

    -   **安装截止时间**：选择“尽快” 。

        > [!NOTE]
        >  软件更新截止时间在两小时时间段内变化，以防止所有客户端在同一时间请求更新。

19. 单击“下一步” 。

20. 在向导的“用户体验”  页上，在“用户通知”  列表中，选择“在软件中心和所有通知中隐藏” 。   这可确保以无提示方式安装定义更新。 单击“下一步” 。

21. 在向导的“警报”  页中，你无需配置任何警报。 Configuration Manager 中的 Endpoint Protection 会生成任何可能需要的警报。 单击“下一步” 。

22. 在向导的“下载设置”  页中，选择必要的软件更新下载行为，然后单击“下一步” 。

23. 在向导的“部署包”  页中，选择现有部署包或创建新的部署包，以包含与规则关联的软件更新文件。

    > [!NOTE]
    >  考虑将定义更新放置在不包含其他软件更新的包中。 此策略可保持定义更新包的大小较小，从而使其可以更快复制到分发点。

24. 在向导的“分发点”  页中，选择此包的内容将被复制到的一个或多个分发点，然后单击“下一步” 。

25. 在向导的“下载位置”  页中，选择“从 Internet 下载软件更新” ，然后单击“下一步” 。

26. 在向导的“语言选择”  页中，选择要下载的更新的每个语言版本，然后单击“下一步” 。

27. 完成“创建自动部署规则向导”。

28. 验证新规则显示在Configuration Manager 控制台的“自动部署规则”节点中。


> [!div class="button"]
[下一步 >](endpoint-antimalware-policies.md)

> [!div class="button"]
[返回 >](endpoint-configure-alerts.md)
