---
title: "预声明具有 IMEI 或 iOS 序列号的设备 | Microsoft Docs"
description: "预声明具有 IMEI 或 iOS 序列号的公司拥有的设备。"
ms.custom: na
ms.date: 08/15/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: "3"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 7d139a2c74c0f29604f2f3d9b8e2739364633f17
ms.sourcegitcommit: db7b7ec347638efd05cdba474e8a8f8535516116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2017
---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>预声明具有 IMEI 或 iOS 序列号的设备

*适用范围：System Center Configuration Manager (Current Branch)*

可通过导入公司拥有设备的国际移动设备识别 (IMEI) 码或 iOS 序列号对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。  导入的信息将设置在设备列表中注册为“公司”的设备的“所有权”。 访问该服务的每位用户仍需要 Intune 许可证。  

为公司拥有的 iOS 设备上载序列号时，它们必须与公司注册配置文件成对使用。 然后，必须使用 Apple 的设备注册程序 (DEP) 或 Apple 配置器注册这些设备，以使其显示为公司所有。

>[!NOTE]
>Android 设备（不包括 Samsung Knox Standard 设备）必须有 SIM 卡，才能通过 IMEI 号码预声明并注册为公司拥有的设备。

## <a name="how-to-predeclare-corporate-owned-devices"></a>如何预声明公司拥有的设备

1.  在 Configuration Manager 控制台中，转至“资产和符合性” > “概述” > “所有公司拥有的设备” > “预声明设备”。

2.  单击“创建预声明的设备”。 将打开“创建预声明设备”向导。

3.  选择添加设备信息的方式：

     -  **上传包含 IMEI 或序列号和详细信息的 CSV 文件**

        对于此选项，单击“浏览”，指定包含信息的 .csv 文件，以预声明公司拥有的设备。 .csv 文件格式必须正确。 有关详细信息，请参阅[上传的 .csv 文件的格式](#format-for-uploading-csv-files)。

     -  **手动添加 IMEI 或序列号和详细信息**

        若要手动输入信息，请键入 IMEI 号码或 iOS 序列号和设备的详细信息。 在继续操作前请更正所有错误或警告。

    单击“下一步” 。

4. 如果已上传 .csv 文件，查看文件导入的结果。 如果之前已导入设备编号，Configuration Manager 将显示这些设备和替换**详细信息**。 选择希望重写其详细信息的设备。 设备详细信息只能通过重新导入设备标识或序列号来修改。

  如果选择手动输入编号，请填写要预声明的设备表单。

  单击 **“下一步”** 以继续。

4. 如果列表中包含 iOS 序列号，请从提供的配置文件列表中选择“待分配的注册配置文件”，然后单击“下一步”。

5. 单击“下一步”查看详细信息，然后再次单击“下一步”上传数据。

6. 单击“关闭”完成操作。

## <a name="format-for-uploading-csv-files"></a>上传的 .csv 文件的格式

用于通过 IMEI 或 iOS 序列号来标识设备的 .csv 文件必须具有以下格式（仅用于提供指导的顶行除外）。 每一行都必须包含 ID 号，即 IMEI 号码或 iOS 序列号。 对于 iOS 设备，可以包括这两者。 IMEI 号码可用于 Android、iOS 和 Windows 设备。 此表格包含示例数据：

| IMEI 编号  | iOS 序列号  | 操作系统 | 详细信息 |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | 公司拥有的 Windows 设备|
|   | A1B2C3D4E5C6 | IOS |  公司拥有的 iOS 设备|
| 223456789012345 | E6D5C4B3A210 |   IOS |  另一台 iOS 设备|
| 323456789012345 |        |   IOS |    第三台 iOS 设备|
| 123456789012346 |         |   ANDROID |   公司拥有的 Android 设备|

.Csv 文件中不能包含标题行。 以下示例显示 CSV 格式的相同示例数据：

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

.csv 文件中的列支持以下值：

| 列 1 | 列 2 | 列 3 | 第 4 列 |
|---|---|---|---|
|不含空格的 IMEI 号码 | iOS 序列号 | IOS、WINDOWS 或 ANDROID | 可选设备详细信息（不超过 1024 个字符） |
