---
title: "使用应用配置策略配置 iOS 应用 | Microsoft Docs"
description: "通过在用户运行应用之前向其部署应用配置策略，帮助消除运行 iOS 8 或更高版本的设备上的配置问题。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 50aea2afaf34974ca92ac58b6569bff56403a9ab
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中将设置应用于使用应用配置策略的 iOS 应用

*适用范围：System Center Configuration Manager (Current Branch)*


可以使用 System Center Configuration Manager (Configuration Manager) 中的应用配置策略来分发用户运行应用时可能需要的设置。 例如，应用可能要求用户指定以下详细信息：
- 自定义端口号
- 语言设置
- 安全设置
- 公司徽标之类的品牌设置

如果用户设置输入错误，则修复它们的重担将落到支持人员身上，并且应用部署也将变慢。
为了帮助避免这类问题，可以使用应用配置策略在用户运行应用前先部署所需设置。 这些设置自动与用户关联。 用户无需采取任何操作。
若要在 Configuration Manager 中使用应用配置策略，而非将配置策略直接部署到用户和设备，请在部署应用时将策略与部署类型关联。 每当应用检查是否存在策略设置时（通常是应用首次运行时），便应用这些策略设置。

应用配置策略目前仅在运行 iOS 8 及更高版本的设备上可用，并且可用于下列应用程序类型：

- **iOS 应用程序包（*.ipa 文件）**
- **App Store 中的 iOS 应用程序包**

有关应用安装类型的详细信息，请参阅[应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。

## <a name="create-an-app-configuration-policy"></a>创建应用配置策略

1. 在 Configuration Manager 控制台中，选择“软件库” > “应用程序管理” > “应用配置策略”。
2. 在“主页”选项卡的“应用配置策略”组中，选择“创建新的应用程序配置策略”。
3. 在“创建应用配置策略”向导的“常规”页上，设置此策略信息：
  - **名称**。 输入策略的唯一名称。
  - **说明**。 （可选）为了便于轻松识别策略，可以添加说明。
  - **分配类别以改进搜索和筛选**。 （可选）若要对策略创建和分配类别，选择“类别”。 类别可以方便用户在 Configuration Manager 控制台中对项目进行排序和查找。
4. 在“iOS 策略”页上，选择设置配置策略信息的方式：
  - **指定名称和值对**。 可以将此选项用于不使用嵌套的属性列表文件。

      指定名称和值对
        1. 若要添加新的值对，请选择“新建”。
        2. 在“添加名称/值对”对话框中，指定以下内容：
            - **类型**。 从列表中，选择要指定的值的类型。
            - **名称**。 输入要为其指定值的属性列表键的名称。
            - **值**。 输入将应用于所输入的键的值。

  - **浏览到属性列表文件**。 如果已经有一个应用配置 XML 文件或使用嵌套的更复杂的文件，使用此选项。

    *浏览到属性列表文件*

      1.  在“应用配置策略”字段中，以正确的 XML 格式输入属性列表信息。

      若要了解有关 XML 属性列表的详细信息，请参阅 iOS 开发人员库中的[了解 XML 属性列表](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)。

根据你所配置的应用，XML 属性列表的格式可能有所不同。 如需了解要使用格式的详细信息，请联系应用供应商。
Intune 支持属性列表中的以下数据类型：
            
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
有关数据类型的详细信息，请参阅 iOS 开发人员库中的[关于属性列表](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html)。
Intune 还支持属性列表中的以下令牌类型：
            
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices
            ```

{{ 和 }} 字符仅供令牌类型使用，且不能用于其他目的。
            
5. 若要导入以前创建的 XML 文件，请选择“选择文件”。
6. 选择“下一步”。 如果 XML 代码中存在错误，则必须在继续之前更正这些错误。
7. 完成向导中的步骤。

新应配置策略显示在“软件库”工作区的“应用配置策略”节点中。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>将应用配置策略与 Configuration Manager 应用程序关联

若要将应用配置策略与 iOS 应用的部署相关联，可按通常方式使用[部署应用程序](/sccm/apps/deploy-use/deploy-applications)主题中的过程来部署应用程序。

在“部署软件向导”的“应用配置策略”页上，选择“新建”。 在“选择应用配置策略”对话框中，选择应用程序部署类型和要将其与之关联的应用配置策略。
安装部署类型后，应用配置策略设置将自动应用。

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>移动应用配置 XML 文件的示例格式

创建移动应用配置文件时，可以使用此格式指定一个或多个以下值：

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```
