---
title: OneDrive for Business 配置文件
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中使用 OneDrive for Business 配置文件将 Windows 已知文件夹重定向到 OneDrive for Business。
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22fcc8704651d75b4123e7942d14b861b3f6c099
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802456"
---
# <a name="onedrive-for-business-profiles"></a>OneDrive for Business 配置文件

从 Configuration Manager 1902 版开始，可以创建 OneDrive for Business 配置文件用来将 Windows 已知文件夹移动到 OneDrive for Business。 这些文件夹包括桌面、文档和图片。 在每个配置文件中，可以指定用于移动 Windows 已知文件夹的设置。 有关 OneDrive for Business 的详细信息，请参阅[将 Windows 已知文件夹重定向并移动到 OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders)。 <!--3556021-->

## <a name="prerequisites"></a>先决条件

- [找到你的 Office 365 租户 ID](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- 部署 OneDrive 同步客户端版本 18.111.0603.0004 或更高版本。 有关详细信息，请参阅[使用 System Center Configuration Manager 部署 OneDrive 应用](https://docs.microsoft.com/onedrive/deploy-on-windows)。  

## <a name="bkmk_odfb"></a>将 Windows 已知文件夹移动到 OneDrive
<!--3556021-->
使用 Configuration Manager 将 Windows 已知文件夹移动到 OneDrive for Business。 这些文件夹包括桌面、文档和图片。 若要简化 Windows 10 升级过程，请先将这些设置部署到 Windows 7 客户端，然后部署任务序列。 

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“OneDrive for Business 配置文件”节点。  

   ![OneDrive for Business 配置文件节点](media/onedrive-for-business-profiles-node.png)
2. 在功能区中，选择“创建 OneDrive for Business 配置文件”。  

3. 指定一个名称以标识此策略，然后选择“下一步”。  

4. 选择要使用 OneDrive for Business 配置文件预配的平台。 选择平台后，单击“下一步”。

    ![选择 OneDrive for Business 配置文件的平台](media/onedrive-for-business-profile-select-platforms.png) 

5. 在“设置”页上：

    1. 指定你的 Office 365 租户 ID。  

    2. 选择以下选项之一将已知文件夹移动到 OneDrive：  

        - **提示用户将 Windows 已知文件夹移动到 OneDrive**：使用此选项，用户会看到一个用于移动其文件的向导。 如果用户选择推迟或拒绝移动其文件夹，则 OneDrive 将定期提醒他们。  

        - **以无提示方式将 Windows 已知文件夹移动到 OneDrive**：将此策略应用于设备时，OneDrive 客户端将自动将已知文件夹重定向到 OneDrive for Business。  

            - **重定向文件夹后向用户显示通知**：如果启用此选项，OneDrive 客户端将在它移动用户的文件夹后通知用户。  

    3. **防止用户将其 Windows 已知文件夹重定向回其电脑**：在客户端上的 OneDrive for Business 中禁用让用户将这些文件夹移回设备的选项。  

       ![OneDrive for Business 的“已知文件夹移动”设置](media/onedrive-for-business-profile-move-folder-settings.png)

6. 完成向导，然后部署策略。  


## <a name="deploy-the-onedrive-for-business-profile"></a>部署 OneDrive for Business 配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“OneDrive for Business 配置文件”节点。  


2. 选择配置文件，然后选择功能区中的“部署”。

3. 为部署指定以下设置：

   1. **集合**：单击“浏览...”，然后选择要为其部署配置文件的集合。  
   1. **生成警报**：

      - **符合性低于**：要保持的客户端符合性的最小百分比时，则会生成警报。
      -  **日期和时间**：根据配置文件符合性首先开始生成日期警报。
      - **生成 System Center Operations Manager 警报**：向 System Center Operations Manager 发送符合性警报。
   1. **计划**：

      - **简单计划**：默认情况下，此设置使用简单的计划，每七天启动一次符合性评估。
      - **自定义计划**：定义何时运行符合性评估。 开始时间基于在创建计划时时运行 Configuration Manager 控制台的计算机的本地时间，也可以使用 UTC。
 
      ![部署 OneDrive for Business 配置文件](media/onedrive-for-business-deploy-profile.png)

4. 单击“确定”部署 OneDrive for Business 配置文件。


## <a name="next-steps"></a>后续步骤

[创建远程连接配置文件](/sccm/compliance/deploy-use/create-remote-connection-profiles)
