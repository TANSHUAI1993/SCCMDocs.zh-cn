---
title: "配置选项 | Microsoft Docs"
description: "配置选项以使用 System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: b66ed0a5e1c87d8c82853da86e3d55b0e2c043bb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-options-for-updates-publisher"></a>为 Updates Publisher 配置选项

*适用范围：System Center Updates Publisher*

检查并配置影响 Updates Publisher 操作的选项和相关设置。

若要访问 Updates Publisher 选项，请单击控制台左上角的“Updates Publisher 属性”选项卡，然后选择“选项”。

![选项](media/properties1.png)   


选项的分类如下：

-   更新服务器
-   ConfigMgr 服务器
-   代理设置
-   受信任的发行者
-   高级
-   更新
-   日志记录

## <a name="update-server"></a>更新服务器
必须先将 Updates Publisher 配置为与 Windows Server Update Services (WSUS) 等更新服务器协同工作，然后才能[发布更新](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles)。 这包括指定服务器、用于连接远离控制台的服务器的方法，以及用于对你发布的更新进行数字签名的证书。

-   **配置更新服务器**。 配置更新服务器时，请选择 Configuration Manager 层次结构中的顶层 WSUS 服务器（更新服务器），以便所有子网站均有权访问你发布的更新。

  如果更新服务器远离 Updates Publisher 服务器，请指定服务器的完全限定的域名 (FQDN) 以及是否通过 SSL 连接。 通过 SSL 连接时，默认端口介于 8530 到 8531 之间。 请确保设置的端口与更新服务器使用的端口一致。

    > [!TIP]  
    > 如果未配置更新服务器，仍可以使用 Updates Publisher 编写软件更新。

-   **配置签名证书**。 必须先配置并成功连接更新服务器，然后才能配置签名证书。

    Updates Publisher 使用签名证书对发布到更新服务器的软件更新进行签名。 如果更新服务器或运行 Updates Publisher 的计算机的证书存储中没有数字证书，那么发布将失败。

    若要详细了解如何向证书存储添加证书，请参阅 [Updates Publisher 中的证书和安全性](/sccm/sum/tools/updates-publisher-security)。

    如果没有设置为更新服务器自动检测数字证书，请选择以下选项之一：

    -   浏览：仅在运行控制台的服务器上安装了更新服务器后，“浏览”才可用。 选择证书后，必须选择“创建”，才能将证书添加到更新服务器上的 WSUS 证书存储中。 必须为通过此方法选择的证书输入 **.pfx** 文件密码。

    -   创建：选择此选项可新建证书。 还可以将证书添加到更新服务器上的 WSUS 证书存储中。

    **如果创建你自己的签名证书**，请配置以下选项：

    -   启用“允许导出私钥”选项。

    -   为数字签名设置“密钥用法”。

    -   将“最小密钥大小”设置为不小于 2048 位的值。

    使用“删除”选项可从 WSUS 证书存储中删除证书。 当更新服务器位于所使用的 Updates Publisher 控制台附近，或通过 **SSL** 连接远程更新服务器时，此选项可用。

## <a name="configmgr-server"></a>ConfigMgr 服务器
将 Configuration Manager 与 Updates Publisher 结合使用时，请配置下面这些选项。

-   指定 Configuration Manager 服务器：启用对 Configuration Manager 的支持后，指定 Configuration Manager 层次结构中的顶层网站服务器的位置。 如果此服务器远离 Updates Publisher 安装项，请指定网站服务器的 FQDN。 选择“测试连接”，以确保可以连接网站服务器。

