---
title: 如何使用文档
titleSuffix: Configuration Manager
description: 了解关于使用 Configuration Manager 技术文档库的技巧。
ms.date: 06/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 085f91bfb99bcfabbcdee8083fb3a3089a33057e
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285667"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>如何使用 Configuration Manager 文档

适用范围：*System Center Configuration Manager (Current Branch)*

本文分为以下几个部分提供了有关使用 Configuration Manager 文档库的多个资源和技巧：  

- [如何搜索](#bkmk_searchtips)  

- [提交文档的 bug、增强功能、问题和新想法](#bkmk_docfeedback)  

- [如何获取更改通知](#bkmk_notifications)  

- [如何参与编辑文档](#bkmk_contribute)  


有关产品的常规帮助，请参阅[查找帮助](/sccm/core/understand/find-help)。


##  <a name="bkmk_searchtips"></a> 搜索   
 使用下列搜索提示来帮助你查找所需信息：  

-   在使用首选搜索引擎查找 Configuration Manager 的内容时，请同时使用 `SCCM` 和搜索关键字。  

    - 请从 docs.microsoft.com 查找 Configuration Manager Current Branch 结果。 Technet.microsoft.com 或 msdn.microsoft.com 用于搜索较早产品版本的结果。  

    - 若要进一步将搜索结果集中到当前内容库，请包含 `site:docs.microsoft.com` 以限定搜索引擎的范围。  

-   使用和用户界面以及在线文档中的术语相匹配的搜索词。 避免使用可能在社区内容中见过的非正式术语或缩写。 例如，搜索“management point”（管理点）而不是“MP”、搜索“deployment type”（部署类型）而不是“DT”，以及搜索“software updates”（软件更新）而不是“SUM”。  

-   若要在当前正在查看的文章中进行搜索，请使用浏览器的“查找”功能  。 对于大多数新式 Web 浏览器，请按 Ctrl+F，然后输入搜索词   。  

-   Docs.microsoft.com 上的每篇文章都包括以下字段以帮助搜索内容：  

    - 右上角的“搜索”  。 若要在所有文章中进行搜索，请在这里输入搜索词。 Configuration Manager 库中的文章自动包括“ConfigMgr”作用域。  

    - 左侧目录上方的“按标题筛选”  。 若要对当前目录进行搜索，请在此字段中输入搜索词。 此字段仅匹配出现在当前节点的文章标题中的搜索词。 例如，核心基础结构或应用程序管理。  

- 查找时遇到问题？ [提供反馈！](#bkmk_docfeedback) 提出问题时，请提供使用的搜索引擎、尝试搜索的关键字以及目标文章。 此反馈有助于 Microsoft 优化内容以实现更好的搜索。  

> [!TIP] 
> 从 Configuration Manager 版本 1902 起，新“社区”工作区包含“文档”节点。   此节点包含有关 Configuration Manager 文档和支持文章的最新信息。 有关详细信息，请参阅[使用 Configuration Manager 控制台](/sccm/core/servers/manage/admin-console#bkmk_doc-dashboard)

## <a name="bkmk_docfeedback"></a> 反馈

单击任意文章右上方的“反馈”链接，转到底部的“反馈”部分  。 此部分与 GitHub 问题相集成。 有关与 GitHub 问题集成的详细信息，请参阅[文档平台博客文章](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs)。

若要共享有关 Configuration Manager 产品本身的反馈，请单击“产品反馈”  。 有关详细信息，请参阅[产品反馈](/sccm/core/understand/find-help#product-feedback)。 

[GitHub 帐户](https://github.com/join)是提供文档反馈的先决条件。 用户登录后，会获得 MicrosoftDocs 的一次性授权。 然后，单击“内容反馈”  输入标题和评论，再单击“提交反馈”  。 此操作可为 [SCCMdocs 存储库](https://github.com/MicrosoftDocs/SCCMdocs/issues)中的目标文章提出一个新问题。

此集成还显示目标文章的任何现有未解决的问题或已关闭的问题。 如果存在任何此类问题，请在提交新问题之前先查看这些问题。 如果发现相关问题，请单击人脸图标以添加回应，或者可展开添加评论。 

#### <a name="types-of-feedback"></a>反馈类型
使用 GitHub 问题提交以下反馈类型：
- 文档 bug：内容过期、不清楚、令人混淆或不完整。
- 文档增强功能：改善文章的建议。
- 文档问题：需要帮助查找现有文档。
- 文档想法：撰写新文章的建议。 使用此方法代替 UserVoice 提供文档反馈。
- 称赞：关于有用或信息性文章的积极反馈！
- 本地化：关于内容翻译的反馈。
- 搜索引擎优化 (SEO)：关于搜索内容时所遇到的问题的反馈。 在评论中包含搜索引擎、关键字和目标文章。

如果针对非文档相关主题提出问题，例如[产品反馈](/sccm/core/understand/find-help#product-feedback)、[产品问题](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)或[支持请求](https://aka.ms/cmcbsupport)，则这些问题将被关闭，用户重定向到正确的反馈通道。

若要共享有关 docs.microsoft.com 平台的反馈，请参阅[文档反馈](https://aka.ms/sitefeedback)。 该平台包含所有包装组件，如标题、目录和右侧菜单。 以及文章在浏览器中的呈现方式，如字体、警报框和页面书签。



## <a name="bkmk_notifications"></a> 通知

若要在文档库中的内容更改时接收通知，请使用以下步骤：

1. 使用[文档搜索](https://docs.microsoft.com/search/index?scope=ConfigMgr)查找一篇文章或一组文章。 例如：
    - 按标题搜索一篇文章：[“故障排除的日志文件 - Configuration Manager”](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)
    - 搜索有关 [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr) 的任何文章
2. 在右上角单击“RSS”链接  。 
3. 任何搜索结果更改时，在任何 RSS 应用程序中使用此信息提要接收通知。


> [!Tip]  
> 也可在 GitHub 上监视 [SCCMdocs 存储库](https://github.com/MicrosoftDocs/SCCMdocs)  。 此方法会生成大量通知。 但其中不包括 Microsoft 使用的专用存储库中的更改。  



## <a name="bkmk_contribute"></a> 参与

与 docs.microsoft.com 上的大多数内容一样，Configuration Manager 文档库在 GitHub 上也是使用开放源代码编写的。 此库接受并鼓励社区参与。 有关如何参与的详细信息，请参阅[参与者指南](https://docs.microsoft.com/contribute)。 创建一个 [GitHub 帐户](https://github.com/join)是唯一的先决条件。

#### <a name="basic-steps-to-contribute-to-sccmdocs"></a>参与编辑 SCCM 文档的基本步骤
1. 从目标文章中，单击“编辑”  。 此操作可在 GitHub 中打开源文件。  

2. 若要编辑源文件，请单击铅笔图标。  

3. 在 Markdown 源中进行更改。 有关详细信息，请参阅 [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/how-to-write-use-markdown)（如何使用 Markdown 编写文档）。  

4. 在“建议文件更改”部分中，输入描述已更改内容的公开提交评论  。 然后单击“建议文件更改”  。  

5. 向下滚动然后验证所做的更改。 单击“创建拉取请求”以打开窗体  。 描述进行此更改的原因  。 标记文章作者并请求他们查看。 单击“创建拉取请求”  。  


### <a name="what-to-contribute"></a>要参与的内容

如果有兴趣参与但不知道从何处着手，请参阅以下建议：  

- 搜索针对社区的标签的问题列表：  
  - [精选问题](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)   
  - [需要帮助](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Microsoft 作者会将这些标签分配给适用于社区贡献的候选问题。  

- 查看文章以确保准确性。 然后使用 `mm/dd/yyyy` 格式更新 ms.date 元数据  。 此贡献有助于内容保持最新状态。  

- 根据经验添加说明、示例或指导。 此贡献借助社区的力量共享知识。   

- 以非英语语言更正翻译。 此贡献可提高本地化内容的可用性。  

> [!Note]  
> 如果你不是 Microsoft 员工，那么对于较大的贡献，需要签署贡献许可协议 (CLA)。 当贡献达到阈值，GitHub 会自动要求你签署此协议。  


### <a name="tips"></a>提示

贡献 Configuration Manager 文档时，请遵循以下通用准则：

- 不要使用大型拉取请求来制造惊喜。 相反，请[提出问题](https://docs.microsoft.com/sccm/core/understand/use-docs#bkmk_docfeedback)并开始讨论。 然后，在你投入大量时间之前，我们会就某个方向表示同意。  

- 阅读 [Microsoft 风格指南](https://aka.ms/MicrosoftStyle)。 了解[有关 Microsoft 风格和语态的前 10 个提示](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)。  

- 使用[拉取请求模板](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md)作为工作的起始点。  

- 请按照 [GitHub 流工作流](https://guides.github.com/introduction/flow/)操作。  

- 会经常推出有关你发布内容的博客和推文（或任何内容）！  

（此列表借用自 [.NET 参与指南](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts)。）
