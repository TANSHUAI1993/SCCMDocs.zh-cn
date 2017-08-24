---
title: "管理更新目录 | Microsoft Docs"
description: "管理 System Center Updates Publisher 中的软件更新目录"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 7451d699e0e5e146b0538a57deca595188d113bf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>管理 Updates Publisher 中的软件更新目录

*适用范围：System Center Updates Publisher*

使用“目录工作区”可管理软件更新目录。 这包括添加新目录、管理现有目录订阅，以及将更新信息从目录导入 Updates Publisher 存储库。

软件更新目录包含非 Microsoft 组织创建的相关更新的信息。 其他组织包括你自己的组织，以及向 Microsoft 注册过目录的第三方软件供应商。 软件供应商注册的目录称为*合作伙伴目录*。 你创建的未向 Microsoft 注册的目录称为*用户*目录。

## <a name="add-software-update-catalogs"></a>添加软件更新目录
必须先向 Updates Publisher 添加更新目录，然后才能管理其中包含的更新。 在你添加目录后，Updates Publisher 便会：
-   创建此目录的订阅，从而能够检查此目录的最新动态。
-   将此目录添加到“目录工作区”的“我的软件更新目录”窗口中的列表内。  

控制台中显示每个已订阅目录的信息。 信息包括下载 URL 或位置、目录创建公司或组织名称以及上次导入或修改时间。

Updates Publisher 可以在每次启动时自动检查订阅是否有变化。 这可配置为[高级选项](/sccm/sum/tools/updates-publisher-options#advanced)。 配置后，Updates Publisher 会引用订阅的下载 URL 或位置信息，然后在目录自上次导入存储库起有变化时提醒你。

若要手动查看目录最新动态，请选择“我的软件更新目录”列表中的目录，然后从功能区中选择“刷新”。

除了添加目录和查看已订阅目录的信息以外，还可以：
-  **编辑***用户*目录的信息。
-  从 Updates Publisher 中**删除**（移除）目录。
-  将目录中的更新**导入** Updates Publisher 存储库。 导入更新时，即导入目录中包含的所有更新。 然后，可以在“更新工作区”中查看更新，稍后可以在其中选择更新，并将其发布到更新服务器。

> [!NOTE]   
> 从 Updates Publisher 中删除目录也会将其中包含的更新从存储库中删除。 此操作不会影响已发布到更新服务器的更新。 若要从更新服务器中删除存储库中不再有的更新，请参阅[终止未引用的软件更新](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates)。

## <a name="manage-update-catalogs"></a>管理更新目录
可以在“目录工作区”的“我的软件更新目录”窗口中查看已导入的列表目录。 在此工作区中，可以执行下列操作：

-   **添加合作伙伴目录：**使用以下任一方法查找新的合作伙伴目录：

    -   在控制台中，依次转到“更新工作区” > “概述”。 在“入门”窗口中，选择“添加合作伙伴软件更新目录”。

    -   在控制台中，依次转到“目录工作区” > “我的目录”。 然后，从功能区中选择“添加目录”。

-   **添加用户目录：**在控制台中，依次转到“目录工作区” > “我的目录”。 然后，从功能区中选择“添加目录”。 除了 .cab 文件的位置以外，还必须指定“发布者”、“名称”和“说明”来标识目录。


-   **检查目录最新动态：**选择一个或多个目录，然后选择功能区中的“刷新”。

-   **编辑用户目录：**选择*用户*目录，然后选择功能区中的“编辑”。 然后，可以修改用户定义的属性。

-   **删除目录：**选择一个或多个目录，然后选择功能区中的“删除”。 这会从 Updates Publisher 存储库中删除目录、订阅以及目录中的更新。

-   **向存储库添加目录中的更新**：选择功能区中的“导入”，启动“导入目录”向导。 有关详细信息，请参阅[导入更新](#import-updates)

## <a name="import-updates"></a>导入更新
如果导入目录，Updates Manager 会将相应目录中的更新添加到 Updates Publisher 存储库中。 导入更新后，可以将其发布到更新服务器，以供受管理设备使用。

### <a name="to-import-updates"></a>如何导入更新
1.  若要启动“导入目录”向导，请从以下任一工作区的功能区中选择“导入”：

    -   目录工作区

    -   更新工作区

2.  在“导入类型”页中，选择已添加到 Updates Publisher 中的一个或多个目录，或指定尚未添加为订阅的目录的路径。 选择“下一步”查看摘要屏幕。完成后，选择“下一步”开始导入。

3.  在“安全警告 - 目录验证”窗口中，检查目录证书。完成后，选择“接受”导入更新。

    > [!CAUTION]    
    > 仅接受你信任的发布者发布的更新。 不受信任的发布者发布的软件更新可能会在扫描更新时损坏客户端计算机。

    >  如果不再信任某发布者，请将此发布者从受信任的发布者列表中删除。 若要详细了解如何接受目录，请单击“安全警告 - 目录验证”对话框中的“告诉我详细信息”。

    如果选择始终接受某发布者发布的目录，请将此发布者添加到[“受信任的发布者列表”](/sccm/sum/tools/updates-publisher-options#trusted-publishers)中。 可以使用 Updates Publisher 选项检查和编辑此列表。

4.  当存储库中已有更新且满足以下任一条件时，导入向导会跳过更新导入：

    -   更新自上次导入后未发生变化。

    -   更新已经过编辑且具有新的数字哈希。 编辑更新可防止新更新覆盖原始更新，因为如果导入，则会覆盖你可能已部署的更改。

5.  在“确认”页上，检查导入结果。

6.  单击“关闭”，完成向导。 现在，可以在“更新工作区”中查看此目录的更新。

## <a name="next-steps"></a>后续步骤
导入更新后，可执行的常见操作包括：
-   [管理更新](/sccm/sum/tools/manage-updates-with-updates-publisher)，从而在更新服务器上捆绑、分配和部署更新。
-   [创建适用性规则](/sccm/sum/tools/updates-publisher-applicability-rules)，以帮助确定更新在更新服务器上的部署时间。
