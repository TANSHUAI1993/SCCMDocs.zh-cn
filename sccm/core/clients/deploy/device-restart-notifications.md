---
title: 设备重新启动通知
titleSuffix: Configuration Manager
description: 重新启动 Configuration Manager 中各种客户端设置的通知行为。
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b73d3072883405d1ac2b455f12e1c252244884d1
ms.sourcegitcommit: e2e07d74779a2f48693ecaa17a5974204949d109
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999445"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager 中的设备重新启动通知

适用范围：  System Center Configuration Manager (Current Branch)

用户收到等待设备重新启动的通知可能因[计算机重新启动客户端设置](/sccm/core/clients/deploy/about-client-settings#computer-restart)和所使用的 Configuration Manager 版本而异。 本文可帮助管理员确定哪些用户体验用于等待设备重新启动的通知。

>[!NOTE]
> - 本文重点介绍 Configuration Manager 版本 1902 和版本 1906 中找到的客户端设置。


## <a name="deployment-types-for-restart-notifications"></a>重新启动通知的部署类型

[计算机重新启动客户端设置](/sccm/core/clients/deploy/about-client-settings#computer-restart)可更改需要重新启动以下类型的所有必需部署的用户体验：

- [应用程序](/sccm/apps/deploy-use/deploy-applications)
- [任务序列](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [软件更新](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="restart-notification-types"></a>重新启动通知类型

需要重新启动时，将向最终用户显示即将重新启动的通知。 用户可以收到以下四个常规通知：

**Toast 通知**告知你需要重新启动。 Toast 通知中的信息可能因所运行的 Configuration Manager 版本而异。 此类通知是 Windows OS 的本机通知，你也可以使用此类通知来查看第三方软件。

![等待重新启动的 Toast 通知](media/3555947-restart-toast.png)

带有暂停选项的软件中心通知，用于显示在强制重新启动之前剩余的时间。 该消息可能因 Configuration Manager 版本而异。

![带有暂停按钮的等待重新启动软件中心通知](media/3976435-snooze-restart-countdown.png)

用户无法关闭的软件中心最终倒计时通知。 暂停按钮灰显。

![软件中心最终倒计时通知](media/3976435-final-restart-countdown.png)

如果用户在截止时间之前主动安装需要重新启动的必需软件，则他们将看到不同的通知。 当用户体验设置允许通知，并且不使用部署的 Toast 通知时，将显示以下通知。 有关配置这些设置的详细信息，请参阅[部署用户体验设置](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-ux)和[所需部署的用户通知](/sccm/apps/deploy-use/deploy-applications#bkmk_notify)  。

![主动安装的软件的通知](media/3976435-proactive-user-restart-notification.png)

- 当你不使用 Toast 通知时，标记为“可用”的软件的对话框与主动安装的软件类似  。

  - 对于  可用软件，通知没有重新启动的截止时间，用户可以选择自己的暂停间隔。 有关详细信息，请参阅[批准设置](/sccm/apps/deploy-use/deploy-applications#bkmk_approval)。

    ![标记为“可用”的软件在通知中没有重新启动的截止时间。](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>版本 1902 中的设备重新启动通知

<!--3555947-->
有时用户看不到有关重启或必需的部署的 Windows toast 通知。 然后，他们也看不到推迟提醒体验。 当客户端临近截止时间时，此行为可能导致不佳的用户体验。

从版本 1902 开始，在要求进行软件更改或部署需要重新启动时，可以选择使用侵入性更强的对话框窗口。

在客户端设置的[计算机重新启动](/sccm/core/clients/deploy/about-client-settings#computer-restart)组中，启用以下选项：**当部署要求重启时，向用户显示一个对话框窗口而不是 toast 通知**。  

配置此客户端设置可更改需要重新启动 Toast 通知的所有必需部署的用户体验：

![需要重启的 Toast 通知](media/3555947-restart-toast-initial.png)  

侵入性更强的软件中心对话框窗口：

![重新启动计算机的对话框窗口](media/3976435-proactive-user-restart-notification.png)

如果用户在安装后未重新启动其设备，则他们将收到通知作为提醒。 系统会根据客户端设置向用户显示此临时提醒：**向用户显示一条临时通知，指示注销用户或重新启动计算机之前的时间间隔(分钟)** 。 此设置是指在强制重新启动之前，用户必须重新启动计算机的总时间。

- 使用 Toast 通知时的临时通知：

  ![等待重新启动的 Toast 通知](media/3555947-restart-toast.png)

- 使用软件中心对话框窗口时的临时通知，而不是 Toast 通知：

  ![带有暂停按钮的等待重新启动软件中心通知](media/3555947-1902-hide-notification.png)

如果用户在收到临时通知后未重新启动，则会为其显示他们无法关闭的最终倒计时通知。 最终通知的显示时间取决于客户端设置：**显示用户无法关闭的对话框，该对话框显示注销用户或重新启动计算机之前的倒计时间隔(分钟)** 。 例如，如果设置为 60，则会在强制重新启动的前一小时向用户显示最终通知：

![软件中心最终倒计时通知](media/3555947-1902-final-countdown.png)

以下设置的持续时间必须比应用于计算机的最短[维护时段](/sccm/core/clients/manage/collections/use-maintenance-windows)更短：

- **向用户显示一条临时通知，指示注销用户或重新启动计算机之前的间隔(分钟)**
- **显示用户无法关闭的对话框，该对话框显示注销用户或重新启动计算机之前的倒计时间隔(分钟)**

> [!IMPORTANT]
> 在某些情况下，Configuration Manager 1902 中的该对话框将不会替换 Toast 通知。 要解决此问题，请安装 [Configuration Manager 版本1902 的更新汇总](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>从版本 1906 开始的设备重新启动通知
<!--3976435-->
某些管理员倾向于经常发送重新启动通知并将重新启动推迟较短的时间。 而其他管理员允许用户将重新启动推迟更长一段时间，并希望用户不经常收到等待重新启动的通知。 Configuration Manager 版本 1906 使管理员可以更好地控制重新启动通知的时间和频率。 在 1906 中引入了以下各项以使管理员拥有更大的控制权限：

- “指定计算机重启倒计时通知的暂停持续时间(分钟)”  已添加到[“计算机重启客户端设置”](/sccm/core/clients/deploy/about-client-settings#computer-restart)。
- 向用户显示一条临时通知，指示注销用户或重启计算机之前的时间间隔（以分钟为单位），这一时间间隔的最大值从 1440 分钟（24小时）增加到了 20160 分钟（两周）  。
- 在挂起重启时间小于 24 小时之前，用户在重启通知中将无法看到进度条。

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>在截止时间或截止时间之后安装所需软件时的通知

在截止时间或截止时间之后安装所需软件时，用户将看到因所选客户端设置而异的通知。

如果设置“当部署要求重启时，向用户显示对话框窗口，而不是 toast 通知”  设置为：

- **否** - 在收到最终倒计时通知之前，将使用 Toast 通知。
- **是** - 会显示软件中心通知。
  - 如果重新启动时间大于 24 小时，则会显示估计的重新启动时间。 此通知的时间取决于以下设置：**向用户显示一条临时通知，指示注销用户或重新启动计算机之前的时间间隔(分钟)** 。

     ![重新启动时间大于 24 小时](media/3976435-notification-greater-than-24-hours.png)

  - 如果重启时间小于 24 小时，则会显示进度栏。 此通知的时间取决于以下设置：**向用户显示一条临时通知，指示注销用户或重新启动计算机之前的间隔(分钟)**

     ![重新启动时间小于 24 小时](media/3976435-notification-less-than-24-hours.png)

如果用户选择“暂停”  按钮，则会在暂停时段过后显示另一个临时通知，假设尚未进入最终倒计时。 下一个通知的时间取决于以下设置：**指定计算机重新启动倒计时通知的暂停持续时间(小时)** 。 如果用户选择“暂停”  ，并且暂停间隔为 1 小时，则将在 60 分钟内再次通知用户，假设尚未进入最终倒计时。

进入最后倒计时时，将向用户显示他们无法关闭的通知。 进度条用红色显示，用户不能点击“暂停”  。

![版本 1906 中的软件中心最终倒计时通知](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>用户在截止时间之前主动安装

如果用户在截止时间之前主动安装需要重新启动的必需软件，则他们将看到不同的通知。 有关配置这些设置的详细信息，请参阅[部署用户体验设置](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-ux)和[所需部署的用户通知](/sccm/apps/deploy-use/deploy-applications#bkmk_notify)  。 

当用户体验设置允许通知，并且不使用部署的 Toast 通知时，将显示以下通知：

![主动安装的软件的通知](media/3976435-proactive-user-restart-notification.png)

软件的截止时间过后，就会遵循[在截止时间或截止时间之后安装所需软件时的通知](#notifications-when-required-software-is-installed-at-or-after-the-deadline)行为。

## <a name="log-files"></a>日志文件

使用 RebootCoordinator.log 和 SCNotify.log 对设备重新启动进行故障排除   。 你可能还需要根据所使用的部署类型使用其他客户端[日志文件](/sccm/core/plan-design/hierarchy/log-files)。

## <a name="next-steps"></a>后续步骤

- [应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)
- [操作系统部署简介](/sccm/osd/understand/introduction-to-operating-system-deployment)
- [软件更新管理简介](/sccm/sum/understand/software-updates-introduction)
