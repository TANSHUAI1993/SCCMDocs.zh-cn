---
title: "安装和配置软件更新点 | Microsoft 文档"
description: "主站点需要管理中心站点上的软件更新点，以便评估软件更新合规性，并将软件更新部署到客户端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 05/30/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 7d369384d133c90a15e01df50ac53992d61f3873
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="install-and-configure-a-software-update-point"></a>安装和配置软件更新点  

*适用范围：System Center Configuration Manager (Current Branch)*


> [!IMPORTANT]  
>  在安装软件更新点站点系统角色之前，你必须验证服务器是否满足所需的依赖关系，并确定站点上的软件更新点基础结构。 有关如何规划软件更新和确定软件更新点基础结构的详细信息，请参阅[规划软件更新](../plan-design/plan-for-software-updates.md)。  

 管理中心站点和主站点上需要软件更新点以便启用软件更新符合性评估和将软件更新部署到客户端。 软件更新点在辅助站点上是可选的。 必须在安装了 WSUS 的服务器上创建软件更新点站点系统角色。 软件更新点与 WSUS 服务交互以配置软件更新设置，并请求软件更新元数据的同步。 如果有 Configuration Manager 层次结构，请先在管理中心站点上安装和配置软件更新点，然后依次在子主站点上和根据需要在辅助站点上安装和配置软件更新点。 如果有独立主站点（而不是管理中心站点），请先在主站点上安装和配置软件更新点，然后根据需要在辅助站点上安装和配置软件更新点。 只有当你在顶层站点上配置软件更新点时，某些设置才可用。 视软件更新点安装在何处而定，你必须考虑不同的选项。  

> [!IMPORTANT]  
>  你可以在站点上安装多个软件更新点。 你安装的第一个软件更新点配置为同步源，它从 Microsoft 更新或上游同步源中同步更新。 站点上的其他软件更新点配置为第一个软件更新点的副本。 因此，在你安装和配置初始软件更新点之后，某些设置不可用。  

