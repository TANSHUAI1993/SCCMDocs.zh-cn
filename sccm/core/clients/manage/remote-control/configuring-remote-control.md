---
title: 配置远程控制
titleSuffix: Configuration Manager
description: 在 System Center Configuration Manager 中设置远程控制。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e4d380319704eda608930ac938232513800b81a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>配置 System Center Configuration Manager 中的远程控制

*适用范围：System Center Configuration Manager (Current Branch)*

 此过程介绍了如何为远程控制配置默认客户端设置。 这些设置将应用于层次结构中的所有计算机。 如果希望这些设置仅应用于某些计算机，请向包含这些计算机的集合分配自定义设备客户端设置。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。 

要使用远程协助或远程桌面，必须在运行 Configuration Manager 控制台的计算机上安装并配置它。 有关如何安装和配置远程协助或远程桌面的详细信息，请参阅 Windows 文档。  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>若要启用远程控制并配置客户端设置  

1.  在 Configuration Manager 控制台中，选择“管理” > “客户端设置” > “默认客户端设置”。  

4.  在“主页”选项卡上的“属性”组中，选择“属性”。  

5.  在“默认”对话框中，选择“远程工具”。  

6.  配置远程控制、远程协助和远程桌面客户端设置。 有关可配置的远程工具客户端设置的列表，请参阅[远程工具](../../../../core/clients/deploy/about-client-settings.md#remote-tools)。  

    可以更改“ConfigMgr 远程控制”  对话框中出现的公司名，方法是配置“计算机代理”  客户端设置中的“在软件中心显示的组织名称”  值。  

 当客户端计算机下一次下载客户端策略时，将使用这些设置进行配置。 要为单个客户端启动策略检索，请参阅 [如何在 System Center Configuration Manager 中管理客户端](../../../../core/clients/manage/manage-clients.md)。  

#### <a name="enable-keyboard-translation"></a>启用键盘转换

默认情况下，Configuration Manager 会将键位置从查看者的位置传输到共享者的位置。 当查看者和共享者的键盘配置不同时会导致出现问题。 例如，使用英语键盘的查看者键入“A”，但使用法语键盘的共享者则是“Q”。 现在可以选择配置远程控制，以便字符本身从查看者的键盘传输给共享者，且查看者希望键入的字符会传达给共享者。

若要开启键盘转换，请在“Configuration Manager 远程控制”中，选择“操作”，然后选择“启用键盘转换”来传输键位置。

> [!NOTE]
>
> 无法正确转换特殊键（如 ~!#@$%）。


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>远程控制查看器的键盘快捷键

|键盘快捷方式|说明|  
|-----------------------|-----------------|  
|Alt+Page Up|运行程序方向从左到右之间切换。|  
|Alt+Page Down|运行程序方向从右到左之间切换。|  
|Alt+Insert|以打开程序的顺序循环运行。|  
|Alt+Home|显示“开始”  菜单。|  
|Ctrl+Alt+End|显示“Windows 安全”对话框 (Ctrl+Alt+Del)。|  
|Alt+Delete|显示 Windows 菜单。|  
|Ctrl+Alt+减号（位于数字键盘）|将本地计算机的活动窗口复制到远程计算机剪贴板。|  
|Ctrl+Alt+加号（位于数字键盘）|将整个本地计算机的活动窗口窗口区复制到远程计算机剪贴板。|  
