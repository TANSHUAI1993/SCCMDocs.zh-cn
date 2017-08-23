---
title: "虛擬化的支援 | Microsoft Docs"
description: "取得在虛擬化環境中安裝 System Center Configuration Manager 用戶端和站台系統角色的需求。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b49bd179da850cee35b2487a353bb1788df03d58
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>System Center Configuration Manager 的虛擬化環境支援

適用於：System Center Configuration Manager (最新分支)

Configuration Manager 支援在支援的作業系統上安裝用戶端和站台系統角色，且這些作業系統是在本文所列的虛擬化環境中執行作為虛擬機器。 這項支援即使是在虛擬機器主機 (虛擬化環境) 不支援做為用戶端或站台伺服器的情況下都存在。  

 例如，如果您使用 Microsoft Hyper-V Server 2012 來裝載虛擬機器，而該虛擬機器執行 Windows Server 2012，則您可以在虛擬機器 (Windows Server 2012) 上安裝用戶端或站台系統角色，但不能在主機 (Microsoft Hyper-V Server 2012) 上安裝。  

|虛擬化環境|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(請參閱附註 1)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(請參閱附註 1)|
-  附註 1：Configuration Manager 不支援[巢狀虛擬化](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new)，這是 Windows Server 2016 的新功能。


 您使用的每部虛擬電腦都必須滿足或超過用於實體 Configuration Manager 電腦的相同硬體和軟體需求。  

 您可以驗證您的虛擬化環境受到 Configuration Manager 支援，方法是使用伺服器虛擬化驗證方案和其線上虛擬化方案支援原則精靈。 如需伺服器虛擬化驗證方案的詳細資訊，請參閱 [Windows 伺服器虛擬化驗證方案](https://www.windowsservercatalog.com/svvp.aspx)。  

> [!NOTE]  
>  Configuration Manager 不支援在 Mac 電腦上執行的虛擬電腦或虛擬伺服器客體作業系統。  

除非虛擬機器處於線上狀態，否則 Configuration Manager 無法管理虛擬機器。 無法更新離線虛擬機器映像，也無法在主機電腦上使用 Configuration Manager 用戶端收集清查。  

虛擬機器沒有特殊的考量。 例如，如果虛擬機器已停止並重新啟動，而未儲存已套用更新之虛擬機器的狀態，Configuration Manager 可能無法判斷更新是否要重新套用至虛擬機器映像。  

##  <a name="bkmk_Azure"></a> Microsoft Azure 虛擬機器  
 Configuration Manager 可以在 Azure 虛擬機器上執行，就像在實體公司網路中內部部署執行一樣。 您可以在下列案例中，搭配使用 Configuration Manager 與 Azure 虛擬機器：  

-   **案例 1：**您可以在 Azure 虛擬機器上執行 Configuration Manager，並用它來管理安裝在其他 Azure 虛擬機器上的用戶端。  

-   **案例 2：**您可以在 Azure 虛擬機器上執行 Configuration Manager，並用它來管理未在 Azure 上執行的用戶端。  

-   **案例 3：**您可以一方面在 Azure 虛擬機器上執行不同的 Configuration Manager 站台系統角色，一方面在您的實體公司網路 (具備用於通訊的適當網路連線) 上執行其他角色。  

適用於在您的實體公司網路上內部部署安裝 Configuration Manager 的相同網路、支援的設定和硬體 System Center Configuration Manager 需求，也適用於在 Azure 虛擬機器上安裝。  

如需詳細資訊，請參閱 [Azure 的 Configuration Manager - 常見問題集](/sccm/core/understand/configuration-manager-on-azure)。

> [!IMPORTANT]  
>  此外，在 Azure 虛擬機器上執行的 Configuration Manager 站台和用戶端受限於與內部部署安裝相同的授權需求。  
