---
title: "Technical Preview 1702 Configuration Manager 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1702 版中的可用功能。"
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3bdbcd1a3c64a1d50f2f6219b2a5e17d60979864
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1702 中的功能

*适用范围：System Center Configuration Manager (Technical Preview)*

本文介绍了 System Center Configuration Manager Technical Preview（版本 1702）中的可用功能。 可以安装此版本以更新 Configuration Manager Technical Preview 站点的功能并向其添加新功能。 在安装此版本的 Technical Preview 前，请查看介绍性主题 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用 Technical Preview 的常规要求和限制、如何在版本之间进行更新，以及如何提供关于 Technical Preview 中的功能的反馈。    


**以下是可以试用的此版本的新功能。**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>从 Configuration Manager 控制台发送反馈

此预览版在 Configuration Manager 控制台中引入了新反馈选项。 借助“反馈”选项，可通过 Configuration Manager UserVoice 反馈网站直接向开发团队发送反馈。  

>可在以下位置找到“反馈”选项：
-  在功能区中每个节点的“主页”选项卡的最左侧。  
   ![功能区](./media/feedback-home.png)

-  右键单击控制台中的任何对象时。   
    ![右键单击选项](./media/feedback-option.png)   

选择“反馈”可打开浏览器并转到 Configuration Manager UserVoice 反馈网站，网址为：https://configurationmanager.uservoice.com/forums/300492-ideas。
##  <a name="changes-for-updates-and-servicing"></a>更新和维护服务的更改
以下是此预览版引入的功能。

**简化更新选项**  
下次当你的基础架构有资格下载两个或多个更新时，将仅下载最新更新。 例如，如果当前站点版本比最新可用版本低两个或更多版本，将仅自动下载最新版本的更新。  

仍可选择下载并安装其他可用更新，即使它们不是最新版本。 但是，你将收到此更新已由较新更新替换的警告。 若要下载可下载的更新，在控制台中选择更新，然后单击“下载”。

**针对较旧更新的清理功能得到改进**   
已添加自动清理功能，可从站点服务器上的“EasySetupPayload”文件夹中删除不需要的下载文件。  


## <a name="peer-cache-improvements"></a>对等缓存功能改进
从此版本开始，当对等缓存源计算机满足以下任一条件时，对等缓存源计算机将拒绝对内容的请求：  
 -  处于低电量模式。
 -  请求内容时 CPU 负载超过 80%。
 -  磁盘 I/O 的 AvgDiskQueueLength 超过 10。
 -  该计算机没有其他可用连接。   

使用 System Center Configuration Manager SDK 时，可以使用对等源功能的客户端代理配置类 (*SMS_WinPEPeerCacheConfig*) 配置这些设置。

如果计算机拒绝对内容的请求，请求计算机会继续在其可用内容源位置池中的备用源中搜索内容。   

## <a name="azurediscovery"></a>使用 Azure Active Directory 域服务管理设备、用户和组

借助此技术预览版，可以管理加入 Azure Active Directory (AD) 域服务托管域的设备。 还可使用各种 Configuration Manager 发现方法发现域中的设备、用户和组。

技术预览版站点基础结构、客户端和 Azure AD 域服务域必须均在 Azure 中运行。


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>设置 Configuration Manager 以便使用 Azure AD
若要将 Azure AD 与 Configuration Manager 配合使用，将需要以下项：
-   Azure 订阅。
-   包含域服务 (DS) 的 Azure AD。
-   在加入到 Azure AD 的 Azure VM 上运行的 Configuration Manager 站点。
-   在同一 Azure AD 环境中运行的 Configuration Manager 客户端。

若要配置 Azure AD 域服务，请参阅 [Azure AD 域服务入门](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started)。

### <a name="discover-resources"></a>发现资源
设置 Configuration Manager 以在 Azure AD 中运行后，可以使用以下 Active Directory 发现方法搜索 Azure AD 寻找资源：  
- Active Directory 系统发现
- Active Directory 用户发现
- Active Directory 组发现  

对于使用的每种方法，请编辑 LDAP 查询以搜索 Azure AD OU 结构，而不是本地 Active Directory 常用的容器。 这要求你对查询作出指示，让其在 Azure 订阅中搜索 Active Directory。  

下面的示例使用 contoso.onmicrosoft.com 的 Azure AD：
 - **系统发现**   
