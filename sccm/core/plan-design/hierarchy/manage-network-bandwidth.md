---
title: "管理用于内容的网络带宽 | Microsoft Docs"
description: "配置 System Center Configuration Manager 的计划、限制和预安排内容。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 14ce376f385ec19d224e8b1a2918eed5379a64e5


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>计划和限制  
 为帮助管理用于内容管理过程的网络带宽，可以使用 Configuration Manager 内置控件进行计划和限制或使用预安排内容。  

 创建包、更改内容的源路径或者更新分发点上的内容时，文件会从源路径复制到站点服务器上的内容库中。 然后，会从站点服务器上的内容库中将内容复制到分发点上的内容库中。 如果已更新内容源文件并分发源文件，则 Configuration Manager 仅检索新文件或更新的文件，然后将其发送到分发点。 可以为站点对站点的通信以及站点服务器与远程分发点之间的通信配置计划和限制控制。 当站点服务器与远程分发点之间的网络带宽受到限制时，即使配置了计划和限制设置之后，你也可能会考虑在分发点上预留内容。  

 在 Configuration Manager 中，可以针对远程分发点配置计划并设置特定限制设置，以确定执行内容分发的时间和方式。 每个远程分发点都可以具有不同的配置，以帮助解决站点服务器到远程分发点的网络带宽限制。 用于远程分发点的计划和限制的控制类似于标准发送程序地址的设置，但是在此情况下，名为“包传输管理器”的新组件使用这些设置。 包传输管理器将站点服务器（主站点或辅助站点）中的内容分发到站点系统上安装的分发点。 限制设置是在“速率限制”  选项卡上配置的，计划设置是在“计划”  选项卡上为不在站点服务器上的分发点配置的。 时间设置是基于发送站点所在时区，而不是分发点的时区。  

> [!WARNING]  
>  仅在未在站点服务器上安装的分发点的属性中显示“速率限制”  和“计划”  选项卡。  

有关为远程分发点配置计划和限制设置的详细信息，请参阅[安装和配置 System Center Configuration Manager 的分发点](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points)。  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>预安排内容  
 可以预留内容，以便在分发内容之前将内容文件添加到站点服务器或分发点上的内容库  

-   由于内容文件已在内容库中，因此，在你分发内容时，不会通过网络传输内容文件。  

-   你可以预留应用程序和包的内容文件  

在 Configuration Manager 控制台中，选择想要预留的内容，然后使用“创建预安排内容文件向导”创建压缩的预安排内容文件，其中包含内容的文件和关联的元数据。 然后，你可以在站点服务器或分发点中手动导入内容。  

-   在站点服务器上导入预留内容文件时，会将内容文件添加到站点服务器上的内容库，然后在站点服务器数据库中注册内容文件  

-   在分发点上导入预留内容文件时，会将内容文件添加到分发点上的内容库，并且向站点服务器发送状态消息，以通知站点内容在分发点上可用  

你可以根据需要将分发点配置为 **预留** 分发点以帮助管理内容分发。 然后，分发内容时可以选择是否希望执行以下操作：  

-   始终在分发点上预留内容  

-   预留包的初始内容，然后在有内容更新时使用标准内容分发流程  

-   对包中的内容始终使用标准内容分发流程  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>确定是否预留内容  
 考虑在下列情况下为应用程序和包预留内容：  

-   **限制从站点服务器到分发点的网络带宽**：如果计划和限制未解决关于通过网络将内容分发到远程分发点的相关问题，请考虑在分发点上预留内容。 每个分发点都具有你可以在分发点属性中配置的“为预留的内容启用此分发点”  设置。 如果你启用此选项，则会将分发点标识为预留的分发点，并且你可以选择如何按包来管理内容。  

     以下设置在应用程序、包、驱动程序包、启动映像、操作系统安装程序和映像的属性中可用，并且允许你配置如何在标识为预留的远程分发点上管理内容分发：  

    -   **在将包分配到分发点时自动下载内容**：如果你具有的包较小，并且其中的计划和限制设置为内容分发提供了足够的控制，请使用此选项。  

    -   **仅下载对分发点所做的内容更改**：如果你具有可能较大的初始包，但你希望对包中内容的未来更新通常较小，请使用此选项。 例如，你可以预留 Microsoft Office 等应用程序，因为初始包大小超过 700 MB 并且太大而无法通过网络发送。 但是，对此包的内容更新可能小于 10 MB 并且容许通过网络进行分发。 另一个示例可能是驱动程序包，其中初始包大小较大，但逐渐添加到包中的驱动程序可能较小。  

    -   **手动将此包中的内容复制到分发点**：如果你具有较大的包（其中包含诸如操作系统之类的内容），并且决不想使用网络将内容分发到分发点，请使用此选项。 如果选择此选项，则必须在分发点上预留内容。  

    > [!WARNING]  
    >  前面的选项适用于单个包，并且仅在分发点被标识为预留时使用。 未被标识为预留的分发点将忽略这些设置。 在此情况下，内容始终通过网络从站点服务器分发到分发点。  

-   **在站点服务器上还原内容库**：当站点服务器失败时，关于内容库中所包含的包和应用程序的信息会在还原过程中还原到站点数据库，但在此过程中不会还原内容库文件。 如果没有用于还原内容库的文件系统备份，则可以从包含必须具有的包和应用程序的其他站点来创建预留的内容文件，然后在还原的站点服务器上提取预留的内容文件。 有关站点服务器备份和恢复的详细信息，请参阅 [System Center Configuration Manager 的备份和恢复](/sccm/protect/understand/backup-and-recovery)  



<!--HONumber=Dec16_HO3-->


