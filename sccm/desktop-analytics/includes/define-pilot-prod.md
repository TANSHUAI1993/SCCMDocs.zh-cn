---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754705"
---
使用以下定义试点和生产环境之间进行区分：  

- **试点**：你想要验证之前先部署到更多的设备的子集。 使用 Desktop 分析将设备标记为唯一的试验组。 试运行中的设备已准备好升级时阻止所有资产。 阻塞的资产标记为*关键*并*无法*升级。  

- **生产**：所有其他设备注册到 Desktop 分析不在试验中。 生产型设备已准备好升级且注销所有资产时。 桌面分析自动对关闭任何非关键资产进行签名。  

