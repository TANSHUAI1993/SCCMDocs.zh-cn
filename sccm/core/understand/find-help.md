---
title: 查找帮助
titleSuffix: Configuration Manager
description: 查找有关 Configuration Manager 的其他信息的资源。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e767d46c81e3942efb44d9d94ba7f66ecd1f5281
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083124"
---
# <a name="find-help-for-using-configuration-manager"></a>查找使用 Configuration Manager 的帮助

适用范围：System Center Configuration Manager (Current Branch)

本文以下部分提供多种资源，可用于查找有关使用 Configuration Manager 的帮助：  

- [产品文档](#bkmk_Info)  

- [分享产品反馈](#product-feedback)  

- [关注 Configuration Manager 团队博客](#BKMK_ProductGroupBlog)  

- [支持选项和社区资源](#BKMK_SupportOptions)  

有关产品辅助功能的帮助，请参阅[辅助功能](/sccm/core/understand/accessibility-features)。  



##  <a name="bkmk_Info"></a> 产品文档  

若要访问最新的产品文档，请从[库索引](https://docs.microsoft.com/sccm/)开始。  

<a name="BKMK_SearchTips"></a>  

有关搜索、提供反馈的提示和使用产品文档的详细信息，请参阅[如何使用文档](/sccm/core/understand/use-docs)。  



<a name="product-feedback"></a>

## <a name="BKMK_1806Feedback"></a> 从 1806 版开始的产品反馈

从 Configuration Manager 1806 版开始，可直接从控制台发送产品反馈。 如果需要附加日志，请使用[反馈中心](#BKMK_FeedbackHub)。 可执行以下操作： <!--1357542-->

  - **发送笑脸**：就喜欢的内容发送反馈。
  - **发送哭脸**：就不喜欢的内容发送反馈。
  - **发送建议**：转到 [UserVoice 网站](https://configurationmanager.uservoice.com/)分享你的观点。

    ![在 Configuration Manager 1806 版中提交反馈](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>发送笑脸

若要就喜欢的内容发送反馈，请按照以下说明操作： 
1. 在控制台的右上角，单击笑脸。 
2. 在下拉菜单中，选择“发送笑脸”。
3. 使用文本框对喜欢的内容进行说明。 
4. 选择是否要分享电子邮件地址和屏幕截图。 
5. 单击“提交反馈”
     - 如果没有 Internet 连接，请单击底部的“保存”。 按照[发送为稍后提交而保存的反馈](#BKMK_NoInternet)部分中的说明，将其发送给 Microsoft。 

![在 Configuration Manager 1806 版中提交反馈表单](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>发送哭脸

若要就不喜欢的内容发送反馈，请按照以下说明操作：

1. 在控制台的右上角，单击笑脸。 
2. 在下拉菜单中，选择“发送哭脸”。
3. 使用文本框对不喜欢的内容进行说明。 
4. 选择是否要分享电子邮件地址和屏幕截图。 
5. 单击“提交反馈”
     - 如果没有 Internet 连接，请单击底部的“保存”。 按照[发送为稍后提交而保存的反馈](#BKMK_NoInternet)部分中的说明，将其发送给 Microsoft。  

### <a name="send-a-suggestion"></a>发送建议

发送建议时，将直接转到第三方网站 [UserVoice](https://configurationmanager.uservoice.com/) 来分享意见。 Configuration Manager 产品团队使用以下 UserVoice 状态值：

- **已注意** - 我们已了解该请求，它很有意义。 我们已将其添加到积压工作 (backlog)。
- **已计划** - 我们已开始编码此功能，并且希望它在接下来的数月内能够在技术预览版本中提供。
- **已启动** - 此功能现已在技术预览版中提供。 请查看该功能，并向我们提供反馈。 请告诉我们该功能是否可以正常运作。 请在原始请求的评论区中添加其他反馈，以便其他人可以查看并评论。 我们将阅读反馈，并利用其改进功能。
- **已完成** - 该功能的第一个版本已于生产版本中提供。 此状态并不意味着该功能已经 100% 完成且无需再改进。 但其确实意味着该功能的第一个版本已于生产版本中提供，并且可以开始真正使用。 我们将其标记为已完成是因为：
  - 我们希望你了解该功能已可用于生产。
  - 我们想要返还你的 UserVoice 投票，以便于你可以将其用于其他项。
  - 你可以申请对于此功能的新的设计更改请求，以帮助我们了解此功能的下一个最重要的改进。

### <a name="information-sent-with-feedback"></a>随反馈一起发送的信息

发送笑脸或发送哭脸时，以下信息将随反馈发送：
 
   - OS 内部版本信息
   - Configuration Manager 层次结构 ID
   - 产品内部版本信息
   - 语言信息
   - 设备标识符 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="BKMK_NoInternet"></a> 发送为稍后提交而保存的反馈

1. 单击“提供反馈”窗口底部的“保存”。 
2. 保存 .zip 文件。 如果本地计算机无法访问 Internet，请将文件复制到连接了 Internet 的计算机。 
3. 如果需要，复制位于 `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\` 的 UploadOfflineFeedback 文件夹
    - 有关 cd.latest 文件夹的详细信息，请参阅 [CD.Latest 文件夹](../servers/manage/the-cd.latest-folder.md)

4. 在连接了 Internet 的计算机上，打开命令提示符。 
5. 运行以下命令：`UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - 可选择指定以下参数：
        -  `-t, --timeout` 发送数据时的超时时间（以秒为单位）。 0 表示无限制。 默认值为 30。
        - `-s --silent` 不记录到控制台（不能与 --verbose 配合使用）
        - `-v, --verbose` 输出详细日志记录到控制台（不能与 --silent 配合使用）
        - `--help` 显示帮助屏幕

## <a name="bkmk_feedbackid"></a>控制台反馈确认

<!--3556010-->
从版本 1902 开始，通过 Configuration Manager 控制台或 UploadOfflineFeedback.exe 发送反馈时，将显示确认消息。 此消息包含反馈 ID，可将其作为跟踪标识符提供给 Microsoft。

- 若要复制反馈 ID，请选择 ID 旁边的复制图标，或使用 Ctrl + C 键盘快捷方式。
  - 此 ID 不会存储在计算机上，请确保在关闭窗口前先将其复制。
- 单击“不再显示此消息”将禁止显示对话框并阻止其将来出现。

   ![Configuration Manager 1902 控制台的反馈确认](media/1902-feedback-id-example.png)
- UploadOfflineFeedback 命令工具将 FeedbackID 写入控制台，除非使用 - s 或 --silent 。

  ![Configuration Manager 1902 控制台中的 UploadOfflineFeedback.exe 的反馈确认](media/1902-offline-feedback-id-example.png)

##  <a name="BKMK_FeedbackHub"></a> 1802 版及更早版本的产品反馈

通过 Windows 10 内置的[反馈中心应用](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)报告潜在的产品缺陷。 添加新的反馈时，请务必选择“企业管理”类别，然后选择下列子类别之一：
 - Configuration Manager 客户端
 - Configuration Manager 控制台
 - Configuration Manager 操作系统部署
 - Configuration Manager 服务器

继续使用 [UserVoice 页面](https://configurationmanager.uservoice.com/)为 Configuration Manager 中的新功能想法投票。 Configuration Manager 产品团队使用以下 UserVoice 状态值：

- **已注意** - 我们已了解该请求，它很有意义。 我们已将其添加到积压工作 (backlog)。
- **已计划** - 我们已开始编码此功能，并且希望它在接下来的数月内能够在技术预览版本中提供。
- **已启动** - 此功能现已在技术预览版中提供。 请查看该功能，并向我们提供反馈。 请告诉我们该功能是否可以正常运作。 请在原始请求的评论区中添加其他反馈，以便其他人可以查看并评论。 我们将阅读反馈，并利用其改进功能。
- **已完成** - 该功能的第一个版本已于生产版本中提供。 此状态并不意味着该功能已经 100% 完成且无需再改进。 但其确实意味着该功能的第一个版本已于生产版本中提供，并且可以开始真正使用。 我们将其标记为已完成是因为：
  - 我们希望你了解该功能已可用于生产。
  - 我们想要返还你的 UserVoice 投票，以便于你可以将其用于其他项。
  - 你可以申请对于此功能的新的设计更改请求，以帮助我们了解此功能的下一个最重要的改进。

##  <a name="BKMK_ProductGroupBlog"></a> Configuration Manager 团队博客  

Configuration Manager 工程和合作伙伴团队使用[企业移动性 + 安全性博客](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager)为用户提供有关 Configuration Manager 和相关技术的技术信息和其他新闻。 我们的博客文章补充了产品文档和支持信息。  


##  <a name="BKMK_SupportOptions"></a> 支持选项和社区资源  

下列链接提供有关支持选项和社区资源的信息：  

-   [Microsoft 支持](https://aka.ms/cmcbsupport)  

-   [Configuration Manager 社区：System Center Configuration Manager (Current Branch) 生存指南](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager 论坛页面](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
