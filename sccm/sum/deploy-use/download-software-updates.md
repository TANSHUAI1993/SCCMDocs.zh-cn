---
title: "下載軟體更新 - Configuration Manager | Microsoft Docs"
description: "使用 [下載軟體更新精靈] 下載軟體更新，並將它們發佈到發佈點，以準備好部署至用戶端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: de78e8d3-043f-4cd3-97e0-4dfb824fd3fb
ms.openlocfilehash: f38f72f9f547b82c92789f02975cbd0193b79b2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="download-software-updates"></a>下載軟體更新  

*適用於：System Center Configuration Manager (最新分支)*

您有幾種方式可以下載 Configuration Manager 中的軟體更新。 當您建立自動部署規則 (ADR)，或手動部署軟體更新時，軟體更新會下載到站台伺服器上的內容庫。 接著，軟體更新會複製到與設定之部署套件相關聯之發佈點上的內容庫。 如果您想要在部署之前下載軟體更新，可以使用「下載更新精靈」。 如此將可讓您在將軟體更新部署至用戶端電腦之前先確認軟體更新可以在發佈點上使用。  

> [!NOTE]  
>  如需監視內容狀態的相關資訊，請參閱 [Content status monitoring](../deploy-use/monitor-software-updates.md#BKMK_ContentStatus)。  

利用下列程序，藉由「下載軟體更新精靈」下載軟體更新。  

#### <a name="to-download-software-updates"></a>下載軟體更新  
[!INCLUDE[下載更新](..\includes\downloadupdates.md)]
<!---
1.  In the Configuration Manager console, navigate to **Software Library** > **Software Updates**.  

3.  Choose the software update to download by using one of the following methods:  

    -   Select one or more software update groups from **Software Update Groups**, and then, on the **Home** tab, in the **Update Group** group, click **Download**.  

    -   Select one or more software updates from **All Software Updates**, and then, on the **Home** tab, in the **Update** group, click **Download**.  

        > [!NOTE]  
        >  On the **All Software Updates** node, Configuration Manager displays only software updates with a **Critical** and **Security** classification that have been released in the last 30 days.  

        > [!TIP]  
        >  Click **Add Criteria** to filter the software updates that are displayed in the **All Software Updates** node, save search criteria that you often use, and then manage saved searches on the **Search** tab.  

         The **Download Software Updates Wizard** opens.  

4.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Choose this setting to select an existing deployment package for the software updates that are in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package will not be downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates that are in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. The package must have a unique name that briefly describes the package content.  It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files. Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

5.  On the **Distribution Points** page, specify the distribution points or distribution point groups that will host the software update files, and then click **Next**. For more information about distribution points, see [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  The Distribution Points page is available only when you create a new software update deployment package.  

6.  On the **Distribution Settings** page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Deployment packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

7.  On the **Download Location** page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

8.  On the **Language Selection** page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

9. On the **Summary** page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

10. On the **Completion** page, verify that the software updates were successfully downloaded, and then click **Close**.  --->
