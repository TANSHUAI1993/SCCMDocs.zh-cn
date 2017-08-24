---
title: "辅助功能 | Microsoft Docs"
description: "了解使 System Center Configuration Manager 可供残疾人使用的功能。"
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: ca518796477dda149a9f4c0ebd65f0a082eab806
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的辅助功能

*适用范围：System Center Configuration Manager (Current Branch)*


System Center Configuration Manager 包含可供残疾人使用的功能。


## <a name="bkmk_aconsole"></a>Configuration Manager 控制台的辅助功能  

**版本 1706 及更高版本的快捷方式和改进**

|键盘快捷方式|  目的|
|--------|--------|  
|Ctrl + M|将焦点设置在主（中心）窗格中。|
|Ctrl + T|将焦点设置到导航窗格中的顶级节点。 如果焦点已在此窗格中，则将焦点设置到你访问的最后一个节点。|
|Ctrl + I|将焦点设置到功能区下方的痕迹导航栏中。|
|Ctrl + L|将焦点设置到“搜索”字段中（可用时）。|
|Ctrl + D|将焦点设置到细节窗格中（可用时）。|
|Alt     |将焦点移入和移出功能区。|


- 改进了在导航窗格键入节点名称字母时的导航。
- 现在，通过主视图和功能区的键盘导航为圆形。
- 现在详细信息窗格中的键盘导航为圆形。 要返回到上一个对象或窗格，使用 Ctrl + D，然后按住 Shift + TAB 即可实现。
- 在刷新工作区视图后，焦点将设置到该工作区的主窗格中。
- 修复了一个问题，可使屏幕阅读器公布列表项的名称。
- 为页面上的多个控件添加了可访问名称，使得屏幕阅读器可以公布重要信息。


**以下快捷方式在所有版本中可用**

- 要访问工作区，请使用以下键盘快捷方式：  

|键盘快捷方式| 工作区|
|--------|--------|  
|Ctrl + 1| 资产和符合性|
|Ctrl + 2|  软件库|
|Ctrl + 3|  监视|
|Ctrl + 4|  管理|


-   要访问工作区菜单，请选择 Tab 键，直到焦点位于“展开/折叠”图标上为止。 然后，选择向下箭头键以访问工作区菜单。  

-   要在工作区菜单中导航，请使用箭头键。  

-   要访问工作区中的其他区域，请使用 Tab 键和 Shift+Tab 键。 要在工作区区域（如功能区）内导航，请使用箭头键。  

-   当焦点在树节点中时，若要访问地址栏，请使用 3 次 Shift+Tab。  

-   在向导或属性页上，可以使用键盘快捷方式在方框之间移动。 按住 Alt 键的同时按下划线字符 (Alt+_) 可以选择特定框。     

-  若要导航到工作区的不同节点，需输入节点名称的第一个字母。 每次按键都会将光标移动到以该字母开头的下一节点。 如果使用屏幕阅读器，阅读器会读出该节点的名称。

> [!NOTE]  
>  本节中的信息可能仅适用于在美国获得 Microsoft 产品许可的用户。 如果在美国以外的国家/地区获得本产品，可以使用软件包附带的子公司信息卡或访问 [Microsoft 辅助功能网站](http://go.microsoft.com/fwlink/?LinkId=8431)，获取 Microsoft 支持服务的联系信息。 可与你所在地的子公司联系，了解本节中描述的产品和服务的类型在你所在地区是否可用。 辅助功能的相关信息具有其他语言（包括日语和法语）版本。  

##  <a name="bkmk_ahelp"></a>Configuration Manager 帮助的辅助功能  
 Configuration Manager 帮助中包括的功能适用于范围更广的用户（包括行动不便和低视力用户，或其他残障人士）。  

|若要执行此操作|使用此键盘快捷方式|  
|----------------|--------------------------------|  
|显示“帮助”窗口。|F1|  
|在帮助主题窗格与导航窗格（“内容” 、“搜索” 和“索引”  选项卡）之间移动光标。|F6|  
|在导航窗格中的选项卡（例如，“内容”、“搜索”和“索引”）之间切换。|Alt + 选项卡的带下划线的字母|  
|选择下一个隐藏的文本或超链接。|选项卡|  
|选择上一个隐藏的文本或超链接。|Shift+Tab|  
|为所选的“全部显示”、“全部隐藏”、隐藏文本或超链接执行操作。|Enter|  
|显示“选项”  菜单以访问任何帮助工具栏命令。|Alt+O|  
|隐藏或显示包含“内容”、“搜索”和“索引”选项卡的窗格。|Alt+O，再按 T|  
|显示以前查看过的主题。|Alt+O，再按 B|  
|显示以前显示的主题序列中的下一主题。|Alt+O，再按 F|  
|返回指定的主页。|Alt+O，再按 H|  
|阻止“帮助”窗口打开帮助主题，例如阻止网页下载。|Alt + O，再按 S|  
|打开 Windows Internet Explorer 的“Internet 选项”  对话框，您可以在其中更改辅助功能设置。|Alt+O，再按 I|  
|刷新主题，例如链接的网页。|Alt+O，再按 R|  
|打印书中的所有主题或仅打印选定的主题。|Alt+O，再按 P|  
|关闭“帮助”窗口。|Alt+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>更改帮助主题的外观  

1.  若要准备自定义“帮助”中的颜色、字形和字号，请打开“帮助”窗口。  

2.  选择“选项”，然后选择“Internet 选项”。  

3.  在“常规”选项卡上，选择“辅助功能”。 选择“不使用网页中指定的颜色”、“不使用网页中指定的字体样式”和“不使用网页中指定的字体大小”。 也可以选择使用在你自己的样式表中指定的设置。  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>更改“帮助”中的背景或文本的颜色  

1.  打开“帮助”窗口。  

2.  选择“选项”，然后选择“Internet 选项”。  

3.  在“常规”选项卡上，选择“辅助功能”。 然后，选择“不使用网页中指定的颜色”。 也可以选择使用在你自己的样式表中指定的设置。  

4.  要自定义帮助中使用的颜色，请在“常规”选项卡上选择“颜色”。 取消选中“使用 Windows 颜色”框，然后选择要使用的字体颜色和背景颜色。  

    > [!NOTE]  
    >  如果在“帮助”窗口中更改帮助主题的背景颜色，则更改还会影响 Windows Internet Explorer 中的网页的背景颜色。  

#### <a name="to-change-the-font-in-help"></a>更改“帮助”中的字体  

1.  打开“帮助”窗口。  

2.  选择“选项”，然后选择“Internet 选项”。  

3.  在“常规”选项卡上，选择“辅助功能”。 要使用与 Windows Internet Explorer 实例中使用的设置相同的设置，请选择“不使用网页中指定的字体样式”和“不使用网页中指定的字体大小”。 也可以选择使用在你自己的样式表中指定的设置。  

4.  要自定义“帮助”中使用的字形，请在“常规”选项卡上选择“字体”，然后选择所需的字形。  

    > [!NOTE]  
    >  如果在“帮助”窗口中更改帮助主题的字体，则更改还会影响 Windows Internet Explorer 中的网页的字体。  
