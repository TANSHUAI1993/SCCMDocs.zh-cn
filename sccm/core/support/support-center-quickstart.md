---
title: 支持中心快速入门
titleSuffix: Configuration Manager
description: 快速捕获 Configuration Manager 客户端的状态用于进行故障排除。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f63193f9d4c9c754a56186f7a36cb9fabaf95725
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500736"
---
# <a name="support-center-quickstart-guide"></a>支持中心快速入门指南

适用范围：System Center Configuration Manager (Current Branch)

支持中心拥有强大的功能，包括故障排除和实时日志查看。 它还可用于在几分钟内捕获 Configuration Manager 客户端计算机的状态。 此功能包括访问远程客户端。

创建捕获客户端状态的完整*故障排除捆绑包*文件 (.zip)。 捆绑包不会仅包含日志文件。 它可以包含其他类型的数据，例如注册表设置和客户端配置。 向使用支持中心查看器的技术支持人员提供该捆绑包。



## <a name="prerequisites"></a>先决条件

- Configuration Manager 客户端的本地管理权限  

- 支持中心安装程序。 此文件位于 `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` 上的站点服务器中。 有关详细信息，请参阅[ - 安装](/sccm/core/support/support-center#install)。  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>步骤 1：在本地客户端上创建数据包

1.  在 Configuration Manager 客户端上安装支持中心。  

2.  转到“开始”菜单，在“Microsoft System Center”组中，选择“支持中心”。  

3.  在功能区的“主页”选项卡上，选择“收集选定数据”。 默认情况下，支持中心仅收集最小数据集：日志文件、客户端配置和操作系统。  

4.  将故障排除捆绑包文件 (.zip) 保存到计算机上的文件夹。 默认情况下，文件名类似以下示例：`Support_c885cdfed3c7482bba4f9e662978ec07.zip`。  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>步骤 2:使用支持中心查看器查看数据捆绑包

1.  启动“Support Center 查看器” 。 此操作可在安装支持中心的任何计算机上发生。  

2.  选择“打开捆绑包”，浏览到捆绑包文件，然后选择“打开”。  

3.  支持中心查看器处理文件后，切换到每个可用的选项卡。查看支持中心默认收集的数据类型：  

    - **配置**  

        - Configuration Manager 客户端配置  

        - 操作系统  

        - 计算机  

        - 服务  

        - 网络适配器  

    - **日志**：在列表中选择一个或多个条目，并选择“打开”。 此操作将在日志查看器中打开选定的日志文件。 使用此功能查找错误代码，并使用高级筛选器来帮助更快地分析日志文件。  



## <a name="collect-more-data"></a>收集更多数据

除了这些基本功能之外，Support Center 还可以收集各种其他客户端状态信息。 打开“支持中心”，然后选择“收集所有数据”。 此过程通常持续几分钟，即使在较新的计算机上也是如此。 支持中心会收集如下其他数据：

  - **策略**：Configuration Manager 策略设置，其中包含请求的策略配置和实际的策略配置  

  - **证书**：客户端证书的公钥信息。 支持中心不会收集证书私钥。  

  - **客户端注册表**：从注册表收集客户端配置信息。 支持中心只收集 Configuration Manager 注册表信息。  

  - **客户端 WMI**：来自 WMI 的客户端配置信息。 支持中心不会收集客户端策略。  

  - **故障排除**：对数据进行实时故障排除，以帮助诊断与 Active Directory、管理点、网络、策略分配和注册有关的常见客户端问题。  

  - **调试转储**：执行客户端和相关进程的调试转储。 调试转储可能会非常大。 仅当对客户端性能问题进行故障排除时才启用此选项。  

