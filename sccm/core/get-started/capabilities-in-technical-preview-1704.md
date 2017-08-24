---
title: "Technical Preview 1704 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview（版本 1704）中的可用功能。"
ms.custom: na
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7caee47ca74064630e09c1bdb94187af256d4b4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1704 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview（版本 1704）中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    


**以下是可以试用的此版本的新功能。**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>使用应用配置策略配置 Android 应用
可以使用 System Center Configuration Manager (Configuration Manager) 中的应用配置策略来分发用户在 Android for Work 设备上运行应用时可能需要的设置。 Android 应用配置政策仅适用于运行 Android for Work 的设备，并可从 Play for Work 商店应用到已批准应用。

### <a name="try-it-out"></a>试试看                 

在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用配置策略”，然后选择“创建应用配置策略”。 在向导的“常规”页中，现在你可以“选择配置策略类型”。 指定应用配置策略所针对的平台：**适用于Android for Work 应用的配置策略**。 然后，你可以**指定名称和值对**或**浏览到属性列表 JSON 文件**。 新应配置策略显示在“软件库”工作区的“应用配置策略”节点中。 若要将应用配置策略与 Android for Work 应用的部署相关联，可按通常方式使用[部署应用程序](/sccm/apps/deploy-use/deploy-applications)主题中的过程来部署应用程序。

## <a name="hardware-inventory-collects-secure-boot-information"></a>硬件清单收集安全启动信息
硬件清单现在收集有关是否在客户端启用安全启动的信息。 该信息存储在 **SMS_Firmware** 类（在 1702 版本中引入）中，并在硬件清单中默认启用。 有关硬件清单的详细信息，请参阅[如何配置硬件清单](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

## <a name="add-child-task-sequences-to-a-task-sequence"></a>将子任务序列添加到任务序列
在此版本中，你可以添加一个运行其他任务序列的新任务序列步骤，该步骤在任务序列之间创建父/子关系。 这允许创建更多可重复使用的模块式任务序列。  

将子任务序列添加到任务序列时，请考虑以下事项：

- 父和子任务序列有效地组合成客户端运行的单个策略。
- 不支持添加作为其他任务序列父项的子任务序列。
- 该环境是全局环境。 例如，如果变量由父任务序列设置，然后由子任务序列更改，那么之后变量将保持更改。 类似地，如果子任务序列创建了一个新变量，那么该变量可用于父任务序列中的其余步骤。
- 对于单个任务序列操作，状态消息均按正常发送。
- 任务序列将条目写入 smsts.log 文件，包括在子任务序列启动时使其清晰明确的新日志条目。
- 在 Technical Preview for Configuration Manager（版本 1704）中，如果子任务序列引用任何程序包，并且你从软件中心运行父任务序列，则在运行子任务序列时，客户端将找不到程序包内容。 在这种情况下，必须从媒体（启动媒体、PXE 等）运行任务序列。  

    如果子任务序列使用“运行命令行”（无任何程序包引用）、“格式”“BitLocker”等步骤，则任务序列将可从软件中心成功运行。

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>将子任务序列添加到任务序列
1. 在任务序列编辑器中，单击“添加”，选择“常规”，然后单击“运行任务序列”。
2. 单击“浏览”，选择子任务序列。  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>重载当前的 Windows PE 版本的启动映像
当你在所选启动映像上运行“更新分发点”时，现在可以选择在启动映像中从 Windows ADK 安装目录重载最新版本的 Windows PE。 该向导的“常规”页提供有关安装在站点服务器上的 Windows ADK 版本、启动映像中使用 Windows PE 的 Windows ADK 版本以及 Configuration Manager 客户端版本的信息。 你可以使用此信息来帮助你决定是否重载启动映像。 此外，当你在“启动映像”节点中查看启动映像时，新列（**客户端版本**）已添加，这样你就了解每个启动映像使用的 Configuration Manager 客户端是哪个版本。

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>使用当前的 Windows PE 版本重载启动映像

1. 在 Configuration Manager 控制台中，转到“软件库” > “操作系统” > “启动映像”。
2. 选择“启动映像”，然后单击“更新分发点”。
3. 在向导的“常规”页面上，选择“使用当前版本的 Windows PE 从安装的 Windows ADK 重载启动映像”。

## <a name="improvements-to-operating-system-deployment"></a>对操作系统部署的改进
我们根据用户的语音反馈，对操作系统部署做了以下改进。

- 操作系统映像的[新**操作系统版本**列](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f)：我们添加了一个名为**操作系统版本**的新列，以便在“操作系统映像”和“操作系统升级包”节点中查看信息时显示映像的操作系统版本。 仅显示 WIM 中第一条索引的版本。 转到映像的“详细信息”选项卡，查看其他索引的操作系统版本。

- [更高效地登录 Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless)：从此版本开始，我们不再向 smsts.log 文件写入用于获取 CCM_CIVersionInfo.PolicyID 信息的条目。 此版本之前的版本可能包含很多带有此信息的条目，这使得在日志文件中查找相关度更高的信息非常困难。
