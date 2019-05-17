---
title: 管理 Office 365 ProPlus 更新
titleSuffix: Configuration Manager
description: Configuration Manager 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器，使更新可部署到客户端。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/11/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.collection: M365-identity-device-management
ms.openlocfilehash: 021fa2a29512fa3dde06af77093100f5c1dff0ad
ms.sourcegitcommit: ab9f2a7fb7ea3a0c65808fce2975ab25a670281f
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65613049"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus

*适用范围：System Center Configuration Manager (Current Branch)*

使用 Configuration Manager，可以通过下列方式管理 Office 365 专业增强版应用：

- [部署 Office 365 应用](#deploy-office-365-apps)：可从 [Office 365 客户端管理仪表板](/sccm/sum/deploy-use/office-365-dashboard)启动 Office 365 安装程序，使首次 Office 365 应用安装体验更简单。 该向导可让你配置 Office 365 安装设置、从 Office 内容分发网络 (CDN) 下载文件以及创建并部署脚本应用程序的内容。

- [部署 Office 365 更新](#deploy-office-365-updates)：可以使用软件更新管理工作流管理 Office 365 客户端更新。 当 Microsoft 将新的 Office 365 客户端更新发布到 Office 内容分发网络 (CDN) 时，Microsoft 还会将更新包发布到 Windows Server 更新服务 (WSUS)。 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器之后，更新可部署到客户端。    

- [添加 Office 365 更新下载的语言](#bkmk_o365_lang)：可以添加对 Configuration Manager 的支持，以下载 Office 365 支持的任意语言的更新。 这意味着只要 Office 365 支持，Configuration Manager 就可不必支持该语言。 在 Configuration Manager 版本 1610 之前，必须使用 Office 365 客户端上配置的语言下载和部署更新。

- [更改更新频道](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager)：可以使用组策略向 Office 365 客户端分发注册表项值更改，从而更改更新频道。

若要查看 Office 365 客户端信息并开始执行一些 Office 365 管理操作，请使用 [Office 365 客户端管理仪表板](/sccm/sum/deploy-use/office-365-dashboard)。

## <a name="deploy-office-365-apps"></a>部署 Office 365 应用  
从 Office 365 客户端管理仪表板启动 Office 365 安装程序，以执行首次 Office 365 应用安装。 该向导可让你配置 Office 365 安装设置、从 Office 内容分发网络 (CDN) 下载文件以及创建并部署文件的脚本应用程序。 在客户端上安装 Office 365 并运行 [Office自动更新任务](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus)之前，Office 365 更新不适用。 出于测试目的，可以手动运行更新任务。

对于旧版 Configuration Manager，必须按照以下步骤操作，才能在客户端上首次安装 Office 365 应用：
- 下载 Office 365 部署工具 (ODT)
- 下载 Office 365 安装源文件，包括需要的所有语言包。
- 生成 Configuration.xml，以指定正确的 Office 版本和频道。
- 创建和部署旧包或脚本应用，以便客户端可以安装 Office 365 应用。

### <a name="requirements"></a>要求
- 运行 Office 365 安装程序的计算机必须具有 Internet 访问权限。  
- 运行 Office 365 安装程序的用户必须对向导中提供的文件位置共享具有读取和写入权限。
- 如果收到 404 下载错误，将以下文件复制到用户的 %temp%文件夹中：
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>使用 Configuration Manager 版本 1806 或更高版本部署 Office 365 应用： 
从 Configuration Manager 1806 开始，Office 自定义工具在 Configuration Manager 控制台中已与 Office 365 安装程序集成。 在为 Office 365 创建部署时，可以动态配置最新的 Office 可管理性设置。 <!--1358149-->

1. 在 Configuration Manager 控制台中，导航到“软件库” > “概述” > “Office 365 客户端管理”。
2. 单击右上方窗格中的“Office 365 安装程序”。 将打开 Office 365 客户端安装向导。
3. 在“应用程序设置”页上，提供应用的名称和说明，输入文件的下载位置，然后单击“下一步”。 必须将位置指定为 &#92;&#92;server&#92;share。
4. 在“Office 设置”页上，单击“转到 Office 自定义工具”。 这将打开[即点即用 Office 自定义工具](https://config.office.com)。
5. 为 Office 365 安装配置所需的设置。 完成配置时，单击页面右上角的“提交”。 
6. 在“部署”页上，确定是希望立即部署还是稍后部署。 如果选择稍后部署，可以在“软件库” < “应用程序管理” < “应用程序”中找到应用程序。  
7. 在“摘要”页上，确认设置。 
8. 完成 Office 365 客户端安装向导后，单击“下一步”，然后单击“关闭”。 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>使用 Configuration Manager 版本 1802 或早期版本部署 Office 365 应用：

1. 在 Configuration Manager 控制台中，导航到“软件库” > “概述” > “Office 365 客户端管理”。
2. 单击右上方窗格中的“Office 365 安装程序”。 将打开 Office 365 客户端安装向导。
3. 在“应用程序设置”页上，提供应用的名称和说明，输入文件的下载位置，然后单击“下一步”。 必须将位置指定为 &#92;&#92;server&#92;share。
4. 在“导入客户端设置”页上，选择是从现有 XML 配置文件导入 Office 365 客户端设置还是手动指定设置。 完成后单击“下一步”。  

    如果具有现有的配置文件，请输入文件的位置并跳到步骤 7。 必须采用 \\server\share\filename.XML 形式指定位置。
    > [!IMPORTANT]    
    > XML 配置文件必须仅包含 [Office 365 ProPlus 客户端支持的语言](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016)。

5. 在“客户端产品”页上，请选择使用的 Office 365 套件。 选择想要包括的应用程序。 选择应包括的任何其他 Office 产品，然后单击“下一步”。
6. 在“客户端设置”页上，选择要包括的设置，然后单击“下一步”。
7. 在“部署”页上，选择是否部署该应用程序，然后单击“下一步”。 <br/>如果选择不部署向导中的包，请跳到步骤 9。
8. 像配置典型应用程序那样，配置该向导页的其余部分。 有关详细信息，请参阅[创建和部署应用程序](/sccm/apps/get-started/create-and-deploy-an-application)。
9. 完成向导。
10. 可以依次转到“软件库” > “概述” > “应用管理” > “应用”，部署或编辑应用。    

使用 Office 365 安装程序创建并部署 Office 365 应用程序后，默认情况下，Configuration Manager 不会管理 Office 更新。 若要允许 Office 365 客户端从 Configuration Manager 接收更新，请参阅[使用 Configuration Manager 部署 Office 365 更新](#deploy-office-365-updates)。

部署 Office 365 应用后，可以创建自动部署规则以维护该应用。 若要创建 Office 365 应用的自动部署规则，请单击 [Office 365 客户端管理仪表板](/sccm/sum/deploy-use/office-365-dashboard)中的“创建 ADR”。 选择产品时，请选择“Office 365 客户端”。 有关详细信息，请参阅[自动部署软件更新](/sccm/sum/deploy-use/automatically-deploy-software-updates)。


## <a name="deploy-office-365-updates"></a>部署 Office 365 更新

使用以下步骤通过 Configuration Manager 部署 Office 365 更新：

1. 在本文章的“使用 Configuration Manager 管理 Office 365 客户端更新的要求”部分，验证使用 Configuration Manager 管理 Office 365 客户端更新的[要求](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates)。  

2. [配置软件更新点](../get-started/configure-classifications-and-products.md)来同步 Office 365 客户端更新。 针对分类设置**更新**，并为产品选择 **Office 365 客户端**。 将软件更新点配置为使用“更新”分类后，同步软件更新。
3. 使 Office 365 客户端可以从 Configuration Manager 接收更新。 可使用 Configuration Manager 客户端设置或组策略启动客户端。

    **方法 1**：自 Configuration Manager 版本 1606 起，可使用 Configuration Manager 客户端设置来管理 Office 365 客户端代理。 配置此设置和部署 Office 365 更新后，Configuration Manager 客户端代理将与 Office 365 客户端代理通信，从分发点下载更新并进行安装。 Configuration Manager 盘点了 Office 365 ProPlus 客户端设置的步骤。    

      1. 在 Configuration Manager 控制台中，单击“管理” > “概述” > “客户端设置”。  

      2. 打开相应的设备设置以启用客户端代理。 有关默认客户端设置和自定义客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

      3. 单击“软件更新”，并针对“启用 Office 365 客户端代理的管理”设置选择“是”。  

    **方法 2**：使用 Office 部署工具或组策略从 Configuration Manager [启用 Office 365 客户端以接收更新](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient)。  

4. [将 Office 365 更新部署](deploy-software-updates.md)到客户端。

> [!Important]
> - 从 Configuration Manager 版本 1706 开始，Office 365 客户端更新已移至“Office 365 客户端管理” >“Office 365 更新”节点。 此移动不会影响当前 ADR 配置。 
> - 在 Configuration Manager 版本 1610 之前，必须使用 Office 365 客户端上配置的语言下载和部署更新。 例如，假设 Office 365 客户端上配置的语言为 en-us 和 de-de。 在站点服务器上，对适用的 Office 365 更新只下载并部署 en-us 内容。 当用户从软件中心开始安装此更新时，该更新会在下载 de-de 内容时挂起。 

> [!NOTE]  
>
> 如果最近安装了 Office 365 专业增强版，根据其安装方式，更新通道可能尚未设置。 在这种情况下，已部署的更新将被检测为不适用。 在安装 Office 365 专业增强版时，将会创建一个[计划的自动更新任务](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus)。 在这种情况下，此任务需要至少运行一次，以设置更新通道并使更新检测为适用。
>
> 如果最近安装了 Office 365 专业增强版且未检测已部署的更新，出于测试目的，可以手动启动 Office 自动更新任务，然后在客户端上启动[软件更新部署评估周期](https://docs.microsoft.com/sccm/sum/understand/software-updates-introduction#scan-for-software-updates-compliance-process)。 有关如何在任务序列中执行此操作的说明，请参阅[在任务序列中更新 Office 365 专业增强版](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#updating-office-365-ProPlus-in-a-task-sequence)。

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Office 365 更新的重启行为和客户端通知
将更新部署到 Office 365 客户端时，重启行为和客户端通知会存在差异，具体取决于 Configuration Manager 的版本。 下表提供了有关客户端收到 Office 365 更新时的最终用户体验的信息：

|Configuration Manager 版本 |最终用户体验|  
|----------------|---------------------|
|1706、1710|安装更新前，客户端收到弹出消息、应用内通知及倒计时对话框。|
|1802| 安装更新前，客户端收到弹出消息、应用内通知及倒计时对话框。 </br>如果强制执行 Office 365 客户端更新期间有任何 Office 365 应用程序正在运行，将不会强制关闭 Office 应用程序。 更新安装将改为返回要求系统重启 <!--510006-->|


> [!Important]
>
>在 Configuration Manager 版本 1706 中，请注意以下详细信息：
>
>- 对于截止时间在未来 48 小时内并已下载更新内容的必需应用，通知图标显示在任务栏的通知区域中。 
>- 对于截止时间在未来 7.5 小时内并已下载更新内容的必需应用，将显示倒计时对话框。 在达到截止时间前，用户可以将倒计时对话框推迟三次。 推迟后，倒计时会在两个小时后再次显示。 如果没有推迟，则会显示 30 分钟倒计时，且在倒计时到期时安装更新。
>- 用户单击通知区域中的图标前，不会显示弹出通知。 此外，如果通知区域已最小化，除非用户打开或展开通知区域，否则不能看到通知图标。 
>- 当用户未在设备上频繁执行操作时，可能启动通知和倒计时对话框。 例如，当设备整夜处于锁定状态时，设备上运行的 Office 应用可能被强制关闭以安装更新。 在关闭应用前，Office 将保存应用数据，防止数据丢失。 
>- 如果已过截止时间或配置为尽快开始，则可能会在没有通知的情况下强制关闭正在运行的 Office 应用。 
>- 如果用户在截止时间之前安装 Office 更新，Configuration Manager 会在达到截止时间时验证是否已安装更新。 如果在设备上未检测到更新，则会安装更新。 
>- 在下载更新之前，应用内通知栏不会显示于正在运行的 Office 应用中。 下载更新后，应用内通知仅为新打开的应用显示。
>- 对于由服务窗口触发的或安排在非营业时间的 Office 更新，则可能会在没有通知的情况下强制关闭正在运行的 Office 应用以安装更新。 
>- 有关详细信息，请参阅 [Office 365 的最终用户更新通知](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)


## <a name="bkmk_o365_lang"></a>添加 Office 365 更新下载语言
可以添加对 Configuration Manager 的支持，以下载 Office 365 支持的任意语言的更新。

### <a name="download-updates-for-additional-languages-in-version-1902"></a>下载 1902 版中其他语言的更新
<!--3555955-->

从 Configuration Manager 1902 版开始，更新工作流将“Windows 更新”的 38 种语言与“Office 365 客户端更新”的多种其他语言分开。

若要选择必要的语言，请使用以下位置的“语言选择”页面：
- 创建自动部署规则向导
- 部署软件更新向导
- 下载软件更新向导
- 自动部署规则属性

在“语言选择”页上，选择“Office 365 客户端更新”，然后单击“编辑”。 添加 Office 365 的所需语言，然后单击“确定”。

![为 Office 365 添加其他语言的屏幕截图](media/office-update-languages-selection.png)

### <a name="to-add-support-to-download-updates-for-additional-languages-in-version-1810-and-earlier"></a>添加支持以下载 1810 版及更高版本其他语言的更新

对管理中心站点或独立主站点上的软件更新点执行以下过程。

> [!IMPORTANT]  
> 配置其他 Office 365 更新语言是网站范围的设置。 通过执行以下过程添加语言后，将下载这些语言的所有 Office 365 更新，以及在“下载软件更新”或“部署软件更新”向导中的“语言选择”页上选择的语言的所有 Office 365 更新。

1. 从命令提示符处键入 wbemtest，以管理用户身份打开 Windows Management Instrumentation 测试器。
2. 单击“连接”，然后键入 root\sms\site_&lt;siteCode&gt;。
3. 单击“查询”，然后运行下列查询：select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"  
   ![WMI 查询](../media/1-wmiquery.png)
4. 在结果窗格中，双击具有管理中心站点或独立主站点的站点代码的对象。
5. 选择“属性”属性，单击“编辑属性”，然后单击“查看嵌入项”。
   ![属性编辑器](../media/2-propeditor.png)
6. 从第一个查询结果开始，打开每个对象，直到找到 **PropertyName** 属性为 **AdditionalUpdateLanguagesForO365** 的对象。
7. 选择“Value2”，然后单击“编辑属性”。  
   ![编辑 Value2 属性](../media/3-queryresult.png)
8. 向“Value2”属性添加其他语言，然后单击“保存属性”。 <br/> 例如，pt-pt（葡萄牙语 - 葡萄牙）、af-za（南非荷兰语 - 南非），以及 nn-no（挪威尼诺斯克文 - 挪威）等等。可以为示例语言键入 `pt-pt,af-za,nn-no`。 请勿在语言之间使用空格。
 
   ![在“属性编辑器”中添加语言](../media/4-props.png)  
9. 依次单击“关闭”->“关闭”->“保存属性”，然后单击“保存对象”（如果在此处单击“关闭”，值将被丢弃）。 单击“关闭”，然后单击“退出”，退出 Windows Management Instrumentation 测试器。
10. 在 Configuration Manager 控制台中，转到“软件库” > “概述” > “Office 365 客户端管理” > “Office 365 更新”。
11. 现在，如果下载 Office 365 更新，将下载在向导中选择的语言的更新，并在此过程中配置更新。 若要验证是否下载了正确语言的更新，请转到更新的包源，再查找文件名中包含语言代码的文件。  
    ![使用其他语言的文件名](../media/5-verification.png)

## <a name="updating-office-365-proplus-in-a-task-sequence"></a>在任务序列中更新 Office 365 专业增强版
在使用[安装软件更新](https://docs.microsoft.com/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)任务序列步骤来安装 Office 365 更新时，可能会将已部署的更新检测为不适用。  如果计划的 Office 自动更新任务尚未运行至少一次，则可能会出现这种情况（请参阅[部署 Office 365 更新中的说明](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-updates)）。 例如，如果在安装 Office 365 专业增强版后立即运行此步骤，则可能会出现这种情况。

为确保对更新通道进行设置，以便正确检测已部署的更新，请使用以下方法之一：

**方法 1：**
1. 在具有与 Office 365 专业增强版相同版本的计算机上，打开任务计划程序 (taskschd.msc) 并标识 Office 365 自动更新任务。 它通常位于“任务计划程序库” >“Microsoft”>“Office”下。
2. 右键单击自动更新任务，选择“属性”。
3. 转到“操作”选项卡，单击“编辑”。 复制命令和所有参数。 
4. 在 Configuration Manager 控制台中，编辑你的任务序列。
5. 在任务序列中“安装软件更新”步骤的前面添加新的“运行命令行”步骤。 如果将 Office 365 专业增强版作为同一任务序列的一部分安装，请确保在安装 Office 之后运行此步骤。
6. 复制从 Office 自动更新计划任务收集的命令和参数。 
7. 单击" **确定**"。 

**方法 2：**
1. 在具有与 Office 365 专业增强版相同版本的计算机上，打开任务计划程序 (taskschd.msc) 并标识 Office 365 自动更新任务。 它通常位于“任务计划程序库” >“Microsoft”>“Office”下。
2. 在 Configuration Manager 控制台中，编辑你的任务序列。
3. 在任务序列中“安装软件更新”步骤的前面添加新的“运行命令行”步骤。 如果将 Office 365 专业增强版作为同一任务序列的一部分安装，请确保在安装 Office 之后运行此步骤。
4. 在命令行字段中，输入将运行计划的任务的命令行。 请参阅以下示例，确保引号中的字符串与步骤 1 中标识的路径和任务名称相匹配。  

    示例：`schtasks /run /tn "\Microsoft\Office\Office Automatic Updates 2.0"`
5. 单击" **确定**"。 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>在使 Office 365 客户端可从 Configuration Manager 接收更新后更改更新频道
若要在将 Office 365 客户端启用为从 Configuration Manager 接收更新后更改更新频道，请使用组策略向 Office 365 客户端分发注册表项值更改。 更改 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** 注册表项以使用以下值之一：

- 每月频道 <br/>
<i>（以前为当前频道）</i>：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- 半年频道 <br/>
<i>（以前为延期频道）</i>：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- 每月频道(定向)<Br/>
 <i>（以前为当前频道的首次发布）</i>：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- 半年频道(定向) <br/>
<i>（以前为延期频道的首次发布）</i>：  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
<!--the channel names changed in Sept 2017- https://docs.microsoft.com/en-us/DeployOffice/overview-of-update-channels-for-office-365-proplus?ui=en-US&rs=en-US&ad=US-->


<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

## <a name="next-steps"></a>后续步骤

在 Configuration Manager 中使用 Office 365 客户端管理仪表板查看 Office 365 客户端信息并部署 Office 365 应用。 有关详细信息，请参阅 [Office 365 客户端管理仪表板](/sccm/sum/deploy-use/office-365-dashboard)。 --->
