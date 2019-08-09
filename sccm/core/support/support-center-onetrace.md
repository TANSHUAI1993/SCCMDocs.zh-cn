---
title: 支持中心 OneTrace（预览）
titleSuffix: Configuration Manager
description: OneTrace 是一个带有支持中心的新日志查看器，它在 CMTrace 的基础上进行了改进。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a015277f9a2fb05c4fbecc4d702d63a5a97777ca
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537973"
---
# <a name="support-center-onetrace-preview"></a>支持中心 OneTrace（预览）

<!--3555962-->

从版本 1906 开始，OneTrace 是一个带有支持中心的新日志查看器。 它的工作方式与 CMTrace 类似，同时具有以下改进：

- 选项卡式视图
- 可停靠窗口
- 改进了搜索功能
- 无需离开日志视图，即可启用筛选器
- 可以快速识别错误群集的滚动条提示
- 可快速打开大型文件的日志

![OneTrace 日志查看器的屏幕截图](media/3555962-onetrace.png)

OneTrace 适用于许多类型的日志文件，如：

- Configuration Manager 客户端日志
- Configuration Manager 服务器日志
- 状态消息
- Windows 10 上的 Windows 更新 ETW 日志文件
- Windows 7 和 Windows 8.1 上的 Windows 更新日志文件

## <a name="prerequisites"></a>先决条件

- .NET Framework 版本 4.6 或更高版本

## <a name="install"></a>安装

OneTrace 与支持中心一起安装。 通过以下路径在站点服务器上找到支持中心安装程序：`cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

> [!Note]  
> 支持中心和 OneTrace 使用 Windows Presentation Foundation (WPF)。 此组件在 Windows PE 中不可用。 继续在具有任务序列部署的启动映像中使用 CMTrace。  

## <a name="see-also"></a>另请参阅

- [支持中心日志查看器](/sccm/core/support/support-center-ui-reference#bkmk_log-viewer)

- [CMTrace](/sccm/core/support/cmtrace)
