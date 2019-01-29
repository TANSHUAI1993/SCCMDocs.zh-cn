---
title: Technical Preview 1608 中的功能
titleSuffix: Configuration Manager
description: 了解 System Center Configuration Manager Technical Preview 1608 版中的可用功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 304f5e65d97682914f917bd2e125763156098225
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896373"
---
# <a name="capabilities-in-technical-preview-1608-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1608 版中的功能

适用范围：System Center Configuration Manager (Technical Preview)

本文介绍了 System Center Configuration Manager Technical Preview 1608 版中的可用功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。      在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager 技术预览版](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    


**以下是此版本可以试用的新功能。**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>准备 ConfigMgr 客户端以便捕获任务序列步骤的改进  
“准备 ConfigMgr 客户端”一步现在将完全删除 Configuration Manager 客户端，而不是仅删除密钥信息。 任务序列每次部署捕获的操作系统映像时，都将安装新的 Configuration Manager 客户端。  


## <a name="improvements-to-software-center"></a>对软件中心的改进
* 软件中心“应用程序”、“更新”和“操作系统”选项卡现在会显示最近添加的软件。 导航窗格中的数字显示每个选项卡中有多少个新软件。
* 用户现在可以请求批准应用程序，然后在“软件中心”的“应用程序详细信息”视图中查看请求历史记录。 “应用程序详细信息”中的“请求”按钮将不再重定向到基于 Web 的应用程序目录。

## <a name="improvements-to-asset-intelligence"></a>对资产智能的改进
针对可让你与其他软件设置父子关系的已列出清单的软件，我们向其属性添加了字段。 在“已列出清单的软件”列表中，可以随后查看任何软件的父软件并隐藏所有子软件。

### <a name="configure-a-parent-to-child-relationship"></a>配置父子关系
  1. 若要设置父软件，请在“已列出清单的软件”节点中，右键单击“已列出清单的软件”列表中的软件项目，然后选择“属性”。
  2. 在打开的对话框中，选择想要设置为父软件的软件（作为初始选择）。

### <a name="filter-the-software-display"></a>筛选软件显示
定义父子关系后，可以筛选视图以仅显示父软件或不具备定义关系的软件。 这将隐藏被设为另一个已列出清单软件的子级的所有软件。 为此，请执行以下操作：
   1.   在搜索栏中选择“添加条件”
   2. 选择“父软件”，然后将条件值更改为“空”，然后单击“搜索”。

现在屏幕将仅显示父软件项目，或不具备定义关系的软件。 只属于另一标题的子级的软件将不会显示。

## <a name="remote-control-keyboard-translation"></a>远程控制键盘转换
以前，Configuration Manager 会将键位置从查看者的位置传输到共享者的位置。 当查看者和共享者的键盘配置不同时会出现问题。 例如，使用英语键盘的查看者键入“A”，但使用法语键盘的共享者则是“Q”。 我们正在更改这种默认行为，以便字符本身从查看者的键盘传输给共享者，且查看者希望键入的字符会传达给共享者。

如果他们希望根据共享者的键盘布局来键入内容，则查看者可以用关闭此行为。 若要更改此行为，请在“Configuration Manager 远程控制”中，选择“操作”，然后选择“启用键盘转换”来传输键位置。

> [!NOTE]
>
> 无法正确转换特殊键（如 ~!#@$%）。