> [!IMPORTANT]  
>  不支持在服务器上安装已配置和用作独立 WSUS 服务器的软件更新点站点系统，或使用软件更新点来直接管理 WSUS 客户端。 现有 WSUS 服务器仅支持作为活动软件更新点的上游同步源。 请参阅[从上游数据源位置同步](#BKMK_wsussync)

 你可以将软件更新点站点系统角色添加到现有站点系统服务器，或者可以创建新站点系统服务器。 在“创建站点系统服务器向导”或“添加站点系统角色向导”的“系统角色选择”页上，根据你是将站点系统角色添加到新站点服务器还是现有站点服务器，选择“软件更新点”，然后在向导中配置软件更新点设置。 根据所使用的 Configuration Manager 版本，设置会有所不同。 有关如何安装站点系统角色的详细信息，请参阅[安装站点系统角色](../../core/servers/deploy/configure/install-site-system-roles.md)。  

 使用下列部分来了解有关站点上的软件更新点设置的信息。  

## <a name="proxy-server-settings"></a>代理服务器设置  
 可以配置“创建站点系统服务器向导”或“添加站点系统角色向导”不同页上的代理服务器设置，具体取决于使用的 Configuration Manager 的版本。  

-   你必须配置代理服务器，然后指定何时为软件更新使用代理服务器。 配置下列设置：  

    -   在向导的“代理”页上或“站点系统属性”的“代理”选项卡上配置代理服务器设置。 代理服务器设置特定于站点系统，这意味着所有站点系统角色都使用你指定的代理服务器设置。  

    -   指定是否在 Configuration Manager 同步软件更新或通过使用自动部署规则下载内容时使用代理服务器。 在向导的“代理和帐户设置”页上或“软件更新点属性”中的“代理和帐户设置”选项卡上配置软件更新点代理服务器设置。  

        > [!NOTE]  
        >  辅助站点上提供了“使用自动部署规则下载内容时使用代理服务器”设置，但不用于软件更新点。 只有管理中心站点和主站点上的软件更新点才从 Microsoft 更新页下载内容。  

> [!IMPORTANT]  
>  默认情况下，当自动部署规则运行时，将使用在其上创建自动部署规则的服务器的“本地系统”帐户连接到 Internet 并下载软件更新。 当此帐户没有 Internet 访问权限时，软件更新将无法下载并且以下条目会被记录在 ruleengine.log 中：**无法从 Internet 下载更新。错误 = 12007**。 当“本地系统”帐户没有 Internet 访问权限时，配置凭据以连接到代理服务器。  


## <a name="wsus-settings"></a>WSUS 设置  
 必须在“创建站点系统服务器向导”或“添加站点系统角色向导”的不同页上配置 WSUS 设置，具体取决于使用的 Configuration Manager 的版本，在某些情况下，必须仅在软件更新点的属性（也称为软件更新点组件属性）中进行配置。 使用下列部分中的信息来配置 WSUS 设置。  

### <a name="BKMK_wsusport"></a>WSUS 端口设置  
 你必须在向导的“软件更新点”页上或软件更新点的属性中配置 WSUS 端口设置。 使用下列过程来确定 WSUS 使用的端口设置。  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>在 IIS 中确定所用的端口设置  

 1.  在 WSUS 服务器上，打开 Internet Information Services (IIS) 管理器。  

 2.  展开“网站”，右键单击 WSUS 服务器的网站，再单击“编辑绑定”。 在“网站绑定”对话框中，HTTP 和 HTTPS 端口值显示在“端口”列中。


### <a name="configure-ssl-communications-to-wsus"></a>配置与 WSUS 的 SSL 通信  
 你可以在向导的“常规”页上或软件更新点属性的“常规”选项卡上配置 SSL 通信。  

 有关如何使用 SSL 的详细信息，请参阅 [Decide whether to configure WSUS to use SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL)。  

### <a name="wsus-server-connection-account"></a>WSUS 服务器连接帐户  
 你可以配置要在站点服务器连接到软件更新点上运行的 WSUS 时使用的帐户。 如果不配置此帐户，Configuration Manager 将使用要连接到 WSUS 的站点服务器的计算机帐户。 在向导的“代理和帐户设置”页上或“软件更新点属性”中的“代理和帐户设置”选项卡上配置 WSUS 服务器连接帐户。  可以在向导的不同位置中配置帐户，具体情况视使用的 Configuration Manager 版本而定。  

 有关 Configuration Manager 帐户的详细信息，请参阅 [System Center Configuration Manager 中使用的帐户](../../core/plan-design/hierarchy/accounts.md)。  

## <a name="synchronization-source"></a>同步源  
 在向导的“同步源”页上，或者在“软件更新点组件属性”中的“同步设置”选项卡上，你可以配置软件更新同步的上游同步源。 同步源的选项因站点而异。  

 使用下表以了解配置站点中的软件更新点时的可用选项。  

|站点|可用的同步源选项|  
|----------|----------------------------------------------|  
|-   管理中心站点<br />-   独立主站点|-   从 Microsoft 更新网站同步<br />-   从上游数据源位置同步<br />-   不从 Microsoft 更新或上游数据源同步|  
|-   站点中的附加软件更新点<br />-   子主站点<br />-   辅助站点|-   从上游数据源位置同步|  

 以下列表提供了有关可用作同步源的每个选项的详细信息：  

-   从 Microsoft 更新同步：使用此设置以从 Microsoft 更新同步软件更新元数据。 管理中心站点必须具有 Internet 访问权限。否则，同步将失败。 只有在配置顶层站点的软件更新点后才可以使用此设置。  

    > [!NOTE]  
    >  如果软件更新点与 Internet 之间存在防火墙，则可能需要将防火墙配置为接受用于 WSUS 网站的 HTTP 和 HTTPS 端口。 你也可以选择将防火墙上的访问权限局限于受限制的域。 有关如何规划支持软件更新的防火墙的详细信息，请参阅 [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)。  

-   **<a name="BKMK_wsussync"></a>**从上游数据源位置同步：使用此设置以从上游同步源同步软件更新元数据。 系统会将子主站点和辅助站点自动配置为将父站点 URL 用于此设置。 你可以选择将从现有的 WSUS 服务器同步软件更新。 指定 URL，如 https://WSUSServer:8531 ，其中 8531 是用于连接到 WSUS 服务器的端口。  

-   不要从 Microsoft 更新或上游数据源同步：使用此设置以在顶层站点上的软件更新点从 Ineternet 断开连接时手动同步软件更新。 有关详细信息，请参阅[从断开连接的软件更新点中同步软件更新](synchronize-software-updates-disconnected.md)。  

> [!NOTE]  
>  如果软件更新点与 Internet 之间存在防火墙，则可能需要将防火墙配置为接受用于 WSUS 网站的 HTTP 和 HTTPS 端口。 你也可以选择将防火墙上的访问权限局限于受限制的域。 有关如何规划支持软件更新的防火墙的详细信息，请参阅 [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls)。  

 你还可配置是在向导“同步源”页上还是在“软件更新点组件属性”的“同步设置”选项卡上创建 WSUS 报告事件。 Configuration Manager 不使用这些事件；因此，通常选择默认设置“不创建 WSUS 报告事件”。  

## <a name="synchronization-schedule"></a>同步计划  
 在向导的“同步计划”页上或者在“软件更新点组件属性”中配置同步计划。 仅在顶层站点的软件更新点上配置此设置。  

 如果启用计划，则可以配置一个简单或自定义的定期同步计划。 如果只是配置简单的计划，则开始时间基于在创建计划时运行 Configuration Manager 控制台的计算机的本地时间。 如果配置自定义计划的开始时间，则此开始时间基于运行 Configuration Manager 控制台的计算机的本地时间。  

> [!TIP]  
>  使用适合你的环境的时间范围来计划运行软件更新同步。 常见的一种情况是将软件更新同步计划设置为在每月第二个星期二发布了 Microsoft 定期安全更新（这通常称为周二补丁日）之后立即运行。 另一种常见的情况是将软件更新同步计划设置为每天使用软件更新提供 Endpoint Protection 定义和引擎更新时运行。  

> [!NOTE]  
>  如果选择不按计划启用软件更新同步，则可以从“软件库”工作区内的“所有软件更新”或“软件更新组”节点中手动同步软件更新。 有关详细信息，请参阅[同步软件更新](synchronize-software-updates.md)。  

## <a name="supersedence-rules"></a>取代规则  
 在向导的“取代规则”页上或者在“软件更新点组件属性”中的“取代规则”选项卡上配置取代设置。 只能在顶层站点上配置取代规则。  

 在此页上，你可以指定被取代的软件更新立即过期，这会阻止将它们包含在新部署中并标记现有部署，以指明被取代的软件更新包含一个或多个过期的软件更新。 或者，你可以指定被取代软件更新过期之前的时间段，从而允许你继续部署这些更新。 有关详细信息，请参阅 [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules)。  

> [!NOTE]  
>  向导的“取代规则”页仅当在站点配置第一个软件更新点时可用。 当你安装其他软件更新点时，此页不会显示。  

## <a name="classifications"></a>分类  
 在向导的“分类”页上或者在“软件更新点组件属性”中的“分类”选项卡上配置分类设置。 有关软件更新分类的详细信息，请参阅 [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications)。  

> [!NOTE]  
>  向导的“分类”页仅当在站点配置第一个软件更新点时可用。 当你安装其他软件更新点时，此页不会显示。  

> [!TIP]  
>  当你首次在顶层站点上安装软件更新点时，请清除所有软件更新分类。 初次软件更新同步之后，请配置更新的列表中的分类，然后重新启动同步。 仅在顶层站点的软件更新点上配置此设置。  

## <a name="products"></a>产品  
 在向导的“产品”页上或者在“软件更新点组件属性”中的“产品”选项卡上配置产品设置。  

> [!NOTE]  
>  向导的“产品”页仅当在站点配置第一个软件更新点时可用。 当你安装其他软件更新点时，此页不会显示。  

> [!TIP]  
>  当你首次在顶层站点上安装软件更新点时，请清除所有产品。 初次软件更新同步之后，请配置更新的列表中的产品，然后重新启动同步。 仅在顶层站点的软件更新点上配置此设置。  

## <a name="languages"></a>语言  
 在向导的“语言”页上或者在“软件更新点组件属性”中的“语言”选项卡上配置语言设置。 指定想要对其同步软件更新文件和摘要详细信息的语言。 在 Configuration Manager 层次结构中的每个软件更新点上配置“软件更新文件”设置。 “摘要详细信息”设置仅在顶层软件更新点上配置。 有关详细信息，请参阅 [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages)。  

> [!NOTE]  
>  向导的“语言”页仅在安装管理中心站点的软件更新点时可用。 你可以在“软件更新点组件属性”内的“语言”选项卡中配置子站点中的软件更新文件语言。  

## <a name="next-steps"></a>后续步骤
在 Configuration Manager 层次结构中的顶层站点，开始安装软件更新点。 重复该主题中的步骤，在子级站点上安装软件更新点。

安装软件更新点后，请转到[同步软件更新](synchronize-software-updates.md)。
