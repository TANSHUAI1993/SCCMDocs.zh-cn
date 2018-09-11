---
title: 错误消息
titleSuffix: Configuration Manager
description: 了解包转换管理器中的错误消息。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 62c4453cc383fa14eebf6e66c2582b878aaebae2
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297184"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>包转换管理器错误消息的技术参考

*适用范围：System Center Configuration Manager (Current Branch)*

<!--1357861-->

本文介绍包转换管理器将显示的错误消息。 它还包括可能的错误原因和更正错误的方法。 包转换管理器在 PCMTrace.log 中记录错误消息。 有关详细信息，包括如何控制详细级别，请参阅[日志文件](/sccm/apps/pcm/troubleshoot-pcm#log-files)。


#### <a name="application-creation-failed-with-the-following-exception"></a>应用程序创建失败，出现以下异常

在向 Configuration Manager 服务器提交应用程序对象期间出现指定的异常。

检查你在 Configuration Manager 中的权限并验证连接情况，然后重试。 如果这些操作没有解决问题，请检查 PCMtrace.log 文件（详细级别 4）和 SMSProv.log。


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>转换错误 – 适用于包转换状态

在包转换过程中出现了一般异常。 查看 PCMtrace.log 日志文件（详细级别 4）。

检查网络共享（包数据源）的用户权限，验证连情况，然后重试。 如果这些操作没有解决问题，请检查 PCMtrace.log 文件（详细级别 4）。


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>未在工作流输出中找到转换后的包及其生成的应用程序
应用程序（转换后的包/程序）已删除。

修改从属包/程序以确保从属包/程序存在。


#### <a name="objects-were-not-created-successfully"></a>对象未成功创建
有几种可能的原因。

检查你在 Configuration Manager 中的权限并验证连接情况，然后重试。 如果这些操作没有解决问题，请检查 PCMtrace.log 文件（详细级别 4）和 SMSProv.log 文件。


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>请关闭该向导并解决所选包的任何问题。 有关详细详细信息，请参阅 PCMTrace.Log
有几种可能的原因。

检查你在 Configuration Manager 中的权限并验证连接情况，然后重试。 如果这些操作没有解决问题，请检查 PCMtrace.log 文件（详细级别 4）和 SMSProv.log 文件。


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>某些部署类型缺少检测方法。 所有部署类型都必须具有检测方法
程序中缺少检测方法。

在“修复并转换”进程期间添加一个或多个检测方法。


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>准备包以进行转换时出现错误
有几种可能的原因。

检查你在 Configuration Manager 中的权限并验证连接情况，然后重试。 如果这些操作没有解决问题，请检查 PCMtrace.log 文件（详细级别 4）和 SMSProv.log 文件。


