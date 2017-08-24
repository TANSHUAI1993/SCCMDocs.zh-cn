---
title: "远程管理 Windows 计算机 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理远程 Windows 客户端计算机。"
ms.custom: na
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: aecc4ccfec98932f3988f1ca1fcdc898cd417933
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>如何使用 System Center Configuration Manager 远程管理 Windows 客户端计算机

*适用范围：System Center Configuration Manager (Current Branch)*

在开始使用远程控制之前，请确保已经查看了以下主题的信息：  

-   [System Center Configuration Manager 中远程控制的先决条件](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [配置 System Center Configuration Manager 中的远程控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

以下是启动远程控制查看器的三种方式：  

-   在 Configuration Manager 控制台中。  

-   在 Windows 命令提示符中。  

-   在运行 Configuration Manager 控制台的计算机上的 Windows“开始”菜单中（从“Microsoft System Center”程序组）。  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>若要从 Configuration Manager 控制台中远程管理客户端计算机  

1.  在 Configuration Manager 控制台中，依次选择“资产和符合性” > “设备”或“设备集合”。  

3.  选择要远程管理的计算机，然后在“主页”选项卡上的“设备”组中，选择“启动” > “远程控制”。  

    > [!IMPORTANT]  
    >  如果将“提示用户进行远程控制”  客户端设置权限设置为“真” ，直至远程计算机上的用户同意远程控制提示后才会启动连接。 有关详细信息，请参阅[配置 System Center Configuration Manager 中的远程控制](../../../../core/clients/manage/remote-control/configuring-remote-control.md)。  

4.  “Configuration Manager 远程控制”  窗口打开后，就可以远程管理客户端计算机了。 使用下列选项来配置连接。  

    > [!NOTE]  
    >  如果连接的计算机有多台监视器，那么远程控制窗口中会显示所有这些监视器的显示内容。  

    -   **文件 - 连接** - 连接到另一台计算机。 远程控制会话处于活动状态时，此选项不可用。  

    -   **文件 - 断开** - 断开活动远程控制会话的连接，但不会关闭“Configuration Manager 远程控制”窗口。  

    -   **文件 - 退出** - 断开活动远程控制会话的连接，并关闭“Configuration Manager 远程控制”窗口。  

        > [!NOTE]  
        >  当断开远程控制会话的连接时，将删除正在查看的计算机上 Windows 剪贴板的内容。  

    -   **视图 - 全屏** - 最大化显示“Configuration Manager 远程控制”窗口。  

        > [!NOTE]  
        >  要退出全屏显示模式，请按 Ctrl + Alt + Break。  

    -   **视图 - 调整为适合页面** - 缩放远程计算机的显示尺寸以适合“Configuration Manager 远程控制”窗口的大小。  

    -   **视图 - 状态栏** - 切换“Configuration Manager 远程控制”窗口状态栏显示。  

    -   **操作 - 发送 Ctrl+Alt+Del 键** - 向远程计算机发送 Ctrl+Alt+Del 键组合。  

    -   **操作 - 启用剪贴板共享** - 允许从/向远程计算机复制和粘贴项目。 如果更改此值，必须重新启动远程控制会话，更改才会生效。  

        > [!NOTE]  
        >  如果不希望在 Configuration Manager 控制台中启用剪贴板共享，请在运行控制台的计算机上将注册表项“HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing”的值设置为“0”。  

    -   **操作 - 锁定远程键盘和鼠标** - 锁定远程键盘和鼠标以阻止用户操作远程计算机。  

    -   **帮助 - 关于远程控制** - 显示查看器的当前版本。  

5.  远程计算机上的用户在单击 Windows 通知区域中的 Configuration Manager“远程控制”图标或远程控制会话栏上的图标时可以查看有关远程控制会话的详细信息。  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>若要从 Windows 命令行中启动远程控制查看器  

-   在 Windows 命令提示符处键入 <Configuration Manager Installation Folder\>**\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe 支持以下命令行选项：  

- Address - 指定要连接的客户端计算机的 NetBIOS 名称、完全限定域名 (FQDN) 或 IP 地址。
- Site Server Name - 指定要向其发送与远程控制会话相关的状态消息的 System Center Configuration Manager 站点服务器的名称。
- **/?** - 显示远程控制查看器的命令行选项。  
     
**示例：CmRcViewer.exe** <Address\> <\\\Site Server Name>  
