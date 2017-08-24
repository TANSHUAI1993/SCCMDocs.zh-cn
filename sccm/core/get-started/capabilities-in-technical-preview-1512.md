---
title: "Technical Preview 1512 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1512 版中的可用功能。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 5cf8d54fbaa98a75ac2a875a23a43b1d3e5be0dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1512-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1512 版中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview 1512 版中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。  

 以下是可以试用的此版本的新功能。  

##  <a name="bkmk_devicehealth"></a> 设备运行状况证明  
 从 Technical Preview 1512 开始，管理员可以在 Configuration Manager 中查看 Windows 10 设备运行状况证明的状态。  此功能适用于 Configuration Manager 和带 Microsoft Intune 的 Configuration Manager。 设备运行状况证明让管理员能够确保客户端计算机具有可信 BIOS、TPM 和启动软件配置。 为了支持设备运行状况证明，客户端设备必须运行 Win10 并启用 TPM 2。 设备运行状况证明显示为以下各项启用的设备数：  

-   开机初期启动的反恶意软件  

-   BitLocker  

-   安全启动  

-   代码完整性  

控制台还显示丢失最多的运行状况证明设置和设备数。  

若要预览设备运行状况证明视图，请在 Configuration Manager 中转到“监视”工作区，单击“安全”节点，然后单击“运行状况证明”。  

##  <a name="bkmk_viewterms"></a>条款和条件的控制台中监视  
从 Technical Preview 1512 开始，如果将 Configuration Manager 与 Microsoft Intune 集成，便可以使用 Configuration Manager 查看已接受和未接受你的 IT 部门所配置条款和条件的用户。  

**查看摘要信息：**  

-   在 Configuration Manager 控制台中，转到“监视” > “概述” > “部署”，然后选择要查看的条款和条件部署。  

**查看详细信息：**  

1.  在 Configuration Manager 控制台中，转到“资产和符合性” > “概述” > “符合性设置” > “条款和条件”，然后选择要查看的条款和条件。  

2.  在控制台底部，选择“部署”选项卡并选择部署，然后单击“查看状态”。  

##  <a name="bkmk_EPpolicy"></a>对 Endpoint Protection 策略设置的改进  
在 1512 Technical Preview 中，我们在 Endpoint Protection 反恶意软件策略中添加了以下新设置：  

-   实时保护：**在下载时和安装前阻止可能不需要的应用程序**  

    -   可能不需要的应用程序 (PUA) 是一种基于信誉和研究驱动的标识的威胁分类。 大多数情况下，它们是不需要的应用程序捆绑程序或其捆绑应用程序。  

    -   默认启用了保护策略设置（设置为“是”）。 启用后，此设置将在下载和安装时阻止 PUA。 但是，您可以排除特定文件或文件夹，以满足您的环境的特定需求。  

-   扫描设置：**在运行完全扫描时扫描映射的网络驱动器**  

    -   此设置可以提供更高的粒度，让管理员能够在按计划完全扫描的过程中允许按需扫描网络文件，从而规避始终扫描映射的网络驱动器的风险。  

    -   必须先启用“扫描网络文件”设置（“是”），才可对此设置进行配置。  

    -   默认情况下，此设置为“否”，表示完全扫描将不访问映射的网络驱动器。  

-   自动示例文件提交配置：  

     反恶意软件引擎可能会请求将文件示例发送到 Microsoft 供进一步分析。 默认情况下，发送此类示例之前将始终给出提示。 管理员现在可以管理以下设置以配置此行为：  

    -   高级：**启用自动示例文件提交以帮助 Microsoft 确定某些检测到的项是否为恶意项**：将此设置更改为“是”以启用自动示例文件提交。 默认情况下，此设置为“否”，这意味着禁用了自动示例文件提交，并且将在发送示例前提示用户。   （此设置是在 System Center 2012 R2 Configuration Manager SP1 中首次推出的）  

    -   高级：**允许用户修改自动示例文件提交设置**：此设置决定在设备上具有本地管理权限的用户可否在客户端界面中更改自动示例文件提交设置。 默认情况下，此设置为“否”，这意味着只能从 Configuration Manager 内更改设置，设备上的本地管理员不能更改此配置。  

         例如，下面显示了启用时由管理员设置的 Windows 10 中的 Windows Defender 设置，并且不允许用户对其进行修改：  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    此外，Endpoint Protection 反恶意软件政策的“排除设置”部分中的现有“排除文件和文件夹”设置已改进为允许设备排除。 例如，你现在可以将以下内容指定为排除项： **\device\mvfs** （适用于 Multiversion 文件系统）。 策略不会验证设备路径；将 Endpoint Protection 策略提供给客户端上必须能够解释设备字符串的反恶意软件引擎。  

**使用 Endpoint Protection 策略的先决条件：**  

必须先使用 Endpoint Protection 客户端设置安装并管理 Endpoint Protection 客户端，才能使用 Endpoint Protection 策略。 该操作使用适用于 Windows 7、Windows 8、Windows 8.1 的 System Center Endpoint Protection 客户端或适用于 Windows 10 的托管 Windows Defender 完成。 请参阅 [System Center Configuration Manager 中的 Endpoint Protection](../../protect/deploy-use/endpoint-protection.md)。  
