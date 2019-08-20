---
title: 基于文件的复制
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 如何使用基于文件的复制在层次结构中的站点之间传输数据
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 685dd1cf6ad0bdea6e6c4aca756a47016cc419b6
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957887"
---
# <a name="file-based-replication"></a>基于文件的复制

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 使用基于文件的复制在层次结构中的站点之间传输基于文件的数据。 此数据包括要部署到子站点中的分发点的应用程序和包。 它还处理未处理的发现数据记录，站点将这些记录传输到其父站点然后进行处理。  

站点之间基于文件的通信通过 TCP/IP 端口 445 使用服务器消息块  (SMB) 协议。 要控制通过网络传输的站点的数据量，请指定带宽限制和脉冲模式。 使用计划来控制何时通过网络发送数据。  

## <a name="bkmk_routes"></a> 路由

下列信息有助于你设置和使用文件复制路由。  

### <a name="file-replication-route"></a>文件复制路由

每个文件复制路由都确定站点将基于文件的数据传输到其中的目标站点。 每个站点都支持到特定目标站点的单一文件复制路由。  

若要管理文件复制路由，请转到“管理”  工作区。 展开“层次结构配置”  节点，然后选择“文件复制”  。  

可以为文件复制路由更改以下设置：  

#### <a name="file-replication-account"></a>文件复制帐户

此帐户连接目标站点，并将数据写入该站点的 **SMS_Site** 共享。 接收站点处理写入到此共享的数据。 默认情况下，将站点添加到层次结构后，Configuration Manager 将新站点服务器的计算机帐户指定为该站点的文件复制帐户。 然后，会将此帐户添加到目标站点的 `SMS_SiteToSiteConnection_<sitecode>` 组。 这个组是计算机的本地组，用于授予对 SMS_Site 共享的访问权限。 你可以将此帐户更改为 Windows 用户帐户。 如果更改帐户，请确保将新帐户添加到目标站点的 `SMS_SiteToSiteConnection_<sitecode>` 组。  

> [!NOTE]  
> 辅助站点始终使用辅助站点服务器的计算机帐户作为“文件复制帐户”  。  

#### <a name="schedule"></a>计划

设置每个文件复制路由的计划。 此操作限制数据可以传输到目标站点时的数据类型和时间。  

#### <a name="rate-limits"></a>速率限制

指定每个文件复制路由的速率限制。 此操作控制站点将数据传输到目标站点时站点所使用的网络带宽：  

- **脉冲模式**：指定由站点发送到目标站点的数据块的大小。 你也可以指定在两次发送各个数据块之间的时间延迟。 如果必须在连接目标站点的低带宽网络上发送数据，请使用此选项。

    例如，你有每五秒发送 1 KB 数据（而不是每三秒发送 1 KB）的限制。 此限制不考虑某个给定时间的链接速度或其使用率。

- **限制为按小时计算的最大传输速率**：站点仅使用你指定的时间百分比将数据发送到目标站点。 Configuration Manager 无法识别网络的可用带宽。 它将可发送数据的时间划分为多个时间片段。 然后，在一个短时间段内发送数据，之后的几个时间段则不发送数据。

    例如，将最大速率设置为 50%  。 Configuration Manager 传输数据并持续一段时间后，在相同的时长内不发送任何数据。 它不会管理其发送的数据块的实际大小。 该站点只管理发送数据的时间量。  

    > [!CAUTION]  
    > 默认情况下，站点可使用最多三个“并发发送”  来将数据传输到目标站点。 如果为文件复制路由启用速率限制，则针对该站点的“并发发送”  数将限制为 1。 即使“限制可用带宽(%)”  设置为“100%”  ，此行为也适用。 例如，如果为发送程序使用默认设置，则此设置会将传输到目标站点时的速率减少到默认能力的三分之一。  

#### <a name="routes-between-secondary-sites"></a>在辅助站点之间路由

在两个辅助站点之间配置文件复制路由，以在这些站点之间路由基于文件的内容。  


### <a name="sender"></a>发送程序

每个站点均具有一个发送程序。 发送程序管理从一个站点到目标站点的网络连接。 它可以同时建立与多个站点的连接。 为连接到站点，发送程序使用指向站点的文件复制路由，并标识要用于建立网络连接的帐户。 发送程序还使用此帐户将数据写入目标站点的 SMS_Site 共享。  

默认情况下，发送程序通过使用多个“并发发送”  或“线程”  将数据写到目标站点。 每个线程可以将基于文件的不同对象传输到目标站点。 发送程序开始发送对象时，它会持续写入该对象的数据块直到发送完整个对象。 在发送完该对象的所有数据后，即可在该线程上开始发送新的对象。  

若要管理站点的发送程序，请转到“管理”工作区，然后展开“站点配置”节点   。 选择“站点”节点，然后选择要管理的站点的“属性”   。 切换到“发送程序”  选项卡以更改发送程序设置。  

可以为发送程序更改下列设置：  

#### <a name="maximum-concurrent-sendings"></a>最大并发发送数

默认情况下，每个站点都使用五个并发发送（线程）。 在向任何一个目标站点发送数据时，可以使用三个线程。 增加此数字后，可以提高站点之间的数据吞吐量。 更多线程意味着 Configuration Manager 可以同时传输更多文件。 提高此数字还会提高对站点之间的网络带宽的要求。  

#### <a name="retry-settings"></a>重试设置

默认情况下，每个站点对问题连接重试两次，并在连接尝试之间延迟一分钟。 可以修改站点所做的连接尝试数和尝试之间的等待时长。  


## <a name="next-steps"></a>后续步骤

[Database replication](/sccm/core/plan-design/hierarchy/database-replication)
