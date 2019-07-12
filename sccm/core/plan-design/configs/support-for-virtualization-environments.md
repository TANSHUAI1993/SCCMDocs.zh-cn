---
title: 支持虚拟化
titleSuffix: Configuration Manager
description: 在虚拟化环境中安装 Configuration Manager 客户端和站点系统角色的要求。
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 313f49804bb526d3a1e8d208b8efdc849d674e2e
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623368"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Configuration Manager 支持虚拟化环境

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 支持在受支持的操作系统上安装客户端和站点系统角色，这些操作系统在本文的虚拟化环境中作为虚拟机运行。 即使虚拟机主机（虚拟化环境）不被支持作为客户端或站点服务器，这种支持仍存在。  

例如，使用 Microsoft Hyper-V Server 2012 托管运行 Windows Server 2012 的虚拟机。 可以在运行 Windows Server 2012 的虚拟机上安装客户端或站点系统角色。 无法在运行 Microsoft Hyper-V Server 2012 的主机上安装客户端。  


## <a name="virtualization-environments"></a>虚拟化环境

- Windows Server 2019  
- Windows Server 2016<sup>[注 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016<sup>[注 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a> 注释 1：嵌套虚拟化
Configuration Manager 不支持[嵌套虚拟化](/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new)，这是 Windows Server 2016 的新增功能。


### <a name="virtualization-environment-support"></a>虚拟化环境支持

每台虚拟计算机都需要与物理 Configuration Manager 计算机相同或 更多的硬件和软件要求。  

若要验证 Configuration Manager 是否支持虚拟化环境，请使用服务器虚拟化验证计划。 其中包括联机的“虚拟化计划支持策略向导”。 有关详细信息，请参阅 [Windows 服务器虚拟化验证计划](https://www.windowsservercatalog.com/svvp.aspx)。  

> [!NOTE]  
> Configuration Manager 不支持在 Mac 计算机上运行的虚拟 PC 或虚拟服务器来宾操作系统。  

Configuration Manager 无法管理处于脱机状态的虚拟机。 既无法更新脱机虚拟机映像，也无法使用主计算机上的 Configuration Manager 客户端来收集清单。  

未提供虚拟机的特别注意事项。 例如，如果虚拟机停止并重启，但没有保存更新应用到的虚拟机的状态，Configuration Manager 可能无法确定是否需要将更新重新应用到虚拟机映像。  



##  <a name="bkmk_Azure"></a> Microsoft Azure 虚拟机  

Configuration Manager 可以在 Azure 中的虚拟机上运行，就像在数据中心内本地运行一样。 在以下方案中，请结合使用 Configuration Manager 与 Azure 虚拟机：  

- **方案 1**：在 Azure 虚拟机中运行 Configuration Manager。 使用它来管理其他 Azure 虚拟机上的客户端。  

- **方案 2**：在 Azure 虚拟机中运行 Configuration Manager。 使用它来管理不在 Azure 上运行的客户端。  

- **方案 3**：在 Azure 虚拟机中运行不同的 Configuration Manager 站点系统角色。 在本地数据中心内运行其他角色（已正确连接到 Azure）。  

如果相同的网络 Configuration Manager 要求、受支持的配置和硬件要求适用于在本地安装它，这些要求也适用于在 Azure 虚拟机中进行安装。  

有关详细信息，请参阅 [Azure 上的 Configuration Manager](/sccm/core/understand/configuration-manager-on-azure)。

> [!IMPORTANT]  
> Configuration Manager 站点和在 Azure 虚拟机中运行的客户端与本地安装遵循相同的许可证要求。  
