---
title: "使用应用配置策略配置 iOS 应用 | System Center Configuration Manager"
description: "通过在用户运行应用之前向其部署应用配置策略，帮助消除运行 iOS 8 或更高版本的设备上的配置问题。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*适用范围：System Center Configuration Manager (Current Branch)*


使用 System Center Configuration Manager 中的应用配置策略可提供用户在运行应用时可能需要的设置。 例如，应用可能要求用户指定：
- 自定义端口号
- 语言设置
- 安全设置
- 公司徽标之类的品牌设置

如果用户输入的这些设置不正确，可能会加重支持人员的负担并降低新应用的采用率。
通过让你在运行应用之前将策略中的这些设置部署给用户，应用配置策略可消除此类问题。 随后这些设置会自动提供，用户无需执行任何操作。
无需直接向用户和设备部署这些策略， 而是在部署应用程序时，将该策略与部署类型关联。 只要应用检测到策略设置（通常在其首次运行时），即会使用它们。

应用配置策略目前仅在运行 iOS 8 及更高版本的设备上可用，并支持下列应用安装程序类型：

- iOS 应用包（*.ipa 文件）*
- **App Store 中的 iOS 应用包**

有关应用安装类型的详细信息，请参阅[应用程序管理简介](/sccm/apps/understand/introduction-to-application-management)。

## <a name="create-an-app-configuration-policy"></a>创建应用配置策略

1. 在 Configuration Manager 控制台中，单击“软件库” > “应用程序管理” > “应用配置策略”。
3. 在“主页”选项卡上的“应用配置策略”组中，单击“创建新的应用程序配置策略”。
4. 在“创建应用配置策略向导”的“常规”页上，指定以下信息：
    - **名称**：为策略指定唯一名称。
    - **说明**：（可选）指定可帮助你识别该策略的描述。
    - **用以改进搜索和筛选的分配类别**：（可选）单击“类别”以创建和分配策略的类别。 这让你能更轻松地在 Configuration Manager 控制台中对项目进行排序和查找。
5. 在“iOS 策略”页上，选择指定配置策略信息的方式：
    - **指定名称和值对**：可以将此选项用于不使用嵌套的属性列表文件。
    指定名称和值对
        - 若要添加新的对，请单击“新建”。
        - 在“添加名称/值对”对话框中，指定以下内容：
            - **类型**：从列表中，选择要指定的值的类型。
            - **名称**：输入要为其指定值的属性列表键的名称。
            - **值**：输入将应用于所输入的键的值。
        - 浏览到属性列表文件：如果已经有一个应用配置 XML 文件或使用嵌套的更复杂的文件，则使用此选项。
        浏览到属性列表文件
            - 在“应用配置策略”字段中，以正确的 XML 格式输入属性列表信息。
            若要了解有关 XML 属性列表的详细信息，请参阅 iOS 开发人员库中的[了解 XML 属性列表](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)。
            根据你所配置的应用，XML 属性列表的格式可能有所不同。 若需了解要使用确切格式的详细信息，请联系应用供应商。
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
            此外，Intune 支持属性列表中的以下令牌类型：
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

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            还可以单击“选择文件”导入以前创建的 XML 文件。
6. 单击“下一步” 。 如果 XML 代码中存在错误，则必须在继续之前更正这些错误。
6. 完成向导。

新应配置策略显示在“软件库”工作区的“应用配置策略”节点中。

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>将应用配置策略与 Configuration Manager 应用程序关联

若要将应用配置策略与 iOS 应用的部署相关联，可按通常方式使用[部署应用程序](/sccm/apps/deploy-use/deploy-applications)主题中的过程来部署应用程序。
在“部署软件向导”的“应用配置策略”页上，单击“新建”。 然后，在“选择应用配置策略”对话框中，选择应用程序部署类型和要将其与之关联的应用配置策略。
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



<!--HONumber=Nov16_HO1-->


