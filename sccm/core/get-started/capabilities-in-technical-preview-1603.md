---
title: "Technical Preview 1603 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1603 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: dee2b4ce042bb4a434bb019e17a6b16e2807945c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1603 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview 1603 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 或者，如果使用的是 System Center Technical Preview 5，此版本将作为 System Center Configuration Manager Technical Preview 的基准版本安装。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

 **此 Technical Preview 中的已知问题：**  

-   此版本包括以前发布的功能的更新，但不会引入新功能。 因此，如果以前升级到 1602 并启用了 1602 中包含的所有功能，则更新向导的“功能”页将为空。  

-   站点服务器更新到 Technical Preview 1603 之后，客户端无法使用任何远程控制功能，直到它们也更新到版本 1603。  

 **以下是可以试用的此版本的新功能。**  

##  <a name="BKMK_SC1603"></a>对软件中心的改进  

### <a name="new-tiled-view-for-apps"></a>应用的新平铺视图  
 最终用户现在可以在软件中心的“应用程序”选项卡中选择应用列表或应用的平铺视图。  

### <a name="select-multiple-updates-in-software-center"></a>在软件中心中选择多个更新  
 在软件中心的“更新”选项卡中，现在可以选择多个更新，或选择“全部更新”以开始同时安装多个更新。  

##  <a name="BKMK_RC1603"></a>对远程控制的改进  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>在远程控制会话中限制共享剪贴板访问  
 现在可以启用新的远程工具客户端设置“提示用户提供共享剪贴板文件传输权限”，以在远程控制会话中限制对共享剪贴板的访问。  

 启用时，共享远程会话的最终用户必须先向该会话的查看者授予权限，然后查看者才能通过共享剪贴板将文件从会话传输到其本地计算机。  

 这会如同以前一样为最终用户添加一层保护，如果向查看者授予了最终用户计算机的完全控制，则他们能够采用对最终用户完全透明的方式，使用共享剪贴板将文件从会话传输到其本地计算机。  

##  <a name="BKMK_RamDiskTFTP"></a> 在启用 PXE 的分发点上自定义 RamDisk TFTP 块大小和窗口大小  
 在 1603 Technical Preview 中，可以为启用 PXE 的分发点自定义 RamDisk TFTP 块大小和窗口大小。 如果自定义了网络，则可能导致启动映像下载由于超时错误而失败，因为块大小或窗口大小太大。 通过 RamDisk TFTP 块大小和窗口大小自定义可以在使用 PXE 时优化 TFTP 流量，以满足特定网络要求。   
需要在环境中测试自定义设置以确定最高效的设置。  

-   **TFTP 块大小**：块大小是服务器发送到下载文件（如 RFC 2347 中所述）的客户端的数据包大小。 较大的块大小使服务器可以发送较少的数据包，因此服务器与客户端之间的往返延迟较少。 但是，较大的块大小会导致零碎的数据包，而大多数 PXE 客户端实现不支持这一点。  

-   **TFTP 窗口大小**：对于发送的每个数据块，TFTP 需要确认 (ACK) 数据包。 服务器在收到上一个块的 ACK 数据包之前，不会发送序列中的下一个块。 TFTP 窗口是 Windows 部署服务中的一个功能，使你可以定义填满窗口所需的数据块数。 服务器在窗口填满之前会背靠背地发送数据块，随后客户端会发送 ACK 数据包。 增加此窗口大小会减少客户端与服务器之间的往返延迟数，并缩短下载启动映像所需的总体时间。  

### <a name="try-it-out"></a>试试看！  
 尝试完成下面的任务，然后使用本主题顶部附近的反馈信息，让我们知道它的工作方式：  

-   我可以在启用 PXE 的分发点上自定义 RamDisk TFTP 窗口大小。  

-   我可以在启用 PXE 的分发点上自定义 RamDisk TFTP 块大小。  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>修改 RamDisk TFTP 窗口大小  

-   在启用 PXE 的分发点上添加以下注册表项以自定义 RamDisk TFTP 窗口大小：  

     **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    名称：RamDiskTFTPWindowSize  

     **类型**：REG_DWORD  

     **值**：&lt;customized window size\>  

 默认值为 1（1 个数据块填满窗口）  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>修改 RamDisk TFTP 块大小  

-   在启用 PXE 的分发点上添加以下注册表项以自定义 RamDisk TFTP 窗口大小：  

     **位置**：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    名称：RamDiskTFTPBlockSize  

     **类型**：REG_DWORD  

     **值**：&lt;customized block size\>  

 默认值为 4096 (4k)。  
