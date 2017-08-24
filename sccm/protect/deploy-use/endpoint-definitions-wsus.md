---
title: "WSUS 中的 Endpoint Protection 恶意软件定义 | Microsoft Docs"
definition: Learn how to configure Windows Server Updates Services to auto-approve definition updates.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 0e606b25065fa25c782d1b5f3fbf164e60733353
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>启用 Endpoint Protection 恶意软件定义，以便从 Server Update Services (WSUS) 为 Configuration Manager 下载定义

*适用范围：System Center Configuration Manager (Current Branch)*

 如果使用 WSUS 来使反恶意软件定义保持最新，可以将其配置为自动批准定义更新。 尽管推荐使用 Configuration Manager 软件更新使定义保持最新，但还可以将 WSUS 配置为允许用户手动启动更新的定义。 使用以下过程将 WSUS 配置为定义更新源。

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>在 Configuration Manager 软件更新中同步 Endpoint Protection 定义更新

1.  在 Configuration Manager 控制台中，单击“管理” 。

2.  在“管理”  工作区中，展开“站点配置” ，然后单击“站点” 。

3.  选择包含你的软件更新点的站点。 在“设置”  组中，单击“配置站点组件” ，然后单击“软件更新点” 。

4.  在“软件更新点组件属性”  对话框的“分类”  选项卡中，选择“定义更新”  复选框。

5.  指定使用 WSUS 更新的“产品”  ：

    -   对于 Windows 8.1 和更早版本，在“软件更新点组件属性”  对话框的“产品”  选项卡上，选择“Forefront Endpoint Protection 2010”  复选框。

    -   对于 Windows 10 及更高版本，在“软件更新点组件属性”  对话框的“产品”  选项卡上，选择“Windows Defender”  和“Windows Technical Preview 2”  复选框。

6.  单击“确定”  以关闭“软件更新点组件属性”  对话框。

 WSUS 服务器未集成到 Configuration Manager 环境中时，则使用以下过程配置 Endpoint Protection 更新。

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>若要在独立 WSUS 中同步 Endpoint Protection 定义更新

1.  在 WSUS 管理控制台中，展开“计算机” ，单击“选项” ，然后再单击 “产品和分类” 。

2.  指定使用 WSUS 更新的“产品”  ：

    -   对于 Windows 8.1 和更早版本，在“软件更新点组件属性”  对话框的“产品”  选项卡上，选择“Forefront Endpoint Protection 2010”  复选框。

    -   对于 Windows 10 及更高版本，在“软件更新点组件属性”  对话框的“产品”  选项卡上，选择“Windows Defender”  和“Windows Technical Preview 2”  复选框。

3.  在“产品和分类”  对话框的“分类”  选项卡上，选择“定义更新”  和“更新”  复选框。

## <a name="approving-definition-updates"></a>批准定义更新
 必须先批准 Endpoint Protection 定义更新并将其下载到 WSUS 服务器，然后再将其提供给请求可用更新列表的客户端。 客户端连接到 WSUS 服务器以检查适用的更新，然后请求最新批准的定义更新。

### <a name="to-approve-definitions-and-updates-in-wsus"></a>若要在 WSUS 中批准定义和更新

1.  在 WSUS 管理控制台中，单击“更新” ，然后单击“所有更新”  或想要批准的更新的分类。

2.  在更新列表中，右键单击想要批准以安装的更新，然后单击“批准” 。

3.  在“批准更新”  对话框中，选择想要为其批准更新的计算机组，然后单击“批准安装” 。

 除手动批准以外，还可以为定义更新和 Endpoint Protection 更新设置自动批准规则。 这会将 WSUS 配置为自动批准 WSUS 下载的 Endpoint Protection 定义更新。

### <a name="to-configure-an-automatic-approval-rule"></a>若要配置自动批准规则

1.  在 WSUS 管理控制台中，单击“选项” ，然后单击“自动批准” 。

2.  在“更新规则”  选项卡上，单击“新规则” 。

3.  在“添加规则”  对话框中，在“步骤 1：选择属性” 下选择“当更新在某个特定分类中时”  复选框。

4.  在“步骤 2：编辑属性” 下，单击“任何分类” 。

5.  清除除“定义更新” 以外的所有复选框，然后单击“确定” 。

6.  在“添加规则”  对话框中，在“步骤 1：选择属性” 下选择“当更新在某个特定产品中时”  复选框。

7.  在“步骤 2：编辑属性” 下，单击“任何产品” 。

8.  除适用于 Windows 8.1 及更早版本的“Forefront Endpoint Protection”  或适用于 Windows 10 及更高版本的“Windows Defender”  以外，清除其余所有复选框，然后单击“确定” 。

9. 在“步骤 3：指定一个名称” 下，为该规则输入名称，然后单击“确定” 。

10. 在“自动批准”  对话框中，选择用于新创建的规则的复选框，然后单击“运行规则” 。

> [!NOTE]
>  若要使 WSUS 服务器和客户端计算机上的性能最大化，则拒绝旧定义更新。 若要完成此任务，可以配置自动批准修订和自动拒绝过期更新。 有关详细信息，请参阅 [Microsoft 知识库文章 938947](http://go.microsoft.com/fwlink/p/?LinkId=204078)。

> [!div class="button"]
[下一步 >](endpoint-antimalware-policies.md)

> [!div class="button"]
[返回 >](endpoint-configure-alerts.md)
