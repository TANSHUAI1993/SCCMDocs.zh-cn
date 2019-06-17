---
title: 许可和分支
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 提供的安装选项的许可要求
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02c0839bf7587fa9ee1421bf7035e31a3ca59cd1
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748086"
---
# <a name="licensing-and-branches-for-system-center-configuration-manager"></a>System Center Configuration Manager 的许可和分支

适用范围：*System Center Configuration Manager (Current Branch) 和 (Long-Term Servicing Branch)*

通过本文了解 System Center Configuration Manager 提供的安装选项的许可要求。 这些安装选项包括下列分支：

- Current Branch
- Long-Term Servicing Branch (LTSB)
- Current Branch 的评估安装
- Technical Preview Branch

## <a name="licensing-overview"></a>许可概述

自 2016 年 10 月 1 日起，具有 System Center Configuration Manager 许可证上可用的软件保障 (SA) 或同等订阅权限的客户，有权使用 System Center Configuration Manager 的 2016 年 10 月发行的版本 1606。 自 2016 年 10 月 1 日起（含），具有 System Center Configuration Manager 权限的客户在安装时将会发现两个许可选项：Current Branch 和 Long Term Servicing Branch (LTSB)。

若要查看通过 Microsoft 批量许可计划购买的产品的完整条款和条件，请参阅[许可条款和文档](https://go.microsoft.com/fwlink/?LinkId=800052)。


## <a name="licensed-branches"></a>许可的分支

本文引用软件保障协议或等效订阅权限。 此 Microsoft 许可协议授予安装和使用 Configuration Manager 的权限。

### <a name="current-branch"></a>Current Branch

Current Branch 需要 Configuration Manager 的可用的软件保障协议或等效权限。 有关详细信息，请参阅[软件保障和 Current Branch](#software-assurance-and-the-current-branch)。

支持在希望接收来自 Microsoft 的定期质量和功能更新的生产环境中使用此分支。 它提供使用所有功能和改进的访问权限。

从 1710 版本开始，对于每个更新版本，支持器仍为自通用版本发布日期起 18 个月。 有关详细信息，请参阅[对 System Center Configuration Manager Current Branch 版本的支持](/sccm/core/servers/manage/current-branch-versions-supported)。

### <a name="long-term-servicing-branch-ltsb"></a>Long-Term Servicing Branch (LTSB)

自 2016 年 10 月 1 日起，LTSB 需要具有与 Microsoft 签订的最新软件保障协议。 有关详细信息，请参阅[软件保障和 LTSB](#software-assurance-and-the-ltsb)。

支持在生产环境中使用此分支。 它适用于 Configuration Manager 的软件保障 (SA) 或等效订阅权限于 2016 年 10 月 1 日后过期的客户。 与 Current Branch 相比，此分支有所限制。

对于此分支，提供 Configuration Manager 的关键安全更新，但不提供新功能。

### <a name="evaluation-installation-of-the-current-branch"></a>Current Branch 的评估安装

评估版本不需要与 Microsoft 签订软件保障协议。 [评估安装](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection)始终是 Current Branch，使用期限为 180 天。

可将评估安装升级到 Current Branch 的完整安装。 不能将评估安装升级到 Long-Term Servicing Branch。

### <a name="technical-preview-branch"></a>Technical Preview Branch

也可以使用 [Technical Preview Branch](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview)。 此分支是用于试用新功能的 Configuration Manager 受限版本。 使用不同于许可版本的介质安装 Technical Preview。 有关详细信息，请参阅 [Technical Preview](/sccm/core/get-started/technical-preview)。


## <a name="software-assurance-agreements"></a>软件保障协议

自 2016 年 10 月 1 日起（包含当日），System Center Configuration Manager 许可证上的软件保障或等效订阅权限的状态决定可安装和使用的分支。

### <a name="software-assurance-and-the-current-branch"></a>软件保障和 Current Branch

Configuration Manager Current Branch 的使用权限可以由以下提供：

- **System Center：** 如果客户具有 System Center Standard 上的可用 SA 或数据中心许可证，则可安装和使用 Configuration Manager 的 Current Branch 选项。

- **System Center Configuration Manager：** 如果客户具有 System Center Configuration Manager 许可证上的可用 SA 或等效订阅权限，则可安装和使用 Configuration Manager 的 Current Branch 选项。

自 2016 年 10 月 1 日起（含），如果具有 System Center Configuration Manager 许可证上的可用 SA 或等效订阅权限：

- 可以安装并使用 Current Branch。
- 如果允许 SA 或订阅失效，必须卸载 Current Branch。

### <a name="software-assurance-and-the-ltsb"></a>软件保障和 LTSB

自 2016 年 10 月 1 日起（含），如果具有 System Center Configuration Manager 许可证上的可用 SA 或等效订阅权限：

- 可以安装并使用 LTSB。 如果客户对 System Center Configuration Manager 具有永久权限或者允许 SA 或订阅失效，则其可在失效时安装当前的 Configuration Manager LTSB 版本。

LTSB 以 Current Branch 1606 版为基础，具有以下限制：

- 不支持将 Current Branch 转换为 LTSB。 如果当前拥有 Current Branch 站点，必须将 LTSB 作为新站点安装。  

- LTSB 并非支持 Current Branch 的每一项功能。 有关详细信息，请参阅 [Long-Term Servicing Branch 简介](introduction-to-the-ltsb.md)。 这些限制包括有限的功能集、有限的升级选项和单独的产品支持生命周期。  

### <a name="software-assurance-expiration-date"></a>软件保障到期日期

从 2016 年 10 月发布的 Configuration Manager 的 1606 版基线介质开始，可以指定软件保障协议的到期日期。 “软件保障到期日期”是用作方便的提醒日期的可选值。  请在运行 Configuration Manager 安装时添加它，或稍后从 Configuration Manager 控制台添加。

> [!NOTE]
> Microsoft 不会验证指定的到期日期，且不使用此日期验证许可证。 请将该日期用作到期日期提醒。 当 Configuration Manager 定期检查在线提供的新软件更新时，此值将发挥作用。 软件保障许可证状态应该处于最新状态，以便有资格使用这些额外的更新。

#### <a name="to-specify-the-software-assurance-expiration-date"></a>指定软件保障到期日期

- 通过 Configuration Manager 介质运行安装程序时，可在安装向导的“产品密钥”  页指定该值。

- 在 Configuration Manager 控制台的“层次结构设置”  的“许可”  选项卡上指定此值。


## <a name="licensing-resources"></a>许可资源

请参阅以下资源，了解更多有关产品许可的详细信息。

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft 批量许可服务中心 (VLSC)

- [VLSC 概述](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Microsoft 批量许可产品条款](https://go.microsoft.com/fwlink/?LinkId=800052)

- 批量许可证客户可以从此处获得许可证摘要：[批量许可证服务中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx)。 转到“许可证”菜单，选择“许可证摘要”。  

### <a name="vlsc-videos"></a>VLSC 视频

- 请转到 [Microsoft 批量许可服务中心培训和资源](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources)，选择“操作方法视频”，观看关于 VLSC 如何工作的培训视频。 

- [在何处查看可用的软件保障协议](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0)（从 43 秒开始）  

- [如何获取 VLSC 的权限](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4)。 可以将 VLSC 读取和写入权限委派给组织中的其他人。