Azure AD 将设备存储在 **AADDC 计算机** OU 下。  进行下列配置：  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **用户发现** AAD 将用户存储于 **AADDC 用户** OU 下。  进行下列配置：
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **组发现**  
Azure AD 没有存储组的 OU。 将同一常规结构用作系统或用户查询并配置 LDAP 查询，以指向包含想要发现的组的 OU。

有关 Azure AD 的详细信息，请参阅以下内容：  
 - azure.microsoft.com 上的 [Azure Active Directory 域服务](https://azure.microsoft.com/en-us/services/active-directory-ds)。
 - docs.microsoft.com 上的 [Active Directory 域服务文档](https://docs.microsoft.com/azure/active-directory-domain-services)。

## <a name="conditional-access-device-compliance-policy-improvements"></a>条件性访问设备符合性策略改进

当用户使用非符合性应用列表中的应用时，新的设备符合性策略规则可用于帮助阻止对支持条件性访问的公司资源的访问。 当添加新的符合性规则“无法安装的应用”时，可由管理员定义非符合性应用列表。 将应用添加到非符合性列表时，此规则要求管理员输入“应用名称”、“应用 ID”和“应用发布者”（可选）。 此设置仅适用于 iOS 和 Android 设备。

此外，这可帮助组织缓解使用不安全应用导致的数据泄漏，并防止通过某些应用过度使用数据。

- 深入了解[设备符合性策略的工作原理](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies)。
- 深入了解[如何创建设备符合性策略](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy)。

### <a name="try-it-out"></a>试试看

**方案：**识别可能通过将公司数据发送到公司外导致数据泄漏的应用或识别导致数据过度使用的应用，然后[创建条件性访问设备符合性策略](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy)，将这些应用添加到不符合的应用列表中。 在用户删除已阻止的应用前，这将阻止访问支持条件性访问的公司资源。

## <a name="antimalware-client-version-alert"></a>反恶意软件客户端版本警报
从此预览版开始，如果超过 20%（默认值）托管客户端使用反恶意软件客户端（即 Windows Defender 或 Endpoint Protection 客户端）的过期版本，Configuration Manager Endpoint Protection 将发出警报。

### <a name="try-it-out"></a>试试看
确保使用客户端设置策略的所有桌面和服务器客户端上均已启用 Endpoint Protection。 现在，可通过转到“资产和符合性” > “概述” > “设备” > “所有桌面和服务器客户端”来查看“反恶意软件客户端版本”和“Endpoint Protection 部署状态”。 若要查看警报，请在“监视”工作区中查看“警报”。 如果超过 20% 托管客户端运行反恶意软件的过期版本，将显示“反恶意软件客户端版本已过期”警报。 此警报不会出现在“监视” > “概述”选项卡中。 若要更新过期的反恶意软件客户端，可启用反恶意软件客户端的软件更新。

若要配置生成警报的百分比，请展开“监视” > “警报” > “所有警报”，双击“反恶意软件客户端已过期”，然后修改“如果具有过期版本的反恶意软件客户端的托管客户端百分比超过以下值，发出警报”选项。

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Windows Update for Business 更新的符合性评估
现在，可以配置符合性策略更新规则，将 Windows Update for Business 评估结果包含在条件性访问评估中。
> [!IMPORTANT]
> 必须拥有 Windows 10 Insider Preview 版本 15019 或更高版本，才能使用 Windows Update for Business 更新的符合性评估。

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>允许 Windows Update for Business 管理 Windows 10 更新
若要收集 Windows Update for Business 更新的符合性评估信息，请按照以下步骤配置客户端代理设置，以显式允许 Windows Update for Business 管理 Windows 10 更新。
1. 在 Configuration Manager 控制台中，转到“管理” > “客户端设置”。
2. 在客户端设置的属性中，请转至“软件更新”，然后对“使用 Windows Update for Business 管理 Windows 10 更新”设置选择“是”。

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>创建 Windows Update for Business 评估的符合性策略
1. 在 Configuration Manager 控制台中，转到“资产和符合性” > “符合性设置” > “符合性策略”。
2. 单击“创建符合性策略”或选择现有的符合性策略进行修改。
3. 在“常规”页上提供名称和说明，选择“使用 Configuration Manager 客户端管理的设备的符合性规则”，设置用于报告的不符合性严重程度，然后单击“下一步”。
4. 在“支持的平台”页上，选择“Windows 10”，然后单击“下一步”。
5. 在“规则”页上，单击“新建...”，然后对“条件”选择“需要 Windows Update for Business 符合性”。 “值”设置自动设置为“true”。

新的策略将在  “资产和符合性”工作区的  “符合性策略”节点处显示。

### <a name="deploy-a-compliance-policy"></a>部署合规性策略
1. 在 Configuration Manager 控制台中，转到“资产和符合性” > “符合性设置”然后单击“符合性策略”。
2. 在“主页”  选项卡上的“部署”  组中，单击“部署” 。
3. 在“部署符合性策略”  对话框中，单击  “浏览”以选择要将策略部署到的用户集合。
   此外，当策略不合规时可以选择选项以生成警报，还可配置将按其评估策略符合性的计划。
4. 完成后，请单击“确定” 。

### <a name="monitor-the-compliance-policy"></a>监视合规性策略
创建符合性策略后，可以在 Configuration Manager 控制台中监视符合性结果。 有关详细信息，请参阅[监视合规性策略](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)。


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>针对影响重大的任务序列，改进软件中心设置和消息通知
本版本包括针对影响重大的任务序列，对软件中心设置和通知消息进行的以下改进：

- 在任务序列的属性中，现可将任何任务序列（包括非操作系统任务序列）配置为高风险部署。 任何符合特定条件的任务序列都将自动定义为“影响重大”。 有关详细信息，请参阅[管理高风险部署](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments)。
- 在任务序列的属性中，可以选择针对影响重大的部署，使用默认通知消息或创建自定义通知消息。
- 在任务序列的属性中，可以配置软件中心属性，其中包括设置必要的重启、任务序列的下载大小和预计运行时间。
- 对于就地升级，默认的重大影响部署消息指示你的应用、数据和设置将自动迁移。 以前，任何操作系统安装的默认消息均指示所有应用、数据和设置将丢失，但这样的消息实际上并不适用于就地升级。

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>将任务序列设置为影响重大的任务序列
使用下列过程将任务序列设置为“影响重大”。
> [!NOTE]
> 任何符合特定条件的任务序列都将自动定义为“影响重大”。 有关详细信息，请参阅[管理高风险部署](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments)。

1. 在 Configuration Manager 控制台中，转到“软件库” > “操作系统” > “任务序列”。
2. 选择要编辑的任务序列，然后单击“属性”。
3. 在“用户通知”选项卡上，选择“这是影响重大的任务序列”。

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>创建高风险部署的自定义通知
1. 在 Configuration Manager 控制台中，转到“软件库” > “操作系统” > “任务序列”。
2. 选择要编辑的任务序列，然后单击“属性”。
3. 在“用户通知”选项卡上，选择“使用自定义文本”。
>  [!NOTE]
>  只能在已选择“这是影响重大的任务序列”时设置用户通知文本。

4. 配置下列设置（每个文本框最多 255 个字符）：

   **用户通知标题文本**：指定在软件中心用户通知上显示的蓝色文本。 例如，在默认用户通知中，本部分包含类似“确认想要升级此计算机上的操作系统”的内容。

   **用户通知消息文本**：三个文本框提供自定义通知的正文。
   - 第一个文本框：指定文本的主要正文，通常包含针对用户的说明。 例如，在默认用户通知中，本部分包含类似“操作系统升级可能需要一些时间，并且计算机可能会多次重启”的内容。
   - 第二个文本框：指定文本主要正文下的粗体文本。 例如，在默认用户通知中，本部分包含类似“此就地升级将安装新的操作系统并自动迁移你的应用、数据和设置”的内容。
   - 第三个文本框：指定粗体文本下的最后一行文本。 例如，在默认用户通知中，本部分包含类似“单击‘安装’以开始。 否则，单击‘取消’”的内容。   

   假设在属性中配置以下自定义通知。

   ![任务序列的的自定义通知](.\media\user-notification.png)

   当最终用户从软件中心打开安装时，将显示以下通知消息。

   ![任务序列的的自定义通知](.\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>配置软件中心属性
使用以下过程配置软件中心中显示的任务序列的详细信息。 这些详细信息仅供参考。  
1. 在 Configuration Manager 控制台中，转到“软件库” > “操作系统” > “任务序列”。
2. 选择要编辑的任务序列，然后单击“属性”。
3. 在“常规”选项卡上，可使用软件中心的以下设置：
  - **需要重启**：让用户了解安装期间是否需要重新启动。
  - **下载大小(MB)**：指定任务序列在软件中心中显示多少兆字节。  
  - **预计运行时间(分钟)**：指定任务序列在软件中心中显示的预计运行时间（以分钟为单位）。


## <a name="check-for-running-executable-files-before-installing-an-application"></a>在安装应用程序之前检查运行的可执行文件

在部署类型的*<deployment type name>*“属性”对话框中的“安装行为”选项卡中，现在可以指定一个或多个可执行文件，如果运行此类文件，将阻止安装部署类型。 用户必须先关闭运行中的可执行文件（或者因为部署的特定要求而自动关闭），然后才能安装部署类型。

### <a name="try-it-out"></a>试试看。

1.  在 Configuration Manager 部署类型的属性中，选择“安装行为”选项卡。
2.  选择“添加”可添加要查看的一个或多个可执行文件名称。 还可以添加显示名称，以便用户轻松识别列表中的应用程序。
3.  如果部署是必需的，在部署软件向导中，可以选择自动关闭在“部署类型属性”对话框的“安装行为”选项卡中指定的任何运行中的可执行文件。

如果应用程序已部署为“可用”，最终用户尝试安装应用程序时，系统会提示其先关闭指定的任何运行中的可执行文件，然后才能继续安装。

如果应用程序已部署为“必需”，且已选择“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何运行中的可执行文件”选项，他们将看到一个对话框，通知他们在应用程序安装截止时间到达时将自动关闭指定的可执行文件。 可在“客户端设置” > “计算机代理”中计划这些对话框。 如果不希望最终用户看到这些消息，请选择部署属性的“用户体验”选项卡上的“在软件中心和所有通知中隐藏”。

如果应用程序已部署为“必需”，且未选择“自动关闭在‘部署类型属性’对话框中的‘安装行为’选项卡中指定的任何运行中的可执行文件”选项，如果一个或多个指定的应用程序在运行中，则应用安装将失败。

## <a name="create-pfx-certificates-with-s-mime-support"></a>创建具有 S MIME 支持的 PFX 证书

现在，可以创建支持 S/MIME 的 PFX 证书配置文件，并将其部署到用户。  然后这些证书可以用于用户已注册设备中的 S/MIME 加密和解密。

此外，现在还可对多个证书注册点站点系统角色指定多个证书颁发机构 (CA)，然后分配哪些 CA 处理证书配置文件中的请求。

对于 iOS 设备，可以将 PFX 证书配置文件与电子邮件配置文件相关联，然后启用 S/MIME 加密。  然后在 iOS 的本机电子邮件客户端中启用 S/MIME，并将正确的 S/MIME 加密证书与其关联。

有关 Configuration Manager 中的证书的详细信息，请参阅 [System Center Configuration Manager 中的证书配置文件简介]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles)。


## <a name="new-compliance-settings-for-ios-devices"></a>iOS 设备的新符合性设置

我们添加了许多新设置，可以用于 iOS 设备的配置项目中。 这些设置之前存在于 Microsoft Intune 的独立配置中，现在结合使用 Intune 和 Configuration Manager 时可以使用这些设置。 如果需要有关这些设置的帮助，请参阅 [Microsoft Intune 中的 iOS 策略设置](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune)。

- **将数据从托管应用同步到 iCloud**
- **提交以继续其他设备上的活动**
- **iCloud 照片共享**
- **iCloud 照片库**
- **信任新的企业应用作者**
- **允许用户从 iBook 商店下载标记为“成人”的内容**（仅限监督模式下）
- **强制配对 Apple Watch，以使用手腕检测**
- **AirPlay 传出请求的密码**
- **修改帐户设置**（仅限监督模式下）
- **对应用手机网络数据使用情况设置的更改**（仅限监督模式下）
- **清除所有内容和设置**（仅限监督模式下）
- **配置设备的限制**（仅限监督模式下）
- **使用主机配对来控制可与 iOS 设备配对的设备**（仅限监督模式下）
- **安装配置文件和证书**（仅限监督模式下）
- **修改设备名称**（仅限监督模式下）
- **修改密码**（仅限监督模式下）
- **Apple Watch 配对**（仅限监督模式下）
- **修改通知设置**（仅限监督模式下）
- **修改壁纸**（仅限监督模式下）
- **修改诊断提交设置**（仅限监督模式下）
- **修改蓝牙**（仅限监督模式下）
- **AirDrop**（仅限监督模式下）
- **使用 Siri 从 Internet 查询用户生成的内容**（仅限监督模式下）
- **Siri 猥亵内容筛选器**（仅限监督模式下）
- **在 Spotlight 搜索中返回来自 Internet 的结果**（仅限监督模式下）
- **查找词语定义**（仅限监督模式下）
- **预测键盘**（仅限监督模式下）
- **自动更正**（仅限监督模式下）
- **键盘拼写检查**（仅限监督模式下）
- **键盘快捷方式**（仅限监督模式下）
<!--- - **Enterprise app trust settings modification** --->
- **仅使用 Apple Configurator 和 iTunes 安装应用**（仅限监督模式下）
- **自动下载应用**（仅限监督模式下）
- **更改“查找我的朋友”应用设置**（仅限监督模式下）
- **访问 iBooks 商店**（仅限监督模式下）
- **“邮件”应用**（仅限监督模式下）
- **播客**（仅限监督模式下）
- **Apple 音乐**（仅限监督模式下）
- **iTunes Radio**（仅限监督模式下）
- **Apple 新闻**（仅限监督模式下）
- **Game Center**（仅限监督模式下）
- **将 AirDrop 视为非托管目标**

## <a name="android-for-work-support"></a>Android for Work 支持

从技术预览版 1702 开始，可以将 Google 帐户绑定到混合 MDM 租户。 用户从而可以执行以下操作：

- 将[支持的 Android 设备](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)注册为 Android for Work，在这些已注册的设备上创建工作配置文件
- 在 Play for Work 应用商店中批准应用，将其与 Configuration Manager 控制台同步，然后将其部署到设备的工作配置文件中
- 创建和部署配置项以配置这些设备的工作配置文件和密码设置
- 创建和部署 Android for Work 设备的符合性策略项和资源访问配置文件，正如你已对 Android 设备采取的操作一样
- 在 Android for Work 设备上执行选择性擦除

将设备注册为 Android for Work 设备时，将在 Intune 可以管理的设备上创建工作配置文件。 此工作配置文件与 Android 设备上的个人配置文件并行存在。 用户可以在工作配置文件应用和个人配置文件应用间轻松切换。 无法在个人配置文件中管理项目。 个人应用和数据保持非托管状态。 Configuration Manager 可以完全控制工作配置文件及其内容，并可以从设备中将其删除。

Android for Work 是独立于 Android 的平台，你需要决定对支持工作配置文件的 Android 设备使用哪种管理形式。

### <a name="try-it-out"></a>试试看！
以下各节介绍 Android for Work 管理。

#### <a name="enable-android-for-work-management"></a>启用 Android for Work 管理
1. 在 https://accounts.google.com/SignUp 创建 Google 帐户，作为 Android for Work 管理员帐户，并将其与此 Intune 租户的 Android for Work 管理任务相关联。 可以是在管理 Android 设备的管理员中共享的 Google 帐户。 组织使用此 Google 帐户，在 Play for Work 控制台中管理和发布应用。 此帐户将用于在 Play for Work 应用商店中批准应用，因此请记录帐户名和密码。
2. 通过将 Google 帐户绑定到在 Configuration Manager 中托管的 Intune 租户来启用 Android 注册：
  1. 转到“管理” > “概述” > “云服务” > “Microsoft Intune 订阅”，然后选择 Intune 订阅。
  2. 在功能区中，单击“配置平台” > “Android”，并确保已选中“启用 Android 注册”。
  3. 在功能区中，单击“配置平台” > “Android for Work”。
  4. 在对话框中，单击“在 Intune 控制台中配置 Android for Work”。 Intune 控制台将在 Web 浏览器中打开。
  5. 使用你的 Intune 管理员凭据登录 Intune 门户。
  6. 单击“配置”，打开 Google Play 的 Android for Work 网站。
  7. 在 Google 登录页上，输入步骤 1 中的 Google 帐户凭据，然后提供你的公司信息。
3. 返回 Intune 门户时，Android for Work 已启用，Android for Work 设备有三个注册选项：
  - **将所有设备作为 Android 设备管理** -（已禁用）所有 Android 设备（包括支持 Android for Work 的设备）均将注册为传统的 Android 设备
  - **将受支持设备作为 Android for Work 设备管理** -（已启用）将支持 Android for Work 的所有设备均注册为 Android for Work 设备。 任何不支持 Android for Work 的 Android 设备均将注册为传统的 Android 设备。
  - **仅针对这些组中的用户将受支持设备作为 Android for Work 设备管理** -（测试中）可使 Android for Work 管理面向有限的一组用户。 只有注册支持 Android for Work 的设备的所选组的成员能注册为 Android for Work 设备。 其他所有成员均注册为 Android 设备。
  
> [!NOTE]
> 一个已知的问题将阻止“仅为这些组中的用户将受支持设备作为 Android for Work 设备管理”选项按预期方式正常运行。 指定 Azure AD 组中的用户设备将注册为 Android 而不是 Android for Work。 若要测试 Android for Work，必须使用“将所有受支持设备作为 Android for Work 管理”。


  若要启用 Android for Work 注册，必须选择底部的两个选择之一。 “仅为这些组中的用户将受支持设备作为 Android for Work 设备管理”选项要求首先设置 Azure Active Directory 安全组。

完成绑定后，将在 Intune 门户中看到帐户名和组织名称；此时，可关闭两个浏览器。

#### <a name="approve-and-deploy-android-for-work-apps"></a>批准和部署 Android for Work 应用
使用以下步骤在 Play for Work 应用商店中批准应用，将其同步到 Configuration Manager 控制台，然后将其部署到托管的 Android for Work 设备中。 若要将应用部署到用户的工作配置文件中，需要在 Play for Work 中批准该应用，然后将应用与 Configuration Manager 控制台同步。

1. 打开浏览器并转到：https://play.google.com/work。
2. 使用绑定到你的 Intune 租户的 Google 管理员帐户登录。
3. 浏览要在你的环境中部署的应用，然后对每个应用单击“批准”。
4. 在 Configuration Manager 控制台中，转到“管理员” > “概述” > “云服务” > “Android for Work”，然后单击“同步”。
5. 等待应用同步（最多 10 分钟），然后转到“软件库” > “概述” > “应用程序管理” > “应用商店应用的许可证信息”。
6. 单击从 Play for Work 同步的应用，然后单击“创建应用程序”。
7. 完成该向导，然后单击“关闭”。
8. 转到“软件库” > “概述” > “应用程序管理” > “应用程序”，选择 Android for Work 应用，然后照常部署。

若要将 Play for Work 应用与 Configuration Manager 同步，必须在 Play for Work 网站上至少批准一个应用。

#### <a name="enroll-an-android-for-work-device"></a>注册 Android for Work 设备
注册 Android for Work 设备的方式类似于注册 Android 设备。 在移动设备上下载并运行适用于 Android 的公司门户应用。 注册过程中将提示你创建工作配置文件。  创建工作配置文件后，必须切换到公司门户的托管版本。 托管的公司门户的右下角具有小型橙色公文包标记。

#### <a name="create-and-deploy-a-configuration-item"></a>创建和部署配置项
Android for Work 具有配置项的两个设置组：
- Password
- 工作配置文件

可以配置在工作配置文件间共享的内容，也可以配置运行 Android 6 或更高版本的设备上的以下配置项：
- 应用请求特定权限的行为
- 工作配置文件内的应用程序的通知是否在锁定屏幕上可见

若要尝试此操作，可通过标准的工作流创建配置项，在“常规”页上选择“Android for Work”，并为每个设置组配置设置，将配置项添加到基线，然后照常部署。 这些设置仅适用于注册为 Android for Work 的设备，不适用于注册为 Android 的设备。

#### <a name="perform-selective-wipe"></a>执行选择性擦除
只能选择性擦除注册为 Android for Work 的设备，因为你只管理工作配置文件。 这可防止擦除个人配置文件。 在 Android for Work 设备上执行选择性擦除将删除工作配置文件（包括所有应用和数据）并注销设备。

若要选择性擦除 Android for Work 设备，请在 Configuration Manager 控制台中使用[选择性擦除过程](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)。

#### <a name="known-issues-for-android-for-work"></a>Android for Work 的已知问题
**在 Android for Work 电子邮件配置文件中配置同步计划将导致无法部署它们**：Android for Work 电子邮件配置文件的 ConfigMgr UI 中的其中一个选项就是“计划”。 在其他平台上，这将使管理员可以配置一个计划，以将电子邮件和其他电子邮件帐户数据同步到移动设备（计划将被部署到该移动设备）。 但是，它不适用于 Android for Work 电子邮件配置文件，并选择“未配置”之外的任何选项将导致配置文件不会部署到任何设备。