-   配置阈值：如果发布的更新的发布项类型为“自动”，需要使用阈值。 阈值有助于确定何时发布更新的完整内容，而不是只发布元数据。 若要详细了解发布项类型，请参阅[将更新分配给发布项](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    可以使用以下阈值之一，也可以两种阈值都使用：

    -   请求客户端计数阈值：此阈值定义了必须有多少个客户端请求更新，Updates Publisher 才能自动发布更新的完整内容。 如果没有指定数量的客户端请求更新，只会发布更新元数据。

    -   包源大小阈值(MB)：此阈值可阻止自动发布超出指定大小的更新。 如果更新的大小超出此阈值，只会发布元数据。 如果更新的大小小于指定阈值，可以发布更新的完整内容。

## <a name="proxy-settings"></a>代理设置
从 Internet 导入软件目录或向 Internet 发布更新时，Updates Publisher 使用代理设置。

-   指定代理服务器的 FQDN 或 IP 地址。 支持 IPv4 和 IPv6。

-   如果代理服务器验证用户是否有权访问 Internet，必须指定 Windows 名称。 不支持通用主体名称 (UPN)。

## <a name="trusted-publishers"></a>受信任的发行者
如果导入更新目录，目录（基于证书）的源被添加为受信任的发布者。 同样，如果发布更新，更新证书的源被添加为受信任的发布者。

可以查看每个发布者的证书详细信息，并从受信任的发布者列表中删除发布者。

不受信任的发布者发布的内容可能会在客户端扫描更新时损坏客户端计算机。 应只接受你信任的发布者发布的内容。

## <a name="advanced"></a>高级
高级选项如下：

-   存储库位置：查看和修改数据库文件 **scupdb.sdf** 的位置。 此文件是 Updates Publisher 存储库。

-   时间戳：启用后，时间戳会添加到签名的更新中，以标识签名时间。 在证书有效时签名的更新可以在签名证书过期后继续使用。 默认情况下，无法部署签名证书过期的软件更新。

-   检查已订阅目录的最新动态：每次启动时，Updates Publisher 都可以自动检查已订阅目录的最新动态。 发现的目录最新动态会在“更新工作区”的“概述”窗口中以“最新警报”的形式详细显示。

-   证书吊销：选择此选项可以启用证书吊销检查。

-   本地源发布：从 Internet 下载要发布的更新前，Updates Publisher 可以先使用它的本地副本。 位置必须是运行 Updates Publisher 的计算机上的文件夹。 默认情况下，此位置是 **My Documents\LocalSourcePublishing**。 如果以前下载过一个或多个更新，或对要部署的更新进行了修改，请选择此选项。

-   软件更新清理向导：启动更新清理向导。 此向导会终止更新服务器上有、但 Updates Publisher 存储库中没有的更新。 请参阅[终止未引用的软件更新](#expire-unreferenced-software-updates)，了解更多详情。

## <a name="updates"></a>更新
 Updates Publisher 可以在每次打开时自动检查是否有新更新。 也可以选择接收 Updates Publisher 的预览版。

若要手动检查更新，请单击 Updates Publisher 控制台中的“属性”![](media/properties2.png)，  
打开“Updates Publisher 属性”，然后选择“检查更新”。

找到新更新后，Updates Publisher 会在“更新可用”窗口中进行显示，然后你可以选择安装。 如果选择不安装更新，将在下次打开控制台时看到安装提示。

## <a name="logging"></a>日志记录
Updates Publisher 将 Updates Publisher 的基本信息记录到 **&lt;*路径*&gt;\Windows\Temp\UpdatesPublisher.log**。

使用记事本或 **CMTrace** 可以查看日志。 CMTrace 是 Configuration Manager 日志文件工具，位于 Configuration Manager 源媒体的 **\SMSSetup\Tools** 文件夹中。

可以更改日志大小及其详细程度。

启用数据库日志记录后，将包括对 Updates Publisher 数据库运行的查询的相关信息。 使用数据库日志记录可能会导致 Updates Publisher 计算机的性能下降。

若要查看日志文件，请单击控制台中的“属性”![](media/properties2.png)，打开“Updates Publisher 属性”，然后选择“查看日志文件”。

## <a name="expire-unreferenced-software-updates"></a>终止未引用的软件更新
可以运行“软件更新清理向导”，终止更新服务器上有、但 Updates Publisher 存储库中没有的更新。 这会通知 Configuration Manager，然后它会从任何未来部署中删除这些更新。

终止更新的操作无法撤回。 只有在确认组织不再需要你选择的软件更新时，才能执行此任务。

### <a name="to-remove-expired-software-updates"></a>如何删除已终止的软件更新
1.  在 Updates Publisher 控制台中，单击“属性”![](media/properties2.png)，打开“Updates Publisher 属性”，然后选择“选项”。

2.  依次选择“高级”和“软件更新清理向导”下的“启动”。

3.  选择要终止的软件更新，然后选择“下一步”。

4.  检查选择的更新后，选择“下一步”，接受选择并终止这些更新。

5.  此向导完成后，选择“关闭”，完成向导。
